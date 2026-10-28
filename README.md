# Lama Berada di Kantin FST: Hasil Kajian dan Simulasi

Kantin FST menjadi tempat mahasiswa, staf, dosen, dan pengunjung fakultas membeli makan. Area makan di tempatnya terbatas, dan sebagian besar orang yang diamati membeli makanan dalam bungkus untuk dibawa keluar dari area kantin. Kajian ini mengolah 77 catatan kunjungan untuk menjawab empat hal: berapa lama orang biasanya berada di sana, seperti apa pola kunjungannya, distribusi apa yang paling cocok dengan pola itu, dan apakah pola tersebut dapat dipakai untuk membuat simulasi.

## Temuan Singkat

- Setengah kunjungan berakhir dalam 1 menit 47 detik atau kurang. Sebanyak 56% berakhir dalam 2 menit dan 69% dalam 3 menit.
- Rata-rata kunjungan mencapai 2 menit 33 detik. Angka ini lebih tinggi karena enam kunjungan berlangsung antara 8 menit 2 detik dan 8 menit 50 detik.
- Kunjungan singkat jauh lebih banyak daripada kunjungan panjang. Jumlah kunjungan menurun ketika durasi bertambah, dengan celah kosong pada rentang 6 sampai 8 menit.
- Distribusi eksponensial cocok dengan data (uji Kolmogorov-Smirnov: D = 0,117; p = 0,222), sedangkan distribusi normal dan uniform ditolak.
- Simulasi 1.000 kunjungan menghasilkan rata-rata 2 menit 29 detik dan pola yang mirip dengan data asli.

## Latar Belakang

Kantin FST memiliki area makan di tempat yang cukup kecil. Pengunjungnya mayoritas mahasiswa, staf, dosen, dengan sedikit pengunjung dari luar fakultas. Sebagian besar orang yang diamati memilih membeli makanan dalam bungkus dan membawanya keluar dari area kantin. Pola ini membuat kunjungan lebih banyak terjadi di area pembelian dan pengambilan makanan, bukan di meja makan.

Pengelola kantin perlu tahu berapa lama orang berada di area kantin. Informasi itu membantu mengatur antrean, menata ruang, dan memperkirakan seberapa cepat area digunakan. Karena makanan umumnya dibawa keluar, lama kunjungan di sini lebih menggambarkan waktu memilih, membeli, dan menunggu makanan, bukan waktu duduk makan.

Data mencatat lama kunjungan, hari, dan jam pengamatan. Data itu tidak mencatat waktu kedatangan, jumlah orang yang datang bersamaan, atau berapa lama seseorang mengantre. Karena itu, kajian ini membatasi pertanyaannya pada lama tinggal dan pola kunjungan. Pertanyaan tentang jam ramai dan panjang antrean memerlukan data tambahan.

## Data yang Dianalisis

Data yang dianalisis ada di `data/tabel_durasi.csv` dan berisi 77 catatan kunjungan dari hari Senin, Selasa, Kamis, dan Jumat, pada pukul 10.00, 12.00, dan 15.00. Sebarannya belum merata: Kamis mendominasi dengan 41 catatan, lalu Selasa 25 catatan, Senin 6 catatan, dan Jumat 5 catatan. Menurut jam, tercatat 35 kunjungan pada pukul 10.00, 33 pada pukul 12.00, dan 9 pada pukul 15.00.

Setiap catatan berisi lama kunjungan dalam bentuk seperti "1 menit 50 detik". Durasi tersebut diubah menjadi detik agar bisa dihitung. Ringkasan datanya ada di Tabel 1.

**Tabel 1. Ringkasan lama kunjungan**

| Ukuran | Hasil |
| --- | --- |
| Jumlah kunjungan | 77 |
| Kunjungan tercepat | 14 detik |
| Kunjungan terlama | 8 menit 50 detik |
| Rata-rata | 2 menit 33 detik |
| Nilai tengah | 1 menit 47 detik |
| Kuartil bawah (Q1) | 1 menit 1 detik |
| Kuartil atas (Q3) | 3 menit 15 detik |
| Selesai dalam 2 menit | 55,8% |
| Selesai dalam 3 menit | 68,8% |
| Selesai dalam 5 menit | 84,4% |

Nilai tengah adalah durasi yang membagi data menjadi dua bagian sama banyak. Jika semua kunjungan diurutkan dari yang tercepat sampai yang terlama, kunjungan di posisi tengah berlangsung 1 menit 47 detik. Angka ini menggambarkan kunjungan yang biasa terjadi.

