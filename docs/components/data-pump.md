---
icon: fontawesome/solid/share
---

# Data Pump

Data Pump adalah Extract tambahan yang membaca local trail di sisi source dan mengirimkannya ke target.

Data Pump umum digunakan pada OGG Classic Architecture. Dengan Data Pump, Extract utama tidak langsung bergantung pada koneksi jaringan ke target.

## Fungsi

- Membaca local trail,
- Mengirim data perubahan ke host target,
- Menulis remote trail,
- Membantu isolasi gangguan jaringan dari proses capture utama.

## Manfaat

Jika koneksi target bermasalah, Extract utama tetap bisa menulis local trail selama disk source masih cukup. Setelah jaringan pulih, Data Pump dapat melanjutkan pengiriman.
