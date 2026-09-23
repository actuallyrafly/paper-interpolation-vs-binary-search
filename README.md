# Paper: Interpolation Search vs Binary Search

Eksperimen terkontrol untuk menganalisis kinerja **Interpolation Search** dan **Binary Search** pada data numerik terurut dengan variasi distribusi dan ukuran data.

> Repository: `paper-interpolation-vs-binary-search`
>

## Tujuan Penelitian

Penelitian ini bertujuan membandingkan kinerja Interpolation Search dan Binary Search berdasarkan karakteristik data, khususnya:

- distribusi nilai data;
- ukuran dataset;
- waktu eksekusi;
- jumlah iterasi/perbandingan; dan
- penggunaan memori sebagai metrik tambahan.

Penelitian ini tidak hanya menanyakan algoritma mana yang lebih cepat, tetapi juga **pada kondisi apa** masing-masing algoritma lebih sesuai digunakan.

## Rumusan Masalah

1. Bagaimana perbandingan kinerja Interpolation Search dan Binary Search berdasarkan waktu eksekusi, jumlah iterasi, dan penggunaan memori pada berbagai distribusi data numerik?
2. Bagaimana pengaruh ukuran data terhadap kinerja kedua algoritma pada distribusi uniform, normal, eksponensial, dan clustered?
3. Pada distribusi dan ukuran data seperti apa Interpolation Search memiliki kinerja lebih baik, setara, atau lebih rendah dibandingkan Binary Search?
4. Apakah perbedaan kinerja antara kedua algoritma menunjukkan perbedaan yang signifikan secara statistik?

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
- `10^7` sebagai target jika perangkat bisa

## Referensi Utama

1. Ariza, S. F., & Majid, A. (2025). **Studi Perbandingan Algoritma Pencarian Binary, Jump, Interpolation, dan Fibonacci: Efisiensi Memori dan Waktu Eksekusi**. *JATI (Jurnal Mahasiswa Teknik Informatika), 9*(4). https://doi.org/10.36040/jati.v9i4.14360

2. Yasmin, N. N., Sofia, L., Sabrina, A. R. P., Putri, A. A.-Z., & Pujiono, I. P. (2025). **Interpolation Searching Algorithm Vs Algoritma Pencarian Tradisional: Analisis Efisiensi Memori dan Waktu Komputasi**. *Simkom, 10*(2), 212–223. https://doi.org/10.51717/simkom.v10i2.857

3. Purnama, N. (2025). **Comparative Performance Study of Search Algorithms on Large-Scale Data Structures**. *JITK (Jurnal Ilmu Pengetahuan dan Teknologi Komputer), 11*(1). https://doi.org/10.33480/jitk.v11i1.6592

### Referensi Pendukung Indonesia

- **Analisis Perbandingan Penggunaan Algoritma Sequential Search dan Binary Search pada Aplikasi Surat Perjalanan Dinas**. JATI. https://ejournal.itn.ac.id/jati/article/view/4569
- **Perbandingan Algoritma Binary Search dan Sequential Search untuk Pencarian Persediaan Stok Barang Berbasis Web**. STRING. https://www.journal.lppmunindra.ac.id/index.php/STRING/article/view/16475
- Imamah, N., & Bahari, M. I. (2021). **Perbandingan Algoritma Sequential Search dan Algoritma Binary Search pada Aplikasi Kamus Bahasa Indonesia Menggunakan PHP dan jQuery**. *Jurnal Informatika COMPUTING, 8*(1). http://download.garuda.kemdikbud.go.id/article.php?article=3297556&val=28843
- **Implementasi dan Analisis Algoritma Binary Search**. *Multidisciplinary Indonesian Journal*. https://urj.uin-malang.ac.id/index.php/mij/article/view/14003
- **Interpolation Extrapolation Search: An Optimized Hybrid Algorithm for Data Retrieval in Management Applications**. *Teknika*. https://ejournal.ikado.ac.id/index.php/teknika/article/download/1289/446/6864

### Referensi Tambahan

Referensi internasional berikut digunakan untuk memperkuat landasan teori, bukan sebagai pengganti referensi jurnal Indonesia:

- Perl, Y., Itai, A., & Avni, M. (1978). **Interpolation Search—A Log Log N Search**. *Communications of the ACM, 21*(7), 550–553. https://doi.org/10.1145/359545.359557
- Mohammed, A. S., Amrahov, Ş. E., & Çelebi, F. V. (2021). **Interpolated Binary Search: An Efficient Hybrid Search Algorithm on Ordered Datasets**. *Engineering Science and Technology, an International Journal, 24*(5), 1072–1079. https://doi.org/10.1016/j.jestch.2021.02.009
- Lin, J.-L. (2024). **Interpolation Once Binary Search over a Sorted List**. *Mathematics, 12*(9), 1394. https://doi.org/10.3390/math12091394



## Catatan dan Reproduksibilitas

Semua perubahan protokol, keterbatasan perangkat, kegagalan eksperimen, dan hasil yang tidak sesuai hipotesis perlu dicatat di `docs/research-log.md`.
