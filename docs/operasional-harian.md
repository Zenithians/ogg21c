# Monitoring dan Operasional Harian

Operasional harian OGG bertujuan memastikan proses replikasi tetap running, lag terkendali, dan tidak ada error tersembunyi.

## Checklist Harian

- Cek semua proses OGG running.
- Cek lag Extract, Pump atau Distribution, dan Replicat.
- Cek report file terbaru.
- Cek event log.
- Cek disk space trail.
- Cek transaksi yang gagal di discard file.
- Cek koneksi antar host.
- Cek data sample di source dan target jika diperlukan.

## Cek Status Proses

Classic Architecture:

```text
GGSCI> INFO ALL
GGSCI> INFO EXTRACT <nama_extract>, DETAIL
GGSCI> INFO REPLICAT <nama_replicat>, DETAIL
```

Microservices Architecture:

- Buka Administration Service,
- Cek halaman Overview,
- Cek status Extract dan Replicat,
- Buka Distribution Service untuk status path,
- Buka Receiver Service di target.

## Cek Lag

Classic Architecture:

```text
GGSCI> LAG EXTRACT <nama_extract>
GGSCI> LAG REPLICAT <nama_replicat>
```

Microservices Architecture:

- Cek kolom lag di web UI,
- Cek Statistics,
- Cek Performance Metrics Service jika tersedia.

## Start dan Stop Process

Classic Architecture:

```text
GGSCI> START EXTRACT <nama_extract>
GGSCI> STOP EXTRACT <nama_extract>
GGSCI> START REPLICAT <nama_replicat>
GGSCI> STOP REPLICAT <nama_replicat>
```

Microservices Architecture:

- Gunakan tombol start/stop di Administration Service,
- Atau gunakan Admin Client sesuai deployment.

## Cek Report File

Classic Architecture:

```text
GGSCI> VIEW REPORT <nama_process>
```

Report file biasanya berisi:

- Waktu process start,
- Parameter yang dibaca,
- Error detail,
- Statistik operasi,
- Posisi trail.

## Cek Trail File

Pastikan trail bertambah saat ada transaksi dan tidak menumpuk terlalu lama.

Contoh Linux:

```bash
ls -lh ./dirdat
```

Contoh Windows:

```powershell
Get-ChildItem C:\OGG\source\dirdat
```

## Maintenance Aman

Sebelum maintenance:

1. Cek lag sampai mendekati nol.
2. Stop proses secara berurutan.
3. Catat checkpoint terakhir.
4. Backup parameter file penting.
5. Jalankan maintenance.
6. Start proses kembali.
7. Cek report dan lag.

## Urutan Stop yang Disarankan

Untuk replikasi satu arah:

```text
Stop Extract
Stop Data Pump / Distribution
Stop Replicat
```

Pada beberapa kasus, Replicat dibiarkan menyelesaikan apply dulu sebelum dihentikan.

## Urutan Start yang Disarankan

```text
Start Manager atau service utama
Start Replicat
Start Data Pump / Distribution
Start Extract
```

Urutan ini membantu target siap menerima data sebelum source mulai mengirim perubahan baru.

## Indikator Replikasi Sehat

Replikasi bisa dianggap sehat jika:

- Semua proses running,
- Lag stabil dan rendah,
- Tidak ada error baru di report,
- Trail tidak menumpuk berlebihan,
- Data sample source dan target sesuai,
- Tidak ada record baru di discard file.
