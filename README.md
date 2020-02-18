# BigData_Tugas1

# Dokumentasi Praktek ETL menggunakan KNIME

[Business Understanding]
[Data Understanding]
[Data Preparation]
[Modeling]
   [Proses membaca data dari dua sumber yang berbeda]
   [Proses Modeling]
[Evaluation]
[Deployment]

# Business Understanding
hal yang dapat dilakukan pada dataset tersebut: 
1. mengakumulasi data pertandingan 
2. melihat team yang paling banyak menang dalam 1 dekade
3. melihat team yang paling banyak mencetak goal dan kebobolan dalam 1 dekade
4. melihat tanggal dimainkannya pertandingan 
5. mengakumulasi suatu negara berapa kali menjadi tuan rumah

# Data Understanding

  
- dataset ini berisi statistik pertandingan sepakbola dari tahun 1872 sampai 2019

- dataset ini terdiri dari 83.080 baris dan 9 kolom
	- date			: tanggal pertandingan 
	- home-team		: tuan rumah pertandingan
	- away-team		: tamu pertandingan
	- home-score		: skor tuan rumah
	- away-score		: skor tamu
	- tournament		: penyelenggara tournament
	- city			: kota pertandingan
	- country		: negara penyelenggara pertandingan
	- neutral		: lokasi yang tidak mempunyai tuan rumah 
- Source dataset : https://www.kaggle.com/martj42/international-football-results-from-1872-to-2017/data

# Data Preparation
- Karena hanya terdiri dari 1 file csv, saya memisahkan isi data dengan node column splitter yang ada di knime.
- Pertama, saya menggunakan node file reader yang tersedia di knime<br/>
![file read](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/fileread.png "fileread")<br/>

- Kedua, klik kanan lalu buka settings dan "browse file .csv yang ingin digunakan, lalu klik ok<br/>
![filereadfind](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/filereadfind.png "filereadfind")<br/>

- Ketiga, Drag node column splitter kedalam workflow, lalu hubungkan dengan node file reader<br/>
![colsplit](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/colsplit.png "colsplit")<br/>

- Keempat, klik kanan pada node column splitter lalu buka settings.<br/>
![colsplitset](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/colsplitset.jpg "colsplitset")<br/>
  -2 hasil splitter<br/>
      ![colsplit1](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/colsplit1.jpg "colsplit1")<br/>    
      ![colsplit2](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/colsplit2.jpg "colsplit2")<br/>
 
-Kelima, simpan salah satu bagian data di database, dan satu bagian lagi di file csv dengan cara:<br/>
 -Database:
  -Gunakan MySQL Connector lalu hubungkan dan setting dengan database yang ingin dipakai<br/>
    ![sqlconn](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/sqlconn.png "sqlconn")<br/>
    ![sqlconnset](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/sqlconnset.png "sqlconnset")<br/>
  -Ambil node DB Writer, lalu hubungkan dengan MySQL Connector dan node Column splitter<br/>
    ![dbwrite](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/dbwrite.png "dbwrite")<br/>
  -Konfigurasi node DB Writer lalu klik ok <br/>
    ![dbwriteset](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/dbwriteset.jpg "dbwriteset")<br/>
  -Tabel baru sudah ada di phpmyadmin<br/>
    ![phpadmin](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/phpadmin.jpg "phpadmin")<br/>
 -CSV:
  -Gunakan node CSV Writer<br/>
    ![csvwrite](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/csvwrite.png "csvwrite")<br/>
  -lalu klik kanan untuk melakukan konfigurasi<br/>
    ![csvwriteset](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/csvwriteset.jpg "csvwriteset")<br/>
  -Pilih output location lalu klik ok, lalu execute<br/>


# Modeling
### Proses membaca data dari dua sumber yang berbeda
#### Proses membaca dari MYSQL
- yang pertama membaca data dari mysql, dengan menggunakan mysql connector nodes dari knime<br/>
 ![sqlconn](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/sqlconn.png "sqlconn")<br/>
- data di mysql seperti dibawah<br/>
 ![phpadmin](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/phpadmin.jpg "phpadmin")<br/>
- melakukan configurasi disesuaikan dengan mysql yang ada di phpmyadmin, mulai dari database, port dari localhost dan username.<br/>
 ![sqlconnset](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/sqlconnset.png "sqlconnset")<br/>
- db table selector untuk mengambil Koneksi DB sebagai input dan memungkinkan untuk memilih tabel atau tampilan dari dalam database yang terhubung.<br/>
 ![tabsel](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/tabsel.png "tabsel")<br/>
- db reader untuk Mengeksekusi kueri input dalam database dan mengambil hasilnya ke dalam tabel data KNIME.<br/>
 ![dbread](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/dbread.png "dbread")<br/>
- hasil akhir dari pembacaan database yang terhubung dari mysql<br/>
 ![dbreadnew](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/dbreadnew.jpg "dbreadnew")<br/>

#### Proses membaca dari csv
- memasang csv reader untuk membaca file csv<br/>
 ![fileread](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/fileread.png "fileread")<br/>
- melakukan konfigurasi , menentukan path file dimana csv disimpan<br/>
 ![filereadfind](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/filereadfind.jpg "filereadfind")<br/>


### Proses Modeling
- menggunakan joiner node, dengan mengsambungkan node dari database yang mengolah mysql dan csv<br/>
 ![joiner](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/joiner.png "joiner")<br/>
- melakukan configure dengan memilih kolom yang urutan nya sama<br/>
  -hasilnya seperti ini<br/>


- menggunakan column filter untuk menentukan column mana yang mau ditampilkan<br/>
 ![alt text](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/colfilt.png "colfilt" ) <br/>
- hasil akhir<br/>
 ![colfiltres](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/colfiltres.jpg "colfiltres")<br/>


# Evaluation

- dari kedua data yang ada di mysql dan csv telah berhasil di join

- hasil join


- data asli 


- tes berhasil karena hasil join sama dengan data asli sebelum dipisah

# Deployment
### simpan ke csv
- data yang pertama akan disimpan ke csv dengan menggunakan csv writer<br/>
![csvwrite](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/csvwrite.png "csvwrite")<br/>

- memilih penempatan dan konfigurasi lain nya
![csvwritefinale](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/csvwritefinale.jpg "csvwritefinale")<br/>
 
- data berhasil tersimpan


 ### simpan ke db
- data akan disimpan ke database menggunakan db writer<br/>
![dbwrite](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/dbwrite.png "dbwrite")<br/>

- memilih konfigurasi lain nya, seperti nama dan db yang dituju<br/>
![dbwritefinale](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/dbwritefinale.jpg "dbwritefinale")<br/>

- berhasil tersimpan<br/>
![phpadmfinale](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/phpadmfinale.jpg "phpadmfinale")<br/>

 ### gambar knime secara lengkap
-Preparation Phase<br/>
![prep](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/prep.png "prep")<br/>
-Modelling Phase<br/>
![schemefinale](https://github.com/BagasJwn/BigData_Tugas1/blob/master/dokumentasi/ssimg/schemefinale.jpg "schemefinale")<br/>


