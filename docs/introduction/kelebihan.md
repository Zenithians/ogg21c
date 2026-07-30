---
icon: fontawesome/solid/wand-magic-sparkles
---

# Kelebihan

Oracle GoldenGate banyak dipakai karena fleksibel untuk berbagai skenario replikasi dan migrasi data.

## Kelebihan Utama

- **Latensi rendah**: Perubahan data dapat direplikasi hampir real-time.
- **Heterogeneous support**: Dapat digunakan lintas platform database sesuai dukungan versi OGG.
- **Downtime minimal**: Cocok untuk migrasi atau cutover bertahap.
- **Selective replication**: Replikasi bisa dibatasi pada schema, tabel, atau mapping tertentu.
- **Trail-based**: Perubahan disimpan dalam trail file sehingga proses capture dan apply dapat dipisahkan.
- **Monitoring terpisah**: Proses seperti Extract, Pump, Distribution, dan Replicat dapat dipantau secara individual.

## Catatan

OGG bukan pengganti backup database. OGG mereplikasi perubahan data, sedangkan backup tetap dibutuhkan untuk pemulihan penuh saat terjadi kerusakan data atau sistem.
