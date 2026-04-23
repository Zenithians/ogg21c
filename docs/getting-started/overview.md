# Gambaran Umum

## Tujuan Dokumentasi

Dokumentasi ini menjelaskan langkah-langkah lengkap untuk menginstal dan mengkonfigurasi **Oracle GoldenGate 21c** dalam arsitektur **Microservices** untuk replikasi data real-time dari database Oracle source ke Oracle target menggunakan dua Virtual Machine (VM).

---

## Skenario Replikasi

Replikasi yang diimplementasikan adalah **Unidirectional Replication** (satu arah), yaitu perubahan data di VM1 (Source) akan secara otomatis direplikasi ke VM2 (Target) secara real-time.

<div style="text-align: center;">
  <img src="../../assets/images/skenario-replicat.png" alt="Diagram Topologi OGG" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
</div>

### Tabel yang Direplikasi

| Schema | Tabel | Keterangan |
|---|---|---|
| RAFI | EMPLOYEES | Data karyawan |
| RAFI | TRANSAKSI_QRIS | Data transaksi QRIS |

---

## Alur Kerja OGG


<div style="text-align: center;">
  <img src="../../assets/images/workflow-ogg.png" alt="Diagram Topologi OGG" style="max-width: 100%; border-radius: 8px; border: 1px solid #ddd;">
</div>


---

## Versi Software

| Software | Versi |
|---|---|
| Oracle GoldenGate | 21.3.0.0.0 |
| Oracle Database | 19c (19.3.0.0.0) |
| Oracle Linux | 7 (UEK) |
| Java (JDK) | Bundled dengan OGG |

---

## File Download

| File | Keterangan | Link |
|---|---|---|
| OGG 21c untuk Oracle | Installer OGG Microservices | [Download di Oracle Software Delivery](https://edelivery.oracle.com/) |
| Oracle Database 19c | Installer Oracle DB | [Download di Oracle Technology Network](https://www.oracle.com/database/technologies/oracle19c-linux-downloads.html) |
| Oracle Linux 7 | OS yang digunakan | [Download Oracle Linux](https://yum.oracle.com/oracle-linux-isos.html) |

!!! warning "Perhatian"
    File installer OGG memerlukan akun Oracle (gratis). Daftarkan akun di [oracle.com](https://profile.oracle.com/myprofile/account/create-account.jspx).
