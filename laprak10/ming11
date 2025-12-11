# <h1 align="center">Laporan Praktikum Modul 10 <br> TREE (BAGIAN PERTAMA) </h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129 </p>

## Dasar Teori

Rekursif adalah teknik pemrograman di mana fungsi memanggil dirinya sendiri untuk menyelesaikan masalah secara berulang dan harus memiliki kondisi berhenti agar proses tidak berjalan tanpa akhir. Konsep ini banyak digunakan pada struktur data tree, yaitu struktur hirarki yang memiliki root sebagai node utama serta node lain yang terhubung sebagai parent, child, dan leaf. Salah satu bentuk terpenting adalah Binary Search Tree (BST), yaitu binary tree yang setiap node-nya memiliki aturan left child bernilai lebih kecil dan right child lebih besar dari parent, sehingga proses insert, search, update, dan delete dapat dilakukan dengan efisien. Untuk membaca isi BST digunakan traversal seperti pre-order, in-order, dan post-order yang menentukan urutan kunjungan node.


## Guided

### tree
```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *kiri, *kanan;
};

Node *buatNode(int nilai)
{
    Node *baru = new Node();
    baru-> data = nilai;
    baru->kiri = baru->kanan = NULL;
    return baru;
}

//insert
Node *insert(Node *root, int nilai)
{
    if (root == NULL)
        return buatNode(nilai);

    if (nilai < root->data)
        root->kiri = insert(root->kiri, nilai); // kiri jika lebih kecil
    else if(nilai > root->data)
        root->kanan = insert(root->kanan, nilai); // kanan jika lebih besar

    return root;
}

//search
Node *search(Node *root, int nilai)
{
    if (root == NULL || root->data == nilai)
        return root;
    
    if (nilai < root->data)
        return search(root->kiri, nilai);

    return search(root->kanan, nilai);

}

//cari nilai terkecil(untuk proses hapus)
Node *nilaiTerkecil(Node *node)
{
    Node *current = node;
    while (current && current->kiri != NULL)
        current = current->kiri;
    return current;
}

//delete
Node *hapus(Node *root, int nilai)
{
    if (root == NULL)
        return root;
    if (nilai < root->data)
        root->kiri = hapus(root->kiri, nilai);
    else if(nilai > root->data)
        root->kanan = hapus(root->kanan, nilai);
    else
    {
        //jika data ketemu
        if (root->kiri == NULL)
        {
            Node *temp = root->kanan;
            delete root;
            return temp;
        }
        if (root->kanan == NULL)
        {
            Node *temp = root->kiri;
            delete root;
            return temp;
        }
        //jika punya 2 anak:ambil terkecil dari kanan
        Node *temp = nilaiTerkecil(root->kanan);
        root->data = temp->data;
        root->kanan = hapus(root->kanan, temp->data);
    }
    return root;
    
}

//update
Node *update(Node *root, int lama, int baru)
{
    if (search(root, lama) != NULL)
    {
        root = hapus(root, lama);// hapus lama
        root = insert(root, baru);// masukkan baru
        cout << "Data " << lama << " diupdate menjadi " << baru << endl;
    }
    else
    {
        cout << "Data " << lama << " tidak ditemukan! " << endl;
    }
    return root;
}

//menampilkan data
void preOrder(Node *root)
{ // akar->kiri->kanan
    if (root != NULL)
    {
        cout << root->data<< " ";
        preOrder(root->kiri);
        preOrder(root->kanan);
    }
}

void inOrder(Node *root)
{// kiri->akar->kanan
    if (root != NULL)
    {
        inOrder(root->kiri);
        cout << root->data << " ";
        inOrder(root->kanan);
    }
}

void postOrder(Node *root)
{// kiri->kanan->akar
    if (root != NULL)
    {
        postOrder(root->kiri);
        postOrder(root->kanan);
        cout << root->data << " ";
    }
}

int main()
{
    Node *root = NULL;

    cout << "=== 1. INSERT DATA ===" << endl;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);
    cout << "Data berhasil dimasukkan.\n"
        << endl;

    cout << "=== 2. TAMPILKAN TREE (TRAVERSAL) ===" << endl;
    cout << "preOrder : ";
    preOrder(root);
    cout << endl;
    cout << "InOrder : ";
    inOrder(root);
    cout << endl;
    cout << "PostOrder : ";
    postOrder(root);
    cout << "\n"
        << endl;

    cout << "=== 3. TEST SEARCH ===" << endl;
    int cari1 = 7, cari2 = 99;
    cout << "Cari " << cari1 << ": " << (search(root, cari1) ? "Ketemu" : "Tidak Ada") << endl;
    cout << "Cari " << cari2 << ": " << (search(root, cari2) ? "Ketemu" : "Tidak Ada") << endl;
    cout << endl;

    cout << "=== 4. TEST UPDATE ===" << endl;
    //mengubah angka 5 menjadi 8
    root = update(root, 5,8);
    cout << "Hasil inOrder setelah update: ";
    cout << endl;
    cout << endl;

    cout << "preOrder : ";
    preOrder(root);
    cout << endl;
    cout << "inOrder : ";
    inOrder(root);
    cout << endl;
    cout << "postOrder : ";
    postOrder(root);
    cout << "\n"
        << endl;

    cout << "=== 5. TEST DELETE ===" << endl;
    //menghapus angka 20 (Node yang punya anak)
    cout << "Menghapus angka 20..." << endl;
    root = hapus(root, 20);

    cout << "preOrder : ";
    preOrder(root);
    cout << endl;
    cout << "inOrder : ";
    inOrder(root);
    cout << endl;
    cout << "postOrder : ";
    postOrder(root);
    cout << "\n"
        << endl;

    return 0;

}
```

## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “queue.h”:
```go
Type infotype: integer
Type address : pointer to Node
Type Node: <
info : infotype
left, right : address
>
function alokasi( x : infotype ) → address
procedure insertNode( input/output root : address,
input x : infotype )
function findNode( x : infotype, root : address )→address
procedure printInorder( input root : address )
```

Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 1 (head diam, tail bergerak).
```go
#include <iostream>
#include "bstree.h"
using namespace std;
int main() {
cout << "Hello World" << endl;
address root = Nil;
insertNode(root,1);
insertNode(root,2);
insertNode(root,6);
insertNode(root,4);
insertNode(root,5);
insertNode(root,3);
insertNode(root,6);
insertNode(root,7);
InOrder(root);
return 0;
}
```
### file bstree.h
```cpp
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;

typedef struct Node *address;
struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(address root, infotype x);
void printInorder(address root);

#endif
```
### file bstree.cpp
```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address newNode = new Node;
    newNode->info = x;
    newNode->left = Nil;
    newNode->right = Nil;
    return newNode;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
    // Jika x sudah ada, abaikan (tidak ada duplikat)
}

address findNode(address root, infotype x) {
    if (root == Nil || root->info == x) {
        return root;
    } else if (x < root->info) {
        return findNode(root->left, x);
    } else {
        return findNode(root->right, x);
    }
}

void printInorder(address root) {
    if (root != Nil) {
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}
```
### file main.cpp
```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    address root = Nil;
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6); // duplikat, akan diabaikan
    insertNode(root, 7);
    
    cout << "Inorder traversal: ";
    printInorder(root);
    cout << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul10no1.jpg)

Penjelasan :
kode diatas bertujuan mengimplementasikan struktur data Binary Search Tree (BST) dengan operasi dasar menyisipkan node dan mencetak isi tree menggunakan traversal in-order. BST dibangun dengan aturan bahwa node kiri lebih kecil dan node kanan lebih besar dari parent, menghasilkan urutan terurut menaik saat traversal in-order. Contoh data {1, 2, 6, 4, 5, 3, 6, 7} membentuk BST dengan struktur tertentu dan output "1 - 2 - 3 - 4 - 5 - 6 - 7 -".
### Soal 2
Buatlah fungsi untuk menghitung jumlah node dengan fungsi berikut.
- fungsi hitungJumlahNode( root:address ) : integer
   /* fungsi mengembalikan integer banyak node yang ada di dalam BST*/
- fungsi hitungTotalInfo( root:address, start:integer ) : integer
  /* fungsi mengembalikan jumlah (total) info dari node-node yang ada di dalam BST*/
- fungsi hitungKedalaman( root:address, start:integer ) : integer
  /* fungsi rekursif mengembalikan integer kedalaman maksimal dari binary tree */

```cpp
int main() {
cout << "Hello World" << endl;
address root = Nil;
insertNode(root,1);
insertNode(root,2);
insertNode(root,6);
insertNode(root,4);
insertNode(root,5);
insertNode(root,3);
insertNode(root,6);
insertNode(root,7);
InOrder(root);
cout<<"\n";
cout<<"kedalaman : "<<hitungKedalaman(root,0)<<endl;
cout<<"jumlah Node : "<<hitungNode(root)<<endl;
cout<<"total : "<<hitungTotal(root)<<endl;
return 0;
}
```

### file bstree.h
```cpp
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;

typedef struct Node *address;
struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(address root, infotype x);
void printInorder(address root);

// Fungsi tambahan untuk latihan 2
int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root);

#endif
```
### file bstree.cpp
```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address newNode = new Node;
    newNode->info = x;
    newNode->left = Nil;
    newNode->right = Nil;
    return newNode;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
}

address findNode(address root, infotype x) {
    if (root == Nil || root->info == x) {
        return root;
    } else if (x < root->info) {
        return findNode(root->left, x);
    } else {
        return findNode(root->right, x);
    }
}

