# 🌋 Multi-Sensor Environmental Assessment of Mount Bromo: Wildfire Impact, LULC Dynamics, and Atmospheric Emissions Profiling (2022–2024)

Ekosistem skrip **Google Earth Engine (GEE)** komprehensif untuk memetakan, memodelkan, dan menganalisis dampak ekologis serta jejak atmosferik akibat kebakaran hutan besar di kawasan Taman Nasional Bromo Tengger Semeru (TNBTS) pada September 2023.

---

## 📌 1. Alur Arsitektur Sistem

Proyek ini mengintegrasikan data penginderaan jauh multi-sensor (*Sentinel-2 L2A* & *Sentinel-5P TROPOMI*) beserta data reanalisis iklim (*ERA5*) untuk melacak perubahan biofisik daratan sebelum, selama, dan setelah bencana.

```metasql
🧭 ALUR ANALISIS GEOSPASIAL BROMO
├── 🟢 Bagian A: Dinamika Terestrial & Vegetasi (Sentinel-2)
│   ├── Modul 1: LULC Tracking (Algoritma Random Forest - 100 Trees)
│   ├── Modul 2: Mapping Keparahan Kebakaran (Format dNBR Global AOI)
│   └── Modul 7: Profiling Piksel Mikro dNBR (Zonasi Lokal Box 1, 2, 3)
│
├── 🟠 Bagian B: Pemantauan Atmosfer & Emisi (Sentinel-5P TROPOMI)
│   ├── Modul 3: Absorbing Aerosol Index (AAI) & Spasial Kerapatan Partikulat
│   ├── Modul 5: Combined Sensor Mapping (Integrasi Dinamis Aerosol & CO)
│   └── Modul 6: Ekstraksi Array Data Kontinu Karbon Monoksida (CO)
│
└── 🔵 Bagian C: Pemodelan Iklim & Transportasi Polutan (ERA5 Reanalysis)
    └── Modul 4: Integrasi Vektor Angin (U/V 10m) & Pemetaan Dispersi NO₂
```

---

## 🛠️ 2. Katalog Modul & Tautan Skrip GEE

Seluruh skrip di bawah ini siap dijalankan secara interaktif melalui Google Earth Engine Code Editor:

### 🔹 Bagian A: Dinamika Terestrial & Keparahan Kebakaran (Sentinel-2)

