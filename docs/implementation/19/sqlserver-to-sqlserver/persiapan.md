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

## Checklist Persiapan

- [ ] Windows 64-bit (Windows Server 2016/2019 atau Windows 10/11)
- [ ] SQL Server 2019 Developer Edition tersedia untuk diinstall
- [ ] Koneksi jaringan antara PC Source dan PC Target
- [ ] Akses Administrator pada kedua mesin
- [ ] Akun Oracle eDelivery untuk download OGG
- [ ] Minimal 4 GB RAM dan 20 GB disk space bebas
- [ ] Port `7809` dan `7909` tidak diblokir firewall

## Urutan Instalasi

Ikuti urutan fase instalasi berikut secara berurutan:

1. **Phase 1** — Install SQL Server 2019 & SSMS
2. **Phase 2** — Buat database PROD2 (source) dan DRC (target)
3. **Phase 3** — Install ODBC Driver 17
4. **Phase 4** — Install Oracle GoldenGate 21.4
5. **Phase 5** — Konfigurasi SQL Server (CDC, Login, Mixed Mode)
6. **Phase 6** — Konfigurasi OGG (GLOBALS, TRANDATA)
7. **Phase 7** — Buat parameter files (mgr, ext1, pump1, rep1)
8. **Phase 8** — Jalankan semua proses OGG
9. **Phase 9** — Pengujian replikasi
