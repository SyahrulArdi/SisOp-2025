# Nama : Syahrul Ardi Prasetiyo

# Perbedaan Multiprogramming dan Multitasking

---

## **Multiprogramming** 
Teknik di mana sistem operasi menyimpan **beberapa program** dalam memori secara bersamaan dan menjalankannya secara bergantian oleh CPU. Tujuannya adalah memaksimalkan penggunaan CPU saat satu program menunggu I/O.

### Ciri-Ciri Multiprogaming  
- **Tujuan**: Meningkatkan utilisasi CPU (mencegah *idle time*).  
- **Konteks**: Digunakan pada sistem *batch processing* (non-interaktif).  
- **Alur Eksekusi**:  
  - CPU beralih ke program lain hanya jika program aktif menunggu I/O.  
  - Tidak ada pembagian waktu (*time slicing*).  
- **Contoh**: Sistem mainframe era 1960-1970an (misal: IBM OS/360).

---

## **Multitasking** 
Teknik di mana CPU menjalankan **beberapa tugas/proses** secara *bersamaan* dengan membagi waktu (*time-sharing*). Bertujuan memberikan ilusi paralelisme kepada pengguna.

### Ciri-Ciri Multitasking
- **Tujuan**: Meningkatkan responsivitas untuk pengguna interaktif.  
- **Konteks**: Digunakan pada sistem modern (Windows, Linux, macOS).  
- **Alur Eksekusi**:  
  - CPU mengalokasikan *time quantum* ke setiap tugas, lalu berpindah ke tugas berikutnya.  
  - Perpindahan terjadi **terlepas dari status I/O** (dipicu *timer interrupt*).  
- **Contoh**: Menjalankan browser, editor teks, dan musik secara bersamaan di PC.

---

## Tabel Perbedaan Utama  
| **Aspek**               | Multiprogramming                          | Multitasking                          |  
|-------------------------|-------------------------------------------|----------------------------------------|  
| **Tujuan**              | Maksimalkan penggunaan CPU              | Responsivitas untuk pengguna interaktif |  
| **Konteks Switching**   | Dipicu oleh I/O wait                     | Dipicu oleh *timer interrupt*          |  
| **Interaksi Pengguna**  | Non-interaktif (*batch processing*)      | Interaktif (real-time)                 |  
| **Alokasi Waktu**       | Tidak ada *time-sharing*                 | Ada *time-sharing*                     |  
| **Contoh Sistem**       | Mainframe lama (IBM OS/360)              | Windows, Linux, macOS                 |  

---

## Kesimpulan  
- **Multiprogramming**: Fokus pada efisiensi CPU untuk sistem non-interaktif.  
- **Multitasking**: Fokus pada responsivitas untuk pengguna yang membutuhkan eksekusi "bersamaan".  
- **Hubungan**: Multitasking adalah evolusi dari konsep multiprogramming dengan tambahan *time-sharing*.  
