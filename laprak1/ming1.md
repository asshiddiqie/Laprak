# <h1 align="center">Laporan Praktikum Modul 1 <br> Pengenalan C++</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

yang panjang dikit

## Unguided

### Soal 1

Buatlah program yang menerima input-an dua buah bilangan bertipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

```go
#include <iostream>
using namespace std;

int main() {
    float bilangan1, bilangan2;
    

    cout << "Masukkan bilangan pertama: ";
    cin >> bilangan1;
    cout << "Masukkan bilangan kedua: ";
    cin >> bilangan2;
    
    cout << "\nHasil Operasi:" << endl;
    cout << "Penjumlahan: " << bilangan1 << " + " << bilangan2 << " = " << bilangan1 + bilangan2 << endl;
    cout << "Pengurangan: " << bilangan1 << " - " << bilangan2 << " = " << bilangan1 - bilangan2 << endl;
    cout << "Perkalian: " << bilangan1 << " * " << bilangan2 << " = " << bilangan1 * bilangan2 << endl;
    
    if (bilangan2 != 0) {
        cout << "Pembagian: " << bilangan1 << " / " << bilangan2 << " = " << bilangan1 / bilangan2 << endl;
    } else {
        cout << "Pembagian: Tidak dapat membagi dengan nol" << endl;
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

penjelasan kode

### Soal 3

Buatlah program yang dapat memberikan input dan output sbb.

```go
#include <iostream>
using namespace std;

int main() {
    int n;
    
    cout << "input: ";
    cin >> n;
    
    cout << "output:" << endl;
    
    for (int i = n; i >= 0; i--) {
        for (int s = 0; s < (n - i) * 2; s++) {
            cout << " ";
        }
        
        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }
        
        cout << "*";
        
        if (i > 0) {
            cout << " ";
            for (int j = 1; j <= i; j++) {
                cout << j << " ";
            }
        }
        
        cout << endl;
    }
    
    return 0;
}
```

> Output
> ![Screenshot soal 3](https://github.com/asshiddiqie/Laprak/blob/main/laprak1/soal3.jpg)

Program ini membuat pola segitiga simetris dengan angka dan bintang. User memasukkan angka n, kemudian program menggambar segitiga setinggi n+1 baris.
Cara kerja: Program menggunakan loop bertingkat untuk membuat setiap baris. Setiap baris terdiri dari 4 bagian:

Spasi untuk indentasi (membentuk segitiga)
Angka kiri yang menurun (dari i ke 1)
Bintang di tengah sebagai sumbu
Angka kanan yang menaik (dari 1 ke i)

## Referensi

1. https://www.w3schools.com/cpp/cpp_for_loop.asp
2. https://www.w3schools.com/cpp/cpp_conditions.asp
3. https://www.w3schools.com/cpp/cpp_conditions_elseif.asp
4. https://www.w3schools.com/cpp/cpp_conditions_else.asp
5. https://www.w3schools.com/cpp/cpp_variables_multiple.asp

