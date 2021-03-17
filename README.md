<h1 align="center">
<br>
  <img src="https://upload.wikimedia.org/wikipedia/en/thumb/5/53/Magento.svg/1280px-Magento.svg.png" alt="Mahento2" width="500">
</h1>

<h4 align="center">An Open Source eCommerce .</h4>

<p align="center">
  <a href="#sekilas-tentang">Sekilas Tentang</a> •
  <a href="#alur-instalasi">Alur Instalasi</a> •
  <a href="#kebutuhan-sistem-magento">Kebutuhan Sistem Magento</a> •
  <a href="Langkah Instalasi">Langkah Instalasi</a> •
  <a href="#cara-pemakaian">Cara Pemakaian</a> •
  <a href="#pembahasan">Pembahasan</a> •
  <a href="#referensi">Referensi</a>
</p>

<p align="center">
	<img src="https://img.shields.io/badge/ecommerce-magento2-orange">
	<img src="https://img.shields.io/badge/version-v2.3.x-blue">
	<img src="https://github.com/thelounge/thelounge/workflows/Build/badge.svg"></a>
	<img src="https://img.shields.io/badge/part%20of-adobe-red">
</p>


# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**Magento 2** merupakan sebuah platform CMS atau *Content mManagement System* yang bersifat *Open Source* dan banyak diaplikasikan untuk membuat website *e-commerce* yang dapat di *custom* sesuai dengan keinginan dan kebutuhan pengguna.  **Magento 2** di rilis pada tahun 2015, rilis nya magento 2 ini karena ada kekurangan dalam magento 1. Untuk menyempurnakan kekurangan magento 1 maka dirilislah magento 2.

# Alur Instalasi
[`^ kembali ke atas ^`](#)
<h1 align="center"><img src="https://devdocs.magento.com/common/images/install-diagram-24.svg"></h1>
Diagram tersebut menunjukkan hal berikut:

1. Siapkan lingkungan server .
Instal perangkat lunak prasyarat, termasuk PHP, Apache, MySQL, dan Elasticsearch.

2. Dapatkan perangkat lunak Magento.
Dapatkan paket metapackage Magento Open Source atau Magento Commerce Composer untuk mengelola komponen Magento dan dependensinya.

3. Instal perangkat lunak Magento menggunakan baris perintah.
Jika langkah tersebut gagal karena perangkat lunak prasyarat tidak disiapkan dengan benar, tinjau Prasyarat tersebut

4. Verifikasi penginstalan dengan melihat etalase toko dan Admin Magento.

# Kebutuhan Sistem Magento
[`^ kembali ke atas ^`](#)

#### Sistem Operasi (Linux x86-64) :
Distribusi Linux, seperti RedHat Enterprise Linux (RHEL), CentOS, Ubuntu, Debian, dan sejenisnya. Magento tidak didukung di Microsoft Windows dan macOS.

#### Persyaratan Memori :
Memerlukan RAM hingga 2 GB.

#### Brower yang Didukung :
-   Microsoft Edge ,Firefox terbaru (sistem operasi apapun),
-   Chrome terbaru (sistem operasi apapun),
-   Safari terbaru (khusus Mac OS),

#### Composer :
-   Magento 2.4.2 dan yang lebih baru kompatibel dengan Composer 1.x dan 2.x
-   Magento 2.4.1 dan sebelumnya hanya kompatibel dengan Composer 1.x.

#### Server web :
-   Apache 2.4  
-   nginx 1.x

#### Database :
-   MySQL 8.0
-   MariaDB 10.4 

#### PHP :
Magento mendukung PHP 7.4.0. Anda dapat menginstal Magento 2.4.0 dengan 7.3, tetapi itu tidak diuji atau disarankan. Akan tetapi untuk Magento 2.3.x direkomendasikan menggunakan PHP 7.2

# Langkah Instalasi
[`^ kembali ke atas ^`](#)

### Langkah 1: Instal Apache2 PHP dan Ekstensi yang Diperlukan :
#### Langkah 1.1 Instal Apache2 Server
Untuk menginstal Apache, Anda harus mengupdate paket sebelum menjalankan perintah install Apache install:
```
$ sudo apt update
$ sudo apt install apache2
```
Untuk menjalankan apache secara otomatis selama startup, jalankan baris perintah berikut:
```
$ sudo systemctl enable apache2.service
```
#### Langkah 1.2 Konfigurasi Virtual Host Apache2
Untuk mendeklarasikan konfigurasi situs Apache2 untuk penyimpanan Magento 2, anda harus membuat file konfigurasi baru magento2.conf:
```
$ sudo nano /etc/apache2/sites-available/magento2.conf
```
Salin dan tempel konten berikut ke file di atas. Ingat, anda harus mengubah `domain.com` menjadi `localhost.com` anda.

<details><summary><b>Show instructions</b>
</summary>

```
<VirtualHost *:80>
	ServerAdmin admin@localhost.com
	DocumentRoot /var/www/html/magento2/
	ServerName localhost.com
	ServerAlias www.localhost.com
		
	<Directory /var/www/html/magento2/>
		Options Indexes FollowSymLinks MultiViews
		AllowOverride All
		Order allow,deny
		allow from all
	</Directory>
	
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

</details>

Disini kita menginstal Magento secara lokal. Kemudian anda harus memperbarui file `$ sudo nano /etc/hosts` lalu tambah `127.0.0.1 localhost.com`

Pastikan anda mengaktifkan *mod rewrite* untuk menggunakan situs
```
$ sudo a2ensite magento2.conf
$ sudo a2enmod rewrite
```
#### Langkah 1.3: Instal PHP 7.2 dan ekstensi
```
$ sudo add-apt-repository ppa:ondrej/php
$ sudo apt install php7.2 libapache2-mod-php7.2 php7.2-common php7.2-gmp php7.2-curl php7.2-soap php7.2-bcmath php7.2-intl php7.2-mbstring php7.2-xmlrpc php7.2-mcrypt php7.2-mysql php7.2-gd php7.2-xml php7.2-cli php7.2-zip
```
#### Langkah 1.4: Perbarui file php.ini
```
$ sudo nano /etc/php/7.2/apache2/php.ini
```
Ubah data berikut:


<details><summary><b>Show instructions</b>
</summary>


```
file_uploads = On
allow_url_fopen = On
short_open_tag = On
memory_limit = 512M
upload_max_filesize = 128M
max_execution_time = 3600
```

</details>

Kemudian simpan file `php.ini`. Setelah itu, anda harus merestart apache2 dan jalankan perintah ini:
```
$ sudo systemctl restart apache2.service
```
### Langkah 2: Instal Server Database
Magento lebih memilih server basis data MariaDB daripada server basis data MySQL default, karena kinerja yang lebih cepat dan lebih baik. Untuk menginstal MariaDB Server dan Klien, jalankan baris perintah ini:
```
$ sudo apt-get install mariadb-server mariadb-client
```
Pastikan itu mulai dan mulai setiap kali anda *me-reboot* server:
```
$ sudo systemctl restart mariadb.service
$ sudo systemctl enable mariadb.service
```
Anda baru saja menginstal server MariaDB, sekarang anda harus menyiapkan server database ini terlebih dahulu.
```
$ sudo mysql_secure_installation
```
Lalu anda akan diminta untuk memilih opsi berikut:
<details><summary><b>Show instructions</b>
</summary>

```
Enter current password for root (enter for none): Masukan Password root
Set root password? [Y/n]: n
Remove anonymous users? [Y/n]: Y
Disallow root login remotely? [Y/n]: Y
Remove test database and access to it? [Y/n]: Y
Reload privilege tables now? [Y/n]: Y
```
</details>

### Langkah 3: Buat Pengguna MySQL (Wajib)
Dari Magento 2.3.x, Magento membutuhkan pengguna unik untuk instalasi Magento, Magento tidak dapat menggunakan pengguna `default: root`.

Pertama-tama, anda harus masuk ke MariaDB:
```
$ sudo mysql -u root
```
Buat database baru untuk Magento 2:
```
CREATE DATABASE magento2;
```
Kemudian buat panggilan nama pengguna baru: `magento2os`
```
CREATE USER 'magento2os'@'localhost' IDENTIFIED BY 'YOUR_PASSWORD';
```
Berikan pengguna `magento2os` ke database `magento2`:
```
GRANT ALL ON magento2.* TO 'magento2os'@'localhost' IDENTIFIED BY 'YOUR_PASSWORD' WITH GRANT OPTION;

GRANT ALL PRIVILEGES ON magento2.* TO 'magento2os'@'localhost' WITH GRANT OPTION;
```
*Flush* hak istimewa dan keluar
```
FLUSH PRIVILEGES;
EXIT;
```
### Langkah 4 : Instal Composer
Anda dapat menggunakan baris perintah berikut untuk menginstal Composer
```
$ sudo apt install curl
$ curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```
Karena kita akan menginstall `Magento versi 2.3.x` maka harus menggunakan `Composer versi 1` dengan baris perintah
```
$ sudo composer self-update --1
```
Periksa Komposer diinstal atau tidak dengan mengetik 
```
$ composer -v
```
Output
```
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 1.10.20 2021-01-27 15:41:06
```
### Langkah 5 : Unduh Magento
Anda dapat mengunduh dari salah satu sumber daya berikut [magento2-2.3](https://ipb.link/magento2/)

Setelah mengunduh ubah nama folder menjadi `magento2` *seperti pada gambar dibawah* dan Anda harus mengekstrak paket ke `/var/www/html/`

<img src="https://i.ibb.co/nD1FbDh/Screenshot-2021-03-12-13-54-39.png" width="500">

```
$ sudo apt-get install unzip
$ cd /Downloads
$ sudo unzip magento2-2.3.zip -d /var/www/html/
```
Setel izin, jalankan perintah ini
```
sudo chown -R www-data:www-data /var/www/html/magento2/
sudo chmod -R 755 /var/www/html/magento2/
```
### Langkah 7: Instal Magento 2
```
$ cd /var/www/html/magento2/
$ sudo composer install
```
Setelah terinstal magento 2 dengan composer, untuk menghindari eror ketika setup wizard mengenai admin tambahkan baris perintah berikut :
```
$ sudo apt-get install php7.1-sodium -y
$ php bin/magento admin:user:create --admin-user=admin123 --admin-password=1235678 \ --admin-email=hi@mydomian.com --admin-firstname=Admin --admin-lastname=Doe
```
Akses ke alamat ini `http://localhost.com/magento2`, Anda akan mendapatkan Magento Setup Wizard sebagai berikut:
![magento](https://cdn2.mageplaza.com/media/general2/ySUWqGm.png)
#### Langkah 7.1: Mulai Menginstal

-   Klik Start Readiness Check. Jika ada kesalahan yang ditampilkan, anda harus mengatasinya sebelum melanjutkan. Klik Lebih detail jika tersedia untuk melihat informasi lebih lanjut tentang setiap cek.
![1](https://i.ibb.co/0Y2RRjr/Screenshot-2021-03-11-22-18-44.png)
- Jika tidak atau aman seperti di gambar Klik Next
#### Langkah 7.2 Tambahkan Database
-   Isi informasi database sesuai dengan yang anda buat sebelumnya yaitu pada saat membuat user yaitu dengan nama `magento2os` dan password yang sesuai, untuk nama database yaitu `magento2` sama seperti yang dibuat di MariaDB
![2](https://i.ibb.co/GWB4kYn/2.png)
![2.1](https://i.ibb.co/cvJfBwK/3.png)
#### Langkah 7.3 Konfigurasi Web
![3](https://i.ibb.co/xCbpYZ2/web.png)
-   Masukkan informasi berikut:
	-   Alamat Toko Anda: [http://localhost.com](http://localhost.com)
	-   Alamat Admin Magento: Edit URL relatif yang digunakan untuk mengakses Admin Magento. Atau gunakan yang sudah tergenerate otomatis oleh Magento.
- Kemudian klik Next
#### Langkah 7.4 Sesuaikan Toko Anda
![4](https://i.ibb.co/0DgWbkQ/Screenshot-2021-03-11-22-48-38.png)
-   Dari daftar Zona Waktu Default Toko, klik nama zona waktu toko Anda.
-   Dari daftar Simpan Mata Uang Default, klik mata uang default untuk digunakan di toko Anda.
-   Dari daftar Store Default Language, klik bahasa default yang akan digunakan di toko Anda.
-   Perluas Konfigurasi Modul Lanjutan untuk mengaktifkan atau menonaktifkan modul secara opsional sebelum Anda menginstal perangkat lunak Magento.
#### Langkah 7.5 Buat Akun Admin
Sekarang masukkan informasi admin seperti
-   Username Baru
-   Email Baru
-   Password Baru
-   Konfirmasi Password Baru
-   Lalu Klik Next
#### Langkah 7.6 Install
Setelah menyelesaikan semua langkah sebelumnya di Setup Wizard , klik Instal Now.
![6](https://i.ibb.co/wzj32wv/l3zTxQm.png)
![6.1](https://i.ibb.co/tLYLyhJ/Screenshot-2021-03-11-22-50-55.png)
![6.3](https://i.ibb.co/QPJfxmb/hahsh.png)

Penginstalan Berhasil Pesan Berhasil akan ditampilkan untuk menunjukkan penginstalan yang berhasil.

# Cara Pemakaian
[`^ kembali ke atas ^`](#)

Cara pemakaian **Magento2** ini cenderung bersifat *user-friendly* dimana dalam aplikasi ini bersifat dashboarding yang didesain khusus untuk kegiatan *e-commerce* admin. Rincian deatilnya adalah sebagai berikut :
1. Untuk masuk ke dalam halaman admin toko kita, kita harus login terlebih dahulu dengan memasukan link yang sudah kita buat contohnya yaitu localhost.com/admin_en1brm dan memasukan username dan password yang sudah kita buat sebelumnya.
<img src="https://i.ibb.co/26PSWgb/Screenshot-2021-03-11-23-14-35.png">

2. Setelah itu, kita akan masuk ke halaman admin toko atau **Dashboard**. Disini kita dapat melihat laporan penjualan toko kita diantaranya **lifetime sales**, **average order**, dan **last order** dan kita juga bisa melihat *bestsellers*, *most viewed product*, *new customers* dan *customers*.
<img src="https://i.ibb.co/nzbBBVZ/Dashboard.png">

3. Pada bagian samping kiri, terdapat berbagai menu yang dapat kita gunakan. Menu **Order** berguna untuk mengetahui informasi lebih detail tentang penjualan pada website kita. Disini kita dapat mencetak **invoices**, **status shipment**, **credit memos**, **billing agreements**, dan **transactions**.
<img src="https://i.ibb.co/CVrYv6H/Sales.png">

4. Pada bagian **Catalog** kita bisa menampilkan products yaitu daftar **produk** dan **categories** yaitu kategori dari produk tersebut.
<img src="https://i.ibb.co/H4jx0xV/catalog.png">

5. Pada bagian **Customers** kita bisa lihat daftar semua customers pada **all customers**, melihat customer yang sedang aktif pada now online dan bisa melihat grup customer pada **customers groups**.
<img src="https://i.ibb.co/3yJhbXY/customers.png">

6. Pada bagian **Marketing** disini bisa kita lihat banyak sekali fitur-fitur mengenai marketing yaitu ada bagian **promotions**, **communications**, **seo & search** dan **user content**.
<img src="https://i.ibb.co/QPtyscn/Marketing.png">

7. Pada bagian **Content** terdapat beberapa kustomisasi umum mengenai content yang akan di tampilkan di dalam toko contohnya pada **elements** kita bisa mengatur *pages*, *blocks* dan *widgets* sedangkan pada **design** kita bisa mengatur dari *configurations*, *themes*, dan *schedule*.
<img src="https://i.ibb.co/Xy3DB6R/Content.png">

8. Pada bagian **Reports** terdapat beberapa menu mengenai pembuatan laporan dimulai dari **marketing**, **sales**, **customers** dan **business intelligence**.
<img src="https://i.ibb.co/dgCxMtT/Reports.png">

9. Pada bagian **Stores** kita bisa melihat secara umum konfigurasi mengenai toko yaitu pada bagian **settings**, **attributes**, **taxes** dan **currency**. 
<img src="https://i.ibb.co/dkLZxnB/Stores.png">

10. Pada bagian **System** yaitu konfigurasi atau pengaturan secara keseluruhan sepert **data transfer**, **permissions**, **extensions**, **action logs**, **tools** dan **other settings**.
<img src="https://i.ibb.co/NLFXqNk/system.png">

11. Dan yang terakhir pada bagian **Find Partners & Extensions** adalah kita bisa mencari partners engagments sebagai services magento untuk membantu pedagang lainya dalam mengembankan bisnis. Dan fitur dalam pencarian Ekstensi untuk toko kita.
<img src="https://i.ibb.co/vcW2MmD/Screenshot-2021-03-12-19-15-22.png">

# Pembahasan
[`^ kembali ke atas ^`](#)

**Magento2** adalah platform built-in `PHP` yang membantu dalam pengembangan website e-Commerce. Terdapat 2 pilihan platform magento yaitu Magento Opensource dan Magento Commerce. Kelebihan dari magento versi open source adalah :
- Gratis tanpa biaya tambahan 
- Kaya akan fitur-fitur
- Sangat skalabilitas
- Fleksibilitas tinggi dan dapat dikostumisasi sesuka hati
- Ramah terhadap perangkat mobile
- Komunitas pengguna yang besar

Kekurangan dari **Magento2** ini adalah :
- Waktu respon lambat
- Proses kustomisasi dapat lebih lama dibandingkan dengan platform lainnya
- Platform yang kompleks dan membutuhkan pengembang yang berpengalaman
- Membutuhkan tempat hosting yang bagus
- Technical support yang buruk


Jika dibandingkan dengan platform terbaik menurut techliance, **Woocommerce** perbandingannya adalah sebagai berikut:
- **Woocommerce** mudah digunakan oleh pemula dalam pengembangan e-commerce sedangkan **Magento2** membutuhkan pengembang berpengalaman dikarenakan sistem yang kompleks
- Fitur security pada magento lebih baik daripada **Woocommerce**. pada **Magento2** 
- Kedua platform memang menyediakan opsi plug in dan ekstensi tambahan. Tetapi ekstensi pada **Woocommerce** lebih mudah untuk diinstall dan lebih murah.
- **Magento2** memiliki banyak fitur out-of-the-box sedangkan **Woocommerce** hanya menyediakan fitur basic.
# Referensi
[`^ kembali ke atas ^`](#)

1. [About Magento2](https://www.magento.com/) - Magento2
2. [7 Steps to Install Magento 2 on Ubuntu/Debian](https://www.mageplaza.com/devdocs/how-install-magento-2-ubuntu.html) - MagePlaza
3. [How to Install Magento in Linux {Step-By-Step Guide}](https://ccbill.com/kb/how-to-install-magento-in-linux) - ccbill
4. [Installation flow](https://devdocs.magento.com/guides/v2.4/install-gde/install-flow-diagram.html) - Magento2
5. [Pros and Cons of Magento Ecommerce Platforms](https://elogic.co/blog/pros-and-cons-of-magento-ecommerce-platforms/) - elogic
6. [Magento vs WooCommerce 2021: Which One Is Better?](https://www.mageplaza.com/blog/magento-2-woocommerce.html) - MagePlaza
