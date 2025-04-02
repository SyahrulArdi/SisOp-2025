# **SISTEM OPERASI - RANGKUMAN APPENDIX A**

**Nama**: Syahrul Ardi Prasetiyo  
**NRP**: 3124500035  

---

## **Ringkasan Sistem Operasi**
Konsep fundamental dalam sistem operasi. Tujuan utama sistem operasi adalah menjadi perantara antara perangkat keras dan pengguna, mengelola sumber daya komputer, serta menyediakan lingkungan eksekusi yang efisien dan aman untuk aplikasi.

### **1. Pengantar Sistem Operasi**
Sistem operasi adalah perangkat lunak yang mengelola perangkat keras komputer dan menyediakan layanan bagi aplikasi pengguna. Fungsi utama sistem operasi meliputi:
- Manajemen proses dan tugas
- Manajemen memori dan penyimpanan
- Pengelolaan perangkat I/O
- Sistem keamanan dan proteksi data
- Penjadwalan tugas dan optimalisasi penggunaan sumber daya

Sistem operasi modern mendukung **multi-user** dan **multitasking**. Contoh sistem operasi: Windows, Linux, macOS, Android, dan iOS.

---

### **2. Struktur dan Arsitektur Sistem Operasi**
Sistem operasi memiliki berbagai model arsitektur:
- **Monolithic System**: Semua fungsi terintegrasi dalam satu unit besar (contoh: UNIX versi awal).
- **Layered System**: Sistem dibagi menjadi lapisan (*layer*) yang bekerja secara hierarkis (contoh: THE System, Multics).
- **Microkernel**: Hanya fungsi minimal yang dimasukkan ke dalam kernel, sisanya dijalankan di luar kernel (contoh: Minix, QNX).
- **Hybrid System**: Kombinasi berbagai model (contoh: Windows, macOS).

---

### **3. Manajemen Proses**
Sistem operasi bertanggung jawab atas:
- Pembuatan, penjadwalan, dan penghentian proses.
- Komunikasi antar proses (*Inter-Process Communication* - IPC).
- Sinkronisasi proses untuk menghindari konflik.

Tahapan proses:
1. **New** - Proses baru dibuat.
2. **Ready** - Menunggu eksekusi oleh CPU.
3. **Running** - Sedang dieksekusi oleh CPU.
4. **Waiting** - Menunggu kejadian tertentu (misalnya input pengguna).
5. **Terminated** - Proses selesai dan dihentikan.

**Algoritma penjadwalan CPU**:
- First-Come, First-Served (FCFS)
- Shortest Job Next (SJN)
- Round Robin (RR)
- Priority Scheduling

---

### **4. Manajemen Memori**
Metode manajemen memori yang digunakan dalam sistem operasi:
- **Paging**: Membagi memori menjadi blok kecil (*pages*), mengurangi fragmentasi eksternal.
- **Segmentation**: Membagi memori berdasarkan segmen logis (kode, data, stack).
- **Virtual Memory**: Menggunakan *swap space* sebagai perpanjangan memori utama untuk mendukung proses yang lebih besar dari RAM.

---

### **5. Sistem I/O dan Manajemen File**
#### **a. Manajemen I/O**
- Mengontrol perangkat seperti keyboard, printer, hard drive, dan jaringan.
- Menggunakan *buffering*, *spooling*, dan *interrupt handling* untuk efisiensi.

#### **b. Manajemen File**
- Sistem operasi mengorganisasi data dalam file dan direktori.
- Berbagai sistem file digunakan: FAT32, NTFS (Windows), EXT4 (Linux).
- Menyediakan proteksi akses, struktur direktori, dan mekanisme backup.

---

### **6. Keamanan dan Proteksi**
Sistem operasi melindungi data dan sumber daya dari akses tidak sah dengan:
- **Autentikasi & Otorisasi**: Kata sandi, biometrik, autentikasi multi-faktor.
- **Enkripsi**: Melindungi data saat disimpan atau dikirim melalui jaringan.
- **Proteksi Akses**: *Role-Based Access Control* (RBAC) membatasi tindakan pengguna.
- **Keamanan Jaringan**: Firewall, deteksi intrusi, perlindungan malware.

---

### **7. Multiprocessing dan Multithreading**
#### **a. Multiprocessing**
- Menggunakan lebih dari satu prosesor untuk mengeksekusi tugas secara bersamaan.
- Bisa berbentuk *symmetric multiprocessing (SMP)* atau *asymmetric multiprocessing (AMP)*.

#### **b. Multithreading**
- Satu proses dapat dibagi menjadi beberapa *threads* yang berjalan secara independen.
- Digunakan dalam aplikasi berbasis multitasking seperti server web dan game.

---

### **Kesimpulan**
Appendix A dari *Operating System Concepts* memberikan wawasan tentang:
- Arsitektur sistem operasi
- Manajemen proses dan memori
- Pengelolaan I/O dan sistem file
- Keamanan dan proteksi sistem
- Dukungan terhadap multiprocessing dan multithreading

Sistem operasi merupakan elemen kunci dalam dunia komputasi modern, mendukung efisiensi, keamanan, dan keandalan dalam penggunaan komputer.
