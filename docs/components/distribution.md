---
icon: fontawesome/solid/route
---

# Distribution

Distribution Service adalah komponen pada OGG Microservices Architecture yang mengirim trail file dari deployment source ke deployment target.

Komponen ini menggantikan banyak kebutuhan Data Pump pada arsitektur Microservices.

## Fungsi

- Membaca trail dari deployment source,
- Mengirim trail ke Receiver Service pada target,
- Mengelola path distribusi,
- Menyediakan monitoring pengiriman melalui web interface.

## Kapan Digunakan

Distribution Service digunakan pada implementasi OGG Microservices, seperti skenario Oracle GoldenGate 21c Oracle to Oracle dalam dokumentasi ini.
