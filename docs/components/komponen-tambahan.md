# Komponen Tambahan

Selain Extract, Data Pump, Replicat, Distribution, dan Trail File, ada beberapa komponen pendukung yang penting dipahami saat mengelola Oracle GoldenGate.

## Manager

Manager adalah proses utama pada Classic Architecture yang mengontrol proses OGG lain.

Fungsi Manager:

- menjalankan dan menghentikan proses,
- menerima koneksi dari Data Pump,
- mengelola port komunikasi,
- menjalankan purge trail sesuai konfigurasi,
- menulis report dan event log.

Contoh parameter umum:

```text
PORT 7809
DYNAMICPORTLIST 7810-7820
PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
```

## Service Manager

Service Manager adalah service pusat pada Microservices Architecture.

Fungsi Service Manager:

- mengelola deployment OGG,
- menyediakan akses ke service lain,
- mengatur lifecycle service,
- menjadi pintu awal administrasi web.

## Administration Service

Administration Service digunakan untuk mengelola Extract dan Replicat pada Microservices.

Fungsi utama:

- membuat Extract,
- membuat Replicat,
- mengedit parameter file,
- start dan stop process,
- melihat status dan report process.

## Receiver Service

Receiver Service menerima trail yang dikirim dari Distribution Service.

Fungsi utama:

- menerima data trail dari source,
- menulis remote trail di target,
- menjaga koneksi distribusi antar deployment.

## Performance Metrics Service

Performance Metrics Service menyediakan informasi performa dan monitoring.

Data yang biasanya dipantau:

- status process,
- lag,
- throughput,
- statistik operasi,
- health deployment.

## Credential Store

Credential Store menyimpan kredensial database secara aman agar user dan password tidak ditulis langsung di parameter file.

Contoh pemakaian:

```text
USERIDALIAS srcdb DOMAIN OracleGoldenGate
```

Dengan cara ini, parameter file hanya menyimpan alias, bukan password asli.

## Parameter File

Parameter file adalah file konfigurasi untuk proses OGG.

Contoh proses yang memakai parameter file:

- Manager,
- Extract,
- Data Pump,
- Replicat.

Parameter file menentukan koneksi database, nama trail, mapping tabel, filtering, report, discard file, dan opsi lain.

## Checkpoint Table

Checkpoint table biasanya digunakan Replicat untuk menyimpan posisi apply di database target.

Manfaat checkpoint table:

- membantu recovery setelah restart,
- menghindari apply transaksi ganda,
- menyimpan posisi apply secara lebih aman,
- memudahkan monitoring posisi Replicat.

## Heartbeat Table

Heartbeat table digunakan untuk memantau lag replikasi secara lebih jelas.

Konsepnya sederhana:

1. Source membuat atau memperbarui record heartbeat secara berkala.
2. OGG mereplikasi record itu ke target.
3. Selisih waktu antara source dan target dipakai untuk membaca lag.

Heartbeat berguna untuk membedakan apakah replikasi benar-benar sehat atau hanya terlihat running tetapi tidak memproses data baru.
