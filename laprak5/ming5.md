
# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA)</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang terdiri dari rangkaian node, di mana setiap node menyimpan data dan pointer ke node berikutnya. Operasi dasarnya meliputi pencarian, penambahan, penghapusan, serta manipulasi seperti menyalin dan membalik list. Proses pencarian dilakukan dengan menelusuri tiap node hingga data ditemukan. Dalam C++, semua operasi ini diimplementasikan menggunakan ADT (Abstract Data Type) melalui file header (*.h) dan implementasi (*.cpp), sehingga pengelolaan memori menjadi lebih fleksibel dibandingkan array statis.


## Guided

### linklist
```cpp
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

buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya(modul 4 nomor 1)
```go
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

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
    AntrianPembeli() {
        front = rear = nullptr;
    }
    
    ~AntrianPembeli() {
        while (front != nullptr) {
            Pembeli* temp = front;
            front = front->next;
            delete temp;
        }
        rear = nullptr;
    }
    
    void tambahAntrian() {
        Pembeli* pembeliBaru = new Pembeli;
        
        cout << "\n---TAMBAH ANTRIAN---" << endl;
        cout << "Nama Pembeli: ";
        getline(cin, pembeliBaru->nama);
        cout << "Pesanan: ";
        getline(cin, pembeliBaru->pesanan);
        
        pembeliBaru->next = nullptr;
        
        if (rear == nullptr) {
            front = rear = pembeliBaru;
        } else {
            rear->next = pembeliBaru;
            rear = pembeliBaru;
        }
        
        cout << "Pembeli " << pembeliBaru->nama << " telah ditambahkan ke antrian!" << endl;
    }
    
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
            rear = nullptr;
        }
        
        delete temp;
        cout << "Antrian berhasil dilayani!" << endl;
    }
    
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
    
    string toLower(string str) {
        transform(str.begin(), str.end(), str.begin(), ::tolower);
        return str;
    }
    
    void cariPembeli() {
        if (front == nullptr) {
            cout << "\nAntrian kosong! Tidak ada data untuk dicari." << endl;
            return;
        }
        
        string namaCari;
        cout << "\n---CARI PEMBELI---" << endl;
        cout << "Masukkan nama pembeli yang dicari: ";
        getline(cin, namaCari);
        
        Pembeli* current = front;
        int nomor = 1;
        bool ditemukan = false;
        
        cout << "\n---HASIL PENCARIAN---" << endl;
        
        while (current != nullptr) {
            if (toLower(current->nama).find(toLower(namaCari)) != string::npos) {
                if (!ditemukan) {
                    cout << "No.\tNama Pembeli\tPesanan" << endl;
                    cout << "-------------------------------" << endl;
                    ditemukan = true;
                }
                cout << nomor << ".\t" << current->nama << "\t\t" << current->pesanan << endl;
            }
            current = current->next;
            nomor++;
        }
        
        if (!ditemukan) {
            cout << "Pembeli dengan nama '" << namaCari << "' tidak ditemukan dalam antrian." << endl;
        }
    }
};

void menu() {
    AntrianPembeli antrian;
    int pilihan;
    
    do {
        cout << "\n====================================" << endl;
        cout << " ---SISTEM ANTRIAN PEMBELI--- " << endl;
        cout << "====================================" << endl;
        cout << "1. Tambah Antrian" << endl;
        cout << "2. Layani Antrian" << endl;
        cout << "3. Tampilkan Antrian" << endl;
        cout << "4. Cari Pembeli" << endl;
        cout << "5. Keluar" << endl;
        cout << "====================================" << endl;
        cout << "Pilihan Anda: ";
        cin >> pilihan;
        
        cin.ignore();
        
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
                antrian.cariPembeli();
                break;
            case 5:
                cout << "\nTerima kasih! Program selesai." << endl;
                break;
            default:
                cout << "\nPilihan tidak valid!" << endl;
        }
    } while (pilihan != 5);
}

int main() {
    menu();
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul2no2.jpg)

Penjelasan Kode:

### Soal 2

