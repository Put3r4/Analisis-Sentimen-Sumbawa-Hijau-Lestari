# Analisis Sentimen Sumbawa Hijau Lestari

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Status](https://img.shields.io/badge/Status-Selesai-brightgreen)
![Komentar Dianalisis](https://img.shields.io/badge/Komentar%20Dianalisis-401-informational)
![Notebook](https://img.shields.io/badge/Tools-Jupyter%20Notebook-orange)

Analisis sentimen publik terhadap program penghijauan Pemerintah Kabupaten Sumbawa, berdasarkan komentar warga di Facebook.

## Daftar Isi

1. [Ringkasan Proyek](#1-ringkasan-proyek)
2. [Latar Belakang](#2-latar-belakang)
3. [Tujuan](#3-tujuan)
4. [Struktur Proyek](#4-struktur-proyek)
5. [Tahapan Pelaksanaan](#5-tahapan-pelaksanaan)
6. [Akurasi dan Kualitas Data](#6-akurasi-dan-kualitas-data)
7. [Insight yang Diperoleh](#7-insight-yang-diperoleh)
8. [Kesimpulan dan Rekomendasi](#8-kesimpulan-dan-rekomendasi)
9. [Cara Menjalankan Ulang Proyek](#9-cara-menjalankan-ulang-proyek)

## Ringkasan Cepat

| Metrik | Nilai |
|---|---|
| Sumber data | 54 postingan Facebook |
| Data mentah | 436 baris |
| Data bersih dianalisis | 401 baris |
| Sentimen dominan | Netral (56.11%) |
| Kategori isu terbanyak | Obrolan/Balasan Personal (57.61%) |
| Kategori paling kritis | Kritik/Skeptisisme Keberlanjutan (100% negatif) |

## 1. Ringkasan Proyek

Proyek ini merupakan analisis sentimen publik terhadap program Pemerintah Kabupaten Sumbawa bernama "Sumbawa Hijau Lestari" berdasarkan komentar warga di platform media sosial Facebook. Data dikumpulkan dari 54 postingan yang mencakup unggahan foto, tautan berita, dan video reels dari berbagai akun instansi pemerintah, sekolah, serta warga masyarakat. Tujuan akhir dari penelitian ini adalah untuk mengukur persepsi publik, memetakan kategori isu yang berkembang di tengah masyarakat, dan merumuskan rekomendasi kebijakan yang berbasis data bagi Pemerintah Kabupaten Sumbawa dalam meningkatkan efektivitas program penghijauan daerah.

## 2. Latar Belakang

Program "Sumbawa Hijau Lestari" merupakan salah satu inisiatif strategis Pemerintah Kabupaten Sumbawa dalam menangani isu lingkungan hidup, degradasi lahan, dan perubahan iklim. Evaluasi terhadap program pemerintah umumnya dilakukan melalui survei internal atau laporan administratif. Namun, evaluasi berbasis media sosial menawarkan keunggulan berupa data pendapat masyarakat secara spontan dan transparan. Facebook dipilih sebagai sumber data utama karena platform tersebut merupakan media sosial yang paling populer dan aktif digunakan oleh pemerintah daerah, pihak sekolah, serta masyarakat luas di Kabupaten Sumbawa untuk mendistribusikan informasi resmi dan melakukan diskusi publik.

## 3. Tujuan

Penelitian ini dilaksanakan dengan tujuan eksplisit sebagai berikut.

1. Mengetahui distribusi persepsi dan tingkat sentimen publik terhadap pelaksanaan program "Sumbawa Hijau Lestari".
2. Mengidentifikasi dan memetakan kategori isu serta topik pembahasan utama yang muncul pada kolom komentar warga.
3. Merumuskan masukan dan saran rekomendasi perbaikan program yang objektif berbasis temuan data untuk menjadi bahan pertimbangan pemangku kepentingan.

## 4. Struktur Proyek

```
Analisis-Sentimen-Sumbawa-Hijau-Lestari/
├── data/
│   ├── dataset/
│   │   ├── daftar_link_sumber.csv
│   │   └── dataset_analisis_sumbawa_hijau_lestari.csv
│   ├── processed_dataset/
│   │   ├── figures/
│   │   │   ├── 01_distribusi_sentimen.png
│   │   │   ├── 02_distribusi_kategori_isu.png
│   │   │   ├── 03_crosstab_kategori_sentimen.png
│   │   │   ├── 04_jenis_komentar_sentimen.png
│   │   │   ├── 05_top10_nama_sumber_sentimen.png
│   │   │   ├── 06_tren_sentimen_bulanan.png
│   │   │   └── 07_top_words_kategori_kritis.png
│   │   ├── crosstab_jenis_komentar_sentimen.csv
│   │   ├── crosstab_kategori_sentimen.csv
│   │   ├── dataset_siap_label_sumbawa_hijau_lestari.xlsx
│   │   ├── ringkasan_statistik_sentimen.csv
│   │   └── top_words_kritis.csv
│   └── labelled/
│       └── dataset_siap_label_sumbawa_hijau_lestari_labelled.xlsx
├── documents/
├── notebook/
│   ├── 01_cleaning_dataset.ipynb
│   └── 02_analisis_sentimen.ipynb
├── .gitignore
├── README.md
├── requirements.txt
└── SET_UP.md
```

Fungsi setiap folder dan file utama dirangkum pada tabel berikut.

| Folder / File | Fungsi |
|---|---|
| `data/dataset/` | Data mentah hasil ekstraksi menggunakan Apify Facebook Comments Scraper. `dataset_analisis_sumbawa_hijau_lestari.csv` menyimpan seluruh baris komentar mentah beserta metadata postingan. `daftar_link_sumber.csv` memuat pemetaan 54 tautan postingan Facebook beserta nama akun pembuat konten. |
| `data/processed_dataset/` | Data hasil pembersihan yang siap dilabeli (`dataset_siap_label_sumbawa_hijau_lestari.xlsx`), beserta seluruh output analisis: tabel silang sentimen, ringkasan statistik, frekuensi kata kunci, dan sub-folder `figures/` berisi 7 grafik visualisasi format PNG. |
| `data/labelled/` | `dataset_siap_label_sumbawa_hijau_lestari_labelled.xlsx`, dataset final hasil pelabelan manual penuh oleh peneliti. |
| `documents/` | Dokumen pendukung proyek, catatan metodologi, dan referensi prompt analisis. |
| `notebook/01_cleaning_dataset.ipynb` | Tahap pembersihan data mentah. |
| `notebook/02_analisis_sentimen.ipynb` | Tahap validasi label, kalkulasi statistik deskriptif, analisis silang, serta visualisasi grafik. |
| `.gitignore` | Konfigurasi pengecualian file atau folder temporer agar tidak ikut tercatat oleh git. |
| `README.md` | Dokumentasi utama proyek yang menjelaskan metodologi, hasil analisis, serta panduan proyek. |
| `requirements.txt` | Daftar pustaka Python yang dibutuhkan untuk menjalankan kode program. |
| `SET_UP.md` | Petunjuk teknis penyiapan lingkungan kerja virtual dan tata cara eksekusi ulang proyek. |

## 5. Tahapan Pelaksanaan

Seluruh tahapan proyek dilaksanakan secara sistematis dalam empat langkah utama berikut.

### 5.1 Pengumpulan Data

Data komentar dikumpulkan menggunakan alat pemindaian otomatis Apify Facebook Comments Scraper dari 54 tautan postingan Facebook yang berkaitan dengan kegiatan "Sumbawa Hijau Lestari". Dari proses ekstraksi ini diperoleh data mentah sebanyak 436 baris dan 243 kolom data. Metode ini dipilih karena dapat mengumpulkan komentar secara akurat, mencakup hierarki komentar balasan, waktu penulisan, dan identitas pembuat postingan secara efisien.

### 5.2 Pembersihan Data

Proses pembersihan data dilakukan melalui notebook `notebook/01_cleaning_dataset.ipynb`, meliputi penyelarasan format tanggal ke standar ISO (YYYY-MM-DD) dan pemetaan nama akun sumber postingan, di samping pengurangan baris data berikut.

| Alasan Pengurangan | Jumlah Baris |
|---|---|
| Postingan tidak dapat diakses (privat/dihapus) | 5 |
| Komentar tanpa isi teks (stiker/GIF) | 29 |
| Data duplikat | 1 |
| **Total dikurangi** | **35 (8.03%)** |
| **Data bersih akhir** | **401** |

Komentar bersih ini terbagi menjadi dua jenis berikut.

| Jenis Komentar | Jumlah | Persentase |
|---|---|---|
| Utama | 234 | 58.35% |
| Balasan | 167 | 41.65% |

Selain itu, dilakukan penandaan terhadap 10 baris kandidat spam untuk diverifikasi secara manual.

### 5.3 Pelabelan Data

Setiap komentar bersih diberi dua atribut label, yaitu Kategori Isu dan Sentimen. Pelabelan awal dibantu oleh usulan berbasis kata kunci untuk mempercepat penelaahan awal, namun keputusan label akhir ditentukan sepenuhnya melalui peninjauan manual oleh peneliti terhadap setiap isi komentar.

Skema Kategori Isu terdiri atas delapan kelas berikut.

| Kategori Isu | Definisi |
|---|---|
| Obrolan/Balasan Personal | Komentar berisi sapaan, obrolan antar pengguna, atau balasan sosial yang tidak membahas isi materi program secara langsung. |
| Apresiasi/Dukungan Program | Komentar yang menyampaikan pujian, apresiasi, wujud dukungan, serta semangat terhadap pelaksanaan program. |
| Kritik Kebijakan & Isu Terkait | Komentar yang menyampaikan kritik terhadap kebijakan pemerintah, dampaknya terhadap alih fungsi lahan pertanian, atau isu lingkungan secara umum. |
| Pertanyaan/Klarifikasi Program | Komentar berisi pertanyaan teknis atau permintaan penjelasan mengenai mekanisme, lokasi, dan tata cara pelaksanaan program. |
| Saran Teknis Pelaksanaan | Komentar yang memberikan masukan praktis terkait teknis pelaksanaan, seperti jenis bibit tanaman yang sesuai atau teknik perawatan. |
| Kritik/Skeptisisme Keberlanjutan | Komentar yang meragukan komitmen jangka panjang, kelangsungan pemeliharaan pohon, atau efektivitas riil program pasca-seremoni penanaman. |
| Informasi/Netral | Komentar yang menyampaikan fakta, informasi tambahan, atau pernyataan netral tanpa memuat emosi atau pandangan subjektif. |
| Spam/Promosi | Komentar yang berisi promosi penjualan barang atau jasa, tautan komersial tidak relevan, atau pesan berulang. |

Skema Sentimen terdiri atas tiga kelas, yaitu Positif, Netral, dan Negatif.

### 5.4 Analisis dan Penggalian Insight

Tahap akhir dilaksanakan pada notebook `notebook/02_analisis_sentimen.ipynb`. Analisis dilakukan dengan menghitung distribusi statistik sentimen dan kategori isu, analisis silang antara jenis komentar dengan sentimen, perbandingan sentimen antar sumber postingan, tren sentimen bulanan, serta ekstraksi frekuensi kata kunci pada kelompok komentar yang bersifat kritis.

## 6. Akurasi dan Kualitas Data

Tingkat keandalan data dalam analisis ini didukung oleh proses pembersihan yang terukur dan pelabelan manual secara menyeluruh. Dari 436 baris data mentah yang dikumpulkan, terdapat 401 baris data akhir yang dianalisis, atau setara dengan tingkat retensi data sebesar 91.97%.

Terdapat dua keterbatasan utama pada data ini.

1. Penggunaan bahasa daerah Sumbawa (basa Samawa) pada sebagian komentar warga. Hal ini membutuhkan penafsiran konteks budaya lokal secara cermat pada saat proses pelabelan manual agar tidak terjadi kesalahan klasifikasi sentimen.
2. Adanya potensi bias sampel karena data yang terambil hanya berasal dari akun Facebook yang bersifat publik dan dari warga yang aktif menuliskan komentar di media sosial.

## 7. Insight yang Diperoleh

### Distribusi Sentimen Keseluruhan

| Sentimen | Jumlah Komentar | Persentase |
|---|---|---|
| Netral | 225 | 56.11% |
| Positif | 131 | 32.67% |
| Negatif | 45 | 11.22% |
| **Total** | **401** | **100%** |

### Distribusi Kategori Isu

| Kategori Isu | Jumlah | Persentase | Sentimen Dominan |
|---|---|---|---|
| Obrolan/Balasan Personal | 231 | 57.61% | Netral (166) dan Positif (65) |
| Apresiasi/Dukungan Program | 63 | 15.71% | Positif (100%) |
| Kritik Kebijakan & Isu Terkait | 29 | 7.23% | Negatif (28 dari 29) |
| Pertanyaan/Klarifikasi Program | 20 | 4.99% | Netral (100%) |
| Saran Teknis Pelaksanaan | 17 | 4.24% | Netral (15) dan Positif (2) |
| Kritik/Skeptisisme Keberlanjutan | 17 | 4.24% | Negatif (100%) |
| Informasi/Netral | 13 | 3.24% | Netral (100%) |
| Spam/Promosi | 11 | 2.74% | Netral (100%) |
| **Total** | **401** | **100%** | |

### Tiga Pola Utama

> **Dukungan kuat dari jaringan internal instansi dan sekolah.** Kategori Apresiasi/Dukungan Program mencatat sentimen positif sebesar 100%. Jenis komentar utama juga memiliki proporsi sentimen positif yang jauh lebih tinggi (51.28%) dibandingkan jenis komentar balasan (6.59%).

> **Skeptisisme terhadap keberlanjutan program pasca-seremoni.** Sebanyak 17 komentar pada kategori Kritik/Skeptisisme Keberlanjutan seluruhnya bersentimen negatif. Masyarakat menyuarakan kekhawatiran bahwa tanaman yang telah ditanam tidak diperhatikan pemeliharaannya sehingga berpotensi mati.

> **Kritik konstruktif terkait jenis pohon dan alih fungsi lahan.** Pada 28 komentar negatif kategori Kritik Kebijakan, kata kunci paling sering muncul adalah "pohon" (13 kali), "hutan" (10 kali), "tanam" (8 kali), "bage" (7 kali), "jagung" (5 kali), dan "beringin" (4 kali). Warga menyoroti perlunya pemilihan jenis pohon berkayu keras dan tahan lama seperti asam jawa ("bage") atau beringin, serta kritik atas ketidakseimbangan antara kegiatan penghijauan di satu sisi dengan maraknya pembukaan hutan untuk tanaman jagung di sisi lain.

## 8. Kesimpulan dan Rekomendasi

Kesimpulan dari analisis ini menunjukkan bahwa respon publik di media sosial terhadap program "Sumbawa Hijau Lestari" secara umum bersifat netral hingga positif. Sentimen positif didorong oleh partisipasi aktif sekolah dan instansi pemerintah. Namun demikian, substansi kritik dari warga masyarakat berfokus pada dua isu krusial, yaitu kepastian pemeliharaan bibit tanaman jangka panjang dan penataan kebijakan lahan lereng bukit.

Berdasarkan temuan tersebut, dirumuskan rekomendasi perbaikan bagi pemangku kepentingan Pemerintah Kabupaten Sumbawa sebagai berikut.

| No | Rekomendasi | Rasional |
|---|---|---|
| 1 | Membentuk mekanisme evaluasi dan pemeliharaan berkala pasca-penanaman | Memastikan ketersediaan anggaran dan petugas pemeliharaan agar bibit yang ditanam dapat tumbuh berkelanjutan, bukan sekadar kegiatan seremoni |
| 2 | Memilih jenis bibit pohon yang tepat dan memberikan edukasi publik | Memprioritaskan bibit tanaman lokal berakar kuat dan bermanfaat ekonomis atau ekologis panjang, seperti asam jawa ("bage") dan beringin, disertai penyampaian tata cara perawatan kepada masyarakat |
| 3 | Menyelaraskan kebijakan penghijauan dengan penataan alih fungsi lahan pertanian | Memperketat regulasi pembukaan hutan untuk ladang jagung di area lereng dan kawasan tangkapan air, agar kegiatan penghijauan tidak kontradiktif dengan alih fungsi hutan yang masih berlangsung |

## 9. Cara Menjalankan Ulang Proyek

1. Pastikan sistem telah terinstal Python 3.9 atau versi yang lebih baru.
2. Instal dependensi pustaka yang dibutuhkan menggunakan perintah `pip install -r requirements.txt`.
3. Untuk petunjuk teknis penyiapan lingkungan kerja virtual dan urutan eksekusi notebook, rujuk dokumen [SET_UP.md](./SET_UP.md).