| Modul | Fokus Analisis | Deskripsi Teknikal | Akses Skrip |
| :---: | :--- | :--- | :---: |
| **Modul 1** | LULC Tracking (2022–2024) | Klasifikasi tutupan lahan (4 kelas) menggunakan **Random Forest**. Dilengkapi kalkulasi luas area (Hektar) dan matriks akurasi resubstitusi. | [Buka Skrip 🔗](https://code.earthengine.google.com/b46b2264328ccee4179b296ed1754d96) |
| **Modul 2** | Burn Severity ($dNBR$) | Deliniasi regional area terdampak kebakaran dengan indeks $dNBR$ (SCL Masked) berdasarkan standar USGS global seluruh AOI. | [Buka Skrip 🔗](https://code.earthengine.google.com/df47951fd395ec83fdf8fe5189d0ec34) |
| **Modul 7** | Localized $dNBR$ Pixel | Ekstraksi array nilai piksel $dNBR$ resolusi tinggi (skala 20m) pada 3 zonasi *box chart* kustom untuk analisis variabilitas mikro kerusakan vegetasi. | [Buka Skrip 🔗](https://code.earthengine.google.com/9b2f22a07a811919d13186ce46f6c1a3) |

### 🔹 Bagian B: Pemantauan Atmosfer & Dinamika Angin (Sentinel-5P & ERA5)

| Modul | Fokus Analisis | Deskripsi Teknikal | Akses Skrip |
| :---: | :--- | :--- | :---: |
| **Modul 3** | Aerosol Index (AAI) | Pemantauan kerapatan aerosol partikulat atmosfer sebelum dan saat kebakaran menggunakan ekstraksi spasial berbasis *Box Pixel Extraction* pada Periode 2. | [Buka Skrip 🔗](https://code.earthengine.google.com/5f5f4a955c66143a5aa1427626d52094) |
| **Modul 4** | $\text{NO}_2$ & Wind Dynamics | Korelasi spasial konsentrasi $\text{NO}_2$ harian dan arah/kecepatan angin menggunakan data vektor komponen $u$ dan $v$ **ERA5 Reanalysis** (ketinggian 10m). | [Buka Skrip 🔗](https://code.earthengine.google.com/7ec3d3a043d090776f902bdad2300b16) |
| **Modul 5** | Combined Aerosol & $\text{CO}$ | Pemetaan multi-parameter dinamis yang menggabungkan matriks sebaran Aerosol Index dan Karbon Monoksida ($\text{CO}$) lintas dua periode kritis (1–5 Sep vs 6–15 Sep 2023). | [Buka Skrip 🔗](https://code.earthengine.google.com/0f45a927cb5cd9fac5e68a53779d0db8) |
| **Modul 6** | $\text{CO}$ Array Extraction | Isolasi data spasial kontinu Karbon Monoksida ($\text{CO}$) menggunakan skema reduksi wilayah (`ee.Reducer.toList()`) pada 3 sektor sampel area makro (Periode 2). | [Buka Skrip 🔗](https://code.earthengine.google.com/6efbe7eba42998aa28cdb4972b4fc8fa) |

---

## 📐 3. Landasan Metodologi & Formulasi Spektral

### A. Indeks Spektral Kebakaran (Sentinel-2)
Aktivitas kebakaran dideteksi menggunakan kombinasi saluran NIR (Band 8) dan SWIR (Band 12). Formulasi *Normalized Burn Ratio* ($NBR$) didefinisikan sebagai:

$$NBR = \frac{\text{B8} - \text{B12}}{\text{B8} + \text{B12}}$$

Selisih indeks ($dNBR$) dihitung untuk memperoleh komparasi absolut tingkat kerusakan biomassa vegetasi:

$$dNBR = NBR_{\text{pre}} - NBR_{\text{post}}$$

> [!NOTE]
> **Klasifikasi Threshold Kebakaran (USGS Standard):**
> * **Low Severity:** $0.10 < dNBR \le 0.27$
> * **Moderate Severity:** $0.27 < dNBR \le 0.44$
> * **High Severity:** $dNBR > 0.44$

### B. Rekonstruksi Dinamika Vektor Angin (ERA5)
Dispersi polutan udara ($\text{NO}_2$ dan $\text{CO}$) dipengaruhi oleh pergerakan massa udara. Arah dan kecepatan angin dihitung secara trigonometris dari komponen angin zonal ($u$) dan komponen angin meridional ($v$) pada altitudo 10 meter:

$$\text{Wind Speed} = \sqrt{u^2 + v^2}$$

$$\text{Wind Direction (Degrees)} = \arctan2(v, u) \times \left(\frac{180}{\pi}\right) + 180$$

### C. Ekstraksi Profil Piksel (Zonasi Box 1, 2, 3)
Untuk keperluan validasi statistik, fungsi `reduceRegion` dikombinasikan dengan `ee.Reducer.toList()` digunakan untuk mengubah representasi spasial piksel raster menjadi struktur array linear (list data) di dalam geometri `box_1`, `box_2`, dan `box_3`. Pendekatan ini diterapkan pada parameter $dNBR$ (skala 20m), Aerosol Index (skala 1000m), dan Karbon Monoksida (skala 1000m).

---

## 📊 4. Antarmuka Grafis & Dashboard Interaktif

Seluruh skrip telah dioptimalkan dengan antarmuka grafis (GUI) interaktif langsung pada panel Google Earth Engine Code Editor:
* 🎚️ **Dual Palette Gradient Legend:** Komponen visualisasi polutan udara menggunakan bar gradien dua sisi untuk membedakan konsentrasi gas secara intuitif.
* 📈 **Multi-Temporal Line Charts:** Grafik deret waktu harian otomatis untuk mendeteksi lonjakan polutan atmosferik tepat pada waktu mula kebakaran (*analisis onset*).
* 📦 **Statistical Box Charts:** Representasi grafis distribusi piksel mikro guna mendukung analisis statistik sebaran polutan dan identifikasi pencilan (*outliers*).

---

## 🚀 5. Panduan Operasional Run Skrip

1. **Akses Link GEE:** Buka salah satu tautan skrip di atas melalui peramban yang telah terautentikasi dengan akun Google Earth Engine.
2. **Definisikan Region of Interest (ROI):**
   > [!IMPORTANT]
   > **Khusus Modul 3, 6, dan 7:** Sebelum menekan tombol **Run**, gunakan ikon *Drawing Tools* di sudut kiri atas peta untuk menggambar tiga geometri poligon/persegi terpisah. Ganti nama variabel default geometry tersebut menjadi `box_1`, `box_2`, dan `box_3`.
3. **Eksekusi:** Klik tombol **Run** pada panel kontrol atas GEE Code Editor.
4. **Analisis Output:** Periksa tab **Console** di panel kanan layar untuk melihat hasil grafik tren harian, matriks akurasi *error matrix*, komparasi statistik *box*, serta luas wilayah terdampak dalam satuan Hektar (ha).

---

## 👥 6. Kolaborasi & Sitasi Peneliti

Repository ini bersifat terbuka untuk keperluan akademis, penelitian lanjutan, dan pengembangan model mitigasi bencana geo-atmosfer.

```text
Sitasi Rekomendasi:
[Nama Anda/Institusi], 2026. Analisis Spasial Multi-Sensor Dampak Kebakaran Hutan Gunung Bromo Menggunakan Google Earth Engine. Repositori GitHub.
```