gunakan latihan pada pertemuan minggun ini dan tambahkan searching untuk mencari buku berdasarkan judul, penulis, dan ISBN
```go
#include <iostream>
using namespace std;

struct Buku {
    string isbn;
    string judul;
    string penulis;
    Buku* next;
};

Buku* head = nullptr;

void tambah() {
    Buku* baru = new Buku();
    cout << "ISBN: "; cin >> baru->isbn;
    cout << "Judul: "; cin.ignore(); getline(cin, baru->judul);
    cout << "Penulis: "; getline(cin, baru->penulis);
    baru->next = nullptr;
    
    if (head == nullptr) {
        head = baru;
    } else {
        Buku* temp = head;
        while (temp->next != nullptr) temp = temp->next;
        temp->next = baru;
    }
    cout << "Berhasil!\n";
}

void hapus() {
    string isbn;
    cout << "ISBN: "; cin >> isbn;
    
    if (head == nullptr) {
        cout << "Kosong!\n";
        return;
    }
    
    if (head->isbn == isbn) {
        Buku* temp = head;
        head = head->next;
        delete temp;
        cout << "Dihapus!\n";
        return;
    }
    
    Buku* temp = head;
    while (temp->next != nullptr && temp->next->isbn != isbn) {
        temp = temp->next;
    }
    
    if (temp->next != nullptr) {
        Buku* hapus = temp->next;
        temp->next = temp->next->next;
        delete hapus;
        cout << "Dihapus!\n";
    } else {
        cout << "Tidak ada!\n";
    }
}

void perbarui() {
    string isbn;
    cout << "ISBN: "; cin >> isbn;
    
    Buku* temp = head;
    while (temp != nullptr && temp->isbn != isbn) {
        temp = temp->next;
    }
    
    if (temp == nullptr) {
        cout << "Tidak ada!\n";
        return;
    }
    
    cout << "Judul baru: "; cin.ignore(); getline(cin, temp->judul);
    cout << "Penulis baru: "; getline(cin, temp->penulis);
    cout << "Diperbarui!\n";
}

void lihat() {
    if (head == nullptr) {
        cout << "Kosong!\n";
        return;
    }
    
    Buku* temp = head;
    while (temp != nullptr) {
        cout << "\nISBN: " << temp->isbn;
        cout << "\nJudul: " << temp->judul;
        cout << "\nPenulis: " << temp->penulis << "\n";
        temp = temp->next;
    }
}

void cari() {
    if (head == nullptr) {
        cout << "Kosong!\n";
        return;
    }

    int pilihan;
    string kataKunci;
    bool ditemukan = false;

    cout << "\nCari berdasarkan:\n";
    cout << "1. ISBN\n";
    cout << "2. Judul\n";
    cout << "3. Penulis\n";
    cout << "Pilih: "; cin >> pilihan;
    cin.ignore(); // Membersihkan newline dari buffer

    cout << "Masukkan kata kunci: ";
    getline(cin, kataKunci);

    Buku* temp = head;
    while (temp != nullptr) {
        bool cocok = false;
        switch (pilihan) {
            case 1:
                if (temp->isbn == kataKunci) cocok = true;
                break;
            case 2:
                if (temp->judul.find(kataKunci) != string::npos) cocok = true;
                break;
            case 3:
                if (temp->penulis.find(kataKunci) != string::npos) cocok = true;
                break;
            default:
                cout << "Pilihan tidak valid!\n";
                return;
        }

        if (cocok) {
            cout << "\nISBN: " << temp->isbn;
            cout << "\nJudul: " << temp->judul;
            cout << "\nPenulis: " << temp->penulis << "\n";
            ditemukan = true;
        }
        temp = temp->next;
    }

    if (!ditemukan) {
        cout << "Tidak ditemukan!\n";
    }
}

int main() {
    int pilih;
    
    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Tambah Buku" << endl;
        cout << "2. Hapus Buku" << endl;
        cout << "3. Perbarui Buku" << endl;
        cout << "4. Lihat Buku" << endl;
        cout << "5. Cari Buku" << endl;
        cout << "6. Keluar" << endl;
        cout << "Pilih: "; cin >> pilih;
        
        if (pilih == 1) tambah();
        else if (pilih == 2) hapus();
        else if (pilih == 3) perbarui();
        else if (pilih == 4) lihat();
        else if (pilih == 5) cari();
        
    } while (pilih != 6);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul2no2.jpg)

Penjelasan Kode:

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

