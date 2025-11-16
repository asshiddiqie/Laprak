# <h1 align="center">Laporan Praktikum Modul 8 <br> QUEUE </h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129 </p>

## Dasar Teori

Stack adalah struktur data linear dengan prinsip **LIFO (Last In First Out)**, di mana elemen terakhir yang dimasukkan akan dikeluarkan pertama. Stack memiliki Queue adalah struktur data linear yang bekerja dengan prinsip **FIFO (First In First Out)**, artinya elemen yang pertama masuk menjadi elemen pertama yang keluar. Queue memiliki **Head** sebagai tempat menghapus elemen (dequeue) dan **Tail** sebagai tempat menambah elemen (enqueue). Operasi hanya dilakukan secara berurutan: tambah di belakang dan hapus di depan. Queue dapat dibuat menggunakan **linked list** (elemen tak terbatas dan fleksibel) atau **array** (elemen terbatas dan memerlukan pengaturan indeks). Dalam array terdapat tiga mekanisme: **head tetap–tail bergerak**, **head dan tail bergerak**, serta **circular queue** yang paling efisien karena head dan tail berputar tanpa pergeseran. Queue biasa digunakan pada sistem antrean seperti antrian layanan, buffer printer, dan penjadwalan proses CPU.



## Guided

### queue
```go
#include <iostream>
using namespace std;

// ukuran maksimal queue
#define MAX 5

// struktur queue
struct Queue {
   // datanya pake array yaa, bukan linked list
   int data[MAX];
   int head;
   int tail;
};

// membuat antrian kosong
void buat_queue (Queue &Q) {
   Q.head = -1;
   Q.tail = -1;
   // kenapa head dan tail-nya -1?
   // karena index array mulai dari 0
}

// cek queueu-nya kosong ngga?
bool cek_kosong (Queue Q) {
   return (Q.head == -1 && Q.tail == -1);
}

// cek queue-nya penuh ngga?
bool cek_penuh (Queue Q) {
   return (Q.tail == MAX - 1);
}

// menampilkan isi queue
void print_queue (Queue Q) {
   if (cek_kosong(Q)) {
      cout << "queue kosong" << endl;
   } else {
      cout << "queue : ";
      for (int i = Q.head; i <= Q.tail; i++) {
         cout << Q.data[i] << " -> ";
      }
      cout << endl;
   }
}

// menambahkan elemen (enqueue)
void enqueue (Queue &Q, int x) {
   if (cek_penuh(Q)) {
      cout << "queue sudah penuh, tidak bisa menambah data" << endl;
   } else {
      if (cek_kosong(Q)) {
         Q.head = Q.tail = 0;
      } else {
         Q.tail++;
      }

      Q.data[Q.tail] = x;
      cout << "menambahkan " << x << " ke dalam queue" << endl;
   }
}

// menghapus elemen (dequeue)
void dequeue (Queue &Q) {
   if (cek_kosong(Q)) {
      cout << "queue kosong, tidak ada yang bisa dihapus" << endl;
   } else {
      cout << "dequeue " << Q.data[Q.head] << " dari dalam queue" << endl;

      // jika hanya ada 1 elemen
      if (Q.head == Q.tail) {
         Q.head = Q.tail = -1;
      } else {
         // geser semua elemen ke depan/kiri
         // biar tempat kosong di depan dipenuhin
         // dan tempat di belakang bisa dikosongin
         for (int i = Q.head; i < Q.tail; i++) {
            Q.data[i] = Q.data[i + 1];
         }

         Q.tail--;
      }
   }
}

// eksekutor
int main() {
   Queue Q;
   buat_queue(Q);

   enqueue(Q, 5);
   enqueue(Q, 2);
   enqueue(Q, 7);
   print_queue(Q);

   dequeue(Q);
   print_queue(Q);

   enqueue(Q, 4);
   enqueue(Q, 9);
   print_queue(Q);

   dequeue(Q);
   dequeue(Q);
   print_queue(Q);

   return 0;
}
```

## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “queue.h”:
```go
Type infotype: integer
Type Queue: <
info : array [5] of infotype {index array dalam C++
dimulai dari 0}
head, tail : integer
>
procedure CreateQueue (input/output Q: Queue)
function isEmptyQueue (Q: Queue) → boolean
function isFullQueue (Q: Queue) → boolean
procedure enqueue (input/output Q: Queue, input x: infotype)
function dequeue (input/output Q: Queue) → infotype
procedure printInfo (input Q: Queue)
```

Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 1 (head diam, tail bergerak).
```go
int main() {
cout << "Hello World" << endl;
Queue Q;
createQueue(Q);
cout<<"----------------------"<<endl;
cout<<" H - T \t | Queue info"<<endl;
cout<<"----------------------"<<endl;
printInfo(Q);
enqueue(Q,5); printInfo(Q);
enqueue(Q,2); printInfo(Q);
enqueue(Q,7); printInfo(Q);
dequeue(Q); printInfo(Q);
enqueue(Q,4); printInfo(Q);
dequeue(Q); printInfo(Q);
dequeue(Q); printInfo(Q);
return 0;
}
```
### file queue.h
```cpp
#ifndef QUEUE_H
#define QUEUE_H

typedef int infotype;
const int MAX = 5; // ukuran queue

struct Queue {
    infotype info[MAX];
    int head;
    int tail;
};

// Prototype fungsi
void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
### file queue_alt1.cpp
```cpp
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh! Tidak bisa menambahkan " << x << endl;
        return;
    }
    
    if (isEmptyQueue(Q)) {
        Q.head = 0;
        Q.tail = 0;
    } else {
        Q.tail++;
    }
    Q.info[Q.tail] = x;
}

infotype dequeue(Queue &Q) {
    infotype x;
    
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong! Tidak bisa menghapus" << endl;
        return -1;
    }
    
    x = Q.info[Q.head];
    
    if (Q.head == Q.tail) {
        // hanya ada 1 elemen
        Q.head = -1;
        Q.tail = -1;
    } else {
        // geser semua elemen ke kiri
        for (int i = Q.head + 1; i <= Q.tail; i++) {
            Q.info[i-1] = Q.info[i];
        }
        Q.tail--;
    }
    
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " \t | ";
    
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);
    cout << "-------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "-------------------" << endl;
    printInfo(Q);
    
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul7no1.jpg)

Penjelasan :
```go
CreateStack(S) - Membuat stack kosong

push(S,3) - Menambahkan angka 3 → Stack: [3]

push(S,4) - Menambahkan angka 4 → Stack: [3, 4]

push(S,8) - Menambahkan angka 8 → Stack: [3, 4, 8]

pop(S) - Mengambil angka 8 → Stack: [3, 4]

push(S,2) - Menambahkan angka 2 → Stack: [3, 4, 2]

push(S,3) - Menambahkan angka 3 → Stack: [3, 4, 2, 3]

pop(S) - Mengambil angka 3 → Stack: [3, 4, 2]

push(S,9) - Menambahkan angka 9 → Stack: [3, 4, 2, 9]

printInfo(S) - Menampilkan stack dari atas ke bawah

balikStack(S) - Membalik urutan elemen stack

printInfo(S) - Menampilkan stack setelah dibalik
```
Penjelasan Output:
Sebelum dibalik: Elemen ditampilkan dari atas (TOP) ke bawah: 9 (paling atas), 2, 4, 3 (paling bawah)

Setelah dibalik: Urutan elemen terbalik: 3 (sekarang paling atas), 4, 2, 9 (sekarang paling bawah)

### Soal 2
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 2 (head bergerak, tail bergerak).

### file queue.h
```cpp
#ifndef QUEUE_H
#define QUEUE_H

typedef int infotype;
const int MAX = 5; // ukuran queue

struct Queue {
    infotype info[MAX];
    int head;
    int tail;
};

// Prototype fungsi
void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
### file queue_alt2.cpp
```cpp
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh! Tidak bisa menambahkan " << x << endl;
        return;
    }
    
    if (isEmptyQueue(Q)) {
        Q.head = 0;
        Q.tail = 0;
    } else {
        Q.tail++;
    }
    Q.info[Q.tail] = x;
}

infotype dequeue(Queue &Q) {
    infotype x;
    
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong! Tidak bisa menghapus" << endl;
        return -1;
    }
    
    x = Q.info[Q.head];
    
    if (Q.head == Q.tail) {
        // hanya ada 1 elemen
        Q.head = -1;
        Q.tail = -1;
    } else {
        Q.head++; // head bergerak maju
    }
    
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " \t | ";
    
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);
    cout << "-------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "-------------------" << endl;
    printInfo(Q);
    
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul7no2.jpg)

Penjelasan :
Prosedur pushAscending memastikan elemen selalu tersimpan dalam stack secara terurut menurun dari atas ke bawah. Setiap elemen baru akan disisipkan pada posisi yang tepat sehingga urutan tetap terjaga.

Algoritma Push Ascending:
1. Buat stack temporary kosong
2. Pindahkan elemen-elemen dari stack asli ke temporary selama elemen tersebut lebih kecil dari nilai yang akan dimasukkan
3. Masukkan nilai baru ke stack asli
4. Kembalikan semua elemen dari temporary ke stack asli

