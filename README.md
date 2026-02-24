# 🛡️ SafeStair — Stair Handrail Compliance Detection System

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/YOLOv8-Ultralytics-purple?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/FastAPI-0.104+-green?style=for-the-badge&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/React-18+-61DAFB?style=for-the-badge&logo=react&logoColor=black"/>
  <img src="https://img.shields.io/badge/SQLite-Database-003B57?style=for-the-badge&logo=sqlite&logoColor=white"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  <strong>Sistem monitoring berbasis Computer Vision dan AI untuk mendeteksi kepatuhan penggunaan handrail di area tangga secara real-time.</strong>
</p>

<p align="center">
  <a href="#-project-brief">Project Brief</a> •
  <a href="#-latar-belakang">Latar Belakang</a> •
  <a href="#-tujuan-proyek">Tujuan</a> •
  <a href="#-fitur-sistem">Fitur</a> •
  <a href="#-instalasi">Instalasi</a> •
  <a href="#-training-model">Training</a> •
  <a href="#-api-endpoints">API</a>
</p>

---

## 📋 Daftar Isi

### 📄 Dokumentasi Proyek
- [Project Brief](#-project-brief)
- [Latar Belakang](#-latar-belakang)
- [Rumusan Masalah](#-rumusan-masalah)
- [Tujuan Proyek](#-tujuan-proyek)
- [Ruang Lingkup](#-ruang-lingkup)
- [Metodologi](#-metodologi)
- [Manfaat Sistem](#-manfaat-sistem)
- [Batasan Sistem](#-batasan-sistem)

### 🔧 Dokumentasi Teknis
- [Fitur Sistem](#-fitur-sistem)
- [Arsitektur Sistem](#-arsitektur-sistem)
- [Alur Deteksi](#-alur-deteksi)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Struktur Folder](#-struktur-folder)
- [Database Schema](#-database-schema)

### 🚀 Panduan Penggunaan
- [System Requirements](#-system-requirements)
- [Instalasi](#-instalasi)
- [Training Model](#-training-model)
- [Anotasi Dataset](#-anotasi-dataset)
- [Menjalankan Sistem](#-menjalankan-sistem)
- [API Endpoints](#-api-endpoints)
- [Konfigurasi](#-konfigurasi)
- [Troubleshooting](#-troubleshooting)

### 📎 Lainnya
- [Roadmap](#-roadmap)
- [Kontribusi](#-kontribusi)
- [Lisensi](#-lisensi)
- [Author](#-author)

---

<br>

# 📄 DOKUMENTASI PROYEK

---

## 📌 Project Brief

| Item | Detail |
|------|--------|
| **Nama Proyek** | SafeStair — Stair Handrail Compliance Detection System |
| **Versi** | 1.0.0 |
| **Kategori** | Computer Vision / AI Safety Monitoring |
| **Domain** | Keselamatan Kerja (Occupational Safety & Health / K3) |
| **Platform** | Web-based (Local / On-Premise) |
| **Bahasa Pemrograman** | Python 3.10+, JavaScript (React) |
| **Status Proyek** | Active Development |
| **Lisensi** | MIT License |

### Deskripsi Singkat

SafeStair adalah sistem monitoring keselamatan berbasis kecerdasan buatan yang dirancang untuk mendeteksi dan mencatat pelanggaran penggunaan handrail di area tangga secara **otomatis** dan **real-time**. Sistem ini menggunakan model **YOLOv8 Instance Segmentation** yang telah dilatih untuk mengenali tiga objek kunci: orang (`person`), batang pegangan tangga (`handrail`), dan titik kontak tangan (`wrist_contact`). Dengan menganalisis hubungan geometris antara ketiga objek tersebut, sistem secara independen mengevaluasi kepatuhan setiap individu, mengaktifkan alarm saat pelanggaran terdeteksi, menyimpan bukti foto, dan menyajikan seluruh data melalui dashboard web yang intuitif.

---

## 🏢 Latar Belakang

Kecelakaan di area tangga merupakan salah satu penyebab cedera paling umum di lingkungan industri, perkantoran, fasilitas kesehatan, dan fasilitas umum. Berbagai studi di bidang keselamatan kerja menunjukkan bahwa **jatuh di tangga** menyumbang persentase signifikan dari total kecelakaan kerja setiap tahunnya, dengan banyak kasus mengakibatkan cedera serius bahkan kematian.

Sebagian besar insiden jatuh di tangga dapat dicegah apabila pengguna secara konsisten **memegang handrail** saat naik atau turun. Handrail berfungsi sebagai titik keseimbangan dan titik pegangan darurat yang dapat mencegah seseorang terjatuh ketika tersandung atau kehilangan keseimbangan.

### Tantangan Pengawasan Konvensional

Dalam praktiknya, pengawasan manual terhadap kepatuhan penggunaan handrail menghadapi berbagai keterbatasan:

- **Keterbatasan sumber daya manusia** — Seorang petugas keamanan tidak dapat memantau semua area tangga secara bersamaan dan 24 jam penuh
- **Faktor kelelahan** — Pengawasan manual rentan terhadap menurunnya kewaspadaan seiring berjalannya waktu
- **Tidak ada rekam jejak** — Pelanggaran yang tidak diamati secara langsung tidak tercatat sehingga sulit untuk evaluasi
- **Efektivitas rambu** — Pemasangan rambu peringatan dan kampanye keselamatan sering kali tidak cukup efektif untuk mengubah perilaku pengguna secara permanen

### Peluang Teknologi

Kemajuan teknologi **Computer Vision** dan **Deep Learning**, khususnya model deteksi objek berbasis YOLO *(You Only Look Once)*, membuka peluang besar untuk membangun sistem monitoring otomatis yang mampu:

- Bekerja **24/7 tanpa kelelahan**
- Mendeteksi pelanggaran secara **akurat dan konsisten**
- Memberikan **bukti visual** yang terstruktur
- Menghasilkan **laporan otomatis** untuk keperluan audit dan evaluasi

Proyek ini hadir sebagai jawaban atas kebutuhan tersebut — sebuah sistem AI yang terjangkau, dapat dikustomisasi, dan dapat diimplementasikan menggunakan infrastruktur kamera yang sudah ada.

---

## ❓ Rumusan Masalah

Berdasarkan latar belakang di atas, proyek ini berupaya menjawab rumusan masalah berikut:

1. **Bagaimana** membangun sistem yang mampu mendeteksi secara otomatis apakah seseorang yang berada di area tangga memegang handrail atau tidak, tanpa memerlukan intervensi atau pengawasan manusia secara langsung?

2. **Bagaimana** sistem dapat membedakan antara orang yang sedang aktif menggunakan tangga dengan orang yang sekadar berada di dekat area tangga, untuk menghindari false alarm yang tidak relevan?

3. **Bagaimana** mengatasi masalah *false alarm* yang disebabkan oleh pergerakan sesaat — misalnya seseorang melepas pegangan hanya selama 1–2 frame video yang bukan merupakan pelanggaran nyata?

4. **Bagaimana** menyimpan bukti pelanggaran secara otomatis beserta metadata yang relevan (waktu kejadian, foto, identifikasi orang) untuk keperluan dokumentasi dan tindak lanjut?

5. **Bagaimana** menyajikan data monitoring dan riwayat pelanggaran dalam antarmuka web yang mudah digunakan oleh petugas keamanan atau manajemen, tanpa memerlukan keahlian teknis khusus?

---

## 🎯 Tujuan Proyek

### Tujuan Umum

Membangun sistem monitoring kepatuhan penggunaan handrail berbasis Computer Vision dan Kecerdasan Buatan yang dapat bekerja secara real-time, otomatis, dan akurat untuk mendukung program keselamatan kerja di area tangga.

### Tujuan Khusus

1. **Mengimplementasikan model YOLOv8 Instance Segmentation** yang mampu mendeteksi tiga objek kunci secara bersamaan dalam satu frame: `person` (orang), `handrail` (batang pegangan), dan `wrist_contact` (titik kontak tangan dengan handrail).

2. **Membangun mekanisme tracking multi-person** menggunakan Centroid Tracker berbasis IoU agar setiap individu dalam frame dipantau secara independen dengan ID unik yang konsisten antar frame selama satu sesi monitoring.

3. **Mengembangkan logika compliance check** berbasis analisis geometris (overlap mask) yang secara akurat menentukan apakah pergelangan tangan seseorang benar-benar bersinggungan dengan area handrail pada level piksel.

4. **Menerapkan temporal filtering** untuk menekan false alarm dengan mewajibkan kondisi pelanggaran terjadi secara konsisten selama minimal 1 detik (≈ 20 frame pada 20 FPS) sebelum alarm dipicu.

5. **Mengintegrasikan sistem dengan backend FastAPI dan database SQLite** untuk pencatatan otomatis setiap pelanggaran yang terconfirm, beserta foto bukti, timestamp, dan metadata terkait.

6. **Membangun web dashboard berbasis React** yang menyajikan live video stream dengan overlay deteksi, statistik kepatuhan real-time, dan riwayat pelanggaran yang dapat diakses melalui browser.

---

## 🗺️ Ruang Lingkup

### Yang Termasuk dalam Sistem *(In-Scope)*

- ✅ Deteksi orang yang berada di area tangga dari feed satu kamera
- ✅ Deteksi handrail secara otomatis tanpa konfigurasi ROI manual
- ✅ Deteksi apakah tangan menyentuh handrail menggunakan instance segmentation
- ✅ Tracking multi-person dengan ID unik per individu per sesi
- ✅ Temporal filtering untuk menekan false alarm
- ✅ Penyimpanan bukti foto pelanggaran secara otomatis
- ✅ Pencatatan data pelanggaran ke database dengan metadata lengkap
- ✅ REST API untuk akses data oleh aplikasi lain
- ✅ Web dashboard monitoring real-time berbasis React
- ✅ Live video stream dengan visualisasi anotasi
- ✅ Statistik dan grafik tren pelanggaran harian

### Yang Tidak Termasuk *(Out-of-Scope)*

- ❌ Identifikasi identitas orang secara permanen (face recognition)
- ❌ Dukungan multi-kamera secara bersamaan
- ❌ Notifikasi eksternal otomatis (email/SMS/WhatsApp) — dijadwalkan di roadmap v1.1
- ❌ Deployment ke server cloud atau jaringan publik
- ❌ Integrasi langsung dengan sistem CCTV / NVR yang sudah ada
- ❌ Dukungan kamera thermal / infrared / night vision
- ❌ Autentikasi pengguna untuk dashboard web

---

## 🔬 Metodologi

Pengembangan sistem ini mengikuti pendekatan iteratif yang terbagi dalam tiga fase utama sesuai dengan komponen sistem:

```
┌───────────────────────────────────────────────────────────────────┐
│                      ALUR PENGEMBANGAN                            │
├───────────────────────────────────────────────────────────────────┤
│                                                                   │
│  FASE 0 — PERSIAPAN DATA                                         │
│  ├── Rekam video di area tangga (berbagai kondisi)                │
│  ├── Ekstraksi frame dari video (1 frame / 0.5 detik)             │
│  ├── Upload ke Roboflow                                           │
│  ├── Anotasi 3 class: person, handrail, wrist_contact             │
│  ├── Augmentasi data (flip, rotasi, brightness, blur)             │
│  └── Export dataset format YOLOv8                                 │
│                                                                   │
│  FASE 1 — AI ENGINE                                               │
│  ├── Training YOLOv8m-seg di Google Colab (GPU T4)                │
│  ├── Evaluasi: mAP50, Precision, Recall                           │
│  ├── Export model terbaik (best.pt)                               │
│  ├── detector.py — YOLOv8 inference & mask extraction             │
│  ├── compliance.py — geometric overlap analysis                   │
│  └── tracker.py — centroid tracking per person                    │
│                                                                   │
│  FASE 2 — BACKEND                                                 │
│  ├── FastAPI server (main.py)                                     │
│  ├── Camera processing loop (background thread)                   │
│  ├── MJPEG stream endpoint                                        │
│  ├── SQLAlchemy + SQLite integration (database.py)                │
│  └── REST API endpoints                                           │
│                                                                   │
│  FASE 3 — FRONTEND                                                │
│  ├── React app setup                                              │
│  ├── Dashboard — statistik overview                               │
│  ├── Live Monitor — stream + real-time status                     │
│  ├── Violation Logs — tabel + preview foto                        │
│  └── Statistics — grafik tren harian                              │
│                                                                   │
│  FASE 4 — INTEGRASI & PENGUJIAN                                   │
│  ├── End-to-end testing                                           │
│  ├── Tuning parameter (threshold, cooldown, FPS)                  │
│  └── Dokumentasi                                                  │
│                                                                   │
└───────────────────────────────────────────────────────────────────┘
```

### Mengapa Instance Segmentation?

Sistem menggunakan pendekatan **Instance Segmentation** alih-alih Object Detection biasa, karena:

| Aspek | Object Detection (Bounding Box) | Instance Segmentation (Mask) |
|-------|--------------------------------|------------------------------|
| Output | Kotak persegi | Mask piksel presisi |
| Analisis kontak | Tidak akurat — dua bounding box bisa overlap meski objek tidak bersentuhan | Akurat — overlap mask = kontak fisik nyata |
| Kebutuhan proyek | Tidak memadai | ✅ Sesuai kebutuhan |

### Logika Compliance (Pseudocode)

```
UNTUK setiap frame yang masuk:
  Jalankan YOLOv8-seg → dapatkan mask: persons, handrails, wrist_contacts
  
  UNTUK setiap person yang terdeteksi:
    Dapatkan ID unik dari tracker
    
    JIKA person tidak berada di dekat area handrail:
      Lewati (bukan pengguna tangga)
    
    AMBIL wrist_contact yang berada dalam area person
    
    HITUNG overlap: mask(wrist_contact) ∩ mask(handrail)
    
    JIKA overlap ≥ 50 piksel:
      status = COMPLIANT
      violation_counter[id] -= 2  (decay)
    LAIN:
      status = VIOLATION
      violation_counter[id] += 1
    
    JIKA violation_counter[id] ≥ 20 frame:
      JIKA waktu sekarang - waktu_alarm_terakhir[id] ≥ 5 detik:
        AKTIFKAN alarm
        SIMPAN foto bukti
        CATAT ke database
        RESET counter
```

---

## 💡 Manfaat Sistem

### Bagi Manajemen / Perusahaan

- **Pencegahan proaktif** — Sistem memberi peringatan real-time sebelum kecelakaan terjadi
- **Dokumentasi otomatis** — Setiap pelanggaran tercatat dengan foto dan timestamp tanpa intervensi manusia
- **Efisiensi biaya** — Monitoring 24/7 tanpa memerlukan penambahan petugas keamanan
- **Data untuk audit** — Riwayat pelanggaran tersedia sebagai bukti dokumentasi program K3
- **Evaluasi program** — Grafik tren memperlihatkan apakah program keselamatan efektif dari waktu ke waktu

### Bagi Petugas Keamanan / HSE Officer

- **Dashboard terpusat** — Seluruh informasi monitoring dalam satu layar
- **Akses riwayat** — Riwayat pelanggaran terstruktur dan mudah dicari berdasarkan tanggal
- **Bukti visual** — Foto pelanggaran dapat digunakan untuk pembinaan karyawan
- **Notifikasi real-time** — Alarm langsung saat pelanggaran terconfirm

### Bagi Pengembang / Peneliti

- **Arsitektur modular** — Setiap komponen (AI engine, backend, frontend) dapat dikembangkan secara independen
- **Open-source** — Dapat diadaptasi untuk kasus compliance monitoring serupa (helm, rompi, masker, dll.)
- **Baseline sistem** — Dapat dijadikan titik awal penelitian lebih lanjut di bidang AI safety monitoring

---

## ⚠️ Batasan Sistem

Berikut adalah keterbatasan yang perlu diperhatikan sebelum mengimplementasikan sistem:

| Batasan | Penjelasan |
|---------|------------|
| **Kualitas kamera** | Sistem memerlukan kamera resolusi minimal 720p dengan pencahayaan cukup untuk hasil deteksi yang optimal |
| **Sudut kamera** | Model dilatih dengan sudut pandang tertentu; sudut kamera yang sangat berbeda dari data training dapat menurunkan akurasi deteksi |
| **Oklusi** | Jika tangan seseorang terhalang oleh objek lain, tubuh orang lain, atau sudut kamera, deteksi `wrist_contact` mungkin tidak berhasil |
| **Jumlah kamera** | Versi saat ini hanya mendukung satu kamera sekaligus dalam satu instance sistem |
| **Identitas** | Sistem menggunakan ID sementara per sesi (bukan identitas permanen individu); ID akan reset saat server diulang |
| **Jaringan** | Backend dan frontend harus berjalan di jaringan lokal yang sama; belum mendukung akses jarak jauh |
| **Akurasi model** | Akurasi deteksi bergantung pada kualitas dan kuantitas data training yang digunakan |

---

<br>

# 🔧 DOKUMENTASI TEKNIS

---

## ✨ Fitur Sistem

| # | Fitur | Deskripsi | Status |
|---|-------|-----------|--------|
| 1 | **Real-Time Detection** | Mendeteksi person, handrail, dan wrist_contact menggunakan YOLOv8 Segmentation pada setiap frame kamera | ✅ |
| 2 | **Automatic Handrail Detection** | Handrail terdeteksi otomatis oleh model AI tanpa perlu konfigurasi area (ROI) secara manual | ✅ |
| 3 | **Wrist Contact Analysis** | Menganalisis overlap piksel antara mask tangan dan mask handrail untuk menentukan kontak fisik | ✅ |
| 4 | **Multi-Person Tracking** | Setiap orang yang terdeteksi mendapat ID unik dan dipantau secara independen antar frame | ✅ |
| 5 | **Temporal Filtering** | Pelanggaran hanya dikonfirmasi jika berlangsung ≥ 1 detik untuk menghindari false alarm | ✅ |
| 6 | **Cooldown Per Person** | Setiap person memiliki cooldown 5 detik setelah alarm berbunyi untuk mencegah spam notifikasi | ✅ |
| 7 | **Alarm Trigger** | Alarm dipicu otomatis di console server saat pelanggaran terconfirm | ✅ |
| 8 | **Evidence Capture** | Foto area person disimpan otomatis dengan nama file berisi timestamp | ✅ |
| 9 | **Database Logging** | Semua pelanggaran dicatat ke SQLite dengan ID, timestamp, person_id, image path, dan confidence | ✅ |
| 10 | **Live Stream Dashboard** | Video stream real-time dengan overlay bounding box, mask, dan label status ditampilkan di browser | ✅ |
| 11 | **Violation Logs** | Tabel riwayat pelanggaran dengan filter hari ini / semua waktu, dan preview foto modal | ✅ |
| 12 | **Statistics & Charts** | Grafik bar chart tren pelanggaran per hari untuk 14 hari terakhir | ✅ |
| 13 | **REST API** | Semua data dapat diakses oleh aplikasi lain melalui HTTP API yang terdokumentasi | ✅ |

---

## 🏗️ Arsitektur Sistem

```
┌──────────────────────────────────────────────────────────────────┐
│                      SYSTEM ARCHITECTURE                          │
├──────────────────────────────────────────────────────────────────┤
│                                                                   │
│   📷 Camera Input (Webcam / IP Cam / RTSP / Video File)          │
│          │                                                        │
│          ▼                                                        │
│   ┌──────────────────────────────────────────────────────┐       │
│   │                    AI ENGINE                          │       │
│   │                                                      │       │
│   │   ┌─────────────────────────────────────────────┐   │       │
│   │   │       YOLOv8 Instance Segmentation           │   │       │
│   │   │   Class 0: person      → polygon mask        │   │       │
│   │   │   Class 1: handrail    → polygon mask        │   │       │
│   │   │   Class 2: wrist_contact → polygon mask      │   │       │
│   │   └─────────────────────────────────────────────┘   │       │
│   │                                                      │       │
│   │   ┌─────────────────────────────────────────────┐   │       │
│   │   │       Geometric Analysis Engine              │   │       │
│   │   │   overlap = mask(wrist) ∩ mask(handrail)     │   │       │
│   │   │   COMPLIANT if overlap ≥ 50px                │   │       │
│   │   └─────────────────────────────────────────────┘   │       │
│   │                                                      │       │
│   │   ┌─────────────────────────────────────────────┐   │       │
│   │   │       Centroid Tracker (IoU-based)           │   │       │
│   │   │   Assigns consistent Person ID per session   │   │       │
│   │   └─────────────────────────────────────────────┘   │       │
│   │                                                      │       │
│   │   ┌─────────────────────────────────────────────┐   │       │
│   │   │       Temporal Filter + Cooldown             │   │       │
│   │   │   Confirm violation after ≥ 20 frames        │   │       │
│   │   │   5-second cooldown per person ID            │   │       │
│   │   └─────────────────────────────────────────────┘   │       │
│   └──────────────────────────┬───────────────────────────┘       │
│                               │                                   │
│              ┌────────────────┼────────────────┐                 │
│              ▼                ▼                ▼                 │
│        ┌──────────┐   ┌────────────┐   ┌──────────────┐         │
│        │  ALARM   │   │  CAPTURE   │   │   DATABASE   │         │
│        │ Console  │   │  Photo     │   │   SQLite     │         │
│        │  Alert   │   │  Save JPG  │   │  violations  │         │
│        └──────────┘   └────────────┘   └──────┬───────┘         │
│                                                │                 │
│                                        ┌───────▼───────┐        │
│                                        │   FastAPI     │        │
│                                        │   Backend     │        │
│                                        │   Port :8000  │        │
│                                        └───────┬───────┘        │
│                                                │                 │
│                            ┌───────────────────┼──────────────┐ │
│                            ▼                   ▼              ▼ │
│                      /api/stream      /api/violations    /api/stats│
│                            │                                     │
│                     ┌──────▼──────┐                             │
│                     │    React    │                             │
│                     │  Frontend   │                             │
│                     │  Port :3000 │                             │
│                     └─────────────┘                             │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🔄 Alur Deteksi

```
Frame Capture (Target: 20–25 FPS)
         │
         ▼
YOLOv8-seg Inference (conf=0.4, iou=0.45)
  ├── Deteksi & Ekstrak Mask: person
  ├── Deteksi & Ekstrak Mask: handrail
  └── Deteksi & Ekstrak Mask: wrist_contact
         │
         ▼
Centroid Tracker Update
  └── Assign/maintain Person ID berdasarkan IoU bbox
         │
         ▼
Proximity Filter per Person
  └── Apakah person berada dalam radius 200px dari handrail?
         │
         ├── TIDAK → skip person ini (bukan pengguna tangga)
         │
         └── YA → lanjut ke compliance check
                    │
                    ▼
         Ambil wrist_contact yang berada dalam bbox person
                    │
                    ▼
         Geometric Overlap Analysis
           mask(wrist_contact) ∩ mask(handrail) ≥ 50px ?
                    │
                    ├── YA  → COMPLIANT ✅
                    │         violation_counter -= 2 (gradual decay)
                    │
                    └── TIDAK → VIOLATION candidate ⚠️
                                 violation_counter += 1
                                         │
                                         ▼
                              violation_counter ≥ 20 ?
                                         │
                                         ├── TIDAK → terus monitoring
                                         │
                                         └── YA → Confirmed VIOLATION ❌
                                                         │
                                                         ▼
                                               Cooldown check
                                               (waktu sekarang - alarm terakhir) ≥ 5 detik ?
                                                         │
                                               ┌─────────┴────────┐
                                               ▼                  ▼
                                        Masih cooldown      Cooldown selesai
                                           │                      │
                                           │               🔔 Alarm trigger
                                           │               📸 Capture & crop foto
                                           │               💾 Simpan JPG
                                           │               🗄️ Insert ke database
                                           │               🔄 Reset counter & timer
                                           │
                                      Lewati trigger
```

---

## 🛠️ Teknologi yang Digunakan

| Layer | Teknologi | Versi | Fungsi |
|-------|-----------|-------|--------|
| **AI / ML** | Ultralytics YOLOv8-seg | 8.0+ | Instance segmentation model utama |
| **Computer Vision** | OpenCV | 4.8+ | Frame capture, image processing, anotasi visual |
| **Backend Framework** | FastAPI | 0.104+ | REST API server, MJPEG stream handler |
| **ASGI Server** | Uvicorn | 0.24+ | Menjalankan FastAPI secara asynchronous |
| **Database ORM** | SQLAlchemy | 2.0+ | Abstraksi database, query builder |
| **Database** | SQLite | Built-in | Penyimpanan data pelanggaran (file-based) |
| **Image Handling** | Pillow | 10.0+ | Manipulasi dan penyimpanan gambar |
| **Numerik** | NumPy | 1.24+ | Operasi array & kalkulasi mask |
| **Frontend** | React.js | 18+ | Web dashboard SPA (Single Page App) |
| **Charts** | Recharts | 2.0+ | Grafik statistik pelanggaran |
| **HTTP Client** | Axios | 1.0+ | Komunikasi HTTP antara frontend dan backend |
| **Training Platform** | Google Colab | — | Cloud GPU (T4 gratis) untuk training model |
| **Dataset Tool** | Roboflow | — | Manajemen dataset, anotasi, augmentasi |
| **Bahasa (AI/BE)** | Python | 3.10+ | Bahasa utama untuk AI engine & backend |
| **Bahasa (FE)** | JavaScript ES6+ | — | Bahasa untuk React frontend |

---

## 📁 Struktur Folder

```
handrail-detection/
│
├── 📂 ai_engine/                    # Core AI Module
│   ├── 🧠 best.pt                   # Model YOLOv8 hasil training (dari Google Colab)
│   ├── 📄 detector.py               # Inference YOLOv8 & ekstraksi mask per objek
│   ├── 📄 compliance.py             # Logika pengecekan kepatuhan (geometric overlap)
│   └── 📄 tracker.py                # Centroid Tracker — multi-person ID assignment
│
├── 📂 backend/                      # FastAPI Server
│   ├── 📄 main.py                   # Entry point: routes, camera loop, stream, alarm
│   └── 📄 database.py               # SQLAlchemy models & fungsi CRUD database
│
├── 📂 frontend/                     # React Web Application
│   ├── 📂 public/
│   │   └── index.html               # HTML template
│   └── 📂 src/
│       ├── 📄 App.jsx               # Root component & navigasi antar halaman
│       ├── 📄 index.js              # React entry point
│       ├── 📄 index.css             # Global dark theme styles
│       ├── 📂 components/
│       │   └── 📄 Sidebar.jsx       # Navigasi sidebar dengan highlight aktif
│       └── 📂 pages/
│           ├── 📄 Dashboard.jsx     # Halaman utama: stat cards & system guide
│           ├── 📄 LiveMonitor.jsx   # Halaman live camera stream & status panel
│           ├── 📄 ViolationLogs.jsx # Tabel riwayat pelanggaran & image preview
│           └── 📄 Statistics.jsx    # Grafik bar chart tren pelanggaran harian
│
├── 📂 violations_img/               # Direktori penyimpanan foto bukti pelanggaran
│   └── violation_person1_20240115_093000.jpg   # (contoh nama file)
│
├── 📄 violations.db                 # SQLite database (dibuat otomatis saat pertama run)
├── 📄 extract_frames.py             # Utility: ekstrak frame dari file video
├── 📄 requirements.txt              # Daftar Python package dependencies
└── 📄 README.md                     # Dokumentasi proyek (file ini)
```

---

## 🗄️ Database Schema

```sql
-- Tabel utama: violations
-- Menyimpan setiap pelanggaran yang terconfirm

CREATE TABLE violations (
    id          TEXT PRIMARY KEY,    -- UUID unik per record pelanggaran
    timestamp   DATETIME NOT NULL,   -- Waktu pelanggaran terjadi (format ISO 8601)
    person_id   INTEGER NOT NULL,    -- ID tracking orang (unik per sesi, reset saat restart)
    image_path  TEXT NOT NULL,       -- Path relatif ke file foto bukti
    confidence  REAL NOT NULL,       -- Confidence score deteksi (0.0 - 1.0)
    status      TEXT NOT NULL        -- Status: selalu "VIOLATION" pada versi ini
);
```

**Contoh isi data:**

| id | timestamp | person_id | image_path | confidence | status |
|----|-----------|-----------|------------|------------|--------|
| `a1b2-...` | 2024-01-15 09:30:00 | 1 | violations_img/violation_person1_20240115_093000.jpg | 0.87 | VIOLATION |
| `c3d4-...` | 2024-01-15 10:15:42 | 2 | violations_img/violation_person2_20240115_101542.jpg | 0.91 | VIOLATION |
| `e5f6-...` | 2024-01-15 14:22:17 | 1 | violations_img/violation_person1_20240115_142217.jpg | 0.83 | VIOLATION |

---

<br>

# 🚀 PANDUAN PENGGUNAAN

---

## 🔧 System Requirements

### Minimum *(Development / Prototype)*

| Komponen | Spesifikasi |
|----------|-------------|
| **OS** | Windows 10 / Ubuntu 20.04+ / macOS 11+ |
| **CPU** | Intel Core i5 Gen 8+ / AMD Ryzen 5 3000+ |
| **RAM** | 8 GB |
| **GPU** | Tidak wajib — CPU mode tersedia (lebih lambat) |
| **Storage** | 5 GB free space |
| **Kamera** | Webcam 720p @ 30fps |
| **Python** | 3.10+ |
| **Node.js** | 18+ |

### Recommended *(Production)*

| Komponen | Spesifikasi |
|----------|-------------|
| **OS** | Ubuntu 22.04 LTS |
| **CPU** | Intel Core i7 Gen 10+ / AMD Ryzen 7 5000+ |
| **RAM** | 16 GB |
| **GPU** | NVIDIA RTX 3060 / GTX 1080 Ti (CUDA 11.8+) |
| **Storage** | 50 GB free (untuk penyimpanan log jangka panjang) |
| **Kamera** | IP Camera 1080p @ 30fps |
| **Python** | 3.10.x |
| **Node.js** | 18.x LTS |

> ⚡ **Catatan Performa GPU:** Dengan GPU NVIDIA, inference YOLOv8 mencapai **25–40 FPS**. Tanpa GPU (CPU only), perkiraan **5–10 FPS** tergantung spesifikasi CPU.

---

## 💻 Instalasi

### Langkah 1 — Verifikasi Prerequisites

```bash
python --version    # Harus 3.10+
node --version      # Harus 18+
npm --version       # Harus 8+
git --version
```

### Langkah 2 — Clone Repository

```bash
git clone https://github.com/username/handrail-detection.git
cd handrail-detection
```

### Langkah 3 — Setup Python Virtual Environment

```bash
# Buat virtual environment
python -m venv venv

# Aktifkan — Windows CMD
venv\Scripts\activate

# Aktifkan — Windows PowerShell
venv\Scripts\Activate.ps1

# Aktifkan — Mac / Linux
source venv/bin/activate

# Install semua dependency Python
pip install -r requirements.txt
```

### Langkah 4 — Setup Frontend React

```bash
cd frontend
npm install
cd ..
```

### Langkah 5 — Taruh Model AI

Setelah proses training selesai, taruh file `best.pt` ke lokasi berikut:

```
handrail-detection/
└── ai_engine/
    └── best.pt    ← taruh di sini
```

### Langkah 6 — Verifikasi Instalasi

```bash
# Cek Python dependencies
python -c "import ultralytics, cv2, fastapi, sqlalchemy; print('✅ Python OK')"

# Cek kamera
python -c "
import cv2
found = [i for i in range(5) if cv2.VideoCapture(i).isOpened()]
print(f'✅ Kamera tersedia: {found}')
"
```

---

## 🎓 Training Model

### Fase 1 — Kumpulkan Data

Kumpulkan **minimal 200–500 foto** dengan variasi berikut:

| Variasi | Contoh |
|---------|--------|
| **Kondisi** | Naik tangga, turun tangga, berdiri di tangga |
| **Status tangan** | Pegang handrail (compliant) vs tidak pegang (violation) |
| **Sudut kamera** | Depan, samping kiri, samping kanan, 45°, sedikit dari atas |
| **Pencahayaan** | Terang, redup, malam, cahaya artificial |
| **Pakaian** | Berbagai warna, lengan panjang, lengan pendek |
| **Jumlah orang** | 1 orang, 2 orang, 3+ orang secara bersamaan |
| **Kecepatan** | Berjalan normal, berjalan cepat |

**Ekstrak frame dari video:**
```bash
# Edit path video di dalam file sebelum menjalankan
python extract_frames.py
# Menghasilkan 1 frame setiap 0.5 detik dari video input
```

---

### Fase 2 — Anotasi di Roboflow

1. Daftar gratis di **[roboflow.com](https://roboflow.com)**
2. **Buat project baru:**
   - Project Type: **`Instance Segmentation`** *(bukan Object Detection!)*
   - Project Name: `handrail-detection`
3. Upload semua foto
4. **Anotasi dengan 3 class menggunakan tool Polygon:**

| Class | Warna | Cara Anotasi |
|-------|-------|--------------|
| `person` | 🔴 Merah | Polygon mengikuti kontur luar tubuh orang (kepala hingga kaki) |
| `handrail` | 🔵 Biru | Polygon memanjang mengikuti bentuk fisik batang handrail |
| `wrist_contact` | 🟢 Hijau | Polygon kecil di area tangan **hanya jika tangan benar-benar menyentuh handrail** |

5. **Generate dataset:**
   - Preprocessing: Resize 640×640, Auto-Orient ON
   - Augmentation: Flip Horizontal, Rotation ±15°, Brightness ±25%, Blur 1.5px
   - Format Export: **YOLOv8**

---

### Fase 3 — Training di Google Colab

1. Buka **[Google Colab](https://colab.research.google.com)** → New Notebook
2. Set runtime: **Runtime → Change runtime type → T4 GPU**
3. Jalankan cell berikut secara berurutan:

```python
# Cell 1 — Install
!pip install ultralytics roboflow -q
import torch
print(f"GPU: {torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'CPU'}")
```

```python
# Cell 2 — Download Dataset dari Roboflow
from roboflow import Roboflow
rf = Roboflow(api_key="MASUKKAN_API_KEY_KAMU")
project = rf.workspace("WORKSPACE_KAMU").project("handrail-detection")
dataset = project.version(1).download("yolov8")
print("Dataset siap:", dataset.location)
```

```python
# Cell 3 — Training
from ultralytics import YOLO
model = YOLO("yolov8m-seg.pt")
results = model.train(
    data=f"{dataset.location}/data.yaml",
    epochs=100,
    imgsz=640,
    batch=16,       # Kurangi ke 8 jika CUDA Out of Memory
    device=0,
    patience=20,
    project="handrail_training",
    name="exp1"
)
```

```python
# Cell 4 — Evaluasi & Download
metrics = model.val()
print(f"mAP50     : {metrics.box.map50:.3f}")
print(f"Precision : {metrics.box.p.mean():.3f}")
print(f"Recall    : {metrics.box.r.mean():.3f}")

from google.colab import files
files.download("handrail_training/exp1/weights/best.pt")
```

**Target performa model:**

| Metrik | Minimum Layak | Target Bagus |
|--------|:-------------:|:------------:|
| mAP50 | > 0.70 | > 0.85 |
| Precision | > 0.70 | > 0.85 |
| Recall | > 0.65 | > 0.80 |

> Jika mAP50 < 0.60, tambahkan data lebih banyak dan perbaiki konsistensi anotasi terlebih dahulu.

---

## 🏷️ Anotasi Dataset

### Panduan Visual

```
╔══════════════════════════════════════════════════════════════════╗
║               PANDUAN ANOTASI YANG BENAR                         ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   SITUASI A: COMPLIANT (Tangan menyentuh handrail)               ║
║   ─────────────────────────────────────────────────             ║
║   ┌────────────────────────────────────────────────┐            ║
║   │  🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵  │ ← handrail    ║
║   │  ┌──────────────────────────────────────────┐  │            ║
║   │  │                                          │  │            ║
║   │  │         🔴 PERSON                        │  │            ║
║   │  │         (polygon seluruh tubuh)          │  │            ║
║   │  │                                          │  │            ║
║   │  │              ✋ 🟢 WRIST_CONTACT         │  │            ║
║   │  │              (polygon kecil di tangan)   │  │            ║
║   │  │                                          │  │            ║
║   │  └──────────────────────────────────────────┘  │            ║
║   └────────────────────────────────────────────────┘            ║
║   ✅ Anotasi: person ✓ + handrail ✓ + wrist_contact ✓           ║
║                                                                  ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   SITUASI B: VIOLATION (Tangan TIDAK menyentuh handrail)         ║
║   ────────────────────────────────────────────────────          ║
║   ┌────────────────────────────────────────────────┐            ║
║   │  🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵🔵  │ ← handrail    ║
║   │  ┌──────────────────────────────────────────┐  │            ║
║   │  │                                          │  │            ║
║   │  │         🔴 PERSON                        │  │            ║
║   │  │         (polygon seluruh tubuh)          │  │            ║
║   │  │                                          │  │            ║
║   │  │         (tidak ada wrist_contact)        │  │            ║
║   │  │                                          │  │            ║
║   │  └──────────────────────────────────────────┘  │            ║
║   └────────────────────────────────────────────────┘            ║
║   ❌ Anotasi: person ✓ + handrail ✓ (TANPA wrist_contact)       ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
```

### Aturan Detail per Class

**`person`:**
- Gunakan tool **Polygon** di Roboflow
- Ikuti kontur luar tubuh (kepala → bahu → lengan → pinggang → kaki)
- Jika tubuh terpotong tepi frame, ikuti batas frame sebagai batas polygon
- Setiap orang = 1 polygon `person`

**`handrail`:**
- Gambar polygon memanjang mengikuti bentuk fisik batang rel
- Sertakan seluruh bagian handrail yang terlihat di frame
- Jika ada handrail di sisi kiri **DAN** kanan → buat **2 polygon terpisah**
- Ikuti lebar fisik batang pegangan

**`wrist_contact`:**
- Gambar polygon kecil (±area telapak tangan + pergelangan)
- **Buat HANYA jika** tangan terlihat jelas menyentuh / menggenggam handrail
- Jika tangan dekat handrail tapi tidak menyentuh → **jangan buat anotasi**
- Jika dua tangan menyentuh → buat **2 polygon** `wrist_contact` terpisah

### Distribusi Dataset yang Disarankan

```
Dataset Total (contoh: 500 gambar)
├── Train (70%)         = 350 gambar
│   ├── Compliant       ≈ 175 gambar
│   └── Violation       ≈ 175 gambar
│
├── Validation (20%)    = 100 gambar
│   ├── Compliant       ≈  50 gambar
│   └── Violation       ≈  50 gambar
│
└── Test (10%)          =  50 gambar
    ├── Compliant       ≈  25 gambar
    └── Violation       ≈  25 gambar
```

---

## ▶️ Menjalankan Sistem

### Terminal 1 — Backend

```bash
# Pastikan venv aktif, posisi di root folder project
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8000
```

Output yang diharapkan:
```
INFO:     Uvicorn running on http://0.0.0.0:8000
INFO:     Application startup complete.
[SERVER] Camera thread started
```

Verifikasi backend: buka [http://localhost:8000](http://localhost:8000)

### Terminal 2 — Frontend

```bash
cd frontend
npm start
```

Buka dashboard di: [http://localhost:3000](http://localhost:3000)

---

### Konfigurasi Sumber Kamera

Edit `backend/main.py`:

```python
# Webcam default
cap = cv2.VideoCapture(0)

# Webcam kedua
cap = cv2.VideoCapture(1)

# IP Camera via RTSP
cap = cv2.VideoCapture("rtsp://admin:password@192.168.1.100:554/stream1")

# File video (untuk testing tanpa kamera)
cap = cv2.VideoCapture("video_tangga.mp4")
```

---

## 📡 API Endpoints

**Base URL:** `http://localhost:8000`

| Method | Endpoint | Deskripsi |
|--------|----------|-----------|
| `GET` | `/` | Health check — cek apakah server aktif |
| `GET` | `/api/stream` | Live MJPEG video stream dengan overlay |
| `GET` | `/api/violations` | Semua data pelanggaran (newest first) |
| `GET` | `/api/violations/today` | Pelanggaran hari ini saja |
| `GET` | `/api/stats` | Statistik sistem real-time |
| `GET` | `/violations_img/{filename}` | Akses file foto pelanggaran |

**Response Examples:**

```jsonc
// GET /api/stats
{
  "total_violations_today": 5,
  "total_violations_all": 47,
  "camera_active": true,
  "fps": 22,
  "total_persons_detected": 2
}

// GET /api/violations (array)
[
  {
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "timestamp": "2024-01-15T09:30:00",
    "person_id": 1,
    "image_path": "violations_img/violation_person1_20240115_093000.jpg",
    "confidence": 0.87,
    "status": "VIOLATION"
  }
]
```

Dokumentasi interaktif Swagger UI tersedia di: [http://localhost:8000/docs](http://localhost:8000/docs)

---

## ⚙️ Konfigurasi

Parameter sistem dapat disesuaikan di `backend/main.py`:

```python
# ─── Kamera ────────────────────────────────────────────────────
CAMERA_SOURCE        = 0       # 0=webcam, string=RTSP/path video

# ─── Model Inference ───────────────────────────────────────────
CONFIDENCE_THRESHOLD = 0.4     # Min confidence deteksi (0.0-1.0)
IOU_THRESHOLD        = 0.45    # IoU threshold untuk NMS

# ─── Compliance Logic ──────────────────────────────────────────
VIOLATION_THRESHOLD  = 20      # Frame berturut-turut sebelum alarm
                               # 20 frame ≈ 1 detik di 20 FPS
COOLDOWN_SECONDS     = 5       # Jeda antar alarm per person (detik)
MIN_OVERLAP_PIXELS   = 50      # Min overlap pixel wrist ∩ handrail

# ─── Video Stream ──────────────────────────────────────────────
STREAM_FPS           = 25      # Target FPS output ke browser
JPEG_QUALITY         = 80      # Kualitas JPEG (1-100)

# ─── Tracker ───────────────────────────────────────────────────
MAX_DISAPPEARED      = 30      # Frame sebelum person ID dihapus
```

---

## 🐛 Troubleshooting

### ❌ Kamera tidak terdeteksi

```bash
python -c "
import cv2
for i in range(5):
    cap = cv2.VideoCapture(i)
    if cap.isOpened():
        print(f'✅ Kamera ditemukan di index {i}')
        cap.release()
    else:
        print(f'❌ Index {i}: tidak ada kamera')
"
```

Ganti angka di `cv2.VideoCapture(0)` sesuai index yang ditemukan.

---

### ❌ Model tidak ditemukan (`best.pt`)

```
FileNotFoundError: [Errno 2] No such file or directory: 'ai_engine/best.pt'
```

**Solusi:** Pastikan file `best.pt` sudah ada di folder `ai_engine/`. Jika belum punya model hasil training, gunakan model default untuk testing:

```bash
python -c "
from ultralytics import YOLO
import shutil
YOLO('yolov8m-seg.pt')  # auto-download
shutil.copy('yolov8m-seg.pt', 'ai_engine/best.pt')
print('✅ Model default siap (untuk testing — class handrail belum terlatih)')
"
```

---

### ❌ CORS Error di browser

```
Access to XMLHttpRequest blocked by CORS policy
```

Pastikan origin frontend sudah ditambahkan di `backend/main.py`:

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],  # Sesuaikan port
)
```

---

### ❌ CUDA Out of Memory saat training

```python
# Kurangi batch size di notebook Colab:
model.train(..., batch=8)   # 8GB VRAM
model.train(..., batch=4)   # 4GB VRAM
```

---

### ❌ mAP50 rendah setelah training

| Kemungkinan Penyebab | Solusi |
|----------------------|--------|
| Data terlalu sedikit | Tambah foto hingga 300–500+ |
| Anotasi tidak konsisten | Tinjau ulang dan standarisasi aturan anotasi |
| Variasi data kurang | Tambah variasi sudut, cahaya, pakaian |
| Epoch kurang | Naikkan ke 150–200 epoch |
| Model terlalu kecil | Coba `yolov8l-seg.pt` atau `yolov8x-seg.pt` |

---

### ❌ Stream video lambat / lag

```python
# Tambahkan resize setelah membaca frame di backend/main.py
ret, frame = cap.read()
frame = cv2.resize(frame, (640, 480))  # Kurangi resolusi

# Turunkan kualitas JPEG
JPEG_QUALITY = 60  # Dari 80 ke 60
```

---

## 🗺️ Roadmap

### ✅ Versi 1.0 — Rilis Sekarang
- [x] YOLOv8 Instance Segmentation AI Engine
- [x] Multi-person Centroid Tracker
- [x] Geometric compliance analysis
- [x] Temporal filtering & per-person cooldown
- [x] FastAPI backend dengan MJPEG stream
- [x] SQLite database logging + REST API
- [x] React dashboard — 4 halaman lengkap

### 🔜 Versi 1.1 — Direncanakan
- [ ] Notifikasi email otomatis saat violation
- [ ] Notifikasi WhatsApp via Fonnte / Twilio
- [ ] Export laporan ke PDF dan Excel
- [ ] Filter & pencarian di violation logs

### 🔜 Versi 2.0 — Direncanakan
- [ ] Dukungan multi-kamera sekaligus
- [ ] Docker containerization
- [ ] Autentikasi pengguna (login dashboard)
- [ ] Konfigurasi parameter via UI (tanpa edit kode)
- [ ] Integrasi dengan sistem NVR / CCTV yang ada

### 🔮 Masa Depan
- [ ] Face recognition untuk identifikasi karyawan
- [ ] Mobile app (React Native)
- [ ] Dukungan kamera thermal / night vision
- [ ] ML-based anomaly detection untuk prediksi pola pelanggaran
- [ ] Cloud deployment (Docker + VPS)

---

## 🤝 Kontribusi

Kontribusi sangat disambut! Cara berkontribusi:

1. **Fork** repository ini
2. Buat **branch** baru: `git checkout -b feature/nama-fitur`
3. **Commit** perubahan: `git commit -m 'feat: deskripsi singkat'`
4. **Push** ke branch: `git push origin feature/nama-fitur`
5. Buat **Pull Request** ke branch `main`

**Konvensi Commit Message:**

| Prefix | Digunakan untuk |
|--------|----------------|
| `feat:` | Menambahkan fitur baru |
| `fix:` | Memperbaiki bug |
| `docs:` | Perubahan dokumentasi |
| `refactor:` | Refactoring kode tanpa perubahan fungsionalitas |
| `perf:` | Peningkatan performa |
| `test:` | Menambahkan atau mengubah test |

---

## 📄 Lisensi

Distributed under the **MIT License**.

```
MIT License — Copyright (c) 2024 [Nama Kamu]

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software to deal in the Software without restriction,
including the rights to use, copy, modify, merge, publish, distribute,
sublicense, and/or sell copies of the Software.
```

Lihat file [LICENSE](LICENSE) untuk teks lengkap.

---

## 👤 Author

**Nama Kamu**

- 🐙 GitHub: [@username](https://github.com/username)
- 📧 Email: email@example.com
- 💼 LinkedIn: [linkedin.com/in/username](https://linkedin.com/in/username)

---

## 🙏 Acknowledgements

Proyek ini dibangun di atas kontribusi dari komunitas open-source berikut:

- [**Ultralytics YOLOv8**](https://github.com/ultralytics/ultralytics) — State-of-the-art object detection & segmentation
- [**Roboflow**](https://roboflow.com) — Platform manajemen dataset dan anotasi computer vision
- [**FastAPI**](https://fastapi.tiangolo.com) — Modern, high-performance Python web framework
- [**React**](https://react.dev) — JavaScript library untuk antarmuka pengguna
- [**OpenCV**](https://opencv.org) — Open source computer vision & machine learning library
- [**Recharts**](https://recharts.org) — Composable charting library untuk React
- [**Google Colab**](https://colab.research.google.com) — Free cloud GPU untuk training model AI

---

<p align="center">
  <strong>⭐ Jika proyek ini bermanfaat, berikan bintang di GitHub! ⭐</strong>
  <br><br>
  Dibangun untuk keselamatan kerja yang lebih baik 🦺
</p>
