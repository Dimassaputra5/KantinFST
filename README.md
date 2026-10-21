# Lama Berada di Kantin

## Tujuan

Dokumen ini merangkum hasil pengolahan data tentang **berapa lama seseorang berada di kantin**. Tujuannya bukan mengukur kecepatan pelayanan, melainkan mengetahui kebiasaan pengunjung: apakah mereka proses pembelian makanan yang cepat, atau ada yang proses pembelian makanan yang lama. Hasilnya dipakai sebagai dasar untuk membuat simulasi kunjungan kantin.

Perhitungan dan grafik lengkapnya ada di `src/simulasi/kantin.ipynb`.

## Instalasi

Cara yang disarankan, memakai `pyproject.toml` dan `uv.lock`:

```bash
uv sync
```

Alternatifnya, memakai `requirements.txt` yang sudah berisi semua paket beserta versinya:

```bash
uv venv
uv pip install -r requirements.txt
```

Setelah itu, buka notebook di VS Code atau Jupyter, lalu pilih kernel/interpreter dari `.venv`.

Jika dependensi di `pyproject.toml` berubah, `requirements.txt` dapat diperbarui dengan:

```bash
uv export --format requirements-txt --no-hashes --no-emit-project -o requirements.txt
```

## Data yang Dipakai

Data berisi 52 catatan durasi kunjungan dari beberapa hari (Senin, Selasa, Kamis, Jumat) dan beberapa jam (pukul 10, 12, dan 15). Sebagian besar catatan berasal dari hari Selasa (25 catatan) dan Kamis (16 catatan).

Gambaran umum datanya:

- Kunjungan tercepat: **14 detik**.
- Kunjungan terlama: **8 menit 38 detik** (518 detik).
- Rata-rata: **2 menit 12 detik** (131,98 detik).
- Nilai tengah: **1 menit 28 detik** (88 detik).
- Sebanyak 34 dari 52 kunjungan (**65%**) selesai dalam 2 menit atau kurang.
- Sebanyak 75% selesai dalam 3 menit atau kurang, dan 88% selesai dalam 5 menit atau kurang.
- Hanya 3 kunjungan yang lebih dari 6 menit.

Rata-rata jauh lebih besar daripada nilai tengah. Artinya, sebagian besar pengunjung keluar dalam waktu singkat, tetapi ada beberapa orang yang tinggal sangat lama sehingga menaikkan rata-rata. Karena itu, nilai tengah (1 menit 28 detik) lebih menggambarkan kunjungan yang "biasa", sedangkan rata-rata (2 menit 12 detik) ikut terangkat oleh kunjungan panjang.

## Alur Pengolahan

1. **Mengubah bentuk data.** Durasi yang semula ditulis seperti "1 menit 50 detik" diubah menjadi jumlah detik agar bisa dihitung.
2. **Memeriksa catatan yang mencolok.** Ada tiga kunjungan yang jauh lebih lama daripada kunjungan lain, yaitu sekitar 8 menit. Catatan ini tetap dipakai karena memang benar-benar terjadi, tetapi perlu diingat sebagai kasus yang jarang.
3. **Mencocokkan data dengan beberapa kemungkinan pola.** Ada tiga pola yang dicoba:
   - banyak kunjungan singkat lalu jumlahnya menurun cepat untuk durasi yang lebih lama;
   - durasi yang simetris di sekitar nilai rata-rata;
   - durasi yang tersebar merata dari singkat sampai lama.
4. **Memilih pola yang paling dekat dengan data.** Hasilnya, hanya pola pertama yang cocok. Pola simetris dan pola merata tidak menggambarkan data dengan baik.

| Pola yang diuji | Hasil |
| --- | --- |
| Menurun cepat, lalu jarang ada kunjungan panjang | Cocok |
| Simetris di sekitar rata-rata | Tidak cocok |
| Tersebar merata | Tidak cocok |

Pola yang terpilih adalah **pola eksponensial**. Secara sederhana, pola ini berarti: semakin lama seseorang berada di kantin, semakin kecil kemungkinan ia masih bertahan di sana. Kunjungan singkat sangat umum, kunjungan sedang cukup sering, dan kunjungan sangat panjang jarang terjadi.

## Arti Hasilnya

Dari pencocokan tersebut, diperoleh dua angka penting:

- **14 detik** adalah batas bawah. Model menganggap tidak ada kunjungan yang lebih singkat dari ini, karena 14 detik adalah durasi tercepat yang tercatat.
- **117,98 detik** adalah tambahan waktu rata-rata setelah batas bawah tersebut.

Jika digabungkan, rata-rata lama kunjungan menjadi:

```text
14 + 117,98 = 131,98 detik
```

Angka ini sama dengan rata-rata data, yaitu sekitar **2 menit 12 detik**.

Pola ini juga menjelaskan mengapa kunjungan 8 menit tetap masuk akal. Dalam pola yang menurun cepat, kunjungan sepanjang itu memang jarang, tetapi bukan mustahil. Jadi, catatan terpanjang tidak perlu dibuang; ia hanya mewakili ekor dari kebiasaan pengunjung.

## Membaca Grafik di Notebook

Ada tiga grafik yang saling melengkapi:

1. **Grafik batang dan garis merah.** Batang menunjukkan data asli, sedangkan garis merah menunjukkan pola yang dipilih. Garis merah mengikuti bentuk batang: tinggi di durasi pendek, lalu menurun untuk durasi panjang. Ini tanda bahwa pola tersebut cukup menggambarkan data.
2. **Grafik dua garis menanjak.** Garis data asli dan garis pola hampir berhimpit. Artinya, perbandingan jumlah kunjungan yang sudah selesai pada setiap batas waktu juga mirip antara data dan model.
3. **Grafik titik-titik.** Titik-titik mengikuti garis lurus diagonal. Semakin dekat titik ke garis, semakin cocok pola tersebut dengan data. Penyimpangan kecil hanya terlihat pada kunjungan yang sangat lama, yang jumlahnya sedikit.

Ketiganya menunjukkan kesimpulan yang sama: pola menurun cepat adalah pola yang paling masuk akal untuk data ini.

## Keterbatasan

- Jumlah data hanya 52 catatan dan tidak merata antar hari maupun jam. Hari Selasa dan Kamis lebih banyak terwakili, sedangkan Jumat hanya 5 catatan. Hasil ini belum tentu berlaku untuk semua hari.
- Tiga kunjungan yang sangat lama cukup berpengaruh terhadap rata-rata. Jika ketiganya tidak dihitung, rata-rata turun menjadi sekitar 1 menit 49 detik. Karena itu, nilai tengah sebaiknya dibaca bersama rata-rata.
- "Cocok" bukan berarti pola ini pasti benar. Artinya, dari data yang ada, pola inilah yang paling dekat dan tidak bertentangan dengan kenyataan.
- Data berasal dari satu kantin. Pola kunjungan bisa berbeda pada jam sibuk, hari libur, atau kantin lain.

## Penggunaan untuk Simulasi

Lama kunjungan dapat dibuat secara acak dengan rumus berikut:

```python
np.random.exponential(scale=117.98) + 14
```

atau:

```python
stats.expon.rvs(loc=14, scale=117.98, size=n)
```

Cara membacanya:

- `+ 14` memastikan tidak ada kunjungan yang lebih singkat dari 14 detik.
- `scale=117.98` menghasilkan tambahan waktu yang rata-rata sekitar 118 detik.
- Hasil akhirnya banyak berisi kunjungan singkat, sebagian kunjungan sedang, dan sedikit kunjungan panjang, sesuai dengan data asli.

Pola ini juga menganggap sisa waktu seseorang di kantin tidak bergantung pada sudah berapa lama ia berada di sana. Dengan kata lain, orang yang sudah 10 menit di kantin dianggap punya peluang keluar dalam menit berikutnya yang sama dengan orang yang baru masuk. Untuk data kunjungan manusia, anggapan ini sebaiknya dipakai dengan hati-hati dan diuji lagi jika data bertambah.

## Kesimpulan

- Sebagian besar pengunjung berada di kantin dalam waktu singkat: 65% tidak lebih dari 2 menit.
- Pola yang paling menggambarkan data adalah pola menurun cepat: kunjungan singkat sangat umum, kunjungan panjang semakin jarang.
- Rata-rata lama kunjungan adalah 2 menit 12 detik, sedangkan kunjungan yang "khas" sekitar 1 menit 28 detik.
- Untuk simulasi, lama kunjungan dapat dibangkitkan dengan `np.random.exponential(scale=117.98) + 14`.
