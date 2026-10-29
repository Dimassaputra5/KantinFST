# Lama Berada di Kantin FST: Hasil Kajian dan Simulasi

Kantin FST menjadi tempat mahasiswa, staf, dosen, dan pengunjung fakultas membeli makan. Area makan di tempatnya terbatas, dan sebagian besar orang yang diamati membeli makanan dalam bungkus untuk dibawa keluar dari area kantin. Kajian ini mengolah 77 catatan kunjungan untuk menjawab empat hal: berapa lama orang biasanya berada di sana, seperti apa pola kunjungannya, distribusi apa yang paling cocok dengan pola itu, dan apakah pola tersebut dapat dipakai untuk membuat simulasi.

## Temuan Singkat

- Setengah kunjungan berakhir dalam 1 menit 47 detik atau kurang. Sebanyak 56% berakhir dalam 2 menit dan 69% dalam 3 menit.
- Rata-rata kunjungan mencapai 2 menit 33 detik. Angka ini lebih tinggi karena enam kunjungan berlangsung antara 8 menit 2 detik dan 8 menit 50 detik.
- Kunjungan singkat jauh lebih banyak daripada kunjungan panjang. Jumlah kunjungan menurun ketika durasi bertambah, dengan celah kosong pada rentang 6 sampai 8 menit.
- Dari empat distribusi yang dibandingkan (normal, uniform, log-normal, dan eksponensial standar), **log-normal paling sesuai**: AIC 915,55 dan KS D 0,0647. Eksponensial memiliki AIC 930,92, uniform 965,90, dan normal 971,80.
- Simulasi 1.000 kunjungan dari model log-normal menghasilkan rata-rata sekitar 2 menit 29 detik dan median sekitar 1 menit 52 detik; proporsi kunjungan singkat tetap mendekati data asli.

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

Kajian membandingkan empat kandidat distribusi: **normal**, **uniform**, **log-normal** dengan `loc=0`, dan **eksponensial standar** dengan `loc=0`. Log-normal dan eksponensial dibatasi `loc=0` agar keduanya tidak menggunakan pergeseran lokasi.

Kecocokan diperiksa melalui log-likelihood, AIC/BIC, dan statistik Kolmogorov–Smirnov (KS). AIC/BIC yang lebih kecil menunjukkan model yang lebih disukai dengan mempertimbangkan jumlah parameter; statistik KS `D` yang lebih kecil berarti kurva kumulatif model lebih dekat ke distribusi empiris. Nilai p KS pada tabel dihitung dengan **parametric bootstrap 2.000 replikasi**, dan parameter diestimasi ulang di setiap replikasi.

**Tabel 2. Perbandingan kecocokan empat distribusi**

| Model | Parameter hasil fit | Log-likelihood | AIC | BIC | KS D | p-value bootstrap KS |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| Log-normal (`loc=0`) | `shape = 0,8101`; `scale = 111,14` | -455,774 | **915,548** | **920,236** | **0,0647** | 0,6037 |
| Eksponensial (`loc=0`) | `scale = 153,23` | -464,461 | 930,923 | 933,266 | 0,1748 | 0,0010 |
| Uniform | `loc = 14`; `scale = 516` | -480,950 | 965,900 | 970,588 | 0,4188 | 0,0005 |
| Normal | `mean = 153,23`; `std = 129,73` | -483,901 | 971,802 | 976,489 | 0,1835 | 0,0005 |

**Interpretasi.** Log-normal paling sesuai dalam perbandingan ini karena mempunyai AIC terendah dan statistik KS D terkecil. Hasil bootstrap KS juga tidak menolak log-normal pada taraf 5% (`p = 0,6037`), sedangkan normal, uniform, dan eksponensial standar ditolak oleh pemeriksaan tersebut (`p < 0,05`). Ini merupakan dukungan relatif untuk log-normal di antara empat kandidat, bukan bukti bahwa distribusi data pasti log-normal.
Pola data tetap didominasi durasi singkat: 53 dari 77 kunjungan selesai dalam 3 menit atau kurang, sementara 12 kunjungan melewati 5 menit. Enam kunjungan berada di kisaran 8 menit dan termasuk pencilan menurut batas IQR 6 menit 36 detik. Kelompok tersebut berkontribusi pada ekor kanan yang panjang dan perlu dipertahankan dalam analisis karena memang diamati di lapangan.

**Catatan interpretasi uji.** p-value bootstrap yang tidak kecil bukan bukti bahwa model pasti benar. Dengan 77 catatan, hasil ini merupakan dukungan relatif terhadap bentuk distribusi, bukan kepastian mengenai mekanisme yang menghasilkan durasi.

## Hasil Simulasi

Simulasi memakai 1.000 durasi baru dari model log-normal (`shape ≈ 0,8101`, `loc = 0`, `scale ≈ 111,14` detik) dan membandingkannya dengan 77 kunjungan asli. Seed acak ditetapkan agar hasil dapat direproduksi.

**Tabel 3. Perbandingan data asli dan hasil simulasi log-normal**