Rata-rata lebih tinggi daripada nilai tengah. Sebagian besar pengunjung keluar dalam waktu singkat, tetapi beberapa orang tinggal jauh lebih lama. Enam kunjungan berlangsung antara 8 menit 2 detik dan 8 menit 50 detik. Dengan batas kewajaran statistik Q3 + 1,5 × IQR, yaitu 6 menit 36 detik, keenam catatan itu tergolong pencilan. Catatan tersebut tetap dihitung karena memang terjadi. Tanpa keenamnya, rata-rata turun menjadi sekitar 2 menit 4 detik. Perbedaan ini menunjukkan bahwa rata-rata mudah terangkat oleh sedikit kunjungan panjang, sedangkan nilai tengah lebih stabil untuk menggambarkan kebiasaan sehari-hari.

## Pola Kunjungan

Kajian ini menguji tiga kemungkinan bentuk sebaran. Bentuk pertama adalah eksponensial, yaitu kunjungan singkat yang jumlahnya menurun cepat ketika durasi bertambah. Bentuk kedua adalah normal, yaitu durasi yang simetris di sekitar rata-rata sehingga kunjungan sangat singkat dan sangat lama sama-sama jarang. Bentuk ketiga adalah uniform, yaitu durasi yang tersebar merata dari singkat sampai lama.

Kecocokan setiap bentuk diuji dengan Kolmogorov-Smirnov. Uji ini membandingkan sebaran kumulatif data dengan sebaran kumulatif model; semakin kecil statistik D, semakin dekat model dengan data. Hasilnya ada di Tabel 2.

**Tabel 2. Hasil uji kecocokan distribusi**

| Distribusi | Parameter hasil fit | D | p-value | Keputusan (α = 0,05) |
| --- | --- | --- | --- | --- |
| Eksponensial | loc = 14; scale = 139,23 | 0,117 | 0,222 | Tidak ditolak |
| Normal | rata-rata = 153,23; simpangan baku = 129,73 | 0,184 | 0,010 | Ditolak |
| Uniform | loc = 14; scale = 516 | 0,419 | < 0,001 | Ditolak |

Data paling dekat dengan bentuk eksponensial. Sebanyak 53 dari 77 kunjungan selesai dalam 3 menit atau kurang, dan hanya 12 kunjungan melewati 5 menit. Jumlah kunjungan menurun ketika durasi bertambah, meskipun ada kenaikan kecil pada rentang 3 sampai 5 menit. Bentuk normal dan uniform tidak menggambarkan data dengan baik karena data tidak simetris dan tidak tersebar merata.

Pola menurun cepat dapat diringkas menjadi dua bagian:

- Kunjungan tercepat 14 detik, yang dipakai sebagai titik awal.
- Tambahan waktu rata-rata sekitar 139 detik di atas titik awal itu.

Gabungan keduanya menghasilkan rata-rata 153,23 detik atau 2 menit 33 detik. Sebagian besar tambahan waktu berukuran pendek. Hanya sebagian kecil yang panjang, dan itulah yang menjelaskan keberadaan enam kunjungan sekitar 8 menit. Pola ini juga menjelaskan mengapa kunjungan panjang tidak perlu dibuang. Kunjungan seperti itu jarang, tetapi tetap merupakan bagian dari kebiasaan pengunjung. Perlu dicatat, p-value 0,222 hanya berarti data belum cukup untuk menolak bentuk eksponensial, bukan bukti bahwa pola itu pasti benar.

## Hasil Simulasi

Simulasi menguji apakah pola yang ditemukan dapat menghasilkan data baru yang mirip dengan data asli. Simulasi memakai 1.000 kunjungan acak dengan aturan 14 detik ditambah tambahan waktu acak yang rata-rata 139,23 detik. Hasilnya dibandingkan dengan 77 kunjungan asli.

**Tabel 3. Perbandingan data asli dan hasil simulasi**

| Ukuran | Data asli (77 kunjungan) | Simulasi (1.000 kunjungan) |
| --- | --- | --- |
| Rata-rata | 2 menit 33 detik | 2 menit 29 detik |
| Nilai tengah | 1 menit 47 detik | 1 menit 50 detik |
| Kunjungan tercepat | 14 detik | 14,6 detik |
| Kunjungan terlama | 8 menit 50 detik | 19 menit 12 detik |
| Selesai dalam 2 menit | 55,8% | 54,2% |
| Selesai dalam 3 menit | 68,8% | 70,8% |
| Selesai dalam 5 menit | 84,4% | 86,7% |

