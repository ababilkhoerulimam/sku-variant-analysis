# Metodologi Analisis Varian SKU

## Tujuan

Analisis ini memilih sedikitnya tiga varian aktif dari SKU induk HMUG untuk diprioritaskan dalam uji listing mandiri. Unit analisisnya adalah satu kombinasi kode varian dan warna dengan agregat penjualan bulanan selama Juni hingga Agustus 2026.

Pendekatan yang digunakan bersifat deskriptif dan rule-based. Tidak ada model machine learning atau forecast karena setiap varian hanya memiliki tiga observasi bulanan.

## Data

Workbook sumber terdiri dari lima sheet:

- Total penjualan toko
- Kontribusi SKU induk
- Varian HMUG
- Varian HAMPERS
- Varian HAMPERS WEDDING-1

Data mencakup 2.830 SKU induk, 110 baris varian, dan total penjualan toko Rp816.449.942. Data Agustus hanya tercatat sampai tanggal 28.

## Audit Kualitas Data

Pemeriksaan awal mencakup:

- Nilai kosong pada kunci utama
- Nilai penjualan atau produk negatif
- Duplikasi kombinasi SKU dan varian
- Konsistensi status varian
- Rekonsiliasi total bulanan
- Konsistensi share terhadap total toko

Tidak ditemukan kegagalan blocking. Satu anomali ditemukan pada HMUG, yaitu total mentah seluruh baris varian lebih besar daripada total SKU induknya.

## Rekonsiliasi Angka Berulang

Total mentah baris varian HMUG adalah Rp259.906.900, sedangkan total SKU induk HMUG adalah Rp177.705.421. Selisih Rp82.201.479 berasal dari empat kelompok kombinasi bulan, penjualan, dan unit yang tercatat identik pada empat varian berbeda.

Karena workbook tidak memiliki transaction ID atau kolom pemilik omzet, angka tersebut tidak dapat dikaitkan secara pasti kepada salah satu varian. Setiap kelompok identik kemudian dihitung satu kali untuk kebutuhan rekonsiliasi.

Hasilnya cocok dengan total induk pada setiap bulan:

| Bulan | Total HMUG setelah rekonsiliasi |
|---|---:|
| Juni | Rp72.286.794 |
| Juli | Rp52.723.759 |
| Agustus | Rp52.694.868 |
| Total | Rp177.705.421 |

Rekonsiliasi ini membuktikan adanya pencatatan berulang, tetapi tidak membuktikan varian mana yang sebenarnya menghasilkan omzet tersebut.

## Aturan Atribusi Utama

Ranking utama menggunakan aturan konservatif. Nilai penjualan dan unit yang muncul identik pada beberapa varian tidak dikreditkan kepada kandidat mana pun. Sebuah varian hanya menerima omzet ketika kombinasi penjualan dan unit bulanannya dapat dikaitkan secara unik.

Pendekatan ini dipilih untuk mencegah satu nilai yang sama dihitung sebagai omzet penuh bagi beberapa kandidat.

## Syarat Kandidat

Varian harus memenuhi tiga syarat berikut:

1. Berstatus `Normal` pada dataset.
2. Seluruh omzet yang digunakan dalam ranking memiliki atribusi jelas.
3. Memiliki penjualan positif pada Juni, Juli, dan Agustus.

Funnel seleksi menghasilkan:

| Tahap | Jumlah varian |
|---|---:|
| Seluruh varian HMUG | 38 |
| Berstatus Normal | 25 |
| Lolos seluruh syarat | 8 |
| Direkomendasikan | 3 |

## Ranking

Delapan kandidat dibandingkan menggunakan empat metrik:

- Total omzet terkonfirmasi
- Total produk terjual
- Median omzet bulanan
- Omzet pada bulan terlemah

Ketiga rekomendasi menempati tiga besar pada seluruh metrik tersebut dalam ranking konservatif.

| Prioritas | Varian | Omzet | Unit | ASP |
|---:|---|---:|---:|---:|
| 1 | A01/01 | Rp94.297.119 | 629 | Rp149.916 |
| 2 | C01/03 | Rp12.827.862 | 71 | Rp180.674 |
| 3 | D02/01 | Rp8.446.915 | 44 | Rp191.975 |

ASP dihitung sebagai omzet terkonfirmasi dibagi produk terkonfirmasi. ASP tidak dapat digunakan sebagai pengganti margin.

## Pengujian Ketahanan

Keputusan diuji melalui enam kondisi:

1. Omzet ambigu tidak dialokasikan.
2. Omzet ambigu dibagi rata ke seluruh varian terkait.
3. Omzet ambigu dibagi rata hanya ke varian aktif.
4. Ranking dihitung tanpa Juni.
5. Ranking dihitung tanpa Juli.
6. Ranking dihitung tanpa Agustus.

Hasil pengujian:

| Varian | Masuk tiga besar |
|---|---:|
| A01/01 | 6 dari 6 uji |
| C01/03 | 6 dari 6 uji |
| D02/01 | 4 dari 6 uji |

D02 tetap dipilih sebagai kandidat ketiga karena seluruh omzetnya terkonfirmasi dan varian tersebut menang pada mayoritas pengujian. A02 menjadi kandidat alternatif apabila atribusi omzet berulang dapat dibuktikan melalui sumber operasional.

## Konsentrasi Katalog

Pemisahan tiga rekomendasi merupakan reklasifikasi historis. Total omzet toko dan total omzet HMUG tidak berubah.

Pada tiga skenario atribusi, HHI katalog turun dari 982,7 menjadi 703,8 atau 700,9. Penurunan berkisar 28,4% hingga 28,7%. HHI digunakan sebagai indikator konsentrasi pencatatan katalog, bukan sebagai bukti kausal bahwa risiko bisnis pasti menurun.

Di dalam portofolio tiga rekomendasi, A01 masih menyumbang 81,6% omzet. Artinya, pemisahan memperbaiki struktur katalog tetapi belum membuktikan bahwa permintaan sudah terdiversifikasi.

## What-if

Skenario perubahan omzet tiga rekomendasi menggunakan input asumsi dari -10% sampai +20%. Dampaknya terhadap total omzet toko berkisar -1,4% sampai +2,8%.

Skenario nol mempertahankan total toko dan omzet tiga rekomendasi. Seluruh skenario merupakan ilustrasi sensitivitas, bukan prediksi atau probabilitas keberhasilan.

## Batasan

- Hanya tersedia tiga bulan data agregat.
- Agustus merupakan bulan parsial sampai tanggal 28.
- Tidak tersedia transaction ID untuk menyelesaikan atribusi angka berulang.
- Status `Normal` belum tentu menjamin kesiapan persediaan atau produksi.
- Tidak tersedia COGS, biaya marketplace, subsidi pengiriman, packaging, biaya iklan, retur, dan data margin.
- Tidak tersedia hasil eksperimen listing mandiri.

## Validasi Akhir

Notebook memuat 29 pemeriksaan kualitas akhir. Pemeriksaan tersebut mencakup rekonsiliasi bulanan, jumlah rekomendasi, status kandidat, atribusi omzet, kontinuitas penjualan, ranking, sensitivity analysis, leave-one-month-out, konservasi total, HHI, what-if, ASP, dan kebutuhan data margin.

Seluruh pemeriksaan pada saved output terakhir berstatus `LULUS`.