| Ukuran | Data asli (77 kunjungan) | Simulasi log-normal (1.000 kunjungan) |
| --- | ---: | ---: |
| Rata-rata | 153,23 detik (2 menit 33 detik) | 149,26 detik (2 menit 29 detik) |
| Nilai tengah | 107 detik (1 menit 47 detik) | 111,70 detik (1 menit 52 detik) |
| Kunjungan tercepat | 14 detik | 5,78 detik |
| Kunjungan terlama | 530 detik (8 menit 50 detik) | 1.459,69 detik (24 menit 20 detik) |
| Selesai dalam 2 menit | 55,8% | 54,0% |
| Selesai dalam 3 menit | 68,8% | 75,1% |
| Selesai dalam 5 menit | 84,4% | 89,6% |

Rata-rata dan median hasil simulasi dekat dengan data asli. Proporsi yang selesai dalam 2–5 menit juga berada pada kisaran yang sama, meskipun selisihnya terlihat pada batas 3 dan 5 menit. Simulasi lebih besar daripada sampel asli sehingga nilai ekstrem lebih mungkin muncul; durasi maksimum 24 menit 20 detik adalah keluaran model, bukan pengamatan nyata.

Model log-normal dengan `loc=0` memiliki dukungan positif mulai dekat nol, sehingga simulasi dapat menghasilkan durasi di bawah minimum sampel 14 detik. Nilai minimum yang teramati adalah minimum **dalam sampel**, bukan bukti bahwa durasi di bawah 14 detik mustahil.

Simulasi ini hanya membangkitkan lama kunjungan. Ia tidak memodelkan waktu kedatangan, antrean, atau jumlah pengunjung yang berada di kantin pada saat bersamaan.

## Apa Artinya bagi Kantin

Sebagian besar pengunjung tidak berlama-lama di area kantin. Sekitar 56% kunjungan selesai dalam 2 menit, 69% dalam 3 menit, dan 84% dalam 5 menit. Karena makanan umumnya dibawa keluar, durasi ini lebih menggambarkan alur pembelian dan pengambilan makanan, bukan waktu makan di tempat.

Kelompok yang tinggal lama jumlahnya kecil, tetapi keberadaannya perlu diperhitungkan. Enam kunjungan berlangsung sekitar 8 menit, sementara kunjungan biasa hanya sekitar satu setengah sampai dua menit. Karena area makan di tempat kecil, beberapa kunjungan panjang sudah cukup membuat area terasa penuh.

Simulasi yang ada sekarang baru menghasilkan lama kunjungan. Untuk mengukur berapa banyak orang di kantin pada jam tertentu, berapa tempat duduk yang dibutuhkan, atau seberapa panjang antrean, kantin perlu mencatat waktu kedatangan pengunjung. Data lama kunjungan saja tidak cukup untuk menjawab pertanyaan tersebut.

## Keterbatasan

- Jumlah data 77 catatan dan belum merata antar hari maupun jam. Kamis menyumbang 41 catatan, sedangkan Jumat hanya 5 catatan dan pukul 15.00 hanya 9 catatan.
- Data berasal dari Kantin FST pada beberapa hari dan jam. Pengunjungnya didominasi mahasiswa, sehingga pola ini belum tentu menggambarkan kebiasaan staf dan dosen. Pola kunjungan juga bisa berbeda pada jam sibuk, hari libur, atau kantin lain.
- Enam kunjungan sekitar 8 menit tergolong pencilan menurut IQR dan cukup memengaruhi rata-rata. Karena itu, nilai tengah perlu dibaca bersama rata-rata.
- Data tidak mencatat waktu kedatangan. Kajian ini belum bisa menjelaskan jam ramai, jumlah pengunjung pada waktu yang sama, atau antrean.
- Log-normal lebih disukai berdasarkan AIC, statistik KS, dan p-value bootstrap pada perbandingan empat kandidat. Normal, uniform, dan eksponensial standar tidak sesuai menurut pemeriksaan KS bootstrap; hasil tetap perlu dievaluasi dengan lebih banyak data.

## Kesimpulan

Kunjungan ke Kantin FST didominasi durasi singkat. Nilai tengahnya 1 menit 47 detik, 55,8% kunjungan selesai dalam 2 menit, dan 84,4% selesai dalam 5 menit. Rata-rata 2 menit 33 detik lebih tinggi karena enam kunjungan berlangsung sekitar 8 menit.

Dari empat distribusi yang dibandingkan, **log-normal (`loc=0`) paling disukai** berdasarkan AIC (915,55), statistik KS (D = 0,0647), dan p-value bootstrap KS (0,6037). Eksponensial standar memiliki AIC 930,92; uniform 965,90; dan normal 971,80. Simulasi 1.000 kunjungan dari model log-normal menghasilkan rata-rata 2 menit 29 detik dan median 1 menit 52 detik.

Untuk perencanaan kapasitas, jam sibuk, dan antrean, kajian perlu dilengkapi pencatatan waktu kedatangan serta waktu layanan. Sampel yang lebih seimbang menurut hari dan jam juga diperlukan untuk memperkuat kesimpulan.

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