Hasil simulasi mendekati data asli pada rata-rata, nilai tengah, dan persentase kunjungan pendek. Selisih beberapa poin persen muncul karena data asli hanya berisi 77 catatan, sedangkan simulasi memakai 1.000 kunjungan. Jumlah data yang berbeda membuat kejadian langka lebih mudah muncul di simulasi. Salah satunya adalah kunjungan 19 menit 12 detik, yang tidak muncul di data asli tetapi mungkin terjadi dalam pola eksponensial. Karena memakai angka acak, hasil simulasi dapat berbeda sedikit jika dijalankan ulang; notebook memakai `np.random.seed(42)` agar hasilnya dapat diulang.

Simulasi membantu melihat kemungkinan yang masuk akal berdasarkan data. Di notebook, grafik durasi simulasi mengikuti pola menurun cepat. Garis data asli dan garis simulasi hampir berhimpit. Bagian kunjungan yang selesai dalam 2, 3, serta 5 menit juga berada di kisaran yang berdekatan.

## Apa Artinya bagi Kantin

Sebagian besar pengunjung tidak berlama-lama di area kantin. Sekitar 56% kunjungan selesai dalam 2 menit, 69% dalam 3 menit, dan 84% dalam 5 menit. Karena makanan umumnya dibawa keluar, durasi ini lebih menggambarkan alur pembelian dan pengambilan makanan, bukan waktu makan di tempat.

Kelompok yang tinggal lama jumlahnya kecil, tetapi keberadaannya perlu diperhitungkan. Enam kunjungan berlangsung sekitar 8 menit, sementara kunjungan biasa hanya sekitar satu setengah sampai dua menit. Karena area makan di tempat kecil, beberapa kunjungan panjang sudah cukup membuat area terasa penuh.

Simulasi yang ada sekarang baru menghasilkan lama kunjungan. Untuk mengukur berapa banyak orang di kantin pada jam tertentu, berapa tempat duduk yang dibutuhkan, atau seberapa panjang antrean, kantin perlu mencatat waktu kedatangan pengunjung. Data lama kunjungan saja tidak cukup untuk menjawab pertanyaan tersebut.

## Keterbatasan

- Jumlah data 77 catatan dan belum merata antar hari maupun jam. Kamis menyumbang 41 catatan, sedangkan Jumat hanya 5 catatan dan pukul 15.00 hanya 9 catatan.
- Data berasal dari Kantin FST pada beberapa hari dan jam. Pengunjungnya didominasi mahasiswa, sehingga pola ini belum tentu menggambarkan kebiasaan staf dan dosen. Pola kunjungan juga bisa berbeda pada jam sibuk, hari libur, atau kantin lain.
- Enam kunjungan sekitar 8 menit tergolong pencilan menurut IQR dan cukup memengaruhi rata-rata. Karena itu, nilai tengah perlu dibaca bersama rata-rata.
- Data tidak mencatat waktu kedatangan. Kajian ini belum bisa menjelaskan jam ramai, jumlah pengunjung pada waktu yang sama, atau antrean.
- Pola eksponensial adalah model terdekat dari data yang ada, bukan kepastian. Data yang lebih banyak dapat mengubah gambaran dan hasil uji.

## Kesimpulan

Kunjungan ke Kantin FST didominasi kunjungan singkat. Nilai tengah 1 menit 47 detik, 55,8% kunjungan selesai dalam 2 menit, dan 84,4% selesai dalam 5 menit. Rata-rata 2 menit 33 detik lebih tinggi karena enam kunjungan berlangsung sekitar 8 menit.

Pola yang paling menggambarkan data adalah penurunan cepat yang sesuai dengan distribusi eksponensial (loc 14 detik, scale 139,23 detik). Uji Kolmogorov-Smirnov tidak menolak model ini (D = 0,117; p = 0,222), sedangkan model normal dan uniform ditolak. Simulasi 1.000 kunjungan berhasil meniru pola itu dengan rata-rata 2 menit 29 detik dan persentase kunjungan pendek yang berdekatan dengan data asli.

Meski begitu, untuk perencanaan kapasitas dan jam sibuk, kajian ini perlu dilengkapi data waktu kedatangan.

## Lampiran: Menjalankan Ulang

Perhitungan dan grafik lengkap ada di `src/simulasi/kantin.ipynb`, dengan data di `data/tabel_durasi.csv` (77 catatan). Proyek memakai Python 3.12.

Cara yang disarankan, memakai `pyproject.toml` dan `uv.lock`:

```bash
uv sync
```

Alternatifnya, memakai `requirements.txt` yang sudah berisi semua paket beserta versinya:

```bash
uv venv
uv pip install -r requirements.txt
```

Setelah itu, buka notebook di VS Code atau Jupyter, lalu pilih kernel atau interpreter dari `.venv`.

Jika dependensi di `pyproject.toml` berubah, perbarui `requirements.txt` dengan:

```bash
uv export --format requirements-txt --no-hashes --no-emit-project -o requirements.txt
```
