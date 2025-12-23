
# <h1 align="center">Laporan Praktikum Modul 13 <br> GRAPH </h1>
<p align="center">ASSHIDDIQIE SYABANA PUTRA - 103112400129 </p>

## Dasar Teori

Graph adalah struktur data non-linear yang merepresentasikan himpunan objek (disebut vertex atau node) yang terhubung oleh sisi (edge) yang dapat memiliki arah (pada directed graph) maupun tidak (pada undirected graph). Dalam implementasinya, graph dapat direpresentasikan menggunakan adjacency matrix atau adjacency list (multilist), dengan adjacency list sering dipilih karena efisiensi memorinya untuk graph yang sparse. Algoritma dasar pada graph meliputi penelusuran seperti Breadth-First Search (BFS) yang menjelajahi graph per level dan Depth-First Search (DFS) yang menjelajahi secara mendalam, serta topological sort untuk mengurutkan vertex pada directed acyclic graph berdasarkan dependensi antar node.


## Guided

### graph.h
```go
#ifndef GRAF_H_INCLUDED
#define GRAF_H_INCLUDED

#include <iostream>
using namespace std;

typedef char infoGraph;

struct ElmNode;
struct ElmEdge;

typedef ElmNode *adrNode;
typedef ElmEdge *adrEdge;

struct ElmNode
{
    infoGraph info;
    int visited;
    adrEdge firstEdge;
    adrNode next;
};

struct ElmEdge
{
    adrNode node;
    adrEdge next;
};

struct Graph
{
    adrNode first;
};

// PRIMITIF GRAPH
void CreateGraph(Graph &G);
adrNode AllocateNode(infoGraph X);
adrEdge AllocateEdge(adrNode N);

void InsertNode(Graph &G, infoGraph X);
adrNode FindNode(Graph G, infoGraph X);

void ConnectNode(Graph &G, infoGraph A, infoGraph B);

void PrintInfoGraph(Graph G);

// Traversal
void ResetVisited(Graph &G);
void PrintDFS(Graph &G, adrNode N);
void PrintBFS(Graph &G, adrNode N);

#endif
```

### graph.cpp
```go

#include "graf.h"
#include <queue>
#include <stack>

void CreateGraph(Graph &G)
{
    G.first = NULL;
}

adrNode AllocateNode(infoGraph X)
{
    adrNode P = new ElmNode;
    P->info = X;
    P->visited = 0;
    P->firstEdge = NULL;
    P->next = NULL;
    return P;
}

adrEdge AllocateEdge(adrNode N)
{
    adrEdge P = new ElmEdge;
    P->node = N;
    P->next = NULL;
    return P;
}

void InsertNode(Graph &G, infoGraph X)
{
    adrNode P = AllocateNode(X);
    P->next = G.first;
    G.first = P;
}

adrNode FindNode(Graph G, infoGraph X)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        if (P->info == X)
            return P;
        P = P->next;
    }
    return NULL;
}

void ConnectNode(Graph &G, infoGraph A, infoGraph B)
{
    adrNode N1 = FindNode(G, A);
    adrNode N2 = FindNode(G, B);

    if (N1 == NULL || N2 == NULL)
    {
        cout << "Node tidak ditemukan!\n";
        return;
    }

    // Buat edge dari N1 ke N2
    adrEdge E1 = AllocateEdge(N2);
    E1->next = N1->firstEdge;
    N1->firstEdge = E1;

    // Karena undirected → buat edge balik
    adrEdge E2 = AllocateEdge(N1);
    E2->next = N2->firstEdge;
    N2->firstEdge = E2;
}

void PrintInfoGraph(Graph G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        cout << P->info << " -> ";
        adrEdge E = P->firstEdge;
        while (E != NULL)
        {
            cout << E->node->info << " ";
            E = E->next;
        }
        cout << endl;
        P = P->next;
    }
}

void ResetVisited(Graph &G)
{
    adrNode P = G.first;
    while (P != NULL)
    {
        P->visited = 0;
        P = P->next;
    }
}

void PrintDFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    N->visited = 1;
    cout << N->info << " ";

    adrEdge E = N->firstEdge;
    while (E != NULL)
    {
        if (E->node->visited == 0)
        {
            PrintDFS(G, E->node);
        }
        E = E->next;
    }
}

void PrintBFS(Graph &G, adrNode N)
{
    if (N == NULL)
        return;

    queue<adrNode> Q;
    Q.push(N);

    while (!Q.empty())
    {
        adrNode curr = Q.front();
        Q.pop();

        if (curr->visited == 0)
        {
            curr->visited = 1;
            cout << curr->info << " ";

            adrEdge E = curr->firstEdge;
            while (E != NULL)
            {
                if (E->node->visited == 0)
                {
                    Q.push(E->node);
                }
                E = E->next;
            }
        }
    }
}

```

