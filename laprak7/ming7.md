# <h1 align="center">Laporan Praktikum Modul 7 <br> STACK </h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129 </p>

## Dasar Teori

Stack adalah struktur data linear dengan prinsip **LIFO (Last In First Out)**, di mana elemen terakhir yang dimasukkan akan dikeluarkan pertama. Stack memiliki penunjuk utama **Top** yang menunjukkan elemen paling atas. Implementasinya dapat menggunakan **pointer** atau **array**, dengan operasi dasar **Push** untuk menambah data dan **Pop** untuk menghapus data. Selain itu, terdapat operasi seperti `createStack()`, `isEmpty()`, dan `viewStack()` untuk mengelola isi stack. Struktur ini banyak digunakan dalam pemrograman karena efisien untuk pengelolaan data berurutan sementara.


## Guided

### double linked list
```go
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

bool isEmpty(Node *top)
{
    return top == nullptr;
}
void push (Node *&top, int data)
{
    Node *newNode = new Node();
    newNode-> data = data;
    newNode-> next = top;
    top = newNode;
}

int pop(Node *&top)
{
    if (isEmpty(top))
    {
        cout << "Stack Kosong, tidak bisa pop!" << endl;
        return 0;
    }
    int poppedData = top-> data;
    Node *temp = top;
    top = top-> next;

    delete temp;
    return poppedData;
}

void show(Node *top)
{
    if (isEmpty(top))
{
    cout << "Stack Kosong." << endl;
    return;
}
cout << "TOP ->";
Node *temp = top;

while (temp != nullptr)
{
    cout << temp-> data << " ->";
    temp = temp-> next;
}
cout << "NULL" << endl;
}

int main()
{
    Node *stack = nullptr;

    push (stack, 10);
    push (stack, 20);
    push (stack, 30);

    cout << "Menampilkan isi stack: " << endl;
    show(stack);

    cout << "Pop: " << pop(stack) << endl;

    cout << "Menampilkan sisa stack: " << endl;
    show(stack);

    return 0;
}
```

## Unguided

### Soal 1

Buatlah ADT Stack menggunakan ARRAY sebagai berikut di dalam file “stack.h”:
```go
Type infotype : integer
Type Stack <
info : array [20] of integer
top : integer
>
procedure CreateStack( input/output S : Stack )
procedure push(input/output S : Stack,
input x : infotype)
function pop(input/output t S : Stack )
→ infotype
procedure printInfo( input S : Stack )
procedure balikStack(input/output S :
Stack )
```

Buatlah implementasi ADT Stack menggunakan Array pada file “stack.cpp” dan “main.cpp” 
```go
int main()
{
cout << "Hello world!" <<
endl;
Stack S;
createStack(S);
Push(S,3);
Push(S,4);
Push(S,8);
pop(S)
Push(S,2);
Push(S,3);
pop(S);
Push(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}
```
### file stack.h
```cpp
#ifndef STACK_H
#define STACK_H

const int MAX_SIZE = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX_SIZE];
    int top;
};

void CreateStack(Stack &S);
void Push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
### file stack.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void CreateStack(Stack &S) {
    S.top = -1;
}

void Push(Stack &S, infotype x) {
    if (S.top < MAX_SIZE - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (S.top == -1) {
        cout << "Stack kosong" << endl;
        return;
    }
    
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    CreateStack(temp);
    
    // Pindahkan semua elemen ke stack temporary
    while (S.top >= 0) {
        Push(temp, pop(S));
    }
    
    // Copy kembali ke stack asli (sudah terbalik)
    S = temp;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    
    Stack S;
    CreateStack(S);
    
    Push(S, 3);
    Push(S, 4);
    Push(S, 8);
    pop(S);
    Push(S, 2);
    Push(S, 3);
    pop(S);
    Push(S, 9);
    
    printInfo(S);
    
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    
    return 0;
}
```
### Soal 2
Tambahkan prosedur pushAscending( in/out S : Stack, in x : integer)
```cpp
int main()
{
cout << "Hello world!" << endl;
Stack S;
createStack(S);
pushAscending(S,3);
pushAscending(S,4);
pushAscending(S,8);
pushAscending(S,2);
pushAscending(S,3);
pushAscending(S,9);
printInfo(S);
cout<<"balik stack"<<endl;
balikStack(S);
printInfo(S);
return 0;
}
```

