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
