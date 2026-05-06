# Phase 6 — Konfigurasi OGG

## 6.1 Setup File GLOBALS

File GLOBALS harus dibuat di **kedua** folder OGG (source dan target).

**Untuk Source:**

```cmd
cd C:\OGG\source
echo GGSCHEMA ggadmin> GLOBALS
type GLOBALS
```

**Untuk Target:**

```cmd
cd C:\OGG\target
echo GGSCHEMA ggadmin> GLOBALS
type GLOBALS
```

Output `type GLOBALS` harus menampilkan:

```
GGSCHEMA ggadmin
```

!!! danger "File GLOBALS Wajib Ada"
    Jika file GLOBALS tidak ada, OGG akan menampilkan error `GGSCHEMA not specified` dan semua proses tidak bisa dijalankan.

## 6.2 DBLOGIN & ADD TRANDATA (Source)

Buka GGSCI di folder source:

```cmd
cd C:\OGG\source
ggsci.exe
```

Jalankan perintah berikut di dalam GGSCI:

```
GGSCI> DBLOGIN SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"

GGSCI> ADD TRANDATA dbo.employees

GGSCI> INFO TRANDATA dbo.employees
```

!!! success "Verifikasi INFO TRANDATA"
    Output `INFO TRANDATA` harus menampilkan bahwa supplemental logging sudah aktif pada tabel `dbo.employees`.
