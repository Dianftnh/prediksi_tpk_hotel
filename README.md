# Analisis dan Prediksi Tingkat Penghunian Kamar (TPK) & Tempat Tidur (TPTT) Hotel di Provinsi Lampung

<div align="center">

[![Looker Studio Dashboard](https://img.shields.io/badge/Google%20Looker%20Studio-Dashboard-blue?style=for-the-badge&logo=looker)](https://datastudio.google.com/embed/reporting/43a1513e-6f6d-4136-8cee-4c59b38b046d/page/FcWRF)
[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-black?style=for-the-badge&logo=github)](https://github.com/Dianftnh/prediksi_tpk_hotel)
[![Python](https://img.shields.io/badge/Python-3.8%2B-yellow?style=for-the-badge&logo=python)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)]()

</div>

---

## 📖 Deskripsi Proyek

Proyek ini merupakan sistem analisis data statistik pariwisata dan peramalan runtun waktu (*time series forecasting*) untuk mengeksplorasi serta memprediksi **Tingkat Penghunian Kamar (TPK)** dan **Tingkat Penghunian Tempat Tidur (TPTT)** hotel di Provinsi Lampung periode **2022–2025**. 

Dengan memadukan pengolahan data berbasis **Python (Pandas & NumPy)**, pemodelan matematis **Fuzzy Time Series (FTS) metode Chen**, serta visualisasi interaktif tingkat lanjut menggunakan **Google Looker Studio**, proyek ini dirancang untuk memberikan wawasan mendalam mengenai dinamika okupansi akomodasi pariwisata daerah.

---

## 🔗 Tautan Akses Cepat

- **Dashboard Visualisasi & Prediksi:** [Akses Looker Studio Dashboard](https://datastudio.google.com/embed/reporting/43a1513e-6f6d-4136-8cee-4c59b38b046d/page/FcWRF)
- **Repositori Kode Sumber:** [GitHub - Dianftnh/prediksi_tpk_hotel](https://github.com/Dianftnh/prediksi_tpk_hotel)

---

## 📌 Latar Belakang & Pertanyaan Bisnis

Sektor perhotelan memegang peranan vital dalam mendukung perekonomian dan pariwisata daerah. Tingkat Penghunian Kamar (TPK) dan Tempat Tidur (TPTT) menjadi indikator utama efisiensi pengelolaan akomodasi. Proyek ini dibangun untuk menjawab berbagai pertanyaan analisis krusial, di antaranya:
1. Bagaimana tren bulanan TPK dan TPTT hotel di Provinsi Lampung dari tahun 2022 hingga Mei 2025?
2. Seberapa besar perbedaan kinerja okupansi antara hotel kategori berbintang dan non-bintang?
3. Pada bulan-bulan apa saja tingkat kunjungan mencapai puncak (*peak season*) atau titik terendah (*low season*)?
4. Bagaimana korelasi dan tingkat signifikansi kedatangan tamu Nusantara (WNI) versus tamu Asing (WNA) terhadap kenaikan TPK?
5. Bagaimana proyeksi peramalan tingkat hunian kamar dan tempat tidur untuk periode mendatang menggunakan metode FTS Chen?

---

## 📊 Sumber Data & Variabel

- **Instansi Sumber:** Badan Pusat Statistik (BPS) Provinsi Lampung.
- **Cakupan Periode:** Januari 2022 – Mei 2025 (41 bulan data historis teragregasi).
- **Skala Dataset:** 2.477 baris data mentah terstruktur (`prepared_for_eda_gabungan_df.xlsx`).
- **Variabel Utama:**
  - `Tahun` & `Bulan`: Atribut waktu observasi.
  - `Jenis`: Klasifikasi akomodasi (`Bintang` / `Non Bintang`).
  - `TPK`: Persentase Tingkat Penghunian Kamar (%).
  - `TPTT`: Persentase Tingkat Penghunian Tempat Tidur (%).
  - `wna_in/jml_tamu_asing` & `wni_in/jml_tamu_nusantara`: Jumlah kedatangan tamu asing dan nusantara.

---

## 🛠️ Metodologi & Tahapan Analisis

### 1. Data Wrangling & Preprocessing (`src/` scripts)
- Pembersihan format string numerik, konversi pemisah koma, dan eliminasi nilai error (`#DIV/0!`, missing values).
- Standarisasi kategori jenis hotel serta pembentukan kolom penanggalan terstruktur (`Tanggal`) guna mendukung analisis runtun waktu.
- Agregasi data bulanan untuk memfasilitasi pemodelan prediktif.

### 2. Exploratory Data Analysis (EDA)
- **Analisis Tren & Musiman:** Mengidentifikasi lonjakan okupansi pada musim liburan sekolah, hari raya keagamaan, dan libur akhir tahun.
- **Komparasi Segmentasi Hotel:** Membandingkan karakteristik okupansi hotel berbintang yang cenderung lebih stabil dengan hotel non-bintang.
- **Analisis Korelasi Tamu:** Menghitung koefisien korelasi untuk mengetahui apakah wisatawan nusantara atau mancanegara yang memberikan dampak dominan terhadap kenaikan TPK.

### 3. Pemodelan Peramalan (Fuzzy Time Series Metode Chen)
- **Penentuan Semesta Pembicaraan ($U$):** Ditetapkan berdasarkan nilai minimum ($D_{\min} = 21,91$) dan maksimum ($D_{\max} = 55,8244$) dari data historis TPK.
- **Pembentukan Interval Fuzzy:** Membagi rentang semesta pembicaraan menjadi sub-interval dengan panjang yang sama (*equal length*).
- **Fuzzifikasi & Hubungan Logika (FLR/FLRG):** Mengubah data historis menjadi himpunan fuzzy berdasarkan relasi transisi antar waktu.
- **Defuzzifikasi:** Menghitung nilai *crisp output* sebagai hasil peramalan nilai TPK dan TPTT bulanan berikutnya.

### 4. Evaluasi Performa Model
Performa akurasi model diuji menggunakan metrik **Mean Absolute Error (MAE)** dengan nilai kesalahan rata-rata tercatat sebesar **3,497**, menunjukkan tingkat deviasi yang rendah terhadap data historis aktual.

---

## 🚀 Panduan Cara Menjalankan Proyek

Ikuti langkah-langkah di bawah ini untuk menjalankan kode sumber secara lokal:

### Prasyarat Sistem
Pastikan terpasang:
- **Python 3.8+**
- **Git**

### Langkah 1: Kloning Repositori
```bash
git clone https://github.com/Dianftnh/prediksi_tpk_hotel.git
cd prediksi_tpk_hotel
```

### Langkah 2: Buat & Aktifkan Virtual Environment (Direkomendasikan)
```bash
# Membuat virtual environment
python -m venv venv

# Mengaktifkan (Windows):
venv\Scripts\activate

# Mengaktifkan (macOS / Linux):
source venv/bin/activate
```

### Langkah 3: Instalasi Dependensi Pustaka
Pasang seluruh pustaka yang diperlukan:
```bash
pip install -r requirements.txt
```
*(Paket utama meliputi: `numpy`, `pandas`, `matplotlib`, `seaborn`, `statsmodels`, `openpyxl`)*

### Langkah 4: Menjalankan Script Utama Peramalan
Proyek ini memisahkan proses komputasi peramalan ke dalam dua skrip terpisah:
1. **Menjalankan Pemodelan & Prediksi TPK:**
   ```bash
   python src/prediksiTPK.py
   ```
2. **Menjalankan Pemodelan & Prediksi TPTT:**
   ```bash
   python src/prediksiTPTT.py
   ```
Skrip akan memproses dataset, menjalankan algoritma peramalan, mencetak evaluasi metrik MAE, serta menghasilkan file CSV hasil prediksi (`tpk_forecast_for_looker_studio.csv` & `tptt_forecast_for_looker_studio.csv`) yang terhubung langsung dengan Google Looker Studio.

---

## 📂 Struktur Repositori

```text
prediksi_tpk_hotel/
├── data/
│   ├── 2024.csv                              # Dataset mentah awal
│   ├── prepared_for_eda_gabungan_df.xlsx     # Dataset utama terstruktur & bersih
│   ├── tpk_forecast_for_looker_studio.csv    # Hasil ekspor prediksi TPK (Looker Studio)
│   └── tptt_forecast_for_looker_studio.csv   # Hasil ekspor prediksi TPTT (Looker Studio)
├── src/
│   ├── prediksiTPK.py                        # Skrip utama pembersihan, EDA, & peramalan TPK
│   └── prediksiTPTT.py                       # Skrip utama pembersihan, EDA, & peramalan TPTT
├── README.md                                 # Dokumentasi lengkap proyek
└── requirements.txt                          # Daftar dependensi pustaka Python
```

---

## ⚠️ Batasan & Catatan Analitis

- Cakupan data historis bulanan terbatas pada rentang Januari 2022 hingga Mei 2025; proyeksi jangka panjang memerlukan pembaruan berkala dengan penambahan data terbaru.
- Nilai MAE sebesar **3,497** merupakan hasil pengujian performa pada data historis dan tidak boleh diinterpretasikan sebagai kepastian mutlak untuk kondisi pariwisata di masa depan.

---

## 👤 Author & Kontributor

**Dian Fatonah**  
- Mahasiswa Statistika / Informatika — Universitas Lampung  
- GitHub: [https://github.com/Dianftnh](https://github.com/Dianftnh)
