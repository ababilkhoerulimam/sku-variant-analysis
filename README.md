<div align="center">
  <h1>SKU Variant Analysis</h1>
  <p><strong>Memilih tiga varian HMUG untuk diuji sebagai listing mandiri</strong></p>

  <p align="center">
    <img src="https://img.shields.io/badge/Domain-E--commerce-0D47A1?style=flat-square" alt="Domain E-commerce">
    <img src="https://img.shields.io/badge/Analysis-Descriptive-17785D?style=flat-square" alt="Descriptive Analysis">
    <img src="https://img.shields.io/badge/Status-Completed-success?style=flat-square" alt="Status Completed">
  </p>

  <p align="center">
    Analisis penjualan Juni hingga Agustus 2026 untuk mengurangi ketergantungan katalog pada satu SKU induk. Proyek ini mencakup audit kualitas data, rekonsiliasi angka berulang, ranking kandidat, sensitivity analysis, dan rekomendasi bisnis.
  </p>
</div>

## Ringkasan

Toko memiliki 2.830 SKU, tetapi 49,8% omzet berasal dari tiga SKU induk. HMUG merupakan salah satu kontributor terbesar dan masih terkonsentrasi pada satu varian utama.

Tujuan analisis ini adalah memilih minimal tiga varian HMUG yang memiliki bukti penjualan paling kuat untuk diprioritaskan dalam uji listing mandiri. Listing mandiri berarti setiap varian memperoleh halaman produk sendiri agar performa, stok, iklan, dan promonya lebih mudah dievaluasi.

## Temuan Utama

- Total omzet toko selama tiga bulan mencapai Rp816.449.942.
- Total mentah varian HMUG sebesar Rp259.906.900 mengandung kelebihan pencatatan Rp82.201.479.
- Setelah setiap kelompok angka identik dihitung satu kali, omzet HMUG direkonsiliasi menjadi Rp177.705.421 dengan selisih Rp0 pada setiap bulan.
- Dari 38 varian HMUG, 25 berstatus Normal dan 8 memenuhi seluruh syarat kandidat.
- A01/01 dan C01/03 masuk tiga besar pada seluruh enam pengujian ketahanan.
- D02/01 masuk tiga besar pada empat dari enam pengujian dan dipertahankan karena omzetnya dapat dikonfirmasi sepenuhnya.

## Rekomendasi

| Prioritas | Varian | Omzet terkonfirmasi | Unit | Ketahanan |
|---:|---|---:|---:|---:|
| 1 | A01/01 | Rp94.297.119 | 629 | 6 dari 6 uji |
| 2 | C01/03 | Rp12.827.862 | 71 | 6 dari 6 uji |
| 3 | D02/01 | Rp8.446.915 | 44 | 4 dari 6 uji |

Rekomendasi ini adalah prioritas untuk pengujian listing mandiri, bukan jaminan kenaikan omzet. Dampak aktual perlu diukur melalui pilot atau eksperimen terkontrol.

## Metode

1. Memeriksa struktur workbook, tipe data, nilai kosong, duplikasi kunci, status varian, dan konsistensi total.
2. Mengidentifikasi kelompok penjualan dan unit yang berulang persis pada beberapa varian.
3. Menggunakan pendekatan konservatif dengan tidak mengkreditkan omzet ambigu kepada kandidat utama.
4. Menyaring kandidat yang berstatus Normal, memiliki atribusi penuh, dan terjual pada ketiga bulan.
5. Meranking kandidat berdasarkan omzet, unit, median omzet bulanan, dan omzet pada bulan terlemah.
6. Menguji ketahanan melalui tiga skenario atribusi dan tiga pengujian leave-one-month-out.
7. Mengevaluasi perubahan konsentrasi katalog dan skenario dampak tanpa menganggapnya sebagai forecast.

Penjelasan lebih lengkap tersedia di [dokumen metodologi](docs/methodology.md).

## Struktur Repository

```text
data/raw/                            Workbook sumber
notebooks/sku_variant_analysis.ipynb Analisis utama dan saved output
reports/sku_variant_recommendation.pdf Presentasi hasil analisis
docs/methodology.md                  Metode, asumsi, dan keterbatasan
```

## Menjalankan Notebook

Clone repository dan masuk ke direktorinya:

```bash
git clone https://github.com/ababilkhoerulimam/stock-keeping-unit-data-analyst.git
cd stock-keeping-unit-data-analyst
```

Buat environment dan instal dependency:

```bash
python -m venv .venv
```

Aktifkan environment pada Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Pada macOS atau Linux:

```bash
source .venv/bin/activate
```

Kemudian instal dependency:

```bash
pip install -r requirements.txt
```

Jalankan Jupyter dari root repository, kemudian buka `notebooks/sku_variant_analysis.ipynb`:

```bash
jupyter lab
```

Notebook juga dapat dijalankan langsung dari folder `notebooks` karena pencarian file sumber mendukung kedua working directory.

## Laporan

- [Notebook analisis](notebooks/sku_variant_analysis.ipynb)
- [Presentasi rekomendasi](reports/sku_variant_recommendation.pdf)
- [Metodologi dan keterbatasan](docs/methodology.md)

## Tech Stack

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?style=for-the-badge&logo=Jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-ffffff?style=for-the-badge&logo=Matplotlib&logoColor=black)

## Keterbatasan

- Data hanya mencakup tiga bulan dan Agustus tercatat sampai tanggal 28.
- Tidak tersedia transaction ID untuk menentukan pemilik sebenarnya dari angka varian yang berulang.
- Data tidak memuat COGS, biaya marketplace, iklan, retur, dan ketersediaan stok.
- ASP bukan margin dan skenario what-if bukan forecast.
- Keputusan peluncuran tetap membutuhkan validasi kesiapan stok dan eksperimen bisnis.

## License

Repository ini menggunakan [MIT License](LICENSE).
