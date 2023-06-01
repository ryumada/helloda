# Membuat Project
Referensi berikut menunjukkan bagaimana membuat Github Project:
- [Creating a Project](https://docs.github.com/en/issues/planning-and-tracking-with-projects/creating-projects/creating-a-project#creating-a-project)[^1]

Di referensi ini kalian bisa memahami lebih lanjut tentang konsep manajemen project dengan Agile:
- [https://www.atlassian.com/agile/project-management](https://www.atlassian.com/agile/project-management)[^2]

Pada repositori ini, saya membuat project dengan templat `Feature`. Saya menggunakan templat ini untuk menerapkan konsep iterasi pada pengembangan dengan *Iterative Model*.

![](../assets-README/Pasted%20image%2020230129213918.png)

## Memahami tampilan project
Terdapat 4 view pada project yang saya buat ini:
| nama tampilan     | keterangan                                                                                                        |
| ----------------- | ----------------------------------------------------------------------------------------------------------------- |
| Home              | Tampilan tabel yang berisi keseluruhan informasi project. Mulai dari iterasi, status, dan estimasi.               |
| Current Iteration | Tampilan board yang berisi daftar tugas yang harus diselesaikan di iterasi saat ini (biasanya dalam satu minggu). |
| Next Iteration    | Tampilan board yang berisi daftar tugas yang harus diselesaikan di iterasi selanjutnya.                           |
| Epics             | Tampilan board yang berisi daftar Epic (Bagian besar pekerjaan yang dibagi menjadi tugas-tugas kecil).            | 
| Planning          | Tampilan tabel yang berisi daftar tugas yang dikelompokkan dalam field iterasi.                                   |

Untuk lebih memahami tampilan-tampilan tersebut. Kalian harus memahami terlebih dahulu bagaimana proyek manajemen dengan Agile.[^2]

### Memahami view dan field pada project
Masing-masing view pada project terdiri dari beberapa field. Kita akan membahas per-view-nya.

#### Home
Tampilan awal yang berisi sekilas daftar tugas.

![](../assets-README/Pasted%20image%2020230501084044.png)

|      nama field      | keterangan                                                                                                                                                                         |
|:--------------------:| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|        Title         | Judul tugas yang biasanya berupa issue atau pull-request.                                                                                                                          |
|      Assignees       | Daftar orang yang terlibat dalam tugas.                                                                                                                                            |
|        Status        | Status progres tugas yang berupa 🆕 New, 📋 Backlog, 🔖 Ready, 🏗 In progress, 👀 In review, dan ✅ Done.                                                                        |
|      Iteration       | Menandakan pada iterasi ke-berapa tugas berada. (Iteration 1, Iteration 2, Iteration 3, ...).                                                                                      |
|       Estimate       | Menandakan seberapa rumit tugas bisa dinyatakan dalam story points. Baca terkait estimasi di referensi berikut: [https://www.atlassian.com/agile/project-management/estimation](https://www.atlassian.com/agile/project-management/estimation).[^3] | 
| Linked pull requests | Menunjukkan pull-request yang terhubung.                                                                                                                                           |
|        Labels        | Menunjukkan label tugas.                                                                                                                                                           |

#### Current Iteration, Next Iteration, & Epics (Memahami field Status)
Pada kedua tampilan ini menggunakan satu field yakni **Status**. Setiap status dikelompokkan dalam satu kartu. Tugas dapat dipindahkan dari satu kartu ke kartu selanjutnya sesuai status pengerjaannya. Cara kerja dengan board ini disebut dengan [Kanban Board](https://www.atlassian.com/agile/kanban/boards).

Berikut ketiga tampilannya:
- Tampilan **Current Iteration**
![Current Iteration View](../assets-README/Screen%20Shot%202023-05-01%20at%2008.44.24-fullpage.png)
- Tampilan **Next Iteration**
![Next Iteration View](../assets-README/Screen%20Shot%202023-05-01%20at%2008.45.45-fullpage.png)
- Tampilan **Epics**
Di tampilan ini terdapat filter `label:epic`, ini digunakan untuk hanya menampilkan issue yang memiliki label `epic` saja.
![Epics View](../assets-README/Screen%20Shot%202023-05-01%20at%2008.45.49-fullpage.png)

Field status memiliki 6 item untuk menunjukkan progres dari suatu tugas. Di antaranya sebagai berikut:

|   nama item   | keterangan                                                                                                                                                                                                                                                                  |
|:-------------:| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|    🆕 New     | Tugas baru untuk suatu iterasi.                                                                                                                                                                                                                                             |
|  📋 Backlog   | Tugas perlu diprioritaskan atau sedang dibahas kebutuhan pengembangannya (dalam tahap ini kemungkinan tugas bisa dipecah menjadi tugas-tugas yang lebih kecil). Lihat referensi berikut untuk memahaminya lebih lanjut: [https://www.atlassian.com/agile/scrum/backlogs](https://www.atlassian.com/agile/scrum/backlogs).[^4] | 
|   🔖 Ready    | Tugas siap untuk dikerjakan. Biasanya tugas yang diprioritaskan terlebih dahulu akan muncul di sini.                                                                                                                                                                        |
| 🏗 In progress | Tugas sedang dalam proses pengerjaan.                                                                                                                                                                                                                                       |
| 👀 In review  | Tugas sedang dalam proses reviu.                                                                                                                                                                                                                                            |
|    ✅ Done    | Tugas sudah selesai dikerjakan.                                                                                                                                                                                                                                             |

#### Planning
Tampilan ini berfokus pada perencanaan iterasi proyek. Untuk itu, tampilan ini daftar tugasnya dikelompokkan dalam field iterasi.

![](assets/Pasted%20image%2020230501084840.png)

Tampilan ini memiliki filter `-label:epic`. Filter ini menghapus *issue* dengan label `epic`. Epic tidak perlu dimasukkan ke dalam iterasi pengembangan, cukup tugas-tugas kecilnya saja.

| nama field | keterangan                                                                                                                                                                                                                                          |
|:----------:| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   title    | Nama tugas.                                                                                                                                                                                                                                         |
| Assignees  | Daftar orang yang terlibat dalam tugas.                                                                                                                                                                                                             |
| Iteration  | Menandakan pada iterasi ke-berapa tugas berada. (Iteration 1, Iteration 2, Iteration 3, ...). ==Daftar tugas dikelompokkan dalam field ini untuk menandakan kapan tugas harus dilaksanakan==.                                                       |
|  Estimate  | Menandakan seberapa rumit tugas bisa dinyatakan dalam story points. Baca terkait estimasi di referensi berikut: [https://www.atlassian.com/agile/project-management/estimation](https://www.atlassian.com/agile/project-management/estimation).[^3] |
|   Status   | Status progres tugas yang berupa 🆕 New, 📋 Backlog, 🔖 Ready, 🏗 In progress, 👀 In review, dan ✅ Done.                                                                                                                                            |

[^1]:Github. (2023, February 15). _Creating a project_ [Documentation]. GitHub Docs. [https://ghdocs-prod.azurewebsites.net/en/issues/planning-and-tracking-with-projects/creating-projects/creating-a-project](https://ghdocs-prod.azurewebsites.net/en/issues/planning-and-tracking-with-projects/creating-projects/creating-a-project)
[^2]:Drumond, C. & Atlassian. (2022). _Get started with agile project management_ [Blog]. Atlassian. [https://www.atlassian.com/agile/project-management](https://www.atlassian.com/agile/project-management)
[^3]:Radigan, D. & Atlassian. (2022). _What are story points and how do you estimate them?_ [Blog]. Atlassian. [https://www.atlassian.com/agile/project-management/estimation](https://www.atlassian.com/agile/project-management/estimation)
[^4]:Radigan, D. & Atlassian. (2022). _The product backlog: Your ultimate to-do list_ [Blog]. Atlassian. [https://www.atlassian.com/agile/scrum/backlogs](https://www.atlassian.com/agile/scrum/backlogs)
