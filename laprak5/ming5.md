
# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA)</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang terdiri dari rangkaian node, di mana setiap node menyimpan data dan pointer ke node berikutnya. Operasi dasarnya meliputi pencarian, penambahan, penghapusan, serta manipulasi seperti menyalin dan membalik list. Proses pencarian dilakukan dengan menelusuri tiap node hingga data ditemukan. Dalam C++, semua operasi ini diimplementasikan menggunakan ADT (Abstract Data Type) melalui file header (*.h) dan implementasi (*.cpp), sehingga pengelolaan memori menjadi lebih fleksibel dibandingkan array statis.


## Guided

### array
```go
#include <iostream>
using namespace std;

int main() {

    int nilai[5] = {1, 2, 3, 4, 5};

    for ( int i = 0;  i < 5; i++)
    {
       
        cout << "elemen ke-" << i << "=" << nilai[i] << endl;
    }
    return 0;
} 
```

### array 2
```go
#include <iostream>
using namespace std;

int main()
{
    char pesan_array[] = "Nasi Padang";
    char *pesan_pointer = "Ayam Bakar 23";

    cout << "String Array : " << pesan_array << endl;
    cout << "String Pointer : " << pesan_pointer << endl;

    // Mengubah karakter dalam array diperbolehkan
    pesan_array[0] = 'h';
    cout << "String Array setelah diubah: " << pesan_array << endl;

    // Pointer dapat diubah untuk menunjuk ke string lain
    pesan_pointer = "Sariaman";
    cout << "String Pointer setelah menunjuk ke string lain: " << pesan_pointer << endl;

    return 0;
}

```

## Unguided

### Soal 1

Buatlah sebuah program untuk melakukan transpose pada sebuah matriks persegi berukuran 3x3. Operasi transpose adalah mengubah baris menjadi kolom dan sebaliknya. Inisialisasi matriks awal di dalam kode, kemudian buat logika untuk melakukan transpose dan simpan hasilnya ke dalam matriks baru. Terakhir, tampilkan matriks awal dan matriks hasil transpose.

Contoh Output:

Matriks Awal:

1 2 3

4 5 6

7 8 9

Matriks Hasil Transpose:

1 4 7

2 5 8

3 6 9


```go
#include <iostream>
using namespace std;

int main() {
    int matriks[3][3], transpose[3][3];
    
    // Input matriks
    cout << "Masukkan elemen matriks 3x3:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cin >> matriks[i][j];
        }
    }
    
    // Proses transpose
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            transpose[j][i] = matriks[i][j];
        }
    }
    
    // Tampilkan matriks awal
    cout << "\nMatriks Awal:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << matriks[i][j] << " ";
        }
        cout << endl;
    }
    
    // Tampilkan hasil transpose
    cout << "\nMatriks Transpose:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << transpose[i][j] << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul2no1.jpg)
> 
Program ini membuat transpose dari matriks 3x3. Transpose matriks adalah operasi menukar baris menjadi kolom (elemen baris ke-i menjadi kolom ke-i).

### Soal 2

Buatlah program yang menunjukkan penggunaan call by reference. Buat sebuah prosedur bernama kuadratkan yang menerima satu parameter integer secara referensi (&). Prosedur ini akan mengubah nilai asli variabel yang dilewatkan dengan nilai kuadratnya. Tampilkan nilai variabel di main() sebelum dan sesudah memanggil prosedur untuk membuktikan perubahannya. 

Contoh Output:

Nilai awal: 5
Nilai setelah dikuadratkan: 25

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

1. void = Prosedur ini tidak mengembalikan nilai (return). Dia hanya mengubah nilai parameter yang dikirim.
2. int &angka = Parameter dengan tanda & (ampersand). Ini adalah KUNCI dari call by reference!
    & membuat angka menjadi alias (nama lain) untuk variabel asli
    Bukan salinan, tapi referensi langsung ke variabel asli
3. angka = angka * angka = Mengkuadratkan nilai
    Jika angka = 5, maka 5 × 5 = 25
    Karena angka adalah reference, perubahan ini langsung mempengaruhi variabel asli di main()

Program ini berfungsi untuk mengkuadratkan bilangan yang dimasukkan pengguna menggunakan parameter referensi sehingga nilai variabel langsung berubah.

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

