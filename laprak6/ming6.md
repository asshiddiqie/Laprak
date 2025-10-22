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

buatlah single linked list untuk Antrian yang menyimpan data pembeli( nama dan pesanan). program memiliki beberapa menu seperti tambah antrian,  layani antrian(hapus), dan tampilkan antrian. \*antrian pertama harus yang pertama dilayani


```go
#include <iostream>
#include <string>
using namespace std;

// Struktur data untuk pembeli
struct Pembeli {
    string nama;
    string pesanan;
    Pembeli* next;
};

class AntrianPembeli {
private:
    Pembeli* front;
    Pembeli* rear;
    
public:
    // Constructor
    AntrianPembeli() {
        front = rear = nullptr;
    }
    
    // Destructor - SUDAH BENAR
    ~AntrianPembeli() {
        while (front != nullptr) {
            Pembeli* temp = front;
            front = front->next;
            delete temp;
        }
        rear = nullptr;
    }
    
    // Fungsi untuk menambah antrian
    void tambahAntrian() {
        Pembeli* pembeliBaru = new Pembeli;
        
        cout << "\n---TAMBAH ANTRIAN---" << endl;
        cout << "Nama Pembeli: ";
        getline(cin, pembeliBaru->nama);
        cout << "Pesanan: ";
        getline(cin, pembeliBaru->pesanan);
        
        pembeliBaru->next = nullptr;
        
        if (rear == nullptr) {
            // Jika antrian kosong
            front = rear = pembeliBaru;
        } else {
            // Tambah di belakang
            rear->next = pembeliBaru;
            rear = pembeliBaru;
        }
        
        cout << "Pembeli " << pembeliBaru->nama << " telah ditambahkan ke antrian!" << endl;
    }
    
    // Fungsi untuk melayani antrian (menghapus dari depan)
    void layaniAntrian() {
        if (front == nullptr) {
            cout << "\nAntrian kosong! Tidak ada yang dilayani." << endl;
            return;
        }
        
        Pembeli* temp = front;
        cout << "\n---MELAYANI ANTRIAN---" << endl;
        cout << "Melayani: " << front->nama << endl;
        cout << "Pesanan: " << front->pesanan << endl;
        
        front = front->next;
        
        if (front == nullptr) {
            rear = nullptr; // Antrian menjadi kosong
        }
        
        delete temp;
        cout << "Antrian berhasil dilayani!" << endl;
    }
    
    // Fungsi untuk menampilkan antrian
    void tampilkanAntrian() {
        if (front == nullptr) {
            cout << "\nAntrian kosong!" << endl;
            return;
        }
        
        Pembeli* current = front;
        int nomor = 1;
        
        cout << "\n---DAFTAR ANTRIAN---" << endl;
        cout << "No.\tNama Pembeli\tPesanan" << endl;
        cout << "-------------------------------" << endl;
        
        while (current != nullptr) {
            cout << nomor << ".\t" << current->nama << "\t\t" << current->pesanan << endl;
            current = current->next;
            nomor++;
        }
    }
};

// Menu utama
void menu() {
    AntrianPembeli antrian;
    int pilihan;
    
    do {
        cout << "\n ---SISTEM ANTRIAN PEMBELI--- " << endl;
        cout << "1. Tambah Antrian" << endl;
        cout << "2. Layani Antrian" << endl;
        cout << "3. Tampilkan Antrian" << endl;
        cout << "4. Keluar" << endl;
        cout << "Pilihan Anda: ";
        cin >> pilihan;
        
        cin.ignore(); //Membersihkan newline character
        
        switch (pilihan) {
            case 1:
                antrian.tambahAntrian();
                break;
            case 2:
                antrian.layaniAntrian();
                break;
            case 3:
                antrian.tampilkanAntrian();
                break;
            case 4:
                cout << "\nTerima kasih! Program selesai." << endl;
                break;
            default:
                cout << "\nPilihan tidak valid!" << endl;
        }
    } while (pilihan != 4);
}

int main() {
    menu();
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul4no1.jpg)
> 
Program diatas mengimplementasikan linked list dalam C++ dengan dua metode reversal - iteratif menggunakan tiga pointer untuk membalik node secara sequential dalam loop, dan rekursif yang memanfaatkan stack call function untuk membalik dari node terakhir. Program menyediakan menu interaktif untuk menambah data, menampilkan list dalam format visual dengan tanda panah, serta memilih metode reversal yang diinginkan, dilengkapi destructor untuk mencegah memory leak dengan menghapus semua node secara otomatis.
### Soal 2

buatlah program kode untuk membalik (reverse) singly linked list (1-2-3 menjadi 3-2-1) 

```go
#include <iostream>
using namespace std;

