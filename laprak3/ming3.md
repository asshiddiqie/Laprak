
# <h1 align="center">Laporan Praktikum Modul 3 <br> ABSTRACT DATA TYPE (ADT)</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

C++ adalah bahasa pemrograman yang memiliki struktur dasar dimulai dari fungsi main(), menggunakan tipe data seperti int, float, char, dan string, operator untuk operasi matematika dan logika, struktur kontrol if-else untuk percabangan, loop for/while untuk perulangan, array untuk menyimpan banyak data, serta cin dan cout untuk input dan output, di mana setiap perintah diakhiri dengan semicolon (;) dan program harus dikompilasi terlebih dahulu sebelum dijalankan.

## Guided

### Soal 1

```go
#include <iostream>
#include <string>
using namespace std;

// Definisi struct
struct Mahasiswa {
    string nama;
    string nim;
    float ipk;
};

int main() {

    Mahasiswa mhs1;

    cout << "Masukkan Nama Mahasiswa: ";
    getline(cin, mhs1.nama);
    // cin >> mhs1.nama;
    cout << "Masukkan NIM Mahasiswa : ";
    cin >> mhs1.nim;
    cout << "Masukkan IPK Mahasiswa : ";
    cin >> mhs1.ipk;

    cout << "\n=== Data Mahasiswa ===" << endl;
    cout << "Nama : " << mhs1.nama << endl;
    cout << "NIM  : " << mhs1.nim << endl;
    cout << "IPK  : " << mhs1.ipk << endl;

    return 0;
}

```

### Soal 2
```go
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}
```
### Soal 3
```go
#include <iostream>
using namespace std;
int main()
{
    double tot_pembelian, diskon;
    cout << "total pembelian: Rp";
    cin >> tot_pembelian;
    diskon = 0;
    if (tot_pembelian >= 100000)
        diskon = 0.05 * tot_pembelian;
    cout << "besar diskon = Rp" << diskon;
}



int main()
{
    double tot_pembelian, diskon;
    cout << "total pembelian: Rp";
    cin >> tot_pembelian;
    diskon = 0;
    if (tot_pembelian >= 100000)
        diskon = 0.05 * tot_pembelian;
    else
        diskon = 0;
    cout << "besar diskon = Rp" << diskon;
}



int main()
{
    int kode_hari;
    cout << "Menentukan hari kerja/libur\n"<<endl;
    cout << "1=Senin 3=Rabu 5=Jumat 7=Minggu "<<endl;
    cout << "2=Selasa 4=Kamis 6=Sabtu "<<endl;
    cin >> kode_hari;
    switch (kode_hari)
    {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout<<"Hari Kerja";
        break;
    case 6:
    case 7:
        cout<<"Hari Libur";
        break;
    default:
        cout<<"Kode masukan salah!!!";
    }
    return 0;
}
```
### Soal 4
```go
#include <iostream>
using namespace std;
int main()
{
    int jum;
    cout << "jumlah perulangan: ";
    cin >> jum;
    for (int i = 0; i < jum; i++)
    {
        cout << "saya sahroni\n";
    }
    return 1;
}


int main()
{
    int i = 1;
    int jum;
    cin >> jum;
    do
    {
        cout << "bahlil ke-" << (i + 1) << endl;
        i++;
    } while (i < jum);
    return 0;
}
```
### Soal 5
```go
#include <iostream>
using namespace std;

// Prosedur: hanya menampilkan hasil, tidak mengembalikan nilai
void tampilkanHasil(double p, double l)
{
    cout << "\n=== Hasil Perhitungan ===" << endl;
    cout << "Panjang : " << p << endl;
    cout << "Lebar   : " << l << endl;
    cout << "Luas    : " << p * l << endl;
    cout << "Keliling: " << 2 * (p + l) << endl;
}

// Fungsi: mengembalikan nilai luas
double hitungLuas(double p, double l)
{
    return p * l;
}

// Fungsi: mengembalikan nilai keliling
double hitungKeliling(double p, double l)
{
    return 2 * (p + l);
}

int main()
{
    double panjang, lebar;

    cout << "Masukkan panjang: ";
    cin >> panjang;
    cout << "Masukkan lebar  : ";
    cin >> lebar;

    // Panggil fungsi
    double luas = hitungLuas(panjang, lebar);
    double keliling = hitungKeliling(panjang, lebar);

    cout << "\nDihitung dengan fungsi:" << endl;
    cout << "Luas      = " << luas << endl;
    cout << "Keliling  = " << keliling << endl;

    // Panggil prosedur
    tampilkanHasil(panjang, lebar);

    return 0;
}

```
### Soal 6
```go
#include <iostream>
using namespace std;
int main()
{
    string ch;
    cout << "Masukkan sebuah karakter: ";
    // cin >> ch;
    ch = getchar();  //Menggunakan getchar() untuk membaca satu karakter
    cout << "Karakter yang Anda masukkan adalah: " << ch << endl;
    return 0;
}

```
## Unguided


### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI dengan rumus 0.3*uts+0.4*uas+0.3*tugas.

```go
#include <iostream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilai(float uts, float uas, float tugas) {
    return (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

int main() {
    Mahasiswa data[10];
    int jumlah = 0;
    int pilihan;
    
    while(true) {
        cout << "\nMenu:" << endl;
        cout << "1. Tambah Data" << endl;
        cout << "2. Lihat Data" << endl;
        cout << "3. Keluar" << endl;
        cout << "Pilih: ";
        cin >> pilihan;
        
        if(pilihan == 1) {
            if(jumlah >= 10) {
                cout << "Data penuh!" << endl;
                continue;
            }
            
            cout << "Nama: ";
            cin.ignore();
            getline(cin, data[jumlah].nama);
            
            cout << "NIM: ";
            getline(cin, data[jumlah].nim);
            
            cout << "UTS: ";
            cin >> data[jumlah].uts;
            
            cout << "UAS: ";
            cin >> data[jumlah].uas;
            
            cout << "Tugas: ";
            cin >> data[jumlah].tugas;
            
            data[jumlah].nilaiAkhir = hitungNilai(data[jumlah].uts, data[jumlah].uas, data[jumlah].tugas);
            
            jumlah++;
            cout << "Data ditambah!" << endl;
            
        } else if(pilihan == 2) {
            if(jumlah == 0) {
                cout << "Belum ada data!" << endl;
                continue;
            }
            
            cout << "\nData Mahasiswa:" << endl;
            for(int i = 0; i < jumlah; i++) {
                cout << i+1 << ". " << data[i].nama << " - " << data[i].nim << endl;
                cout << "   Nilai Akhir: " << data[i].nilaiAkhir << endl;
            }
            
        } else if(pilihan == 3) {
            cout << "Program selesai" << endl;
            break;
        } else {
            cout << "Pilihan salah!" << endl;
        }
    }
    
    return 0;
}
```

