Tugas 1: Scraping Daftar Berita dari Portal Berita
Latar Belakang Pemilihan Portal Berita

Saya memilih dua portal berita populer, cnnindonesia.com dan tempo.co, untuk tugas ini dengan beberapa pertimbangan strategis:

Struktur yang Mirip Namun Tetap Berbeda

Keduanya sama-sama menyajikan daftar berita dengan struktur HTML yang rapi, sehingga cocok dijadikan target scraping.

Namun, ada perbedaan penting: CNN Indonesia cenderung menekankan kategori berita pada headline, sedangkan Tempo lebih menonjolkan detail metadata seperti tanggal, ringkasan, bahkan penulis di beberapa artikelnya. Hal ini menjadi studi kasus menarik untuk menunjukkan bagaimana satu skrip dasar dapat diadaptasi ke dua situs dengan pola berbeda.

Kekayaan dan Variasi Data

CNN Indonesia menampilkan berita nasional dan internasional dengan kategori jelas (politik, ekonomi, olahraga, dsb.), meskipun metadata tambahan di halaman utama relatif terbatas.

Tempo menawarkan variasi data yang lebih kaya, termasuk ringkasan berita dan informasi tambahan pada artikel tertentu.

Menggabungkan keduanya memberi variasi data yang lebih lengkap untuk analisis.

Penjelasan Rinci Alur Kode

Kode untuk tugas ini dirancang untuk "memborong" semua daftar berita yang ada di halaman utama kedua situs tersebut. Alurnya adalah:

Persiapan Alat

requests: Untuk "mengunjungi" dan mengunduh halaman web. Saya menambahkan headers agar scraping terlihat seperti permintaan dari browser biasa.

BeautifulSoup: Untuk merapikan kode HTML sehingga lebih mudah dicari elemennya.

pandas & json: Untuk menyusun semua data menjadi tabel (.csv, .xlsx) dan format JSON.

Mengunjungi Halaman & Mencari Artikel

Skrip mengakses URL target (CNN Indonesia dan Tempo).

Lalu soup.find_all('article') dipakai untuk menyisir halaman dan mengumpulkan setiap blok berita.

“Membongkar” Setiap Artikel (Adaptasi per Situs)

CNN Indonesia:

Judul: diambil dari tag <h2> atau <h3> di dalam blok artikel.

Kategori: dicari dari elemen dengan kelas seperti text-cnn_red.

Metadata lain seperti penulis dan ringkasan tidak tersedia di halaman utama, jadi diberi nilai default.

Tempo:

Judul: biasanya muncul dalam tag <h2> dengan kelas tertentu.

Metadata: Tempo relatif lebih lengkap, misalnya menampilkan tanggal publikasi dan ringkasan singkat di halaman utama. Informasi ini bisa diambil dengan selector khusus (misalnya <span class="date"> atau <p class="excerpt">).

Mengumpulkan dan Mengekspor Hasil

Setiap artikel yang berhasil diproses dimasukkan ke dalam dictionary.

Semua dictionary kemudian dikumpulkan ke dalam list collected_data.

Data diekspor menjadi .json, .csv, dan .xlsx agar mudah digunakan di tahap analisis selanjutnya.
