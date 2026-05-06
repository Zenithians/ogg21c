# Distribution

Distribution Service adalah komponen pada OGG Microservices Architecture yang mengirim trail file dari deployment source ke deployment target.

Komponen ini menggantikan banyak kebutuhan Data Pump pada arsitektur Microservices.

## Fungsi

- membaca trail dari deployment source,
- mengirim trail ke Receiver Service pada target,
- mengelola path distribusi,
- menyediakan monitoring pengiriman melalui web interface.

## Kapan Digunakan

Distribution Service digunakan pada implementasi OGG Microservices, seperti skenario Oracle GoldenGate 21c Oracle to Oracle dalam dokumentasi ini.
