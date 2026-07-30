---
icon: fontawesome/solid/file-lines
---

# Membuat Parameter Files

Parameter files adalah file konfigurasi untuk setiap proses OGG. Jalankan semua perintah di bawah ini melalui **CMD as Administrator**.

## Manager Source (`mgr.prm`)

```cmd
(
echo PORT 7809
echo DYNAMICPORTLIST 7810-7820
echo AUTORESTART EXTRACT *, RETRIES 5, WAITMINUTES 3
echo PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
)> C:\OGG\source\dirprm\mgr.prm
```

Isi file `mgr.prm` (source):

```
PORT 7809
DYNAMICPORTLIST 7810-7820
AUTORESTART EXTRACT *, RETRIES 5, WAITMINUTES 3
PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
```

## Extract (`ext1.prm`)

```cmd
(
echo EXTRACT ext1
echo SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"
echo EXTTRAIL ./dirdat/lt
echo.
echo TABLE dbo.employees;
)> C:\OGG\source\dirprm\ext1.prm
```

Isi file `ext1.prm`:

```
EXTRACT ext1
SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"
EXTTRAIL ./dirdat/lt

TABLE dbo.employees;
```

## Data Pump (`pump1.prm`)

```cmd
(
echo EXTRACT pump1
echo SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"
echo RMTHOST localhost, MGRPORT 7909
echo RMTTRAIL C:\OGG\target\dirdat\rt
echo.
echo TABLE dbo.employees;
)> C:\OGG\source\dirprm\pump1.prm
```

Isi file `pump1.prm`:

```
EXTRACT pump1
SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"
RMTHOST localhost, MGRPORT 7909
RMTTRAIL C:\OGG\target\dirdat\rt

TABLE dbo.employees;
```

!!! note "RMTHOST"
    Ganti `localhost` dengan IP address PC Target jika Source dan Target berada di mesin yang berbeda.

## Manager Target (`mgr.prm`)

```cmd
(
echo PORT 7909
echo DYNAMICPORTLIST 7910-7920
echo AUTORESTART REPLICAT *, RETRIES 5, WAITMINUTES 3
echo PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
)> C:\OGG\target\dirprm\mgr.prm
```

Isi file `mgr.prm` (target):

```
PORT 7909
DYNAMICPORTLIST 7910-7920
AUTORESTART REPLICAT *, RETRIES 5, WAITMINUTES 3
PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
```

## Replicat (`rep1.prm`)

```cmd
(
echo REPLICAT rep1
echo TARGETDB DRC, USERID ggadmin, PASSWORD "OGGAdmin123!"
echo DISCARDFILE ./dirrpt/rep1.dsc, APPEND, MEGABYTES 50
echo ASSUMETARGETDEFS
echo.
echo MAP dbo.employees, TARGET dbo.employees;
)> C:\OGG\target\dirprm\rep1.prm
```

Isi file `rep1.prm`:

```
REPLICAT rep1
TARGETDB DRC, USERID ggadmin, PASSWORD "OGGAdmin123!"
DISCARDFILE ./dirrpt/rep1.dsc, APPEND, MEGABYTES 50
ASSUMETARGETDEFS

MAP dbo.employees, TARGET dbo.employees;
```

## Verifikasi Semua File

Pastikan kelima file berhasil dibuat:

```cmd
type C:\OGG\source\dirprm\mgr.prm
type C:\OGG\source\dirprm\ext1.prm
type C:\OGG\source\dirprm\pump1.prm
type C:\OGG\target\dirprm\mgr.prm
type C:\OGG\target\dirprm\rep1.prm
```

!!! warning "Format File"
    Pastikan setiap parameter berada di **baris terpisah**. Jika semua parameter muncul dalam satu baris, parameter file tidak akan terbaca dengan benar oleh OGG.
