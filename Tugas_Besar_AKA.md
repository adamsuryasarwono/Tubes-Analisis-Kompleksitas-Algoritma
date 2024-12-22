# <h1 align="center">TUGAS BESAR ANALISIS KOMPLEKSITAS ALGORITMA (AKA)</h1>
# <h2 align="center">Algoritma Pencarian Tercepat dalam Aplikasi E-commerce</h2>

### Anggota Kelompok 
Christoba Joshua Hutagalung - 2311102133 <br/>
Adam Surya Sarwono - 2311102112 <br/>
Kelas S1IF-11-04 <br/>
Telkom University Purwokerto <br/>

### Dasar Teori Algoritma Search
Searching (pencarian) pada struktur data mengacu pada proses algoritmik untuk memeriksa, menemukan, mengambil posisi elemen tertentu (target) dari kumpulan elemen di dalam struktur data. Kumpulan elemen dapat berupa array, list, linked list, tree, dan lain sebagainya.
Berdasarkan jenis operasinya, dua algoritma pencarian yaitu Sequential Search dan Binary Search pada data array.
### Sequential search <br/>
Sequential Search (pencarian berurutan) dikenal juga sebagai pencarian linier. Sequential Search merupakan algoritma pencarian paling dasar dan paling sederhana yang bekerja menggunakan pendekatan brute force, mencoba segala kemungkinan yang ada hingga target yang diinginkan ditemukan. 
Sebagai contoh, mencari nilai 36 dari data array {12, 7, 30, 28, 2, 19, 36, 21, 16, 9}. Sequential Search dimulai dengan membandingkan/mencocokkan 36 dengan elemen pertama/index[0] yaitu 12, karena 12 tidak sesuai dengan kriteria pencarian (12 != 36) maka dilanjutkan dengan membandingkan 36 
dengan elemen berikutnya hingga ditemukan elemen yang cocok, yaitu pada index[6] dimana 36 == 36.

Cara kerja sequential search Algoritma dimulai dengan membandingkan elemen pertama dengan elemen yang dicari. Jika cocok, pencarian selesai.Jika tidak, ia akan terus memeriksa elemen berikutnya sampai menemukan elemen yang dicari atau mencapai akhir kumpulan data.lalu sequential search memilikki 
kekurangan seperti kurang efisien untuk kumpulan data besar karena memerlukan pemeriksaan setiap elemen dalam kumpulan data, bahkan jika elemen yang dicari ada di awal kumpulan data.
Berikut adalah konsep dasar dan langkah-langkah implementasi Sequential Search:
A.Konsep Dasar:

    Pencarian Berurutan: Algoritma Sequential Search melakukan pencarian satu per satu dari awal hingga akhir kumpulan data.
    Metode Brute Force: Ini adalah pendekatan brute force di mana algoritma mencoba semua kemungkinan sampai elemen yang dicari ditemukan.
    Kompleksitas Waktu: Kompleksitas waktu dari Sequential Search adalah O(n), di mana n adalah jumlah elemen dalam kumpulan data.

B.Langkah-langkah Implementasi:

    1.Inisialisasi indeks pencarian:
    2.Memulai perulangan untuk memeriksa setiap elemen dalam kumpulan data.
    3.Membandingkan elemen yang sedang diperiksa dengan elemen yang dicari.
    4.Jika elemen yang sedang diperiksa cocok dengan elemen yang dicari, pencarian selesai, dan indeks elemen tersebut dikembalikan.
    5.Jika tidak, lanjutkan perulangan untuk memeriksa elemen berikutnya.
    6.Jika seluruh kumpulan data telah diperiksa dan elemen yang dicari tidak ditemukan, kembalikan nilai yang menunjukkan bahwa elemen tidak ada dalam kumpulan data.

