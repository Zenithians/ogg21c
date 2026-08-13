# Perbandingan OGG 23 Microservices vs OGG 21c

Halaman ini menyajikan perbandingan komprehensif antara **Oracle GoldenGate 23ai (Microservices Architecture)** dan **Oracle GoldenGate 21c**, mencakup arsitektur, fitur, keamanan, performa, dan rekomendasi migrasi.

---

## Ringkasan Umum

| Aspek | OGG 21c | OGG 23ai (Microservices) |
|---|---|---|
| **Tipe Rilis** | Innovation Release | Long-Term Support (LTS) |
| **Periode Premier Support** | Berakhir April 2026 | Berakhir Juni 2029 |
| **Extended Support** | Tersedia terbatas | Didukung hingga Juni 2032 |
| **Status Rekomendasi** | End of Premier Support | ✅ Versi yang direkomendasikan Oracle |

---

## Arsitektur & Deployment

| Aspek | OGG 21c | OGG 23ai (Microservices) |
|---|---|---|
| **Arsitektur yang Didukung** | Microservices + Classic (deprecated) | **Microservices Only** |
| **Classic Architecture** | Deprecated (masih bisa digunakan) | ❌ Dihapus sepenuhnya |
| **Unified Build** | ✅ Tersedia | ✅ Tersedia (schema baru) |
| **Konfigurasi Response File** | Response file 21c | ❌ Tidak kompatibel dengan 23ai |
| **Service Manager** | Terpusat | Terpisah dari administrasi deployment |
| **Direktori Deployment** | Standar | Kontrol granular yang lebih presisi |
| **Manajemen via CLI** | GGSCI + REST API | REST API dominan, GGSCI terbatas |

---

## Layanan Microservices

| Layanan | OGG 21c | OGG 23ai |
|---|---|---|
| **Service Manager** | ✅ | ✅ (redesain antarmuka) |
| **Administration Server** | ✅ | ✅ |
| **Distribution Server** | ✅ | ✅ |
| **Receiver Server** | ✅ | ✅ |
| **Performance Metrics Server** | ✅ | ✅ |
| **WebUI / GUI** | HTML5 awal | ✅ GUI modern, didesain ulang lengkap |

---

## Antarmuka Web (GUI / WebUI)

Kedua versi memiliki antarmuka berbasis web (browser) yang bisa diakses tanpa perlu instalasi client tambahan. Namun terdapat perbedaan signifikan dalam desain, fitur, dan kemudahan penggunaan.

### Akses & URL

| Aspek | OGG 21c | OGG 23ai |
|---|---|---|
| **URL Akses** | `https://<host>:<port>` | `https://<host>:<port>` |
| **Protokol** | HTTPS | HTTPS |
| **Default User** | `oggadmin` | `oggadmin` |
| **Port** | Ditentukan saat instalasi (custom) | Ditentukan saat instalasi (custom) |
| **Browser Support** | Modern browsers | Modern browsers |

### Tampilan & Desain

| Aspek | OGG 21c | OGG 23ai |
|---|---|---|
| **Gaya Desain** | Fungsional / utilitarian | Modern, bersih, dan intuitif |
| **UX/UI** | Form-based, tampilan sederhana | Redesain penuh, lebih visual |
| **Alur Setup** | Manual, familiar bagi pengguna lama | Guided step-by-step (assistant-led) |
| **Navigasi** | Standar, navigasi per service | Navigasi lebih logis dan terstruktur |
| **Responsivitas** | Standar | Ditingkatkan |

### Fitur yang Tersedia di WebUI

| Fitur WebUI | OGG 21c | OGG 23ai |
|---|---|---|
| **Kelola Extract & Replicat** | ✅ | ✅ |
| **Edit Parameter File** | ✅ | ✅ |
| **Manajemen Credentials** | ✅ | ✅ |
| **Lihat Report & Log File** | ✅ | ✅ |
| **Monitoring Real-time** | ✅ (basic) | ✅ (ditingkatkan) |
| **Manajemen Sertifikat / TLS** | ✅ | ✅ |
| **Trail File Management** | ⚠️ Terbatas / via CLI | ✅ **Terintegrasi penuh di WebUI** |
| **Data Streams Dashboard** | ❌ | ✅ Baru di 23ai |
| **Performance Advisor** | ❌ (via prosedur DB) | ✅ **Terintegrasi langsung di WebUI** |
| **Deployment Assistant** | ❌ | ✅ Panduan setup terintegrasi |
| **Health / Lag / Throughput Monitor** | ⚠️ Terbatas | ✅ Observabilitas ditingkatkan |
| **REST API via UI** | ✅ | ✅ (endpoint dioptimalkan) |

### Layanan yang Dapat Diakses via Browser

| Layanan | OGG 21c | OGG 23ai |
|---|---|---|
| **Service Manager** | ✅ Port terpisah | ✅ Port terpisah (tampilan didesain ulang) |
| **Administration Server** | ✅ Kelola Extract & Replicat | ✅ + Deployment Assistant, Performance Advisor |
| **Distribution Server** | ✅ Kelola Distribution Path | ✅ |
| **Receiver Server** | ✅ | ✅ |
| **Performance Metrics Server** | ✅ Grafik dasar | ✅ Dashboard lebih detail & interaktif |
| **Data Streams Service** | ❌ Tidak ada | ✅ Dashboard Pub/Sub, AsyncAPI |

### Ringkasan Perbedaan GUI

