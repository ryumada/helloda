# Github Workflow
Github memiliki beberapa fitur yang sangat bermanfaat untuk mendokumentasikan proses pengembangan *software*. Mulai dari repositorinya yang dapat menyimpan artefak kode program aplikasi, sistem Git yang digunakan untuk membantu dalam mencatat perubahan yang terjadi pada pengembangan aplikasi, hingga ke fitur *issues* dan *pull-request* yang dapat digunakan untuk melakukan manajemen pengembangan *software*.

Jika kalian belum tau apa itu *issue* ataupun *pull-request*, referensi berikut menjelaskan keduanya:
- [Github Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues)
- [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests)

Di instruksi ini, kita akan membahas bagaimana alur pengembangan *software* dengan workflow Github. Mulai dari perencanaan pengembangan *software* dengan fitur issues sampai menggabungkan perubahan yang kita lakukan ke branch utama (*main*/*master*).

Setelah membuat repositori di Github, kita dapat melakukan beberapa persiapan untuk melakukan manajemen proyek.

## Langkah 1 - Persiapan awal
Terdapat 3 langkah untuk melakukan persiapan awal Github Workflow.
1. [Mengatur Github Labels](README-persiapan_awal/README-mengatur_github_labels.md)
2. [Membuat templat *pull-request* dan *issue*](README-persiapan_awal/README-membuat_templat_pull_request_dan_issue.md)
3. [Membuat Project](README-persiapan_awal/README-membuat_project.md)

## Langkah 2 - Mencatat atau mengumpulkan kebutuhan pengembangan software dengan membuat *issues*
Kita bisa melakukannya dengan membuat *issues* dan memberikannya label:
- `user-story` untuk mengumpulkan kebuthan.
- `bug` untuk membuat catatan eror aplikasi.
- dll. Silakan buka README [Github Labels](README-persiapan_awal/README-mengatur_github_labels.md) untuk memahami semua label yang tersedia secara *default*.

Sebelum membuat *issue*, ada 2 hal yang perlu diperhatikan:
- Tanyakan kembali pada dirimu sendiri kenapa kamu ingin membuat *issues*. Apakah manfaatnya untuk pengembang dan pengguna software di repositori tersebut. 
- Gunakan `issue template` yang sudah ada di repositori atau bila tidak ada templat berikan informasi sejelas mungkin terkait *issue* yang ingin dibuat. Hal ini bisa dilakukan dengan menanyakan pada diri sendiri. Namun bila tidak tahu jawabannya, kamu bisa menanyakannya.

Ada beberapa atribut informasi yang dapat kita sertakan ke dalam issue yang kita buat, **namun bila tidak tahu apa yang harus diisi, lebih baik kosongkan saja**. Biarkan item-item ini disetel oleh para maintainer repositori. Alangkah lebih baik jika kamu:
- **Sebagai kontributor luar memberikan label yang sesuai** dengan topik issue yang kamu buat.
- **Sebagai maintainer repositori menyetel semua atribut informasi**.

Berikut atribut informasi yang terdapat pada *issue* Github:

|   Atribut   | keterangan                                                                                  |
|:-----------:| ------------------------------------------------------------------------------------------- |
|  Assignees  | Berikan tugas kepada kontributor terkait issue ini.                                         | 
|   Labels    | Kaitkan dengan label topik terkait.                                                         |
|   Project   | Kaitkan dengan Github Project.                                                              |
|  Milestone  | Kaitkan dengan milestones yang ditetapkan dalam pengerjaan proyek di jangka waktu tertentu. |
| Development | Menampilkan branch dan pull-requests yang terkait dengan issue ini.                         |

> Untuk atribut `Assignees`, `Project`, dan `Milestone`, lebih baik diisi oleh para maintainer repositori.

> Atribut `Development` hanya tersedia oleh para maintainer repositori saja.

## Langkah 3 - Manajemen tugas dengan Github Project
Satu iterasi dapat dilakukan selama 1, sampai 4 minggu. Kita dapat memberikan bobot estimasi di masing-masing tugas berdasarkan jumlah hari yang diperlukan untuk menyelesaikannya. Misalnya pada gambar berikut:

![](assets-README/Pasted%20image%2020230501111831.png)

Bobot estimasi yang diberikan untuk tugas tersebut adalah 2 yakni 2 hari. Ini menandakan bahwa tugas itu dapat diselesaikan selama 2 hari. Tugas-tugas lainnya juga dapat diberikan bobot estimasi seperti itu.

![](assets-README/Pasted%20image%2020230501112111.png)

Untuk menentukan iterasi, kita dapat ke menu settings:
![](assets-README/Pasted%20image%2020230501112224.png)

Lalu ke menu iteration:
![](assets-README/Pasted%20image%2020230501112256.png)

Di sana, kita bisa menentukan jadwal pengerjaan iterasinya dengan mengeklik rentang tanggal pada tiap iterasinya.

Setelah iterasi dibuat, selanjutnya adalah menentukan prioritas tugas mana yang dapat dikerjakan di iterasi pertama dan  selanjutnya. Namun lebih baik, kita dapat fokus untuk mengerjakan iterasi pengembangan yang akan kita lakukan terlebih dahulu, yakni iterasi pertama.

Terkadang, pembuatan tugas-tugas sulit untuk dilakukan. Kita dapat membuat **Epic** untuk mendefinisikan tujuan pengembangan secara lebih luas. Setelah itu, kita dapat menentukan tugas-tugas kecilnya. Seperti pada gambar berikut:
![](assets-README/Pasted%20image%2020230501112848.png)

Tujuan utama dari pengembangan ini ada 2, yakni pembuatan akses material *training* yang lebih mudah dan forum training yang memungkinkan sebagai sarana untuk berbagi dari apa yang sudah dipelajari. Mereka dapat menanyakan materi yang belum mereka pahami dengan rekan mereka di modul *training* tersebut.

Kita dapat menghubungkan tugas-tugas kecil ke satu epic ini. Atau kita dapat membuat epic terlebih dahulu, baru setelah itu menentukan tugas-tugas kecil yang dapat dilakukan untuk mencapai tujuan tersebut.
![](assets-README/Pasted%20image%2020230501113326.png)

## Langkah 4 - Menjalankan Iterasi
Langkah pertama untuk menjalankan iterasi adalah dengan masuk ke tab `current iteration`, lalu kita bisa pindahkan kartu tugas ke dalam daftar `📋 Backlog`. 
![](assets-README/Pasted%20image%2020230521064758.png)

Dalam tahapan `📋 Backlog`, *issue* didefinisikan secara lebih detail dengan menambahkan desain aplikasinya atau membuat test cases seperti pada gambar di bawah ini.

![](assets-README/Screen%20Shot%202023-05-21%20at%2006.53.04.png)

Desain aplikasi yang dibuat pada gambar di atas adalah desain Mockup dan UML. Kemudian, di sana juga terdapat test cases yang dibuat dengan Format [Syntax Gherkin](https://cucumber.io/docs/gherkin/reference/).

Setelah pembuatan spesifikasinya selesai dan sudah ada bayangan bagaimana nanti logika programnya dibuat, kemudian kita dapat memindahkan issue tersebut ke daftar `🔖 Ready`. Kita dapat melanjutkan untuk membuat Backlog di issue lainnya.

![](assets-README/Pasted%20image%2020230521070330.png)

Atau, kita dapat memulai pengembangannya terlebih dahulu dengan memindahkannya langsung ke `🏗 In progress`.

![](assets-README/Pasted%20image%2020230521070620.png)

Di setiap *issue*, kita dapat membuat [branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches) untuk melakukan pengembangan yang spesifik di satu *issue*. Pada hakikatnya, kita harus membuat branch baru apabila ingin mengembangkan satu fitur. Biasanya satu fitur dikembangkan oleh satu pengembang atau developer. Hal ini membuat kolaborasi pengembangan *Software* menjadi lebih mudah untuk dilakukan.[^1]

![](assets-README/Pasted%20image%2020230521070151.png)

Apabila ingin mencatat perubahan secara lebih detail, kita dapat menggunakan Pull Request untuk mencatat perubahan yang detail tersebut. Kita dapat membuat branch baru (`dev-submission-training#stage2`) yang mencatat perubahan yang lebih detail. Lalu, kita dapat membuat pull-request ke  branch yang dibuat dengan *issue* (`dev-submission_training`).

![](assets-README/Screen%20Shot%202023-05-21%20at%2007.21.431.png)

Kita dapat menambahkan *issue reference*, menambahkan catatan baru, melihat perubahan yang terjadi pada branch. Lalu diakhir kita dapat melakukan Squash and Merge untuk menggabungkan perubahan tersebut menjadi 1 commit di branch *issue* (`dev-submission_training`). 

## Langkah 5 - Memindahkan tugas ke in-review bila sudah selesai
Jika pengembangan fitur dari aplikasi sudah selesai dan sudah memenuhi dari issue yang telah dibuat, kita dapat memindahkan issue tersebut ke daftar in-review. Setelah itu, kita dapat melanjutkan reviu fitur dengan membuat *pull-request*.

![](assets-README/Screenshot%202023-06-01%20112718.png)

## Langkah 6 - Buat pull-request
Langkah selanjutnya adalah membuat pull-request untuk mencatat pengembangan walaupun suatu saat branch yang kita pakai untuk mengembangkan fitur tersebut dihapus. Catatan perubahan akan tetap tersimpan dalam *pull-request* ini.

![](assets-README/Screen%20Shot%202023-06-01%20at%2011.41.09.png)

## Langkah 7 - Memproses pull-request atau menunggu di-merge
Jika Anda adalah seorang kontributor, Anda dapat menunggu pemilik repositori untuk menerima atau memberikan balasan terkait perubahan yang telah ada lakukan di *pull-request* tersebut. Anda mungkin akan terlibat diskusi di *pull-request* tersebut untuk membahas perubahan anda. Pemilik repositori juga dapat mengecek baris demi baris kode dan memberikan komentar yang mengarah ke baris kode langsung untuk menanyakan terkait logika kode yang telah Anda buat.

Tampilan berikut memuat daftar perubahan yang telah Anda lakukan di *pull-request* Anda. Daftar perubahan ini akan tersimpan walaupun branch pengembangan Anda telah dihapus.

![](assets-README/Pasted%20image%2020230601115517.png)

Jika Anda sebagai kontributor atau pemilik repositori, Anda dapat memberikan komentar dan reviu per baris kode dan menanyakan terkait logika perubahan kode yang telah dibuat.

![](assets-README/Pasted%20image%2020230601120349.png)

Jika perubahan *pull-request* sudah siap untuk digabungkan dengan branch utama, kita dapat menggabungkan *pull-request* dengan 3 aksi ini.
- **Create a merge commit** → mode normal dalam menggabungkan perubahan di *pull-request* dengan branch utama yang mana akan membuat 1 commit baru dengan nama "Merge" untuk menandai bahwa di perubahan tersebut terjadi penggabungan branch.
- **Squash and merge** → beberapa commit yang ada di *pull-request* ini akan digabungkan menjadi 1 commit di branch utama yang digabungkan. Fitur ini sangat berguna jika Anda melakukan commit di setiap perubahan kecil ketimbang dalam per fitur. Jadi commit-commit perubahan terkecil tersebut tidak akan mengotori riwayat commit di branch utama.
- **Rebase and merge** → beberapa commit yang ada di *pull-request* akan dimasukkan ke dalam branch utama tanpa membuat branch baru. Ini membuat seolah-olah perubahan yang ada di *pull-request*  dilakukan di branch utama.

![](assets-README/Pasted%20image%2020230601130745.png)

Pada gambar di atas, saya menggunakan fitur Squash and merge untuk menggabungkan semua perubahan yang ada di *pull-request* menjadi 1 commit. Kemudian pada gambar di bawah ini, perubahan commit pada *pull-request* akan diambil secara otomatis oleh Github dan dimasukkan ke dalam pesan commit. Kita dapat mengubah judul dan pesan commit-nya.

![](assets-README/Screen%20Shot%202023-06-01%20at%2013.25.12.png)

Setelah tombol confirm merge warna hijau diklik, *pull-request* akan otomatis berubah statusnya menjadi "**Merged**" yang menandakan bahwa perubahan pada *pull-request* ini telah digabungkan.

![](assets-README/Pasted%20image%2020230601133221.png)

## Langkah 8 - Melanjutkan ke iterasi selanjutnya
Langkah selanjutnya adalah memindahkan issue ke dalam daftar tugas `✅ Done`. Setelah itu kita dapa fokus ke pengembangan fitur selanjutnya. di daftar `📋 Backlog` atau `🆕 New`.

![](assets-README/Pasted%20image%2020230601132541.png)

Kita juga dapat memindahkan beberapa issue dari iterasi sebelumnya ke iterasi saat ini, jika pengerjaan fitur pada iterasi sebelumnya belum selesai dengan mengunjungi tab `Roadmap`. 

![](assets-README/Pasted%20image%2020230601133740.png)

Kita dapat melakukan *drag and drop* keempat issue tersebut ke kanan dan menjalankannya di iterasi ketiga.

![](assets-README/Pasted%20image%2020230601133956.png)

Selanjutnya kita akan menjalankan kembali workflow Github ini dari langkah ke dua sampai semua issue yang telah kita tetapkan sebelumnya berhasil dikembangkan ke dalam aplikasi HC Portal. 


[^1]:Schmitt, J. (2023, March 7). _Git tags vs branches: Differences and when to use them_ [Blog]. CircleCI. [https://circleci.com/blog/git-tags-vs-branches/](https://circleci.com/blog/git-tags-vs-branches/)
