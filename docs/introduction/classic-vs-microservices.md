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

```text
Source DB
  -> Extract
  -> Local Trail
  -> Data Pump
  -> Remote Trail
  -> Replicat
  -> Target DB
```

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

```text
Source DB
  -> Extract
  -> Trail
  -> Distribution Service
  -> Receiver Service
  -> Remote Trail
  -> Replicat
  -> Target DB
```

## Kapan Menggunakan Classic

Classic cocok ketika:

- lingkungan sudah memakai OGG versi lama,
- tim lebih nyaman dengan GGSCI,
- deployment kecil dan sederhana,
- automation sudah dibangun berbasis script CLI.

## Kapan Menggunakan Microservices

Microservices cocok ketika:

- butuh web interface untuk administrasi,
- ingin integrasi dengan REST API,
- ingin monitoring yang lebih mudah,
- deployment perlu dikelola lebih terstruktur,
- memakai OGG versi modern seperti 21c.

## Hubungan dengan Dokumentasi Ini

Implementasi SQL Server to SQL Server di dokumentasi ini mengikuti gaya Classic, sedangkan implementasi Oracle to Oracle 21c memakai Microservices.
