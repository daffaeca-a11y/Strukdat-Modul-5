# <h1 align="center">Laporan Praktikum Modul 5 - SinglyList Bagian 2</h1>
<p align="center">Muhammad Daffa Sha'ib Nandana - 109082500023</p>

## Dasar Teori
Operasi utama pada Singly Linked List meliputi penelusuran, penambahan, penghapusan, dan pencarian elemen. Penelusuran dilakukan dengan mengunjungi setiap node secara berurutan mulai dari penanda awal hingga node terakhir yang menunjuk ke nilai null, yang berguna untuk menampilkan data atau menghitung total elemen. Penambahan node dapat dilakukan di awal dengan mengarahkan pointer node baru ke node awal saat ini, di akhir dengan menelusuri hingga node paling belakang, atau di posisi tertentu dengan menyesuaikan acuan pointer node sebelumnya. Sementara itu, penghapusan node dilakukan dengan mengubah alur pointer node sebelum target langsung ke node setelahnya lalu membebaskan alokasi memori, sedangkan pencarian elemen bekerja dengan memeriksa nilai data pada setiap node satu per satu dari awal.



## Unguided 

### 1. Menampilkan Singly Linked List

#ifndef SINGLYLIST_H_INCLUDED
#define SINGLYLIST_H_INCLUDED

typedef int infotype;
typedef struct ElmList *address;

struct ElmList {
    infotype info;
    address next;
};

struct List {
    address first;
};

void createList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(const List &L);
void insertFirst(List &L, address P);
address findElm(const List &L, infotype x);
int totalInfo(const List &L);

#endif 

##### Output 1
![Screenshot Output Unguided 1_1] https://github.com/daffaeca-a11y/Strukdat-Modul-5/blob/main/output%20modul%205.jpeg

#ifndef, #define, dan #endif di bagian awal dan akhir berkas berfungsi sebagai header guard untuk mencegah terjadinya kesalahan pendefinisian ulang saat berkas ini dipanggil lebih dari satu kali dalam program.


### 2. Mencari Elemen Bernilai 8

#include <iostream>
#include "Singlylist.h"
using namespace std;

void createList(List &L) {
    L.first = nullptr;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = nullptr;
    return P;
}

void dealokasi(address &P) {
    if (P != nullptr) {
        delete P;
        P = nullptr;
    }
}

void printInfo(const List &L) {
    address P = L.first;
    while (P != nullptr) {
        cout << P->info;
        if (P->next != nullptr) cout << " ";
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    if (P == nullptr) return;
    P->next = L.first;
    L.first = P;
}

address findElm(const List &L, infotype x) {
    address P = L.first;
    while (P != nullptr) {
        if (P->info == x) return P;
        P = P->next;
    }
    return nullptr;
}

int totalInfo(const List &L) {
    int total = 0;
    address P = L.first;
    while (P != nullptr) {
        total += P->info;
        P = P->next;
    }
    return total;
}

##### Output 2
![Screenshot Output Unguided 2_1] https://github.com/daffaeca-a11y/Strukdat-Modul-5/blob/main/output%20modul%205.jpeg

Prosedur createList berfungsi mengosongkan list dengan mengatur pointer awal L.first menjadi nullptr. Fungsi alokasi bertugas membuat node baru secara dinamis di memori menggunakan operator new, mengisi variabel info dengan nilai x, menyetel pointer next ke nullptr, lalu mengembalikan alamat node tersebut. Sebaliknya, prosedur dealokasi membebaskan memori node menggunakan operator delete dan mengubah pointer P menjadi nullptr untuk mencegah terjadinya dangling pointer.

### 3. Menghitung Total Nilai Semua Elemen

#include <iostream>
#include "Singlylist.h"
using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5;
    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    cout << "Isi linked list: ";
    printInfo(L);

    address hasil = findElm(L, 8);
    if (hasil != nullptr) {
        cout << hasil->info << " ditemukan dalam list" << endl;
    } else {
        cout << "Data tidak ditemukan dalam list" << endl;
    }

    cout << "Total info dari kelima elemen adalah "
         << totalInfo(L) << endl;

    while (L.first != nullptr) {
        address Hapus = L.first;
        L.first = L.first->next;
        dealokasi(Hapus);
    }

    return 0;
}

##### Output 3
![Screenshot Output Unguided 3_1] https://github.com/daffaeca-a11y/Strukdat-Modul-5/blob/main/output%20modul%205.jpeg

Program diawali dengan mendeklarasikan variabel list L serta pointer node P1 hingga P5, lalu memanggil createList(L) untuk memastikan pointer L.first bernilai nullptr. Selanjutnya, program mengalokasikan dan menyisipkan lima elemen bernilai 2, 0, 8, 12, dan 9 secara berurutan di posisi paling depan list menggunakan insertFirst. Karena setiap penambahan dilakukan di awal, urutan penyimpanan di dalam memori menjadi terbalik dari urutan pembuatannya, sehingga panggilan printInfo(L) akan mencetak keluaran 9 12 8 0 2.

## Kesimpulan
Kesimpulan dari modul kali ini adalah program Singly Linked List yang disusun secara modular, terbagi menjadi berkas header untuk definisi tipe data, berkas implementasi logika operasi, serta berkas utama untuk pengujian alur program. Penggunaan fungsi penyisipan di awal membuat setiap elemen baru diletakkan pada posisi paling depan, sehingga urutan pengalokasian data dari angka 2 hingga 9 menghasilkan urutan penyimpanan terbalik menjadi 9, 12, 8, 0, dan 2 saat ditampilkan ke layar. Operasi pemrosesan seperti menampilkan isi list, mencari elemen bernilai 8, hingga menghitung akumulasi total nilai elemen sebesar 31 bekerja melalui penelusuran sekuensial dengan mengikuti rantai pointer dari node awal hingga akhir

## Referensi
[1] Triase. (2020). Diktat Edisi Revisi : STRUKTUR DATA. Medan: UNIVERSTAS ISLAM NEGERI SUMATERA UTARA MEDAN. 
<br>[2] Indahyati, Uce., Rahmawati Yunianita. (2020). "BUKU AJAR ALGORITMA DAN PEMROGRAMAN DALAM BAHASA C++". Sidoarjo: Umsida Press. Diakses pada 10 Maret 2024 melalui https://doi.org/10.21070/2020/978-623-6833-67-4.

