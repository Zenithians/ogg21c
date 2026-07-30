---
icon: fontawesome/solid/download
---

# Replicat

Replicat adalah proses OGG yang menerapkan perubahan data ke database target.

Replicat membaca trail file, menerjemahkan record perubahan, lalu menjalankan operasi yang sesuai pada tabel target.

## Fungsi

- Membaca remote trail atau local trail,
- Menerapkan `INSERT`, `UPDATE`, dan `DELETE` ke target,
- Menjalankan mapping tabel dan kolom,
- Menjaga checkpoint agar apply bisa dilanjutkan dengan aman.

## Catatan

Replicat sangat bergantung pada struktur tabel target. Primary key, constraint, dan mapping perlu disiapkan dengan benar agar apply berjalan stabil.