// Struktur node untuk linked list
struct Node {
    int data;
    Node* next;
    
    Node(int val) {
        data = val;
        next = nullptr;
    }
};

class LinkedList {
private:
    Node* head;
    
public:
    LinkedList() {
        head = nullptr;
    }
    
    // Fungsi untuk menambah node di akhir
    void tambahNode(int data) {
        Node* newNode = new Node(data);
        
        if (head == nullptr) {
            head = newNode;
            return;
        }
        
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    
    // Fungsi untuk menampilkan linked list
    void tampilkanList() {
        Node* temp = head;
        cout << "Linked List: ";
        while (temp != nullptr) {
            cout << temp->data;
            if (temp->next != nullptr) {
                cout << " -> ";
            }
            temp = temp->next;
        }
        cout << " -> NULL" << endl;
    }
    
    // Fungsi untuk reverse linked list
    void reverseIteratif() {
        Node* prev = nullptr;
        Node* current = head;
        Node* next = nullptr;
        
        while (current != nullptr) {
            next = current->next;  // Simpan node berikutnya
            current->next = prev;  // Balik pointer
            prev = current;        // Geser prev
            current = next;        // Geser current
        }
        
        head = prev; // prev sekarang menjadi head baru
    }
    
    // Fungsi untuk reverse linked list (rekursif)
    Node* reverseRekursif(Node* node) {
        // Base case
        if (node == nullptr || node->next == nullptr) {
            return node;
        }
        
        // Reverse sisa list
        Node* rest = reverseRekursif(node->next);
        
        // Letakkan node pertama di akhir
        node->next->next = node;
        node->next = nullptr;
        
        return rest;
    }
    
    void reverseRekursif() {
        head = reverseRekursif(head);
    }
    
    // Destructor untuk menghapus semua node
    ~LinkedList() {
        Node* current = head;
        Node* next;
        
        while (current != nullptr) {
            next = current->next;
            delete current;
            current = next;
        }
        head = nullptr;
    }
};

// Menu untuk program reverse
void menuReverse() {
    LinkedList list;
    int pilihan, data;
    
    do {
        cout << "\n=== PROGRAM REVERSE LINKED LIST ===" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Tampilkan List" << endl;
        cout << "3. Reverse (Iteratif)" << endl;
        cout << "4. Reverse (Rekursif)" << endl;
        cout << "5. Keluar" << endl;
        cout << "Pilihan Anda: ";
        cin >> pilihan;
        
        switch (pilihan) {
            case 1:
                cout << "Masukkan data (angka): ";
                cin >> data;
                list.tambahNode(data);
                cout << "Data " << data << " ditambahkan!" << endl;
                break;
                
            case 2:
                list.tampilkanList();
                break;
                
            case 3:
                list.reverseIteratif();
                cout << "List berhasil di-reverse (iteratif)!" << endl;
                list.tampilkanList();
                break;
                
            case 4:
                list.reverseRekursif();
                cout << "List berhasil di-reverse (rekursif)!" << endl;
                list.tampilkanList();
                break;
                
            case 5:
                cout << "Program selesai." << endl;
                break;
                
            default:
                cout << "Pilihan tidak valid!" << endl;
        }
    } while (pilihan != 5);
}

int main() {
    menuReverse();
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul4no2.jpg)

Penjelasan Kode:

Program tersebut merupakan implementasi linked list dalam C++ yang terdiri dari struktur Node untuk menyimpan data integer dan pointer ke node berikutnya, serta kelas LinkedList yang menyediakan fungsi untuk menambah node di akhir list, menampilkan seluruh isi list, dan membalikkan urutan node menggunakan dua pendekatan yaitu reverse iteratif dengan tiga pointer yang melakukan traversal sambil membalik arah link setiap node, dan reverse rekursif yang menggunakan stack call recursive sampai node terakhir kemudian membalik pointer saat backtracking, dengan antarmuka menu interaktif yang memungkinkan pengguna untuk menambah data, menampilkan list, serta memilih metode reverse yang diinginkan, dilengkapi destructor untuk mencegah memory leak dengan menghapus semua node saat program berakhir.
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