```
OGG 21c WebUI
  ├── Desain fungsional, form-based
  ├── Manajemen Extract / Replicat ✅
  ├── Monitoring dasar ✅
  └── Trail & Performance via CLI ⚠️

OGG 23ai WebUI
  ├── Desain modern, guided assistant ✅
  ├── Manajemen Extract / Replicat ✅
  ├── Trail File Management terintegrasi ✅
  ├── Performance Advisor langsung di UI ✅
  ├── Data Streams Dashboard (baru) ✅
  └── Monitoring Health/Lag/Throughput ditingkatkan ✅
```

---

## Extract & Replicat

| Aspek | OGG 21c | OGG 23ai |
|---|---|---|
| **Metode Capture (Oracle DB)** | Per-PDB + Multi-PDB | **Per-PDB Extract Only** (selain Downstream Capture) |
| **Integrated Replicat** | ✅ Tersedia | ⚠️ Deprecated |
| **Parallel Replicat** | ✅ Tersedia | ✅ **Metode Standar yang direkomendasikan** |
| **Auto Capture** | ✅ Diperkenalkan | ✅ Ditingkatkan |
| **Trail File Naming** | 6-digit dan standar | ❌ 6-digit naming dihapus |
| **Trace Tables** | ✅ Didukung | ❌ Dihapus |

---

## Keamanan

| Aspek | OGG 21c | OGG 23ai |
|---|---|---|
| **Enkripsi** | AES + Blowfish (deprecated) | **AES Only** — Blowfish dihapus |
| **Protokol TLS** | TLS standar | **TLS 1.3** (lebih aman) |
| **Manajemen Kredensial** | Wallet + Credential Store | **Tanpa Wallet** — menggunakan file .pem & private key |
| **Autentikasi Sertifikat** | Wallet-based | Direct .pem + private key file path |
| **Password di Parameter File** | Disarankan menggunakan alias | ❌ **Tidak diizinkan** — wajib pakai USERIDALIAS |
| **USERIDALIAS** | Direkomendasikan | ✅ **Diwajibkan** |
| **Pendekatan Keamanan** | Standard security | Zero Trust architecture ready |

---

## Performa & Fitur Data

| Aspek | OGG 21c | OGG 23ai |
|---|---|---|
| **Vector Data Type Replication** | ❌ Tidak didukung | ✅ Native support untuk Oracle 23ai VECTOR type |
| **JSON Relational Duality** | ❌ | ✅ Capture perubahan sisi dokumen langsung |
| **Blockchain/Immutable Tables** | ❌ | ✅ Logical replication didukung |
| **Data Streaming (AsyncAPI)** | ❌ | ✅ Pub/Sub via WebSockets |
| **Throughput** | Standar tinggi | Ditingkatkan untuk workload AI/ML |
| **SQL Server Connectivity** | Via driver standar | ✅ Direct connectivity (performa lebih baik) |

---

## Integrasi & Ekosistem

| Aspek | OGG 21c | OGG 23ai |
|---|---|---|
| **REST API** | ✅ Tersedia | ✅ Diperluas & dioptimalkan |
| **AsyncAPI / Data Streaming** | ❌ | ✅ Tersedia |
| **CI/CD Pipeline Support** | Terbatas | ✅ Lebih native |
| **Cloud Deployment (OCI/AWS/Azure/GCP)** | ✅ | ✅ (lebih optimal) |
| **Oracle AI/ML Workload** | Terbatas | ✅ Native (RAG pipelines, Vector DB) |
| **Heterogeneous DB Support** | Oracle, SQL Server, MySQL, PostgreSQL, DB2 | Oracle, SQL Server, MySQL, PostgreSQL, DB2 + peningkatan |

---

## Fitur yang Dihapus di OGG 23ai

Berikut adalah daftar fitur OGG 21c yang **tidak lagi tersedia** di OGG 23ai:

| Fitur Dihapus | Keterangan |
|---|---|
| Classic Architecture | Wajib migrasi ke Microservices |
| Blowfish Encryption | Gunakan AES sebagai gantinya |
| Oracle Wallet untuk sertifikat | Gunakan file .pem dan private key langsung |
| 6-digit trail file naming | Gunakan format penamaan standar baru |
| Trace Tables & parameter terkait | Fitur ini ditiadakan sepenuhnya |
| Integrated Replicat (deprecated) | Gunakan Parallel Replicat |
| Password plain-text di parameter file | Wajib menggunakan USERIDALIAS |

---

## Jalur Upgrade

```
OGG 19c (Classic)
    ──► Migrasi ke Microservices (21c) ──► Upgrade ke 23ai

OGG 21c (Microservices)
    ──► Upgrade langsung ke 23ai (jalur paling mudah)

OGG 21c (Classic)
    ──► Migrasi ke Microservices dulu ──► Upgrade ke 23ai
```

> **Catatan:** Oracle menyediakan patch migrasi khusus (contoh: Patch 33565581 / 37274898) untuk membantu proses perpindahan dari Classic Architecture ke Microservices.

---

## Rekomendasi

| Skenario | Rekomendasi |
|---|---|
| Instalasi baru | ✅ Gunakan OGG 23ai langsung |
| Sudah di 21c Microservices | ✅ Upgrade ke 23ai (migrasi mudah) |
| Masih di 21c Classic | ⚠️ Migrasi ke MA dulu, lalu upgrade ke 23ai |
| Masih di 19c | ⚠️ Pertimbangkan upgrade langsung ke 23ai |
| Workload AI/ML/Vector | ✅ **Wajib** menggunakan 23ai |

---

*Referensi: Oracle GoldenGate 23ai Documentation — [docs.oracle.com/goldengate](https://docs.oracle.com/en/middleware/goldengate/)*
