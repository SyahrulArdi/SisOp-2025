# Analisis SJF Scheduling Algorithm (Dengan dan Tanpa Arrival Time)

## Anggota

- **Rafif Ahmad Yudhistira** (3124500045)
- **Syahrul Ardi Prasetiyo** (3124500035)
- **Muhammad Rizqi Putra N.** (3124500044)

## Dosen Pengajar
**Dr Ferry Astika Saputra ST, M.Sc**

## 1. **SJF Scheduling Algorithm Without Arrival Time.c**


















```markdown
# Penjelasan Program SJF (Non-Preemptive) Tanpa Arrival Time

## Kode Program
```c
#include<stdio.h>

struct proc {
    int no, bt, ct, tat, wt;
};

struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}

int main() {
    struct proc p[10], tmp;
    float avgtat = 0, avgwt = 0;
    int n, ct = 0;
    
    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);
    
    for (int i = 0; i < n; i++)
        p[i] = read(i + 1);
    
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (p[j].bt > p[j + 1].bt) {
                tmp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = tmp;
            }
    
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for (int i = 0; i < n; i++) {
        ct += p[i].bt;
        p[i].ct = ct;
        p[i].tat = p[i].ct;          // TAT = CT (karena AT = 0)
        p[i].wt = p[i].tat - p[i].bt; // WT = TAT - BT
        avgtat += p[i].tat;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }
    
    avgtat /= n;
    avgwt /= n;
    printf("\nAverage TurnAroundTime = %.2f\nAverage WaitingTime = %.2f", avgtat, avgwt);
    return 0;
}
```

---

## Penjelasan Kode

### 1. **Struktur Data**
- **`struct proc`**: Menyimpan informasi proses, termasuk nomor proses (`no`), burst time (`bt`), completion time (`ct`), turnaround time (`tat`), dan waiting time (`wt`).

### 2. **Fungsi `read()`**
- Membaca input burst time untuk setiap proses.
- Contoh input:  
  ```plaintext
  Process No: 1  
  Enter Burst Time: 6
  ```

### 3. **Sorting Proses**
- Menggunakan **Bubble Sort** untuk mengurutkan proses berdasarkan burst time secara ascending.
- Tujuan: Proses dengan burst time terpendek dijalankan lebih dulu.

### 4. **Perhitungan Waktu**
- **Completion Time (CT)**: Diakumulasi dari burst time proses sebelumnya.
- **Turnaround Time (TAT)**: `CT - 0` (karena arrival time = 0).
- **Waiting Time (WT)**: `TAT - BT`.
- **Response Time (RT)**: Sama dengan `WT` (karena non-preemptive).

### 5. **Output**
- Menampilkan tabel proses dengan detail waktu.
- Menghitung rata-rata TAT dan WT.

---

## Kelebihan dan Kekurangan

| **Kelebihan**                          | **Kekurangan**                                 |
|----------------------------------------|-----------------------------------------------|
| Minimizes average waiting time.        | Risk of starvation untuk proses BT besar.     |
| Sederhana dan mudah diimplementasikan. | Tidak praktis untuk sistem waktu nyata.       |
| Optimal untuk batch processing.        | Membutuhkan prediksi BT (tidak selalu mungkin). |
| Efisien jika semua BT diketahui.       | Sorting menambah overhead komputasi.          |

---

## Contoh Eksekusi
**Input**:  
```
Enter Number of Processes: 4  
Burst Time untuk P1: 6  
Burst Time untuk P2: 8  
Burst Time untuk P3: 7
Burst Time untuk P4: 3
```	

SJF Scheduling Algorithm With Arrival Time.c
# Analisis Kode Penjadwalan SJF Non-Preemptive

---

## Kode Program Lengkap
```c
#include<stdio.h>

// Struktur untuk menyimpan informasi proses
struct proc {
    int no, at, bt, it, ct, tat, wt;
};

// Fungsi untuk membaca input proses
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}

