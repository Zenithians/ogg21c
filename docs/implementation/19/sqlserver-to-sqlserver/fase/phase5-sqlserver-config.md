---
icon: fontawesome/solid/sliders
---

# Konfigurasi SQL Server untuk OGG

## Aktifkan SQL Server Agent

Di SSMS → **Object Explorer** → **SQL Server Agent** → klik kanan → **Start**

Pastikan statusnya **Running** (ikon hijau).

!!! warning "SQL Server Agent Wajib"
    CDC Cleanup job membutuhkan SQL Server Agent dalam kondisi Running. Jika Agent tidak aktif, cleanup job tidak akan berjalan.

## Buat Login & Aktifkan Mixed Mode Authentication

```sql
USE master;

-- Aktifkan Mixed Mode Authentication
EXEC xp_instance_regwrite
    N'HKEY_LOCAL_MACHINE',
    N'Software\Microsoft\MSSQLServer\MSSQLServer',
    N'LoginMode', REG_DWORD, 2;

-- Buat login ggadmin
CREATE LOGIN ggadmin
    WITH PASSWORD = 'OGGAdmin123!',
    DEFAULT_DATABASE = PROD2,
    CHECK_EXPIRATION = OFF,
    CHECK_POLICY = OFF;

EXEC sp_addsrvrolemember 'ggadmin', 'sysadmin';
```

!!! warning "Restart SQL Server"
    Setelah mengaktifkan Mixed Mode, **restart SQL Server** agar perubahan authentication mode berlaku.

## Setup User & Schema

```sql
-- Setup di database PROD2 (Source)
USE PROD2;
CREATE USER ggadmin FOR LOGIN ggadmin;
EXEC sp_addrolemember 'db_owner', 'ggadmin';
CREATE SCHEMA ggadmin;

-- Setup di database DRC (Target)
USE DRC;
CREATE USER ggadmin FOR LOGIN ggadmin;
EXEC sp_addrolemember 'db_owner', 'ggadmin';
CREATE SCHEMA ggadmin;
```

## Aktifkan CDC (Change Data Capture)

```sql
-- Set recovery model ke FULL (wajib untuk CDC)
USE master;
ALTER DATABASE PROD2 SET RECOVERY FULL;

-- Aktifkan CDC pada database PROD2
USE PROD2;
EXEC sys.sp_cdc_enable_db;
EXEC sys.sp_cdc_add_job @job_type = N'capture';
EXEC sys.sp_cdc_add_job @job_type = N'cleanup';

-- Aktifkan CDC pada tabel employees
EXEC sys.sp_cdc_enable_table
    @source_schema = N'dbo',
    @source_name   = N'employees',
    @role_name     = NULL,
    @supports_net_changes = 1;

-- Verifikasi CDC aktif
SELECT name, is_cdc_enabled
FROM sys.databases
WHERE name = 'PROD2';

SELECT name, is_tracked_by_cdc
FROM sys.tables
WHERE name = 'employees';
```

!!! success "Verifikasi"
    Kolom `is_cdc_enabled` harus bernilai `1` untuk database PROD2, dan `is_tracked_by_cdc` harus `1` untuk tabel `employees`.

## Install OGG CDC Cleanup Job

Jalankan di **CMD as Administrator**:

```cmd
cd C:\OGG\source

sqlcmd -S DESKTOP-MVMVJSO\MSQL2019 -U ggadmin -P "OGGAdmin123!" -C -d PROD2 ^
  -v ggschema="ggadmin" -v retention_minutes="4320" ^
  -v threshold="5000" -v freq_minutes="10" ^
  -i ogg_create_cdc_cleanup_job.sql
```

Verifikasi job berhasil dibuat:

```cmd
sqlcmd -S DESKTOP-MVMVJSO\MSQL2019 -U ggadmin -P "OGGAdmin123!" -C -d PROD2 ^
  -Q "SELECT job_id, name FROM msdb.dbo.sysjobs WHERE name LIKE '%OracleGG%'"
```

!!! success "Hasil yang Diharapkan"
    Harus muncul satu baris job dengan nama mengandung `OracleGG`.
