---
icon: fontawesome/solid/file-code
---

# Menjalankan DEFGEN untuk Modul T24

Panduan eksekusi utility `DEFGEN` untuk menghasilkan file definisi tabel/file Enscribe/DDL yang digunakan oleh OGG pada integrasi T24.

---

## 1. Persiapan File Enscribe T24 (FUP)

Sebelum menjalankan DEFGEN, persiapakan struktur file melalui `FUP`:

```tac
FUP
-SET TYPE E
-SET FORMAT 2
-SET EXT( 4, 32 )
-SET REC 4048
-SET BLOCK 4096
-SET ALTKEY ( "CR", FILE 0, KEYOFF 38, KEYLEN 30 )
-SET ALTKEY ( "TR", FILE 0, KEYOFF 14, KEYLEN 24 )
-SET ALTFILE ( 0, $DATA24.T24.T24TLFD0 )
-SET NO ALTCREATE
-SET MAXEXTENTS 100
-CREATE T24TLFDF
-EXIT
```

---

## 2. Eksekusi Utility DEFGEN

Jalankan utility `DEFGEN` dengan opsi pemrosesan struktur DDL:

```tac
RUN DEFGEN EXPANDDDL RESOLVEDUPGROUP OMITREDEFS
```

### Prompt Input Data:

1. **`Enter definitions file name (or Exit)`**: `T24DEF.T24TLF`
2. **`File/Table to create definition for (or Exit)`**: `T24.T24TLFDF`
3. **`Include DDL record definition (Y/N)?`**: `Y`
4. **`DDL dictionary:`**: `$DATA24.T24`
5. **`DDL record or definition name:`**: `T24-TLF`
6. **`File/Table to create definition for (or Exit)`**: `EXIT`

DEFGEN akan memproses skema, menghapus definisi *redefines*, merapikan nama field, dan menyimpan hasilnya.

---

## 3. Verifikasi File Definisi Target

Pastikan file definisi berhasil dibuat:

```tac
FI 24 T24DEF.*
```

Contoh output:
```
$DATA24.T24DEF

              CODE              EOF   LAST MODIFIED  OWNER  RWEP   PExt   SExt
README         101                0 02JUL2026 16:10 202,255 GOGO     14     14
T24TLF         101            11042 02JUL2026 17:51 202,255 GOGO     14     28
```