### file stack.h
```cpp
#ifndef STACK_H
#define STACK_H

const int MAX_SIZE = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX_SIZE];
    int top;
};

void CreateStack(Stack &S);
void push(Stack &S, infotype x);
void pushAscending(Stack &S, infotype x);  // Tambahan
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
### file stack.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void CreateStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX_SIZE - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

void pushAscending(Stack &S, infotype x) {
    if (S.top == -1) {
        // Stack kosong, langsung push
        push(S, x);
        return;
    }
    
    if (S.top >= MAX_SIZE - 1) {
        cout << "Stack penuh!" << endl;
        return;
    }
    
    Stack temp;
    CreateStack(temp);
    
    // Pindahkan elemen dari stack asli ke temp sampai menemukan posisi yang tepat
    while (S.top >= 0 && S.info[S.top] < x) {
        push(temp, pop(S));
    }
    
    // Push elemen baru
    push(S, x);
    
    // Kembalikan elemen dari temp ke stack asli
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (S.top == -1) {
        cout << "Stack kosong" << endl;
        return;
    }
    
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    CreateStack(temp);
    
    // Pindahkan semua elemen ke stack temporary
    int originalTop = S.top;
    for (int i = 0; i <= originalTop; i++) {
        push(temp, S.info[i]);
    }
    
    // Clear stack asli
    CreateStack(S);
    
    // Pindahkan kembali dari temp ke S (akan terbalik)
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}
```
### file main.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    
    Stack S;
    CreateStack(S);
    
    pushAscending(S, 3);
    pushAscending(S, 4);
    pushAscending(S, 8);
    pushAscending(S, 2);
    pushAscending(S, 3);
    pushAscending(S, 9);
    
    printInfo(S);
    
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    
    return 0;
}
```

### Soal 3
Tambahkan prosedur getInputStream( in/out S : Stack ). Prosedur akan terus membaca dan
menerima input user dan memasukkan setiap input ke dalam stack hingga user menekan
tombol enter. Contoh: gunakan cin.get() untuk mendapatkan inputan user.
### file stack.h
```cpp
#ifndef STACK_H
#define STACK_H

const int MAX_SIZE = 20;

typedef int infotype;

struct Stack {
    infotype info[MAX_SIZE];
    int top;
};

void CreateStack(Stack &S);
void push(Stack &S, infotype x);
void pushAscending(Stack &S, infotype x);
void getInputStream(Stack &S);
void processNumberInput(Stack &S);  // Tambahan untuk nomor 3
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif
```
### file stack.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

void CreateStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype x) {
    if (S.top < MAX_SIZE - 1) {
        S.top++;
        S.info[S.top] = x;
    } else {
        cout << "Stack penuh!" << endl;
    }
}

void pushAscending(Stack &S, infotype x) {
    if (S.top == -1) {
        push(S, x);
        return;
    }
    
    if (S.top >= MAX_SIZE - 1) {
        cout << "Stack penuh!" << endl;
        return;
    }
    
    Stack temp;
    CreateStack(temp);
    
    while (S.top >= 0 && S.info[S.top] < x) {
        push(temp, pop(S));
    }
    
    push(S, x);
    
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}

void getInputStream(Stack &S) {
    cout << "Masukkan karakter (tekan Enter untuk berhenti): ";
    
    char ch;
    while (true) {
        ch = cin.get();
        
        if (ch == '\n') {
            break;
        }
        
        if (S.top < MAX_SIZE - 1) {
            push(S, (int)ch);
        } else {
            cout << "Stack penuh! Input dihentikan." << endl;
            break;
        }
    }
}

void processNumberInput(Stack &S) {
    cout << "Masukkan angka: ";
    string input;
    cin >> input;
    
    // Push setiap digit angka ke stack
    for (int i = 0; i < input.length(); i++) {
        if (isdigit(input[i])) {
            int digit = input[i] - '0';  // Konversi char ke int
            push(S, digit);
        }
    }
}

infotype pop(Stack &S) {
    if (S.top >= 0) {
        infotype x = S.info[S.top];
        S.top--;
        return x;
    } else {
        cout << "Stack kosong!" << endl;
        return -1;
    }
}

void printInfo(Stack S) {
    if (S.top == -1) {
        cout << "Stack kosong" << endl;
        return;
    }
    
    cout << "[TOP] ";
    for (int i = S.top; i >= 0; i--) {
        cout << S.info[i] << " ";
    }
    cout << endl;
}

void balikStack(Stack &S) {
    Stack temp;
    CreateStack(temp);
    
    // Pindahkan semua elemen ke stack temporary
    int originalTop = S.top;
    for (int i = 0; i <= originalTop; i++) {
        push(temp, S.info[i]);
    }
    
    // Clear stack asli
    CreateStack(S);
    
    // Pindahkan kembali dari temp ke S (akan terbalik)
    while (temp.top >= 0) {
        push(S, pop(temp));
    }
}
```
### file main.cpp
```cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    
    Stack S;
    CreateStack(S);
    
    processNumberInput(S);
    printInfo(S);
    
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/modul6no1.jpg)


Penjelasan 
**File: Doublylist.h (File Header - Antarmuka)**

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
