# Tugas 6 Sistem Operasi  

**Nama:** Syahrul Ardi Prasetiyo

**NRP:** 3124500035

**Dosen Pengajar:** Dr Ferry Astika Saputra ST, M.Sc  

---

## 1. Program Thread Sederhana (Compile Thread 3)

### Kode Program (C)

```c
#include <stdio.h>
#include <pthread.h>

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond[3] = {
    PTHREAD_COND_INITIALIZER,
    PTHREAD_COND_INITIALIZER,
    PTHREAD_COND_INITIALIZER
};
int current_thread = 1;

void *thread_function(void *arg) {
    int thread_id = *(int *)arg;
    while (1) {
        pthread_mutex_lock(&mutex);
        while (current_thread != thread_id) {
            pthread_cond_wait(&cond[thread_id - 1], &mutex);
        }
        printf("%d ", thread_id);
        current_thread = (current_thread % 3) + 1;
        pthread_cond_signal(&cond[current_thread - 1]);
        pthread_mutex_unlock(&mutex);
    }
    return NULL;
}

int main() {
    pthread_t threads[3];
    int thread_ids[3] = {1, 2, 3};

    for (int i = 0; i < 3; i++) {
        pthread_create(&threads[i], NULL, thread_function, &thread_ids[i]);
    }

    for (int i = 0; i < 3; i++) {
        pthread_join(threads[i], NULL);
    }

    return 0;
}
```

### Jawaban :

- **Struktur Kondisi:** Menggunakan array `cond[3]` untuk menyimpan kondisi setiap thread, bukan variabel terpisah.
- **Logika Pergantian Thread:** Menggunakan operasi modulo `current_thread = (current_thread % 3) + 1` untuk menentukan thread berikutnya, sehingga lebih ringkas.
- **Inisialisasi Thread:** Menggunakan loop `for` untuk membuat dan `join` thread, mengurangi duplikasi kode.

### Output:
```
1 2 3 1 2 3 1 2 3 ...
```
*(Terus berulang hingga dihentikan manual.)*

---

## 2. Program Forking

### Kode Program (C)

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main() {
    pid_t child_pid = fork();

    if (child_pid == -1) {
        fprintf(stderr, "Gagal membuat proses anak.
");
        return 1;
    }

    if (child_pid == 0) {
        printf("Proses Anak - PID: %d, PID Parent: %d\n", getpid(), getppid());
    } else {
        printf("Proses Induk - PID: %d, PID Anak: %d\n", getpid(), child_pid);
    }

    return 0;
}
```

### Jawaban :

- **Pesan Output:** Menambahkan informasi PID parent pada proses anak (`getppid()`).
- **Penanganan Error:** Menggunakan `fprintf` ke `stderr` untuk pesan error.

### Output:
```
Proses Induk - PID: 1234, PID Anak: 1235  
Proses Anak - PID: 1235, PID Parent: 1234  
```
*(Urutan bisa terbalik tergantung penjadwalan.)*

---

## 3. Keuntungan Time Quantum Berbeda di Multilevel Queue

### Jawaban:

- **Penyesuaian Beban Kerja:**  
  Time quantum besar untuk antrian batch (misal 50ms) meminimalkan context switch untuk tugas berat.  
  Time quantum kecil untuk antrian interaktif (misal 5ms) memastikan respons cepat.

- **Prioritas Dinamis:**  
  Antrian prioritas tinggi (seperti sistem real-time) bisa diberi quantum kecil tetapi frekuensi tinggi, sementara antrian rendah (batch) mendapat quantum besar tetapi jarang.

- **Mencegah Dominasi Sumber Daya:**  
  Proses di antrian rendah tetap dapat berjalan lama tanpa mengganggu antrian prioritas tinggi.

- **Optimasi Performa:**  
  Mengurangi overhead dengan meminimalkan perpindahan antrian yang tidak perlu.

---

## 4. Diagram Gantt Chart

### Tabel Proses:

| Proses | Burst Time | Prioritas |
|--------|------------|-----------|
| P1     | 10         | 3         |
| P2     | 1          | 1         |
| P3     | 2          | 3         |
| P4     | 1          | 4         |
| P5     | 5          | 2         |

---

### 1. FCFS (First Come First Serve)  
**Urutan:** P1 → P2 → P3 → P4 → P5  
```
| P1 (0-10) | P2 (10-11) | P3 (11-13) | P4 (13-14) | P5 (14-19) |
```

---

### 2. SJF Nonpreemptive  
**Urutan:** P2 (1) → P4 (1) → P3 (2) → P5 (5) → P1 (10)  
```
| P2 (0-1) | P4 (1-2) | P3 (2-4) | P5 (4-9) | P1 (9-19) |
```

---

### 3. Prioritas Nonpreemptive  
**Urutan:** P2 (1) → P5 (2) → P1 (3) → P3 (3) → P4 (4)  
```
| P2 (0-1) | P5 (1-6) | P1 (6-16) | P3 (16-18) | P4 (18-19) |
```

---

### 4. Round Robin (Quantum = 2)  
```
| P1 (0-2) | P2 (2-3) | P3 (3-5) | P4 (5-6) | P5 (6-8) |
| P1 (8-10) | P5 (10-12) | P1 (12-14) | P5 (14-15) | P1 (15-17) |
| P1 (17-19) |
```

---

### Perbedaan dengan Jawaban Teman:

- **Round Robin:** Menambahkan detail eksekusi terakhir P1 yang tersisa 2 unit waktu (17-19).
- **Prioritas:** Memperjelas bahwa P1 dan P3 memiliki prioritas sama (3), tetapi P1 datang lebih dahulu.

---

## Kesimpulan

- **Thread:** Implementasi menggunakan array dan modulo lebih efisien.
- **Forking:** Menambahkan detail PID parent-child meningkatkan informatif output.
- **Time Quantum:** Penekanan pada adaptasi dinamis dan pencegahan dominasi.
- **Gantt Chart:** Detail tambahan untuk Round Robin dan prioritas.
