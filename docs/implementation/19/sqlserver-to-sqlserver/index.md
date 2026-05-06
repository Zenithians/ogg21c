# Oracle GoldenGate 21.4 for SQL Server

## Dokumentasi Instalasi & Penggunaan

Dokumentasi ini mencakup panduan lengkap instalasi dan konfigurasi **Oracle GoldenGate (OGG) 21.4** untuk replikasi data real-time antara dua instance **SQL Server 2019**.

---

## Ringkasan Konfigurasi

| Item | PC Source | PC Target |
|------|-----------|-----------|
| Database | SQL Server 2019 Developer | SQL Server 2019 Developer |
| GoldenGate | 21.4 for SQL Server | 21.4 for SQL Server |
| ODBC | ODBC Driver 17 for SQL Server | ODBC Driver 17 for SQL Server |
| DB Name | `PROD2` | `DRC` |
| OGG Path | `C:\OGG\source` | `C:\OGG\target` |
| MGR Port | `7809` | `7909` |
| Instance Name | `DESKTOP-MVMVJSO\MSQL2019` | `DESKTOP-MVMVJSO\MSQL2019` |

---

## Alur Dokumentasi

```
Phase 1  →  Install SQL Server 2019 & SSMS
Phase 2  →  Setup Database PROD2 & DRC
Phase 3  →  Install ODBC Driver 17
Phase 4  →  Install OGG 21.4 for SQL Server
Phase 5  →  Konfigurasi SQL Server untuk OGG
Phase 6  →  Konfigurasi OGG (GLOBALS & TRANDATA)
Phase 7  →  Buat Parameter Files
Phase 8  →  Jalankan OGG (MGR, EXTRACT, PUMP, REPLICAT)
Phase 9  →  Testing Replikasi
```

---

## Prasyarat

!!! warning "Kompatibilitas"
    OGG 21.4 hanya mendukung **SQL Server 2019** ke bawah. SQL Server 2022/2025 **tidak didukung**.

!!! info "ODBC Driver"
    Gunakan **ODBC Driver 17** for SQL Server. Driver 18 tidak kompatibel dengan OGG 21.4.

---

## Komponen Utama

| Komponen | Deskripsi |
|----------|-----------|
| **Extract (EXT1)** | Membaca transaction log dari database source |
| **Data Pump (PUMP1)** | Mengirim trail file ke target via jaringan |
| **Replicat (REP1)** | Menerapkan perubahan ke database target |
| **Manager** | Mengontrol dan memonitor semua proses OGG |
| **Trail File** | File antrian perubahan data sementara |
