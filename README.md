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
Aktifkan Docker Desktop: 
