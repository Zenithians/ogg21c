---
icon: fontawesome/solid/terminal
---

# Referensi Command GGSCI

Daftar lengkap perintah GGSCI (GoldenGate Software Command Interface) yang digunakan dalam operasional OGG.

## Perintah Umum

| Perintah | Fungsi |
|----------|--------|
| `INFO ALL` | Melihat status semua proses |
| `STATUS MGR` | Cek status Manager |
| `START MGR` | Menjalankan Manager |
| `STOP MGR` | Menghentikan Manager |
| `CREATE SUBDIRS` | Membuat folder-folder OGG |

## Perintah Extract & Pump

| Perintah | Fungsi |
|----------|--------|
| `ADD EXTRACT <nama>, TRANLOG, BEGIN NOW` | Menambahkan group Extract baru |
| `ADD EXTRACT <nama>, EXTTRAILSOURCE <path>` | Menambahkan group Pump baru |
| `START EXTRACT <nama>` | Menjalankan Extract/Pump |
| `STOP EXTRACT <nama>` | Menghentikan Extract/Pump |
| `DELETE EXTRACT <nama>` | Menghapus group Extract/Pump |
| `INFO EXTRACT <nama>` | Informasi detail suatu Extract |
| `STATS EXTRACT <nama>` | Statistik operasi Extract |
| `LAG EXTRACT <nama>` | Cek keterlambatan Extract |
| `VIEW REPORT <nama>` | Melihat log report proses |

## Perintah Replicat

| Perintah | Fungsi |
|----------|--------|
| `ADD REPLICAT <nama>, EXTTRAIL <path>, CHECKPOINTTABLE <tabel>` | Menambahkan group Replicat baru |
| `START REPLICAT <nama>` | Menjalankan Replicat |
| `STOP REPLICAT <nama>` | Menghentikan Replicat |
| `DELETE REPLICAT <nama>` | Menghapus group Replicat |
| `INFO REPLICAT <nama>` | Informasi detail suatu Replicat |
| `STATS REPLICAT <nama>` | Statistik operasi Replicat |
| `LAG REPLICAT <nama>` | Cek keterlambatan Replicat |

## Perintah Trail File

| Perintah | Fungsi |
|----------|--------|
| `ADD EXTTRAIL <path>, EXTRACT <nama>, MEGABYTES <size>` | Menambahkan local trail file |
| `ADD RMTTRAIL <path>, EXTRACT <nama>, MEGABYTES <size>` | Menambahkan remote trail file |
| `INFO EXTTRAIL <path>` | Informasi trail file lokal |
| `INFO RMTTRAIL <path>` | Informasi remote trail file |

## Perintah Database & Tabel

| Perintah | Fungsi |
|----------|--------|
| `DBLOGIN SOURCEDB <db>, USERID <user>, PASSWORD <pass>` | Login ke database |
| `ADD TRANDATA <schema.tabel>` | Aktifkan supplemental logging pada tabel |
| `DELETE TRANDATA <schema.tabel>` | Nonaktifkan supplemental logging |
| `INFO TRANDATA <schema.tabel>` | Cek status supplemental logging |
| `ADD CHECKPOINTTABLE <schema.tabel>` | Buat checkpoint table di target |

## Perintah Konfigurasi

| Perintah | Fungsi |
|----------|--------|
| `EDIT PARAMS <nama>` | Edit parameter file via text editor |
| `VIEW PARAMS <nama>` | Tampilkan isi parameter file |

---

## Contoh Urutan Start Lengkap

### Source

```
GGSCI> DBLOGIN SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"
GGSCI> START MGR
GGSCI> START EXTRACT ext1
GGSCI> START EXTRACT pump1
GGSCI> INFO ALL
```

### Target

```
GGSCI> DBLOGIN SOURCEDB DRC, USERID ggadmin, PASSWORD "OGGAdmin123!"
GGSCI> START MGR
GGSCI> START REPLICAT rep1
GGSCI> INFO ALL
```

## Contoh Urutan Stop Lengkap

```
-- Di Source
GGSCI> STOP EXTRACT pump1
GGSCI> STOP EXTRACT ext1
GGSCI> STOP MGR

-- Di Target
GGSCI> STOP REPLICAT rep1
GGSCI> STOP MGR
```
