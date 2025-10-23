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

Buatlah ADT Doubly Linked list sebagai berikut di dalam file “Doublylist.h”:
```go
Type infotype : kendaraan < 
    nopol : string 
    warna : string 
    thnBuat : integer 
> 
Type address : pointer to ElmList 
Type ElmList < 
    info : infotype 
    next :address 
    prev : address 
> 
 
Type List < 
    First : address 
    Last : address 
> 
procedure CreateList( input/output L : List ) 
function alokasi( x : infotype ) → address 
procedure dealokasi(input/output P : address ) 
procedure printInfo( input L : List ) 
procedure insertLast(input/output L : List,  
   input P : address ) 
```
Buatlah implementasi ADT Doubly Linked list pada file “Doublylist.cpp” dan coba hasil 
implementasi ADT pada file “main.cpp”. 

### file Doublylist.cpp
```go
#include "Doublylist.h"
#include <iostream>

using namespace std;

void createList(List &L) {
    L.first = NULL;
    L.last = NULL;
}

address alokasi(infotype x) {
    address P = new elmlist;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    cout << "\nDATA LIST KENDARAAN\n";
    cout << "===================\n";
    
    if (L.first == NULL) {
        cout << "List kosong!\n";
        return;
    }
    
    address P = L.first;
    while (P != NULL) {
        cout << "No Polisi : " << P->info.nopol << endl;
        cout << "Warna     : " << P->info.warna << endl;
        cout << "Tahun     : " << P->info.thnBuat << endl;
        cout << "-------------------\n";
        P = P->next;
    }
}

void insertLast(List &L, address P) {
    if (L.first == NULL) {
        // List kosong
        L.first = P;
        L.last = P;
    } else {
        // List tidak kosong
        L.last->next = P;
        P->prev = L.last;
        L.last = P;
    }
}
```
### file Doublylist.h
```go
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H
#include <string>

using namespace std;

struct infotype {
    string nopol;
    string warna;
    int thnBuat;
};

typedef struct elmlist *address;

struct elmlist {
    infotype info;
    address next;
    address prev;
};

struct List {
    address first;
    address last;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);

#endif
```
### file main.cpp
```go
#include <iostream>
#include "Doublylist.h"

using namespace std;

int main() {
    List L;
    createList(L);
    
    char lanjut;
    
    cout << "=== PROGRAM INPUT KENDARAAN ===\n";
    
    do {
        infotype kendaraan;
        
        cout << "\nMasukkan nomor polisi: ";
        cin >> kendaraan.nopol;
        cout << "Masukkan warna kendaraan: ";
        cin >> kendaraan.warna;
        cout << "Masukkan tahun kendaraan: ";
        cin >> kendaraan.thnBuat;
        
        address P = alokasi(kendaraan);
        insertLast(L, P);
        
        cout << "Data berhasil ditambahkan!\n";
        cout << "Tambah data lagi? (y/n): ";
        cin >> lanjut;
        
    } while (lanjut == 'y' || lanjut == 'Y');
    
    // Tampilkan semua data
    printInfo(L);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul3no2.jpg)


Penjelasan 
**File: Doublylist.h (File Header - Antarmuka)**
File ini berisi definisi struktur data (`infotype`, `elmlist`, `List`) dan deklarasi fungsi-fungsi yang tersedia (`CreateList()`, `alokasi()`, `insertLast()`, dll). Dilengkapi dengan header guard untuk mencegah inklusi ganda. File ini berperan sebagai penghubung antara implementasi dan program utama - baik `Doublylist.cpp` maupun `main.cpp` perlu meng-include file ini untuk mengakses struktur data dan fungsi yang ada.

**File: Doublylist.cpp (File Implementasi)**
File ini mengimplementasikan semua fungsi yang telah dideklarasikan di header. Setiap fungsi diberikan kode programnya di sini, seperti:
- `CreateList()`: Membuat list kosong
- `alokasi()`: Membuat elemen baru
- `insertLast()`: Menambah data di akhir list
- `findElm()`: Mencari data berdasarkan nomor polisi
File ini bergantung pada `Doublylist.h` untuk mengetahui apa yang harus diimplementasikan.

**File: main.cpp (Program Utama)**
File program utama yang menggunakan fungsi-fungsi dari ADT. File ini:
- Meng-include `Doublylist.h` untuk mengetahui fungsi apa yang tersedia
- Memanggil fungsi-fungsi seperti `CreateList()`, `alokasi()`, `insertLast()`
- Tidak perlu tahu detail cara kerja fungsi-fungsi tersebut
- Cukup menggunakan fungsi sesuai deklarasi di header

**Hubungan Ketiganya:**
`Doublylist.h` sebagai kontrak → `Doublylist.cpp` sebagai pelaksana → `main.cpp` sebagai pengguna. Ketika dikompilasi bersama (`g++ main.cpp Doublylist.cpp -o program`), ketiga file digabungkan menjadi satu program yang utuh, menerapkan prinsip pemrograman modular dalam ADT Doubly Linked List.

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