Alur Eksekusi:
```go
pushAscending(S,3)  → Stack: [3]

pushAscending(S,4)  → Stack: [4, 3]     (4 > 3, jadi 4 ditaruh di atas)

pushAscending(S,8)  → Stack: [8, 4, 3]  (8 > 4, jadi 8 ditaruh di atas)

pushAscending(S,2)  → Stack: [8, 4, 3, 2] (2 < 3, jadi 2 ditaruh di bawah)

pushAscending(S,3)  → Stack: [8, 4, 3, 3, 2] (3 sama dengan 3, jadi ditaruh setelahnya)

pushAscending(S,9)  → Stack: [9, 8, 4, 3, 3, 2] (9 > 8, jadi 9 ditaruh di paling atas)
```
Penjelasan Output:
Sebelum dibalik: Stack terurut menurun dari atas: 9 (terbesar), 8, 4, 3, 3, 2 (terkecil)

Setelah dibalik: Stack terurut menaik dari atas: 2 (terkecil), 3, 3, 4, 8, 9 (terbesar)


### Soal 3
Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 3 (head dan tail berputar).

### file queue.h
```cpp
#ifndef QUEUE_H
#define QUEUE_H

typedef int infotype;
const int MAX = 5; // ukuran queue

struct Queue {
    infotype info[MAX];
    int head;
    int tail;
};

// Prototype fungsi
void createQueue(Queue &Q);
bool isEmptyQueue(Queue Q);
bool isFullQueue(Queue Q);
void enqueue(Queue &Q, infotype x);
infotype dequeue(Queue &Q);
void printInfo(Queue Q);

#endif
```
### file queue_alt3.cpp
```cpp
#include <iostream>
#include "queue.h"
using namespace std;

void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return ((Q.tail + 1) % MAX == Q.head);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
        cout << "Queue penuh! Tidak bisa menambahkan " << x << endl;
        return;
    }
    
    if (isEmptyQueue(Q)) {
        Q.head = 0;
        Q.tail = 0;
    } else {
        Q.tail = (Q.tail + 1) % MAX;
    }
    Q.info[Q.tail] = x;
}

infotype dequeue(Queue &Q) {
    infotype x;
    
    if (isEmptyQueue(Q)) {
        cout << "Queue kosong! Tidak bisa menghapus" << endl;
        return -1;
    }
    
    x = Q.info[Q.head];
    
    if (Q.head == Q.tail) {
        // hanya ada 1 elemen
        Q.head = -1;
        Q.tail = -1;
    } else {
        Q.head = (Q.head + 1) % MAX;
    }
    
    return x;
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << " \t | ";
    
    if (isEmptyQueue(Q)) {
        cout << "empty queue";
    } else {
        int i = Q.head;
        while (true) {
            cout << Q.info[i] << " ";
            if (i == Q.tail) break;
            i = (i + 1) % MAX;
        }
    }
    cout << endl;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "queue.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    Queue Q;
    createQueue(Q);
    cout << "-------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "-------------------" << endl;
    printInfo(Q);
    
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul7no3.jpg)


Penjelasan 
Konsep Get Input Stream

Prosedur getInputStream membaca input dari user karakter per karakter dan menyimpan setiap digit angka ke dalam stack. Proses berhenti ketika user menekan tombol Enter.

Fitur Get Input Stream:
1. Membaca input karakter per karakter menggunakan cin.get()
2. Hanya menerima digit angka (0-9)
3. Mengabaikan karakter lain seperti huruf atau spasi
4. Berhenti membaca ketika mendeteksi newline character (\n)
5. Setiap digit dikonversi dari char ke integer sebelum dimasukkan ke stack

Contoh Eksekusi dengan Input "4729601":
```
Input: 4 7 2 9 6 0 1
Proses Push:
push(4) → Stack: [4]
push(7) → Stack: [4, 7]
push(2) → Stack: [4, 7, 2]
push(9) → Stack: [4, 7, 2, 9]
push(6) → Stack: [4, 7, 2, 9, 6]
push(0) → Stack: [4, 7, 2, 9, 6, 0]
push(1) → Stack: [4, 7, 2, 9, 6, 0, 1]
```

Penjelasan Output:
1. Input asli: 4-7-2-9-6-0-1 (dibaca dari kiri ke kanan)
2. Dalam stack: 4 (paling bawah), 7, 2, 9, 6, 0, 1 (paling atas)
3. Tampilan normal: Dari atas ke bawah: 1, 0, 6, 9, 2, 7, 4
4. Setelah dibalik: Urutan terbalik: 4, 7, 2, 9, 6, 0, 1


## Referensi

1. https://www.w3schools.com/cpp/cpp_for_loop_nested.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_arrays_loop.asp
4. https://www.w3schools.com/cpp/cpp_references.asp
5. https://www.w3schools.com/cpp/cpp_pointers.asp
6. https://www.w3schools.com/cpp/cpp_function_param.asp
7. https://www.w3schools.com/cpp/cpp_function_array.asp
8. https://www.w3schools.com/cpp/cpp_stacks.asp
