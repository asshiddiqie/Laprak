
# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA)</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

Singly Linked List adalah struktur data dinamis yang terdiri dari rangkaian node, di mana setiap node menyimpan data dan pointer ke node berikutnya. Operasi dasarnya meliputi pencarian, penambahan, penghapusan, serta manipulasi seperti menyalin dan membalik list. Proses pencarian dilakukan dengan menelusuri tiap node hingga data ditemukan. Dalam C++, semua operasi ini diimplementasikan menggunakan ADT (Abstract Data Type) melalui file header (*.h) dan implementasi (*.cpp), sehingga pengelolaan memori menjadi lebih fleksibel dibandingkan array statis.


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

Berikut penjelasan per kode/per fungsi secara detail:

---

**PENJELASAN PROGRAM PER KODE**

```cpp
#include <iostream>
using namespace std;
```
Penjelasan: Baris ini mengimpor library iostream yang berisi fungsi input-output seperti cout dan cin. Using namespace std memungkinkan kita menulis cout tanpa harus menulis std::cout.

```cpp
struct Buku {
    string isbn;
    string judul;
    string penulis;
    Buku* next;
};
```
Penjelasan: Membuat struktur data Buku yang berisi 4 anggota. Variabel isbn, judul, dan penulis bertipe string untuk menyimpan data buku. Variabel next bertipe pointer Buku* yang menunjuk ke buku berikutnya, inilah yang membuat struktur ini menjadi linked list.

```cpp
Buku* head = nullptr;
```
Penjelasan: Mendeklarasikan variabel global head sebagai pointer yang menunjuk ke buku pertama dalam linked list. Nilai nullptr menandakan list masih kosong. Head adalah pintu masuk untuk mengakses seluruh isi linked list.


**BAGIAN 2: FUNGSI TAMBAH BUKU**

```cpp
void tambah() {
```
Penjelasan: Mendeklarasikan fungsi tambah dengan return type void (tidak mengembalikan nilai).

```cpp
    Buku* baru = new Buku();
```
Penjelasan: Membuat node baru dengan mengalokasikan memory menggunakan operator new. Pointer baru menunjuk ke alamat memory yang baru dialokasikan untuk menyimpan satu struct Buku.

```cpp
    cout << "ISBN: "; 
    cin >> baru->isbn;
```
Penjelasan: Menampilkan prompt "ISBN: " dan membaca input dari user. Operator -> digunakan untuk mengakses member isbn dari struct yang ditunjuk oleh pointer baru. Cin membaca input sampai menemukan spasi atau enter.

```cpp
    cin.ignore();
```
Penjelasan: Membersihkan karakter newline (enter) yang tersisa di buffer input setelah menggunakan cin. Tanpa ini, getline() berikutnya akan langsung membaca newline kosong dan melewatkan input user.

```cpp
    cout << "Judul: "; 
    getline(cin, baru->judul);
    cout << "Penulis: "; 
    getline(cin, baru->penulis);
```
Penjelasan: Menggunakan getline() untuk membaca input judul dan penulis. Getline() dipilih karena bisa membaca input yang mengandung spasi, misalnya "Harry Potter and the Philosopher's Stone". Getline() membaca sampai menemukan karakter newline.

```cpp
    baru->next = nullptr;
```
Penjelasan: Mengeset pointer next dari node baru ke nullptr, menandakan bahwa node ini akan menjadi node terakhir dalam list (tidak ada node setelahnya).

```cpp
    if (head == nullptr) {
        head = baru;
```
Penjelasan: Mengecek apakah linked list masih kosong dengan memeriksa apakah head bernilai nullptr. Jika kosong, maka node baru langsung dijadikan head (node pertama).

```cpp
    } else {
        Buku* temp = head;
```
Penjelasan: Jika list sudah berisi data, deklarasikan pointer temp dan set nilainya sama dengan head. Pointer temp akan digunakan untuk traversal (menelusuri) linked list.

```cpp
        while (temp->next != nullptr) {
            temp = temp->next;
        }
```
Penjelasan: Loop while untuk mencari node terakhir. Selama next dari node saat ini bukan nullptr, pindahkan temp ke node berikutnya. Loop berhenti ketika temp berada di node terakhir (yang next-nya nullptr).

```cpp
        temp->next = baru;
    }
```
Penjelasan: Setelah menemukan node terakhir, hubungkan node terakhir dengan node baru dengan mengeset next dari node terakhir menunjuk ke node baru.

