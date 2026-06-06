# 🔥 Bromo Fire Impact & LULC Dynamics Monitor
**Pemantauan Dampak Kebakaran Hutan, Dinamika Tutupan Lahan, dan Analisis Spasial Kawasan Bromo berbasis Google Earth Engine (GEE)**

![Google Earth Engine](https://img.shields.io/badge/Google_Earth_Engine-JavaScript-4285F4?style=for-the-badge&logo=google)
![Machine Learning](https://img.shields.io/badge/Machine_Learning-Random_Forest_%7C_SVM-FF6F00?style=for-the-badge)
![Disaster Management](https://img.shields.io/badge/Disaster_Management-Wildfire_Monitoring-E53935?style=for-the-badge)

## 📌 Deskripsi
**Bromo Fire Impact Monitor** adalah kumpulan *script* Google Earth Engine (GEE) komprehensif yang dirancang untuk memetakan secara presisi dampak kebakaran hutan yang melanda kawasan Taman Nasional Bromo Tengger Semeru.

Dengan mengkomparasikan klasifikasi tutupan lahan (*Land Use Land Cover* / LULC) secara multi-tahun, aplikasi ini mengkuantifikasi transisi fase ekologis: kondisi **Pra-kebakaran (2022)**, **Periode Kebakaran (2023)**, hingga **Pasca-kebakaran & Pemulihan Ekosistem (2024)**. 

Aplikasi ini dirancang untuk mendukung kegiatan:
* 🔬 Riset ekologi restorasi dan geomatika kebencanaan.
* 🌲 Kuantifikasi luasan area vegetasi yang hangus terbakar menjadi lahan terbuka (*burnt area/bare land*).
* 🤖 Uji komparasi algoritma *Machine Learning* dalam mendeteksi perubahan tutupan lahan ekstrem.
* 🏛️ Pembuatan landasan kebijakan mitigasi kebakaran lahan oleh otoritas taman nasional.

---

## 🚀 Modul Analisis Kebakaran Bromo
Riset ini dipecah ke dalam beberapa *script* terintegrasi. Anda dapat menelusuri evolusi dampak kebakaran melalui tautan berikut:

| Modul | Fokus Analisis | Tautan GEE |
| :---: | :--- | :--- |
| 🗂️ | **Modul Utama:** Master LULC & Fire Impact Bromo | [▶️ Buka Script](https://code.earthengine.google.com/?scriptPath=users%2Frosyidpaundra%2Fmangrove%3ALULC_BROMO) |
| 🌿 | **Fase 1:** LULC Kondisi Pra-Kebakaran (2022) | [▶️ Buka Script](https://code.earthengine.google.com/df47951fd395ec83fdf8fe5189d0ec34) |
| 🔥 | **Fase 2:** LULC Periode Kebakaran & Eskalasi (2023) | [▶️ Buka Script](https://code.earthengine.google.com/5f5f4a955c66143a5aa1427626d52094) |
| 🌱 | **Fase 3:** LULC Pasca-Kebakaran / Pemulihan (2024) | [▶️ Buka Script](https://code.earthengine.google.com/7ec3d3a043d090776f902bdad2300b16) |
| 🎯 | **Modul Validasi:** Uji Akurasi LULC (*Confusion Matrix*) | [▶️ Buka Script](https://code.earthengine.google.com/0f45a927cb5cd9fac5e68a53779d0db8) |
| 🧮 | **Modul Statistik:** Kalkulasi Luasan Area Terbakar (Hektar) | [▶️ Buka Script](https://code.earthengine.google.com/6efbe7eba42998aa28cdb4972b4fc8fa) |
| ⚙️ | **Modul AI:** Komparasi Algoritma *Classifier* | [▶️ Buka Script](https://code.earthengine.google.com/9b2f22a07a811919d13186ce46f6c1a3) |

*(Akses memerlukan akun Google Earth Engine)*

---

## ✨ Fitur Utama
| Fitur | Keterangan |
| :--- | :--- |
| 📅 **Time-Series Ekologis** | Menangkap pergeseran kelas tutupan lahan dari vegetasi ke *bare land* secara rinci dalam rentang 2022–2024. |
| 🤖 **ML Classifiers** | Perbandingan kinerja algoritma *Random Forest*, *SVM*, *Naive Bayes*, dan *CART* untuk klasifikasi lanskap vulkanik. |
| 🎯 **Validasi Ketat** | Perhitungan objektif *Overall Accuracy* (OA) dan *Kappa Coefficient* untuk memastikan keandalan deteksi area terbakar. |
| 🧮 **Kalkulasi Deforestasi** | Mengubah piksel menjadi angka pasti (Total Hektar/Km²) untuk menilai kerugian ekologis dan suksesi vegetasi baru. |

---

## 🖥️ Cara Menggunakan
1. Pilih salah satu fase observasi (misalnya Fase 2: 2023) pada tabel modul di atas.
2. Klik tombol **Run** pada antarmuka *Code Editor* GEE.
3. Untuk melihat validitas deteksi lahan terbakar, buka tautan **Modul Validasi** dan periksa tab **Console** untuk hasil *Overall Accuracy*.
4. Gunakan panel **Inspector** untuk mengklik area di peta guna melihat perubahan spektral piksel dari tahun ke tahun.

---

## 🤝 Kontribusi & Rekomendasi Pengembangan Lanjutan
Pengembangan *tools* ini sangat terbuka. Untuk memperkuat analisis kebakaran, beberapa fitur berikut dapat ditambahkan di masa mendatang:

- [ ] **Korelasi Kualitas Udara (Sentinel-5P):** Menarik untuk mengkorelasikan data spasial luasan terbakar ini dengan lonjakan *Aerosol Index* (AAI) dan Emisi Karbon Monoksida (CO) menggunakan citra Sentinel-5P, khususnya untuk menangkap emisi pekat pada periode kritis 1 - 15 September 2023.
- [ ] **Burn Severity Index:** Menambahkan kalkulasi *Normalized Burn Ratio* (NBR) atau dNBR untuk mengklasifikasikan tingkat keparahan luka bakar ekosistem.
- [ ] **Export to GeoTIFF:** Mengizinkan pengunduhan *layer* area terbakar ke *Google Drive* untuk diintegrasikan dengan data administrasi BNPB/BPBD di QGIS/ArcGIS.

Silakan lakukan *Fork*, buat modifikasi, dan ajukan *Pull Request*!

---

## 📄 Lisensi & Sitasi
Proyek ini dirilis di bawah lisensi **MIT License** — bebas digunakan, dimodifikasi, dan didistribusikan dengan atribusi.

Jika Anda menggunakan *script* ini dalam riset kebencanaan atau publikasi ilmiah, mohon sertakan sitasi:
> [Nama Anda]. (2026). *Bromo Fire Impact & LULC Dynamics Monitor: Analisis Spasial Pemulihan Pasca Kebakaran berbasis GEE*. GitHub. https://github.com/[username]/bromo-fire-monitor

<br>
<div align="center">
  Dibuat dengan ❤️ untuk mendukung mitigasi bencana dan pemulihan lingkungan di Indonesia
</div>
