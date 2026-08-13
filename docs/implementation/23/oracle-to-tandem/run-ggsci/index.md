---
icon: fontawesome/solid/play
---

# Menjalankan GGSCI & Konfigurasi GLOBALS

Petunjuk membuka perintah antarmuka OGG (`GGSCI`) dan melakukan pengkonfigurasian file `GLOBALS`.

---

## 1. Menjalankan GGSCI

Untuk pertama kali menjalankan GGSCI:

```tac
run ggsci
```

Output antarmuka OGG Command Interface:
```
Oracle GoldenGate Command Interface
Version 23.26.1.0.1 L06 2026-03-10 Optimized
Copyright (C) 1995, 2026, Oracle and/or its affiliates. All rights reserved.

GGSCI (\CNTH04) 1> env
```

Gunakan `exit` untuk keluar dari prompt GGSCI.

---

## 2. Membuat dan Mengkonfigurasi File GLOBALS

Buat file `GLOBALS` di direktori OGG menggunakan TEDIT:

```tac
tedit globals
```

Isikan konfigurasi DEFINE berikut ke dalam file `GLOBALS`:

```tac
ADD DEFINE =GGS_PREFIX, CLASS MAP, FILE $GGS
ADD DEFINE =GGS_AUDCFG, CLASS MAP, FILE $DATA24.GGS.AUDCFG
ADD DEFINE =tcpip^process^name, FILE $ZTC05
ADD DEFINE =_EMS_TEMPLATES, CLASS MAP, FILE $AUX01.SCRIBE.EMSNRES
```

---

## 3. Verifikasi Environment GGSCI

Jalankan kembali GGSCI dan cek environment untuk memastikan `DEFINE` sudah dimuat dengan benar:

```tac
run ggsci

GGSCI (\CNTH04) 1> env
```

Pastikan pada bagian **Current Defines** sudah terdaftar:
- `=GGS_PREFIX`
- `=GGS_AUDCFG`
- `=TCPIP^PROCESS^NAME`
- `=_EMS_TEMPLATES`
