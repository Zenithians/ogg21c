

# Instalasi OGG pada HP NonStop (Tandem)

Panduan langkah demi langkah untuk melakukan unpak dan kompilasi modul utama Oracle GoldenGate pada environment HP NonStop (Tandem).

---

## 1. Persiapan & Unpak Package

Pastikan file installer (`GGSL06PK` dan `GGSUNPAK`) telah diunggah ke subvolume target (misalnya `$DATA27.GGS2326`).

```tac
-- Set file code GGSUNPAK menjadi 101 (TACL Code File)
FUP ALTER GGSUNPAK, CODE 101

-- Verifikasi file
FI
\CNTH04.$DATA27 GGS2326 5> FI
$DATA27.GGS2326

              CODE              EOF   LAST MODIFIED  OWNER  RWEP   PExt   SExt
GGSL06PK         0         50610404 15JUN2026 11:39 201,255 GOGO     14    112
GGSUNPAK       101             5430 15JUN2026 11:39 201,255 GOGO     14    112
README         101                0 15JUN2026 11:35 201,255 GOGO     14     14
```

Jalankan perintah `unpak` untuk melihat isi package:
```tac
unpak GGSL06PK
```

---

## 2. Menjalankan GGSUNPAK

Jalankan skrip instalasi `GGSUNPAK`:

```tac
run GGSUNPAK
```

Saat muncul konfirmasi:
- **`Installing Oracle GoldenGate at $DATA27.GGS2326. Is this correct?(Y/N)`**: Jawab `Y`

---

## 3. Building Intercept Library (GGSLIB)

`GGSUNPAK` akan menanyakan apakah ingin membangun OGG Intercept Library (`GGSLIB`):

```
Build of new GGSLIB recommended. Build now (Y/N)? Y
```

### Langkah Konfigurasi Buildmac:
1. **User Library Customization**:
   - `Do you want to include your own User Library (Y/N)`: `N`
2. **Lokasi AUDCFG**:
   - `Do you want to change the default location for the AUDCFG segment (Y/N)`: `Y`
   - `Enter the new default AUDCFG location ($VOL.SUBVOL)`: `$DATA27.GGS`
3. **Build Native Mode GGSLIBR & GGSSRL**:
   - `Build Native mode GGSLIBR & GGSSRL (Y/N)?`: `Y`
4. **SQL Catalog Option**:
   - `SQL Catalog for Compilation (X for no catalog)?`: `X`

---

## 4. Hasil Kompilasi

Skrip instalasi akan secara otomatis memicu proses BINDER dan `xld` (TNS/X Native Mode Linker) untuk menghasilkan:
- `BASELIB` & `BASELIBN`
- `GGSLIB` & `GGSLIBR`
- `GGSDLL`

Setelah proses selesai, akan muncul pesan:
```
Installation Complete.
```
