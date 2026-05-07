# Komponen Tambahan

Selain Extract, Data Pump, Replicat, Distribution, dan Trail File, ada beberapa komponen pendukung yang penting dipahami saat mengelola Oracle GoldenGate.

## Manager

Manager adalah proses utama pada Classic Architecture yang mengontrol proses OGG lain.

Fungsi Manager:

- Menjalankan dan menghentikan proses,
- Menerima koneksi dari Data Pump,
- Mengelola port komunikasi,
- Menjalankan purge trail sesuai konfigurasi,
- Menulis report dan event log.

Contoh parameter umum:

```text
PORT 7809
DYNAMICPORTLIST 7810-7820
PURGEOLDEXTRACTS ./dirdat/*, USECHECKPOINTS, MINKEEPDAYS 3
```

## Service Manager

Service Manager adalah service pusat pada Microservices Architecture.

Fungsi Service Manager:

- Mengelola deployment OGG,
- Menyediakan akses ke service lain,
- Mengatur lifecycle service,
- Menjadi pintu awal administrasi web.

## Administration Service

Administration Service digunakan untuk mengelola Extract dan Replicat pada Microservices.

Fungsi utama:

- Membuat Extract,
- Membuat Replicat,
- Mengedit parameter file,
- Start dan stop process,
- Melihat status dan report process.

## Receiver Service

Receiver Service menerima trail yang dikirim dari Distribution Service.

Fungsi utama:

- Menerima data trail dari source,
- Menulis remote trail di target,
- Menjaga koneksi distribusi antar deployment.

## Performance Metrics Service

Performance Metrics Service menyediakan informasi performa dan monitoring.

Data yang biasanya dipantau:

- Status process,
- Lag,
- Throughput,
- Statistik operasi,
- Health deployment.

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

- Membantu recovery setelah restart,
- Menghindari apply transaksi ganda,
- Menyimpan posisi apply secara lebih aman,
- Memudahkan monitoring posisi Replicat.

## Heartbeat Table

Heartbeat table digunakan untuk memantau lag replikasi secara lebih jelas.

Konsepnya sederhana:

1. Source membuat atau memperbarui record heartbeat secara berkala.
2. OGG mereplikasi record itu ke target.
3. Selisih waktu antara source dan target dipakai untuk membaca lag.

Heartbeat berguna untuk membedakan apakah replikasi benar-benar sehat atau hanya terlihat running tetapi tidak memproses data baru.
