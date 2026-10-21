# Lama Berada di Kantin FST: Hasil Kajian dan Simulasi

Kantin FST menjadi tempat mahasiswa, staff, dosen, dan pengunjung fakultas membeli makan. Area makan di tempatnya terbatas, dan sebagian besar orang yang diamati membeli makanan dalam bungkus untuk dibawa keluar dari area kantin. Kajian ini mengolah 52 catatan lama kunjungan untuk menjawab tiga hal: berapa lama orang biasanya berada di sana, seperti apa pola kunjungannya, dan apakah pola itu dapat dipakai untuk membuat simulasi.

## Temuan Singkat

- Setengah kunjungan berakhir dalam 1 menit 28 detik atau kurang. Sebanyak 65% berakhir dalam 2 menit.
- Rata-rata kunjungan mencapai 2 menit 12 detik. Angka ini lebih tinggi karena tiga kunjungan berlangsung sekitar 8 menit.
- Kunjungan singkat jauh lebih banyak daripada kunjungan panjang. Jumlah kunjungan menurun ketika durasi bertambah.
- Simulasi 1.000 kunjungan menghasilkan rata-rata 2 menit 9 detik dan pola yang mirip dengan data asli.

## Latar Belakang

Kantin FST memiliki area makan di tempat yang cukup kecil. Pengunjungnya mayoritas mahasiswa, staf, dosen, dengan sedikit pengunjung dari luar fakultas. Sebagian besar orang yang diamati memilih membeli makanan dalam bungkus dan membawanya keluar dari area kantin. Pola ini membuat kunjungan lebih banyak terjadi di area pembelian dan pengambilan makanan, bukan di meja makan.

Pengelola kantin perlu tahu berapa lama orang berada di area kantin. Informasi itu membantu mengatur antrean, menata ruang, dan memperkirakan seberapa cepat area digunakan. Karena makanan umumnya dibawa keluar, lama kunjungan di sini lebih menggambarkan waktu memilih, membeli, dan menunggu makanan, bukan waktu duduk makan.

Data mencatat lama kunjungan, hari, dan jam pengamatan. Data itu tidak mencatat waktu kedatangan, jumlah orang yang datang bersamaan, atau berapa lama seseorang mengantre. Karena itu, kajian ini membatasi pertanyaannya pada lama tinggal dan pola kunjungan. Pertanyaan tentang jam ramai dan panjang antrean memerlukan data tambahan.

## Data yang Dianalisis

Data berisi 52 catatan kunjungan dari hari Senin, Selasa, Kamis, dan Jumat, pada pukul 10.00, 12.00, dan 15.00. Sebagian besar catatan dicatat pada hari Selasa (25 catatan) dan Kamis (16 catatan). Hari Senin 6 catatan dan Jumat 5 catatan.

Setiap catatan berisi lama kunjungan dalam bentuk seperti "1 menit 50 detik". Durasi tersebut diubah menjadi detik agar bisa dihitung. Ringkasan datanya ada di Tabel 1.

**Tabel 1. Ringkasan lama kunjungan**

| Ukuran | Hasil |
| --- | --- |
| Jumlah kunjungan | 52 |
| Kunjungan tercepat | 14 detik |
| Kunjungan terlama | 8 menit 38 detik |
| Rata-rata | 2 menit 12 detik |
| Nilai tengah | 1 menit 28 detik |
| Selesai dalam 2 menit | 65% |
| Selesai dalam 3 menit | 75% |
| Selesai dalam 5 menit | 88% |

Nilai tengah adalah durasi yang membagi data menjadi dua bagian sama banyak. Jika semua kunjungan diurutkan dari yang tercepat sampai yang terlama, kunjungan di posisi tengah berlangsung 1 menit 28 detik. Angka ini menggambarkan kunjungan yang biasa terjadi.

Rata-rata lebih tinggi daripada nilai tengah. Sebagian besar pengunjung keluar dalam waktu singkat, tetapi beberapa orang tinggal jauh lebih lama. Tiga kunjungan berlangsung lebih dari 6 menit, yaitu sekitar 8 menit 2 detik, 8 menit 28 detik, dan 8 menit 38 detik. Ketiganya ikut dihitung karena memang terjadi. Tanpa ketiga catatan itu, rata-rata turun menjadi sekitar 1 menit 49 detik. Perbedaan ini menunjukkan bahwa rata-rata mudah terangkat oleh sedikit kunjungan panjang, sedangkan nilai tengah lebih stabil untuk menggambarkan kebiasaan sehari-hari.

## Pola Kunjungan

Kajian ini mencoba tiga kemungkinan pola. Pola pertama adalah kunjungan singkat yang jumlahnya menurun cepat ketika durasi bertambah. Pola kedua adalah durasi yang simetris di sekitar rata-rata, sehingga kunjungan sangat singkat dan sangat lama sama-sama jarang. Pola ketiga adalah durasi yang tersebar merata dari singkat sampai lama.

Data paling dekat dengan pola pertama. Sebanyak 39 dari 52 kunjungan selesai dalam 3 menit atau kurang, dan hanya 6 kunjungan melewati 5 menit. Jumlah kunjungan menurun ketika durasi bertambah, meskipun ada kenaikan kecil pada rentang 3 sampai 5 menit. Pola kedua dan pola ketiga tidak menggambarkan data dengan baik karena data tidak simetris dan tidak tersebar merata.

Pola menurun cepat dapat diringkas menjadi dua bagian:

- Kunjungan tercepat 14 detik, yang dipakai sebagai titik awal.
- Tambahan waktu rata-rata sekitar 118 detik di atas titik awal itu.

