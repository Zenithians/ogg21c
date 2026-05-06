# Arsitektur OGG

## Konsep Replikasi

Oracle GoldenGate bekerja dengan menangkap perubahan data (`INSERT`, `UPDATE`, `DELETE`) dari database source melalui **transaction log (CDC)**, kemudian mereplikasikannya secara real-time ke database target.

## Alur Data

```
[SQL Server PROD2]
       |
   [Extract EXT1]          ← Baca transaction log
       |
   [Trail File lt]         ← Simpan sementara di C:\OGG\source\dirdat
       |
   [Data Pump PUMP1]       ← Kirim via port 7909
       |
   [Remote Trail rt]       ← Terima di C:\OGG\target\dirdat
       |
   [Replicat REP1]         ← Terapkan ke SQL Server DRC
       |
[SQL Server DRC]
```

## Komponen Arsitektur

| Komponen | Fungsi | Lokasi |
|----------|--------|--------|
| **Extract (EXT1)** | Membaca transaction log dari PROD2 | `C:\OGG\source` |
| **Trail File (lt)** | Menyimpan sementara data perubahan | `C:\OGG\source\dirdat` |
| **Data Pump (PUMP1)** | Mengirim trail file ke target via port 7909 | `C:\OGG\source` |
| **Remote Trail (rt)** | Trail file di sisi target | `C:\OGG\target\dirdat` |
| **Replicat (REP1)** | Menerapkan perubahan ke DRC | `C:\OGG\target` |
| **Manager Source** | Mengontrol proses OGG Source (port 7809) | `C:\OGG\source` |
| **Manager Target** | Mengontrol proses OGG Target (port 7909) | `C:\OGG\target` |

## Port yang Digunakan

| Port | Digunakan Oleh | Keterangan |
|------|---------------|------------|
| `7809` | Manager Source | Mengontrol proses di sisi source |
| `7810–7820` | Dynamic ports Source | Untuk komunikasi internal |
| `7909` | Manager Target | Menerima data dari pump |
| `7910–7920` | Dynamic ports Target | Untuk komunikasi internal |

!!! note "Catatan Firewall"
    Pastikan port `7909` terbuka di PC Target agar Data Pump dari Source dapat mengirim data.

## Teknologi CDC (Change Data Capture)

OGG memanfaatkan fitur **CDC bawaan SQL Server** untuk menangkap perubahan transaksi tanpa membebani performa database secara signifikan.

Prasyarat CDC:
- Recovery model database harus `FULL`
- SQL Server Agent harus aktif (`Running`)
- CDC harus diaktifkan pada database dan tabel yang direplikasi
