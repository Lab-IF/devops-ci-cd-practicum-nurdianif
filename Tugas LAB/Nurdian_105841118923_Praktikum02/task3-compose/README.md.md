# 🐳 Laporan Praktikum Pertemuan 02
## Docker Fundamentals

---

## 👤 Identitas Mahasiswa

| Item | Keterangan |
|------|------------|
| **Nama** | Nurdian |
| **NIM** | 105841118923 |
| **Kelas** | 5B |
| **Tanggal** | 2026-02-25 |

---

## 📚 Pemahaman Docker

### Apa itu Docker?

Docker adalah platform yang memungkinkan kita untuk mengemas aplikasi ke dalam satu unit standar yang disebut kontainer. Slogannya yang terkenal adalah "Build once, run anywhere". Jadi, kamu tidak perlu pusing lagi menginstal manual satu per satu tools di server; cukup jalankan kontainer yang sudah kamu buat, seperti yang kamu lakukan saat menjalankan nginx:alpine tadi.

Kontainerisasi adalah teknologi di balik Docker yang cara kerjanya mirip seperti pengiriman barang lewat peti kemas di pelabuhan:

Isolasi: Tiap aplikasi punya "kotak" sendiri-sendiri. Jika satu aplikasi error atau butuh versi Python yang berbeda, dia tidak akan mengganggu aplikasi lain di laptopmu.

Ringan: Berbeda dengan Virtual Machine (VM) yang harus menginstal sistem operasi (OS) penuh di dalamnya, kontainer menumpang pada OS asli laptopmu tapi tetap terpisah secara sistem. Ini yang bikin Docker jauh lebih ringan dan cepat saat dijalankan.

Konsistensi: Karena semua kebutuhan aplikasi sudah dibungkus di dalam kontainer melalui Dockerfile, lingkungan kerjamu tidak akan berubah-ubah.

### Komponen Utama Docker

Dalam ekosistem Docker, terdapat tiga komponen utama yang saling bekerja sama untuk menjalankan aplikasi kamu. Memahami ketiga hal ini akan sangat membantu kamu dalam menyelesaikan Task 3 nanti, terutama saat mengelola proyek CRAFT-TECH:

1. Docker Images (Resep/Template)
Images adalah file statis yang bersifat read-only yang berisi semua instruksi untuk membangun kontainer.

Dapat diibaratkan sebagai "resep masakan" atau blueprint dari sebuah aplikasi.

Contohnya adalah file Dockerfile yang baru saja kamu buat; file tersebut nantinya akan di-build menjadi sebuah image.

2. Docker Containers (Aplikasi yang Berjalan)
Containers adalah unit yang berjalan secara nyata dari sebuah Image.

Jika Image adalah resepnya, maka Container adalah masakan yang sudah jadi dan siap dimakan.

Kamu bisa menjalankan, menghentikan (stop), dan menghapus (rm) kontainer berkali-kali tanpa merusak Image aslinya.

Screenshot "Welcome to nginx" yang kamu ambil tadi adalah bukti dari kontainer yang sedang aktif berjalan.

3. Docker Registry (Gudang Penyimpanan)
Registry adalah tempat untuk menyimpan dan membagikan Docker Images.

Docker Hub adalah registry publik yang paling populer, tempat di mana kamu melakukan perintah docker pull nginx:alpine tadi.

Registry memungkinkan tim pengembang untuk saling berbagi image aplikasi agar lingkungan pengembangan tetap konsisten di seluruh tim.

### Perbedaan Docker vs Virtual Machine

Virtual Machine (VM): Setiap VM menyertakan salinan lengkap sistem operasi (Guest OS), semua kode aplikasi, serta library yang diperlukan. VM berjalan di atas hypervisor yang membagi perangkat keras fisik menjadi beberapa bagian.

Docker Container: Kontainer berbagi kernel sistem operasi host (Windows pada laptopmu) dan hanya berisi aplikasi serta library pendukungnya. Kontainer jauh lebih efisien karena tidak perlu menjalankan banyak OS sekaligus.

---

## 🔧 Praktik Docker Commands

### Output docker ps -a

```
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS                   PORTS                                     NAMES
6f63a1e050ae   praktikum-docker:v1   "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes            0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   praktikum-web
66e91e19ae75   hello-world           "/hello"                 4 hours ago      Exited (0) 4 hours ago                                             naughty_germain
557d28d14120   hello-world           "/hello"                 4 hours ago      Exited (0) 4 hours ago                                             elegant_edison
```

### Output docker images

```
                                                                                                    i Info →   U  In Use
IMAGE                 ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest    ef54e839ef54       25.9kB         9.52kB    U
nginx:alpine          1d13701a5f9f       93.4MB         26.9MB
praktikum-docker:v1   1c0ab5be3b3f       92.5MB           26MB    U
```

### Docker Run Command

```bash
$ docker run -d -p 8080:80 --name praktikum-web praktikum-docker:v1

```

---

## 📄 Dockerfile

### Isi Dockerfile

