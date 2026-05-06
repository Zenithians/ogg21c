# Replicat

Replicat adalah proses OGG yang menerapkan perubahan data ke database target.

Replicat membaca trail file, menerjemahkan record perubahan, lalu menjalankan operasi yang sesuai pada tabel target.

## Fungsi

- membaca remote trail atau local trail,
- menerapkan `INSERT`, `UPDATE`, dan `DELETE` ke target,
- menjalankan mapping tabel dan kolom,
- menjaga checkpoint agar apply bisa dilanjutkan dengan aman.

## Catatan

Replicat sangat bergantung pada struktur tabel target. Primary key, constraint, dan mapping perlu disiapkan dengan benar agar apply berjalan stabil.
