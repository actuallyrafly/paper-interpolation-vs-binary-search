# Paper: Interpolation Search vs Binary Search

Eksperimen terkontrol untuk menganalisis kinerja **Interpolation Search** dan **Binary Search** pada data numerik terurut dengan variasi distribusi dan ukuran data.

> Repository: `paper-interpolation-vs-binary-search`
>
> Status: tahap perumusan proposal dan studi literatur.

## Tujuan Penelitian

Penelitian ini bertujuan membandingkan kinerja Interpolation Search dan Binary Search berdasarkan karakteristik data, khususnya:

- distribusi nilai data;
- ukuran dataset;
- waktu eksekusi;
- jumlah iterasi/perbandingan; dan
- penggunaan memori sebagai metrik tambahan.

Penelitian ini tidak hanya menanyakan algoritma mana yang lebih cepat, tetapi juga **pada kondisi apa** masing-masing algoritma lebih sesuai digunakan.

## Judul Sementara

> **Analisis Kinerja Interpolation Search dan Binary Search terhadap Variasi Distribusi Data Numerik Berskala Besar**

Judul ini masih bersifat sementara dan akan dikonfirmasi bersama dosen pembimbing. Istilah “berskala besar” perlu disesuaikan dengan ukuran data yang benar-benar dapat diuji pada perangkat yang tersedia.

## Rumusan Masalah

1. Bagaimana perbandingan kinerja Interpolation Search dan Binary Search berdasarkan waktu eksekusi, jumlah iterasi, dan penggunaan memori pada berbagai distribusi data numerik?
2. Bagaimana pengaruh ukuran data terhadap kinerja kedua algoritma pada distribusi uniform, normal, eksponensial, dan clustered?
3. Pada distribusi dan ukuran data seperti apa Interpolation Search memiliki kinerja lebih baik, setara, atau lebih rendah dibandingkan Binary Search?
4. Apakah perbedaan kinerja antara kedua algoritma menunjukkan perbedaan yang signifikan secara statistik?

## Research Gap Sementara

Penelitian terdahulu di Indonesia telah membandingkan beberapa algoritma pencarian berdasarkan waktu eksekusi dan penggunaan memori. Namun, penelitian tersebut umumnya menggunakan aplikasi atau dataset tertentu, ukuran data yang terbatas, atau belum menguji variasi distribusi data secara sistematis.

Penelitian ini memfokuskan perbandingan pada dua algoritma, yaitu Interpolation Search dan Binary Search, dengan menyilangkan beberapa distribusi data numerik dan ukuran dataset. Fokus analisisnya adalah mengidentifikasi kondisi ketika keunggulan Interpolation Search muncul atau hilang dibandingkan Binary Search.

Research gap ini masih harus diverifikasi melalui pembacaan artikel dan persetujuan dosen pembimbing.

## Ruang Lingkup Eksperimen

### Algoritma

- Binary Search
- Interpolation Search

### Distribusi Data

| Distribusi | Karakteristik |
|---|---|
| Uniform | Nilai tersebar relatif merata |
| Normal | Nilai banyak berkumpul di sekitar rata-rata |
| Eksponensial/skewed | Nilai terkonsentrasi pada salah satu sisi |
| Clustered | Nilai membentuk beberapa kelompok dengan jarak antarkelompok |

Semua dataset harus diurutkan sebelum digunakan oleh kedua algoritma.

### Ukuran Dataset Awal

- `10^3`
- `10^4`
- `10^5`
- `10^6`
- `10^7` sebagai target jika perangkat mampu menjalankannya secara stabil

Eksperimen awal sebaiknya dimulai dari `10^3` sampai `10^6`. Ukuran `10^7` tidak boleh dianggap wajib sebelum dilakukan uji kelayakan perangkat.

### Skenario Pencarian

- target berada di awal data;
- target berada di tengah data;
- target berada di akhir data;
- target tidak ditemukan.

### Rancangan Eksperimen

Secara teoritis:

```text
4 distribusi × 5 ukuran data × 2 algoritma = 40 kombinasi utama
```

Setiap kombinasi direncanakan diulang minimal 30 kali. Jumlah pengulangan dan ukuran dataset dapat disesuaikan setelah uji coba awal.

### Metrik

1. **Waktu eksekusi** menggunakan `time.perf_counter_ns()`.
2. **Jumlah iterasi atau perbandingan** sebagai metrik yang lebih independen dari spesifikasi perangkat.
3. **Penggunaan memori** menggunakan `tracemalloc` sebagai metrik tambahan.
4. **Rata-rata, median, standar deviasi, dan interval kepercayaan** bila memungkinkan.
5. **Uji statistik** menggunakan uji t atau Mann–Whitney dengan `α = 0,05`, setelah memeriksa kesesuaian data dan asumsi uji.

### Aturan Reproduksibilitas

