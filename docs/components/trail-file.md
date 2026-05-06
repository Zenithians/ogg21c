# Trail File

Trail file adalah file internal OGG yang menyimpan data perubahan hasil capture.

Trail menjadi penghubung antara proses capture, pengiriman, dan apply. Dengan trail file, proses Extract dan Replicat tidak harus selalu berjalan dengan kecepatan yang sama.

## Jenis Trail

| Jenis | Lokasi | Fungsi |
|---|---|---|
| Local Trail | Source | Menyimpan perubahan dari Extract utama. |
| Remote Trail | Target | Menyimpan perubahan yang sudah dikirim ke target. |

## Hal yang Perlu Diperhatikan

- kapasitas disk untuk trail,
- retention atau pembersihan trail,
- naming convention trail,
- checkpoint setiap proses yang membaca trail.
