# Arsitektur OGG Classic vs Microservices

Oracle GoldenGate memiliki dua gaya arsitektur yang umum ditemui: Classic Architecture dan Microservices Architecture.

Classic Architecture banyak dikelola lewat command line seperti GGSCI. Microservices Architecture menyediakan service berbasis REST API dan web interface untuk administrasi.

## Ringkasan Perbandingan

| Area | Classic Architecture | Microservices Architecture |
|---|---|---|
| Administrasi | GGSCI dan file konfigurasi | Web UI, REST API, dan Admin Client |
| Proses utama | Manager, Extract, Data Pump, Replicat | Service Manager, Admin Service, Distribution, Receiver, Performance Metrics |
| Pengiriman trail | Data Pump | Distribution Service dan Receiver Service |
| Monitoring | Command line dan report file | Web UI, REST API, metrics service, report file |
| Cocok untuk | Setup sederhana, legacy, lingkungan CLI | Deployment modern, automation, monitoring terpusat |

## Classic Architecture

Pada Classic Architecture, proses OGG biasanya dikelola dari folder instalasi OGG menggunakan GGSCI.

Komponen yang sering dipakai:

- Manager
- Extract
- Data Pump
- Replicat
- Trail file
- Parameter file

Contoh pola umum:

<div style="text-align: center;">
  <img src="../assets/images/common/alur-dasar.png.png" alt="Diagram Alur Dasar OGG" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
</div>

## Microservices Architecture

Pada Microservices Architecture, OGG berjalan dalam deployment yang memiliki beberapa service.

Komponen yang sering dipakai:

- Service Manager
- Administration Service
- Distribution Service
- Receiver Service
- Performance Metrics Service
- Extract
- Replicat
- Trail file

Contoh pola umum:

<div style="text-align: center;">
  <img src="../assets/images/common/microservices.png.png" alt="Diagram Alur Dasar OGG" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
</div>

## Kapan Menggunakan Classic

Classic cocok ketika:

- Lingkungan sudah memakai OGG versi lama,
- Tim lebih nyaman dengan GGSCI,
- Deployment kecil dan sederhana,
- Automation sudah dibangun berbasis script CLI.

## Kapan Menggunakan Microservices

Microservices cocok ketika:

- Butuh web interface untuk administrasi,
- Ingin integrasi dengan REST API,
- Ingin monitoring yang lebih mudah,
- Deployment perlu dikelola lebih terstruktur,
- Memakai OGG versi modern seperti 21c.