int main() {
    int n, j, min = 0;
    float avgtat = 0, avgwt = 0;
    struct proc p[10], temp;

    printf("<--SJF Scheduling Algorithm (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    // Input data proses
    for (int i = 0; i < n; i++)
        p[i] = read(i + 1);

    // Sorting proses berdasarkan arrival time (Bubble Sort)
    for (int i = 0; i < n - 1; i++)
        for (j = 0; j < n - i - 1; j++)
            if (p[j].at > p[j + 1].at) {
                temp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = temp;
            }

    // Memilih proses pertama dengan burst time terpendek di antara yang memiliki AT sama
    for (j = 1; j < n && p[j].at == p[0].at; j++)
        if (p[j].bt < p[min].bt)
            min = j;

    temp = p[0];
    p[0] = p[min];
    p[min] = temp;

    // Menghitung waktu selesai (CT) untuk proses pertama
    p[0].it = p[0].at;
    p[0].ct = p[0].it + p[0].bt;

    // Penjadwalan untuk proses selanjutnya
    for (int i = 1; i < n; i++) {
        for (j = i + 1, min = i; j < n && p[j].at <= p[i - 1].ct; j++)
            if (p[j].bt < p[min].bt)
                min = j;

        temp = p[i];
        p[i] = p[min];
        p[min] = temp;

        // Menentukan waktu mulai (IT) berdasarkan CT proses sebelumnya atau AT
        if (p[i].at <= p[i - 1].ct)
            p[i].it = p[i - 1].ct;
        else
            p[i].it = p[i].at;

        p[i].ct = p[i].it + p[i].bt;
    }

    // Menghitung TAT, WT, dan menampilkan output
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for (int i = 0; i < n; i++) {
        p[i].tat = p[i].ct - p[i].at;
        avgtat += p[i].tat;
        p[i].wt = p[i].tat - p[i].bt;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].at, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }

    avgtat /= n, avgwt /= n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f", avgtat, avgwt);
}
```

---

## Penjelasan Alur Kode

### 1. **Input Data Proses**
   - Pengguna diminta memasukkan jumlah proses (`n`).
   - Setiap proses memiliki `arrival time (AT)` dan `burst time (BT)` yang diinput melalui fungsi `read()`.

### 2. **Sorting Berdasarkan Arrival Time**
   - Proses diurutkan menggunakan **Bubble Sort** berdasarkan `AT` untuk memastikan proses yang datang lebih awal diproses terlebih dahulu.

### 3. **Pemilihan Proses Pertama**
   - Di antara proses dengan `AT` sama, dipilih proses yang memiliki **burst time terpendek** untuk dijalankan pertama kali.

### 4. **Penjadwalan SJF Non-Preemptive**
   - Untuk setiap proses berikutnya:
     - Dipilih proses dengan **burst time terpendek** yang sudah tiba (`AT ≤ CT` proses sebelumnya).
     - Waktu mulai (`IT`) dihitung:
       - Jika proses sudah tiba sebelum/saat proses sebelumnya selesai: `IT = CT proses sebelumnya`.
       - Jika belum: `IT = AT proses tersebut`.
     - Waktu selesai (`CT`) dihitung sebagai `IT + BT`.

### 5. **Perhitungan TAT dan WT**
   - **Turnaround Time (TAT)** = `CT - AT`.
   - **Waiting Time (WT)** = `TAT - BT`.
   - **Response Time (RT)** diisi dengan nilai `WT` karena pada SJF non-preemptive, proses tidak diinterupsi.

### 6. **Output**
   - Menampilkan tabel proses dengan detail `AT`, `BT`, `CT`, `TAT`, `WT`, dan `RT`.
   - Menghitung rata-rata `TAT` dan `WT`.

---

## Kelebihan dan Kekurangan
| **Kelebihan**                                                                 | **Kekurangan**                                                                 |
|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| Mengimplementasikan logika SJF non-preemptive dengan benar.                    | **Bubble Sort** tidak efisien untuk dataset besar.                           |
| Menangani kasus proses dengan `AT` sama dengan memilih `BT` terpendek.         | Variabel `it` (waktu mulai) redundan karena bisa dihitung dari `ct - bt`.    |
| Menghitung **TAT** dan **WT** sesuai rumus standar.                            | **Response Time (RT)** diisi dengan `WT`, tidak sesuai definisi RT sebenarnya.|
| Format output jelas dan terstruktur.                                           | Tidak menangani kasus `AT > CT` proses sebelumnya (proses belum tiba).       |
| Memastikan proses dengan `AT` lebih kecil diprioritaskan setelah sorting.      | Contoh output memiliki nilai WT tidak valid (misal: 55 untuk P3).            |

---