```cpp
    cout << "Buku berhasil ditambahkan!\n";
}
```
Penjelasan: Menampilkan pesan konfirmasi dan menutup fungsi tambah.


**BAGIAN 3: FUNGSI HAPUS BUKU**

```cpp
void hapus() {
    string isbn;
    cout << "Masukkan ISBN: "; 
    cin >> isbn;
```
Penjelasan: Mendeklarasikan variabel lokal isbn, menampilkan prompt, dan membaca input ISBN buku yang akan dihapus dari user.

```cpp
    if (head == nullptr) {
        cout << "Daftar kosong!\n";
        return;
    }
```
Penjelasan: Mengecek apakah list kosong. Jika head bernilai nullptr, tampilkan pesan dan keluar dari fungsi dengan return. Ini mencegah program crash saat mencoba mengakses node yang tidak ada.

```cpp
    if (head->isbn == isbn) {
        Buku* temp = head;
        head = head->next;
        delete temp;
        cout << "Buku berhasil dihapus!\n";
        return;
    }
```
Penjelasan: Kasus khusus jika buku yang dihapus adalah head (buku pertama). Simpan head lama ke pointer temp, geser head ke node berikutnya dengan head = head->next, hapus node lama dari memory dengan delete temp, tampilkan pesan, dan keluar dari fungsi.

```cpp
    Buku* temp = head;
    while (temp->next != nullptr && temp->next->isbn != isbn) {
        temp = temp->next;
    }
```
Penjelasan: Untuk kasus buku di tengah atau akhir, gunakan pointer temp untuk mencari node sebelum node yang akan dihapus. Loop berjalan dengan dua kondisi: temp->next tidak nullptr (belum sampai akhir) DAN ISBN dari node berikutnya tidak sama dengan ISBN yang dicari. Loop berhenti ketika menemukan node yang sebelum node target.

```cpp
    if (temp->next != nullptr) {
        Buku* hapus = temp->next;
        temp->next = temp->next->next;
        delete hapus;
        cout << "Buku berhasil dihapus!\n";
```
Penjelasan: Jika temp->next tidak nullptr berarti node target ditemukan. Simpan alamat node yang akan dihapus ke pointer hapus. Hubungkan node sebelumnya langsung ke node sesudahnya dengan temp->next = temp->next->next (melewati node yang dihapus). Hapus node dari memory dengan delete hapus dan tampilkan pesan konfirmasi.

```cpp
    } else {
        cout << "Buku tidak ditemukan!\n";
    }
}
```
Penjelasan: Jika temp->next bernilai nullptr, berarti loop sampai akhir tanpa menemukan ISBN yang dicari. Tampilkan pesan buku tidak ditemukan dan tutup fungsi.


**BAGIAN 4: FUNGSI PERBARUI BUKU**

```cpp
void perbarui() {
    string isbn;
    cout << "Masukkan ISBN: "; 
    cin >> isbn;
```
Penjelasan: Deklarasi fungsi perbarui, buat variabel isbn, dan minta input ISBN buku yang akan diperbarui.

```cpp
    Buku* temp = head;
    while (temp != nullptr && temp->isbn != isbn) {
        temp = temp->next;
    }
```
Penjelasan: Mencari node dengan ISBN yang sesuai. Mulai dari head, loop terus berjalan selama temp tidak nullptr (belum sampai akhir) DAN ISBN dari node saat ini tidak sama dengan ISBN yang dicari. Loop berhenti ketika menemukan node dengan ISBN yang cocok atau sampai akhir list.

```cpp
    if (temp == nullptr) {
        cout << "Buku tidak ditemukan!\n";
        return;
    }
```
Penjelasan: Jika loop selesai dan temp bernilai nullptr, berarti tidak ada node dengan ISBN yang dicari. Tampilkan pesan error dan keluar dari fungsi.

```cpp
    cin.ignore();
    cout << "Judul baru: "; 
    getline(cin, temp->judul);
    cout << "Penulis baru: "; 
    getline(cin, temp->penulis);
```
Penjelasan: Jika node ditemukan, bersihkan buffer dengan cin.ignore(), kemudian minta input judul baru dan penulis baru menggunakan getline(). Data langsung diupdate pada node yang ditunjuk oleh temp. ISBN tidak diubah karena berfungsi sebagai identifier unik.

