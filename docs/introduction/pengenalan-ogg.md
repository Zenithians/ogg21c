# Pengenalan OGG

Oracle GoldenGate (OGG) adalah platform replikasi data yang digunakan untuk menangkap, memindahkan, dan menerapkan perubahan data antar sistem database dengan latensi rendah.

OGG umum digunakan untuk:

- replikasi real-time antar database,
- migrasi database dengan downtime minimal,
- disaster recovery,
- integrasi data operasional,
- distribusi data antar aplikasi atau lokasi.

Pada prinsipnya, OGG membaca perubahan dari database source, menyimpannya ke trail file, lalu mengirim dan menerapkan perubahan tersebut ke database target.

## Alur Dasar

```text
Database Source
  -> Extract
  -> Local Trail
  -> Data Pump / Distribution
  -> Remote Trail
  -> Replicat
  -> Database Target
```

Implementasi detailnya bisa berbeda tergantung versi OGG, tipe database, dan arsitektur yang digunakan, misalnya Classic Architecture atau Microservices Architecture.
