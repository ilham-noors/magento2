

<h1 align="center"><img src="https://wearesuperb.com/wp-content/uploads/2015/11/magento2.0.jpg"></h1>

[Sekilas Tentang](#sekilas-tentang) | [Alur Instalasi](#alur-instalasi) | [Kebutuhan Sistem Magento](#kebutuhan-sistem-magento) | [Langkah Instalasi](#langkah-instalasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:



# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**Magento 2** merupakan sebuah platform CMS atau *Content mManagement System* yang bersifat *Open Source* dan banyak diaplikasikan untuk membuat website *e-commerce* yang dapat di *custom* sesuai dengan keinginan dan kebutuhan pengguna.  **Magento 2** di rilis pada tahun 2015, rilis nya magento 2 ini karena ada kekurangan dalam magento 1. Untuk menyempurnakan kekurangan magento 1 maka dirilislah magento 2.

# Alur Instalasi
[`^ kembali ke atas ^`](#)
<h1 align="center"><img src="https://devdocs.magento.com/common/images/install-diagram-24.svg"></h1>
Diagram tersebut menunjukkan hal berikut:

1. Siapkan lingkungan server Anda.
Instal perangkat lunak prasyarat, termasuk PHP, Apache, MySQL, dan Elasticsearch. Konsultasikan persyaratan sistem untuk informasi spesifik.

2. Dapatkan perangkat lunak Magento.
(Direkomendasikan) Dapatkan paket metapackage Magento Open Source atau Magento Commerce Composer untuk mengelola komponen Magento dan dependensinya.

3. Instal perangkat lunak Magento menggunakan baris perintah.
Jika langkah tersebut gagal karena perangkat lunak prasyarat tidak disiapkan dengan benar, tinjau Prasyarat kami

4. Verifikasi penginstalan dengan melihat etalase Anda dan Admin Magento.

# Kebutuhan Sistem Magento
[`^ kembali ke atas ^`](#)

#### Sistem Operasi (Linux x86-64) :
Distribusi Linux, seperti RedHat Enterprise Linux (RHEL), CentOS, Ubuntu, Debian, dan sejenisnya. Magento tidak didukung di Microsoft Windows dan macOS.

#### Persyaratan Memori :
Mengupgrade aplikasi dan ekstensi Magento yang Anda peroleh dari Magento Marketplaces dan sumber lain dapat memerlukan RAM hingga 2 GB. Jika Anda menggunakan sistem dengan RAM kurang dari 2GB, kami sarankan Anda membuat file swap; jika tidak, peningkatan Anda mungkin gagal.

#### Brower yang Didukung :
 -   Microsoft Edge ,Firefox terbaru (sistem operasi apapun),
-   Chrome terbaru (sistem operasi apapun),
-   Safari terbaru(khusus Mac OS),
-   Safari Mobile untuk iPad 2, iPad Mini, iPad dengan Retina Display (iOS 12 atau lebih baru), untuk etalase desktop .

#### Composer :
Composer diperlukan untuk pengembang yang ingin berkontribusi pada basis kode Magento 2 atau siapa saja yang ingin mengembangkan ekstensi Magento.
-   Magento 2.4.2 dan yang lebih baru kompatibel dengan Composer 1.x dan 2.x
-   Magento 2.4.1 dan sebelumnya hanya kompatibel dengan Composer 1.x.

#### Server web :
-   Apache 2.4
    Selain itu, Anda harus mengaktifkan modul Apache mod_rewrite dan mod_version. Modul mod_rewrite memungkinkan server untuk melakukan penulisan ulang URL. Modul mod_version menyediakan pemeriksaan versi fleksibel untuk versi httpd yang berbeda. Untuk informasi lebih lanjut, lihat dokumentasi Apache kami.
    
-   nginx 1.x

#### Database :
-   MySQL 8.0 untuk penginstalan di lokasi
-   MariaDB 10.4 untuk proyek Magento Commerce Cloud

Magento juga kompatibel, tetapi belum diuji dan tidak direkomendasikan, dengan MySQL 5.7.9, MariaDB 10.2, dan Percona 5.7.

#### PHP :
Magento mendukung PHP 7.4.0. Anda dapat menginstal Magento 2.4.0 dengan 7.3, tetapi itu tidak diuji atau disarankan. Ini dimaksudkan untuk meningkatkan dari Magento 2.3.x ke Magento 2.4.0.Akan tetapi untuk Magento 2.3.x direkomendasikan menggunakan PHP 7.2.0

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
```
file_uploads = On
allow_url_fopen = On
short_open_tag = On
memory_limit = 512M
upload_max_filesize = 128M
max_execution_time = 3600
```
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
```
Enter current password for root (enter for none): Masukan Password root
Set root password? [Y/n]: n
Remove anonymous users? [Y/n]: Y
Disallow root login remotely? [Y/n]: Y
Remove test database and access to it? [Y/n]: Y
Reload privilege tables now? [Y/n]: Y
```
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
Hapus hak istimewa dan keluar
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

<img src="https://i.ibb.co/nD1FbDh/Screenshot-2021-03-12-13-54-39.png">

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
![login](https://i.ibb.co/26PSWgb/Screenshot-2021-03-11-23-14-35.png)

2. Setelah itu, kita akan masuk ke halaman admin toko atau Dashboard. Disini kita dapat melihat laporan penjualan toko kita diantaranya **Lifetime Sales**, **Average Order**, dan **Last Order** dan kita juga bisa melihat **Bestsellers**, **Most Viewed Product**, **New Customers** dan **Customers**
![Dashboard](https://i.ibb.co/nzbBBVZ/Dashboard.png)
3. Sales
![Sales](https://i.ibb.co/CVrYv6H/Sales.png)
4. Catalog
![Catalog](https://i.ibb.co/H4jx0xV/catalog.png)
5. Customers
![customers](https://i.ibb.co/3yJhbXY/customers.png)
6. Marketing
![Marketing](https://i.ibb.co/QPtyscn/Marketing.png)
7. Content
![Content](https://i.ibb.co/Xy3DB6R/Content.png)
8. Reports
![Reports](https://i.ibb.co/dgCxMtT/Reports.png)
9. Stores
![Stores](https://i.ibb.co/dkLZxnB/Stores.png)
10. System
![System](https://i.ibb.co/NLFXqNk/system.png)
11. Find
![find](https://i.ibb.co/vcW2MmD/Screenshot-2021-03-12-19-15-22.png)
# Pembahasan
[`^ kembali ke atas ^`](#)

**Prestashop** ditulis dalam bahasa pemrograman `PHP` yang support untuk penggunaan MySQL. Sebagai salah satu CMS yang paling banyak digunakan di dunia, aplikasi ini menawarkan berbagai kelebihan, diantaranya :
- Aplikasi memiliki panel administrasinya mudah digunakan dan fleksibel, sehingga dapat disesuaikan dengan kebutuhan.
- Mendukung berbagai layanan pembayaran utama, seperti `PayPal`, `VISA`, `MasterCard`, dan `Maestro`.
- Diterjemahkan dalam banyak bahasa, termasuk Bahasa Indonesia.
- Memiliki desain yang *responsive*, sehingga dapat dibuka menggunakan *device* apapun.
- Memiliki lebih dari tiga ratus fitur untuk memudahkan pengguna.
- Banyak pengguna yang berkontribusi pada *discussion boards* dan sejenisnya, sehingga masalah yang dihadapi pengguna dapat cepat terselesaikan.

Tentu saja, sebuah aplikasi pasti memiliki kekurangan. Kekurangan yang dimiliki **Prestashop** antara lain :
- Penggunaan fitur atau modul yang lengkap menyebakan proses loading dari aplikasi ini menjadi sangat lambat
- Penggunaan *resource* memory aplikasi ini cukup besar, terutama ketika menggunakan fitur atau modul yang lengkap.
- Sebagian besar modul dan tema yang tersedia tidak gratis.

Jika dibandingkan dengan CMS sejenisnya seperti **Microweber**, CMS ini memiliki beberapa keunggulan dan kelemahan. Berikut adalah beberapa perbandingan antara kedua CMS ini :
- **Microweber** menyediakan proses design yang fleksibel dengan fitur *Drag and Drop* tanpa batasan, sehingga pengguna bebas mengkreasikan tampilan websitenya. Sedangkan **Prestashop** hanya menyediakan fitur design berupa penggantian template dan logo, adapun template yang tersedia tidak gratis.
- Modul atau plugin yang tersedia pada **Prestashop** jauh lebih banyak dibandingkan pada **Microweber**.
- **Prestashop** memiliki pengguna yang jauh lebih banyak daripada **Microweber** yang aktif pada forum-forum diskusi untuk membantu pengguna pemula.
- **Microweber** lebih ringan daripada **Prestashop** karena modulnya yang sedikit.
- Proses instalasi **Prestashop** lebih mudah karena berbasis PHP saja, sedangkan **Microweber** menggunakan framework laravel sehingga proses instalasi lebih sulit, terutama dalam hal *dependency*.
# Referensi
[`^ kembali ke atas ^`](#)

1. [About PrestaShop](https://www.prestashop.com/) - PrestaShop
2. [How to Log Into a VPS with PuTTY on Windows](https://www.digitalocean.com/community/tutorials/how-to-log-into-a-vps-with-putty-windows-users) - DigitalOcean
3. [How to Install PrestaShop on Ubuntu 16.04](http://idroot.net/linux/install-prestashop-ubuntu-16-04/) - idroot
4. [One Click Install PrestaShop](https://www.prestashop.com/blog/en/how-to-install-prestashop/) - PrestaShop
5. [PrestaShop Review](http://whichshoppingcart.com/prestashop.html) - whishshoppingcart
