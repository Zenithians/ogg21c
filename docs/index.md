# Dokumentasi Oracle GoldenGate

Dokumentasi ini disusun sebagai basis pengetahuan Oracle GoldenGate (OGG) yang mudah dikembangkan. Materi dibagi menjadi tiga bagian besar:

1. **Introduction** untuk pengenalan konsep, topologi, dan kelebihan OGG.
2. **Komponen OGG** untuk memahami proses inti seperti Extract, Data Pump, Distribution, Replicat, dan Trail.
3. **Implementasi OGG** untuk panduan teknis berdasarkan versi OGG dan skenario database.

## Struktur Implementasi

Setiap implementasi diletakkan berdasarkan versi dan pasangan database. Dengan pola ini, skenario baru bisa ditambahkan tanpa mengubah struktur utama.

| Versi | Skenario | Lokasi |
|---|---|---|
| 19 | SQL Server to SQL Server | `implementation/19/sqlserver-to-sqlserver/` |
| 21 | Oracle to Oracle | `implementation/21/oracle-to-oracle/` |

!!! note "Catatan"
    Materi dari folder `oggsql` berisi panduan OGG untuk SQL Server. Jika nanti ada implementasi MySQL to MySQL, PostgreSQL to Oracle, atau database lain, cukup tambahkan folder baru di bawah versi yang sesuai.

## Mulai Membaca

Mulai dari [Pengenalan OGG](introduction/pengenalan-ogg.md), lanjutkan ke [Komponen OGG](components/index.md), lalu pilih implementasi yang dibutuhkan.
