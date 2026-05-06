# Kelebihan

Oracle GoldenGate banyak dipakai karena fleksibel untuk berbagai skenario replikasi dan migrasi data.

## Kelebihan Utama

- **Latensi rendah**: perubahan data dapat direplikasi hampir real-time.
- **Heterogeneous support**: dapat digunakan lintas platform database sesuai dukungan versi OGG.
- **Downtime minimal**: cocok untuk migrasi atau cutover bertahap.
- **Selective replication**: replikasi bisa dibatasi pada schema, tabel, atau mapping tertentu.
- **Trail-based**: perubahan disimpan dalam trail file sehingga proses capture dan apply dapat dipisahkan.
- **Monitoring terpisah**: proses seperti Extract, Pump, Distribution, dan Replicat dapat dipantau secara individual.

## Catatan Desain

OGG bukan pengganti backup database. OGG mereplikasi perubahan data, sedangkan backup tetap dibutuhkan untuk pemulihan penuh saat terjadi kerusakan data atau sistem.