> Output
> ![Screenshot soal 1](https://github.com/asshiddiqie/Laprak/blob/main/laprak1/soal1.png)

Program di atas adalah kalkulator sederhana dalam C++ yang menerima dua input bilangan float dari pengguna dan menampilkan hasil empat operasi aritmetika dasar (penjumlahan, pengurangan, perkalian, dan pembagian) dengan implementasi pengecekan kondisi untuk mencegah pembagian oleh nol.

### Soal 2

Buatlah sebuah program yang menerima masukan angka dan mengeluarkan output nilai angka tersebut dalam bentuk tulisan. Angka yang akan di-input-kan user adalah bilangan bulat positif mulai dari 0 s.d 100

```go
#include <iostream>
using namespace std;

int main() {
    int angka;
    cout << "Masukkan angka (0-100): ";
    cin >> angka;
    
    cout << angka << " : ";
    
    int p = angka / 10;  // puluhan
    int s = angka % 10;  // satuan
    
    if (angka == 0) cout << "nol";
    else if (angka == 100) cout << "seratus";
    else if (angka == 10) cout << "sepuluh";
    else if (angka == 11) cout << "sebelas";
    else if (angka == 12) cout << "dua belas";
    else if (angka == 13) cout << "tiga belas";
    else if (angka == 14) cout << "empat belas";
    else if (angka == 15) cout << "lima belas";
    else if (angka == 16) cout << "enam belas";
    else if (angka == 17) cout << "tujuh belas";
    else if (angka == 18) cout << "delapan belas";
    else if (angka == 19) cout << "sembilan belas";
    else {
        // Puluhan
        if (p == 2) cout << "dua puluh";
        else if (p == 3) cout << "tiga puluh";
        else if (p == 4) cout << "empat puluh";
        else if (p == 5) cout << "lima puluh";
        else if (p == 6) cout << "enam puluh";
        else if (p == 7) cout << "tujuh puluh";
        else if (p == 8) cout << "delapan puluh";
        else if (p == 9) cout << "sembilan puluh";
        
        // Satuan (kalau ada)
        if (s == 1) cout << " satu";
        else if (s == 2) cout << " dua";
        else if (s == 3) cout << " tiga";
        else if (s == 4) cout << " empat";
        else if (s == 5) cout << " lima";
        else if (s == 6) cout << " enam";
        else if (s == 7) cout << " tujuh";
        else if (s == 8) cout << " delapan";
        else if (s == 9) cout << " sembilan";
        
        // Kalau cuma satuan (1-9)
        if (p == 0) {
            if (s == 1) cout << "satu";
            else if (s == 2) cout << "dua";
            else if (s == 3) cout << "tiga";
            else if (s == 4) cout << "empat";
            else if (s == 5) cout << "lima";
            else if (s == 6) cout << "enam";
            else if (s == 7) cout << "tujuh";
            else if (s == 8) cout << "delapan";
            else if (s == 9) cout << "sembilan";
        }
    }
    
    cout << endl;
    return 0;
}
```

> Output
> ![Screenshot bagian x](https://github.com/asshiddiqie/Laprak/blob/main/laprak1/soal2.jpg)

Program ini mengkonversi angka 0-100 menjadi kata dalam bahasa Indonesia dengan cara memisahkan digit puluhan dan satuan menggunakan operasi pembagian dan modulus, kemudian menggunakan struktur if-else bertingkat untuk menangani tiga kategori: kasus khusus (0, 10-19, 100) yang memiliki nama unik, angka puluhan (20-99) yang menggabungkan kata puluhan dan satuan, serta angka satuan (1-9) yang langsung mencetak kata satuannya.

### Soal 3

Buatlah program dengan ketentuan :
- 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
- fungsi/prosedur yang menampilkan isi sebuah array integer 2D
- fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu

```go
#include <iostream>
using namespace std;

// Fungsi untuk menampilkan isi array 2D
void tampilkanArray(int arr[3][3], string namaArray) {
    cout << "Array " << namaArray << ":" << endl;
    for(int i = 0; i < 3; i++) {
        cout << "| ";
        for(int j = 0; j < 3; j++) {
            cout << arr[i][j] << " ";
        }
        cout << "|" << endl;
    }
    cout << endl;
}

// Fungsi untuk menukar elemen pada posisi tertentu menggunakan pointer
void tukarPosisi(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int *ptr1 = &arr1[baris][kolom];
    int *ptr2 = &arr2[baris][kolom];
    
    cout << "Sebelum tukar: Array1[" << baris << "][" << kolom << "] = " << *ptr1;
    cout << ", Array2[" << baris << "][" << kolom << "] = " << *ptr2 << endl;
    
    // Tukar nilai menggunakan pointer
    int temp = *ptr1;
    *ptr1 = *ptr2;
    *ptr2 = temp;
    
    cout << "Setelah tukar: Array1[" << baris << "][" << kolom << "] = " << *ptr1;
    cout << ", Array2[" << baris << "][" << kolom << "] = " << *ptr2 << endl;
}

void menu() {
    // Array 2D 3x3
    int array1[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
    int array2[3][3] = {{10, 20, 30}, {40, 50, 60}, {70, 80, 90}};
    
    // Pointer integer
    int *ptr1, *ptr2;
    
    int pilihan;
    
    do {
        cout << "\n=== MENU PROGRAM ARRAY 2D ===" << endl;
        cout << "1. Tampilkan Array" << endl;
        cout << "2. Tukar Posisi Tertentu" << endl;
        cout << "3. Keluar" << endl;
        cout << "Pilihan: ";
        cin >> pilihan;
        
        switch(pilihan) {
            case 1:
                tampilkanArray(array1, "Pertama");
                tampilkanArray(array2, "Kedua");
                break;
                
            case 2: {
                int baris, kolom;
                cout << "Masukkan posisi untuk ditukar:" << endl;
                cout << "Baris (0-2): ";
                cin >> baris;
                cout << "Kolom (0-2): ";
                cin >> kolom;
                
                if(baris >= 0 && baris < 3 && kolom >= 0 && kolom < 3) {
                    tukarPosisi(array1, array2, baris, kolom);
                    cout << "\nHasil setelah penukaran:" << endl;
                    tampilkanArray(array1, "Pertama");
                    tampilkanArray(array2, "Kedua");
                } else {
                    cout << "Posisi tidak valid!" << endl;
                }
                break;
            }
                
            case 3:
                cout << "Program selesai." << endl;
                break;
                
            default:
                cout << "Pilihan tidak valid!" << endl;
        }
    } while(pilihan != 3);
}

int main() {
    menu();
    return 0;
}
```

> Output
> ![Screenshot soal 3](https://github.com/asshiddiqie/Laprak/blob/main/laprak1/soal3.jpg)

Program ini membuat pola segitiga simetris dengan angka dan bintang. User memasukkan angka n, kemudian program menggambar segitiga setinggi n+1 baris.
Cara kerja: Program menggunakan loop bertingkat untuk membuat setiap baris. Setiap baris terdiri dari 4 bagian:

-Spasi untuk indentasi (membentuk segitiga)

-Angka kiri yang menurun (dari i ke 1)

-Bintang di tengah sebagai sumbu

-Angka kanan yang menaik (dari 1 ke i)

## Referensi

1. https://www.w3schools.com/cpp/cpp_for_loop.asp
2. https://www.w3schools.com/cpp/cpp_conditions.asp
3. https://www.w3schools.com/cpp/cpp_conditions_elseif.asp
4. https://www.w3schools.com/cpp/cpp_conditions_else.asp
5. https://www.w3schools.com/cpp/cpp_variables_multiple.asp
6. https://www.w3schools.com/cpp/cpp_arrays.asp

