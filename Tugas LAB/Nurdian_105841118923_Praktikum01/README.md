# 📋 Laporan Praktikum Pertemuan 01
## DevOps Culture & Principles

---

## 👤 Identitas Mahasiswa

| Item | Keterangan |
|------|------------|
| **Nama** | Nurdian |
| **NIM** | 105841118923 |
| **Kelas** | 5B |
| **Tanggal** | 2026-02-25 |

---

## 📚 Pemahaman DevOps

### Apa itu DevOps?

Menurut pandangan saya, DevOps bukan sekadar sebuah tren teknologi atau sekumpulan perangkat lunak (tools) seperti Docker dan Git yang baru saja saya pelajari. Lebih dari itu, DevOps adalah sebuah budaya atau filosofi kerja yang bertujuan untuk meruntuhkan "tembok penghalang" yang selama bertahun-tahun memisahkan dua kubu utama dalam dunia IT: tim Developer (pengembang yang fokus membuat fitur baru) dan tim Operations (pengelola infrastruktur yang fokus pada kestabilan server).

Sebelum adanya DevOps, kedua tim ini sering bekerja secara terisolasi. Dampaknya, sering muncul masalah klasik yang dikenal dengan istilah "it works on my machine", di mana kode berjalan lancar di laptop programmer tetapi mengalami error saat dipindahkan ke server produksi. Hal ini terjadi karena perbedaan lingkungan kerja dan kurangnya komunikasi antar tim. DevOps hadir sebagai solusi untuk menyatukan mereka dalam satu siklus hidup pengembangan yang utuh. Dengan DevOps, semua orang bertanggung jawab atas seluruh proses, mulai dari penulisan kode, pengujian, hingga pemeliharaan di server.

Mengapa DevOps sangat penting dalam industri software saat ini? Alasan utamanya adalah kecepatan dan kualitas. Di era digital sekarang, perusahaan tidak bisa lagi menunggu waktu berbulan-bulan hanya untuk merilis satu fitur baru. Dengan otomatisasi yang menjadi jantung dari DevOps (seperti CI/CD), perusahaan dapat melakukan rilis aplikasi ribuan kali dalam sehari dengan risiko kegagalan yang sangat minim. Otomatisasi ini memastikan bahwa setiap perubahan kode dites secara instan, sehingga kesalahan dapat ditemukan lebih awal sebelum sampai ke tangan pengguna.

Contoh nyata kesuksesan DevOps bisa kita lihat pada Netflix. Sebagai layanan streaming terbesar, mereka tidak pernah mengalami "down" meskipun melakukan pembaruan sistem terus-menerus. Mereka bahkan memiliki alat bernama Chaos Monkey yang sengaja merusak server mereka sendiri untuk memastikan sistem otomatis mereka sanggup memulihkan diri tanpa bantuan manusia. Selain itu, Amazon juga sukses menerapkan DevOps hingga mampu melakukan deployment kode baru rata-rata setiap 11,7 detik. Hal ini membuktikan bahwa DevOps adalah kunci utama bagi perusahaan teknologi untuk tetap kompetitif, inovatif, dan mampu memberikan pelayanan terbaik bagi pelanggannya.

### Mengapa DevOps Penting?

Mengapa DevOps Penting dalam Industri Software Saat Ini?
Alasan utama mengapa DevOps sangat krusial adalah karena ia menghapus sekat komunikasi antara tim Developer dan tim Operations. Dalam cara kerja tradisional, kedua tim ini sering bekerja secara terpisah, yang mengakibatkan proses rilis aplikasi menjadi lambat dan penuh dengan kesalahan teknis akibat perbedaan lingkungan server. DevOps hadir untuk menyatukan kedua sisi ini ke dalam satu alur kerja yang otomatis dan terintegrasi.

Berikut adalah beberapa poin utama urgensi DevOps:

Otomatisasi dan Efisiensi: Dengan DevOps, proses pengujian dan penyebaran kode (deployment) tidak lagi dilakukan secara manual. Penggunaan pipeline otomatis memastikan bahwa setiap perubahan kode dicek secara instan. Hal ini meminimalisir kesalahan manusia (human error) dan mempercepat fitur baru sampai ke tangan pengguna.

Stabilitas Lingkungan (Consistency): Menggunakan teknologi seperti Docker, DevOps menjamin bahwa aplikasi akan berjalan dengan cara yang sama di mana pun, baik itu di laptop pengembang maupun di server produksi. Ini menyelesaikan masalah klasik "di laptop saya jalan, di server tidak," yang sering menghambat produktivitas.

Skalabilitas dan Pemulihan Cepat: Di industri saat ini, aplikasi harus siap menghadapi lonjakan pengguna kapan saja. DevOps memungkinkan infrastruktur untuk berkembang secara otomatis sesuai beban trafik. Selain itu, jika terjadi kegagalan sistem, proses pemulihan dapat dilakukan jauh lebih cepat melalui sistem cadangan otomatis.

Secara keseluruhan, DevOps penting karena memungkinkan perusahaan untuk tetap kompetitif. Di dunia yang serba cepat ini, kemampuan untuk merilis pembaruan perangkat lunak dengan cepat, aman, dan stabil adalah kunci utama keberhasilan sebuah produk teknologi. Tanpa DevOps, proses pengembangan akan menjadi lambat, mahal, dan berisiko tinggi terhadap kegagalan sistem.

### Contoh Perusahaan yang Menerapkan DevOps

