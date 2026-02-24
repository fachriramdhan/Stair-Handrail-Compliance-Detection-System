# 🛡️ SafeStair — Stair Handrail Compliance Detection System

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/YOLOv8-Ultralytics-purple?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/FastAPI-0.104+-green?style=for-the-badge&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/React-18+-61DAFB?style=for-the-badge&logo=react&logoColor=black"/>
  <img src="https://img.shields.io/badge/SQLite-Database-003B57?style=for-the-badge&logo=sqlite&logoColor=white"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"/>
</p>

<p align="center">
  Sistem monitoring berbasis AI untuk mendeteksi kepatuhan penggunaan handrail di area tangga secara real-time.
</p>

---

## 📋 Daftar Isi

- [Demo](#-demo)
- [Fitur](#-fitur)
- [Arsitektur Sistem](#-arsitektur-sistem)
- [Alur Deteksi](#-alur-deteksi)
- [Teknologi](#-teknologi)
- [Struktur Folder](#-struktur-folder)
- [Instalasi](#-instalasi)
- [Training Model](#-training-model)
- [Menjalankan Sistem](#-menjalankan-sistem)
- [API Endpoints](#-api-endpoints)
- [Anotasi Dataset](#-anotasi-dataset)
- [Konfigurasi](#-konfigurasi)
- [Troubleshooting](#-troubleshooting)
- [Kontribusi](#-kontribusi)
- [Lisensi](#-lisensi)

---

## 🎥 Demo

```
📹 Live Camera Feed → AI Detection → Alarm Trigger → Web Dashboard
```

| Dashboard | Live Monitor | Violation Logs |
|-----------|--------------|----------------|
| Statistik harian | Real-time stream | Tabel pelanggaran |
| Compliance rate | Overlay deteksi | Preview foto |
| System status | Status per orang | Filter by date |

---

## ✨ Fitur

- **Real-Time Detection** — Deteksi orang dan handrail menggunakan YOLOv8 Segmentation
- **Multi-Person Tracking** — Tracking setiap orang secara independen dengan ID unik
- **Automatic Handrail Detection** — Tidak butuh konfigurasi ROI manual
- **Wrist Contact Detection** — Deteksi apakah tangan benar-benar menyentuh handrail
- **Temporal Filtering** — Filter false alarm, violation harus terjadi ≥ 1 detik
- **Alarm System** — Notifikasi otomatis saat pelanggaran terdeteksi
- **Evidence Capture** — Foto pelanggaran tersimpan otomatis
- **Database Logging** — Semua pelanggaran tercatat di SQLite
- **Web Dashboard** — Monitoring real-time berbasis React
- **REST API** — FastAPI backend yang bisa diintegrasikan ke sistem lain

---

## 🏗️ Arsitektur Sistem

```
┌─────────────────────────────────────────────────────────────┐
│                        SYSTEM OVERVIEW                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   📷 Camera                                                  │
│       │                                                      │
│       ▼                                                      │
│   ┌─────────────────────────────┐                           │
│   │      AI ENGINE              │                           │
│   │  YOLOv8-seg (segmentation)  │                           │
│   │  ├── person detection       │                           │
│   │  ├── handrail detection     │                           │
│   │  └── wrist_contact detect   │                           │
│   │                             │                           │
│   │  Geometric Analysis         │                           │
│   │  Temporal Filter            │                           │
│   │  Centroid Tracker           │                           │
│   └──────────────┬──────────────┘                           │
│                  │                                          │
│       ┌──────────┴──────────┐                               │
│       ▼                     ▼                               │
│   ┌──────────┐        ┌──────────┐                          │
│   │  ALARM   │        │ DATABASE │                          │
│   │  System  │        │  SQLite  │                          │
│   └──────────┘        └────┬─────┘                          │
│                             │                               │
│                        ┌────▼─────┐                         │
│                        │ FastAPI  │                         │
│                        │ Backend  │                         │
│                        └────┬─────┘                         │
│                             │                               │
│                        ┌────▼─────┐                         │
│                        │  React   │                         │
│                        │ Frontend │                         │
│                        └──────────┘                         │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔄 Alur Deteksi

```
Frame Capture (20-25 FPS)
        │
        ▼
YOLOv8-seg Inference
  ├── Detect: person
  ├── Detect: handrail
  └── Detect: wrist_contact
        │
        ▼
Geometric Relationship Analysis
  └── wrist_contact ∩ handrail = ?
        │
        ├── YES → COMPLIANT ✅
        └── NO  → counter++
                    │
                    └── counter ≥ 20 frames (~1 detik)?
                                │
                                ├── NO  → lanjut monitoring
                                └── YES → VIOLATION ❌
                                              │
                                              ▼
                                    Cooldown check (5 detik)
                                              │
                                              ▼
                                    Trigger Alarm
                                    Capture Frame
                                    Save to Database
```

---

## 🛠️ Teknologi

| Layer | Teknologi | Versi |
|-------|-----------|-------|
| AI Model | YOLOv8 Segmentation (Ultralytics) | 8.0+ |
| Backend | FastAPI + Uvicorn | 0.104+ |
| Database | SQLAlchemy + SQLite | 2.0+ |
| Computer Vision | OpenCV | 4.8+ |
| Frontend | React.js | 18+ |
| Charts | Recharts | 2.0+ |
| HTTP Client | Axios | 1.0+ |
| Training | Google Colab (GPU T4) | — |
| Dataset | Roboflow | — |
| Language | Python 3.10+ / JavaScript | — |

---

## 📁 Struktur Folder

```
handrail-detection/
│
├── ai_engine/                  # Core AI module
│   ├── best.pt                 # Model hasil training (download dari Colab)
│   ├── detector.py             # YOLOv8 inference & object extraction
│   ├── compliance.py           # Logika compliance check
│   └── tracker.py              # Centroid tracker multi-person
│
├── backend/                    # FastAPI server
│   ├── main.py                 # Entry point, API routes, camera loop
│   └── database.py             # SQLAlchemy models & query functions
│
├── frontend/                   # React web app
│   ├── public/
│   └── src/
│       ├── App.jsx             # Root component
│       ├── index.js            # Entry point
│       ├── index.css           # Global styles
│       ├── components/
│       │   └── Sidebar.jsx     # Navigation sidebar
│       └── pages/
│           ├── Dashboard.jsx   # Overview page
│           ├── LiveMonitor.jsx # Live stream page
│           ├── ViolationLogs.jsx # Logs page
│           └── Statistics.jsx  # Charts page
│
├── violations_img/             # Foto pelanggaran tersimpan di sini
├── violations.db               # SQLite database (auto-generated)
├── extract_frames.py           # Utility: ambil frame dari video
├── requirements.txt            # Python dependencies
└── README.md
```

---

## 🚀 Instalasi

### Prerequisites

Pastikan software berikut sudah terinstall:

| Software | Versi | Link |
|----------|-------|------|
| Python | 3.10+ | https://python.org |
| Node.js | 18+ | https://nodejs.org |
| Git | Latest | https://git-scm.com |

> **GPU (Opsional tapi disarankan):** NVIDIA GPU dengan CUDA untuk inference lebih cepat.

---

### 1. Clone Repository

```bash
git clone https://github.com/username/handrail-detection.git
cd handrail-detection
```

### 2. Setup Python Environment

```bash
# Buat virtual environment
python -m venv venv

# Aktifkan — Windows
venv\Scripts\activate

# Aktifkan — Mac/Linux
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Setup Frontend

```bash
cd frontend
npm install
cd ..
```

### 4. Siapkan Model

Setelah training selesai (lihat [Training Model](#-training-model)), taruh file `best.pt` ke folder:

```
ai_engine/best.pt
```

---

## 🎓 Training Model

### Langkah 1 — Kumpulkan Data

Kumpulkan **minimal 200–500 foto** orang di tangga dengan dua kondisi:

| Kondisi | Keterangan |
|---------|------------|
| ✅ COMPLIANT | Orang naik/turun tangga sambil memegang handrail |
| ❌ VIOLATION | Orang naik/turun tangga tanpa memegang handrail |

**Tips variasi data:**
- Sudut kamera: depan, samping, sedikit atas
- Pencahayaan: terang, redup, malam
- Jumlah orang: 1 orang, 2+ orang bersamaan
- Pakaian: warna dan jenis berbeda-beda

**Ekstrak frame dari video:**
```bash
python extract_frames.py
```
Script ini mengambil 1 frame setiap 0.5 detik dari file video.

---

### Langkah 2 — Anotasi di Roboflow

1. Daftar di [roboflow.com](https://roboflow.com) (gratis)
2. Buat project baru:
   - **Type:** Instance Segmentation
   - **Name:** `handrail-detection`
3. Upload semua foto
4. Anotasi dengan **3 class**:

| Class | Warna | Cara Anotasi |
|-------|-------|--------------|
| `person` | 🔴 Merah | Polygon seluruh tubuh orang |
| `handrail` | 🔵 Biru | Polygon batang pegangan tangga |
| `wrist_contact` | 🟢 Hijau | Polygon kecil area tangan yang menyentuh handrail |

> ⚠️ **Penting:** `wrist_contact` hanya dianotasi jika tangan benar-benar menyentuh handrail. Jika tidak menyentuh, jangan tambahkan anotasi `wrist_contact`.

5. Generate dataset:
   - Preprocessing: Resize 640x640, Auto-Orient ON
   - Augmentation: Flip Horizontal, Rotation ±15°, Brightness ±25%
   - Format export: **YOLOv8**

---

### Langkah 3 — Training di Google Colab

1. Buka [Google Colab](https://colab.research.google.com)
2. Ganti runtime: **Runtime → Change runtime type → T4 GPU**
3. Jalankan cells berikut:

```python
# Cell 1: Install
!pip install ultralytics roboflow -q

# Cell 2: Download dataset dari Roboflow
from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace("YOUR_WORKSPACE").project("handrail-detection")
dataset = project.version(1).download("yolov8")

# Cell 3: Training
from ultralytics import YOLO
model = YOLO("yolov8m-seg.pt")
results = model.train(
    data=f"{dataset.location}/data.yaml",
    epochs=100,
    imgsz=640,
    batch=16,
    device=0,
    patience=20,
    project="handrail_training",
    name="exp1"
)

# Cell 4: Download model
from google.colab import files
files.download("handrail_training/exp1/weights/best.pt")
```

**Target performa model:**

| Metrik | Minimum | Bagus |
|--------|---------|-------|
| mAP50 | > 0.70 | > 0.85 |
| Precision | > 0.70 | > 0.85 |
| Recall | > 0.65 | > 0.80 |

---

## ▶️ Menjalankan Sistem

### Terminal 1 — Backend

```bash
# Dari root folder, dengan venv aktif
uvicorn backend.main:app --reload --host 0.0.0.0 --port 8000
```

Verifikasi: buka [http://localhost:8000](http://localhost:8000)

### Terminal 2 — Frontend

```bash
cd frontend
npm start
```

Buka dashboard: [http://localhost:3000](http://localhost:3000)

---

### Menggunakan IP Camera / RTSP

Edit `backend/main.py` bagian ini:

```python
# Sebelum (webcam)
cap = cv2.VideoCapture(0)

# Sesudah (IP Camera)
cap = cv2.VideoCapture("rtsp://username:password@192.168.1.100:554/stream")

# Atau file video untuk testing
cap = cv2.VideoCapture("test_video.mp4")
```

---

## 📡 API Endpoints

Base URL: `http://localhost:8000`

| Method | Endpoint | Deskripsi |
|--------|----------|-----------|
| `GET` | `/api/stream` | MJPEG live stream |
| `GET` | `/api/violations` | Semua data pelanggaran |
| `GET` | `/api/violations/today` | Pelanggaran hari ini |
| `GET` | `/api/stats` | Statistik sistem |
| `GET` | `/violations_img/{filename}` | Foto pelanggaran |

**Contoh response `GET /api/stats`:**
```json
{
  "total_violations_today": 5,
  "total_violations_all": 47,
  "camera_active": true,
  "fps": 22,
  "total_persons_detected": 2
}
```

**Contoh response `GET /api/violations`:**
```json
[
  {
    "id": "uuid-string",
    "timestamp": "2024-01-15T09:30:00",
    "person_id": 1,
    "image_path": "violations_img/violation_person1_20240115_093000.jpg",
    "confidence": 0.85,
    "status": "VIOLATION"
  }
]
```

---

## 🏷️ Anotasi Dataset

### Panduan Lengkap Anotasi

Berikut panduan visual untuk anotasi yang benar di Roboflow:

```
╔══════════════════════════════════════════════════════╗
║           CONTOH ANOTASI YANG BENAR                  ║
║                                                      ║
║  ┌─────────────────────────────────────────────┐     ║
║  │  🔵 handrail (polygon biru sepanjang rel)   │     ║
║  │  ┌─────────────────────────────────────┐   │     ║
║  │  │                                     │   │     ║
║  │  │   🔴 person (polygon tubuh)         │   │     ║
║  │  │                                     │   │     ║
║  │  │         ✋ 🟢 wrist_contact         │   │     ║
║  │  │         (jika tangan di handrail)   │   │     ║
║  │  │                                     │   │     ║
║  │  └─────────────────────────────────────┘   │     ║
║  └─────────────────────────────────────────────┘     ║
║                                                      ║
║  COMPLIANT → ada wrist_contact + overlap handrail    ║
║  VIOLATION → TIDAK ada wrist_contact                 ║
╚══════════════════════════════════════════════════════╝
```

### Aturan Anotasi

**`person` class:**
- Gambar polygon mengikuti kontur seluruh tubuh
- Termasuk kepala sampai kaki
- Jika sebagian tubuh terpotong frame, anotasi bagian yang terlihat saja

**`handrail` class:**
- Gambar polygon mengikuti bentuk batang handrail
- Dari ujung kiri sampai kanan handrail yang terlihat
- Jika ada 2 handrail (kiri & kanan), buat 2 anotasi terpisah

**`wrist_contact` class:**
- Gambar polygon kecil di area pergelangan tangan
- HANYA ketika tangan terlihat jelas menyentuh/menggenggam handrail
- Jika tangan tidak menyentuh → JANGAN buat anotasi ini
- Ukuran polygon: sekitar area telapak tangan + pergelangan

### Distribusi Dataset yang Disarankan

```
Total Dataset
├── Train (70%) ≈ 350 gambar
│   ├── COMPLIANT ≈ 175 gambar
│   └── VIOLATION ≈ 175 gambar
├── Validation (20%) ≈ 100 gambar
└── Test (10%) ≈ 50 gambar
```

---

## ⚙️ Konfigurasi

Edit nilai-nilai ini di `backend/main.py` sesuai kebutuhan:

```python
# ─── Konfigurasi Kamera ───────────────────────────────────
CAMERA_SOURCE = 0                    # 0=webcam, atau path RTSP/file

# ─── Konfigurasi Deteksi ─────────────────────────────────
CONFIDENCE_THRESHOLD = 0.4           # Minimum confidence deteksi
IOU_THRESHOLD = 0.45                 # Threshold IoU untuk NMS

# ─── Konfigurasi Compliance ──────────────────────────────
VIOLATION_THRESHOLD = 20             # Frame berturut-turut = ~1 detik
COOLDOWN_SECONDS = 5                 # Jeda alarm per orang

# ─── Konfigurasi Stream ──────────────────────────────────
STREAM_FPS = 25                      # Target FPS untuk web stream
JPEG_QUALITY = 80                    # Kualitas gambar stream (1-100)
```

---

## 🐛 Troubleshooting

### Kamera tidak terdeteksi

```bash
# Cek device kamera yang tersedia
python -c "import cv2; [print(f'Camera {i}: OK') for i in range(5) if cv2.VideoCapture(i).isOpened()]"
```

Ganti angka `0` di `cv2.VideoCapture(0)` dengan device index yang tersedia.

---

### Model tidak ditemukan

```
FileNotFoundError: ai_engine/best.pt not found
```

Pastikan file `best.pt` sudah ada di folder `ai_engine/`. Jika belum training, download contoh model:

```bash
# Download model YOLOv8 default (tanpa training custom) untuk testing
python -c "from ultralytics import YOLO; YOLO('yolov8m-seg.pt')"
# Lalu rename menjadi best.pt
```

---

### CORS Error di browser

Pastikan URL frontend sesuai di `backend/main.py`:

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:3000"],  # Sesuaikan port React kamu
    ...
)
```

---

### Memory error saat training di Colab

Kurangi batch size:

```python
# Ganti batch=16 menjadi
model.train(..., batch=8)   # Untuk GPU 8GB
model.train(..., batch=4)   # Untuk GPU 4GB
```

---

### mAP rendah setelah training

| Kemungkinan penyebab | Solusi |
|---------------------|--------|
| Data terlalu sedikit | Tambah foto hingga 500+ |
| Anotasi tidak konsisten | Review dan perbaiki anotasi |
| Variasi data kurang | Tambah variasi sudut, cahaya, pakaian |
| Epoch kurang | Tambah epochs ke 150-200 |
| Augmentasi kurang | Aktifkan lebih banyak augmentasi di Roboflow |

---

### Stream lambat / lag

```python
# Kurangi resolusi frame di backend/main.py
ret, frame = cap.read()
frame = cv2.resize(frame, (640, 480))  # Tambahkan baris ini
```

---

## 🔧 System Requirements

### Minimum (Prototype/Development)

| Komponen | Minimum |
|----------|---------|
| CPU | Intel Core i5 / AMD Ryzen 5 |
| RAM | 8 GB |
| GPU | NVIDIA GTX 1060 (opsional) |
| Storage | 5 GB free |
| OS | Windows 10 / Ubuntu 20.04 / macOS 11 |
| Python | 3.10+ |

### Recommended (Production)

| Komponen | Recommended |
|----------|-------------|
| CPU | Intel Core i7 / AMD Ryzen 7 |
| RAM | 16 GB |
| GPU | NVIDIA RTX 3060 atau lebih tinggi |
| Storage | 20 GB free (untuk penyimpanan footage) |
| Camera | 1080p @ 30fps |

---

## 🗺️ Roadmap

- [x] AI Engine dengan YOLOv8 Segmentation
- [x] Multi-person tracking
- [x] Temporal filtering
- [x] FastAPI backend
- [x] React dashboard
- [x] SQLite database logging
- [ ] Email/WhatsApp notification saat violation
- [ ] Multi-camera support
- [ ] Export laporan ke PDF/Excel
- [ ] Docker deployment
- [ ] Mobile app (React Native)
- [ ] Night vision / thermal camera support

---

## 🤝 Kontribusi

Kontribusi sangat disambut! Silakan:

1. Fork repository ini
2. Buat branch baru: `git checkout -b feature/nama-fitur`
3. Commit perubahan: `git commit -m 'Add: nama fitur'`
4. Push ke branch: `git push origin feature/nama-fitur`
5. Buat Pull Request

---

## 📄 Lisensi

Distributed under the MIT License. See `LICENSE` for more information.

---

## 👤 Author

**Nama Kamu**
- GitHub: [@username](https://github.com/username)
- Email: email@example.com

---

## 🙏 Acknowledgements

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) — AI model framework
- [Roboflow](https://roboflow.com) — Dataset management & annotation
- [FastAPI](https://fastapi.tiangolo.com) — Python web framework
- [React](https://react.dev) — Frontend framework
- [Recharts](https://recharts.org) — Chart library

---

<p align="center">
  Made with ❤️ for workplace safety
</p>
