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

- host dan IP,
- user database,
- credential alias,
- port Manager atau service,
- folder trail,
- schema atau tabel yang direplikasi.

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

- lag Extract,
- lag Data Pump atau Distribution,
- lag Replicat,
- ukuran trail,
- transaksi besar yang belum selesai.

## Dokumentasikan Parameter

Simpan catatan untuk:

- nama proses,
- nama trail,
- tabel yang direplikasi,
- mapping schema,
- credential alias,
- port yang dipakai,
- lokasi report dan discard file.

Dokumentasi kecil seperti ini sangat membantu saat handover atau incident.

## Test Sebelum Production

Sebelum production, minimal lakukan:

- insert, update, delete,
- transaksi banyak record,
- restart Extract dan Replicat,
- simulasi jaringan putus,
- cek data source dan target,
- cek behavior saat constraint target aktif.

## Hindari Perubahan DDL Sembarangan

Perubahan struktur tabel bisa memengaruhi replikasi.

Sebelum mengubah DDL:

- cek apakah tabel sedang direplikasi,
- sesuaikan struktur target,
- review parameter mapping,
- siapkan rollback plan,
- lakukan di window maintenance jika perlu.
