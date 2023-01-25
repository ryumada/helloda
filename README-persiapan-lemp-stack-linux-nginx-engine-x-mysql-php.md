# Persiapan LEMP Stack (Linux, Nginx {Engine-X}, MySQL, PHP)
Sebelum memulai persiapan, perlu diperhatikan bahwa langkah berikut dijalankan pada perangkat dengan [Ubuntu](https://ubuntu.com/) dengan *Flavor* **[KDE NEON](https://neon.kde.org)**. Gunakan `apt` jika distribusi linux yang kamu gunakan adalah [Ubuntu](https://ubuntu.com/), atau gunakan `pkcon` jika distribusi linux yang kamu gunakan adalah **[KDE Neon](https://neon.kde.org)**.

Terdapat 4 langkah untuk menyiapkan **LEMP Stack**:
1. [Pemasangan Web Server Nginx dan Konfigurasi Firewall](#pemasangan-web-server-nginx-dan-konfigurasi-firewall)
2. [Pemasangan Mesin Basis Data (Database Engine) MySQL](#pemasangan-mesin-basis-data-database-engine-mysql)
3. [Pemasangan PHP 7.4](#pemasangan-php-74)
4. [Konfigurasi Nginx untuk menggunakan pemrosesan PHP](#konfigurasi-nginx-untuk-menggunakan-pemrosesan-php)

## Pemasangan Web Server Nginx dan Konfigurasi Firewall
Web server digunakan untuk menjalankan aplikasi HC Portal dan menampilkannya ke para pengguna. Ia bertugas untuk menerima permintaan dari pengguna, memprosesnya dengan kode program tertentu, dan mengirimkan respon kembali ke pengguna.

### Langkah 1 - Pemasangan Web Server [nginx](https://www.nginx.com)
Perbarui paket apt atau pkcon dengan perintah berikut ini. Gunakan `apt` jika distribusi linux yang kamu pakai Ubuntu, atau gunakan `pkcon` jika menggunakan KDE Neon.

|   apt (Ubuntu)    |  pkcon (KDE Neon)   | 
|:-----------------:|:-------------------:|
| `sudo apt update` | `sudo pkcon update` |

Pasang `Nginx` dengan perintah berikut ini.
|       apt (Ubuntu)       |      pkcon (KDE Neon)      | 
|:------------------------:|:--------------------------:|
| `sudo apt install nginx` | `sudo pkcon install nginx` |

> - Ketika proses tertahan, ketik `y` untuk melanjutkan proses pemasangan.
> - Kemudian tunggu hingga selesai proses pemasangan `nginx` sebelum melanjutkan ke langkah selanjutnya.
> - Jika sudah selesai, maka `nginx` akan secara otomatis diaktifkan. Untuk memastikannya, kamu bisa mencoba perintah bash berikut: `sudo systemctl status nginx`.

### Langkah 2 - Pengaturan Firewall
Langkah ini ditujukan untuk mengizinkan akses masuk dari internet ke server-mu.

Cek status firewall kamu, pastikan pengaturan default *incoming*  adalah *reject* dan pengaturan *outgoing* adalah *allow*.
```bash
sudo ufw status verbose
```

Output:
```output
Status: active
Logging: on (low)
Default: reject (incoming), allow (outgoing), disabled (routed)
New profiles: skip

...
```

Saat memasang `nginx`, `application profile` juga ditambahkan ke `ufw`. Ini akan memudahkan kita dalam memberikan akses firewall untuk `nginx`. Kita bisa mengecek daftar `aplication profile` dengan perintah berikut:
```bash
sudo ufw app list
```

Output:
```output
Available applications:
  CUPS
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
```

Dari output di atas, dapat kita lihat beberapa profil untuk web server Nginx. Kita akan menggunakan HTTP untuk persiapan lingkungan pengembangan aplikasi web HC Portal. Perintah di bawah ini akan mengizinkan `application profile` **Nginx HTTP** yang mana mengizinkan akses incoming ke port `80`.

```bash
sudo ufw allow "Nginx HTTP"
```

Setelah itu, kita dapat memastikan bahwa pengaturan `application profile` **Nginx HTTP** telah ditambahkan ke `firewall rule list`.

```shell
sudo ufw status
```

Output:
```output
Status: active

To                         Action      From
--                         ------      ----
Nginx HTTP                 ALLOW       Anywhere                  
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
...
```

Cari `firewall rule` dengan nama *To* **Nginx HTTP**. Pastikan `Action` dari *rule*-nya adalah `ALLOW`, dan nilai nilai `From` adalah `Anywhere`.

### Langkah 3 - Memastikan Web Server Nginx berjalan dengan baik
Caranya adalah dengan mengunjungi [http://localhost](http://localhost) di web browser kamu. Ketika web browser menunjukkan halaman dengan gambar seperti berikut ini, maka itu tandanya web server telah berjalan dengan baik.

![](assets-README/Pasted%20image%2020230105120514.png)

### Langkah 4 - Menghindari eror `413 - Request entity too large` pada Nginx
Caranya adalah dengan meningkatkan ukuran max body yang dapat ditangani oleh server.[^10] Pada Nginx, konfigurasi `client_max_body_size 100M;` akan membuat server dapat menangani ukuran maksimal body request sebesar 100MB.

Buat berkas konfigurasi `.conf` di `/etc/nginx/conf.d`.
```bash
sudo vi 413-request_entity_too_large.conf
```

Tekan tombol `I`, lalu masukkan konfigurasi tersebut.
```nginx
client_max_body_size 100M;
```

Tekan tombol `:` lalu ketikkan `wq` dan tekan tombol `Enter`.

Setelah itu jangan lupa untuk mengecek konfigurasi dan me-*restart* web server Nginx dengan perintah `sudo nginx -t` dan `sudo systemctl restart nginx`.

### Langkah 5 - Menghindari eror `504 Gateway Time-out` pada Nginx
Caranya adalah dengan membuat beberapa konfigurasi berikut di direktori `/etc/nginx/conf.d`. Sebelumnya buat berkas konfigurasinya.

```bash
sudo vi 504-gateway_time_out.conf
```

Tekan tombol `I`, lalu masukkan konfigurasi berikut.[^11]
```Nginx
proxy_connect_timeout 300s;
proxy_send_timeout 300s;
proxy_read_timeout 300s;
fastcgi_send_timeout 300s;
fastcgi_read_timeout 300s;
```

Konfigurasi tersebut akan menambahkan waktu selama 5 menit untuk memproses request dengan proxy atau fastcgi.

Selanjutnya, tekan tombol `:` lalu ketikkan `wq` dan tekan tombol `Enter`.

Setelah itu, jangan lupa untuk mengecek konfigurasi dan me-*restart* web server Nginx dengan perintah `sudo nginx -t` dan `sudo systemctl restart nginx`.

## Pemasangan Mesin Basis Data (Database Engine) MySQL
Basis data digunakan sebagai media penyimpanan data. Jenis basis data yang digunakan pada aplikasi web HC Portal adalah relasional. Itulah mengapa kita perlu memasang MySQL.

### Langkah 1 - Pemasangan `mysql-server`
Pasang *software* server MySQL dengan perintah berikut ini:

|          apt (Ubuntu)           |         pkcon (KDE Neon)          |
|:-------------------------------:|:---------------------------------:|
| `sudo apt install mysql-server` | `sudo pkcon install mysql-server` |

### Langkah 2 - Membuat akun user selain root MySQL
Kita tidak akan menggunakan `mysql_secure_installation`, karena MySQL server ini tidak digunakan untuk lingkungan produksi. Kita akan membuat akun baru yang akan digunakan oleh aplikasi HC Portal untuk mengakses server basis data MySQL.

Sebelumnya, masuk ke MySQL shell.

```bash
sudo mysql
```

Lalu kita jalankan query berikut untuk membuat akun baru:

> Ganti:
> - `namauser` dengan nama user yang kamu inginkan.
> - `PasswordBaru` dengan password baru.

```sql
CREATE USER 'namauser'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PasswordBaru';
```

Nantinya password tersebut akan digunakan untuk mengoneksikan aplikasi web HC Portal yang mana menggunakan PHP ke basis data MySQL.

Gunakan perintah berikut untuk memberikan akses super-root ke akun `namauser`.
```sql
GRANT ALL PRIVILEGES ON *.* TO 'namauser'@'localhost' WITH GRANT OPTION;
```

> ⚠️ PERHATIAN ⚠️
> cara di atas hanya digunakan untuk lingkungan pengembangan, pelajari cara menyetel mysql untuk lingkungan produksi.[^1]

## Pemasangan PHP 7.4
Walaupun PHP 7.4 sudah tidak didukung[^4], aplikasi HC Portal masih memerlukannya karena PHP framework yang digunakan untuk menjalankan aplikasi web ini adalah CodeIgniter versi 3.1.11.[^3]

Apache menanamkan PHP interpreter dan akan dijalankan setiap kali ada permintaan untuk website yang menggunakan bahasa pemrograman PHP. Nginx memerlukan program luar untuk untuk menangani pemrosesan PHP dan bertindak sebagai jembatan penghubung ke PHP interpreter itu sendiri. Cara ini membuat pemrosesan PHP menjadi lebih optimal pada banyak laman web berbasis PHP, namun ini memerlukan konfigurasi tambahan.

Kamu akan membutuhan `php7.4-fpm`, yang mana kepanjangannya adalah "PHP FastCGI process manager". Kemudian kamu akan membutuhkan `php7.4-mysql` untuk menghubungkan PHP dengan basis data MySQL.

Namun sebelum itu, kamu perlu menambahkan `apt-repository` **Ondřej Surý PPA** untuk dapat memasang `php7.4-fpm` dan `php7.4-mysql`.[^5]

```bash
sudo add-apt-repository ppa:ondrej/php
```

Kemudian update apt:

```bash
sudo apt update
```

Terakhir, barulah kita bisa menjalankan kode berikut:

|          apt (Ubuntu)           |         pkcon (KDE Neon)          |
|:-------------------------------:|:---------------------------------:|
| `sudo apt install php7.4-fpm php7.4-mysql` | `sudo pkcon install php7.4-fpm php7.4-mysql` |

### Meningkatkan ukuran Post dan Upload file untuk PHP
Caranya adalah dengan mengubah konfigurasi di `/etc/php/7.4/fpm/php.ini`. Cari konfigurasi dengan nama berikut lalu ubah nilainya ke yang lebih besar.

```php
post_max_size = 200M
upload_max_filesize = 200M
```

Setelah itu, jangan lupa untuk me-*restart*  php7.4-fpm dengan perintah `sudo systemctl restart php7.4-fpm`.

## Konfigurasi Nginx untuk menggunakan pemrosesan PHP
### Langkah 1 - Membuat berkas konfigurasi aplikasi web
Nginx membaca direktori `/var/www/html` secara default. Direktori tersebut hanya dapat mengolah satu website saja dan tidak cocok untuk pengelolaan banyak website, untuk itu di langkah ini kita akan membuat folder Nginx dapat mengelola lebih dari satu website.

Kita akan membuat direktori baru untuk aplikasi web HC Portal yang dinamai `hcportal`. Buatlah direktori root web untuk aplikasi HC Portal.

```bash
sudo mkdir /var/www/hcportal
```

Selanjutnya, ubah ownership dari direktori `hcportal` ke akun user kamu. Variabel `$USER` menyimpan nama user kamu di linux.

```bash
sudo chown -R $USER:$USER /var/www/hcportal
```

Kemudian, buka berkas pengaturan di direktori `sites-available` Nginx dengan *command-line* editor seperti `nano` atau `vim`. Di sini kita akan menggunakan vim.

```bash
sudo vi /etc/nginx/sites-available/hcportal
```

Lalu tekan tombol `I` di keyboard untuk masuk ke mode INSERT, masukkan kode konfigurasi berikut ke berkasnya:

```nginx
server {
  listen 80 default_server;  
  listen [::]:80 default_server;
  root /var/www/hcportal;

  index index.php index.html index.htm;

  server_name _;

  location / {
    try_files $uri $uri/ /index.php;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
  }

  location ~ /\.ht {
    deny all;
  }
}
```

Berikut penjelasan dari sintaksis di atas:
- `listen` = Mendefinisikan port yang akan digunakan aplikasi HC Portal. Di sini kita menggunakan port 80 yang merupakan port default HTTP.
- `root` = Mendefinisikan direktori root di mana website disimpan.
- `index` = Mendefinisikan urutan prioritas file index website ini. Kita akan menggunakan `index.php` sebagai prioritas utama. Namun pada praktik di dunia industri, kita lebih baik memprioritaskan `index.html` terlebih dahulu untuk memudahkan dalam mengganti *landing page* website ketikan ingin melakukan *maintenance*.
- `server_name` = Mendefinisikan nama domain dan/atau alamat IP server ini. Kita akan menyetelnya dengan karakter garis bawah (`_`) untuk lingkungan pengembangan HC Portal. Namun pada lingkungan produksi, kita bisa dengan alamat domain kita seperti berikut:
```nginx
server_name hcportal www.hcportal;
```
- `location /` = Blok lokasi awal dengan `try_files` yang mana mengecek eksistensi dari berkas-berkas atau direktori dari URL yang cocok. Jika tidak ada yang cocok, Nginx akan merespon eror 404.

> Directive `try_files` pada `location /` akan menghapus ekstensi .php dari url.[^6]

- `location ~ \.php$` = blok ini menangani pemrosesan PHP dengan meng-*include* pengaturan `fastcgi-php.conf` dan berkas `php7.4-fpm.sock`  mendeklarasikan socket yang berhubungan dengna `php7.4-fpm`.
- `location ~ /\.ht` = blok ini akan mengabaikan berkas `.htaccess` yang mana tidak bisa digunakan di Nginx.[^7] Blok ini tidak akan mengizinkan pengguna untuk mengakses berkas tersebut.

Jika sudah selesai, kita bisa menyimpan berkasnya dengan menekan tombol keyboard:[^8]
1. `Esc` = Untuk keluar dari mode Insert.
2. `:` = Untuk memasukkan perintah.
3. Ketikkan `wq` untuk menyimpan perubahan dan keluar dari `vim`.

### Langkah 2 - Mengaktifkan berkas pengaturan `hcportal` dan menonaktifkan berkas konfigurasi `default`
Aktivasi konfigurasi `hcportal` dengan membuat *soft-link*[^9] ke direktori `sites-enabled`.

```bash
sudo ln -s /etc/nginx/sites-available/hcportal /etc/nginx/sites-enabled/
```

Lalu nonaktifkan berkas konfigurasi `default` dengan `unlink` berkasnya di direktori `sites-enabled`.

```bash
sudo unlink /etc/nginx/sites-enabled/default
```

> Untuk mengaktifkan kembali pengaturan `default`, kamu bisa menggunakan cara yang sama untuk mengaktifikan konfigurasinya dengan *soft-link* dan menonaktifkan berkas konfigurasi `hcportal` dengan meng-`unlink`-nya.

### Langkah 3 - Tes konfigurasi Nginx
Kita bisa melakukannya dengan menjalankan perintah berikut untuk melakukan testing konfigurasi Nginx yang baru saja kita buat dan aktifkan.

```bash
sudo nginx -t
```

Pastikan konfigurasi menunjukkan output berikut yang menunjukkan bahwa konfigurasi yang kita buat tidak memiliki eror. Jika masih ada eror, kamu bisa mengecek berkas pengaturannya lagi dan jalankan kembali perintah di atas sampai menunjukkan Output seperti di bawah ini.

Output:
```output
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok  
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

### Langkah 4 - Reload service Nginx
Kita bisa melakukannya dengan menjalankan perintah berikut:

```bash
sudo systemctl reload nginx
```

### Langkah 5 - Tes PHP dengan Nginx
Buat berkas `index.php` di direktori `/var/www/hcportal/index.php`.

```bash
vi /var/www/hcportal/index.php
```

Lalu masukkan kode PHP berikut di berkas tersebut.

```php
<?php
phpinfo();
?>
```

Setelah itu kita bisa mengunjungi [http://localhost](http://localhost) untuk melihat apakah PHP sudah bekerja dengan baik. Jika sudah bekerja dengan baik, maka akan muncul tampilan web seperti berikut:
![](assets-README/Pasted%20image%2020230118133725.png)

---

Copyright © 2023 ryumada. All Rights Reserved.

Licensed under the [MIT](LICENSE) license.

## Referensi
[^1]:Heidi, E., & Horcasitas, J. (2022, April 26). How To Install Linux, Nginx, MySQL, PHP (LEMP stack) on Ubuntu 22.04 [Blog]. DigitalOcean. https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04
[^2]:Simic, S. (2018, October 21). _How to Change MySQL Root Password in Linux or Windows_ [Blog]. Knowledge Base by PhoenixNAP. [https://phoenixnap.com/kb/how-to-reset-mysql-root-password-windows-linux](https://phoenixnap.com/kb/how-to-reset-mysql-root-password-windows-linux)
[^3]:rahulswt7. (2014, October). _Surprised to see codeigniter 3.x running successfull with PHP 8.0 as well._ [Forum]. CodeIgniter Forum. [https://forum.codeigniter.com/showthread.php?tid=78091&pid=383504#pid383504](https://forum.codeigniter.com/showthread.php?tid=78091&pid=383504#pid383504)
[^4]:The PHP Group. (2023). _PHP: Supported Versions_ [Official Website]. PHP. [https://www.php.net/supported-versions.php](https://www.php.net/supported-versions.php)
[^5]:Kili, A. (2021, January 12). _How to Install Different PHP (5.6, 7.0 and 7.1) in Ubuntu_ [Blog]. Tecmint #1 Linux Blog. [https://www.tecmint.com/install-different-php-versions-in-ubuntu/](https://www.tecmint.com/install-different-php-versions-in-ubuntu/)
[^6]:AbuShady, M. (2014, February 20). _Answer to “How to remove both .php and .html extensions from url using NGINX?”_ [Forum]. Stack Overflow. [https://stackoverflow.com/a/21915845/11332583](https://stackoverflow.com/a/21915845/11332583)
[^7]:Nginx. (2023). _Like Apache: .Htaccess_ [Wiki]. Nginx Wiki. [https://www.nginx.com/resources/wiki/start/topics/examples/likeapache-htaccess/](https://www.nginx.com/resources/wiki/start/topics/examples/likeapache-htaccess/)
[^8]:Torruellas, R. (2023). _Vim Cheat Sheet_ [Single Page Website]. Vim Cheat Sheet. [https://vim.rtorr.com/](https://vim.rtorr.com/)
[^9]:Gite, V. (2007, September 25). _How to: Linux / UNIX create soft link with ln command_ [Tutorial]. NixCraft. [https://www.cyberciti.biz/faq/creating-soft-link-or-symbolic-link/](https://www.cyberciti.biz/faq/creating-soft-link-or-symbolic-link/)
[^10]:K, Y. (2019, June 10). Cara Cepat Mengatasi Error 413 Request Entity Too Large [Blog]. _Niagahoster Blog_. [https://www.niagahoster.co.id/blog/413-request-entity-too-large/](https://www.niagahoster.co.id/blog/413-request-entity-too-large/)
[^11]:Kuzma Ivanov. (2023). _An operation or a script that takes more than 60 seconds to complete fails on a website hosted in Plesk: Nginx 504 Gateway Time-out_ [Blog]. Plesk Help Center. [https://support.plesk.com/hc/en-us/articles/115000170354-An-operation-or-a-script-that-takes-more-than-60-seconds-to-complete-fails-on-a-website-hosted-in-Plesk-nginx-504-Gateway-Time-out](https://support.plesk.com/hc/en-us/articles/115000170354-An-operation-or-a-script-that-takes-more-than-60-seconds-to-complete-fails-on-a-website-hosted-in-Plesk-nginx-504-Gateway-Time-out)
[^12]:ikzi. (2014, June 13). _Answer to “Nginx CodeIgniter remove index.php in the URL”_ [Forum]. Stack Overflow. [https://stackoverflow.com/a/24199646/11332583](https://stackoverflow.com/a/24199646/11332583)
