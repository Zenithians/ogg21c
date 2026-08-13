

# Instalasi Modul T24 & NLDEXIT

Langkah-langkah untuk melakukan unpak modul T24 dan membangun file executable `NEXTRACT` yang digabungkan dengan User Exit (`T24UE`).

---

## 1. Unpak Modul T24

Masuk ke volume/subvolume T24 (misalnya `$DATA27.T24`):

```tac
v t24
FUP ALTER X24UNPAK, CODE 101
RUN X24UNPAK T24
```

Jawab `Y` saat konfirmasi pemrosesan unpak object file.

---

## 2. Pembangunan Executable Baru Menggunakan NLDEXIT

Kembali ke subvolume OGG utama (misal `$DATA27.GGS2326`) lalu jalankan `NLDEXIT`:

```tac
v ggs2326
RUN NLDEXIT
```

### Interaksi Prompt NLDEXIT:

1. **`OGG Object Type`**: ketik `extract`
2. **`Enter location of userexit object`**: ketik `$DATA27.T24.T24UE`
3. **`Enter name for new object file`**: ketik `NEXTRACT`
4. **`Does your User Exit contain C++ modules (Y/N)`**: `N`
5. **`Does your User Exit contain Cobol modules (Y/N)`**: `N`
6. **`SQL Catalog for SQLCOMP (or N to avoid SQL compile)`**: `N`

Output:
```
New EXTRACT file $DATA27.GGS2326.NEXTRACT created with user exits.
```

---

## 3. Duplikasi Library dan Swap Executable

Lakukan backup executable Extract lama dan ganti dengan `NEXTRACT`:

```tac
FUP DUP GGSLIB, $ZIT01.XPNET.*, SOURCEDATE
FUP RENAME EXTRACT, OEXTRACT
FUP RENAME NEXTRACT, EXTRACT
```

Verifikasi file `EXTRACT` baru dengan perintah:
```tac
FI *EX*
```
