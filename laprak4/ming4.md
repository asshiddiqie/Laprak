# <h1 align="center">Laporan Praktikum Modul 4 <br> SINGLY LINKED LIST (BAGIAN PERTAMA)</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129 </p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang terdiri dari node-node yang terhubung secara linear, di mana setiap node berisi data dan pointer yang menunjuk ke node berikutnya, membentuk rantai searah yang diakhiri NULL. Struktur ini memungkinkan penambahan dan penghapusan elemen secara efisien tanpa perlu pergeseran data, dengan operasi dasar meliputi penyisipan, penghapusan, penelusuran, dan pembaruan data yang diimplementasikan menggunakan pointer untuk mengelola hubungan antar elemen.

## Guided

### linklist
```go
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}


void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next
    }
    cout << "NULL\n";
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
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
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
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
    
    // Destructor - YANG SUDAH DIBENARKAN
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
        
        cout << "\n=== TAMBAH ANTRIAN ===" << endl;
        cout << "Nama Pembeli: ";
        cin.ignore();
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
        cout << "\n=== MELAYANI ANTRIAN ===" << endl;
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
        
        cout << "\n=== DAFTAR ANTRIAN ===" << endl;
        cout << "No.\tNama Pembeli\t\tPesanan" << endl;
        cout << "----------------------------------------" << endl;
        
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
        cout << "\n=== SISTEM ANTRIAN PEMBELI ===" << endl;
        cout << "1. Tambah Antrian" << endl;
        cout << "2. Layani Antrian" << endl;
        cout << "3. Tampilkan Antrian" << endl;
        cout << "4. Keluar" << endl;
        cout << "Pilihan Anda: ";
        cin >> pilihan;
        
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
> ![Screenshot bagian x](output/modul2no1.jpg)
> 
Program ini membuat transpose dari matriks 3x3. Transpose matriks adalah operasi menukar baris menjadi kolom (elemen baris ke-i menjadi kolom ke-i).

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
> ![Screenshot bagian x](output/modul2no2.jpg)

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


