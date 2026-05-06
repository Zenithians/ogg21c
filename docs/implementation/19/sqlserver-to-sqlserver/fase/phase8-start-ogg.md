# Phase 8 — Menjalankan OGG

## 8.1 Start Source OGG

Buka CMD as Administrator, jalankan:

```cmd
cd C:\OGG\source
ggsci.exe
```

Di dalam GGSCI, jalankan perintah berikut **secara berurutan**:

```
GGSCI> DBLOGIN SOURCEDB PROD2, USERID ggadmin, PASSWORD "OGGAdmin123!"

GGSCI> START MGR

GGSCI> ADD EXTRACT ext1, TRANLOG, BEGIN NOW

GGSCI> ADD EXTTRAIL ./dirdat/lt, EXTRACT ext1, MEGABYTES 50

GGSCI> ADD EXTRACT pump1, EXTTRAILSOURCE ./dirdat/lt

GGSCI> ADD RMTTRAIL C:\OGG\target\dirdat\rt, EXTRACT pump1, MEGABYTES 50

GGSCI> START EXTRACT ext1

GGSCI> START EXTRACT pump1

GGSCI> INFO ALL
```

!!! warning "Urutan Penting"
    Jalankan `START MGR` terlebih dahulu sebelum menambahkan atau menjalankan Extract dan Pump.

## 8.2 Start Target OGG

Buka CMD **baru** as Administrator, jalankan:

```cmd
cd C:\OGG\target
ggsci.exe
```

Di dalam GGSCI:

```
GGSCI> DBLOGIN SOURCEDB DRC, USERID ggadmin, PASSWORD "OGGAdmin123!"

GGSCI> START MGR

GGSCI> ADD CHECKPOINTTABLE ggadmin.chkpt

GGSCI> ADD REPLICAT rep1, EXTTRAIL ./dirdat/rt, CHECKPOINTTABLE ggadmin.chkpt

GGSCI> START REPLICAT rep1

GGSCI> INFO ALL
```

## 8.3 Output yang Diharapkan

Setelah semua proses berjalan, `INFO ALL` harus menampilkan:

```
Program     Status      Group       Lag at Chkpt  Time Since Chkpt
MANAGER     RUNNING
EXTRACT     RUNNING     EXT1        00:00:00      00:00:xx
EXTRACT     RUNNING     PUMP1       00:00:00      00:00:xx
REPLICAT    RUNNING     REP1        00:00:00      00:00:xx
```

!!! success "Semua Proses RUNNING"
    Jika semua proses berstatus `RUNNING` dengan Lag `00:00:00`, konfigurasi OGG berhasil dan siap melakukan replikasi real-time.

!!! danger "Jika Ada Status ABENDED"
    Jika ada proses dengan status `ABENDED`, cek log error dengan:
    ```
    GGSCI> VIEW REPORT <nama_proses>
    ```
    Kemudian lihat bagian [Troubleshooting](../referensi/troubleshooting.md) untuk solusinya.
