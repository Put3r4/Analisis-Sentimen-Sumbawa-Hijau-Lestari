# Analisis Sentimen Sumbawa Hijau Lestari

## 1. Ringkasan Proyek

Proyek ini merupakan analisis sentimen publik terhadap program Pemerintah Kabupaten Sumbawa bernama "Sumbawa Hijau Lestari" berdasarkan komentar warga di platform media sosial Facebook. Data dikumpulkan dari 54 postingan yang mencakup unggahan foto, tautan berita, dan video reels dari berbagai akun instansi pemerintah, sekolah, serta warga masyarakat. Tujuan akhir dari penelitian ini adalah untuk mengukur persepsi publik, memetakan kategori isu yang berkembang di tengah masyarakat, dan merumuskan rekomendasi kebijakan yang berbasis data bagi Pemerintah Kabupaten Sumbawa dalam meningkatkan efektivitas program penghijauan daerah.

## 2. Latar Belakang

Program "Sumbawa Hijau Lestari" merupakan salah satu inisiatif strategis Pemerintah Kabupaten Sumbawa dalam menangani isu lingkungan hidup, degradasi lahan, dan perubahan iklim. Evaluasi terhadap program pemerintah umumnya dilakukan melalui survei internal atau laporan administratif. Namun, evaluasi berbasis media sosial menawarkan keunggulan berupa data pendapat masyarakat secara spontan dan transparan. Facebook dipilih sebagai sumber data utama karena platform tersebut merupakan media sosial yang paling populer dan aktif digunakan oleh pemerintah daerah, pihak sekolah, serta masyarakat luas di Kabupaten Sumbawa untuk mendistribusikan informasi resmi dan melakukan diskusi publik.

## 3. Tujuan

Penelitian ini dilaksanakan dengan tujuan eksplisit sebagai berikut:

1. Mengetahui distribusi persepsi dan tingkat sentimen publik terhadap pelaksanaan program "Sumbawa Hijau Lestari".
2. Mengidentifikasi dan memetakan kategori isu serta topik pembahasan utama yang muncul pada kolom komentar warga.
3. Merumuskan masukan dan saran rekomendasi perbaikan program yang objektif berbasis temuan data untuk menjadi bahan pertimbangan pemangku kepentingan.

## 4. Struktur Proyek

Struktur folder dan file pada direktori proyek adalah sebagai berikut:

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

Penjelasan fungsi dari setiap folder dan file proyek adalah sebagai berikut:

1. Folder `data/dataset` berisi data mentah hasil ekstraksi dari peramban Apify. File `dataset_analisis_sumbawa_hijau_lestari.csv` menyimpan seluruh baris komentar mentah beserta meta data postingan, sedangkan file `daftar_link_sumber.csv` memuat pemetaan 54 tautan postingan Facebook beserta nama akun pembuat konten.
2. Folder `data/processed_dataset` berisi file hasil pembersihan data yang telah siap untuk dilabeli, yaitu `dataset_siap_label_sumbawa_hijau_lestari.xlsx`. Folder ini juga menyimpan file pendukung hasil olahan analisis seperti tabel silang sentimen, ringkasan statistik, frekuensi kata kunci, serta sub-folder `figures/` yang berisi 7 grafik visualisasi format PNG.
3. Folder `data/labelled` berisi file `dataset_siap_label_sumbawa_hijau_lestari_labelled.xlsx` yang merupakan dataset final hasil pelabelan manual penuh oleh peneliti.
4. Folder `documents` diperuntukkan bagi dokumen pendukung proyek, catatan metodologi, dan referensi prompt analisis.
5. Folder `notebook` memuat file Jupyter Notebook untuk seluruh tahapan komputasi. File `01_cleaning_dataset.ipynb` digunakan untuk tahap pembersihan data mentah, dan file `02_analisis_sentimen.ipynb` digunakan untuk tahap validasi label, kalkulasi statistik deskriptif, analisis silang, serta visualisasi grafik.
6. File `.gitignore` berisi konfigurasi pengecualian file atau folder temporer agar tidak terikut dalam lumbung git.
7. File `README.md` merupakan dokumentasi utama proyek yang menjelaskan metodologi, hasil analisis, serta panduan proyek.
8. File `requirements.txt` mencantumkanDaftar pustaka Python yang dibutuhkan untuk menjalankan kode program.
9. File `SET_UP.md` memuat petunjuk teknis mengenai penyiapan lingkungan kerja virtual dan tata cara eksekusi ulang proyek.

## 5. Tahapan Pelaksanaan

Seluruh tahapan proyek dilaksanakan secara sistematis dalam 4 langkah utama berikut:

### 5.1. Pengumpulan Data

Data komentar dikumpulkan menggunakan alat pemindaian otomatis Apify Facebook Comments Scraper dari 54 tautan postingan Facebook yang berkaitan dengan kegiatan "Sumbawa Hijau Lestari". Dari proses ekstraksi ini diperoleh data mentah sebanyak 436 baris dan 243 kolom data. Metode ini dipilih karena dapat mengumpulkan komentar secara akurat, mencakup hierarki komentar balasan, waktu penulisan, dan identitas pemuat postingan secara efisien.

