---
icon: fontawesome/solid/terminal
---

# Konfigurasi BINDSKEL & Kompilasi SKELBN

Macro `BINDSKEL` digunakan untuk melakukan re-bind dan akselerasi library `SKELBN` yang digunakan oleh proses OGG/XPNET.

---

## 1. Memeriksa / Edit Skrip BINDSKEL

Pastikan skrip `BINDSKEL` mengarah pada file `SKELB` dan `SKELBN` yang benar (misalnya di `$AUX01.XPNET.*`).

```tac
TEDIT BINDSKEL
```

### Isi Macro TACL `BINDSKEL`:

```tac
?tacl macro
#frame
#push bindin fl modts modts2
#push axcel_out
#push _accelerator
#push _cmd
#push _nsk_version _os1 _os2

sink [#definedelete =skelb]
sink [#definedelete =skelbn]
sink [#definedelete =baselib]

add define =skelb, class map, file $AUX01.XPNET.SKELB
add define =skelbn, class map, file $AUX01.XPNET.SKELBN
add define =baselib, class map, file baselib

GET_OSVERSION

#set modts 0
[#if [#fileinfo /existence/ =skelbn] | then |
     #set modts [#fileinfo /modification/ =skelbn]
]

[#set bindin
add * from =skelb
add * from =baselib, delete
set highpin on
set highrequesters on
set runnamed on
build =skelbn !, list * off
]

bind /inv bindin/

#unframe
```

---

## 2. Menjalankan BINDSKEL

Jalankan perintah berikut pada TACL:

```tac
RUN BINDSKEL
```

### Output yang Diharapkan:

```
BINDER - OBJECT FILE BINDER - T9621H01   SYSTEM \ARTA04
...
Object file \ARTA03.$AUX01.XPNET.SKELBN created successfully, accelerating code...
OCAX /name, outv axcel_out/ \ARTA04.$AUX01.XPNET.SKELBN; UL
Acceleration finished for \ARTA04.$AUX01.XPNET.SKELBN.
```

---

## 3. Verifikasi File Hasil Build

Periksa status file `SKELBN` dan versi binary `EXTRACT`:

```tac
FI $*.*.SKELB*
VPROC extract
```