### main.cpp
```go
#include "graf.h"
#include "graf.cpp"
#include <iostream>
using namespace std;

int main()
{
    Graph G;
    CreateGraph(G);

    // Tambah node
    InsertNode(G, 'A');
    InsertNode(G, 'B');
    InsertNode(G, 'C');
    InsertNode(G, 'D');
    InsertNode(G, 'E');

    // Hubungkan node (graph tidak berarah)
    ConnectNode(G, 'A', 'B');
    ConnectNode(G, 'A', 'C');
    ConnectNode(G, 'B', 'D');
    ConnectNode(G, 'C', 'E');

    cout << "=== Struktur Graph ===\n";
    PrintInfoGraph(G);

    cout << "\n=== DFS dari Node A ===\n";
    ResetVisited(G);
    PrintDFS(G, FindNode(G, 'A'));

    cout << "\n\n=== BFS dari Node A ===\n";
    ResetVisited(G);
    PrintBFS(G, FindNode(G, 'A'));

    cout << endl;
    return 0;
}
```

## Unguided

### Soal 1

Buatlah ADT Graph tidak berarah file “graph.h”:
```
Type infoGraph: char 
Type adrNode : pointer to ElmNode 
Type adrEdge : pointer to ElmNode 
Type ElmNode  < 
info : infoGraph 
visited : integer 
firstEdge : adrEdge 
Next : adrNode 
> 
Type ElmEdge  < 
Node : adrNode 
Next : adrEdge 
> 
Type Graph  < 
first : adrNode 
> 
procedure CreateGraph (input/output G : Graph) 
procedure InsertNode (input/output G : Graph,  
input X : infotype) 
procedure ConnectNode (input/output N1, N2 : adrNode) 
procedure PrintInfoGraph (input G : Graph)
```
Buatlah implementasi ADT Graph pada file “graph.cpp” dan cobalah hasil implementasi ADT 
pada file “main.cpp”