### Algoritma Search menggunakan Sequential Search secara Iteratif
```C++
#include <iostream>
#include <string>
#include <chrono>

using namespace std;

int cariProdukIteratif(const string produk[], int n, string cariProduk) {
    for (int i = 0; i < n; i++) {
        if (produk[i] == cariProduk) return i;
    }
    return -1;
}

int cariIDIteratif(const int idProduk[], int n, int cariID) {
    for (int i = 0; i < n; i++) {
        if (idProduk[i] == cariID) return i;
    }
    return -1;
}

int main() {
    const int n = 10;
    string produk[n] = {"Laptop", "Smartphone", "Tablet", "Keyboard", "Mouse", "Headphone", "Monitor", "Printer", "Speaker", "Charger"};
    int idProduk[n] = {101, 102, 103, 104, 105, 106, 107, 108, 109, 110};
    string cariProduk;
    int cariID;
    int hasil;

    cout << "Program Pencarian Barang di Toko Online (Iteratif)" << endl;
    cout << "Daftar produk di toko: {" << endl;
    for (int i = 0; i < n; i++) {
        cout << idProduk[i] << ": " << produk[i] << endl;
    }
    cout << "}" << endl;

    cout << "\nPilih cara cari:" << endl;
    cout << "1. Cari berdasarkan nama produk" << endl;
    cout << "2. Cari berdasarkan ID produk" << endl;
    cout << "Masukkan pilihan (1 atau 2): ";
    int pilihan;
    cin >> pilihan;

    auto start = chrono::high_resolution_clock::now();

    if (pilihan == 1) {
        cout << "Masukkan nama produk yang ingin dicari: ";
        cin.ignore();
        getline(cin, cariProduk);
        hasil = cariProdukIteratif(produk, n, cariProduk);
    } else if (pilihan == 2) {
        cout << "Masukkan ID produk yang ingin dicari: ";
        cin >> cariID;
        hasil = cariIDIteratif(idProduk, n, cariID);
    } else {
        cout << "Pilihan nggak valid." << endl;
        return 1;
    }

    auto end = chrono::high_resolution_clock::now();
    chrono::duration<double> elapsed = end - start;

    if (hasil != -1) {
        if (pilihan == 1) {
            cout << "\nProduk " << cariProduk << " ketemu di indeks ke-" << hasil << endl;
        } else {
            cout << "\nID produk " << cariID << " ketemu di indeks ke-" << hasil << endl;
        }
    } else {
        cout << "Produk atau ID nggak ketemu." << endl;
    }
    cout << "Waktu eksekusi: " << elapsed.count() << " detik" << endl;
    return 0;
}
```
### Output Kodenya:
![Output_Iteratif]
### Algoritma Search menggunakan Sequential Search secara Rekursif
```C++
#include <iostream>
#include <string>
#include <chrono>

using namespace std;

int cariProdukRekursif(const string produk[], int n, string cariProduk, int index) {
    if (index >= n) return -1;
    if (produk[index] == cariProduk) return index;
    return cariProdukRekursif(produk, n, cariProduk, index + 1);
}

int cariIDRekursif(const int idProduk[], int n, int cariID, int index) {
    if (index >= n) return -1;
    if (idProduk[index] == cariID) return index;
    return cariIDRekursif(idProduk, n, cariID, index + 1);
}

int main() {
    const int n = 10;
    string produk[n] = {"Laptop", "Smartphone", "Tablet", "Keyboard", "Mouse", "Headphone", "Monitor", "Printer", "Speaker", "Charger"};
    int idProduk[n] = {101, 102, 103, 104, 105, 106, 107, 108, 109, 110};
    string cariProduk;
    int cariID;
    int hasil;

    cout << "Program Pencarian Barang di Toko Online (Rekursif)" << endl;
    cout << "Daftar produk di toko: {" << endl;
    for (int i = 0; i < n; i++) {
        cout << idProduk[i] << ": " << produk[i] << endl;
    }
    cout << "}" << endl;

    cout << "\nPilih cara cari:" << endl;
    cout << "1. Cari berdasarkan nama produk" << endl;
    cout << "2. Cari berdasarkan ID produk" << endl;
    cout << "Masukkan pilihan (1 atau 2): ";
    int pilihan;
    cin >> pilihan;

    auto start = chrono::high_resolution_clock::now();

    if (pilihan == 1) {
        cout << "Masukkan nama produk yang ingin dicari: ";
        cin.ignore();
        getline(cin, cariProduk);
        hasil = cariProdukRekursif(produk, n, cariProduk, 0);
    } else if (pilihan == 2) {
        cout << "Masukkan ID produk yang ingin dicari: ";
        cin >> cariID;
        hasil = cariIDRekursif(idProduk, n, cariID, 0);
    } else {
        cout << "Pilihan nggak valid." << endl;
        return 1;
    }

    auto end = chrono::high_resolution_clock::now();
    chrono::duration<double> elapsed = end - start;

    if (hasil != -1) {
        if (pilihan == 1) {
            cout << "\nProduk " << cariProduk << " ketemu di indeks ke-" << hasil << endl;
        } else {
            cout << "\nID produk " << cariID << " ketemu di indeks ke-" << hasil << endl;
        }
    } else {
        cout << "Produk atau ID nggak ketemu." << endl;
    }
    cout << "Waktu eksekusi: " << elapsed.count() << " detik" << endl;
    return 0;
}
```
### Output Kodenya:

