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