### file multilist.h
```cpp
#ifndef MULTILIST_H_INCLUDED
#define MULTILIST_H_INCLUDED

#define Nil NULL

typedef int infotypeanak;
typedef int infotypeinduk;
typedef struct elemen_list_induk *address;
typedef struct elemen_list_anak *address_anak;

struct elemen_list_anak{
    infotypeanak info;
    address_anak next;
    address_anak prev;
};

struct listanak {
    address_anak first;
    address_anak last;
};

struct elemen_list_induk{
    infotypeinduk info;
    listanak lanak;
    address next;
    address prev;
};

struct listinduk {
    address first;
    address last;
};

typedef int boolean;
#define true 1
#define false 0

/********* pengecekan apakah list kosong ***********/
boolean ListEmpty(listinduk L);
boolean ListEmptyAnak(listanak L);

/********* pembuatan list kosong *********/
void CreateList(listinduk &L);
void CreateListAnak(listanak &L);

/********* manajemen memori *********/
address alokasi(infotypeinduk P);
address_anak alokasiAnak(infotypeanak P);
void dealokasi(address P);
void dealokasiAnak(address_anak P);

/********* pencarian sebuah elemen list *********/
address findElm(listinduk L, infotypeinduk X);
address_anak findElm(listanak Lanak, infotypeanak X);
boolean fFindElm(listinduk L, address P);
boolean fFindElmanak(listanak Lanak, address_anak P);
address findBefore(listinduk L, address P);
address_anak findBeforeAnak(listanak Lanak, infotypeinduk X, address_anak P);

/********* penambahan elemen **********/
void insertFirst(listinduk &L, address P);
void insertAfter(listinduk &L, address P, address Prec);
void insertLast(listinduk &L, address P);
void insertFirstAnak(listanak &L, address_anak P);
void insertAfterAnak(listanak &L, address_anak P, address_anak Prec);
void insertLastAnak(listanak &L, address_anak P);

/********* penghapusan sebuah elemen *********/
void delFirst(listinduk &L, address &P);
void delLast(listinduk &L, address &P);
void delAfter(listinduk &L, address &P, address Prec);
void delP(listinduk &L, infotypeinduk X);
void delFirstAnak(listanak &L, address_anak &P);
void delLastAnak(listanak &L, address_anak &P);
void delAfterAnak(listanak &L, address_anak &P, address_anak Prec);
void delPAnak(listanak &L, infotypeanak X);

/********** proses semua elemen list *********/
void printInfo(listinduk L);
int nbList(listinduk L);
void printInfoAnak(listanak Lanak);
int nbListAnak(listanak Lanak);

/********** proses terhadap list **********/
void delAll(listinduk &L);

#endif
```
### file multilist.cpp
```cpp
#include <iostream>
#include "multilist.h"
using namespace std;

// ========== PENGE CEKAN APAKAH LIST KOSONG ==========
boolean ListEmpty(listinduk L) {
    return (L.first == Nil);
}

boolean ListEmptyAnak(listanak L) {
    return (L.first == Nil);
}

// ========== PEMBUATAN LIST KOSONG ==========
void CreateList(listinduk &L) {
    L.first = Nil;
    L.last = Nil;
}

void CreateListAnak(listanak &L) {
    L.first = Nil;
    L.last = Nil;
}

// ========== MANAJEMEN MEMORI ==========
address alokasi(infotypeinduk P) {
    address newNode = new elemen_list_induk;
    if (newNode != Nil) {
        newNode->info = P;
        newNode->next = Nil;
        newNode->prev = Nil;
        CreateListAnak(newNode->lanak);
    }
    return newNode;
}

address_anak alokasiAnak(infotypeanak P) {
    address_anak newNode = new elemen_list_anak;
    if (newNode != Nil) {
        newNode->info = P;
        newNode->next = Nil;
        newNode->prev = Nil;
    }
    return newNode;
}

void dealokasi(address P) {
    if (P != Nil) {
        delete P;
    }
}

void dealokasiAnak(address_anak P) {
    if (P != Nil) {
        delete P;
    }
}

// ========== PENCARIAN SEBUAH ELEMEN LIST ==========
address findElm(listinduk L, infotypeinduk X) {
    address current = L.first;
    while (current != Nil) {
        if (current->info == X) {
            return current;
        }
        current = current->next;
    }
    return Nil;
}

address_anak findElm(listanak Lanak, infotypeanak X) {
    address_anak current = Lanak.first;
    while (current != Nil) {
        if (current->info == X) {
            return current;
        }
        current = current->next;
    }
    return Nil;
}

boolean fFindElm(listinduk L, address P) {
    address current = L.first;
    while (current != Nil) {
        if (current == P) {
            return true;
        }
        current = current->next;
    }
    return false;
}

boolean fFindElmanak(listanak Lanak, address_anak P) {
    address_anak current = Lanak.first;
    while (current != Nil) {
        if (current == P) {
            return true;
        }
        current = current->next;
    }
    return false;
}

address findBefore(listinduk L, address P) {
    if (P == L.first) {
        return Nil;
    }
    
    address current = L.first;
    while (current != Nil && current->next != P) {
        current = current->next;
    }
    return current;
}

address_anak findBeforeAnak(listanak Lanak, infotypeinduk X, address_anak P) {
    if (P == Lanak.first) {
        return Nil;
    }
    
    address_anak current = Lanak.first;
    while (current != Nil && current->next != P) {
        current = current->next;
    }
    return current;
}

// ========== PENAMBAHAN ELEMEN INDUK ==========
void insertFirst(listinduk &L, address P) {
    if (P != Nil) {
        if (ListEmpty(L)) {
            L.first = P;
            L.last = P;
        } else {
            P->next = L.first;
            L.first->prev = P;
            L.first = P;
        }
    }
}

void insertAfter(listinduk &L, address P, address Prec) {
    if (P != Nil && Prec != Nil) {
        if (Prec == L.last) {
            insertLast(L, P);
        } else {
            P->next = Prec->next;
            P->prev = Prec;
            Prec->next->prev = P;
            Prec->next = P;
        }
    }
}

void insertLast(listinduk &L, address P) {
    if (P != Nil) {
        if (ListEmpty(L)) {
            L.first = P;
            L.last = P;
        } else {
            P->prev = L.last;
            L.last->next = P;
            L.last = P;
        }
    }
}

// ========== PENAMBAHAN ELEMEN ANAK ==========
void insertFirstAnak(listanak &L, address_anak P) {
    if (P != Nil) {
        if (ListEmptyAnak(L)) {
            L.first = P;
            L.last = P;
        } else {
            P->next = L.first;
            L.first->prev = P;
            L.first = P;
        }
    }
}

void insertAfterAnak(listanak &L, address_anak P, address_anak Prec) {
    if (P != Nil && Prec != Nil) {
        if (Prec == L.last) {
            insertLastAnak(L, P);
        } else {
            P->next = Prec->next;
            P->prev = Prec;
            Prec->next->prev = P;
            Prec->next = P;
        }
    }
}

void insertLastAnak(listanak &L, address_anak P) {
    if (P != Nil) {
        if (ListEmptyAnak(L)) {
            L.first = P;
            L.last = P;
        } else {
            P->prev = L.last;
            L.last->next = P;
            L.last = P;
        }
    }
}

// ========== PENGHAPUSAN ELEMEN INDUK ==========
void delFirst(listinduk &L, address &P) {
    if (!ListEmpty(L)) {
        P = L.first;
        if (L.first == L.last) {
            L.first = Nil;
            L.last = Nil;
        } else {
            L.first = L.first->next;
            L.first->prev = Nil;
        }
        P->next = Nil;
        P->prev = Nil;
    }
}

void delLast(listinduk &L, address &P) {
    if (!ListEmpty(L)) {
        P = L.last;
        if (L.first == L.last) {
            L.first = Nil;
            L.last = Nil;
        } else {
            L.last = L.last->prev;
            L.last->next = Nil;
        }
        P->next = Nil;
        P->prev = Nil;
    }
}

void delAfter(listinduk &L, address &P, address Prec) {
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        if (P->next != Nil) {
            P->next->prev = Prec;
        } else {
            L.last = Prec;
        }
        Prec->next = P->next;
        P->next = Nil;
        P->prev = Nil;
    }
}

void delP(listinduk &L, infotypeinduk X) {
    address P = findElm(L, X);
    if (P != Nil) {
        // Hapus semua anak terlebih dahulu
        address_anak anakCurrent = P->lanak.first;
        while (anakCurrent != Nil) {
            address_anak temp = anakCurrent;
            anakCurrent = anakCurrent->next;
            dealokasiAnak(temp);
        }
        
        // Hapus induk dari list
        if (P == L.first) {
            L.first = P->next;
            if (L.first != Nil) {
                L.first->prev = Nil;
            }
        } else if (P == L.last) {
            L.last = P->prev;
            if (L.last != Nil) {
                L.last->next = Nil;
            }
        } else {
            P->prev->next = P->next;
            P->next->prev = P->prev;
        }
        P->next = Nil;
        P->prev = Nil;
        dealokasi(P);
    }
}

// ========== PENGHAPUSAN ELEMEN ANAK ==========
void delFirstAnak(listanak &L, address_anak &P) {
    if (!ListEmptyAnak(L)) {
        P = L.first;
        if (L.first == L.last) {
            L.first = Nil;
            L.last = Nil;
        } else {
            L.first = L.first->next;
            L.first->prev = Nil;
        }
        P->next = Nil;
        P->prev = Nil;
    }
}

void delLastAnak(listanak &L, address_anak &P) {
    if (!ListEmptyAnak(L)) {
        P = L.last;
        if (L.first == L.last) {
            L.first = Nil;
            L.last = Nil;
        } else {
            L.last = L.last->prev;
            L.last->next = Nil;
        }
        P->next = Nil;
        P->prev = Nil;
    }
}

void delAfterAnak(listanak &L, address_anak &P, address_anak Prec) {
    if (Prec != Nil && Prec->next != Nil) {
        P = Prec->next;
        if (P->next != Nil) {
            P->next->prev = Prec;
        } else {
            L.last = Prec;
        }
        Prec->next = P->next;
        P->next = Nil;
        P->prev = Nil;
    }
}

void delPAnak(listanak &L, infotypeanak X) {
    address_anak P = findElm(L, X);
    if (P != Nil) {
        if (P == L.first) {
            L.first = P->next;
            if (L.first != Nil) {
                L.first->prev = Nil;
            }
        } else if (P == L.last) {
            L.last = P->prev;
            if (L.last != Nil) {
                L.last->next = Nil;
            }
        } else {
            P->prev->next = P->next;
            P->next->prev = P->prev;
        }
        P->next = Nil;
        P->prev = Nil;
        dealokasiAnak(P);
    }
}

// ========== PROSES SEMUA ELEMEN LIST ==========
void printInfo(listinduk L) {
    address current = L.first;
    cout << "List Induk: ";
    while (current != Nil) {
        cout << current->info << " ";
        current = current->next;
    }
    cout << endl;
}

int nbList(listinduk L) {
    int count = 0;
    address current = L.first;
    while (current != Nil) {
        count++;
        current = current->next;
    }
    return count;
}

void printInfoAnak(listanak Lanak) {
    address_anak current = Lanak.first;
    cout << "List Anak: ";
    while (current != Nil) {
        cout << current->info << " ";
        current = current->next;
    }
    cout << endl;
}

int nbListAnak(listanak Lanak) {
    int count = 0;
    address_anak current = Lanak.first;
    while (current != Nil) {
        count++;
        current = current->next;
    }
    return count;
}

// ========== PROSES TERHADAP LIST ==========
void delAll(listinduk &L) {
    address current = L.first;
    while (current != Nil) {
        address temp = current;
        current = current->next;
        
        // Hapus semua anak
        address_anak anakCurrent = temp->lanak.first;
        while (anakCurrent != Nil) {
            address_anak anakTemp = anakCurrent;
            anakCurrent = anakCurrent->next;
            dealokasiAnak(anakTemp);
        }
        
        dealokasi(temp);
    }
    L.first = Nil;
    L.last = Nil;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "multilist.h"
using namespace std;

void displayMultiList(listinduk L) {
    cout << "\n=== MULTI LINKED LIST DATA ===" << endl;
    cout << "==============================" << endl;
    
    if (ListEmpty(L)) {
        cout << "List kosong!" << endl;
        return;
    }
    
    int counter = 1;
    address induk = L.first;
    
    while (induk != Nil) {
        cout << counter << ". INDUK: " << induk->info << endl;
        cout << "   Jumlah Anak: " << nbListAnak(induk->lanak) << endl;
        
        if (!ListEmptyAnak(induk->lanak)) {
            cout << "   Daftar Anak: ";
            address_anak anak = induk->lanak.first;
            while (anak != Nil) {
                cout << anak->info;
                if (anak->next != Nil) cout << " -> ";
                anak = anak->next;
            }
            cout << endl;
        } else {
            cout << "   (Tidak memiliki anak)" << endl;
        }
        
        counter++;
        induk = induk->next;
    }
    
    cout << "\nTotal Induk: " << nbList(L) << endl;
    cout << "==============================\n" << endl;
}

int main() {
    cout << "=== PROGRAM MULTI LINKED LIST ===" << endl;
    cout << "=== (Implementasi dari multilist.h) ===\n" << endl;
    
    // ========== 1. Buat list kosong ==========
    listinduk L_pegawai;
    CreateList(L_pegawai);
    cout << "1. List kosong dibuat" << endl;
    cout << "   List kosong? " << (ListEmpty(L_pegawai) ? "Ya" : "Tidak") << endl;
    
    // ========== 2. Alokasi dan insert induk ==========
    cout << "\n2. Alokasi dan insert induk (pegawai):" << endl;
    address peg1 = alokasi(101); // Pegawai dengan ID 101
    address peg2 = alokasi(102); // Pegawai dengan ID 102
    address peg3 = alokasi(103); // Pegawai dengan ID 103
    
    cout << "   - Alokasi pegawai 101: " << (peg1 != Nil ? "Berhasil" : "Gagal") << endl;
    cout << "   - Alokasi pegawai 102: " << (peg2 != Nil ? "Berhasil" : "Gagal") << endl;
    cout << "   - Alokasi pegawai 103: " << (peg3 != Nil ? "Berhasil" : "Gagal") << endl;
    
    insertFirst(L_pegawai, peg1);
    insertLast(L_pegawai, peg2);
    insertLast(L_pegawai, peg3);
    
    cout << "   Data setelah insert: ";
    printInfo(L_pegawai);
    cout << "   Jumlah induk: " << nbList(L_pegawai) << endl;
    
    // ========== 3. Alokasi dan insert anak ==========
    cout << "\n3. Alokasi dan insert anak:" << endl;
    
    // Anak untuk pegawai 101
    address_anak anak1_101 = alokasiAnak(1);
    address_anak anak2_101 = alokasiAnak(2);
    address_anak anak3_101 = alokasiAnak(3);
    
    insertFirstAnak(peg1->lanak, anak1_101);
    insertLastAnak(peg1->lanak, anak2_101);
    insertLastAnak(peg1->lanak, anak3_101);
    
    cout << "   - Anak pegawai 101: ";
    printInfoAnak(peg1->lanak);
    
    // Anak untuk pegawai 102
    address_anak anak1_102 = alokasiAnak(4);
    insertFirstAnak(peg2->lanak, anak1_102);
    
    cout << "   - Anak pegawai 102: ";
    printInfoAnak(peg2->lanak);
    
    // ========== 4. Tampilkan semua data ==========
    cout << "\n4. Tampilkan semua data:" << endl;
    displayMultiList(L_pegawai);
    
    // ========== 5. Cari elemen ==========
    cout << "5. Pencarian elemen:" << endl;
    address foundPeg = findElm(L_pegawai, 102);
    cout << "   - Cari pegawai 102: " << (foundPeg != Nil ? "Ditemukan" : "Tidak ditemukan") << endl;
    
    address_anak foundAnak = findElm(peg1->lanak, 2);
    cout << "   - Cari anak 2 di pegawai 101: " << (foundAnak != Nil ? "Ditemukan" : "Tidak ditemukan") << endl;
    
    // ========== 6. Delete anak ==========
    cout << "\n6. Delete anak 2 dari pegawai 101:" << endl;
    cout << "   Sebelum: ";
    printInfoAnak(peg1->lanak);
    delPAnak(peg1->lanak, 2);
    cout << "   Sesudah: ";
    printInfoAnak(peg1->lanak);
    
    // ========== 7. Delete induk ==========
    cout << "\n7. Delete induk (pegawai) 102:" << endl;
    cout << "   Sebelum delete: ";
    printInfo(L_pegawai);
    delP(L_pegawai, 102);
    cout << "   Sesudah delete: ";
    printInfo(L_pegawai);
    
    // ========== 8. Tampilkan data setelah penghapusan ==========
    cout << "\n8. Data setelah penghapusan:" << endl;
    displayMultiList(L_pegawai);
    
    // ========== 9. Test insertAfter ==========
    cout << "\n9. Test insertAfter:" << endl;
    address peg4 = alokasi(104);
    address peg5 = alokasi(105);
    
    insertLast(L_pegawai, peg4);
    
    // Insert peg5 setelah peg1
    insertAfter(L_pegawai, peg5, peg1);
    cout << "   Setelah insert pegawai 105 setelah 101: ";
    printInfo(L_pegawai);
    
    // ========== 10. Test deleteFirst dan deleteLast ==========
    cout << "\n10. Test deleteFirst dan deleteLast:" << endl;
    address deletedPeg;
    
    delFirst(L_pegawai, deletedPeg);
    cout << "   - Delete first: ";
    printInfo(L_pegawai);
    
    delLast(L_pegawai, deletedPeg);
    cout << "   - Delete last: ";
    printInfo(L_pegawai);
    
    // ========== 11. Hapus semua data ==========
    cout << "\n11. Hapus semua data (delAll):" << endl;
    delAll(L_pegawai);
    cout << "   List kosong? " << (ListEmpty(L_pegawai) ? "Ya" : "Tidak") << endl;
    
    cout << "\n=== PROGRAM SELESAI ===" << endl;
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/soal1modul11.jpg)

Penjelasan :
mengimplementasikan Multi Linked List dengan struktur data hierarkis dua level menggunakan doubly linked list untuk induk dan anak, dimana setiap elemen induk (seperti pegawai) menyimpan pointer ke list anaknya sendiri sehingga operasi insert dan delete harus memperhatikan hubungan parent-child, termasuk penghapusan rekursif dimana menghapus induk akan menghapus semua anaknya, dengan fungsi-fungsi yang mencakup manajemen memori alokasi dan dealokasi untuk kedua level, pencarian elemen baik di induk maupun anak, serta operasi dasar linked list yang dimodifikasi untuk menjaga hubungan hierarkis antara list induk dan list anak dalam sistem yang terintegrasi.

## soal 2
Buatlah prosedur untuk menampilkanhasil penelusuran DFS. 
prosedur PrintDFS (Graph G, adrNode N); 

### file circularlist.h
```cpp
#ifndef CIRCULARLIST_H_INCLUDED
#define CIRCULARLIST_H_INCLUDED

