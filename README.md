
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
Salin dan tempel konten berikut ke file di atas. Ingat, anda harus mengubah domain.com menjadi localhost.com anda.
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
Magento lebih memilih server basis data `MariaDB` daripada server basis data `MySQL` default, karena kinerja yang lebih cepat dan lebih baik. Untuk menginstal MariaDB Server dan Klien, jalankan baris perintah ini:
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
Berikan pengguna magento2os ke database magento2:
```
GRANT ALL ON magento2.* TO 'magento2os'@'localhost' IDENTIFIED BY 'YOUR_PASSWORD' WITH GRANT OPTION;

GRANT ALL PRIVILEGES ON magento2.* TO 'magento2os'@'localhost' WITH GRANT OPTION;
```
Hapus hak istimewa dan keluar
```
FLUSH PRIVILEGES;
EXIT;
```
