# Centratama HC Portal 🆕 (new)

## Iktisar
Repositori ini berisi kode sumber (*source code*) pengembangan aplikasi HC Portal. Aplikasi ini digunakan untuk mendigitalisasi proses-proses internal di divisi HC.

HC Portal harus dapat menangani berbagai proses yang berbeda dalam satu aplikasi. Penggunaan *framework* [CodeIgniter](https://github.com/bcit-ci/CodeIgniter) dapat membantu kebutuhan ini, sebab proses-proses internal yang berbeda tersebut disusun dalam satu kerangka model pemrograman yang disebut dengan [MVC](https://www.dicoding.com/blog/apa-itu-mvc-pahami-konsepnya/) (*Model View Controller*). Setiap modul aplikasi yang dikembangkan di HC Portal memiliki MVC-nya sendiri. Walaupun begitu, mereka memiliki data yang terpusat. Itulah sebabnya data yang tersimpan di satu modul aplikasi dapat digunakan di modul aplikasi lainnya.

## HC Portal yang baru 🆕
Pengembangan HC Portal sebelumnya ada di repositori berikut:

https://github.com/ryumada/centratama-hcportal.

Repositori tersebut merupakan hasil [*forking*](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks) dari pengembang sebelumnya di repositori berikut:

https://github.com/julians22/hc_system

Repositori ini merupakan versi terbaru dari pengembangan aplikasi HC Portal yang terdiri dari berbagai fitur di dalamnya, seperti:
- Penggunaan tampilan yang lebih responsif terhadap berbagai perangkat ([*Responsive Web Design*](https://www.w3schools.com/html/html_responsive.asp)) dengan menggunakan templat [Admin LTE v3](https://github.com/ColorlibHQ/AdminLTE).
- Struktur tampilan dengan konsep hierarki sehingga memudahkan dalam memasang tampilan modul aplikasi yang dibutuhkan saja. Pemasangannya melalui setiap *Controller* modul aplikasi yang dapat diakses melalui URL.
- Kemudahan dalam memasang dan mencopot *library* Javascript melalui *Controller* juga.

## Komponen Aplikasi HC Portal
Components Used:
- [CodeIgniter](https://github.com/bcit-ci/CodeIgniter) v3.1.11 (PHP Framework)
- [MySQL](https://www.mysql.com/) 8 (Database)
- [Admin LTE](https://github.com/ColorlibHQ/AdminLTE) v3 (Bootstrap based)
- [JQuery](https://jquery.com/)

Javasript Libraries:
- [Datatables](https://datatables.net/)
- [JQuery-Validation](https://jqueryvalidation.org/)
- [CKEDITOR](https://ckeditor.com/)
- [SweetAlert 2](https://github.com/sweetalert2/sweetalert2)
- more...

## Cara memasang dan menjalankan aplikasi
Cara dibawah ini diperuntukkan untuk perangkat dengan Linux menggunakan Ubuntu atau Debian. Di sini saya melakukan pemasangan stack teknologinya satu per satu.

### Prasyarat
- Memiliki akses [sudo](https://en.wikipedia.org/wiki/sudo).
- Distribusi Linux memiliki `ufw`. Jika tidak terpasang, bisa memasangnya dengan `sudo apt install ufw` pada Ubuntu atau `sudo pkcon install ufw` pada KDE Neon.
- Terdapat `git` dan `npm`.
- Memiliki software Database Tool seperti [dbeaver](https://dbeaver.io/), [phpmyadmin](https://www.phpmyadmin.net/), atau sejenisnya.
- Memiliki software [FreeFileSync](https://freefilesync.org/) atau sejenisnya untuk menyinkronkan berkas pengembangan di direktori `home` dan direktori server di `/var/www/hcportal/`.
- Sebelum menjalankan Instruksi di bawah pastikan terdapat webserver terpasang di server-mu. Jika belum, kamu bisa membaca [README-persiapan-lemp-stack-linux-nginx-engine-x-mysql-php](README-persiapan-lemp-stack-linux-nginx-engine-x-mysql-php.md).

### Pengembangan HC Portal dan Menjalankannya dengan Nginx
Ada beberapa langkah yang harus dilakukan untuk menyiapkan pengembangan HC Portal:
1. [Clone Repositori ke direktori untuk pengembangan (Development Directory)](#clone-repositori-ke-direktori-untuk-pengembangan-development-directory)
2. [Persiapan Basis Data](#persiapan-basis-data)
3. [Persiapan Dependensi Javascript dan CSS Library](#persiapan-dependensi-javascript-dan-css-library)
4. [Sinkronkan berkas yang ada di Development Directory ke `/var/www/hcportal` (Deployment Directory)](#sinkronkan-berkas-yang-ada-di-development-directory-ke-varwwwhcportal-deployment-directory)
5. [Ubah pengaturan di berkas PHP](#ubah-pengaturan-di-berkas-php)
6. [Buat Controller `Test.php` di `application/controllers` {Optional}](#buat-controller-testphp-di-applicationcontrollers-optional)

#### Clone Repositori ke direktori untuk pengembangan (Development Directory)
**Dev Directory** digunakan untuk melakukan pengembangan HC Portal (*workspace* pengembangan). Biasanya direktori yang digunakan adalah `/home/$USER/development` atau folder apapun yang biasa kamu gunakan untuk mengembangkan *software*.

Kita bisa clone repositori dengan perintah berikut:
```bash
git clone https://github.com/ryumada/centratama-hcportal-new.git
```

#### Persiapan Basis Data
Ada 2 basis data yang digunakan pada aplikasi HC Portal:
- `hcportal_dev` -> Basis data utama yang mendukung proses aplikasi.
- `hcportal_archives` -> Menyimpan data yang sudah usang dan tidak digunakan lagi, namun diperlukan untuk keperluan arsip data.

Buatlah kedua basis data dengan kedua nama tersebut. Lalu, lakukan impor basis data dengan mengimpor berkas `hcportal_dev.sql` ke basis data `hcportal_dev` dan `hcportal_archives.sql` ke basis data `hcportal_archives`.

Impor basis data bisa menggunakan software database tool seperti [dbeaver](https://dbeaver.io/).

#### Persiapan Dependensi Javascript dan CSS Library
Buka terminal (konsole), lalu masuk ke direktori `centratama-hcportal-new/assets/vendor/`.

```bash
cd centratama-hcportal-new/assets/vendor/
```

Kemudian jalankan perintah `npm install`.

```bash
npm install
```

Perintah ini akan memasang semua dependensi Javascript dan CSS Library yang diperlukan oleh Aplikasi HC Portal.

#### Sinkronkan berkas yang ada di Development Directory ke `/var/www/hcportal` (Deployment Directory)
**Deployment Directory** digunakan untuk menjalankan aplikasi HC Portal pada web server `/var/www/hcportal`. Kamu bisa menggunakan aplikasi Folder Sync seperti [FreeFileSync](https://freefilesync.org/).

![](assets-README/Pasted%20image%2020230123143506.png)

#### Ubah pengaturan di berkas PHP
Aplikasi ini belum mendukung file `.env`. Untuk itu, pengaturan pada aplikasi ini perlu diubah langsung ke berkas konfigurasi PHP langsung. Ada 3 langkah yang harus dilakukan:

##### Langkah 1 - Ubah pengaturan environment menjadi `development` di berkas `index.php`
Buka berkas `index.php` di direktori `centratama-hcportal-new`. Kemudian cari bari dengan kode sebagai berikut:
```php
...
/*
 *---------------------------------------------------------------
 * APPLICATION ENVIRONMENT
 *---------------------------------------------------------------
 *
 * You can load different configurations depending on your
 * current environment. Setting the environment also influences
 * things like logging and error reporting.
 *
 * This can be set to anything, but default usage is:
 *
 *     development
 *     testing
 *     production
 *
 * NOTE: If you change these, also change the error_reporting() code below
 */
	define('ENVIRONMENT', isset($_SERVER['CI_ENV']) ? $_SERVER['CI_ENV'] : 'development');
...
```

Pada syntax `define`, kamu bisa lihat terdapat pengaturan Environment `development` yang membuat HC Portal menampilkan semua pesan log saat eror terjadi. Ini membantu kita untuk melakukan proses *debugging*.

> Ingat saat menggelar (deploy) aplikasi ke lingkungan produksi, ubah pengaturan ini menjadi `production`

##### Langkah 2 - Pengaturan di berkas `...application/config/config.php`
Ada 2 hal yang harus dilakukan dengan berkas ini:

###### Ubah pengaturan host
Cari baris kode berikut:
```php
...
/*
|--------------------------------------------------------------------------
| Base Site URL
|--------------------------------------------------------------------------
|
| URL to your CodeIgniter root. Typically this will be your base URL,
| WITH a trailing slash:
|
|	http://example.com/
|
| WARNING: You MUST set this value!
|
| If it is not set, then CodeIgniter will try guess the protocol and path
| your installation, but due to security concerns the hostname will be set
| to $_SERVER['SERVER_ADDR'] if available, or localhost otherwise.
| The auto-detection mechanism exists only for convenience during
| development and MUST NOT be used in production!
|
| If you need to allow multiple domains, remember that this file is still
| a PHP script and you can easily do that on your own.
|
*/
$config['base_url'] = 'http://' . $_SERVER["HTTP_HOST"];
...
```

Kode di atas menggunakan superglobal variabel PHP (`$_SERVER`). Jika server kamu tidak mendukung dengan variabel tersebut, kamu bisa mencari di mana PHP menyimpan nama `HTTP_HOST` atau mengubahnya dengan alamat host `http://localhost`.

###### Ubah pengaturan kunci enkripsi
cari baris kode berikut:

```php
...
/*
|--------------------------------------------------------------------------
| Encryption Key
|--------------------------------------------------------------------------
|
| If you use the Encryption class, you must set an encryption key.
| See the user guide for more info.
|
| https://codeigniter.com/user_guide/libraries/encryption.html
|
*/
$config['encryption_key'] = 'ketikkanrandomstring';
...
```

Ubah kode enkripsi dengan memasukkan random string pada `ketikkanrandomstring`.

##### Langkah 3 - Ubah pengaturan basis data di berkas `..application/config/database.php`
Perlu diingat bahwa HC Portal memakai dua basis data, yaitu `hcportal_dev` dan `hcportal_archives`. Kamu harus mengubah kedua konfigurasi untuk kedua basis data tersebut. Beberapa konfigurasi yang harus kamu ubah:

| Konfigurasi  |                                                                                                                                                             |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `'hostname'` | kamu bisa mengisinya dengan alamat lokasi basis data, untuk pengembangan biasanya menggunakan alamat `localhost`                                            |
| `'username'` | Ubah dengan nama username basis data kamu.                                                                                                                  |
| `'password'` | Ubah dengan password basis data kamu.                                                                                                                       |
| `'database'` | Pastikan nama basis datanya sesuai. (`hcportal_dev` atau `hcportal_archives`)                                                                               |
| `'db_debug'` | Untuk lingkungan pengembangan pastikan nilainya sebagai berikut `(ENVIRONMENT !== 'production')`, Jika lingkungan produksi `(ENVIRONMENT === 'production')` |

#### Buat Controller `Test.php` di `application/controllers` {Optional}
Untuk mencoba kode program, kamu bisa membuat controller `Test.php` dan menjalankannya di browser-mu dengan alamat [http://localhost/test](http://localhost/test).

> Berkas `Test.php` telah diabaikan oleh git. Kamu bisa melihatnya di berkas `.gitignore` untuk memeriksanya.

### Deploy HC Portal ke lingkungan produksi (*Production Environment*)
Untuk melakukannya silakan lakukan kembali proses [persiapan pengembangan HC Portal](#pengembangan-hc-portal-dan-menjalankannya-dengan-nginx), Namun setel untuk lingkungan produksi. Silakan kunjungi laman web berikut untuk mempelajari instalasi dan keamanan di CodeIgniter:
- [https://codeigniter.com/userguide3/general/security.html](https://codeigniter.com/userguide3/general/security.html)
- [https://codeigniter.com/userguide3/installation/index.html](https://codeigniter.com/userguide3/installation/index.html)

---

Copyright © 2023 ryumada. All Rights Reserved.

Licensed under the [MIT](LICENSE) license.
