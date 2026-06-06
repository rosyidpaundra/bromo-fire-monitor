# 🌋 Bromo Fire Emission & Burn Severity Tracker
**Pemantauan Tingkat Keparahan Kebakaran (dNBR), Emisi Kualitas Udara (Aerosol, NO2, CO), dan Dinamika Angin berbasis Google Earth Engine (GEE)**

![Google Earth Engine](https://img.shields.io/badge/Google_Earth_Engine-JavaScript-4285F4?style=for-the-badge&logo=google)
![Sentinel](https://img.shields.io/badge/Copernicus-Sentinel--2_%7C_Sentinel--5P-1E88E5?style=for-the-badge)
![Climate](https://img.shields.io/badge/ECMWF-ERA5_Wind_Vectors-00ACC1?style=for-the-badge)

## 📌 Deskripsi
Repositori ini berisi serangkaian *script* Google Earth Engine (GEE) yang dioptimalkan untuk mengevaluasi dampak langsung dari insiden kebakaran hutan di kawasan Taman Nasional Bromo Tengger Semeru pada **September 2023**.

Analisis dalam repositori ini berfokus pada dua aspek krusial pasca-bencana:
1. **Dampak Ekologis:** Mengukur luasan dan tingkat keparahan area yang terbakar (*Burn Severity*) menggunakan indeks spektral dNBR.
2. **Dampak Atmosferik & Emisi:** Memantau sebaran gas berbahaya (Aerosol, NO2, dan Karbon Monoksida/CO), serta menganalisis arah angin yang membawa polutan tersebut, lengkap dengan ekstraksi nilai piksel untuk analisis statistik (*Box Plot*).

---

## 🚀 Koleksi Modul Analisis
Riset ini dibagi menjadi 6 modul spesifik. Klik tautan untuk menjalankan simulasi langsung di *Code Editor* GEE:

| Modul | Fokus Analisis | Tautan GEE |
| :---: | :--- | :--- |
| 🔥 | **Modul 1: Burn Severity (dNBR) Global** <br> *Klasifikasi area terbakar (Low, Mod, High) menggunakan Sentinel-2 (Pra: 1-5 Sep, Pasca: 6-15 Sep).* | [▶️ Buka Script](https://code.earthengine.google.com/b46b2264328ccee4179b296ed1754d96) |
| 🌫️ | **Modul 2: Aerosol Index Dynamics** <br> *Pemantauan ketebalan polusi asap (Aerosol) dengan S5P, dilengkapi time-series & box plot area.* | [▶️ Buka Script](https://code.earthengine.google.com/df47951fd395ec83fdf8fe5189d0ec34) |
| ☠️ | **Modul 3: NO2 Emissions & Wind Vectors** <br> *Analisis kepadatan kolom NO2 (S5P) dikorelasikan dengan arah & kecepatan angin (ERA5).* | [▶️ Buka Script](https://code.earthengine.google.com/5f5f4a955c66143a5aa1427626d52094) |
| 🔄 | **Modul 4: Integrasi Aerosol & CO** <br> *Pemantauan gabungan Aerosol Index dan Karbon Monoksida (CO) dengan komparasi 4 grafik time-series.* | [▶️ Buka Script](https://code.earthengine.google.com/0f45a927cb5cd9fac5e68a53779d0db8) |
| ☁️ | **Modul 5: Carbon Monoxide (CO) Focus** <br> *Analisis spesifik emisi CO (mol/m²) dengan grafik deret waktu dan ekstraksi array untuk Box Plot.* | [▶️ Buka Script](https://code.earthengine.google.com/6efbe7eba42998aa28cdb4972b4fc8fa) |
| 📊 | **Modul 6: dNBR Pixel Extraction (Box Plot)** <br> *Klasifikasi dNBR ditambah dengan fungsi ekstraksi nilai piksel mentah pada 3 zona sampel spesifik.* | [▶️ Buka Script](https://code.earthengine.google.com/9b2f22a07a811919d13186ce46f6c1a3) |

*(Akses memerlukan akun Google Earth Engine).*

---

## ✨ Fitur Utama & Metodologi
### 1. Burn Severity Assessment (dNBR)
* **Formula:** Menghitung selisih *Normalized Burn Ratio* (Pre-fire NBR dikurangi Post-fire NBR).
* **Klasifikasi USGS:** Secara otomatis membagi tingkat keparahan menjadi *Low* (0.1 - 0.27), *Moderate* (0.27 - 0.44), dan *High* (> 0.44).
* **Output:** Peta visualisasi keparahan, legenda interaktif, dan grafik batang luasan (dalam Hektar).

### 2. Air Quality & Emission Monitoring (S5P)
* **Parameter Atmosfer:** Memantau *Absorbing Aerosol Index* (AAI), *NO2 Column Number Density*, dan *CO Column Number Density*.
* **Analisis Temporal:** Membandingkan emisi pra-kebakaran (awal September) dengan masa puncak eskalasi kebakaran (6-15 September).
* **Charting:** Menghasilkan grafik deret waktu (*time-series*) rata-rata polusi harian secara otomatis.

### 3. Ekstraksi Data Statistik (Box Plot Analysis)
* Sistem `Reducer.toList()` digunakan untuk mengekst
