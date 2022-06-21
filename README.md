# Dokumentasi Proyek Visualisasi Data dan Informasi
Berisi penjelasan dataset dan preprocessing, serta implementasi visualisasi data interaktif.
Hasil visualisasi data interaktif dapat diakses melalui link 
https://public.tableau.com/views/ProfilStatistikKesehatan2021/Story?:language=en-US&:display_count=n&:origin=viz_share_link

## Pengumpulan dan preprocessing data
Data bersumber dari Profil Statistik Kesehatan 2021 oleh Badan Pusat Statistik (BPS) serta data shp provinsi Indonesia. 
Data yang digunakan antara lain:
1.	Persentase Penduduk yang Mempunyai Keluhan Kesehatan dalam Sebulan Terakhir Menurut Provinsi, serta Menurut Kelompok Umur
2.	Persentase Penduduk yang Mempunyai Keluhan Kesehatan dalam Sebulan Terakhir dan Mengakibatkan Terganggunya Kegiatan Sehari-hari Menurut Provinsi, serta Menurut Kelompok Umur
3.	Persentase Penduduk yang Mempunyai Keluhan Kesehatan dan Pernah Mengobati Sendiri dalam Sebulan Terakhir Menurut Provinsi, serta Menurut Kelompok Umur
4.	Persentase Penduduk yang Mempunyai Keluhan Kesehatan dan Pernah Rawat Jalan dalam Sebulan Terakhir Menurut Provinsi, serta Menurut Kelompok Umur
5.	Persentase Penduduk yang Pernah Rawat Inap dalam Setahun Terakhir Menurut Provinsi, serta Menurut Kelompok Umur
6.	Persentase Penduduk Berumur Lima Tahun ke Atas yang Merokok selama Sebulan Terakhir Menurut Provinsi, serta Menurut Kelompok Umur
7.	Persentase Penduduk yang Pernah Melakukan Test COVID-19 Menurut Provinsi dan Jenis Test, serta Menurut Kelompok Umur dan Jenis Test
8.	Persentase Penduduk yang Memiliki Jaminan Kesehatan Menurut Provinsi, serta Kelompok Umur

Setelah data dikumpulkan, kemudian data digabungkan ke dalam bentuk excel. Data dibuat ke dalam dua tabel excel, yaitu berdasarkan provinsi dan kelompok umur. Data diatur dan disusun sedemikian rupa sehingga dapat dibaca oleh perangkat lunak Tableau dan dibuat visualisasinya. Data terdiri dari 6 kolom, yaitu Provinsi/Kelompok Umur, Persentase Penduduk, Tahun, Informasi, dan Kategori. Data menurut provinsi terdiri dari 816 baris, sedangkan menurut kelompok umur terdiri dari 309 baris. Untuk kolom provinsi, sesuaikan isinya dengan provinsi pada data shp provinsi Indonesia. Berikut contoh data yang sudah dilakukan preprocessing.

