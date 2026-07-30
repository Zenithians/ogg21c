---
icon: fontawesome/solid/triangle-exclamation
---

# Troubleshooting

Kumpulan error yang ditemukan selama instalasi dan konfigurasi OGG 21.4 for SQL Server beserta solusinya.

## Daftar Error & Solusi

| Error | Penyebab | Solusi |
|-------|----------|--------|
| `OGG-05312: msodbcsql18.dll not supported` | OGG 21.4 hanya support Driver 17 | Install ODBC Driver 17, buat ulang DSN dengan Driver 17 |
| `SQL Server 2025 not supported` | OGG 21.4 max support SQL Server 2019 | Install SQL Server 2019 Developer Edition |
| `Login failed for ggadmin di ODBC` | Encryption Mandatory + Mixed Mode belum aktif | Set Encryption=Optional, Trust Certificate, aktifkan Mixed Mode |
| `Parameter file jadi 1 baris` | `echo` tanpa tanda kurung | Gunakan perintah `echo` dengan tanda kurung `()` di CMD |
| `OGG-05331: CDC Cleanup job not exist` | OGG CDC job belum dibuat | Jalankan `ogg_create_cdc_cleanup_job.sql` dengan variabel via `sqlcmd` |
| `Manager not currently running` | MGR target belum start | Buka CMD baru, `cd C:\OGG\target`, lalu `START MGR` |
| `TCP/IP error 10061 port 7909` | Manager target tidak running | Start MGR di folder target terlebih dahulu |
| `GGSCHEMA not specified` | File GLOBALS tidak ada | Buat file GLOBALS: `echo GGSCHEMA ggadmin> GLOBALS` |

---

## Panduan Diagnosa

### Cek Status Semua Proses

```
GGSCI> INFO ALL
```

### Lihat Log Error

```
GGSCI> VIEW REPORT ext1
GGSCI> VIEW REPORT pump1
GGSCI> VIEW REPORT rep1
```

### Cek Statistik Replikasi

```
GGSCI> STATS EXTRACT ext1
GGSCI> STATS REPLICAT rep1
```

### Cek Lag (Keterlambatan)

```
GGSCI> LAG EXTRACT ext1
GGSCI> LAG REPLICAT rep1
```

---

## Skenario Umum

### Proses ABENDED Setelah Restart

Jika proses berstatus `ABENDED` setelah PC restart:

1. Jalankan `VIEW REPORT <nama>` untuk cek pesan error
2. Pastikan SQL Server Agent berjalan
3. Restart proses: `START EXTRACT ext1` atau `START REPLICAT rep1`

### Replikasi Terhenti / Lag Tinggi

1. Cek status dengan `INFO ALL`
2. Periksa apakah Manager di kedua sisi berjalan
3. Periksa koneksi jaringan antara Source dan Target (port 7909)
4. Cek disk space — trail file butuh ruang yang cukup

### Reset & Mulai Ulang OGG

Jika perlu memulai ulang konfigurasi OGG dari awal:

```
GGSCI> STOP REPLICAT rep1
GGSCI> STOP EXTRACT pump1
GGSCI> STOP EXTRACT ext1
GGSCI> DELETE REPLICAT rep1
GGSCI> DELETE EXTRACT pump1
GGSCI> DELETE EXTRACT ext1
GGSCI> STOP MGR
```

Kemudian ulangi dari [Phase 8](../fase/phase8-start-ogg.md).
