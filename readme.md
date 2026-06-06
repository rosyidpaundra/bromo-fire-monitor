Berikut adalah satu format file Markdown (`README.md`) utuh yang sudah diintegrasikan secara lengkap dengan ke-7 skrip dan tautannya. Anda tinggal menyalin (*copy*) seluruh isi kotak kode di bawah ini:

```markdown
# 🌋 Multi-Sensor Environmental Assessment of Mount Bromo: Wildfire Impact, LULC Dynamics, and Atmospheric Emissions Profiling (2022–2024)

Kumpulan skrip **Google Earth Engine (GEE)** komprehensif untuk memetakan, memodelkan, dan menganalisis dampak ekologis serta jejak atmosferik akibat kebakaran hutan besar di kawasan Taman Nasional Bromo Tengger Semeru (TNBTS) pada September 2023.

[![Earth Engine](https://img.shields.io/badge/Earth%20Engine-Google-blue?style=for-the-badge&logo=googleearth)](https://earthengine.google.com/)
[![Satellite-Sentinel2](https://img.shields.io/badge/Satellite-Sentinel--2-green?style=for-the-badge&logo=esa)](https://sentinels.copernicus.eu/)
[![Satellite-Sentinel5P](https://img.shields.io/badge/Satellite-Sentinel--5P-orange?style=for-the-badge&logo=esa)](https://sentinels.copernicus.eu/)
[![Climate-ERA5](https://img.shields.io/badge/Climate-ERA5%20Reanalysis-red?style=for-the-badge)](https://www.ecmwf.int/)

---

## 📌 1. Alur Arsitektur Sistem

Proyek ini mengintegrasikan data penginderaan jauh multi-sensor (*Sentinel-2 L2A* & *Sentinel-5P TROPOMI*) beserta data reanalisis iklim (*ERA5*) untuk melacak perubahan biofisik daratan sebelum, selama, dan setelah bencana yang dibagi menjadi tiga pilar utama:

```metasql
🧭 ALUR ANALISIS GEOSPASIAL BROMO
├── 🟢 [1. Terrestrial Dynamics]     
│   └── Sentinel-2: Random Forest Classifier (4 Kelas) & Burn Severity (dNBR)
├── 🟠 [2. Atmospheric Emissions]    
│   └── Sentinel-5P TROPOMI: Monitoring (Aerosol Index, NO2, CO) & Dispersi Angin ERA5
└── 🔵 [3. Micro-Spatial Extraction] 
    └── GEE Reducer: Region-of-Interest (ROI) Array Extraction (Zonasi Box 1, 2, 3)