![image](https://user-images.githubusercontent.com/107906299/174718654-8301f03a-9d1f-4f32-add2-e7f9961b0c4b.png)

## Implementasi visualisasi data interaktif
Tahap pertama yang harus dilakukan adalah menghubungkan Tableau dengan data excel dan data shp. Buat _relationship_ antar kolom provinsi pada data shp dengan data excel Menurut Provinsi. Kemudian buat _relationship_ antar kolom Informasi, Kategori, dan Tahun pada data excel Menurut Provinsi dengan data excel Menurut Kelompok Umur.
![image](https://user-images.githubusercontent.com/107906299/174726454-82123886-7baf-4749-8dbc-227f64e6f38d.png)


### Choropleth map untuk data menurut provinsi
1.  Buat sheet baru, dan ubah nama sheet-nya menjadi ProvMap.
2.  Isi Columns dengan "Longitude" dan Rows dengan "Latitude".
3.  Pada bagian Marks, masukkan "Geometry" ke Detail. Kemudian tambahkan pula "Provinsi (Provinsi)", "Informasi", "Kategori", dan "Tahun".
4.  Pastikan Pada Marks sudah terpilih Map.
5.  Setelah itu, tambahkan "Persentase Penduduk" pada bagian Color untuk menambahkan warna pada setiap provinsi berdasarkan persentasenya. Ubah menjadi _Continuous_. 
6.  Klik kanan, kemudian pilih _Legends_ untuk menambahkan legends pada visualisasi.
7.  Pilih _Show Filter_ pada "Informasi", "Kategori", dan "Tahun" di bagian Marks untuk menambahkan filter.
8.  _Create Calculated Field_, kemudian beri nama "Rank" dan isi RANK(SUM([Persentase Penduduk])). Klik OK. 
9.  Masukkan field "Rank" ke Detail di Marks.
10.  Karena data menurut provinsi akan dibuat dalam bentuk _choropleth map_ dan _bar chart_, buat parameter baru dengan memilih Create Parameter. Beri nama "Chart type", kemudian ubah _Data type: String_. Pada _List of values_, isikan Value "Map" dan "Bar Chart".
11.  Pada parameter "Chart type", klik Show Parameter, kemudian pilih "Map".
12.  _Create Calculated Field_, kemudian diisi [Chart type]. 
13.  Tambahkan field "Chart type" ke dalam Filters. Pilih Pada _Edit filter_, pilih "Map".
14.  Pada Filter, klik tanda segitiga terbalik pada "Informasi", kemudian pilih _Apply to Worksheets_ dan klik _All Using Related Data Source_. Ulangi pada "Kategori" dan "Tahun".
15.  Pada kumpulan filter di sebelah kanan chart, ubah menjadi _Single Value (dropdown)_, kemudian pilih _Customize_ dan hilangkan ceklis pada _Show "All" Value_.
16.  Edit isi Tooltip sesuai dengan yang ingin ditampilkan ketika kursor menyorot salah satu provinsi.

![image](https://user-images.githubusercontent.com/107906299/174727363-0a9a976b-72c1-4f78-9a40-92eb30f7ca01.png)


### Bar chart untuk data menurut provinsi
1.  Buat sheet baru, dan ubah nama sheet-nya menjadi ProvBarChart.
2.  Isi Columns dengan "Provinsi (Provinsi)" dan Rows dengan "Persentase Penduduk". Pada "Persentase Penduduk", ubah menjadi _Attribute_.
3.  Untuk mengurutkan bar, klik segitiga bawah pada "Provinsi (Provinsi)" di Columns, kemudian klik _Sort_. Isikan _Sort_ By dengan Field, pilih _Field Name_ "Persentase Penduduk", dan _Sort Order Descending_.
4.  Pada bagian Marks, masukkan, "Informasi", "Kategori", "Tahun", dan "Rank" ke Detail.
5.  Pastikan pada Marks sudah terpilih Bar.
6.  Setelah itu, tambahkan "Persentase Penduduk" pada bagian Color untuk menambahkan warna pada setiap bar berdasarkan persentasenya. Ubah menjadi _Continuous_.
7.  Klik kanan, kemudian pilih _Legends_ untuk menambahkan legends pada visualisasi.
8.  Pada parameter "Chart type", klik Show Parameter, kemudian pilih "Bar Chart".
9.  Tambahkan field "Chart type" ke dalam Filters. Pada _Edit filter_, pilih "Bar Chart".
10.  Edit isi Tooltip sesuai dengan yang ingin ditampilkan ketika kursor menyorot salah satu bar.

![image](https://user-images.githubusercontent.com/107906299/174726321-275f1e07-c97a-4e3c-9267-8e21765c5ee6.png)


### Bar chart untuk data menurut kelompok umur
1.  Buat sheet baru, dan ubah nama sheet-nya menjadi UmurBarChart.
2.  Isi Columns dengan "Persentase Penduduk (Usia)" dan Rows dengan "Kelompok Umur".
3.  Pada bagian Marks, masukkan, "Informasi", "Kategori", dan "Tahun" ke Detail.
4.  Pastikan pada Marks sudah terpilih Bar.
5.  _Create Calculated Field_, kemudian beri nama "Top 3" dan isi RANK(SUM([Persentase Penduduk (Usia)])) <=3. Klik OK. Field "Top 3" ini menunjukkan tiga teratas kelompok umur yang memiliki persentase penduduk tertinggi.
6.  Tambahkan "Top 3" ke Color pada Marks. Ubah warna sesuai yang diinginkan.
7.  Edit isi Tooltip sesuai dengan yang ingin ditampilkan ketika kursor menyorot salah satu bar.

![image](https://user-images.githubusercontent.com/107906299/174727303-bbdcc7a6-da06-4c1e-a11d-8d73f9feefd0.png)


### Legend
Ketika ingin menggabungkan visualisasi data menurut provinsi, akan terbentuk dua legends, yaitu dari sheets ProvMap dan ProvBarChart. Jika dipilih salah satu chart type, legend dari chart type yang tidak terpilih akan menjadi null. Hal ini mengganggu tampilan visualisasi. Oleh karena itu, dibuat sheet baru untuk membuat legends.
1.  Buat sheet baru, dan ubah nama sheet-nya menjadi Legend.
2.  Masukkan "Persentase Penduduk" ke Color pada Marks.
3.  Pada Marks pilih Polygon.
4.  Klik kanan, kemudian pilih _Legends_ untuk menambahkan legend Persentase.

### Dashboard
Untuk memudahkan pengguna agar dapat melihat visualisasi data menurut provinsi dan kelompok umur sekaligus, visualisasi data yang sudah terbentuk akan digabung ke dalam satu layar, yaitu Dashboard. Fitur-fitur interaktif masih dapat digunakan pada Dashboard ini. 
1.  Buat dashboard baru.
2.  Bagi dua layar secara vertikal, kemudian pada bagian atas dibagi dua secara horizontal.
3.  Pada Sheets, tarik sheet UmurBarChart ke kotak kiri atas.
4.  Pindahkan filter Informasi, Kategori, dan Tahun ke kotak kanan atas. Hapus legend Top 3.
5.  Sesuaikan ukuran chart agar terlihat lebih besar.
6.  Tarik sheet ProvMap ke bawah chart Kelompok Umur.
7.  Setelah itu, tarik sheet ProvBarChart ke bawah choropleth map. Klik kanan dan pilih Hide Title.
8.  Hapus legend Persentase. 
9.  Tarik sheet Legend ke bawah filter Tahun, kemudian pilih Hide Title dan Floating. Atur ukurannya menjadi sekecil mungkin. Pindahkan ke pojok kanan bawah.
10.  Atur urutan filter dan legend pada kolom sebelah kanan yang berisi filter dan legend.
11.  Pada filter Chart type, hapus ceklis Show Title. Ubah menjadi Single Value List kemudian pilih Floating. Pindahkan ke dalam chart Provinsi.
12.  Pada kolom sebelah kanan, klik kanan kemudian pilih Distribute Contents Evenly.

![image](https://user-images.githubusercontent.com/107906299/174732559-af21e37d-8b71-4f85-bc17-d70d7f98d145.png)


### Story
Di Tableau terdapat story/cerita, yaitu urutan visualisasi dari kumpulan sheets dan dashboard untuk menyampaikan informasi dan menjelaskan data secara lebih detail. Pada proyek ini, story dimanfaatkan untuk menambah catatan agar lebih memudahkan pengguna dalam menggunakan visualisasi data interaktif yang sudah dibuat. 
1.  Buat Story baru.
2.  Tarik Dashboard yang sudah dibuat sebelumnya ke dalam Story.
3.  Ceklis Show title dan isi judulnya.
4.  Tarik Drag to add text dan isi catatan yang ingin ditampilkan.

![image](https://user-images.githubusercontent.com/107906299/174733243-425201ea-2610-4e32-8987-68eae919edf7.png)