### 5.2. Pembersihan Data

Proses pembersihan data dilakukan melalui notebook `notebook/01_cleaning_dataset.ipynb`. Tahapan pembersihan meliputi pembuangan 5 baris data dari tautan postingan yang tidak dapat diakses, pembuangan 29 baris komentar tanpa isi teks seperti stiker, gambar, dan GIF, eliminasi 1 baris komentar duplikat, penyelarasan format tanggal ke standar ISO (YYYY-MM-DD), serta pemetaan nama akun sumber postingan. Dari total 436 baris data mentah, sebanyak 35 baris data dikeluarkan (berkurang sebesar 8,03%), sehingga menghasilkan 401 baris komentar bersih. Komentar ini terdiri atas 234 komentar utama (58,35%) dan 167 komentar balasan (41,65%). Selain itu, dilakukan penandaan terhadap 10 baris kandidat spam untuk diverifikasi secara manual.

### 5.3. Pelabelan Data

Setiap komentar bersih diberi dua atribut label, yaitu Kategori Isu dan Sentimen. Pelabelan awal dibantu oleh usulan berbasis kata kunci untuk mempercepat penelaahan awal, namun keputusan label akhir ditentukan 100% melalui peninjauan manual oleh peneliti terhadap setiap isi komentar.

Skema Kategori Isu terdiri atas 8 kelas berikut:

1. Obrolan/Balasan Personal: Komentar yang berisi sapaan, Obrolan antar pengguna, atau balasan sosial yang tidak membahas isi materi program secara langsung.
2. Apresiasi/Dukungan Program: Komentar yang menyampaikan ungkapan pujian, apresiasi, wujud dukungan, serta semangat terhadap pelaksanaan program.
3. Kritik Kebijakan & Isu Terkait: Komentar yang menyampaikan kritik terhadap kebijakan pemerintah, dampaknya terhadap alih fungsi lahan pertanian, atau isu lingkungan secara umum.
4. Pertanyaan/Klarifikasi Program: Komentar yang berisi pertanyaan teknis atau permintaan penjelasan mengenai mekanisme, lokasi, dan tata cara pelaksanaan program.
5. Saran Teknis Pelaksanaan: Komentar yang memberikan masukan praktis terkait teknis pelaksanaan, seperti jenis bibit tanaman yang sesuai atau teknik perawatan.
6. Informasi/Netral: Komentar yang menyampaikan fakta, informasi tambahan, atau pernyataan netral tanpa memuat emosi atau pandangan subjektif.
7. Spam/Promosi: Komentar yang berisi promosi penjualan barang atau jasa, tautan komersial tidak relevan, atau pesan berulang.
8. Kritik/Skeptisisme Keberlanjutan: Komentar yang meragukan komitmen jangka panjang, kelangsungan pemeliharaan pohon, atau efektivitas riil program pasca-seremoni penanaman.

Skema Sentimen terdiri atas 3 kelas, yaitu Positif, Netral, dan Negatif.

### 5.4. Analisis dan Penggalian Insight

Tahap akhir dilaksanakan pada notebook `notebook/02_analisis_sentimen.ipynb`. Analisis dilakukan dengan menghitung distribusi statistik sentimen dan kategori isu, analisis silang antara jenis komentar dengan sentimen, perbandingan sentimen antar sumber postingan, tren sentimen bulanan, serta ekstraksi frekuensi kata kunci pada kelompok komentar yang bersifat kritis.

## 6. Akurasi dan Kualitas Data

Tingkat keandalan data dalam analisis ini didukung oleh proses pembersihan yang terukur dan pelabelan manual secara menyeluruh. Dari 436 baris data mentah yang dikumpulkan, terdapat 401 baris data akhir yang dianalisis. Pengurangan data sebesar 8,03% (35 baris) disebabkan oleh adanya postingan privat yang tidak dapat diakses (5 baris), komentar yang hanya berisi stiker atau GIF (29 baris), dan data duplikat (1 baris).

Terdapat dua keterbatasan utama pada data ini:

1. Penggunaan bahasa daerah Sumbawa (basa Samawa) pada sebagian komentar warga. Hal ini membutuhkan penafsiran konteks budaya lokal secara cermat pada saat proses pelabelan manual agar tidak terjadi kesalahan klasifikasi sentimen.
2. Adanya potensi bias sampel karena data yang terambil hanya berasal dari akun Facebook yang bersifat publik dan dari warga yang aktif menuliskan komentar di media sosial.

## 7. Insight yang Diperoleh

Berdasarkan hasil analisis pada notebook `02_analisis_sentimen.ipynb`, diperoleh temuan empiris sebagai berikut:

Proporsi sentimen secara keseluruhan didominasi oleh kelas Netral sebanyak 225 komentar (56,11%), diikuti oleh kelas Positif sebanyak 131 komentar (32,67%), dan kelas Negatif sebanyak 45 komentar (11,22%).

Distribusi kategori isu dari yang terbanyak adalah:

