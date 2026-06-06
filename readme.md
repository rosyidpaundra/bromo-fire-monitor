# Multi-Sensor Environmental Assessment of Mount Bromo: Wildfire Impact, LULC Dynamics, and Atmospheric Emissions Profiling (2022–2024)

[![Earth Engine](https://img.shields.io/badge/Earth%20Engine-Google-blue)](https://earthengine.google.com/)
[![Satellite-Sentinel2](https://img.shields.io/badge/Satellite-Sentinel--2-green)](https://sentinels.copernicus.eu/)
[![Satellite-Sentinel5P](https://img.shields.io/badge/Satellite-Sentinel--5P-orange)](https://sentinels.copernicus.eu/)
[![Climate-ERA5](https://img.shields.io/badge/Climate-ERA5%20Reanalysis-red)](https://www.ecmwf.int/)

Repository ini menyediakan ekosistem skrip **Google Earth Engine (GEE)** lengkap untuk memetakan, memodelkan, dan menganalisis dampak ekologis serta jejak atmosferik akibat kebakaran hutan besar di kawasan Taman Nasional Bromo Tengger Semeru (TNBTS) pada September 2023. 

Proyek ini mengintegrasikan data penginderaan jauh multi-sensor (Sentinel-2 L2A & Sentinel-5P TROPOMI) beserta data reanalisis iklim (ERA5) untuk melacak perubahan biofisik daratan sebelum, selama, dan setelah kejadian bencana.

---

## 📌 Alur Arsitektur Sistem

Penelitian geospasial ini dibagi menjadi tiga pilar utama: dinamika permukaan (*terrestrial dynamics*), emisi gas & partikulat (*atmospheric tracking*), dan ekstraksi profil spasial mikro (*box pixel statistical profile*).

[1. Terrestrial Dynamics]     ──> S2 Random Forest Classifier & Burn Severity (dNBR)
[2. Atmospheric Emissions]    ──> S5P TROPOMI Monitoring (Aerosol Index, NO2, CO)
[3. Micro-Spatial Extraction] ──> Region-of-Interest (ROI) Array Extraction (Box 1, 2, 3)

Berikut adalah draf pembaruan `README.md` GitHub yang telah diintegrasikan secara komprehensif untuk mencakup seluruh **7 skrip analisis**. Struktur metrik, arsitektur alur kerja, dan pembagian modul telah diperbarui agar selaras dengan standar publikasi ilmiah repositori data geospasial.

---

```markdown
# Multi-Sensor Environmental Assessment of Mount Bromo: Wildfire Impact, LULC Dynamics, and Atmospheric Emissions Profiling (2022–2024)

[![Earth Engine](https://img.shields.io/badge/Earth%20Engine-Google-blue)](https://earthengine.google.com/)
[![Satellite-Sentinel2](https://img.shields.io/badge/Satellite-Sentinel--2-green)](https://sentinels.copernicus.eu/)
[![Satellite-Sentinel5P](https://img.shields.io/badge/Satellite-Sentinel--5P-orange)](https://sentinels.copernicus.eu/)
[![Climate-ERA5](https://img.shields.io/badge/Climate-ERA5%20Reanalysis-red)](https://www.ecmwf.int/)

Repository ini menyediakan ekosistem skrip **Google Earth Engine (GEE)** lengkap untuk memetakan, memodelkan, dan menganalisis dampak ekologis serta jejak atmosferik akibat kebakaran hutan besar di kawasan Taman Nasional Bromo Tengger Semeru (TNBTS) pada September 2023. 

Proyek ini mengintegrasikan data penginderaan jauh multi-sensor (Sentinel-2 L2A & Sentinel-5P TROPOMI) beserta data reanalisis iklim (ERA5) untuk melacak perubahan biofisik daratan sebelum, selama, dan setelah kejadian bencana.

---

## 📌 Alur Arsitektur Sistem

Penelitian geospasial ini dibagi menjadi tiga pilar utama: dinamika permukaan (*terrestrial dynamics*), emisi gas & partikulat (*atmospheric tracking*), dan ekstraksi profil spasial mikro (*box pixel statistical profile*).


```

[1. Terrestrial Dynamics]     ──> S2 Random Forest Classifier & Burn Severity (dNBR)
[2. Atmospheric Emissions]    ──> S5P TROPOMI Monitoring (Aerosol Index, NO2, CO)
[3. Micro-Spatial Extraction] ──> Region-of-Interest (ROI) Array Extraction (Box 1, 2, 3)

```

---

## 🛠️ Modul Arsitektur & Tautan Skrip GEE

Seluruh skrip di bawah ini siap dijalankan secara interaktif melalui Google Earth Engine Code Editor:

### Bagian A: Dinamika Terestrial & Keparahan Kebakaran (Sentinel-2)
| Modul | Fokus Analisis | Deskripsi Teknikal | Akses Skrip (GEE) |
| :--- | :--- | :--- | :--- |
| **Modul 1** | **Multi-Temporal LULC Tracking** | Klasifikasi tutupan lahan (4 kelas) menggunakan algoritma **Random Forest (100 Trees)** pada citra Sentinel-2 (2022–2024). Dilengkapi dengan kalkulasi luas area (Hektar) dan matriks akurasi resubstitusi. | [Buka Skrip Modul 1 🔗](https://code.earthengine.google.com/b46b2264328ccee4179b296ed1754d96) |
| **Modul 2** | **Burn Severity Mapping (dNBR)** | Deliniasi area terdampak kebakaran menggunakan indeks $dNBR$ dari Sentinel-2 L2A (SCL Masked). Mengklasifikasikan tingkat keparahan berdasarkan standar USGS (Low, Moderate, High Severity). | [Buka Skrip Modul 2 🔗](https://code.earthengine.google.com/df47951fd395ec83fdf8fe5189d0ec34) |
| **Modul 7** | **Localized $dNBR$ Pixel Profile** | Ekstraksi array nilai piksel $dNBR$ resolusi tinggi (skala 20m) pada 3 zonasi *box chart* kustom untuk analisis variabilitas mikro tingkat kerusakan vegetasi. | [Buka Skrip Modul 7 🔗](https://code.earthengine.google.com/9b2f22a07a811919d13186ce46f6c1a3) |

### Bagian B: Pemantauan Atmosfer & Dinamika Angin (Sentinel-5P & ERA5)
| Modul | Fokus Analisis | Deskripsi Teknikal | Akses Skrip (GEE) |
| :--- | :--- | :--- | :--- |
| **Modul 3** | **Absorbing Aerosol Index (AAI)** | Pemantauan kerapatan aerosol partikulat di atmosfer sebelum dan saat kebakaran menggunakan Sentinel-5P TROPOMI. Menggunakan ekstraksi spasial berbasis *Box Pixel Extraction* pada Periode 2. | [Buka Skrip Modul 3 🔗](https://code.earthengine.google.com/5f5f4a955c66143a5aa1427626d52094) |
| **Modul 4** | **$NO_2$ Concentration & Wind Dynamics** | Analisis korelasi spasial antara konsentrasi Nitrogen Dioksida ($NO_2$) dan arah/kecepatan angin menggunakan data **ERA5 Reanalysis** (komponen $u$ dan $v$ pada ketinggian 10m). | [Buka Skrip Modul 4 🔗](https://code.earthengine.google.com/7ec3d3a043d090776f902bdad2300b16) |
| **Modul 5** | **Combined Aerosol & $CO$ Mapping** | Pemetaan multi-parameter dinamis yang menggabungkan matriks sebaran Aerosol Index dan Karbon Monoksida ($CO$) lintas dua periode kritis (1-5 Sep vs 6-15 Sep 2023). | [Buka Skrip Modul 5 🔗](https://code.earthengine.google.com/0f45a927cb5cd9fac5e68a53779d0db8) |
| **Modul 6** | **Carbon Monoxide ($CO$) Array Extraction** | Isolasi data spasial kontinu Karbon Monoksida ($CO$) dari Sentinel-5P TROPOMI menggunakan skema reduksi wilayah (`ee.Reducer.toList()`) pada 3 sektor sampel area makro. | [Buka Skrip Modul 6 🔗](https://code.earthengine.google.com/6efbe7eba42998aa28cdb4972b4fc8fa) |

---

## 📐 Landasan Metodologi & Formulasi Spektral

### 1. Indeks Spektral Kebakaran (Sentinel-2)
Aktivitas kebakaran dideteksi menggunakan kombinasi saluran NIR (Band 8) dan SWIR (Band 12). Formulasi *Normalized Burn Ratio* ($NBR$) didefinisikan sebagai:

$$NBR = \frac{B8 - B12}{B8 + B12}$$

Selisih indeks ($dNBR$) dihitung untuk memperoleh komparasi absolut tingkat kerusakan biomassa:

$$dNBR = NBR_{pre} - NBR_{post}$$

> **Klasifikasi Threshold USGS:**
> * Low Severity: $0.10 < dNBR \le 0.27$
> * Moderate Severity: $0.27 < dNBR \le 0.44$
> * High Severity: $dNBR > 0.44$

### 2. Rekonstruksi Dinamika Vektor Angin (ERA5)
Dispersi polutan udara ($NO_2$ dan $CO$) dipengaruhi oleh pergerakan massa udara. Arah dan kecepatan angin dihitung secara trigonometris dari komponen angin zonal ($u$) dan komponen angin meridional ($v$) pada altitudo 10 meter:

$$\text{Wind Speed} = \sqrt{u^2 + v^2}$$

$$\text{Wind Direction (Degrees)} = \arctan2(v, u) \times \left(\frac{180}{\pi}\right) + 180$$

### 3. Ekstraksi Profil Piksel (Zonasi Box 1, 2, 3)
Untuk keperluan validasi statistik, fungsi `reduceRegion` dikombinasikan dengan `ee.Reducer.toList()` digunakan untuk mengubah representasi spasial piksel raster menjadi struktur array linear (list data) di dalam geometri `box_1`, `box_2`, dan `box_3`. Pendekatan ini diterapkan pada parameter $dNBR$ (skala 20m), Aerosol Index (skala 1000m), dan Karbon Monoksida (skala 1000m).

---

## 📊 Visualisasi & Dashboard Interaktif GEE

Seluruh skrip telah dioptimalkan dengan antarmuka grafis (GUI) interaktif pada *Code Editor*:
* **Dual Palette Gradient Legend:** Komponen visualisasi polutan udara menggunakan visualisasi bar gradien dua sisi untuk membedakan konsentrasi gas secara intuitif.
* **Multi-Temporal Line Charts:** Grafik deret waktu harian otomatis untuk mendeteksi lonjakan polutan atmosferik tepat pada waktu mula kebakaran (*onset of wildfire*).
* **Statistical Box Charts:** Representasi grafis distribusi piksel mikro guna mendukung analisis statistik sebaran polutan dan identifikasi pencilan (*outliers*).

---

## 🚀 Panduan Operasional

1. Akses salah satu link repositori GEE di atas menggunakan peramban web yang telah terautentikasi dengan akun Google Earth Engine.
2. **Penting untuk Modul 3, 6, dan 7:** Sebelum menekan tombol **Run**, gunakan ikon *Drawing Tools* di sudut kiri atas peta untuk menggambar tiga geometri poligon/persegi terpisah. Ganti nama variabel default menjadi `box_1`, `box_2`, dan `box_3`.
3. Klik tombol **Run** pada panel kontrol atas.
4. Periksa tab **Console** di sisi kanan layar untuk mengamati visualisasi grafik tren, matriks *error matrix*, hasil ekstraksi list array, serta luas wilayah terdampak dalam satuan Hektar (ha).

---

## 👥 Kolaborasi & Sitasi Peneliti

Proyek open-source ini ditujukan sebagai referensi ilmiah dasar untuk pemodelan polusi udara akibat kebakaran hutan di wilayah kompleks tropis dan vulkanis.

```text
Sitasi Rekomendasi:
[Nama Anda/Institusi], 2026. Analisis Spasial Multi-Sensor Dampak Kebakaran Hutan Gunung Bromo Menggunakan Google Earth Engine. Repositori GitHub.

```

```

```
