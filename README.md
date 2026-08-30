# Analisis Sentimen Sumbawa Hijau Lestari

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Status](https://img.shields.io/badge/Status-Selesai-brightgreen)
![Komentar Dianalisis](https://img.shields.io/badge/Komentar%20Dianalisis-417-informational)
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
| Sumber data | 56 postingan Facebook |
| Data mentah | 453 baris (Rata-rata 8.09 komentar/post) |
| Data bersih dianalisis | 417 baris (Rata-rata 7.45 komentar/post) |
| Sentimen dominan | Netral (54.68%) |
| Dominasi Aspek Person | Obrolan/Balasan Personal (56.35%) |
| Respon Eksplisit Aspek Program | 71 Apresiasi vs 48 Kritik (Positif : Negatif) |
| Tingkat Interaksi (Likes) | Rata-rata 0.40 like/komentar, 2.96 likes/post |

## 1. Ringkasan Proyek

Proyek ini merupakan analisis sentimen publik terhadap program Pemerintah Kabupaten Sumbawa bernama "Sumbawa Hijau Lestari" berdasarkan komentar warga di platform media sosial Facebook. Data dikumpulkan dari 56 postingan yang mencakup unggahan foto, tautan berita, dan video reels dari berbagai akun instansi pemerintah, sekolah, serta warga masyarakat (termasuk 2 postingan tambahan dari akun Iwan Sofian dan Andi Rusni). Tujuan akhir dari penelitian ini adalah untuk mengukur persepsi publik, memetakan kategori isu yang berkembang di tengah masyarakat, dan merumuskan rekomendasi kebijakan yang berbasis data bagi Pemerintah Kabupaten Sumbawa dalam meningkatkan efektivitas program penghijauan daerah.

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
│   │   │   ├── 07_top_words_kategori_kritis.png
│   │   │   ├── 08_keterlibatan_per_postingan.png
│   │   │   └── 09_wordcloud_kategori_kritis.png
│   │   ├── crosstab_jenis_komentar_sentimen.csv
│   │   ├── crosstab_kategori_sentimen.csv
│   │   ├── dataset_siap_label_sumbawa_hijau_lestari.xlsx
│   │   ├── ringkasan_keterlibatan_postingan.csv
│   │   ├── ringkasan_statistik_sentimen.csv
│   │   └── top_words_kritis.csv
│   └── labelled/
│       ├── dataset_siap_label_sumbawa_hijau_lestari_labelled_v3.xlsx
│       ├── dataset_siap_label_sumbawa_hijau_lestari_labelled_with_like.xlsx
│       ├── dataset_siap_label_sumbawa_hijau_lestari_labelled.xlsx
│       └── dataset_siap_label_sumbawa_hijau_lestari_TAMBAHAN.xlsx
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
| `data/dataset/` | Data mentah hasil ekstraksi menggunakan Apify Facebook Comments Scraper. `dataset_analisis_sumbawa_hijau_lestari.csv` menyimpan seluruh baris komentar mentah beserta metadata postingan. `daftar_link_sumber.csv` memuat pemetaan 56 tautan postingan Facebook beserta nama akun pembuat konten. |
| `data/processed_dataset/` | Data hasil pembersihan yang siap dilabeli (`dataset_siap_label_sumbawa_hijau_lestari.xlsx`), beserta seluruh output analisis: tabel silang sentimen, ringkasan statistik, ringkasan keterlibatan postingan (`ringkasan_keterlibatan_postingan.csv`), frekuensi kata kunci, dan sub-folder `figures/` berisi 9 grafik visualisasi format PNG. |
| `data/labelled/` | Dataset final hasil pelabelan manual penuh oleh peneliti (`dataset_siap_label_sumbawa_hijau_lestari_labelled_v3.xlsx` sebanyak 417 baris aktif, serta riwayat versi sebelumnya `_labelled_with_like.xlsx`, `_labelled.xlsx`, dan `_TAMBAHAN.xlsx`). |
| `documents/` | Dokumen pendukung proyek, catatan metodologi, dan referensi prompt analisis. |
| `notebook/01_cleaning_dataset.ipynb` | Tahap pembersihan data mentah. |
| `notebook/02_analisis_sentimen.ipynb` | Tahap validasi label, kalkulasi statistik deskriptif, analisis ABSA, analisis keterlibatan postingan, serta visualisasi grafik dan wordcloud terkini. |
| `.gitignore` | Konfigurasi pengecualian file atau folder temporer agar tidak ikut tercatat oleh git. |
| `README.md` | Dokumentasi utama proyek yang menjelaskan metodologi, kerangka ABSA, hasil analisis, serta panduan proyek. |
| `requirements.txt` | Daftar pustaka Python yang dibutuhkan untuk menjalankan kode program. |
| `SET_UP.md` | Petunjuk teknis penyiapan lingkungan kerja virtual dan tata cara eksekusi ulang proyek. |

## 5. Tahapan Pelaksanaan

Seluruh tahapan proyek dilaksanakan secara sistematis dalam empat langkah utama berikut.

### 5.1 Pengumpulan Data

Data komentar dikumpulkan menggunakan alat pemindaian otomatis Apify Facebook Comments Scraper dari 56 tautan postingan Facebook (mencakup 54 tautan batch awal dan 2 tautan batch tambahan dari akun Iwan Sofian dan Andi Rusni) yang berkaitan dengan kegiatan "Sumbawa Hijau Lestari". Dari proses ekstraksi ini diperoleh data mentah sebanyak 453 baris (436 data awal + 17 data tambahan). Metode ini dipilih karena dapat mengumpulkan komentar secara akurat, mencakup hierarki komentar balasan, waktu penulisan, dan identitas pembuat postingan secara efisien.

### 5.2 Pembersihan Data

Proses pembersihan data dilakukan melalui notebook `notebook/01_cleaning_dataset.ipynb`, meliputi penyelarasan format tanggal ke standar ISO (YYYY-MM-DD) dan pemetaan nama akun sumber postingan, di samping pengurangan baris data berikut.

| Alasan Pengurangan | Jumlah Baris |
|---|---|
| Postingan tidak dapat diakses (privat/dihapus) | 5 |
| Komentar tanpa isi teks (stiker/GIF/attachment) | 30 |
| Data duplikat | 1 |
| **Total dikurangi** | **36 (7.95%)** |
| **Data bersih akhir** | **417** |

Dataset diperluas dengan tambahan 2 postingan (16 komentar bersih dari 17 baris mentah) setelah analisis awal untuk memperluas variasi sumber dan representasi opini publik. Komentar bersih gabungan ini terbagi menjadi dua jenis berikut.

| Jenis Komentar | Jumlah | Persentase |
|---|---|---|
| Utama | 244 | 58.51% |
| Balasan | 173 | 41.49% |
| **Total** | **417** | **100.00%** |

Selain itu, penandaan spam pada dataset final disatukan langsung ke dalam kategori isu "Spam/Promosi" tanpa kolom terpisah.

### 5.3 Pelabelan Data & Kerangka Aspect-Based Sentiment Analysis (ABSA)

Setiap komentar bersih diberi dua atribut label, yaitu Kategori Isu dan Sentimen. Seluruh label ditentukan secara manual penuh oleh peneliti terhadap setiap isi komentar menggunakan skema yang konsisten.

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

#### Kerangka Aspect-Based Sentiment Analysis (ABSA)

Sentimen dalam dataset ini dinilai berdasarkan pendekatan **Aspect-Based Sentiment Analysis (ABSA)**, yaitu memisahkan objek penilaian menjadi dua aspek:
1. **Person**: Figur/akun pengunggah postingan (misalnya pejabat, instansi, atau warga).
2. **Program**: Substansi kebijakan "Sumbawa Hijau Lestari" itu sendiri.

Label Sentimen pada dataset ini secara konsisten mengacu pada **aspek Program**, bukan aspek Person. Konsekuensinya, komentar yang menunjukkan dukungan hangat kepada pengunggah postingan (misalnya ucapan semangat kepada pejabat atau warga yang menanam pohon) tetap diberi label **Netral** apabila komentar tersebut tidak menyatakan sikap eksplisit terhadap substansi program.

Pemetaan kategori isu terhadap aspek yang dinilai disajikan pada tabel berikut.

| Kategori Isu | Aspek yang Dinilai |
|---|---|
| Obrolan/Balasan Personal | Person (pengunggah) |
| Apresiasi/Dukungan Program | Program |
| Kritik Kebijakan & Isu Terkait | Program |
| Pertanyaan/Klarifikasi Program | Program |
| Saran Teknis Pelaksanaan | Program |
| Kritik/Skeptisisme Keberlanjutan | Program |
| Informasi/Netral | Program |
| Spam/Promosi | Tidak relevan (dikeluarkan dari interpretasi aspek) |

> **Tegasan Kunci:** proporsi sentimen Netral yang tinggi pada dataset ini sebagian besar berasal dari volume komentar yang menyasar aspek Person, bukan indikasi sikap netral masyarakat terhadap Program.

### 5.4 Analisis dan Penggalian Insight

Tahap akhir dilaksanakan pada notebook `notebook/02_analisis_sentimen.ipynb`. Analisis dilakukan dengan menghitung distribusi statistik sentimen dan kategori isu, analisis kerangka ABSA, analisis keterlibatan postingan (komentar mentah vs bersih, sebaran per postingan, dan rata-rata like), tren sentimen bulanan (mencakup rentang Desember 2025 s/d Agustus 2026), serta visualisasi frekuensi kata kunci dan wordcloud pada kelompok komentar yang bersifat kritis.

## 6. Akurasi dan Kualitas Data

Tingkat keandalan data dalam analisis ini didukung oleh proses pembersihan yang terukur dan pelabelan manual secara menyeluruh. Dari 453 baris data mentah yang dikumpulkan (436 baris data awal + 17 baris data tambahan), terdapat 417 baris data akhir yang dianalisis, atau setara dengan tingkat retensi data sebesar 92.05%.

Terdapat dua keterbatasan utama pada data ini.

1. Penggunaan bahasa daerah Sumbawa (basa Samawa) pada sebagian komentar warga. Hal ini membutuhkan penafsiran konteks budaya lokal secara cermat pada saat proses pelabelan manual agar tidak terjadi kesalahan klasifikasi sentimen.
2. Adanya potensi bias sampel karena data yang terambil hanya berasal dari akun Facebook yang bersifat publik dan dari warga yang aktif menuliskan komentar di media sosial.

## 7. Insight yang Diperoleh

### Distribusi Sentimen Keseluruhan

| Sentimen | Jumlah Komentar | Persentase |
|---|---|---|
| Netral | 228 | 54.68% |
| Positif | 142 | 34.05% |
| Negatif | 47 | 11.27% |
| **Total** | **417** | **100.00%** |

### Distribusi Kategori Isu & Pemetaan Aspek

| Kategori Isu | Jumlah | Persentase | Aspek | Sentimen Dominan |
|---|---|---|---|---|
| Obrolan/Balasan Personal | 235 | 56.35% | Person | Netral (167) dan Positif (68) |
| Apresiasi/Dukungan Program | 71 | 17.03% | Program | Positif (100%) |
| Kritik Kebijakan & Isu Terkait | 31 | 7.43% | Program | Negatif (30 dari 31) dan Positif (1) |
| Pertanyaan/Klarifikasi Program | 20 | 4.80% | Program | Netral (100%) |
| Saran Teknis Pelaksanaan | 17 | 4.08% | Program | Netral (15) dan Positif (2) |
| Kritik/Skeptisisme Keberlanjutan | 17 | 4.08% | Program | Negatif (100%) |
| Informasi/Netral | 13 | 3.12% | Program | Netral (100%) |
| Spam/Promosi | 13 | 3.12% | Tidak Relevan | Netral (100%) |
| **Total** | **417** | **100.00%** | | |

### Ringkasan Keterlibatan (Engagement) Postingan

- **Total Komentar Mentah**: 453 komentar (Rata-rata: 8.09 komentar per postingan dari 56 postingan).
- **Total Komentar Bersih**: 417 komentar (Rata-rata: 7.45 komentar per postingan).
- **Postingan Komentar Terbanyak**: 22 komentar bersih (Iwan Sofian - Post #4).
- **Postingan Komentar Tersedikit**: 0 komentar (5 postingan yang tidak aktif/tidak dapat diakses).
- **Rata-rata Like per Komentar**: 0.40 likes/komentar.
- **Rata-rata Like per Postingan**: 2.96 likes/postingan.

*Visualisasi sebaran komentar per postingan tersimpan pada `data/processed_dataset/figures/08_keterlibatan_per_postingan.png`.*

### Kata Kunci & Wordcloud Komentar Kritis

Analisis kata kunci pada komentar kritis (`Kritik Kebijakan & Isu Terkait` dan `Kritik/Skeptisisme Keberlanjutan`) ditampilkan secara visual melalui grafik frekuensi kata (`07_top_words_kategori_kritis.png`) dan wordcloud (`09_wordcloud_kategori_kritis.png`) yang saling melengkapi.

### Tiga Pola Utama

> **Dukungan kuat dari jaringan internal instansi dan sekolah.** Kategori Apresiasi/Dukungan Program mencatat 71 komentar dengan sentimen positif 100%. Jenis komentar utama juga memiliki proporsi sentimen positif yang jauh lebih tinggi (52.05%, 127 dari 244) dibandingkan jenis komentar balasan (8.67%, 15 dari 173).

> **Skeptisisme terhadap keberlanjutan program pasca-seremoni.** Sebanyak 17 komentar pada kategori Kritik/Skeptisisme Keberlanjutan seluruhnya bersentimen negatif. Masyarakat menyuarakan kekhawatiran bahwa tanaman yang telah ditanam tidak diperhatikan pemeliharaannya sehingga berpotensi mati dan program berakhir hanya sebatas seremoni.

> **Kritik konstruktif terkait jenis pohon dan alih fungsi lahan.** Pada komentar kritis, kata kunci yang paling sering muncul mencakup "pohon", "hutan", "tanam", "program", "bage", "pemerintah", "jagung", dan "beringin". Warga menyoroti perlunya pemilihan jenis pohon berkayu keras dan tahan lama seperti asam jawa ("bage") atau beringin, serta kritik atas ketidakseimbangan antara kegiatan penghijauan di satu sisi dengan maraknya pembukaan hutan untuk tanaman jagung di sisi lain.

## 8. Kesimpulan dan Rekomendasi

### 8.1 Kesimpulan Berbasis Data

1. **Pemisahan Aspek & Asal Sentimen Netral**:
   Setelah dipisahkan berdasarkan kerangka Aspect-Based Sentiment Analysis (ABSA), proporsi sentimen Netral yang tinggi pada dataset ini (54.68%, 228 komentar) sebagian besar berasal dari komentar yang menyasar aspek **Person** (pengunggah/figur), bukan aspek **Program**. Kategori `Obrolan/Balasan Personal` mencakup **235 dari 417 komentar (56.35%)** sebagai dasar kuantitatif utama temuan ini.

2. **Perbandingan Respon Eksplisit Aspek Program**:
   Di antara komentar yang benar-benar menyasar aspek Program secara eksplisit, kelompok `Apresiasi/Dukungan Program` (**71 komentar**, seluruhnya bersentimen Positif) lebih banyak dibandingkan gabungan dua kategori kritik terhadap Program, yaitu `Kritik Kebijakan & Isu Terkait` (31 komentar: 30 Negatif, 1 Positif) dan `Kritik/Skeptisisme Keberlanjutan` (17 komentar, seluruhnya Negatif) yang berjumlah **48 komentar** (47 bersentimen Negatif, 1 Positif). Perbandingan eksplisit ini mencatatkan angka **71 berbanding 48**.

3. **Tingkat Keterlibatan (Engagement) Publik**:
   Tingkat keterlibatan warga terhadap program di media sosial tergolong rendah, berdasarkan tiga indikator empiris:
   - Rata-rata komentar bersih per postingan hanya sekitar **7 hingga 8 komentar** (7.45 komentar/postingan dari total 56 postingan).
   - Jumlah komentar tertinggi pada satu postingan hanya mencapai **22 komentar**.
   - Mayoritas komentar yang masuk (56.35%) justru menyasar aspek Person (sapaan/obrolan personal), bukan aspek Program.

### 8.2 Catatan Interpretatif Peneliti

1. **Atensi Publik terhadap Program**:
   Rendahnya volume komentar yang secara eksplisit membahas Program, dikombinasikan dengan dominasi komentar bernuansa dukungan personal ke pengunggah, mengindikasikan bahwa program "Sumbawa Hijau Lestari" belum berhasil menarik perhatian publik secara luas di media sosial, terlepas dari sentimen yang ada.

2. **Dua Sudut Pandang Dominasi Apresiasi**:
   Di antara komentar yang secara eksplisit menyasar Program, kecenderungan apresiasi yang lebih tinggi dibanding kritik (71 berbanding 48) dapat dibaca dari dua arah yang berbeda:
   - *Perspektif Pertama*: Sebagai sikap netral masyarakat karena minimnya komentar spesifik yang membahas program secara mendalam.
   - *Perspektif Kedua*: Sebagai kecenderungan psikologis umum terhadap program pemerintah, yaitu warga cenderung tidak banyak memberikan tanggapan eksplisit terhadap program yang tidak mereka anggap bermasalah, sehingga rendahnya penolakan eksplisit tidak serta-merta berarti persetujuan aktif.

3. **Status Hipotesis & Arah Penelitian Lanjutan**:
   Peneliti menegaskan bahwa asumsi "minimnya tanggapan negatif berarti persetujuan diam-diam terhadap program" adalah **hipotesis interpretatif**, bukan kesimpulan yang telah teruji secara statistik. Untuk memvalidasi hipotesis ini diperlukan pengujian statistik lanjutan (misalnya uji-t atau uji-z untuk membandingkan proporsi sentimen antar kelompok, atau metode inferensia lain yang relevan), yang berada di luar cakupan analisis deskriptif pada notebook ini dan menjadi arah bagi penelitian lanjutan.

### 8.3 Rekomendasi Kebijakan

| No | Rekomendasi | Rasional Kebijakan |
| --- | --- | --- |
| 1 | **Mekanisme Evaluasi & Pemeliharaan Berkala Pasca-Penanaman** | Memastikan ketersediaan anggaran dan petugas pemeliharaan agar bibit yang ditanam dapat tumbuh berkelanjutan, bukan sekadar kegiatan seremoni penanaman awal |
| 2 | **Pemilihan Bibit Pohon Lokal & Edukasi Publik** | Memprioritaskan bibit tanaman lokal berakar kuat dan bermanfaat ekologis/ekonomis panjang, seperti asam jawa (*bage*) dan beringin, disertai penyampaian tata cara perawatan kepada masyarakat |
| 3 | **Penyelarasan Kebijakan Penghijauan dengan Penataan Lahan** | Memperketat regulasi pembukaan hutan untuk ladang jagung di area lereng dan kawasan tangkapan air, agar kegiatan penghijauan tidak kontradiktif dengan alih fungsi hutan yang masih berlangsung |

## 9. Cara Menjalankan Ulang Proyek

1. Pastikan sistem telah terinstal Python 3.9 atau versi yang lebih baru.
2. Instal dependensi pustaka yang dibutuhkan menggunakan perintah `pip install -r requirements.txt`.
3. Untuk petunjuk teknis penyiapan lingkungan kerja virtual dan urutan eksekusi notebook, rujuk dokumen [SET_UP.md](./SET_UP.md).