1. Obrolan/Balasan Personal sebanyak 231 komentar (57,61%), dengan rincian 166 sentimen netral dan 65 sentimen positif.
2. Apresiasi/Dukungan Program sebanyak 63 komentar (15,71%), di mana seluruh 63 komentar bernilai sentimen positif (100% positif).
3. Kritik Kebijakan & Isu Terkait sebanyak 29 komentar (7,23%), dengan 28 sentimen negatif dan 1 sentimen positif.
4. Pertanyaan/Klarifikasi Program sebanyak 20 komentar (4,99%), seluruhnya bernilai sentimen netral (20 komentar).
5. Saran Teknis Pelaksanaan sebanyak 17 komentar (4,24%), terdiri atas 15 sentimen netral dan 2 sentimen positif.
6. Kritik/Skeptisisme Keberlanjutan sebanyak 17 komentar (4,24%), di mana seluruh 17 komentar bernilai sentimen negatif (100% negatif).
7. Informasi/Netral sebanyak 13 komentar (3,24%), seluruhnya bernilai sentimen netral (13 komentar).
8. Spam/Promosi sebanyak 11 komentar (2,74%), seluruhnya bernilai sentimen netral (11 komentar).

Terdapat 3 pola utama yang teridentifikasi dalam komentar masyarakat:

1. Kelompok dukungan dan apresiasi yang kuat dari jaringan internal instansi dan sekolah. Pada kategori Apresiasi/Dukungan Program, tingkat sentimen positif mencapai 100%. Selain itu, jenis komentar utama memiliki proporsi sentimen positif yang jauh lebih tinggi (51,28%) dibandingkan jenis komentar balasan (6,59%).
2. Kelompok masyarakat yang skeptis terhadap keberlanjutan program pasca-seremoni. Kelompok ini menyumbangkan 17 komentar sentimen negatif pada kategori Kritik/Skeptisisme Keberlanjutan. Masyarakat menyuarakan kekhawatiran bahwa tanaman yang telah ditanam tidak diperhatikan pemeliharaannya sehingga berpotensi mati.
3. Kelompok yang menyampaikan kritik konstruktif mengenai jenis pohon dan konflik alih fungsi lahan. Pada kategori Kritik Kebijakan (28 komentar negatif), frekuensi kata kunci yang paling sering muncul adalah kata 'pohon' (13 kali), 'hutan' (10 kali), 'tanam' (8 kali), 'bage' (7 kali), 'jagung' (5 kali), dan 'beringin' (4 kali). Warga menyoroti perlunya pemilihan jenis pohon berkayu keras dan tahan lama seperti asam jawa ('bage') atau beringin, serta kritik atas ketidakseimbangan antara kegiatan penghijauan di satu sisi dengan maraknya pembukaan hutan untuk tanaman jagung di sisi lain.

## 8. Kesimpulan dan Rekomendasi

Kesimpulan dari analisis ini menunjukkan bahwa respon publik di media sosial terhadap program "Sumbawa Hijau Lestari" secara umum bersifat netral hingga positif. Sentimen positif didorong oleh partisipasi aktif sekolah dan instansi pemerintah. Namun demikian, substansi kritik dari warga masyarakat berfokus pada dua isu krusial, yaitu kepastian pemeliharaan bibit tanaman jangka panjang dan penataan kebijakan lahan lereng bukit.

Berdasarkan temuan tersebut, dirumuskan rekomendasi perbaikan bagi pemangku kepentingan Pemerintah Kabupaten Sumbawa sebagai berikut:

1. Membentuk mekanisme evaluasi dan pemeliharaan berkala pasca-penanaman. Pemerintah daerah perlu memastikan ketersediaan anggaran dan petugas pemeliharaan agar bibit yang ditanam dapat tumbuh berkelanjutan, bukan sekadar kegiatan seremoni.
2. Memilih jenis bibit pohon yang tepat dan memberikan edukasi publik. Pemerintah disarankan memprioritaskan bibit tanaman lokal berakar kuat dan bermanfaat ekonomis atau ekologis panjang seperti asam jawa ('bage') dan beringin, serta menyampaikan informasi tata cara perawatan kepada masyarakat.
3. Menyelaraskan kebijakan penghijauan dengan penataan alih fungsi lahan pertanian. Pemerintah Kabupaten Sumbawa perlu memperketat regulasi pembukaan hutan untuk ladang jagung di area lereng dan kawasan tangapan air, agar kegiatan penghijauan tidak kontradiktif dengan alih fungsi hutan yang masih berlangsung.

## 9. Cara Menjalankan Ulang Proyek

Untuk menjalankan ulang kode program proyek ini, ikuti petunjuk ringkas berikut:

1. Pastikan sistem telah terinstal Python 3.9 atau versi yang lebih baru.
2. Instal dependensi pustaka yang dibutuhkan menggunakan perintah `pip install -r requirements.txt`.
3. Untuk petunjuk teknis penyiapan lingkungan kerja virtual dan urutan eksekusi notebook, rujuk dokumen [SET_UP.md](file:///c:/Users/Saputra%20Budiman/Documents/Project%20Data%20Science/Analisis%20Sentimen%20Sumbawa%20Hijau%20Lestari/SET_UP.md).
