# Konfigurasi Credential OGG

Credential OGG digunakan oleh Extract dan Replicat untuk login ke Oracle Database.

---

## Buat Credential di VM1 (Source)

### Akses Administration Service VM1

Buka browser dan akses:
```
http://192.168.245.132:9001
```

Login: `ggadmin` / `@Rafi1234`

### Tambah Credential

1. Klik menu **≡ (hamburger)** → **Configuration**
2. Pilih tab **Credentials**
3. Klik tombol **+**
4. Isi form:

| Field | Nilai |
|---|---|
| Credential Domain | `OracleGoldenGate` |
| Credential Alias | `srcdb` |
| User ID | `ggadmin@ORCL` |
| Password | `yourpassword` |

5. Klik **Submit**
6. Klik icon **=** untuk test koneksi


<div style="text-align: center;">
  <img src="../../assets/images/credential-vm1.png" alt="Credential VM1" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
  <p><em>Screenshot halaman Credentials di Administration Service VM1</em></p>
</div>

!!! success "Berhasil"
    Jika test koneksi berhasil, akan muncul informasi **Trandata** dan **Checkpoint** di bawah credential.

---

## Buat Credential di VM2 (Target)

### Akses Administration Service VM2

```
http://192.168.245.133:9001
```

Login: `ggadmin` / `@Rafi1234`

### Tambah Credential

1. Klik menu **≡** → **Configuration** → **Credentials**
2. Klik **+**
3. Isi form:

| Field | Nilai |
|---|---|
| Credential Domain | `OracleGoldenGate` |
| Credential Alias | `tgtdb` |
| User ID | `ggadmin@//192.168.245.133:1521/ORCL` |
| Password | `yourpassword` |

4. Klik **Submit**
5. Test koneksi dengan klik icon **=**

<div style="text-align: center;">
  <img src="../../assets/images/kredensial-vm2.png" alt="Credential VM2" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
  <p><em>Screenshot halaman Credentials di Administration Service VM2</em></p>
</div>

---

## Daftarkan Checkpoint Table di VM2

Setelah credential `tgtdb` terhubung:

1. Scroll ke bawah ke bagian **Checkpoint**
2. Klik **+**
3. Isi: `GGADMIN.CHECKPOINTTABLE`
4. Klik **Submit**

<div style="text-align: center;">
  <img src="../../assets/images/checkpoint-vm2.png" alt="Checkpoint VM2" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
  <p><em>Screenshot pendaftaran checkpoint table</em></p>
</div>

---

## Manajemen User OGG

User untuk login ke Web GUI OGG dikelola di Service Manager.

### Tambah User Baru via adminclient

```bash
# Login sebagai oracle di VM1
/u01/app/ogg/bin/adminclient
```

Setelah masuk adminclient:
```
connect http://192.168.245.132:55000 deployment oggsource as ggadmin password @Rafi1234
create user namauser password Password123# role administrator
info security users *
exit
```

### Role yang Tersedia

| Role | Keterangan |
|---|---|
| `Administrator` | Akses penuh ke semua fitur |
| `Operator` | Bisa start/stop process |
| `Viewer` | Hanya bisa melihat status |
