# Customer Profiling & Clustering — E-Commerce Indonesia

Analisis segmentasi pelanggan menggunakan RFM Analysis dan K-Means Clustering pada data transaksi e-commerce Indonesia periode Januari 2022 – Juni 2024.

---

## Latar Belakang

Dataset terdiri dari 426.000 transaksi dan 28.000 pelanggan unik. Tujuan analisis ini adalah memahami pola perilaku pelanggan, mengidentifikasi segmen yang paling bernilai, dan menghasilkan rekomendasi bisnis yang dapat ditindaklanjuti.

---

## Struktur Project

```
customer-profiling-clustering-ecommerce/
│
├── notebook/
│   └── Customer_Profiling_Clustering.ipynb
│
├── output/
│   ├── rfm_customer_segments.csv
│   ├── segment_summary.csv
│   └── ecommerce_cleaned_sample.csv
│
├── images/
│   └── (screenshot visualisasi)
│
└── README.md
```

---

## Tahapan Analisis

**1. Data Understanding & Cleaning**
Pemeriksaan missing values, konversi tipe data, pengisian nilai kosong dengan median/modus, dan penghapusan outlier menggunakan metode trimming 1%–99% pada kolom `net_revenue`.

**2. Exploratory Data Analysis**
Analisis tren revenue bulanan, performa per kategori produk dan kota, distribusi demografi pelanggan, serta preferensi metode pembayaran.

**3. RFM Analysis**
Setiap pelanggan dihitung nilai Recency, Frequency, dan Monetary-nya, kemudian diberi skor 1–5 per dimensi. Hasilnya digunakan untuk membagi pelanggan ke dalam 10 segmen perilaku.

**4. K-Means Clustering**
Pengelompokan otomatis pelanggan menggunakan algoritma K-Means dengan jumlah cluster optimal k=4, ditentukan melalui elbow method dan silhouette score. Hasil clustering divalidasi dengan PCA untuk visualisasi dan deep-dive demografi per cluster.

**5. Rekomendasi Bisnis**
Strategi spesifik per segmen — dari program retensi untuk Champions hingga win-back campaign untuk At Risk — beserta rekomendasi operasional terkait ekspansi kota dan kerjasama e-wallet.

---

## Temuan Utama

- Champions hanya 23,5% dari total pelanggan, namun menyumbang 69,3% dari total revenue
- Electronics mendominasi revenue (Rp 78 miliar), jauh di atas Fashion (Rp 22,3 miliar)
- Median Recency 97 hari — setengah pelanggan sudah lebih dari 3 bulan tidak bertransaksi
- E-wallet (GoPay, OVO, DANA) mencakup 43% dari seluruh transaksi
- Kelompok Millennial (25–34 tahun) adalah penyumbang revenue terbesar

---

## Dashboard

Visualisasi interaktif tersedia di Looker Studio:

[Lihat Dashboard](https://lookerstudio.google.com/LINK-DUMMY)

Dashboard mencakup ringkasan eksekutif, peta segmentasi RFM, profil demografi pelanggan, dan detail per segmen dengan filter interaktif.

---

## Tech Stack

- Python 3
- Pandas, NumPy
- Scikit-learn (KMeans, PCA, StandardScaler)
- Matplotlib, Seaborn
- Looker Studio

---

## Cara Menjalankan Notebook

1. Clone repository ini
```bash
git clone https://github.com/username/customer-profiling-clustering-ecommerce.git
```

2. Install dependensi
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

3. Letakkan file `ecommerce_raw_data.csv` di direktori yang sama dengan notebook

4. Jalankan notebook secara berurutan dari sel pertama

---

## Author

Novita Anggraini
