Nama: Maria Imakulata Tecira

NIM: 245410043



1. Teorema CAP dan BASE
Teorema CAP
Teorema CAP (Consistency, Availability, Partition Tolerance) menyatakan bahwa dalam sistem terdistribusi, kita hanya dapat memilih dua dari tiga aspek berikut:
- Consistency: Semua node memiliki data yang sama pada saat yang sama.
- Availability: Setiap permintaan akan mendapatkan respon, meskipun node tersebut tidak memiliki data terbaru.
- Partition Tolerance: Sistem tetap berfungsi meskipun terjadi partisi jaringan.
Contoh: Sistem perbankan yang menggunakan model CA (Consistency dan Availability) mungkin tidak dapat berfungsi jika terjadi partisi jaringan. Namun, jika sistem tersebut memilih AP (Availability dan Partition Tolerance), maka sistem dapat tetap berfungsi tetapi dengan risiko data yang tidak konsisten.

Teorema BASE
Teorema BASE (Basically Available, Soft-state, Eventually consistent) adalah alternatif dari teorema CAP yang lebih fleksibel. BASE memungkinkan sistem untuk:
- Basically Available: Sistem tetap tersedia meskipun terjadi kegagalan.
- Soft-state: Data dapat berubah seiring waktu.
- Eventually consistent: Data akan konsisten setelah beberapa waktu.
Contoh: Sistem sosial media yang menggunakan model BASE dapat menampilkan postingan yang berbeda kepada pengguna yang berbeda pada saat yang sama, tetapi pada akhirnya data akan konsisten.

2. Jelaskan keterkaitan antara GraphQL dengan komunikasi antar proses pada sistem terdistribusi. Buat diagramnya.
   Keterkaitan GraphQL dengan Komunikasi Antar Proses pada Sistem Terdistribusi

GraphQL bukan hanya query API, tetapi juga komunikasi antar proses dalam sistem terdistribusi, karena:
Bagaimana GraphQL bekerja dalam sistem terdistribusi?
GraphQL sebagai Orchestrator
GraphQL dapat menjadi gateway yang mengumpulkan data dari banyak microservice:
Service A → user
Service B → transaksi
Service C → notifikasi
GraphQL menggabungkan semuanya dalam satu query.
GraphQL menggunakan resolvers
Resolver memanggil proses lain (REST, gRPC, DB, service lain), sehingga GraphQL bertindak sebagai perantara antar proses.
GraphQL subscription
Ini memungkinkan komunikasi real-time antar node dengan WebSocket.
GraphQL mendukung federasi
GraphQL Federation memungkinkan banyak GraphQL server bekerja sebagai satu kesatuan → bentuk komunikasi antar proses juga.

Diagram Hubungan GraphQL dalam Sistem Terdistribusi
      
<img width="2372" height="768" alt="Untitled diagram-2025-11-17-042035" src="https://github.com/user-attachments/assets/87eafe16-beaa-4071-a7ec-9c2572feb80d" />

Semua microservice saling terhubung dan GraphQL menjadi perantara
komunikasi antar proses dalam sistem terdistribusi.

3. Dengan menggunakan Docker / Docker Compose, buatlah streaming replication di PostgreSQL yang bisa menjelaskan sinkronisasi. Tulislah langkah-langkah pengerjaannya dan buat penjelasan secukupnya.

Streaming Replication di PostgreSQL Windows 
https://www.crunchydata.com/blog/postgres-streaming-replication-on-windows-a-quick-guide
Persiapan Awal
1. Aktifkan Docker Desktop: Pastikan Docker Desktop sudah terpasang dan berjalan di sistem Windows Anda.
2. Struktur Direktori dan File
Periksa Struktur Direktori: Pastikan Anda memiliki struktur direktori yang sesuai untuk menyimpan konfigurasi dan data PostgreSQL.
Periksa File Docker: Pastikan file-file Docker (seperti docker-compose.yml) sudah ada dan terkonfigurasi dengan benar.
3. Tentukan Variabel
Konfigurasi Variabel: Tentukan variabel-variabel yang diperlukan untuk konfigurasi Docker dan PostgreSQL, seperti nama database, username, password, dan lain-lain.
4. Membuat Jaringan dan Volume Docker
Buat Jaringan Docker: Buat jaringan Docker untuk menghubungkan container primary dan standby.
Buat Volume Docker: Buat volume Docker untuk menyimpan data PostgreSQL agar tetap persisten meskipun container di-restart.
5. Jalankan Node Primary
Jalankan Container Primary: Gunakan Docker Compose atau perintah Docker lainnya untuk menjalankan container PostgreSQL sebagai node primary.
6. Konfigurasi Node Primary untuk Replikasi
Ubah Konfigurasi postgresql.conf:
Edit file postgresql.conf di direktori data node primary.
Pastikan parameter seperti wal_level, listen_addresses, dan max_wal_senders sudah dikonfigurasi dengan benar untuk mendukung replikasi.
Ubah Konfigurasi pg_hba.conf:
Edit file pg_hba.conf untuk mengizinkan koneksi dari node standby ke node primary untuk keperluan replikasi.
Restart Node Primary: Setelah mengubah konfigurasi, restart container node primary agar perubahan diterapkan.
7. Buat Slot Replikasi
Buat Slot Replikasi di Primary: Gunakan perintah SQL untuk membuat slot replikasi di node primary. Slot replikasi ini akan digunakan oleh node standby untuk menerima perubahan dari primary.
8. Cloning Database ke Node Standby
Clone Database: Gunakan utilitas seperti pg_basebackup untuk meng-clone database dari node primary ke node standby.
9. Jalankan Node Standby (Database Cadangan)
Jalankan Container Standby: Gunakan Docker Compose atau perintah Docker lainnya untuk menjalankan container PostgreSQL sebagai node standby.
Konfigurasi Standby: Pastikan node standby terkonfigurasi untuk terhubung ke node primary dan menggunakan slot replikasi yang telah dibuat.
10. Uji Coba dan Verifikasi Replikasi
Cek Status di Primary: Periksa status replikasi di node primary untuk memastikan node standby terhubung dan menerima perubahan.
Buat Data di Primary: Buat data baru di node primary (misalnya, membuat tabel atau memasukkan data ke dalam tabel).
Baca Data di Standby: Periksa node standby untuk memastikan data yang baru dibuat di primary sudah direplikasi ke standby.
Tes Gagal Tulis di Standby: Coba lakukan operasi tulis di node standby. Karena standby seharusnya hanya menerima replikasi, operasi tulis akan gagal.
11. Skenario Kasus yang Sempurna untuk Menguji Replikasi
Buat Tabel Mahasiswa di PRIMARY: Buat tabel bernama mahasiswa di node primary dan masukkan beberapa data ke dalamnya.
Verifikasi di Standby: Periksa node standby untuk memastikan tabel mahasiswa dan datanya sudah direplikasi dengan benar.
