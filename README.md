# 🌿 Vrikshaayush — AI Plant Health Diagnostic App

> *Vrikshaayush* (वृक्षायुष) — "Life of the Plant" in Sanskrit

An **offline-first, edge-AI mobile app** for rural Indian farmers to diagnose plant diseases instantly — no internet required.

---

## 📱 What It Does

- 📸 Farmer takes a photo of their plant
- 🤖 AI diagnoses the disease **on-device** (zero internet needed)
- 💊 Shows treatment recommendations instantly
- 📚 Offline crop & disease library
- 📊 Scan history & audit logs
- 🌐 Seven languages: **English, Hindi, Kannada, Malayalam, Marathi, Tamil, Telugu**

---

## 🏗 Architecture

```
Farmer's Phone
│
├── Camera / Gallery Input
│
├── TensorFlow Lite Model (on-device)
│   └── plant_disease_model.tflite
│       └── Trained on PlantVillage Dataset (50,000+ images, 38 classes)
│
├── Local SQLite Database
│   └── Scan history, disease library, user preferences
│
└── UI (Android — Kotlin + XML layouts)
    └── 12 screens, multilingual, offline-ready
```

---

## 📂 Folder Structure

```
vrikshaayush/
├── app/
│   ├── build.gradle                 # compileSdk 35, minSdk 24, TFLite, Room, Glide, coroutines
│   └── src/main/
│       ├── kotlin/com/vrikshaayush/
│       │   ├── data/                # Room database, DAO, scan record entity
│       │   ├── ml/                  # DiseaseClassifier — TFLite inference + preprocessing
│       │   ├── model/               # DiseaseInfo data class
│       │   └── ui/                  # 12 activities + RecyclerView adapters
│       ├── assets/
│       │   ├── plant_disease_model.tflite   # model included in the repo (13 MB)
│       │   ├── labels.txt                   # 38 disease class labels
│       │   └── diseases.json                # offline disease library
│       └── res/                     # layouts, drawables, 7 language folders
├── database/
│   └── diseases.json                # source copy of the offline disease database
├── docs/
│   ├── TFLITE_GUIDE.md              # TFLite integration and retraining notes
│   ├── ARCHITECTURE.md              # system architecture
│   ├── STRESS_TEST.md               # architecture stress-test analysis
│   └── UI_PROMPTS.md                # UI prompts for all screens
├── gradle/                          # Gradle wrapper
├── build.gradle                     # project-level build file
├── settings.gradle
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- Android Studio (Ladybug or newer) with **JDK 17**
- Android SDK 35
- Android device or emulator (API 24+)

### Build and run
```bash
git clone https://github.com/rudransh-dev1/vrikshaayush.git
cd vrikshaayush
./gradlew assembleDebug
```

The APK is written to `app/build/outputs/apk/debug/app-debug.apk`. To run it directly, open the
project folder in Android Studio and press Run.

The TFLite model is already committed at `app/src/main/assets/plant_disease_model.tflite`, so the app
works offline immediately after the first build. No extra download is needed.

---

## 🤖 AI Model

- **Base model:** MobileNetV2 trained on PlantVillage dataset
- **Included in this repo:** yes, no separate download required
- **Format:** TensorFlow Lite (.tflite)
- **Input:** 224×224 RGB image
- **Output:** 38 disease classes + confidence score
- **Size:** ~13 MB, bundled in `app/src/main/assets/` (runs on any Android phone from 2018+)
- **Inference time:** ~150ms on mid-range device

---

## 🌾 Supported Crops & Diseases

| Crop | Diseases Covered |
|------|-----------------|
| Tomato | Early Blight, Late Blight, Leaf Mold, Mosaic Virus, etc. |
| Rice | Blast, Brown Spot, Neck Rot |
| Wheat | Leaf Rust, Yellow Rust, Powdery Mildew |
| Cotton | Boll Rot, Bacterial Blight, Leaf Curl |
| Maize | Common Rust, Gray Leaf Spot, Northern Blight |
| Apple | Scab, Black Rot, Cedar Apple Rust |
| Potato | Early Blight, Late Blight, Healthy |

---

## 🎨 Design System

| Color | Hex | Usage |
|-------|-----|-------|
| Forest Green | `#2E7D32` | Primary, buttons, headers |
| Warm Amber | `#F9A825` | Accent, gallery button, highlights |
| Off-White/Cream | `#F5F5F0` | Background |
| Near Black | `#1C1C1C` | Body text |
| Deep Red | `#C62828` | High severity alerts |

---

## 📚 College Project Context

**Course:** Interdisciplinary Project
**Problem:** Small and marginal farmers lose a large share of every crop to plant disease and unpredictable weather, and expert help rarely reaches villages with poor connectivity
**Solution:** Edge-AI diagnosis tool that works in zero-connectivity rural areas
**Disciplines:** Agriculture + Computer Science (AI/ML) + Design Thinking

---

## 🔒 Privacy

All data stays on the device. No photos, location, or farmer data is ever sent to a server. The TFLite model runs entirely offline.

---

*Built with ❤️ for Indian farmers*