```

---

## 🛠️ 2. Modul Arsitektur & Tautan Skrip GEE

Seluruh skrip di bawah ini siap dijalankan secara interaktif melalui Google Earth Engine Code Editor:

### 🔹 Bagian A: Dinamika Terestrial & Keparahan Kebakaran (Sentinel-2)

| Modul | Fokus Analisis | Deskripsi Teknikal | Akses Skrip (GEE) |
| :---: | :--- | :--- | :---: |
| **Modul 1** | LULC Tracking (2022–2024) | Klasifikasi tutupan lahan menggunakan algoritma **Random Forest (100 Trees)**. Dilengkapi kalkulasi luas area (Hektar) dan matriks akurasi resubstitusi. | [Buka Skrip 🔗](https://code.earthengine.google.com/b46b2264328ccee4179b296ed1754d96) |
| **Modul 2** | Burn Severity Mapping ($dNBR$) | Deliniasi area terdampak kebakaran dengan indeks $dNBR$ (SCL Masked) berdasarkan standar USGS global seluruh AOI. | [Buka Skrip 🔗](https://code.earthengine.google.com/df47951fd395ec83fdf8fe5189d0ec34) |
| **Modul 7** | Localized $dNBR$ Pixel Profile | Ekstraksi array nilai piksel $dNBR$ resolusi tinggi (skala 20m) pada 3 zonasi *box chart* kustom untuk analisis variabilitas mikro kerusakan vegetasi. | [Buka Skrip 🔗](https://code.earthengine.google.com/9b2f22a07a811919d13186ce46f6c1a3) |

### 🔹 Bagian B: Pemantauan Atmosfer & Dinamika Angin (Sentinel-5P & ERA5)

| Modul | Fokus Analisis | Deskripsi Teknikal | Akses Skrip (GEE) |
| :---: | :--- | :--- | :---: |
| **Modul 3** | Absorbing Aerosol Index (AAI) | Pemantauan kerapatan aerosol partikulat atmosfer sebelum dan saat kebakaran menggunakan ekstraksi spasial berbasis *Box Pixel Extraction* pada Periode 2. | [Buka Skrip 🔗](https://code.earthengine.google.com/5f5f4a955c66143a5aa1427626d52094) |
| **Modul 4** | $NO_2$ & Wind Dynamics | Korelasi spasial konsentrasi $NO_2$ harian dan arah/kecepatan angin menggunakan data vektor **ERA5 Reanalysis** (ketinggian 10m). | [Buka Skrip 🔗](https://code.earthengine.google.com/7ec3d3a043d090776f902bdad2300b16) |
| **Modul 5** | Combined Aerosol & $CO$ Mapping | Pemetaan multi-parameter dinamis yang menggabungkan matriks sebaran Aerosol Index dan Karbon Monoksida ($CO$) lintas dua periode kritis (1-5 Sep vs 6-15 Sep 2023). | [Buka Skrip 🔗](https://code.earthengine.google.com/0f45a927cb5cd9fac5e68a53779d0db8) |
| **Modul 6** | $CO$ Array Extraction | Isolasi data spasial kontinu Karbon Monoksida ($CO$) menggunakan skema reduksi wilayah (`ee.Reducer.toList()`) pada 3 sektor sampel area makro (Periode 2). | [Buka Skrip 🔗](https://code.earthengine.google.com/6efbe7eba42998aa28cdb4972b4fc8fa) |

---

## 📐 3. Landasan Metodologi & Formulasi Spektral

### A. Indeks Spektral Kebakaran (Sentinel-2)
Aktivitas kebakaran dideteksi menggunakan kombinasi saluran NIR (Band 8) dan SWIR (Band 12). Formulasi *Normalized Burn Ratio* ($NBR$) didefinisikan sebagai:

$$NBR = \frac{B8 - B12}{B8 + B12}$$

Selisih indeks ($dNBR$) dihitung untuk memperoleh komparasi absolut tingkat kerusakan biomassa:

$$dNBR = NBR_{pre} - NBR_{post}$$

> [!NOTE]
> **Klasifikasi Threshold Kebakaran (USGS Standard):**
> * **Low Severity:** $0.10 < dNBR \le 0.27$
> * **Moderate Severity:** $0.27 < dNBR \le 0.44$
> * **High Severity:** $dNBR > 0.44$

### B. Rekonstruksi Dinamika Vektor Angin (ERA5)
Dispersi polutan udara ($NO_2$ dan $CO$) dipengaruhi oleh pergerakan massa udara. Arah dan kecepatan angin dihitung secara trigonometris dari komponen angin zonal ($u$) dan komponen angin meridional ($v$) pada ketinggian 10 meter:

$$\text{Wind Speed} = \sqrt{u^2 + v^2}$$

$$\text{Wind Direction (Degrees)} = \arctan2(v, u) \times \left(\frac{180}{\pi}\right) + 180$$

### C. Ekstraksi Profil Piksel (Zonasi Box 1, 2, 3)
Untuk keperluan validasi statistik, fungsi `reduceRegion` dikombinasikan dengan `ee.Reducer.toList()` digunakan untuk mengubah representasi spasial piksel raster menjadi struktur array linear (list data) di dalam geometri `box_1`, `box_2`, dan `box_3`. Pendekatan ini diterapkan pada parameter $dNBR$ (skala 20m), Aerosol Index (skala 1000m), dan Karbon Monoksida (skala 1000m).

---

## 📊 4. Visualisasi & Dashboard Interaktif GEE

Seluruh skrip telah dilengkapi dengan antarmuka grafis (GUI) interaktif langsung pada panel Google Earth Engine:
* **Dual Palette Gradient Legend:** Komponen visualisasi polutan udara menggunakan bar gradien dua sisi untuk membedakan konsentrasi gas secara intuif.
* **Multi-Temporal Line Charts:** Grafik deret waktu harian otomatis untuk mendeteksi lonjakan polutan atmosferik tepat pada waktu mula kebakaran (*onset of wildfire*).
* **Statistical Box Charts:** Representasi grafis distribusi piksel mikro guna mendukung analisis statistik sebaran polutan dan identifikasi pencilan (*outliers*).

---

## 🚀 5. Panduan Operasional Run Skrip

1. Akses salah satu link repositori GEE di atas menggunakan peramban web yang telah terautentikasi dengan akun Google Earth Engine.
2. > [!IMPORTANT]
   > **Khusus Modul 3, 6, dan 7:** Sebelum menekan tombol **Run**, gunakan ikon *Drawing Tools* di sudut kiri atas peta untuk menggambar tiga geometri poligon/persegi terpisah. Ganti nama variabel default geometry tersebut menjadi `box_1`, `box_2`, dan `box_3`.
3. Klik tombol **Run** pada panel kontrol atas Code Editor.
4. Periksa tab **Console** di sisi kanan layar untuk mengamati visualisasi grafik tren, matriks *error matrix*, hasil ekstraksi list array, serta luas wilayah terdampak dalam satuan Hektar (ha).

---

## 👥 6. Kolaborasi & Sitasi Peneliti

Repository ini bersifat terbuka untuk keperluan akademis, penelitian lanjutan, dan mitigasi bencana geo-atmosfer.

```text
Sitasi Rekomendasi:
[Nama Anda/Institusi], 2026. Analisis Spasial Multi-Sensor Dampak Kebakaran Hutan Gunung Bromo Menggunakan Google Earth Engine. Repositori GitHub.
```


```
