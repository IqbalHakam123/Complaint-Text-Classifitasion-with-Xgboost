# 🚦 Aduan Masyarakat Transportasi Surabaya

**Klasifikasi Otomatis Aduan Transportasi & Lalu Lintas berbasis AI**

Aplikasi web berbasis Machine Learning yang mendeteksi dan mengklasifikasikan apakah sebuah teks (tweet/laporan masyarakat) merupakan **aduan transportasi & lalu lintas** atau bukan, menggunakan **XGBoost** dan teknik NLP Bahasa Indonesia.

> Dibangun sebagai bagian dari Tugas Akhir Program Studi Sistem Informasi, Telkom University.

---

## ✨ Latar Belakang

Volume aduan masyarakat di media sosial terus meningkat, sementara proses pemilahan secara manual tidak lagi mampu mengimbangi ribuan laporan yang masuk setiap harinya. Project ini hadir untuk mengotomatisasi proses tersebut, membantu instansi terkait mengidentifikasi pola masalah publik secara *real-time* dan mendorong pengambilan keputusan berbasis data.

Dataset yang digunakan berasal dari **23.000+ tweet** akun `@e100ss` (Februari–Desember 2023), mencakup berbagai isu seperti kemacetan, infrastruktur jalan, hingga perilaku pengguna jalan.

## 🧠 Metodologi

Penelitian ini mengikuti kerangka kerja **CRISP-DM**:

`Business Understanding → Data Understanding → Data Preparation → Modeling → Evaluation → Deployment`

Tahapan *preprocessing* teks meliputi:
- **Case Folding** — normalisasi huruf ke lowercase
- **Cleaning** — penghapusan simbol, angka, URL, dan mention
- **Stopword Removal** — Bahasa Indonesia & Inggris
- **Tokenizing & Stemming** — menggunakan Sastrawi
- **Normalisasi Slang & OOV** — mapping kata informal ke bentuk baku

Fitur teks diekstraksi dengan beberapa kombinasi teknik representasi (**CountVectorizer**, **TF-IDF**, **Word2Vec**) lalu diklasifikasikan menggunakan **XGBoost**.

### 📊 Hasil Evaluasi Model

| Kombinasi Fitur | Accuracy | Precision (Aduan) | Recall (Aduan) | F1-Score (Aduan) |
|---|---|---|---|---|
| **CountVectorizer + XGBoost** ⭐ | **93%** | 0.90 | 0.86 | 0.88 |
| TF-IDF + XGBoost | 93% | 0.92 | 0.83 | 0.87 |
| TF-IDF + CountVectorizer + XGBoost | 92% | 0.88 | 0.86 | 0.87 |
| TF-IDF + Word2Vec + XGBoost | 92% | 0.88 | 0.83 | 0.86 |
| CountVectorizer + Word2Vec + XGBoost | 92% | 0.88 | 0.83 | 0.85 |

Kombinasi **CountVectorizer + XGBoost** memberikan performa terbaik dan digunakan sebagai model produksi pada aplikasi ini.

## 🔎 Fitur Aplikasi

| Halaman | Deskripsi |
|---|---|
| 🏠 **Beranda** | Landing page pengenalan sistem |
| 🕵️ **Deteksi Aduan** | Prediksi satu teks aduan secara langsung (real-time) |
| 📥 **Input Data (Batch)** | Unggah file CSV untuk klasifikasi massal, lengkap dengan dashboard: distribusi label, wordcloud, deteksi duplikat, dan unduh hasil |
| 👨🏻‍💻 **Tentang Penelitian** | Penjelasan metodologi, statistik dataset, dan perbandingan evaluasi antar model |

## 🛠️ Tech Stack

- **Python 3.10**
- **Streamlit** — antarmuka web
- **XGBoost** & **scikit-learn** — model klasifikasi
- **Sastrawi** & **NLTK** — NLP Bahasa Indonesia (stemming, stopwords)
- **Pandas / NumPy / SciPy** — pengolahan data
- **Matplotlib / Plotly / WordCloud** — visualisasi
- **OpenCV / Pillow** — pemrosesan gambar


## 🚀 Cara Menjalankan

1. **Clone repository**
```bash
   git clone https://github.com/<username>/COMPLAINT-TEXT-CLASSIFICATION-MODELS-WITH-XGBOOST.git
   cd COMPLAINT-TEXT-CLASSIFICATION-MODELS-WITH-XGBOOST
```

2. **Buat virtual environment (opsional tapi disarankan)**
```bash
   python -m venv venv
   source venv/bin/activate      # Windows: venv\Scripts\activate
```

3. **Install dependensi**
```bash
   pip install -r requirements.txt
```

4. **Jalankan aplikasi**
```bash
   streamlit run main.py
```

5. Buka browser ke `http://localhost:8501` 🎉

> 💡 Bisa juga dijalankan langsung lewat **GitHub Codespaces** — konfigurasi `.devcontainer` sudah tersedia dan akan otomatis meng-install dependensi serta menjalankan aplikasi.

## 📄 Format Data Input (Batch)

Untuk fitur klasifikasi massal, file CSV yang diunggah harus memiliki kolom:

| Kolom | Keterangan |
|---|---|
| `text` | Teks/kalimat yang akan diklasifikasikan |

## 👨‍💻 Penulis

**Iqbal Hakam**
Sistem Informasi, Telkom University
