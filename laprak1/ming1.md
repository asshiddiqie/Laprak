# <h1 align="center">Laporan Praktikum Modul 1 <br> Nama Modul</h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129</p>

## Dasar Teori

yang panjang dikit

## Unguided

### soal 1

blablablabalba

## Unguided

### Soal 1

1. Buatlah program yang menerima input-an dua buah bilangan bertipe float, kemudian memberikan output-an hasil penjumlahan, pengurangan, perkalian, dan pembagian dari dua bilangan tersebut.

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
> ![Screenshot soal 1](https://github.com/asshiddiqie/modul1/blob/main/laprak1/soal1.png)
> %% Untuk mencantumkan screenshot, tidak boleh ada spasi di urlnya `()`, penamaan file bebas asal gak sara dan mudah dipahami aja,, dan jangan lupa hapus komen ini yah%%

Penjelasan ttg kode kalian disini

### Soal 2

soal nomor 2A

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2A")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2A.png)

penjelasan kode

Kalau adalanjutan di lanjut disini aja

soal nomor 2B

```go
package main

func main() {
	fmt.Println("kode untuk soal nomor 2B")
}
```

> Output
> ![Screenshot bagian x](output/screenshot_soal2B.png)

penjelasan bedanya sesuai soal

## Referensi

1. https://www.w3schools.com/cpp/cpp_switch.asp