void printInorder(address root) {
    if (root != Nil) {
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}

// Implementasi fungsi latihan 2
int hitungJumlahNode(address root) {
    if (root == Nil) return 0;
    return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
}

int hitungTotalInfo(address root) {
    if (root == Nil) return 0;
    return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
}

int hitungKedalaman(address root) {
    if (root == Nil) return 0;
    int leftDepth = hitungKedalaman(root->left);
    int rightDepth = hitungKedalaman(root->right);
    return (leftDepth > rightDepth ? leftDepth : rightDepth) + 1;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    cout << "Hello World" << endl;
    address root = Nil;
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 6); // duplikat
    insertNode(root, 7);
    
    cout << "Inorder traversal: ";
    printInorder(root);
    cout << endl;
    
    cout << "Kedalaman tree: " << hitungKedalaman(root) << endl;
    cout << "Jumlah node: " << hitungJumlahNode(root) << endl;
    cout << "Total nilai node: " << hitungTotalInfo(root) << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul10no2.jpg)

Penjelasan :
kode diatas menambahkan fungsi utilitas untuk menganalisis properti BST, yaitu menghitung jumlah node, total nilai semua node, dan kedalaman tree. Ketiga fungsi ini diimplementasikan secara rekursif, di mana perhitungan kedalaman menggunakan prinsip mencari jalur terpanjang dari root ke leaf. Untuk BST dari latihan 1, diperoleh hasil 7 node, total nilai 28, dan kedalaman 5.

### Soal 3
Print tree secara pre-order dan post-order.

### file bstree.h
```cpp
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;

typedef struct Node *address;
struct Node {
    infotype info;
    address left;
    address right;
};

// Fungsi dasar BST
address alokasi(infotype x);
void insertNode(address &root, infotype x);
address findNode(address root, infotype x);

// Traversal functions
void printInorder(address root);
void printPreorder(address root);
void printPostorder(address root);

// Fungsi hitung (dari latihan 2)
int hitungJumlahNode(address root);
int hitungTotalInfo(address root);
int hitungKedalaman(address root);

#endif
```
### file bstree.cpp
```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address newNode = new Node;
    newNode->info = x;
    newNode->left = Nil;
    newNode->right = Nil;
    return newNode;
}

void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
}

address findNode(address root, infotype x) {
    if (root == Nil || root->info == x) {
        return root;
    } else if (x < root->info) {
        return findNode(root->left, x);
    } else {
        return findNode(root->right, x);
    }
}

// IN-ORDER: Left → Root → Right
void printInorder(address root) {
    if (root != Nil) {
        printInorder(root->left);
        cout << root->info << " ";
        printInorder(root->right);
    }
}

// PRE-ORDER: Root → Left → Right
void printPreorder(address root) {
    if (root != Nil) {
        cout << root->info << " ";
        printPreorder(root->left);
        printPreorder(root->right);
    }
}

// POST-ORDER: Left → Right → Root
void printPostorder(address root) {
    if (root != Nil) {
        printPostorder(root->left);
        printPostorder(root->right);
        cout << root->info << " ";
    }
}

int hitungJumlahNode(address root) {
    if (root == Nil) return 0;
    return 1 + hitungJumlahNode(root->left) + hitungJumlahNode(root->right);
}

int hitungTotalInfo(address root) {
    if (root == Nil) return 0;
    return root->info + hitungTotalInfo(root->left) + hitungTotalInfo(root->right);
}

int hitungKedalaman(address root) {
    if (root == Nil) return 0;
    int leftDepth = hitungKedalaman(root->left);
    int rightDepth = hitungKedalaman(root->right);
    return (leftDepth > rightDepth ? leftDepth : rightDepth) + 1;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    address root = Nil;
    
    // Data dari latihan sebelumnya (modul)
    insertNode(root, 1);
    insertNode(root, 2);
    insertNode(root, 6);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 3);
    insertNode(root, 7);
    
    cout << "=== Hasil Traversal BST ===" << endl;
    cout << "BST dibangun dari data: 1, 2, 6, 4, 5, 3, 7" << endl;
    cout << endl;
    
    cout << "In-order traversal   : ";
    printInorder(root);
    cout << endl;
    
    cout << "Pre-order traversal  : ";
    printPreorder(root);
    cout << endl;
    
    cout << "Post-order traversal : ";
    printPostorder(root);
    cout << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul10no3.jpg)


Penjelasan :
berfokus pada implementasi dan perbandingan tiga metode traversal tree: pre-order (Root→Kiri→Kanan), in-order (Kiri→Root→Kanan), dan post-order (Kiri→Kanan→Root). Masing-masing traversal menghasilkan urutan node yang berbeda, di mana pre-order berguna untuk menyalin struktur, in-order pada BST menghasilkan urutan terurut, dan post-order cocok untuk penghapusan tree. BST dari latihan sebelumnya menghasilkan output berbeda untuk setiap traversal.
## Referensi

1. https://www.w3schools.com/cpp/cpp_for_loop_nested.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_arrays_loop.asp
4. https://www.w3schools.com/cpp/cpp_references.asp
5. https://www.w3schools.com/cpp/cpp_pointers.asp
6. https://www.w3schools.com/cpp/cpp_function_param.asp
7. https://www.w3schools.com/cpp/cpp_function_array.asp
8. https://www.w3schools.com/cpp/cpp_stacks.asp