```dockerfile
# Gunakan nginx alpine sebagai base image
FROM nginx:alpine

# Copy file HTML ke direktori nginx di dalam kontainer
COPY app/index.html /usr/share/nginx/html/index.html

# Beritahu Docker bahwa aplikasi berjalan di port 80
EXPOSE 80

# Jalankan nginx
CMD ["nginx", "-g", "daemon off;"]
```

### Penjelasan Dockerfile

FROM nginx:alpine
Instruksi ini menentukan image dasar yang akan digunakan sebagai fondasi. Kamu memilih Alpine Linux karena distribusinya sangat minimalis, sehingga ukuran akhir image kamu akan jauh lebih kecil dan efisien di laptop ASUS kamu dibandingkan image standar.

COPY app/index.html /usr/share/nginx/html/index.html
Baris ini bertugas menyalin file dari sistem lokal (laptop) ke dalam sistem file kontainer. Dengan menaruh file index.html kustom ke lokasi default Nginx, kamu berhasil mengganti tampilan standar "Welcome to nginx" menjadi halaman profil yang berisi nama Nurdian dan NIM kamu.

EXPOSE 80
Instruksi ini berfungsi sebagai dokumentasi yang memberi tahu Docker bahwa kontainer akan mendengarkan (listen) pada port 80 saat dijalankan. Ini membantu kamu mengetahui port mana yang harus dipetakan saat menggunakan perintah -p di terminal.

CMD ["nginx", "-g", "daemon off;"]
Ini adalah perintah utama yang akan dieksekusi saat kontainer mulai menyala. Parameter daemon off; sangat krusial karena memaksa Nginx berjalan di latar depan (foreground). Jika Nginx berjalan di latar belakang (sebagai daemon), Docker akan menganggap prosesnya sudah selesai dan langsung mematikan kontainer tersebut.

---

## 🐙 Docker Compose

### Isi docker-compose.yml

```yaml
version: '3.8'

services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    volumes:
      - ./app:/usr/share/nginx/html:ro
    depends_on:
      - api
    networks:
      - praktikum-net

  api:
    image: httpd:alpine
    ports:
      - "8081:80"
    networks:
      - praktikum-net

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_USER: praktikum
      POSTGRES_PASSWORD: devops123
      POSTGRES_DB: praktikum_db
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - praktikum-net

networks:
  praktikum-net:
    driver: bridge

volumes:
  db_data:
```

### Penjelasan Docker Compose

version: '3.8'
Menentukan versi format Docker Compose yang digunakan agar kompatibel dengan fitur-fitur Docker terbaru di laptop ASUS kamu.

services:
Bagian pembuka yang memberi tahu Docker bahwa kita akan mendefinisikan daftar aplikasi atau layanan yang ingin dijalankan secara bersamaan.

web:, api:, db:
Nama-nama layanan yang kita buat; dalam kasus ini ada tiga layanan yaitu server web (Nginx), server API (Apache), dan Database (Postgres).

image: nginx:alpine (dan lainnya)
Menentukan "bahan dasar" atau template image yang akan diunduh dari Docker Hub untuk setiap layanan tersebut.

ports: - "8080:80"
Melakukan pemetaan port: angka di kiri (8080) adalah port yang kamu akses di browser laptop, dan angka di kanan (80) adalah port asli di dalam kontainer.

volumes: - ./app:/usr/share/nginx/html:ro
Menghubungkan folder app di laptopmu ke dalam kontainer agar perubahan kode HTML langsung ter-update secara otomatis tanpa perlu build ulang image.

depends_on: - api
Mengatur urutan menyala; instruksi ini memastikan kontainer api harus aktif terlebih dahulu sebelum kontainer web dijalankan.

networks: - praktikum-net
Memasukkan setiap layanan ke dalam satu jaringan virtual yang sama agar mereka bisa saling berkomunikasi menggunakan nama layanannya.

environment:
Digunakan khusus pada layanan db untuk mengatur konfigurasi internal seperti username (praktikum) dan password (devops123) secara otomatis.

driver: bridge
Menentukan jenis jaringan "jembatan" yang memungkinkan kontainer-kontainer tersebut terhubung satu sama lain namun tetap terisolasi dari jaringan luar.

### Output Docker Compose Up

