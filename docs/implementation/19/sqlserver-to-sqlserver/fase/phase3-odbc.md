# Phase 3 — Instalasi ODBC Driver 17

!!! warning "Versi Driver"
    OGG 21.4 hanya mendukung **ODBC Driver 17**. Jangan gunakan Driver 18 karena tidak kompatibel (`OGG-05312: msodbcsql18.dll not supported`).

## 3.1 Download & Install

1. Download ODBC Driver 17: [https://go.microsoft.com/fwlink/?linkid=2168524](https://go.microsoft.com/fwlink/?linkid=2168524)
2. Pilih **ODBC Driver 17** for SQL Server
3. Klik kanan installer → **Run as Administrator** → Install

## 3.2 Buat DSN PROD2

1. Buka **ODBC Data Sources (64-bit)**
2. Tab **System DSN** → klik **Add** → pilih **ODBC Driver 17 for SQL Server**
3. Isi form:

    ```
    Name   : PROD2
    Server : DESKTOP-MVMVJSO\MSQL2019
    ```

4. Pilih **SQL Server Authentication**:

    ```
    Login ID : ggadmin
    Password : OGGAdmin123!
    ```

5. Pada halaman enkripsi:

    ```
    Use strong encryption : ☐ (jangan dicentang)
    Trust server certificate : ☑ (centang)
    ```

6. Klik **Finish** → **Test Data Source** → harus muncul:

    ```
    TESTS COMPLETED SUCCESSFULLY
    ```

## 3.3 Buat DSN DRC

Ulangi langkah yang sama seperti pembuatan DSN PROD2, dengan perubahan:

```
Name   : DRC
Server : DESKTOP-MVMVJSO\MSQL2019
```

Kredensial login tetap sama (`ggadmin` / `OGGAdmin123!`).

!!! success "Verifikasi"
    Kedua DSN (`PROD2` dan `DRC`) harus berhasil menampilkan `TESTS COMPLETED SUCCESSFULLY` sebelum melanjutkan ke fase berikutnya.
