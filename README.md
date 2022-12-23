# Project11
## Langkah - Langkah Georeferencing Topo Sheets And Scanned Maps

1. Buka QGIS dan klik Raster ‣ Georeferencer untuk membuka alat.

2. Georeferensi dibagi menjadi 2 bagian. Bagian atas tempat gambar akan ditampilkan dan bagian bawah tempat tabel yang menunjukkan GCP Anda akan muncul.

3. Sekarang kita akan membuka gambar JPG kita. Buka File ‣ Buka Raster. Telusuri ke gambar yang diunduh dari peta yang dipindai dan klik Buka.

4. Anda akan melihat gambar akan dimuat di bagian atas. Anda dapat menggunakan kontrol zoom/pan pada bilah alat untuk mempelajari lebih lanjut tentang peta.

5. Sekarang kita perlu menetapkan koordinat ke beberapa titik di peta ini. Jika Anda melihat lebih dekat, Anda akan melihat kotak koordinat dengan tanda. Ini adalah garis kisi Lintang dan Bujur.

6. Sebelum menambahkan Titik Kontrol Tanah (GCP), kita perlu menentukan Pengaturan Transformasi. Klik ikon roda gigi di jendela georeferensi untuk membuka dialog pengaturan Transformasi.

7. Dalam dialog pengaturan Transformasi, pilih jenis Transformasi sebagai Polinomial 2. Lihat Dokumentasi QGIS untuk mempelajari berbagai jenis transformasi dan penggunaannya. Kemudian pilih metode Resampling sebagai Nearest Neighbor. Klik tombol Select CRS di sebelah Target SRS.

8. Jika Anda melakukan geo-referensi peta yang dipindai seperti ini, Anda dapat memperoleh informasi CRS dari peta itu sendiri. Melihat gambar peta kita, koordinatnya ada di Lintang/Bujur. Tidak ada informasi datum yang diberikan, jadi kita harus mengasumsikan yang sesuai. Karena ini adalah India dan petanya cukup tua, kita bisa bertaruh bahwa data Everest 1830 akan memberi kita hasil yang bagus. Cari everest dan pilih CRS dengan definisi terlama dari datum Everest (EPSG:4042). Klik Oke.

==========
Note :

Survey of India Topo Sheets dibuat antara tahun 1960 dan 2000 menggunakan spheroid Everest 1956 dan datum India_nepal. Jika Anda melakukan georeferensi SOI Topo Sheets, , Anda dapat menentukan CRS Kustom di QGIS dengan parameter berikut dan menggunakannya dalam langkah ini. Definisi ini mencakup parameter delta_x, delta_y dan delta_z untuk mengubah datum ini menjadi WGS84. Lihat halaman ini untuk informasi lebih lanjut tentang Sistem Grid India.

       +proj=longlat +a=6377301.243 +b=6356100.2284 +towgs84=295,736,257,0,0,0,0 +no_defs
       
Note :

Sebagian besar peta dibuat menggunakan Proyeksi CRS. Jika peta yang Anda coba georeferensi menggunakan proyeksi CRS yang Anda ketahui, tetapi label graticules berada dalam CRS Geografis (lintang/bujur), Anda dapat menggunakan alur kerja alternatif untuk meminimalkan distorsi. Alih-alih menggunakan CRS Geografis seperti yang kami gunakan di sini, Anda dapat membuat kisi vektor di QGIS dan mengubahnya menjadi CRS yang diproyeksikan untuk digunakan sebagai referensi pengambilan koordinat yang akurat. Lihat halaman ini untuk detail lebih lanjut.

==========

9. Beri nama raster keluaran Anda sebagai 1870_southern_india_modified.tif. Pilih LZW sebagai Kompresi. Periksa Simpan poin GCP untuk menyimpan poin sebagai file terpisah untuk tujuan di masa mendatang. Pastikan opsi Muat di QGIS saat selesai dicentang. Klik Oke.

==========
Note :

File GeoTIFF yang tidak terkompresi bisa berukuran sangat besar. Jadi mengompresi mereka selalu merupakan ide yang bagus. Anda dapat mempelajari lebih lanjut tentang berbagai opsi kompresi TIFF (LZW, PACKBITS, atau DEFLATE) di artikel ini.

10. Sekarang kita dapat mulai menambahkan Ground Control Points (GCP). Klik pada tombol Tambah Titik.

11. Sekarang tempatkan cross-hair di persimpangan garis grid dan klik kiri, ini akan berfungsi sebagai ground-truth dalam kasus kita. Saat garis kisi diberi label, kita dapat menentukan koordinat X dan Y dari titik-titik tersebut. Di jendela pop-up, masukkan koordinat. Ingat bahwa X = bujur dan Y = lintang. Klik Oke.

12. Anda akan melihat tabel GCP sekarang memiliki baris dengan detail GCP pertama Anda.

13. Demikian pula, tambahkan lebih banyak GCP yang mencakup seluruh gambar. Semakin banyak poin yang Anda miliki, semakin akurat gambar Anda didaftarkan ke koordinat target. Transformasi Polinomial 2 membutuhkan setidaknya 6 GCP. Setelah Anda menambahkan jumlah poin minimum yang diperlukan untuk transformasi, Anda akan melihat bahwa GCP sekarang memiliki nilai kesalahan dX, dY, dan Residual bukan nol. Jika GCP tertentu memiliki nilai error yang luar biasa tinggi, hal itu biasanya berarti kesalahan manusia dalam memasukkan nilai koordinat. Jadi, Anda dapat menghapus GCP itu dan menangkapnya lagi. Anda juga dapat mengedit nilai koordinat di Tabel GCP dengan mengeklik sel di salah satu Tujuan. X atau Des. kolom Y.

14. Setelah Anda puas dengan GCP, klik tombol Mulai Georeferensi. Ini akan memulai proses membengkokkan gambar menggunakan GCP dan membuat raster target.

15. Setelah proses selesai, Anda akan melihat lapisan georeferensi dimuat di QGIS. Georeferensi sekarang selesai. Juga, Anda akan melihat Project CRS di kanan bawah diatur ke EPSG:4042 seperti yang dijelaskan di Pengaturan Transformasi.

16. Seret dan jatuhkan OpenStreetMap sebagai Peta Dasar dari tarik-turun Ubin XYZ di bagian bawah panel Peramban untuk memverifikasi lapisan georeferensi. Untuk menyetel transparansi, klik ikon Open layer styling panel dan pilih tab Transparency. Atur transparansi menjadi 40%. Sekarang gambar georeferensi harus dilapisi dengan garis peta dasar.

17. Jika georeferensi membutuhkan lebih banyak penyesuaian, kita dapat mulai dari poin GCP yang terkumpul. Jelajahi lokasi file 1870_southern_india_modified.tif. Anda dapat menemukan file tambahan,1870_southern_india_modified.tif.points. File ini akan berisi informasi poin GCP.

18. Buka alat georeferensi di QGIS, klik File ‣ Load GCP Points, dan pilih 1870_southern_india_modified.tif.points. Ini akan memuat GCP yang dibuat sebelumnya. Kemudian muat 1870_southern_india_modified.tif untuk menyempurnakan pekerjaan Anda.


