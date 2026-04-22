# ClustrIQ — Customer Profiling & Clustering Dashboard

> E-Commerce Customer Segmentation using K-Means Algorithm · 28,000 Customers · RFM Analysis

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Sklearn](https://img.shields.io/badge/Scikit--Learn-K--Means-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?style=flat-square&logo=pandas&logoColor=white)
![Dashboard](https://img.shields.io/badge/Dashboard-HTML%20%2B%20Chart.js-0D9488?style=flat-square)
![Clusters](https://img.shields.io/badge/Clusters-4%20Segments-0EA5E9?style=flat-square)

---

## Project Overview

Proyek ini bertujuan untuk membangun **profil pelanggan e-commerce** menggunakan teknik **unsupervised machine learning** (K-Means Clustering) berbasis fitur **RFM (Recency, Frequency, Monetary)**. Hasil segmentasi divisualisasikan dalam dashboard interaktif 4 halaman.

**Tujuan utama:**
- Mengidentifikasi segmen pelanggan berdasarkan perilaku transaksi
- Memberikan rekomendasi bisnis yang actionable per segmen
- Menyajikan insight demografis dan RFM secara visual

---

## Project Structure

```
clustriq/
├── customer-profiling-dan-clustering.ipynb   # Notebook utama (EDA + Modeling)
├── customer_segmentation.csv                  # Dataset hasil clustering (28,000 rows)
└── README.md
```

---

## Dataset

| Field | Tipe | Keterangan |
|---|---|---|
| `customer_id` | String | Identifier unik pelanggan |
| `city` | String | Kota domisili |
| `gender` | String | Female / Male / Unknown |
| `age` | Integer | Usia pelanggan (18–65) |
| `loyalty_tier` | String | Bronze / Silver / Gold / Platinum |
| `total_order` | Integer | Total semua pesanan (termasuk cancel) |
| `cancel_count` | Integer | Jumlah pesanan dibatalkan |
| `frequency` | Integer | `total_order - cancel_count` |
| `monetary` | Float | Total nilai transaksi completed (Rp) |
| `recency` | Integer | Hari sejak transaksi terakhir |
| `avg_order_value` | Float | `monetary ÷ frequency` |
| `cancel_rate` | Float | `cancel_count ÷ total_order` |
| `avg_discount` | Float | Rata-rata diskon per transaksi (%) |
| `avg_shipping_cost` | Float | Rata-rata biaya kirim (Rp) |
| `cluster` | Integer | Label cluster K-Means (0–3) |
| `cluster_label` | String | Nama segmen hasil mapping manual |

---

## Methodology

### 1. Data Preprocessing
- Handling missing values & outliers
- Feature engineering: `recency`, `frequency`, `monetary`, `cancel_rate`, `avg_order_value`
- Normalisasi fitur RFM menggunakan **StandardScaler**

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(df[['recency', 'frequency', 'monetary']])
```

### 2. Optimal K Selection
- **Elbow Method** — mencari titik "siku" pada inertia plot
- **Silhouette Score** — mengukur kualitas pemisahan cluster
- Hasil: **k = 4** dipilih sebagai jumlah cluster optimal

### 3. K-Means Clustering

```python
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=4, random_state=42, n_init=10)
df['cluster'] = kmeans.fit_predict(X_scaled)
```

### 4. Cluster Labeling
Label ditetapkan secara manual berdasarkan karakteristik centroid:

| Cluster | Label | Dasar Penamaan |
|---|---|---|
| 0 | High Value Customer | Recency rendah, frequency & monetary tinggi |
| 1 | At Risk Customer | Recency sangat tinggi, cancel rate tinggi |
| 2 | Low Engagement Customer | Recency tinggi, frequency & monetary rendah |
| 3 | Top Spender | Recency sangat rendah, frequency & monetary tertinggi |

---

## Cluster Results

| Segment | Count | % | Avg Recency | Avg Frequency | Avg Monetary | Cancel Rate |
|---|---|---|---|---|---|---|
|  **Top Spender** | 538 | 1.9% | 9 days | 130 txn | Rp 65.3M | 11% |
|  **High Value** | 3,182 | 11.4% | 24 days | 41 txn | Rp 20.6M | 11% |
|  **Low Engagement** | 15,890 | 56.8% | 145 days | 7 txn | Rp 3.4M | 3% |
|  **At Risk** | 8,390 | 30.0% | 225 days | 4 txn | Rp 1.9M | 27% |

---

##  Business Recommendations

###  Top Spender (538 customers · 1.9%)
- Berikan **VIP loyalty rewards** & early access ke produk baru
- Hindari diskon besar — segmen ini tidak price-sensitive
- Monitor peningkatan recency sebagai sinyal churn awal

###  High Value Customer (3,182 customers · 11.4%)
- Kandidat terkuat untuk **upsell** menuju Top Spender
- Berikan loyalty milestone & progress indicator
- Pantau deteriorasi recency secara proaktif

###  Low Engagement Customer (15,890 customers · 56.8%)
- Segmen terbesar yang **belum dioptimalkan** — fokus pada peningkatan frequency
- Aktivasi dengan free shipping & personalized category reminder
- Cancel rate hanya 3% — aman untuk investasi reactivation campaign

###  At Risk Customer (8,390 customers · 30%)
- Cancel rate 27% — **analisis penyebab pembatalan** per kota & kategori produk
- Jalankan satu win-back campaign dengan batas waktu jelas
- Jika tidak ada respons dalam 3 bulan → deprioritize marketing spend

---

##  Interactive Dashboard

[Dashboard](https://datastudio.google.com/s/nehTKEbkDJA)

### Fitur Dashboard
| Halaman | Konten |
|---|---|
| **Overview** | 4 KPI cards, donut cluster distribution, revenue bar, RFM bubble chart, cancel rate |
| **Cluster Detail** | Profil + metrics + rekomendasi bisnis per segmen |
| **Demographics** | Gender, loyalty tier, age group, top 8 kota (stacked by cluster) |
| **RFM Analysis** | Recency, frequency, monetary, discount, AOV filterable per cluster |

### Filter Interaktif
- Filter by **Cluster/Segment**
- Filter by **Loyalty Tier**


## Key Findings

- **56.8%** pelanggan masuk kategori Low Engagement → peluang terbesar untuk pertumbuhan
- **30%** pelanggan At Risk dengan cancel rate 27% → perlu intervensi segera
- **Top Spender** hanya 1.9% namun memiliki avg monetary **34x lebih tinggi** dari At Risk
- **Avg discount hampir seragam** (~10%) di semua cluster → bukan faktor pembeda perilaku
- **Kota Jakarta** mendominasi di semua cluster dengan 6,025 pelanggan total

---

## Author

**[Novita Anggraini]**
- novitanggraini90@gmail.com
- [GitHub](https://github.com/fixveet)

---

<div align="center">
  <sub>Built with 💚 · Customer Profiling & Clustering · K-Means · RFM Analysis</sub>
</div>