```cpp
    cout << "Buku berhasil diperbarui!\n";
}
```
Penjelasan: Tampilkan pesan konfirmasi dan tutup fungsi.


**BAGIAN 5: FUNGSI LIHAT BUKU**

```cpp
void lihat() {
    if (head == nullptr) {
        cout << "Daftar kosong!\n";
        return;
    }
```
Penjelasan: Deklarasi fungsi lihat dan cek apakah list kosong. Jika head bernilai nullptr, tampilkan pesan dan keluar dari fungsi.

```cpp
    Buku* temp = head;
    int nomor = 1;
    cout << "\n=== DAFTAR BUKU ===\n";
```
Penjelasan: Buat pointer temp yang menunjuk ke head, buat variabel nomor dengan nilai awal 1 untuk penomoran buku, dan tampilkan header daftar buku.

```cpp
    while (temp != nullptr) {
        cout << "\nBuku ke-" << nomor++ << endl;
        cout << "ISBN    : " << temp->isbn << endl;
        cout << "Judul   : " << temp->judul << endl;
        cout << "Penulis : " << temp->penulis << endl;
        temp = temp->next;
    }
}
```
Penjelasan: Loop traversal dari head sampai akhir list. Selama temp tidak nullptr, tampilkan nomor buku dengan nomor++ (increment setelah digunakan), tampilkan ISBN, judul, dan penulis dari node saat ini, kemudian pindahkan temp ke node berikutnya dengan temp = temp->next. Loop berhenti ketika temp mencapai nullptr (akhir list).


**BAGIAN 6: FUNGSI CARI BUKU**

```cpp
void cari() {
    if (head == nullptr) {
        cout << "Daftar kosong!\n";
        return;
    }
```
Penjelasan: Deklarasi fungsi cari dan cek apakah list kosong dengan kondisi yang sama seperti fungsi sebelumnya.

```cpp
    int pilihan;
    string kataKunci;
    bool ditemukan = false;
```
Penjelasan: Deklarasi tiga variabel lokal. Variabel pilihan bertipe int untuk menyimpan pilihan mode pencarian (1, 2, atau 3). Variabel kataKunci bertipe string untuk menyimpan kata yang akan dicari. Variabel ditemukan bertipe bool dengan nilai awal false, berfungsi sebagai flag untuk menandai apakah ada hasil pencarian atau tidak.

```cpp
    cout << "\nCari berdasarkan:\n";
    cout << "1. ISBN\n";
    cout << "2. Judul\n";
    cout << "3. Penulis\n";
    cout << "Pilih: "; 
    cin >> pilihan;
    cin.ignore();
```
Penjelasan: Tampilkan menu pilihan pencarian, baca pilihan dari user, dan bersihkan buffer dengan cin.ignore().

```cpp
    cout << "Masukkan kata kunci: ";
    getline(cin, kataKunci);
```
Penjelasan: Minta user memasukkan kata kunci yang akan dicari menggunakan getline() agar bisa menangani input dengan spasi.

```cpp
    cout << "\n=== HASIL PENCARIAN ===\n";
    Buku* temp = head;
    while (temp != nullptr) {
        bool cocok = false;
```
Penjelasan: Tampilkan header hasil pencarian, buat pointer temp yang menunjuk ke head untuk memulai traversal, dan mulai loop untuk memeriksa setiap node. Untuk setiap node, deklarasikan variabel boolean cocok dengan nilai awal false untuk menandai apakah node saat ini memenuhi kriteria pencarian.

```cpp
        if (pilihan == 1) {
            if (temp->isbn == isbn) {
                cocok = true;
            }
        }
```
Penjelasan: Jika user memilih mode pencarian 1 (berdasarkan ISBN), lakukan perbandingan exact match menggunakan operator ==. Jika ISBN dari node saat ini sama persis dengan kata kunci, set cocok = true. Pencarian ISBN tidak mendukung partial matching.

```cpp
        else if (pilihan == 2) {
            if (temp->judul.find(kataKunci) != string::npos) {
                cocok = true;
            }
        }
```
Penjelasan: Jika user memilih mode pencarian 2 (berdasarkan judul), gunakan method find() dari class string. Method find() mencari substring kataKunci di dalam temp->judul dan mengembalikan posisi jika ditemukan, atau mengembalikan nilai string::npos jika tidak ditemukan. String::npos adalah konstanta khusus yang artinya "not found". Dengan kondisi != string::npos, kita mengecek apakah kata kunci ditemukan. Jika ditemukan (tidak sama dengan npos), set cocok = true. Metode ini memungkinkan partial matching, contoh: mencari "Potter" akan menemukan "Harry Potter".

