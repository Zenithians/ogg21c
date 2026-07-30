---
icon: fontawesome/solid/file-lines
---

# Trail File

Trail file adalah file internal OGG yang menyimpan data perubahan hasil capture.

Trail menjadi penghubung antara proses capture, pengiriman, dan apply. Dengan trail file, proses Extract dan Replicat tidak harus selalu berjalan dengan kecepatan yang sama.

## Jenis Trail

| Jenis | Lokasi | Fungsi |
|---|---|---|
| Local Trail | Source | Menyimpan perubahan dari Extract utama. |
| Remote Trail | Target | Menyimpan perubahan yang sudah dikirim ke target. |

## Hal yang Perlu Diperhatikan

- Kapasitas disk untuk trail,
- Retention atau pembersihan trail,
- Naming convention trail,
- Checkpoint setiap proses yang membaca trail.
