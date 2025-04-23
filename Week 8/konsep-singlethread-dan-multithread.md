# Konsep Single-Thread dan Multi-Thread dalam Pemrograman

Thread adalah unit eksekusi terkecil dalam sebuah proses. Sebuah program dapat berjalan menggunakan satu thread (**single-threaded**) atau beberapa thread sekaligus (**multi-threaded**).

---

## 1. Single-Thread (Satu Thread)

### Definisi
Program hanya menjalankan satu rangkaian perintah dalam satu waktu.

### Karakteristik
- Eksekusi tugas dilakukan secara berurutan (*synchronous*).
- Jika ada tugas yang memblokir (misalnya, operasi I/O), seluruh program akan menunggu hingga selesai.
- Lebih sederhana karena tidak perlu mengelola *race condition* atau sinkronisasi.

### Contoh Bahasa
JavaScript (Node.js default), Python (meskipun bisa multi-threaded, ada GIL yang membatasi).

### Keuntungan
- Mudah di-debug dan diprediksi.
- Tidak ada *overhead* sinkronisasi.

### Kekurangan
- Performa buruk untuk tugas berat atau *blocking* (misalnya, operasi file atau jaringan).

---

## 2. Multi-Thread (Banyak Thread)

### Definisi
Program membagi tugas ke beberapa thread yang berjalan secara konkuren (*paralel* atau bergantian).

### Karakteristik
- Thread berbagi memori yang sama dalam satu proses.
- Cocok untuk tugas yang bisa diparalelkan (misalnya, *download* banyak file, komputasi terpisah).
- Memerlukan mekanisme sinkronisasi (*locks*, *semaphores*) untuk menghindari **race condition**.

### Contoh Bahasa
Java, C#, C++ (dengan *library threading*).

### Keuntungan
- Meningkatkan responsivitas aplikasi (misalnya, GUI tetap responsif saat proses berat berjalan di thread lain).
- Memanfaatkan CPU *multi-core* secara efisien.

### Kekurangan
- Lebih kompleks (*bug* seperti *deadlock* atau *data corruption* bisa terjadi).
- *Overhead* karena manajemen thread.

---

## Perbandingan Singkat

| Aspek            | Single-Thread              | Multi-Thread                  |
|------------------|---------------------------|-------------------------------|
| **Kompleksitas** | Sederhana                 | Lebih rumit (sinkronisasi)    |
| **Performa**     | Lambat untuk *blocking task* | Lebih cepat untuk tugas paralel |
| **Resource**     | Hemat memori              | Butuh lebih banyak *resource*   |
| **Scalability**  | Terbatas                  | Lebih baik untuk beban tinggi  |

---

## Kapan Memilih Single-Thread atau Multi-Thread?

### Gunakan Single-Thread
- Untuk tugas sederhana dan berurutan.
- Jika bahasa/*framework* sudah dioptimalkan untuk *single-thread* (contoh: Node.js dengan *event loop*).

### Gunakan Multi-Thread
- Untuk tugas berat seperti komputasi paralel atau *handling* banyak koneksi jaringan.
- Saat aplikasi perlu tetap responsif (misalnya, game atau aplikasi GUI).

