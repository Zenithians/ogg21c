# Troubleshooting Umum

Halaman ini berisi panduan troubleshooting umum yang berlaku untuk banyak implementasi Oracle GoldenGate.

## Langkah Awal

Saat terjadi masalah, mulai dari urutan ini:

1. Cek status semua proses.
2. Cek report file proses yang bermasalah.
3. Cek event log OGG.
4. Cek koneksi database.
5. Cek trail file.
6. Cek disk space.
7. Cek jaringan antar host.

## Extract Abended

Penyebab umum:

- credential database salah,
- privilege user OGG kurang,
- supplemental logging belum aktif,
- source database tidak bisa diakses,
- parameter file salah,
- log yang dibutuhkan sudah tidak tersedia.

Yang perlu dicek:

```text
INFO EXTRACT <nama_extract>, DETAIL
VIEW REPORT <nama_extract>
```

Untuk Microservices, cek report dari Administration Service.

## Replicat Abended

Penyebab umum:

- tabel target tidak ada,
- struktur kolom source dan target berbeda,
- primary key atau unique key bermasalah,
- constraint target menolak data,
- mapping table salah,
- trail file rusak atau tidak lengkap.

Yang perlu dicek:

```text
INFO REPLICAT <nama_replicat>, DETAIL
VIEW REPORT <nama_replicat>
```

Jika ada record gagal, cek discard file.

## Trail Tidak Terkirim

Penyebab umum:

- Data Pump mati,
- Distribution Path berhenti,
- Receiver Service tidak running,
- port target tertutup firewall,
- hostname atau IP target salah,
- disk target penuh.

Yang perlu dicek:

- status Data Pump atau Distribution,
- port Manager atau Receiver,
- ukuran local trail,
- koneksi jaringan source ke target,
- log Manager atau Distribution Service.

## Lag Tinggi

Penyebab umum:

- transaksi source sangat besar,
- target database lambat,
- index target terlalu banyak,
- jaringan lambat,
- disk trail lambat,
- Replicat hanya berjalan single-thread untuk beban besar.

Langkah awal:

- cek proses mana yang lag,
- cek apakah Extract, Pump, atau Replicat yang tertinggal,
- cek report rate,
- cek beban database target,
- cek transaksi long-running di source.

## Credential Error

Penyebab umum:

- alias credential salah,
- domain credential salah,
- password database berubah,
- user database locked,
- service name atau DSN salah.

Yang perlu dicek:

- nama credential alias,
- domain credential,
- koneksi manual ke database,
- status user database.

## Table Not Found

Penyebab umum:

- tabel target belum dibuat,
- schema mapping salah,
- nama tabel case-sensitive,
- parameter `MAP` atau `TABLE` tidak sesuai,
- user target tidak punya akses ke tabel.

Pastikan tabel target tersedia sebelum Replicat dijalankan.

## Disk Full

Disk penuh sering terjadi karena trail, report, atau discard file tidak dibersihkan.

Yang perlu dicek:

- folder `dirdat`,
- folder `dirrpt`,
- folder log deployment,
- konfigurasi purge trail.

Jangan menghapus trail secara manual sebelum memastikan checkpoint sudah melewati trail tersebut.
