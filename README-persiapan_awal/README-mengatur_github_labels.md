# Mengatur Github Labels
Github Labels mengelompokkan *issue* ataupun *pull-request* ke dalam beberapa topik tertentu. Labels memudahkan kita untuk mengorganisir *issue* dan *pull-request*. Github label juga dapat digunakan untuk mengklasifikasikan *Discussions*, namun kita tidak membahasnya di instruksi ini.

## Memahami built-in label yang sudah ada
Terdapat 9 label secara *default* ditambahkan ke repositori baru di Github. Label-label ini telah dibahas pada dokumentasi di dokumentasi Github yang membahas [Managing Labels](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels)[^1]. Di sini kita akan membahas fungsinya satu per satu.

|     nama label     | fungsi                                                                                                                                            |
|:------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------- |
|       `bug`        | Mengindikasikan ada masalah yang tidak terduga atau hal yang tidak diinginkan pada aplikasi.                                                      |
|  `documentation`   | Mengindikasikan adanya kebutuhan untuk meningkatkan atau menambahkan penjelasan pada dokumentasi (di file README, wiki, website dokumentasi, dll). |
|    `duplicate`     | Mengindikasikan duplikat issue, pull-request, atau discussion.                                                                                    |
|   `enhancement`    | Mengindikasikan permintaan fitur baru.                                                                                                                |
| `good first issue` | Mengindikasikan issue yang baik untuk seorang kontributor baru.                                                                                   |
|   `help wanted`    | Mengindikasikan bahwa pengelola repositori memerlukan bantuan untuk issue atau pull-request kepada calon kontributor baru.                               |
|     `invalid`      | Mengindikasikan issue, pull request, atau discussion tidak lagi relevan dengan kondisi pengembangan *software* (out of the topic / OOT).          |
|     `question`     | Mengindikasikan bahwa sebuah issue, pull-request, atau discussion memerlukan informasi lebih.                                                     |
|     `wontfix`      | Mengindikasikan bahawa issue, pull-request, atau discussion tidak akan ditindaklanjuti.                                                           |

## Membuat Label Tambahan
Terkadang kita merasakan bahwa kesembilan label tersebut tidaklah cukup untuk memenuhi kebutuhan proyek. Hal ini wajar dan sering kali di proyek pengembangan *open-source* mereka menambahkan atau mengubah label-label tersebut untuk menyesuaikan dengan kebutuhan proyek.

Namun, hal yang perlu diingat adalah untuk memahami fungsi kesembilan label tersebut dan memaksimalkan penggunaannya ketimbang membuat label baru yang mungkin akan membingungkan dan menyulitkan pengorganisasian *issue*, *pull-request*, dan *discussion* nanti.

Pada proyek pengembangan ini, saya akan membuat beberapa label baru, seperti:

|   nama label   | fungsi                                                                                                        |
|:--------------:| ------------------------------------------------------------------------------------------------------------- |
| `dependencies` | Mengindikasikan bahwa ini berkaitan dengan dependensi software.                                               |
|     `epic`     | Mengindikasikan bahwa ini adalah bagian besar dari pekerjaan yang bisa dibagi lagi menjadi tugas-tugas kecil. | 
| `feature:core` | Mengindikasikan bahwa ini adalah fitur utama (*core*) dari software.                                          |
|  `user-story`  | Mengindikasikan bahwa ini ditulis dengan format user-story yang mana mencatat kebutuhan pengguna.             |

Kemudian saya juga mengubah label berikut:
|   nama lama   | nama baru             | keterangan                                                                                                                                                            |
|:-------------:| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `enhancement` | `feature:enhancement` | Ini karena `enhancement` memiliki fungsi yang serupa dengan label *core*. Untuk itu, label ini diberikan prefiks `feature:` untuk memudahkan dalam mengelompokkannya. |

[^1]:Github. (2023, March 22). _Managing labels_ [Documentation]. GitHub Docs. [https://ghdocs-prod.azurewebsites.net/en/issues/using-labels-and-milestones-to-track-work/managing-labels](https://ghdocs-prod.azurewebsites.net/en/issues/using-labels-and-milestones-to-track-work/managing-labels)
