#  Customer Profiling & Clustering — E-Commerce Indonesia

Analisis segmentasi pelanggan menggunakan RFM Analysis dan K-Means Clustering pada dataset transaksi e-commerce Indonesia.

---

##  Deskripsi

Notebook ini bertujuan memahami siapa pelanggan kita, bagaimana pola pembelian mereka, dan segmen mana yang perlu diprioritaskan secara bisnis.

- **Periode data:** Januari 2022 – Juni 2024
- **Dataset:** 426.000 transaksi | 28.000 pelanggan unik
- **Metode:** RFM Analysis + K-Means Clustering (k=4)

---

##  Struktur Folder

```
├── customer-profiling-clustering.ipynb   # Notebook utama
├── dashboard_final.csv                   # Dataset lengkap dengan label segmen
└── output/
    ├── rfm_customer_segments.csv         # RFM score & cluster per pelanggan
    ├── segment_summary.csv               # Ringkasan per segmen
    ├── 01_missing_values.png
    ├── 02_outlier_boxplots.png
    ├── 03_revenue_trend.png
    ├── 04_category_city.png
    ├── 05_payment_age.png
    ├── 06_rfm_scores.png
    ├── 07_rfm_overview.png
    ├── 08_elbow.png
    ├── 09_cluster_pca.png
    └── 10_cluster_demografi.png
```

---

##  Alur Analisis

1. **Data Cleaning** — konversi tipe, imputasi missing values, trimming outlier
2. **EDA** — tren revenue, performa kategori & kota, demografi pelanggan
3. **RFM Analysis** — scoring & labeling 10 segmen perilaku pelanggan
4. **K-Means Clustering** — pengelompokan berbasis machine learning (k=4 optimal)
5. **Rekomendasi Bisnis** — aksi per segmen berdasarkan temuan data

---

##  Key Insights

| Temuan | Detail |
|---|---|
|  Konsentrasi revenue | Champions (23,5% pelanggan) menyumbang **69,3% total revenue** |
|  Repeat purchase rendah | Median frequency hanya **4x dalam 2,5 tahun** |
|  Cancellation rate tinggi | **11%** — sudah melewati batas aman industri |
|  Peluang kota tier-2 | Balikpapan & kota Kalimantan/Sulawesi punya spending per kapita tinggi |
|  Dominasi e-wallet | GoPay + OVO + DANA = **~43% transaksi** |

---

##  Cluster Hasil K-Means

| Cluster | Karakteristik |
|---|---|
| **VIP — High Spender** | Monetary tertinggi, Gen X & Baby Boomer |
| **Frequent Buyer** | Frekuensi belanja tertinggi |
| **Occasional Buyer** | Belanja sporadis, potensi ditingkatkan |
| **Inactive / Churned** | Sudah lama tidak bertransaksi |

---

##  Tools & Library

`Python` · `Pandas` · `NumPy` · `Scikit-learn` · `Matplotlib` · `Seaborn`
