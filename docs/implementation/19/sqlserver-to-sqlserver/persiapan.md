# Persiapan

Sebelum memulai instalasi, pastikan semua kebutuhan berikut sudah tersedia.

## Spesifikasi Lingkungan

| Item | PC Source | PC Target |
|------|-----------|-----------|
| Database | SQL Server 2019 Developer | SQL Server 2019 Developer |
| GoldenGate | 21.4 for SQL Server | 21.4 for SQL Server |
| ODBC Driver | ODBC Driver 17 for SQL Server | ODBC Driver 17 for SQL Server |
| DB Name | `PROD2` | `DRC` |
| OGG Path | `C:\OGG\source` | `C:\OGG\target` |
| Manager Port | `7809` | `7909` |
| Instance Name | `DESKTOP-MVMVJSO\MSQL2019` | `DESKTOP-MVMVJSO\MSQL2019` |


## Urutan Instalasi

Ikuti urutan fase instalasi berikut secara berurutan:

1. Install SQL Server 2019 & SSMS
2. Buat database PROD2 (source) dan DRC (target)
3. Install ODBC Driver 17
4. Install Oracle GoldenGate 21.4
5. Konfigurasi SQL Server (CDC, Login, Mixed Mode)
6. Konfigurasi OGG (GLOBALS, TRANDATA)
7. Buat parameter files (mgr, ext1, pump1, rep1)
8. Jalankan semua proses OGG
9. Pengujian replikasi