```
 docker compose up -d
time="2026-02-25T23:52:12+08:00" level=warning msg="D:\\Penyimpanan dian\\OneDrive\\Documents\\semester 5\\Nurdian_105841118923_Praktikum02\\docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
[+] Running 22/22
 ✔ api Pulled                                                                                                     23.8s
   ✔ b9df760bab4a Pull complete                                                                                   18.2s
   ✔ 79273eb2147b Pull complete                                                                                    2.5s
   ✔ 4f4fb700ef54 Pull complete                                                                                    1.4s
   ✔ 3688fd767e4a Pull complete                                                                                   17.8s
   ✔ 987f24f891f4 Pull complete                                                                                    2.4s
   ✔ abd702cd48c8 Pull complete                                                                                    1.7s
   ✔ 2bd78f43169f Download complete                                                                                0.0s
   ✔ 8c8ca383ec3c Download complete                                                                                0.3s
 ✔ db Pulled                                                                                                      56.4s
   ✔ 8b6feeda4732 Pull complete                                                                                    2.5s
   ✔ 2af348483d54 Pull complete                                                                                    1.4s
   ✔ e2808358fab6 Pull complete                                                                                    1.5s
   ✔ 6385d21b1497 Pull complete                                                                                    1.5s
   ✔ 49d5e74d1649 Pull complete                                                                                    2.4s
   ✔ fbd2333a8b2e Pull complete                                                                                   50.6s
   ✔ d9fee99ceaeb Pull complete                                                                                    2.4s
   ✔ 1cc5032597da Pull complete                                                                                    2.5s
   ✔ 2b183e31c9f8 Pull complete                                                                                    2.5s
   ✔ 22021ae8a283 Pull complete                                                                                    4.5s
   ✔ 19681da0b740 Download complete                                                                                0.0s
   ✔ 9543e0459960 Download complete                                                                                0.1s
[+] Running 4/5
 ✔ Network nurdian_105841118923_praktikum02_praktikum-net  Created                                                 0.1s
 ✔ Volume nurdian_105841118923_praktikum02_db_data         Cr...                                                   0.0s

 docker compose up -d
time="2026-02-25T23:57:33+08:00" level=warning msg="D:\\Penyimpanan dian\\OneDrive\\Documents\\semester 5\\Nurdian_105841118923_Praktikum02\\docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion"
[+] Running 3/3
 ✔ Container nurdian_105841118923_praktikum02-db-1   Started                                                       1.0s
 ✔ Container nurdian_105841118923_praktikum02-api-1  Started                                                       1.0s
 ✔ Container nurdian_105841118923_praktikum02-web-1  Started                                                       1.3s
```

---

## 📸 Screenshots

| No | Screenshot | Keterangan |
|----|------------|------------|
| 1 | ![Container Running](screenshots/01-container-running.png) | Container yang sedang berjalan |
| 2 | ![Docker Images](screenshots/02-docker-images.png) | Daftar Docker images |
| 3 | ![Dockerfile](screenshots/03-dockerfile-content.png) | Isi file Dockerfile |
| 4 | ![Docker Build](screenshots/04-docker-build.png) | Proses docker build |
| 5 | ![App Browser](screenshots/05-app-browser.png) | Aplikasi berjalan di browser |
| 6 | ![Compose Up](screenshots/06-compose-up.png) | Docker Compose up |

---

## 💭 Refleksi & Kesimpulan

### Yang Dipelajari

Dari praktikum ini, saya belajar bahwa Docker itu seperti membungkus aplikasi dan "bumbunya" (konfigurasi & library) ke dalam wadah praktis bernama kontainer agar bisa jalan lancar di mana saja tanpa pusing masalah error beda laptop. Saya jadi paham cara membuat resep aplikasi sendiri pakai Dockerfile untuk memunculkan identitas saya di server Nginx, serta cara praktis menjalankan banyak layanan sekaligus—seperti Web, API, dan Database—hanya dengan satu perintah Docker Compose. Intinya, teknologi ini bikin kerjaan koding saya jadi lebih rapi, ringan, dan sangat berguna untuk memastikan proyek seperti CRAFT-TECH nanti bisa di-deploy dengan profesional dan konsisten.

### Manfaat Docker

Docker membantu pengembangan software dengan cara membungkus aplikasi dan semua dependensinya ke dalam satu "wadah" konsisten, sehingga masalah klasik aplikasi yang hanya jalan di laptop sendiri tetapi error saat dikirim ke orang lain bisa teratasi sepenuhnya. Teknologi ini memungkinkan kamu membuat lingkungan kerja yang ringan dan terisolasi di laptop ASUS milikmu, di mana kamu bisa menjalankan web server, API, dan database secara bersamaan menggunakan Docker Compose tanpa takut sistem menjadi berat atau saling bentrok. Hal ini sangat berguna untuk mempercepat proses koding dan deployment, terutama untuk memastikan proyek masa depan seperti CRAFT-TECH tetap stabil dan profesional saat dijalankan di server manapun.

### Tantangan dan Solusi

Ada momen di mana container yang baru dibuat langsung berstatus exited dan tidak bisa diakses, dan ada beberapa yg tidak saya pahami

Solusi: Saya menggunakan perintah docker logs [nama_container] untuk melakukan troubleshooting dan melihat pesan error di dalamnya. Ternyata ada kesalahan typo pada nama environment variable, Setelah diperbaiki dan image di-build ulang, container berhasil berjalan normal, dan untuk yg saya kurang pahami saya kembali mencari tau bagaimana cara untuk menjelakannya di beberapa AI sampai saya berhasil jalankan



---

## ✅ Checklist

- [x] Berhasil membuat Dockerfile yang valid
- [x] Berhasil build Docker image
- [x] Container berjalan dan aplikasi bisa diakses
- [x] Docker Compose berhasil dijalankan
- [x] Semua screenshot lengkap dan jelas
- [x] Penjelasan ditulis dengan bahasa sendiri

---

*Laporan ini dibuat pada Kamis, 26 Februari 2026*
