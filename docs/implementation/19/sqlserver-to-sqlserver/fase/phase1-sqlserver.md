---
icon: fontawesome/solid/file-arrow-down
---

# Install SQL Server 2019 & SSMS

## Download SQL Server 2019 Developer

Buka halaman download resmi Microsoft:

- URL: [https://www.microsoft.com/en-us/sql-server/sql-server-downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- Cari **SQL Server 2019** → pilih **Download Developer Edition**
- Atau download langsung: [https://go.microsoft.com/fwlink/p/?linkid=866658](https://go.microsoft.com/fwlink/p/?linkid=866658)

## Instalasi SQL Server 2019

1. Jalankan installer → pilih **Custom**
2. Pada **Feature Selection**, centang:
    -  **Database Engine Services** *(wajib)*
    -  **SQL Server Replication** *(wajib untuk OGG CDC)*
3. Pada **Instance Configuration** → pilih **Named Instance** → isi: `MSQL2019` *(sesuaikan)*
4. Ikuti wizard hingga selesai

!!! warning "Named Instance"
    Pastikan nama instance ditulis dengan benar karena akan digunakan di seluruh konfigurasi OGG. Contoh: `DESKTOP-MVMVJSO\MSQL2019`

## Instalasi SSMS (SQL Server Management Studio)

1. Download dari: [https://aka.ms/ssmsfullsetup](https://aka.ms/ssmsfullsetup)
2. Jalankan `SSMS-Setup-ENU.exe` sebagai **Administrator**
3. Klik **Install** → tunggu selesai → **Restart PC**

## Connect SSMS ke SQL Server 2019

Buka SSMS, isi koneksi:

```
Server name    : DESKTOP-MVMVJSO\MSQL2019
Authentication : Windows Authentication
```

Klik **Connect** → pastikan **Object Explorer** muncul.

!!! success "Verifikasi"
    Jika Object Explorer berhasil menampilkan tree database, maka SQL Server 2019 sudah terinstall dan berjalan dengan benar.