Gabungan keduanya menghasilkan rata-rata 131,98 detik atau 2 menit 12 detik. Sebagian besar tambahan waktu berukuran pendek. Hanya sebagian kecil yang panjang, dan itulah yang menjelaskan keberadaan kunjungan sekitar 8 menit. Pola ini juga menjelaskan mengapa kunjungan panjang tidak perlu dibuang. Kunjungan seperti itu jarang, tetapi tetap merupakan bagian dari kebiasaan pengunjung.

## Hasil Simulasi

Simulasi menguji apakah pola yang ditemukan dapat menghasilkan data baru yang mirip dengan data asli. Simulasi memakai 1.000 kunjungan acak dengan aturan 14 detik ditambah tambahan waktu rata-rata 118 detik. Hasilnya dibandingkan dengan 52 kunjungan asli.

**Tabel 2. Perbandingan data asli dan hasil simulasi**

| Ukuran | Data asli (52 kunjungan) | Simulasi (1.000 kunjungan) |
| --- | --- | --- |
| Rata-rata | 2 menit 12 detik | 2 menit 9 detik |
| Nilai tengah | 1 menit 28 detik | 1 menit 35 detik |
| Kunjungan tercepat | 14 detik | 14,5 detik |
| Kunjungan terlama | 8 menit 38 detik | 16 menit 18 detik |
| Selesai dalam 2 menit | 65% | 60% |
| Selesai dalam 3 menit | 75% | 76% |
| Selesai dalam 5 menit | 88% | 91% |

Hasil simulasi mendekati data asli pada rata-rata dan persentase kunjungan pendek. Selisih beberapa poin persen muncul karena data asli hanya berisi 52 catatan, sedangkan simulasi memakai 1.000 kunjungan. Jumlah data yang berbeda membuat kejadian langka lebih mudah muncul di simulasi. Salah satunya adalah kunjungan 16 menit 18 detik, yang tidak muncul di data asli tetapi mungkin terjadi dalam pola menurun cepat. Karena memakai angka acak, hasil simulasi dapat berbeda sedikit jika dijalankan ulang.

Simulasi membantu melihat kemungkinan yang masuk akal berdasarkan data. Di notebook, grafik durasi simulasi mengikuti pola menurun cepat. Garis data asli dan garis simulasi hampir berhimpit. Bagian kunjungan yang selesai dalam 2, 3, serta 5 menit juga berada di kisaran yang berdekatan.

## Apa Artinya bagi Kantin

Sebagian besar pengunjung tidak berlama-lama di area kantin. Sekitar dua dari tiga kunjungan selesai dalam 2 menit, dan hampir sembilan dari sepuluh kunjungan selesai dalam 5 menit. Karena makanan umumnya dibawa keluar, durasi ini lebih menggambarkan alur pembelian dan pengambilan makanan, bukan waktu makan di tempat.

Kelompok yang tinggal lama jumlahnya kecil, tetapi keberadaannya perlu diperhitungkan. Satu kunjungan 8 menit berada di area kantin selama delapan menit, sementara kunjungan biasa hanya sekitar satu setengah menit. Karena area makan di tempat kecil, beberapa kunjungan panjang sudah cukup membuat area terasa penuh.

Simulasi yang ada sekarang baru menghasilkan lama kunjungan. Untuk mengukur berapa banyak orang di kantin pada jam tertentu, berapa tempat duduk yang dibutuhkan, atau seberapa panjang antrean, kantin perlu mencatat waktu kedatangan pengunjung. Data lama kunjungan saja tidak cukup untuk menjawab pertanyaan tersebut.

## Keterbatasan

- Jumlah data hanya 52 catatan dan tidak merata antar hari maupun jam. Hari Selasa dan Kamis lebih banyak terwakili, sedangkan Jumat hanya 5 catatan.
- Data berasal dari Kantin FST pada beberapa hari dan jam. Pengunjungnya didominasi mahasiswa, sehingga pola ini belum tentu menggambarkan kebiasaan staf dan dosen. Pola kunjungan juga bisa berbeda pada jam sibuk, hari libur, atau kantin lain.
- Tiga kunjungan sekitar 8 menit cukup memengaruhi rata-rata. Karena itu, nilai tengah perlu dibaca bersama rata-rata.
- Data tidak mencatat waktu kedatangan. Kajian ini belum bisa menjelaskan jam ramai, jumlah pengunjung pada waktu yang sama, atau antrean.
- Pola yang ditemukan adalah perkiraan terdekat dari data yang ada, bukan kepastian. Data yang lebih banyak dapat mengubah gambaran.

## Kesimpulan

Kunjungan ke Kantin FST didominasi kunjungan singkat. Nilai tengah 1 menit 28 detik dan 65% kunjungan selesai dalam 2 menit. Rata-rata 2 menit 12 detik lebih tinggi karena tiga kunjungan berlangsung sekitar 8 menit.

Pola yang paling menggambarkan data adalah penurunan cepat: kunjungan singkat banyak, kunjungan panjang jarang. Simulasi 1.000 kunjungan berhasil meniru pola itu dengan rata-rata 2 menit 9 detik dan persentase kunjungan pendek yang berdekatan dengan data asli. Untuk perencanaan kapasitas dan jam sibuk, kajian ini perlu dilengkapi data waktu kedatangan.

## Lampiran: Menjalankan Ulang

Perhitungan dan grafik lengkap ada di `src/simulasi/kantin.ipynb`. Data asli ada di `data/data_durasi.csv`. Proyek memakai Python 3.12.

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