- Gunakan dataset yang sama untuk kedua algoritma.
- Gunakan target pencarian yang sama untuk kedua algoritma.
- Tetapkan random seed.
- Pisahkan waktu pembangkitan dan pengurutan dataset dari waktu pencarian.
- Catat CPU, RAM, sistem operasi, versi Python, dan versi pustaka.
- Validasi bahwa kedua algoritma memberikan hasil pencarian yang sama.
- Protokol awal menggunakan data numerik integer terurut dengan nilai unik. Penanganan duplikasi menjadi pengembangan lanjutan.

## Struktur Repository

```text
paper-interpolation-vs-binary-search/
├── README.md
├── LICENSE
├── .gitignore
├── requirements.txt
├── pyproject.toml
│
├── data/
│   ├── README.md
│   ├── raw/
│   │   └── .gitkeep
│   └── generated/
│       └── .gitkeep
│
├── src/
│   ├── __init__.py
│   ├── algorithms/
│   │   ├── __init__.py
│   │   ├── binary_search.py
│   │   └── interpolation_search.py
│   ├── data_generation.py
│   ├── metrics.py
│   ├── validation.py
│   └── benchmark.py
│
├── experiments/
│   ├── __init__.py
│   ├── run_benchmark.py
│   ├── configs/
│   │   └── default.yaml
│   └── notebooks/
│       └── exploratory_analysis.ipynb
│
├── tests/
│   ├── __init__.py
│   ├── test_algorithms.py
│   └── test_data_generation.py
│
├── results/
│   ├── README.md
│   ├── raw/
│   │   └── .gitkeep
│   ├── tables/
│   │   └── .gitkeep
│   └── figures/
│       └── .gitkeep
│
└── docs/
    ├── literature-review.md
    ├── methodology.md
    └── research-log.md
```

## Penjelasan Folder

### `src/algorithms/`

Implementasi algoritma yang diuji. Setiap algoritma sebaiknya memiliki antarmuka fungsi yang konsisten, misalnya:

```python
def search(sorted_data, target):
    """Mengembalikan indeks target atau -1 jika tidak ditemukan."""
```

### `src/data_generation.py`

Berisi fungsi pembangkitan distribusi uniform, normal, eksponensial, dan clustered. Fungsi harus menerima ukuran data dan random seed agar hasil dapat direproduksi.

### `src/metrics.py`

Berisi fungsi pengukuran waktu, jumlah iterasi, perbandingan, dan memori.

### `src/validation.py`

Memastikan Binary Search dan Interpolation Search menghasilkan jawaban yang benar pada target yang sama.

### `experiments/`

Berisi konfigurasi dan skrip untuk menjalankan eksperimen. Konfigurasi sebaiknya menyimpan ukuran data, jumlah pengulangan, seed, distribusi, dan skenario target.

### `results/`

Berisi hasil eksperimen. Dataset besar dan hasil mentah berukuran besar sebaiknya tidak langsung dimasukkan ke GitHub tanpa pertimbangan ukuran file.

### `docs/`

Berisi dokumentasi penelitian, tabel bedah jurnal, metodologi, keputusan eksperimen, dan catatan perubahan protokol.

## Instalasi Awal

```bash
git clone https://github.com/<username>/paper-interpolation-vs-binary-search.git
cd paper-interpolation-vs-binary-search

python -m venv .venv

# Linux/macOS
source .venv/bin/activate

# Windows PowerShell
# .venv\\Scripts\\Activate.ps1

pip install -r requirements.txt
```

## Dependensi Awal

Dependensi minimum yang direncanakan:

```text
numpy
pandas
scipy
matplotlib
seaborn
pyyaml
psutil
pytest
```

Versi dependensi perlu dikunci setelah lingkungan eksperimen ditetapkan.

## Rencana Menjalankan Eksperimen

Contoh antarmuka yang direncanakan:

```bash
python -m experiments.run_benchmark \
  --config experiments/configs/default.yaml
```

Contoh keluaran:

```text
results/raw/benchmark_results.csv
results/tables/summary_by_distribution.csv
results/figures/execution_time_by_size.png
results/figures/iterations_by_distribution.png
```

Perintah dan nama file tersebut masih dapat berubah ketika implementasi dimulai.

## Pengujian Kebenaran Algoritma

Sebelum benchmarking, jalankan pengujian unit:

```bash
pytest -q
```

Pengujian minimum harus mencakup:

- target ditemukan di awal;
- target ditemukan di tengah;
- target ditemukan di akhir;
- target tidak ditemukan;
- dataset kosong;
- dataset berisi satu elemen;
- dataset dengan ukuran besar;
- hasil kedua algoritma konsisten.

## Analisis Hasil

Analisis hasil akan menjawab beberapa pertanyaan berikut:

- Apakah Interpolation Search lebih cepat pada distribusi uniform?
- Apakah Binary Search lebih stabil pada distribusi normal, eksponensial, dan clustered?
- Pada ukuran data berapa perbedaan kinerja mulai terlihat?
- Apakah hasil jumlah iterasi mendukung hasil waktu eksekusi?
- Apakah perbedaan yang terlihat signifikan secara statistik?
- Apakah hasil empiris sesuai dengan kompleksitas teoretis masing-masing algoritma?

## Referensi Utama yang Akan Dibedah

