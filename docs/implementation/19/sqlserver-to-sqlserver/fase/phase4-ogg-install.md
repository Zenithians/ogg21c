# Phase 4 — Instalasi OGG 21.4 for SQL Server

## 4.1 Download OGG 21.4

1. Login ke Oracle eDelivery: [https://edelivery.oracle.com](https://edelivery.oracle.com)
2. Search: **Oracle GoldenGate 21.4.0.0.0**
3. Platform: **Microsoft Windows x64 (64-bit)**
4. Download file: `V1018256-01.zip` (OGG 21.4 for SQL Server)

## 4.2 Persiapan Folder & Copy File

Buka **CMD as Administrator** dan jalankan:

```cmd
mkdir C:\OGG\source
mkdir C:\OGG\target

xcopy "D:\Microsoft SQL\OGG SQL SERVER\*" "C:\OGG\source\" /E /H /Y
xcopy "D:\Microsoft SQL\OGG SQL SERVER\*" "C:\OGG\target\" /E /H /Y
```

!!! note "Lokasi File"
    Sesuaikan path `D:\Microsoft SQL\OGG SQL SERVER\` dengan lokasi file OGG yang sudah kamu ekstrak dari zip.

## 4.3 Inisialisasi OGG Source

Buka CMD as Administrator, jalankan:

```cmd
cd C:\OGG\source
ggsci.exe
```

Di dalam GGSCI:

```
GGSCI> CREATE SUBDIRS
```

## 4.4 Inisialisasi OGG Target

Buka CMD **baru** (jangan tutup CMD Source), jalankan:

```cmd
cd C:\OGG\target
ggsci.exe
```

Di dalam GGSCI:

```
GGSCI> CREATE SUBDIRS
```

!!! success "Hasil CREATE SUBDIRS"
    Perintah ini akan membuat folder-folder yang dibutuhkan OGG seperti `dirdat`, `dirprm`, `dirrpt`, `dirtmp`, dll. di dalam masing-masing folder source dan target.
