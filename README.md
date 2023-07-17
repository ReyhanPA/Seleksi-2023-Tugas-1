# ANALISIS OBJEK WISATA DI SUMATRA BARAT
---

## A. Latar Belakang
Pembuatan analisis ini dilakukan untuk pemenuhan tugas seleksi asisten laboratorium basis data tahun 2023 Institut Teknologi Bandung. Adapun pemilihan topik objek wisata di sumatra barat ini karena penulis merupakan mahasiswa ITB yang berasal dari Sumatra Barat. Selain itu, pemilihan objek wisata sebagai data karena penulis merasa Sumatra Barat memiliki potensi yang besar dalam pengembangan objek wisata. Saat ini, objek wisata Sumatra Barat mulai dipandang oleh masyarakat di luar Sumatra Barat sebagai salah satu destinasi pariwisata yang diperhitungkan. Jadi, tak jarang wisatawan terkadang bingung dalam memilih daerah dan objek wisata mana yang sebaiknya dikunjungi terlebih dahulu. Hasil analisis ini nantinya berguna bagi calon pengunjung, apalagi bagi pengunjung yang memiliki *budget* terbatas, tapi tetap ingin menikmati wisata di daerah minangkabau ini.

## B. Alur Perancangan dan Pembuatan
Pada pembuatant tugas ini, setelah menentukan topik yang akan dijadikan sebagai data, penulis selanjutnya melakukan eksplorasi menyeluruh tentang website penyedia informasi mengenai objek wisata di Sumatra Barat pada laman [web tripadvisor](https://www.tripadvisor.co.id/Attractions-g2301784-Activities-West_Sumatra_Sumatra.html) berikut. Selama eksplorasi, penulis melakukan pemindaian informasi dan mencatat poin-poin apa saja yang sekiranya bisa dijadikan data dalam tugas analisis ini. Setelah mengetahui data yang dapat diambil, selanjutnya penulis membuat gambaran desain *ER diagram* dan relational *diagram* agar mendapat gambaran tabel-tabel seperti apa yang nantinya dapat dibuat. Pembuatan diagram ini bersifat sementara sebagai gambaran awal saja, karena nantinya di tengah jalan akan ada beberapa modifikasi yang dilakukan terhadap diagram yang telah dibuat. Setelah selesai, selanjutnya penulis melakukan persiapan dengan menyiapkan *tools* yang sekiranya dapat digunakan. Dalam hal ini, penulis menggunakan bahasa pemrograman python dengan library beautifulsoup untuk melakukan *scraping* data, draw.io untuk pembuatan desain, serta postgreSQL sebagai DBMS untuk penyimpanan data. Setelah melakukan persiapan, barulah penulis melakukan proses untuk mendapatkan hasil yang diminta dengan melakukan *data scraping* dan *data storing*.

## C. Deskripsi Data dan Pemilihan DBMS
Data yang penulis ambil terdiri dari data peringkat, nama objek, nama daerah, rata-rata *rating*, *rating* bintang 1, *rating* bintang 2, *rating* bintang 3, *rating* bintang 4, *rating* bintang 5, jumlah ulasan, jumlah objek sedaerah, nama jenis, nama akun pengunjung, asal pengunjung, *rating* pengunjung, waktu berkunjung, dan tipe kunjungan yang semua data tersebut terbagi menjadi 4 tabel pada diagram relasional. Selain itu, untuk membuat relasi objek wisata Sumatra Barat ini lebih akurat, penulis menambahkan tabel pengelola dan operasional sebagai tabel tambahan. Untuk lebih lengkapnya mengenai *ER diagram* dan *relational diagram* dari objek wisata Sumatra Barat ini dapat dilihat pada gambar [ER diagram](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/blob/main/Data%20Storing/design/ER%20Diagram.png) dan [relational diagram](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/blob/main/Data%20Storing/design/Relational%20Diagram.png) berikut. DBMS yang digunakan dalam tugas ini adalah postgreSQL. Penulis memilih DBMS ini karena dirasa cukup mudah digunakan dan fiturnya sangat *powerfull* dalam penyimpanan data. Selain itu, postgreSQL ini dilengkapi dengan UI yang cukup *friendly* sehingga dapat dengan lebih mudah membaca isi *database*.

## D. Spesifikasi Program
Secara umum, program dalam *data scraping* dan *data storing* dapat dilihat pada folder dengan nama yang sama. Untuk *data scraping*, terdiri dari tiga folder, yaitu **data** (tempat penyimpanan data JSON), ***screenshot*** (tempat penyimpanan SS hasil penjalanan program), dan **src** (tempat penyimpanan *source code* dalam *scraping*). Untuk *data storing*, terdapat folder ***design*** (tempat penyimpanan ERD dan diagram relasional), ***eksport*** (tempat penyimpanan file SQL database), dan ***screenshot*** (tempat penyimpanan SS bukti penyimpanan data ke dalam DBMS).

## E. Cara Penggunaan
1. Simpan file SQL [file SQL objek_wisata_sumbar](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Storing/export) ke penyimpanan lokal dan buka melalui CMD atau *command prompt* yang kalian pakai.
2. Buat *database* terlebih dahulu, kemudian lakukan import file SQL dengan mengetik `psql -U {username} -d {database} < objek_wisata_sumbar.sql`.
3. Setelah berhasil, silakan masuk ke akun postgreSQL dan file SQL objek_wisata_sumbar siap digunakan.

## F. Struktur JSON
Struktur JSON yang penulis buat cukup sederhana, setiap file JSON yang terdapat pada [data](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Scraping/data) masing-masingnya mengimplementasikan tabel-tabel yang terdapat pada diagram relasional yang akan dijelaskan pada poin berikutnya. Sebenarnya bisa saja dibuat menjadi satu buah file JSON, tapi penulis membuatnya terpisah untuk kemudahan dalam penyimpanan ke DBMS nya.

**Catatan**: Pada folder data tersebut juga terdapat *file* dengan format CSV karena penulis terkendala dalam penyimpanan file JSON ke DBMS postgreSQL (PgAdmin4), oleh karena itu, penulis mengsiasatinya dengan mengonversi hasil *scraping* ke bentuk JSON dan CSV di mana format CSV ditujukan untuk penyimpanan di DBMS.

## G. Struktur *Database*
Seperti yang dijelaskan pada poin di awal, ER *diagram* dan *relational diagram* yang terdapat pada [ER diagram](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/blob/main/Data%20Storing/design/ER%20Diagram.png) dan [relational diagram](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/blob/main/Data%20Storing/design/Relational%20Diagram.png) merupakan langkah awal yang dilakukan penulis. Untuk ER diagram, terdapat relasi ***one-to-many*** pada tabel daerah dan objek_wisata, hal ini karena 1 daerah bisa memiliki banyak objek wisata, sedangkan 1 objek wisata hanya akan terdapat pada 1 daerah saja. Lalu pada relasi ini pula bersifat parsial pada daerah karena ada beberapa daerah pada tabel daerah yang tidak memiliki objek wisata yang disebabkan oleh *cleaning data* yang dilakukan saat proses *scraping data*, kemudian bersifat total pada objek wisata karena dipastikan semua objek wisata memiliki pasangan daerah di tabel daerah. Untuk pengelola dan objek wisata, terdapat relasi ***one-to-one*** dan sama-sama total karena diasumsikan setiap objek memiliki hanya 1 pengelola dan setiap pengelola memiliki hanya 1 objek yang diurusnya. Terakhir, untuk operasional dengan objek wisata terdapat relasi ***one-to-one*** karena diasumsikan setiap objek wisata punya 1 operasional dan begitupun sebaliknya, pada relasi ini pula pada lengan kirinya hanya menggunakan partisipasi parsial karena diasumsikan terdapat objek wisata yang tidak punya operasional, maksudnya dapat dikunjungi di jam berapa saja dan hari apa saja.

**Catatan**: Tabel ulasan_teratas hanya diambil ulasan pengunjung yang teratas karena di websitenya ulasan setiap objek dibagi-bagi per halaman (sampai ratusan halaman ulasan per 1 objeknya), jadi takutnya membebani server, hal ini dilakukan untuk menjaga salah satu **etika *scraping***, yaitu melakukan *scraping* seperlunya tanpa memberatkan *website*.

## H. Translasi ER *Diagram* ke *Relational Diagram*
Secara umum, translasi ER *diagram* menjadi *relational diagram* mengikuti kaidah translasi. Ada beberapa perubahan setelah translasi, di antaranya ***one-to-many*** di daerah dan objek wisata terbentuk menjadi 2 tabel dengan *primary key* tabel daerah diselipkan pada tabel objek_wisata. Selanjutnya untuk jenis dan ulasan_teratas yang terdapat pada tabel objek_wisata memisahkan diri menjadi masing-masing tabel baru karena merupakan entitas **multivalue**. Tabel pengelola dan operasional menjadi tabel seperti biasa dengan *primary key* pada masing-masingnya diselipkan pada tabel objek_wisata.

## I. *Screenshot* Program
Berikut *screenshot* hasil *scraping* data objek wisata di Sumatra Barat:
1. [*Screenshot* daerah](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Scraping/screenshot/daerah)
2. [*Screenshot* jenis](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Scraping/screenshot/jenis)
3. [*Screenshot* objek_wisata](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Scraping/screenshot/objek_wisata)
4. [*Screenshot* ulasan_teratas](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Scraping/screenshot/ulasan_teratas)

Berikut *screenshot* hasil *storing* data objek wisata di Sumatra Barat:
1. [*Screenshot data storing*](https://github.com/ReyhanPA/Seleksi-2023-Tugas-1/tree/main/Data%20Storing/screenshot)

## J. Bonus (Visualisasi Data)


## K. Referensi
- Library yang digunakan: [dokumentasi beautifulsoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/).
- Tutorial *scraping* dengan beautifulsoup: [tutorial beutifulsoup](https://www.youtube.com/watch?v=YIiYeyfo7MM&t=2254s).
- DBMS yang digunakan: [dokumentasi postgreSQL](https://www.postgresql.org/docs/current/index.html).

## L. Catatan Tambahan
Pada proses *cleaning* data, di kebanyakan waktu penulis banyak memilih untuk menghapus data yang bolong-bolong, dalam artian memiliki nilai null di beberapa kolomnya. Namun, pada tabel ulasan_teratas, penulis menggunakan cara dengan me-*replace* kolom yang kosong tersebut dengan nilai *default* agar tidak ada data terbuang (sayang ygy).

## M. Author
|Nama|NIM|Jurusan|
|----|---|-------|
|Reyhan Putra Ananda|18221161|Sistem dan Teknologi Informasi 2021|