Tiga artikel berikut menjadi referensi awal yang paling dekat dengan penelitian ini. Metadata perlu tetap diperiksa kembali melalui laman jurnal, Google Scholar, dan Garuda sebelum dimasukkan ke naskah final.

1. Ariza, S. F., & Majid, A. (2025). **Studi Perbandingan Algoritma Pencarian Binary, Jump, Interpolation, dan Fibonacci: Efisiensi Memori dan Waktu Eksekusi**. *JATI (Jurnal Mahasiswa Teknik Informatika), 9*(4). https://doi.org/10.36040/jati.v9i4.14360

2. Yasmin, N. N., Sofia, L., Sabrina, A. R. P., Putri, A. A.-Z., & Pujiono, I. P. (2025). **Interpolation Searching Algorithm Vs Algoritma Pencarian Tradisional: Analisis Efisiensi Memori dan Waktu Komputasi**. *Simkom, 10*(2), 212–223. https://doi.org/10.51717/simkom.v10i2.857

3. Purnama, N. (2025). **Comparative Performance Study of Search Algorithms on Large-Scale Data Structures**. *JITK (Jurnal Ilmu Pengetahuan dan Teknologi Komputer), 11*(1). https://doi.org/10.33480/jitk.v11i1.6592

### Referensi Pendukung Indonesia

Referensi berikut digunakan sebagai pendukung pembahasan penerapan dan pengukuran algoritma pencarian. Detail bibliografisnya perlu dilengkapi dan diverifikasi sebelum digunakan dalam artikel:

- **Analisis Perbandingan Penggunaan Algoritma Sequential Search dan Binary Search pada Aplikasi Surat Perjalanan Dinas**. JATI. https://ejournal.itn.ac.id/jati/article/view/4569
- **Perbandingan Algoritma Binary Search dan Sequential Search untuk Pencarian Persediaan Stok Barang Berbasis Web**. STRING. https://www.journal.lppmunindra.ac.id/index.php/STRING/article/view/16475
- Imamah, N., & Bahari, M. I. (2021). **Perbandingan Algoritma Sequential Search dan Algoritma Binary Search pada Aplikasi Kamus Bahasa Indonesia Menggunakan PHP dan jQuery**. *Jurnal Informatika COMPUTING, 8*(1). http://download.garuda.kemdikbud.go.id/article.php?article=3297556&val=28843
- **Implementasi dan Analisis Algoritma Binary Search**. *Multidisciplinary Indonesian Journal*. https://urj.uin-malang.ac.id/index.php/mij/article/view/14003
- **Interpolation Extrapolation Search: An Optimized Hybrid Algorithm for Data Retrieval in Management Applications**. *Teknika*. https://ejournal.ikado.ac.id/index.php/teknika/article/download/1289/446/6864

### Referensi Teoretis Tambahan

Referensi internasional berikut digunakan untuk memperkuat landasan teori, bukan sebagai pengganti referensi jurnal Indonesia:

- Perl, Y., Itai, A., & Avni, M. (1978). **Interpolation Search—A Log Log N Search**. *Communications of the ACM, 21*(7), 550–553. https://doi.org/10.1145/359545.359557
- Mohammed, A. S., Amrahov, Ş. E., & Çelebi, F. V. (2021). **Interpolated Binary Search: An Efficient Hybrid Search Algorithm on Ordered Datasets**. *Engineering Science and Technology, an International Journal, 24*(5), 1072–1079. https://doi.org/10.1016/j.jestch.2021.02.009
- Lin, J.-L. (2024). **Interpolation Once Binary Search over a Sorted List**. *Mathematics, 12*(9), 1394. https://doi.org/10.3390/math12091394

## Status Proyek

- [x] Menentukan nama repository
- [x] Menentukan judul sementara
- [x] Menyusun rumusan masalah awal
- [x] Menentukan tiga artikel utama untuk dibedah
- [ ] Memverifikasi metadata dan status indeks setiap referensi
- [ ] Menyusun tabel literature review
- [ ] Mendapatkan persetujuan dosen terhadap judul dan ruang lingkup
- [ ] Menetapkan protokol eksperimen
- [ ] Mengimplementasikan Binary Search
- [ ] Mengimplementasikan Interpolation Search
- [ ] Membuat generator dataset
- [ ] Menjalankan uji kebenaran
- [ ] Menjalankan benchmark
- [ ] Menganalisis hasil
- [ ] Menulis artikel jurnal

## Catatan Etika dan Reproduksibilitas

Repository ini digunakan untuk penelitian dan dokumentasi eksperimen. Hasil benchmark tidak boleh dimanipulasi untuk mendukung algoritma tertentu. Semua perubahan protokol, keterbatasan perangkat, kegagalan eksperimen, dan hasil yang tidak sesuai hipotesis perlu dicatat di `docs/research-log.md`.

## Lisensi

Lisensi belum ditetapkan. Pilihan yang dapat dipertimbangkan adalah MIT untuk kode eksperimen, sedangkan naskah dan data dapat diberi ketentuan terpisah sesuai kesepakatan dengan dosen pembimbing.
