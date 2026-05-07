# Best Practice

Halaman ini merangkum praktik yang disarankan agar implementasi Oracle GoldenGate lebih mudah dirawat, aman, dan stabil.

## Naming Convention

Gunakan nama proses yang konsisten dan singkat.

| Proses | Contoh | Keterangan |
|---|---|---|
| Extract | `EXTEMP`, `EXTORD` | Capture dari source |
| Data Pump | `PMPEMP`, `PMPORD` | Kirim trail ke target |
| Replicat | `REPEMP`, `REPORD` | Apply ke target |
| Trail | `et`, `lt`, `rt` | Prefix trail dua karakter |

Nama yang konsisten memudahkan troubleshooting, monitoring, dan dokumentasi.

## Pisahkan Environment

Pisahkan konfigurasi untuk development, staging, dan production.

Hal yang sebaiknya dibedakan:

- Host dan IP,
- User database,
- Credential alias,
- Port Manager atau service,
- Folder trail,
- Schema atau tabel yang direplikasi.

## Gunakan Credential Store

Hindari menulis password langsung di parameter file.

Lebih baik gunakan credential alias:

```text
USERIDALIAS srcdb DOMAIN OracleGoldenGate
```

Cara ini lebih aman dan lebih mudah dikelola saat password berubah.

## Aktifkan Report dan Discard File

Report file membantu membaca aktivitas proses. Discard file membantu melihat record yang gagal diproses.

Contoh:

```text
REPORTCOUNT EVERY 30 MINUTES, RATE
DISCARDFILE ./dirrpt/rep1.dsc, APPEND, MEGABYTES 100
```

## Kelola Trail Retention

Trail file bisa tumbuh besar jika tidak dibersihkan.

Gunakan purge dengan checkpoint agar trail yang masih dibutuhkan tidak terhapus.

Contoh Classic:

```text
PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
```

## Monitor Lag

Lag harus dicek rutin, bukan hanya saat ada error.

Pantau:

- Lag Extract,
- Lag Data Pump atau Distribution,
- Lag Replicat,
- Ukuran trail,
- Transaksi besar yang belum selesai.

## Dokumentasikan Parameter

Simpan catatan untuk:

- Nama proses,
- Nama trail,
- Tabel yang direplikasi,
- Mapping schema,
- Credential alias,
- Port yang dipakai,
- Lokasi report dan discard file.

Dokumentasi kecil seperti ini sangat membantu saat handover atau incident.

## Test Sebelum Production

Sebelum production, minimal lakukan:

- Insert, update, delete,
- Transaksi banyak record,
- Restart Extract dan Replicat,
- Simulasi jaringan putus,
- Cek data source dan target,
- Cek behavior saat constraint target aktif.

## Hindari Perubahan DDL Sembarangan

Perubahan struktur tabel bisa memengaruhi replikasi.

Sebelum mengubah DDL:

- Cek apakah tabel sedang direplikasi,
- Sesuaikan struktur target,
- Review parameter mapping,
- Siapkan rollback plan,
- Lakukan di window maintenance jika perlu.
