# <h1 align="center">Laporan Praktikum Modul 6 <br> DOUBLY LINKED LIST (BAGIAN PERTAMA) </h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129 </p>

## Dasar Teori

Doubly Linked List adalah struktur data berantai yang setiap elemennya memiliki dua pointer, yaitu `next` yang menunjuk ke elemen berikutnya dan `prev` yang menunjuk ke elemen sebelumnya, sehingga memungkinkan penelusuran data secara dua arah. Struktur ini memiliki dua pointer utama, yaitu `first` untuk menunjuk elemen pertama dan `last` untuk menunjuk elemen terakhir. Operasi dasarnya meliputi penyisipan (insert) di awal, akhir, atau di antara elemen; penghapusan (delete) pada posisi yang sama; serta operasi tambahan seperti pencarian, pembaruan, dan penampilan data. Dibandingkan dengan singly linked list, doubly linked list lebih fleksibel karena memudahkan manipulasi data di tengah atau akhir list. Struktur ini umumnya didefinisikan menggunakan pointer dengan tipe data bentukan berisi informasi (info), `next`, dan `prev`, serta dilengkapi prosedur seperti `createList`, `alokasi`, `dealokasi`, `insertLast`, `deleteFirst`, dan `findElm` untuk mengelola elemen dalam list.

## Guided

### double linked list
```go
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
};

Node* head = nullptr;
Node* tail = nullptr;

void insertDepan(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->prev = nullptr;
    newNode->next = head;

    if (head != nullptr)
       head->prev = newNode;
    else
       tail = newNode;

    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan. \n";
}

void insertBelakang(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    newNode->prev = tail;

    if (tail != nullptr)
        tail->next = newNode;
    else
        head = newNode;

    tail = newNode;
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int data) {
    Node* current = head;
    while (current != nullptr && current ->data != target)
        current = current->next;

    if(current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = current->next;
    newNode->prev = current;

    if (current->next != nullptr)
        current->next->prev = newNode;
    else
        tail = newNode;

    current->next = newNode;
    cout << "Data " << data << " berhasil disisipkan setelah " << target << ".\n";
}

void hapusDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = head;
    head = head->next;

    if (head != nullptr)
        head->prev = nullptr;
    else
        tail = nullptr;

    cout << "Data " << temp->data << " dihapus dari depan.\n";
    delete temp;
}

void hapusBelakang() {
    if  (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    Node* temp = tail;
    tail = tail->prev;

    if (tail != nullptr)
        tail->next = nullptr;
    else
        head = nullptr;
    
    cout << "Data " << temp->data << " dihapus dari belakang.\n";
    delete temp;
}

void hapusData(int target) {
    Node* current = head;
    while (current != nullptr && current->data != target)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << target << " tidak ditemukan.\n";
        return;
    }

    if (current == head)
        hapusDepan();
    else if (current == tail)
        hapusBelakang();
    else {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        cout << "Data " << target << " dihapus.\n";
        delete current;
    }
}

void updateData(int oldData, int newData) {
    Node* current = head;
    while (current != nullptr && current->data != oldData)
        current = current->next;

    if (current == nullptr) {
        cout << "Data " << oldData << " tidak ditemukan.\n";
        return;
    }

    current->data = newData;
    cout << "Data " << oldData << " diubah menjadi " << newData << ".\n";
}

void tampilDepan() {
    if (head == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari depan): ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->next;
    }
    cout << "\n";
}

// ====================================
// Fungsi: Tampilkan dari belakang
// ====================================
void tampilBelakang() {
    if (tail == nullptr) {
        cout << "List kosong.\n";
        return;
    }

    cout << "Isi list (dari belakang): ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data << " ";
        current = current->prev;
    }
    cout << "\n";
}

// ====================================
// MAIN PROGRAM (MENU INTERAKTIF)
// ====================================
int main() {
    int pilihan, data, target, oldData, newData;

    do {
        cout << "\n===== MENU DOUBLE LINKED LIST =====\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah Data\n";
        cout << "4. Hapus Depan\n";
        cout << "5. Hapus Belakang\n";
        cout << "6. Hapus Data Tertentu\n";
        cout << "7. Update Data\n";
        cout << "8. Tampil dari Depan\n";
        cout << "9. Tampil dari Belakang\n";
        cout << "0. Keluar\n";
        cout << "===================================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> data;
                insertSetelah(target, data);
                break;
            case 4:
                hapusDepan();
                break;
            case 5:
                hapusBelakang();
                break;
            case 6:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> target;
                hapusData(target);
                break;
            case 7:
                cout << "Masukkan data lama: ";
                cin >> oldData;
                cout << "Masukkan data baru: ";
                cin >> newData;
                updateData(oldData, newData);
                break;
            case 8:
                tampilDepan();
                break;
            case 9:
                tampilBelakang();
                break;
            case 0:
                cout << "👋 Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid.\n";
        }

    } while (pilihan != 0);

    return 0;
}
```