```cpp
        else if (pilihan == 3) {
            if (temp->penulis.find(kataKunci) != string::npos) {
                cocok = true;
            }
        }
```
Penjelasan: Mode pencarian 3 (berdasarkan penulis) bekerja dengan cara yang sama persis seperti pencarian judul. Menggunakan method find() untuk mencari substring dalam nama penulis dengan dukungan partial matching.

```cpp
        if (cocok) {
            cout << "\nISBN    : " << temp->isbn << endl;
            cout << "Judul   : " << temp->judul << endl;
            cout << "Penulis : " << temp->penulis << endl;
            ditemukan = true;
        }
```
Penjelasan: Setelah mengecek kriteria pencarian, jika variabel cocok bernilai true (node memenuhi kriteria), tampilkan data lengkap dari node tersebut dan set flag ditemukan = true. Flag ini penting untuk menandai bahwa setidaknya ada satu hasil pencarian.

```cpp
        temp = temp->next;
    }
```
Penjelasan: Setelah memproses node saat ini, pindahkan pointer temp ke node berikutnya dengan temp = temp->next. Loop akan terus berjalan sampai semua node diperiksa. Ini memungkinkan program menemukan multiple results (lebih dari satu buku yang cocok).

```cpp
    if (!ditemukan) {
        cout << "\nTidak ditemukan!\n";
    }
}
```
Penjelasan: Setelah loop traversal selesai memeriksa semua node, cek flag ditemukan. Operator ! adalah NOT logic, jadi !ditemukan berarti "jika tidak ditemukan". Jika flag masih false (tidak ada hasil), tampilkan pesan "Tidak ditemukan!" dan tutup fungsi.


**BAGIAN 7: FUNGSI MAIN**

```cpp
int main() {
    int pilih;
```
Penjelasan: Fungsi main adalah entry point program. Deklarasikan variabel pilih bertipe int untuk menyimpan pilihan menu dari user.

```cpp
    do {
```
Penjelasan: Memulai loop do-while. Loop ini dipilih karena menu harus ditampilkan minimal satu kali sebelum mengecek kondisi. Berbeda dengan while yang cek kondisi dulu, do-while eksekusi dulu baru cek kondisi.

```cpp
        cout << "\n==============================\n";
        cout << "   MENU MANAJEMEN BUKU\n";
        cout << "==============================\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku\n";
        cout << "3. Perbarui Buku\n";
        cout << "4. Lihat Semua Buku\n";
        cout << "5. Cari Buku\n";
        cout << "6. Keluar\n";
        cout << "==============================\n";
        cout << "Pilih menu: "; 
        cin >> pilih;
```
Penjelasan: Menampilkan menu utama program dengan 6 pilihan dan membaca input pilihan dari user ke dalam variabel pilih.

```cpp
        if (pilih == 1) {
            tambah();
        } else if (pilih == 2) {
            hapus();
        } else if (pilih == 3) {
            perbarui();
        } else if (pilih == 4) {
            lihat();
        } else if (pilih == 5) {
            cari();
        } else if (pilih == 6) {
            cout << "\nTerima kasih!\n";
        } else {
            cout << "\nPilihan tidak valid!\n";
        }
```
Penjelasan: Struktur if-else bertingkat yang berfungsi sebagai dispatcher untuk memanggil fungsi yang sesuai dengan pilihan user. Jika pilih == 1 panggil fungsi tambah(), jika pilih == 2 panggil fungsi hapus(), dan seterusnya. Jika pilih == 6, hanya tampilkan pesan terima kasih tanpa memanggil fungsi (program akan keluar dari loop). Jika pilihan tidak valid (bukan 1-6), tampilkan pesan error.

```cpp
    } while (pilih != 6);
```
Penjelasan: Kondisi loop do-while. Loop akan terus berulang selama pilih tidak sama dengan 6. Ketika user memilih 6 (keluar), kondisi pilih != 6 menjadi false dan loop berhenti.

```cpp
    return 0;
}
```
Penjelasan: Mengembalikan nilai 0 ke sistem operasi yang menandakan program berakhir dengan sukses tanpa error. Ini menutup fungsi main dan mengakhiri program.

---

Penjelasan ini mencakup setiap baris kode dengan detail fungsinya!

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

