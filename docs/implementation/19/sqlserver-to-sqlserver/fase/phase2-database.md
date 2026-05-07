# Setup Database PROD2 & DRC

## Buat Database

Jalankan query berikut di SSMS:

```sql
CREATE DATABASE PROD2;

CREATE DATABASE DRC;

-- Verifikasi
SELECT name, database_id
FROM sys.databases
WHERE name IN ('PROD2', 'DRC');
```

## Buat Tabel di PROD2 (Source)

```sql
USE PROD2;

CREATE TABLE dbo.employees (
    id          INT IDENTITY(1,1) PRIMARY KEY,
    name        VARCHAR(100),
    department  VARCHAR(50),
    salary      DECIMAL(10,2),
    created_at  DATETIME DEFAULT GETDATE()
);

-- Insert data awal
INSERT INTO dbo.employees (name, department, salary)
VALUES
    ('Rafi',  'IT',      8500000),
    ('Gaby',  'Finance', 7200000),
    ('Rio',   'HR',      6800000);

-- Verifikasi
SELECT * FROM dbo.employees;
```

## Buat Tabel di DRC (Target)

```sql
USE DRC;

CREATE TABLE dbo.employees (
    id          INT IDENTITY(1,1) PRIMARY KEY,
    name        VARCHAR(100),
    department  VARCHAR(50),
    salary      DECIMAL(10,2),
    created_at  DATETIME DEFAULT GETDATE()
);

-- Verifikasi (seharusnya kosong)
SELECT * FROM dbo.employees;
```

!!! info "Struktur Tabel"
    Struktur tabel di database target (`DRC`) harus **identik** dengan tabel di source (`PROD2`) agar replikasi berjalan dengan benar.

!!! warning "Data Existing"
    Data yang sudah ada di PROD2 **sebelum** OGG dikonfigurasi **tidak akan ter-replikasi secara otomatis**. OGG hanya mereplikasi perubahan yang terjadi setelah proses Extract dijalankan.