## Unguided

### Soal 1

Buatlah ADT pelajaran sebagai berikut di dalam file “pelajaran.h”:
```go
goType pelajaran <
namaMapel : string
kodeMapel : string
>
function create_pelajaran( namapel : string,
kodepel : string ) → pelajaran
procedure tampil_pelajaran( input pel : pelajaran )
```
Buatlah implementasi ADT pelajaran pada file “pelajaran.cpp”

Cobalah hasil implementasi ADT pada file “main.cpp”

### file pelajaran.cpp
```go
#include "pelajaran.h"
#include <iostream>
using namespace std;

// Implementasi function create_pelajaran
Pelajaran create_pelajaran(string namaMapel, string kodeMapel) {
    Pelajaran pel;
    pel.namaMapel = namaMapel;
    pel.kodeMapel = kodeMapel;
    return pel;
}

// Implementasi procedure tampil_pelajaran
void tampil_pelajaran(Pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}
```
### file pelajaran.h
```go
#ifndef PELAJARAN_H
#define PELAJARAN_H

#include <iostream>
#include <string>
using namespace std;

struct Pelajaran {
    string namaMapel;  // namawape1 -> namaMapel
    string kodeMapel;  // kodewape1 -> kodeMapel
};

Pelajaran create_pelajaran(string namaMapel, string kodeMapel);

void tampil_pelajaran(Pelajaran pel);

#endif
```
### file main.cpp
```go
#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namapel = "Struktur Data";
    string kodepel = "STD";  // kodepe1 -> kodepel

    Pelajaran pel = create_pelajaran(namapel, kodepel);
    tampil_pelajaran(pel);  // tampi1_pelajaran -> tampil_pelajaran
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul3no2.jpg)

File pelajaran.h: Header file yang berisi definisi struct pelajaran (dengan field namaPel dan kodePel) serta deklarasi fungsi create_pelajaran() dan tampil_pelajaran(), dilindungi header guard untuk mencegah multiple inclusion. File ini menjadi jembatan penghubung antara implementasi (pelajaran.cpp) dan program utama (main.cpp), dimana kedua file tersebut harus meng-include pelajaran.h untuk mengakses definisi struct dan fungsi yang tersedia.

File pelajaran.cpp: File implementasi yang meng-include pelajaran.h untuk mendapatkan deklarasi fungsi, kemudian memberikan body/isi dari fungsi create_pelajaran() yang membuat dan mengembalikan objek pelajaran, serta tampil_pelajaran() yang menampilkan data pelajaran. File ini bergantung pada pelajaran.h untuk mengetahui struktur data dan fungsi apa yang harus diimplementasikan, dan menyediakan fungsionalitas yang akan digunakan oleh main.cpp.

File main.cpp: Program utama yang meng-include pelajaran.h untuk mengakses struct dan fungsi, lalu menggunakan fungsi-fungsi yang sudah diimplementasikan di pelajaran.cpp dengan membuat objek pelajaran melalui create_pelajaran() dan menampilkannya dengan tampil_pelajaran(). File ini tidak perlu tahu bagaimana fungsi-fungsi tersebut diimplementasikan (information hiding), cukup tahu cara menggunakannya dari deklarasi di header file.

Hubungan Ketiganya: pelajaran.h sebagai interface → pelajaran.cpp sebagai implementasi → main.cpp sebagai user/client, sehingga ketika dikompilasi bersama (g++ main.cpp pelajaran.cpp -o program), compiler akan menggabungkan ketiganya menjadi satu program executable yang utuh, menerapkan prinsip modular programming dan encapsulation dalam ADT.

## Referensi

1. https://www.w3schools.com/cpp/cpp_for_loop_nested.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_arrays_loop.asp
4. https://www.w3schools.com/cpp/cpp_references.asp
5. https://www.w3schools.com/cpp/cpp_pointers.asp
6. https://www.w3schools.com/cpp/cpp_function_param.asp
7. https://www.w3schools.com/cpp/cpp_function_array.asp
8. https://www.geeksforgeeks.org/dsa/linked-list-data-structure/
9. https://en.wikipedia.org/wiki/Linked_list
