> Web Mining 2019 / Weni Pratiwi S (160411100013)

Penambangan dan pencarian web atau *web mining* merupakan proses ektraksi pola dari data-data pada suatu website. Terdiri dari 3 bagian yaitu :

1. **Web content mining**

   Web content mining adalah proses ekstraksi pola/informasi dari dokumen atau data. Cara kerjanya adalah dengan cara mengekstraksi *key word* dari data, bisa berupa teks, citra, audio, video, metadata dan hyperlink.

2. **Web structure mining**

   Web structure mining (log mining) digunakan untuk menemukan struktur link dari suatu website, yang nantinya akan membentuk suatu rangkuman dari bangunan website.

3. **Web usage mining**

   Web usage mining adalah proses pengambilan informasi perilaku user dari log, click stream, query dan cookies.

   

Untuk mendapatkan informasi dari web kita perlu melakukan *crawl* yaitu membaca semua halaman dan membuat index dari data yang dicari, dengam menggunakan *Web Crawler*.

Web crawler merupakan serangkaian script pemrograman yang digunakan untuk melakukan crawl secara otomatis, dan menyimpan data yang diperoleh untuk selanjutnya diolah untuk mendapatkan informasi yang diinginkan.

#### Requirement :

- Python
- BeatifulSoup4
- SQLite3
- Numpy
- Scipy
- Sastrawi
- Sckit-learn
- Sckit-fuzzy
- Math
- Database KBI
- import CSV

Website : "https://www.dicoding.com/events?q=&criteria=&sort=&sort_direction=desc&page=1"

> Install requirement menggunakan pip di command prompt, atau download Anaconda. Library Anaconda sudah lengkap, anda bisa langsung menggunakan library yang anda butuhkan untuk bahasa python.