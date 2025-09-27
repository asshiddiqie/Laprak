# <h1 align="center">Laporan Praktikum Modul 1 <br> Pengenalan C++</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

yang panjang dikit

## Unguided

### soal 1

blablabla

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

soal nomor 2

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2A")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2A.png)

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
> ![Screenshot soal 3](https://github.com/asshiddiqie/Laprak/blob/main/laprak1/soal2.jpg)

penjelasan bedanya sesuai soal

## Referensi

1. https://www.w3schools.com/cpp/cpp_switch.asp

