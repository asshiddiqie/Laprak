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

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “stack.h”:
```go
Type infotype : integer
Type Stack <
info : array [20] of integer
top : integer
>
procedure CreateStack( input/output S : Stack )
procedure push(input/output S : Stack,
input x : infotype)
function pop(input/output t S : Stack )
→ infotype
procedure printInfo( input S : Stack )
procedure balikStack(input/output S :
Stack )
```

Buatlah implementasi ADT Stack menggunakan Array pada file “stack.cpp” dan “main.cpp” 
```go
int main()
{
cout << "Hello world!" <<
endl;
Stack S;
createStack(S);
Push(S,3);
Push(S,4);
Push(S,8);
pop(S)
Push(S,2);
Push(S,3);
pop(S);
Push(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}
```
### file stack.h
```cpp
#ifndef STACK_H
#define STACK_H

typedef int infotype;

struct Stack {
    infotype info[20];
    int top;
};

// Prototype functions
void CreateStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
### file stack.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void CreateStack(Stack &S) {
    S.top = 0;
}

void push(Stack &S, infotype x) {
    if (S.top < 20) {
        S.info[S.top] = x;
        S.top++;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top > 0) {
        S.top--;
        return S.info[S.top];
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top - 1; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    CreateStack(temp);
    
    int originalSize = S.top;
    for (int i = 0; i < originalSize; i++) {
        push(temp, pop(S));
    }
    
    S = temp;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main()
{
    cout << "Hello world!" << endl;
    Stack S;
    CreateStack(S);
    push(S,3);
    push(S,4);
    push(S,8);
    pop(S);
    push(S,2);
    push(S,3);
    pop(S);
    push(S,9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
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
Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)
```cpp
int main()
{
cout << "Hello world!" << endl;
Stack S;
createStack(S);
pushAscending(S,3);
pushAscending(S,4);
pushAscending(S,8);
pushAscending(S,2);
pushAscending(S,3);
pushAscending(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}
```

### file stack.h
```cpp
#ifndef STACK_H
#define STACK_H

typedef int infotype;

struct Stack {
    infotype info[20];
    int top;
};

// Prototype functions
void CreateStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, infotype x);  // Ditambahkan

#endif
```
### file stack.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void CreateStack(Stack &S) {
    S.top = 0;
}

void push(Stack &S, infotype x) {
    if (S.top < 20) {
        S.info[S.top] = x;
        S.top++;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top > 0) {
        S.top--;
        return S.info[S.top];
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    cout << "[TOP] ";
    for (int i = S.top - 1; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    CreateStack(temp);
    
    int originalSize = S.top;
    for (int i = 0; i < originalSize; i++) {
        push(temp, pop(S));
    }
    
    S = temp;
}

void pushAscending(Stack &S, infotype x) {
    Stack temp;
    CreateStack(temp);
    
    while (S.top > 0 && S.info[S.top - 1] < x) {
        push(temp, pop(S));
    }
    
    push(S, x);
    
    while (temp.top > 0) {
        push(S, pop(temp));
    }
}
```
### file main.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main()
{
    cout << "Hello world!" << endl;
    Stack S;
    CreateStack(S);
    pushAscending(S,3);
    pushAscending(S,4);
    pushAscending(S,8);
    pushAscending(S,2);
    pushAscending(S,3);
    pushAscending(S,9);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
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
Tambahkan prosedur getInputStream( in/out S : Stack ). Prosedur akan terus membaca dan
menerima input user dan memasukkan setiap input ke dalam stack hingga user menekan
tombol enter. Contoh: gunakan cin.get() untuk mendapatkan inputan user.
### file stack.h
```cpp
#ifndef STACK_H
#define STACK_H

const int MAX_SIZE = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX_SIZE];
    int top;
};

void CreateStack(Stack &S);
void push(Stack &S, infotype x);
void pushAscending(Stack &S, infotype x);
void getInputStream(Stack &S);
void processNumberInput(Stack &S);  // Tambahan untuk nomor 3
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
### file stack.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void CreateStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX_SIZE - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

void pushAscending(Stack &S, infotype x) {
    if (S.top == -1) {
        push(S, x);
        return;
    }
    
    if (S.top >= MAX_SIZE - 1) {
        cout << "Stack penuh!" << endl;
        return;
    }
    
    Stack temp;
    CreateStack(temp);
    
    while (S.top >= 0 && S.info[S.top] < x) {
        push(temp, pop(S));
    }
    
    push(S, x);
    
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}

void getInputStream(Stack &S) {
    cout << "Masukkan karakter (tekan Enter untuk berhenti): ";
    
    char ch;
    while (true) {
        ch = cin.get();
        
        if (ch == '\n') {
            break;
        }
        
        if (S.top < MAX_SIZE - 1) {
            push(S, (int)ch);
        } else {
            cout << "Stack penuh! Input dihentikan." << endl;
            break;
        }
    }
}

void processNumberInput(Stack &S) {
    cout << "Masukkan angka: ";
    string input;
    cin >> input;
    
    // Push setiap digit angka ke stack
    for (int i = 0; i < input.length(); i++) {
        if (isdigit(input[i])) {
            int digit = input[i] - '0';  // Konversi char ke int
            push(S, digit);
        }
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (S.top == -1) {
        cout << "Stack kosong" << endl;
        return;
    }
    
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    CreateStack(temp);
    
    // Pindahkan semua elemen ke stack temporary
    int originalTop = S.top;
    for (int i = 0; i <= originalTop; i++) {
        push(temp, S.info[i]);
    }
    
    // Clear stack asli
    CreateStack(S);
    
    // Pindahkan kembali dari temp ke S (akan terbalik)
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}
```
### file main.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    
    Stack S;
    CreateStack(S);
    
    processNumberInput(S);
    printInfo(S);
    
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    
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
