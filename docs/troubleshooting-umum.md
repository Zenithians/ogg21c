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

- Credential database salah,
- Privilege user OGG kurang,
- Supplemental logging belum aktif,
- Source database tidak bisa diakses,
- Parameter file salah,
- Log yang dibutuhkan sudah tidak tersedia.

Yang perlu dicek:

```text
INFO EXTRACT <nama_extract>, DETAIL
VIEW REPORT <nama_extract>
```

Untuk Microservices, cek report dari Administration Service.

## Replicat Abended

Penyebab umum:

- Tabel target tidak ada,
- Struktur kolom source dan target berbeda,
- Primary key atau unique key bermasalah,
- Constraint target menolak data,
- Mapping table salah,
- Trail file rusak atau tidak lengkap.

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
- Port target tertutup firewall,
- Hostname atau IP target salah,
- Disk target penuh.

Yang perlu dicek:

- Status Data Pump atau Distribution,
- Port Manager atau Receiver,
- Ukuran local trail,
- Koneksi jaringan source ke target,
- Log Manager atau Distribution Service.

## Lag Tinggi

Penyebab umum:

- Transaksi source sangat besar,
- Target database lambat,
- Index target terlalu banyak,
- Jaringan lambat,
- Disk trail lambat,
- Replicat hanya berjalan single-thread untuk beban besar.

Langkah awal:

- Cek proses mana yang lag,
- Cek apakah Extract, Pump, atau Replicat yang tertinggal,
- Cek report rate,
- Cek beban database target,
- Cek transaksi long-running di source.

## Credential Error

Penyebab umum:

- Alias credential salah,
- Domain credential salah,
- Password database berubah,
- User database locked,
- Service name atau DSN salah.

Yang perlu dicek:

- Nama credential alias,
- Domain credential,
- Koneksi manual ke database,
- Status user database.

## Table Not Found

Penyebab umum:

- Tabel target belum dibuat,
- Schema mapping salah,
- Nama tabel case-sensitive,
- Parameter `MAP` atau `TABLE` tidak sesuai,
- User target tidak punya akses ke tabel.

Pastikan tabel target tersedia sebelum Replicat dijalankan.

## Disk Full

Disk penuh sering terjadi karena trail, report, atau discard file tidak dibersihkan.

Yang perlu dicek:

- Folder `dirdat`,
- Folder `dirrpt`,
- Folder log deployment,
- Konfigurasi purge trail.

Jangan menghapus trail secara manual sebelum memastikan checkpoint sudah melewati trail tersebut.
