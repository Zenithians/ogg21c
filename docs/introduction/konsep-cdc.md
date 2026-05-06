# Konsep Dasar CDC

Change Data Capture (CDC) adalah mekanisme untuk menangkap perubahan data dari database tanpa membaca ulang seluruh isi tabel. Perubahan yang ditangkap biasanya berupa `INSERT`, `UPDATE`, dan `DELETE`.

Oracle GoldenGate memanfaatkan konsep CDC agar perubahan dari database source bisa dikirim ke database target secara cepat dan berurutan.

## Kenapa CDC Penting

Tanpa CDC, proses sinkronisasi biasanya harus membandingkan isi tabel source dan target. Cara itu berat, lambat, dan sulit dipakai untuk replikasi real-time.

Dengan CDC, OGG cukup membaca jejak perubahan transaksi dari database source.

## Sumber Perubahan Data

| Database | Sumber Capture Umum |
|---|---|
| Oracle Database | Redo log dan archive log |
| SQL Server | Transaction log dan CDC |
| MySQL | Binary log |
| PostgreSQL | Write-ahead log atau logical decoding |

Detail teknisnya berbeda per database, tetapi idenya sama: OGG membaca perubahan transaksi yang sudah dicatat database.

## Alur CDC di OGG

```text
User menjalankan transaksi
  -> Database mencatat perubahan di log transaksi
  -> Extract membaca perubahan dari log
  -> Perubahan ditulis ke trail file
  -> Trail dikirim ke target
  -> Replicat menerapkan perubahan ke database target
```

## Commit Order

Commit order adalah urutan transaksi saat berhasil di-commit di source. OGG menjaga urutan ini agar data di target tetap konsisten.

Contoh:

1. Transaksi A insert data customer.
2. Transaksi B insert data order untuk customer tersebut.
3. Target harus menerima transaksi A lebih dulu sebelum transaksi B.

Jika urutan transaksi kacau, constraint atau relasi data di target bisa gagal.

## Checkpoint

Checkpoint menyimpan posisi terakhir proses OGG membaca atau menerapkan data.

Checkpoint membantu OGG melanjutkan proses setelah restart tanpa mengulang dari awal atau melewati transaksi penting.

| Proses | Fungsi Checkpoint |
|---|---|
| Extract | Menyimpan posisi capture terakhir di log source. |
| Data Pump / Distribution | Menyimpan posisi trail terakhir yang dikirim. |
| Replicat | Menyimpan posisi trail terakhir yang sudah diterapkan ke target. |

## Latency dan Lag

Latency adalah jeda waktu antara perubahan di source dan perubahan tersebut muncul di target. Di OGG, istilah yang sering dipakai adalah lag.

Lag bisa muncul karena:

- transaksi source sangat besar,
- jaringan lambat atau putus,
- disk tempat trail penuh atau lambat,
- Replicat lambat apply ke target,
- target database sedang sibuk.

Monitoring lag menjadi bagian penting dari operasional harian OGG.
