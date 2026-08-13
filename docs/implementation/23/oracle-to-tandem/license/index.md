

# Konfigurasi Lisensi & Hak Akses (License)

Untuk menjalankan komponen OGG (seperti `AUDSERV`, `PRIVLIB`, `LOGDUMP`, `TMFARUL2`) di luar SUPER group, file executable tertentu harus dilisensikan dan diubah ownership-nya.

---

## 1. Menjalankan FUP Commands

Login ke sistem Tandem dan buka utility `FUP`:

```tac
FUP
```

Jalankan perintah lisensi dan hak akses berikut:

```tac
GIVE AUDSERV, SUPER.SUPER
SECURE AUDSERV, "NUNU", PROGID
LICENSE AUDSERV
LICENSE PRIVLIB
LICENSE (AUDSERV,PRIV*,LOGDUMP,TMFARUL2)
EXIT
```

---

## 2. Verifikasi Status Lisensi

Verifikasi bahwa file telah mendapatkan atribut `L` (Licensed) dan `P` (PROGID):

```tac
FUP INFO * WHERE LICENSED
```

### Output yang Diharapkan:

```
CODE             EOF      LAST MODIF   OWNER RWEP   TYPE   REC BL
$DATA6.GGS2326
AUDSERV       500PL       5994192           13:47    -1   NUNU
LOGDUMP       500L        6913336           13:47 201,255 GGGO
PRIVLIB       500L          31528 12Mar2026 14:29 201,255 GGGO
PRIVLIBR      500L          15544 12Mar2026 14:29 201,255 GGGO
TMFARUL2      500L         384616  3Jul2020 02:27 201,255 GGGO
```
