# Multithreading: Implementasi, Speedup, Tipe Paralelisme, Jenis Thread, dan Proses Context Switching

Dokumen ini membahas secara komprehensif tentang konsep multithreading, mencakup:

1. **4.1** Tiga ilustrasi kode nyata yang menunjukkan bagaimana multithreading dapat meningkatkan efisiensi program.  
2. **4.2** Perhitungan *speedup* dengan Amdahl’s Law untuk aplikasi yang 60%-nya bisa diparalelkan.  
3. **4.3** Identifikasi jenis paralelisme dalam skenario server multithreaded.  
4. **4.4** Dua perbedaan krusial antara user-level thread dan kernel-level thread serta kapan masing-masing lebih efektif.  
5. **4.5** Penjabaran proses context switching antar thread oleh kernel.

---

## 4.1 Ilustrasi Multithreading dan Perbandingan Performa

Multithreading memberikan kemampuan bagi program untuk melakukan banyak pekerjaan secara bersamaan. Berikut tiga kasus penggunaan umum:

### Contoh 1: Server HTTP Multithreaded

Sebuah server yang melayani banyak klien akan lebih efisien jika tiap koneksi ditangani oleh thread sendiri.

```python
import threading
import socket

def tangani_klien(client_socket):
    request = client_socket.recv(1024)
    print(f"Menerima permintaan: {request.decode()}")
    response = b"HTTP/1.1 200 OK\r\nContent-Length: 13\r\n\r\nHello, world!"
    client_socket.send(response)
    client_socket.close()

def server():
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.bind(("0.0.0.0", 8080))
    server_socket.listen(5)
    print("Server mendengarkan pada port 8080...")

    while True:
        client, addr = server_socket.accept()
        thread_klien = threading.Thread(target=tangani_klien, args=(client,))
        thread_klien.start()

if __name__ == "__main__":
    server()
```

### Contoh 2: Pemrosesan File Paralel

Saat mengolah banyak file besar, multithreading bisa mengurangi waktu total secara signifikan.

```python
import threading

def proses_file(nama_file):
    with open(nama_file, 'r') as file:
        data = file.read()
    print(f"File {nama_file} telah diproses")

daftar_file = ["file1.txt", "file2.txt", "file3.txt"]
threads = []

for file in daftar_file:
    thread = threading.Thread(target=proses_file, args=(file,))
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()

print("Semua file telah diproses.")
```

### Contoh 3: Filter Gambar Serentak

Aplikasi filter gambar akan lebih cepat jika setiap gambar diproses pada thread yang berbeda.

```python
import threading
from PIL import Image, ImageFilter

def proses_gambar(path_input, path_output):
    gambar = Image.open(path_input)
    gambar_filter = gambar.filter(ImageFilter.SHARPEN)
    gambar_filter.save(path_output)
    print(f"Gambar {path_input} telah diproses")

daftar_gambar = [("img1.jpg", "out1.jpg"), ("img2.jpg", "out2.jpg"), ("img3.jpg", "out3.jpg")]
threads = []

for path_input, path_output in daftar_gambar:
    thread = threading.Thread(target=proses_gambar, args=(path_input, path_output))
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()

print("Semua gambar telah diproses.")
```

---

## 4.2 Estimasi Speedup: Amdahl’s Law

Amdahl’s Law digunakan untuk mengukur keuntungan teoretis dari peningkatan paralelisme.

**Rumus:**
```
Speedup = 1 / ((1 - p) + (p / n))
```

Jika 60% kode bisa diparalelkan (p = 0.6):

- **Dua core (n=2):**
  
  `Speedup = 1 / (0.4 + 0.6/2) = 1 / 0.7 = 1.43`

- **Empat core (n=4):**
  
  `Speedup = 1 / (0.4 + 0.6/4) = 1 / 0.55 = 1.82`

---

## 4.3 Task vs Data Parallelism

Dalam contoh server, jenis paralelisme yang digunakan adalah **Task Parallelism**.

- **Task Parallelism:** Setiap thread menjalankan tugas berbeda (misalnya permintaan klien berbeda).
- **Data Parallelism:** Satu tugas dipecah berdasarkan data, misalnya pemrosesan array besar secara paralel.

---

## 4.4 User-Level vs Kernel-Level Threads

| Aspek | User-Level Threads | Kernel-Level Threads |
|-------|---------------------|----------------------|
| Penjadwalan | Dilakukan oleh pustaka di ruang user | Dilakukan oleh kernel |
| Context Switching | Ringan, tanpa perlu masuk kernel | Lebih berat karena melalui kernel |
| Blocking | Seluruh proses bisa terblokir jika satu thread blocking | Thread lain tetap bisa berjalan |

**User-Level Threads:** Efisien untuk tugas ringan tanpa blocking.

**Kernel-Level Threads:** Lebih baik untuk I/O intensif dan lingkungan multicore.

---

## 4.5 Proses Context Switching oleh Kernel

1. **Simpan Konteks Thread Lama:** Register, counter, status ke Thread Control Block (TCB).
2. **Update Scheduler:** Thread lama diubah statusnya; scheduler pilih thread baru.
3. **Ambil Konteks Thread Baru:** Data dari TCB dimuat kembali.
4. **Ganti Konteks Memori:** Jika berasal dari proses berbeda, MMU diatur ulang.
5. **Lanjutkan Eksekusi:** CPU mulai dari titik terakhir thread baru berhenti.

---