1. Amazon
Amazon merupakan salah satu pionir yang mengubah wajah industri melalui DevOps. Sebelum tahun 2001, mereka memiliki sistem monolitik yang sangat besar dan sulit dikelola.

Transformasi: Mereka beralih ke arsitektur microservices dan menerapkan budaya "you build it, you run it". Artinya, tim yang menulis kode juga bertanggung jawab penuh saat kode tersebut berjalan di server.

Hasil Nyata: Dengan otomatisasi pipeline yang sangat canggih, Amazon mampu melakukan deployment kode baru rata-rata setiap 11,7 detik. Hal ini memungkinkan mereka menambah fitur baru atau memperbaiki celah keamanan tanpa mengganggu pengalaman belanja jutaan penggunanya.

2. Netflix
Netflix sukses menerapkan DevOps untuk menjaga stabilitas layanan streaming mereka yang diakses oleh ratusan juta orang di seluruh dunia.

Transformasi: Mereka memigrasikan seluruh infrastruktur ke cloud dan membangun alat-alat otomatisasi sendiri. Salah satu yang paling terkenal adalah Chaos Monkey, sebuah program yang sengaja mematikan server mereka sendiri secara acak untuk menguji sejauh mana sistem otomatis mereka bisa pulih kembali.

Hasil Nyata: Netflix bisa melakukan ribuan perubahan kode setiap hari. Meskipun mereka melakukan pembaruan terus-menerus, kita sebagai penonton hampir tidak pernah merasakan aplikasi mereka down atau mengalami gangguan saat menonton film.

---

## 🎯 Pemahaman Prinsip CALMS

1. Culture (Budaya)
Budaya adalah inti dari DevOps. Fokusnya adalah menghilangkan "sekat" antara tim pengembang (Dev) dan operasional (Ops) agar bisa berkolaborasi dengan rasa tanggung jawab bersama.

Contoh Penerapan: Alih-alih menyalahkan tim server saat aplikasi crash, tim pengembang dan operasional duduk bersama melakukan post-mortem (evaluasi) untuk mencari solusi agar masalah tersebut tidak terulang kembali di masa depan.

2. Automation (Otomatisasi)
Prinsip ini bertujuan untuk menghilangkan tugas-tugas manual yang repetitif guna mengurangi kesalahan manusia (human error) dan mempercepat proses kerja.

Contoh Penerapan: Menggunakan Docker untuk mengemas aplikasi. Daripada menginstal database dan web server secara manual di tiap komputer, kamu cukup menjalankan perintah docker-compose up untuk menyiapkan seluruh lingkungan pengembangan secara otomatis.

3. Lean (Ramping)
Lean fokus pada penghapusan pemborosan (waste) dalam proses pengembangan. Tujuannya adalah bekerja dalam siklus kecil (iterasi), cepat, dan terus memberikan nilai tambah kepada pengguna.

Contoh Penerapan: Menggunakan GitFlow untuk mengerjakan fitur-fitur kecil secara bertahap. Daripada merilis satu aplikasi besar dalam 6 bulan, tim merilis pembaruan kecil setiap 2 minggu agar bisa segera mendapatkan feedback dari pengguna.

4. Measurement (Pengukuran)
Kamu tidak bisa meningkatkan apa yang tidak bisa kamu ukur. Prinsip ini menekankan pentingnya mengumpulkan data dan metrik untuk melihat performa aplikasi dan tim.

Contoh Penerapan: Memasang alat pemantauan (monitoring) untuk melihat berapa lama waktu yang dibutuhkan sejak kode ditulis hingga sukses dirilis ke server, atau memantau berapa banyak memori yang digunakan oleh kontainer Docker saat aplikasi dijalankan.

5. Sharing (Berbagi)
Berbagi pengetahuan dan alat di seluruh organisasi sangat penting untuk menghindari duplikasi pekerjaan dan meningkatkan keahlian tim secara kolektif.

Contoh Penerapan: Membuat dokumentasi di file README.md atau repositori GitHub tentang cara setup environment kerja. Jadi, ketika ada mahasiswa baru atau anggota tim baru masuk, mereka tidak perlu bingung karena panduannya sudah dibagikan secara transparan.

---

## 🔧 Setup Development Environment

### Versi Software

| Software | Versi |
|----------|-------|
| Git | git version 2.52.0.windows.1 |
| Docker | Docker version 29.1.3, build f52814d |

### Konfigurasi Git

```
 user.name "Nurdian"
 user.email "nurdiankrm@gmail.com"

```

### VS Code Extensions

1. Docker
2. Gitlens
3. Yaml
4. remote-containers

### GitHub Account

- Username: nurdianif

---

## 📸 Screenshots

| No | Screenshot | Keterangan |
|----|------------|------------|
| 1 | ![Git Version](screenshots/01-git-version.png) | Output git --version |
| 2 | ![Git Config](screenshots/02-git-config.png) | Output git config --list |
| 3 | ![Docker Version](screenshots/03-docker-version.png) | Output docker --version |
| 4 | ![Docker Hello World](screenshots/04-docker-hello-world.png) | Output docker run hello-world |
| 5 | ![VS Code](screenshots/05-vscode-extensions.png) | VS Code dengan extensions |

---

## ✅ Checklist

- [x] Git terinstall dan terkonfigurasi dengan benar
- [x] Docker dapat menjalankan container hello-world
- [x] VS Code terinstall dengan semua extensions yang diminta
- [x] Laporan ditulis dengan bahasa yang baik dan benar
- [x] Semua screenshot jelas dan terbaca

---

*Laporan ini dibuat pada Rabu, 25 Februari 2026*