#include <string>
using namespace std;

#define Nil NULL

typedef struct {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
} infotype;

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

// 11 fungsi/prosedur untuk ADT circularlist
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertFirst(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void insertLast(List &L, address P);
void deleteFirst(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteLast(List &L, address &P);
address findElm(List L, infotype x);
void printInfo(List L);

#endif
```
### file circularlist.cpp
```cpp
#include <iostream>
#include <iomanip>
#include "circularlist.h"
using namespace std;

// procedure CreateList( input/output L : List )
void createList(List &L) {
    L.first = Nil;
}

// function alokasi( x : infotype ) → address
address alokasi(infotype x) {
    address P = new ElmList;
    if (P != Nil) {
        P->info = x;
        P->next = Nil;
    }
    return P;
}

// procedure dealokasi( input/output t P : address )
void dealokasi(address &P) {
    if (P != Nil) {
        delete P;
        P = Nil;
    }
}

// procedure insertFirst( input/output L : List, input P : address )
void insertFirst(List &L, address P) {
    if (P != Nil) {
        if (L.first == Nil) {
            // List kosong
            L.first = P;
            P->next = P; // Circular: menunjuk ke dirinya sendiri
        } else {
            // Cari elemen terakhir
            address last = L.first;
            while (last->next != L.first) {
                last = last->next;
            }
            
            P->next = L.first;
            L.first = P;
            last->next = P; // Update pointer last ke elemen pertama yang baru
        }
    }
}

// procedure insertAfter( input/output L : List, input Prec : address, P : address)
void insertAfter(List &L, address Prec, address P) {
    if (P != Nil && Prec != Nil) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

// procedure insertLast( input/output L : List, input P : address )
void insertLast(List &L, address P) {
    if (P != Nil) {
        if (L.first == Nil) {
            // List kosong
            L.first = P;
            P->next = P; // Circular
        } else {
            // Cari elemen terakhir
            address last = L.first;
            while (last->next != L.first) {
                last = last->next;
            }
            
            last->next = P;
            P->next = L.first;
        }
    }
}

// procedure deleteFirst( input/output L : List, input/output P : address )
void deleteFirst(List &L, address &P) {
    if (L.first != Nil) {
        if (L.first->next == L.first) {
            // Hanya ada satu elemen
            P = L.first;
            L.first = Nil;
        } else {
            // Cari elemen terakhir
            address last = L.first;
            while (last->next != L.first) {
                last = last->next;
            }
            
            P = L.first;
            L.first = L.first->next;
            last->next = L.first;
            P->next = Nil;
        }
    }
}

// procedure deleteAfter( input/output L : List, input Prec : address, input/output t P : address )
void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != Nil && Prec->next != Nil && Prec->next != Prec) {
        P = Prec->next;
        if (P == L.first) {
            deleteFirst(L, P);
        } else {
            Prec->next = P->next;
            P->next = Nil;
        }
    }
}

// procedure deleteLast( input/output L : List, P : address )
void deleteLast(List &L, address &P) {
    if (L.first != Nil) {
        if (L.first->next == L.first) {
            // Hanya ada satu elemen
            P = L.first;
            L.first = Nil;
        } else {
            // Cari elemen sebelum terakhir
            address last = L.first;
            address beforeLast = Nil;
            
            while (last->next != L.first) {
                beforeLast = last;
                last = last->next;
            }
            
            P = last;
            beforeLast->next = L.first;
            P->next = Nil;
        }
    }
}

// function findElm( L : List, x : infotype ) → address
address findElm(List L, infotype x) {
    if (L.first == Nil) {
        return Nil;
    }
    
    address P = L.first;
    do {
        if (P->info.nim == x.nim) {
            return P;
        }
        P = P->next;
    } while (P != L.first);
    
    return Nil;
}

// procedure printInfo( input L : List )
void printInfo(List L) {
    if (L.first == Nil) {
        cout << "List kosong!" << endl;
        return;
    }
    
    address P = L.first;
    int count = 0;
    
    do {
        cout << "Name : " << P->info.nama << endl;
        cout << "NIP  : " << P->info.nim << endl;
        cout << "L/P  : " << P->info.jenis_kelamin << endl;
        cout << "IPK  : " << fixed << setprecision(2) << P->info.ipk << endl;
        cout << endl;
        
        P = P->next;
        count++;
    } while (P != L.first);
    
    cout << "Total data: " << count << endl;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "circularlist.h"
using namespace std;

address createData(string nama, string nim, char jenis_kelamin, float ipk) {
    /**
    * PR : mengalokasikan sebuah elemen list dengan info dengan info sesuai input
    * FS : address P menunjuk elemen dengan info sesuai input
    */
    infotype x;
    address P;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;
    P = alokasi(x);
    return P;
}

int main() {
    List L, A, B, L2;
    address P1 = Nil;
    address P2 = Nil;
    infotype x;
    
    createList(L);
    
    // 1. Insert Danu (04) first
    P1 = createData("Danu", "04", 'l', 4.0);
    insertFirst(L, P1);
    
    // 2. Insert Fahmi (06) last
    P1 = createData("Fahmi", "06", 'l', 3.45);
    insertLast(L, P1);
    
    // 3. Insert Bobi (02) first
    P1 = createData("Bobi", "02", 'l', 3.71);
    insertFirst(L, P1);
    
    // 4. Insert Ali (01) first
    P1 = createData("Ali", "01", 'l', 3.3);
    insertFirst(L, P1);
    
    // 5. Insert Gita (07) last
    P1 = createData("Gita", "07", 'p', 3.75);
    insertLast(L, P1);
    
    // 6. Insert Cindi (03) after Gita (07)
    x.nim = "07";
    P1 = findElm(L, x);
    P2 = createData("Cindi", "03", 'p', 3.5);
    insertAfter(L, P1, P2);
    
    // 7. Insert Hilmi (08) after Bobi (02)
    x.nim = "02";
    P1 = findElm(L, x);
    P2 = createData("Hilmi", "08", 'p', 3.3);
    insertAfter(L, P1, P2);
    
    // 8. Insert Eli (05) after Danu (04)
    x.nim = "04";
    P1 = findElm(L, x);
    P2 = createData("Eli", "05", 'p', 3.4);
    insertAfter(L, P1, P2);
    
    // 9. Print semua data
    printInfo(L);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/soal2modul11.jpg)

Penjelasan :
Program ini mengimplementasikan Circular Linked List untuk menyimpan data mahasiswa dengan operasi dasar seperti insert first, insert last, insert after, delete, dan pencarian berdasarkan NIM. Struktur data bersifat melingkar dimana elemen terakhir menunjuk kembali ke elemen pertama, dengan fungsi printInfo yang menampilkan semua data dalam format yang sesuai contoh.

## soal 3
Buatlah prosedur untuk menampilkanhasil penelusuran DFS. 
prosedur PrintBFS (Graph G, adrNode N); 

### file circularlist.h
```cpp
#ifndef CIRCULARLIST_H_INCLUDED
#define CIRCULARLIST_H_INCLUDED

#include <string>
using namespace std;

#define Nil NULL

typedef struct {
    string nama;
    string nim;
    char jenis_kelamin;
    float ipk;
} infotype;

typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

// 11 fungsi/prosedur untuk ADT circularlist
void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void insertFirst(List &L, address P);
void insertAfter(List &L, address Prec, address P);
void insertLast(List &L, address P);
void deleteFirst(List &L, address &P);
void deleteAfter(List &L, address Prec, address &P);
void deleteLast(List &L, address &P);
address findElm(List L, infotype x);
void printInfo(List L);

#endif
```
### file circularlist.cpp
```cpp
#include <iostream>
#include <iomanip>
#include "circularlist.h"
using namespace std;

// procedure CreateList( input/output L : List )
void createList(List &L) {
    L.first = Nil;
}

// function alokasi( x : infotype ) → address
address alokasi(infotype x) {
    address P = new ElmList;
    if (P != Nil) {
        P->info = x;
        P->next = Nil;
    }
    return P;
}

// procedure dealokasi( input/output t P : address )
void dealokasi(address &P) {
    if (P != Nil) {
        delete P;
        P = Nil;
    }
}

// procedure insertFirst( input/output L : List, input P : address )
void insertFirst(List &L, address P) {
    if (P != Nil) {
        if (L.first == Nil) {
            // List kosong
            L.first = P;
            P->next = P; // Circular: menunjuk ke dirinya sendiri
        } else {
            // Cari elemen terakhir
            address last = L.first;
            while (last->next != L.first) {
                last = last->next;
            }
            
            P->next = L.first;
            L.first = P;
            last->next = P; // Update pointer last ke elemen pertama yang baru
        }
    }
}

// procedure insertAfter( input/output L : List, input Prec : address, P : address)
void insertAfter(List &L, address Prec, address P) {
    if (P != Nil && Prec != Nil) {
        P->next = Prec->next;
        Prec->next = P;
    }
}

// procedure insertLast( input/output L : List, input P : address )
void insertLast(List &L, address P) {
    if (P != Nil) {
        if (L.first == Nil) {
            // List kosong
            L.first = P;
            P->next = P; // Circular
        } else {
            // Cari elemen terakhir
            address last = L.first;
            while (last->next != L.first) {
                last = last->next;
            }
            
            last->next = P;
            P->next = L.first;
        }
    }
}

// procedure deleteFirst( input/output L : List, input/output P : address )
void deleteFirst(List &L, address &P) {
    if (L.first != Nil) {
        if (L.first->next == L.first) {
            // Hanya ada satu elemen
            P = L.first;
            L.first = Nil;
        } else {
            // Cari elemen terakhir
            address last = L.first;
            while (last->next != L.first) {
                last = last->next;
            }
            
            P = L.first;
            L.first = L.first->next;
            last->next = L.first;
            P->next = Nil;
        }
    }
}

// procedure deleteAfter( input/output L : List, input Prec : address, input/output t P : address )
void deleteAfter(List &L, address Prec, address &P) {
    if (Prec != Nil && Prec->next != Nil && Prec->next != Prec) {
        P = Prec->next;
        if (P == L.first) {
            deleteFirst(L, P);
        } else {
            Prec->next = P->next;
            P->next = Nil;
        }
    }
}

// procedure deleteLast( input/output L : List, P : address )
void deleteLast(List &L, address &P) {
    if (L.first != Nil) {
        if (L.first->next == L.first) {
            // Hanya ada satu elemen
            P = L.first;
            L.first = Nil;
        } else {
            // Cari elemen sebelum terakhir
            address last = L.first;
            address beforeLast = Nil;
            
            while (last->next != L.first) {
                beforeLast = last;
                last = last->next;
            }
            
            P = last;
            beforeLast->next = L.first;
            P->next = Nil;
        }
    }
}

// function findElm( L : List, x : infotype ) → address
address findElm(List L, infotype x) {
    if (L.first == Nil) {
        return Nil;
    }
    
    address P = L.first;
    do {
        if (P->info.nim == x.nim) {
            return P;
        }
        P = P->next;
    } while (P != L.first);
    
    return Nil;
}

// procedure printInfo( input L : List )
void printInfo(List L) {
    if (L.first == Nil) {
        cout << "List kosong!" << endl;
        return;
    }
    
    address P = L.first;
    int count = 0;
    
    do {
        cout << "Name : " << P->info.nama << endl;
        cout << "NIP  : " << P->info.nim << endl;
        cout << "L/P  : " << P->info.jenis_kelamin << endl;
        cout << "IPK  : " << fixed << setprecision(2) << P->info.ipk << endl;
        cout << endl;
        
        P = P->next;
        count++;
    } while (P != L.first);
    
    cout << "Total data: " << count << endl;
}
```
### file main.cpp
```cpp
#include <iostream>
#include "circularlist.h"
using namespace std;

address createData(string nama, string nim, char jenis_kelamin, float ipk) {
    /**
    * PR : mengalokasikan sebuah elemen list dengan info dengan info sesuai input
    * FS : address P menunjuk elemen dengan info sesuai input
    */
    infotype x;
    address P;
    x.nama = nama;
    x.nim = nim;
    x.jenis_kelamin = jenis_kelamin;
    x.ipk = ipk;
    P = alokasi(x);
    return P;
}

int main() {
    List L, A, B, L2;
    address P1 = Nil;
    address P2 = Nil;
    infotype x;
    
    createList(L);
    
    // 1. Insert Danu (04) first
    P1 = createData("Danu", "04", 'l', 4.0);
    insertFirst(L, P1);
    
    // 2. Insert Fahmi (06) last
    P1 = createData("Fahmi", "06", 'l', 3.45);
    insertLast(L, P1);
    
    // 3. Insert Bobi (02) first
    P1 = createData("Bobi", "02", 'l', 3.71);
    insertFirst(L, P1);
    
    // 4. Insert Ali (01) first
    P1 = createData("Ali", "01", 'l', 3.3);
    insertFirst(L, P1);
    
    // 5. Insert Gita (07) last
    P1 = createData("Gita", "07", 'p', 3.75);
    insertLast(L, P1);
    
    // 6. Insert Cindi (03) after Gita (07)
    x.nim = "07";
    P1 = findElm(L, x);
    P2 = createData("Cindi", "03", 'p', 3.5);
    insertAfter(L, P1, P2);
    
    // 7. Insert Hilmi (08) after Bobi (02)
    x.nim = "02";
    P1 = findElm(L, x);
    P2 = createData("Hilmi", "08", 'p', 3.3);
    insertAfter(L, P1, P2);
    
    // 8. Insert Eli (05) after Danu (04)
    x.nim = "04";
    P1 = findElm(L, x);
    P2 = createData("Eli", "05", 'p', 3.4);
    insertAfter(L, P1, P2);
    
    // 9. Print semua data
    printInfo(L);
    
    return 0;
}
```

> Output
> ![Screenshot bagian x](output/soal2modul11.jpg)

Penjelasan :
Program ini mengimplementasikan Circular Linked List untuk menyimpan data mahasiswa dengan operasi dasar seperti insert first, insert last, insert after, delete, dan pencarian berdasarkan NIM. Struktur data bersifat melingkar dimana elemen terakhir menunjuk kembali ke elemen pertama, dengan fungsi printInfo yang menampilkan semua data dalam format yang sesuai contoh.

1. https://www.w3schools.com/cpp/cpp_for_loop_nested.asp
2. https://www.w3schools.com/cpp/cpp_arrays.asp
3. https://www.w3schools.com/cpp/cpp_arrays_loop.asp
4. https://www.w3schools.com/cpp/cpp_references.asp
5. https://www.w3schools.com/cpp/cpp_pointers.asp
6. https://www.w3schools.com/cpp/cpp_function_param.asp
7. https://www.w3schools.com/cpp/cpp_function_array.asp
8. https://www.w3schools.com/cpp/cpp_stacks.asp

