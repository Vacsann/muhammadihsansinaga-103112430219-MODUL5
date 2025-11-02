# muhammadihsansinaga-103112430219-MODUL5
# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA) </h1>
<p align="center">MUHAMMAD IHSAN SINAGA - 103112430219</p>

## Dasar Teori

Singly Linked List merupakan salah satu jenis struktur data dinamis yang tersusun dari kumpulan node, di mana setiap node berisi data dan pointer yang menunjuk ke node berikutnya. Tidak seperti array yang memiliki ukuran tetap, linked list memungkinkan penambahan maupun penghapusan elemen secara mudah tanpa perlu menggeser data lain. Proses pencarian data dilakukan secara berurutan dari node pertama hingga akhir, sedangkan pengelolaan data dilakukan dengan memanipulasi pointer antar node. Keunggulan struktur ini terletak pada fleksibilitas ukuran dan efisiensi dalam operasi penyisipan atau penghapusan, namun memiliki kelemahan karena akses datanya tidak bisa dilakukan secara langsung serta membutuhkan ruang tambahan untuk menyimpan pointer.
## Guided
### soal 1 (linkedlist.cpp)
```c++
#include <iostream>
using namespace std;

struct Node {
    int nilai;
    Node* next;
};

Node* head = nullptr;

// Buat node baru
Node* buatNode(int angka) {
    Node* baru = new Node();
    baru->nilai = angka;
    baru->next = nullptr;
    return baru;
}

// Tambah data di depan
void tambahDepan(int angka) {
    Node* baru = buatNode(angka);
    baru->next = head;
    head = baru;
    cout << "Data " << angka << " ditambahkan di depan.\n";
}

// Tambah data di belakang
void tambahBelakang(int angka) {
    Node* baru = buatNode(angka);
    if (head == nullptr) {
        head = baru;
    } else {
        Node* bantu = head;
        while (bantu->next != nullptr) {
            bantu = bantu->next;
        }
        bantu->next = baru;
    }
    cout << "Data " << angka << " ditambahkan di belakang.\n";
}

// Tambah data setelah target
void sisipSetelah(int target, int angkaBaru) {
    Node* bantu = head;
    while (bantu != nullptr && bantu->nilai != target) {
        bantu = bantu->next;
    }

    if (bantu == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* baru = buatNode(angkaBaru);
        baru->next = bantu->next;
        bantu->next = baru;
        cout << "Data " << angkaBaru << " disisipkan setelah " << target << ".\n";
    }
}

// Hapus data tertentu
void hapusData(int angka) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* hapus = head;
    Node* prev = nullptr;

    if (hapus != nullptr && hapus->nilai == angka) {
        head = hapus->next;
        delete hapus;
        cout << "Data " << angka << " dihapus.\n";
        return;
    }

    while (hapus != nullptr && hapus->nilai != angka) {
        prev = hapus;
        hapus = hapus->next;
    }

    if (hapus == nullptr) {
        cout << "Data " << angka << " tidak ditemukan!\n";
    } else {
        prev->next = hapus->next;
        delete hapus;
        cout << "Data " << angka << " dihapus.\n";
    }
}

// Update data
void ubahData(int lama, int baru) {
    Node* bantu = head;
    while (bantu != nullptr && bantu->nilai != lama) {
        bantu = bantu->next;
    }

    if (bantu == nullptr) {
        cout << "Data " << lama << " tidak ditemukan!\n";
    } else {
        bantu->nilai = baru;
        cout << "Data " << lama << " berhasil diubah menjadi " << baru << ".\n";
    }
}

// Tampilkan isi list
void tampilList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }
    Node* bantu = head;
    cout << "Isi Linked List: ";
    while (bantu != nullptr) {
        cout << bantu->nilai << " -> ";
        bantu = bantu->next;
    }
    cout << "NULL\n";
}

// Program utama
int main() {
    int pilih, angka, target, baru;

    do {
        cout << "\n=== MENU LINKED LIST ===\n";
        cout << "1. Tambah Depan\n";
        cout << "2. Tambah Belakang\n";
        cout << "3. Sisip Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Ubah Data\n";
        cout << "6. Tampilkan List\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilih;

        switch (pilih) {
            case 1:
                cout << "Masukkan angka: ";
                cin >> angka;
                tambahDepan(angka);
                break;
            case 2:
                cout << "Masukkan angka: ";
                cin >> angka;
                tambahBelakang(angka);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> baru;
                sisipSetelah(target, baru);
                break;
            case 4:
                cout << "Masukkan angka yang ingin dihapus: ";
                cin >> angka;
                hapusData(angka);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> angka;
                cout << "Masukkan data baru: ";
                cin >> baru;
                ubahData(angka, baru);
                break;
            case 6:
                tampilList();
                break;
            case 0:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }

    } while (pilih != 0);

    return 0;
}

```
Program ini membuat Singly Linked List dengan node berisi data dan pointer. head sebagai awal list. Ada fungsi untuk tambah, sisip, hapus, ubah, dan tampilkan data. Semua operasi dilakukan dengan mengatur pointer antar node. Program pakai menu agar pengguna bisa pilih operasi.


> Output
### soal 2 (searching.cpp)
```c++
#include <iostream>
using namespace std;

#define NIL nullptr

// Struktur Node
struct Node {
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = NIL;
    }
};

// Kelas Linked List
class LinkedList {
private:
    Node* head;

public:
    // Konstruktor
    LinkedList() {
        head = NIL;
    }

    // Cek list kosong
    bool empty() {
        return head == NIL;
    }

    // Tambah depan
    void addFront(int value) {
        Node* baru = new Node(value);
        baru->next = head;
        head = baru;
    }

    // Tambah belakang
    void addBack(int value) {
        Node* baru = new Node(value);
        if (empty()) {
            head = baru;
        } else {
            Node* tail = head;
            while (tail->next != NIL) tail = tail->next;
            tail->next = baru;
        }
    }

    // Tambah setelah node tertentu
    void addAfter(Node* prev, int value) {
        if (prev != NIL) {
            Node* baru = new Node(value);
            baru->next = prev->next;
            prev->next = baru;
        }
    }

    // Hapus depan
    void removeFront() {
        if (!empty()) {
            Node* temp = head;
            head = head->next;
            delete temp;
        }
    }

    // Hapus belakang
    void removeBack() {
        if (!empty()) {
            if (head->next == NIL) {
                delete head;
                head = NIL;
            } else {
                Node* prev = NIL;
                Node* curr = head;
                while (curr->next != NIL) {
                    prev = curr;
                    curr = curr->next;
                }
                prev->next = NIL;
                delete curr;
            }
        }
    }

    // Hapus setelah node tertentu
    void removeAfter(Node* prev) {
        if (prev != NIL && prev->next != NIL) {
            Node* temp = prev->next;
            prev->next = temp->next;
            delete temp;
        }
    }

    // Hapus node dengan nilai tertentu
    void removeValue(int value) {
        if (empty()) return;
        Node* curr = head;
        Node* prev = NIL;

        while (curr != NIL && curr->data != value) {
            prev = curr;
            curr = curr->next;
        }

        if (curr != NIL) {
            if (prev == NIL) head = curr->next;
            else prev->next = curr->next;
            delete curr;
        }
    }

    // Hitung jumlah node
    int count() {
        int n = 0;
        Node* ptr = head;
        while (ptr != NIL) {
            n++;
            ptr = ptr->next;
        }
        return n;
    }

    // Tampilkan isi list
    void show() {
        if (empty()) {
            cout << "List kosong\n";
            return;
        }
        Node* ptr = head;
        cout << "Isi List: ";
        while (ptr != NIL) {
            cout << ptr->data << " ";
            ptr = ptr->next;
        }
        cout << endl;
    }

    // Cari node berdasarkan nilai
    Node* find(int value) {
        Node* ptr = head;
        while (ptr != NIL) {
            if (ptr->data == value) return ptr;
            ptr = ptr->next;
        }
        return NIL;
    }

    // Balik urutan list
    void reverse() {
        Node* prev = NIL;
        Node* curr = head;
        Node* next = NIL;
        while (curr != NIL) {
            next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        head = prev;
    }

    // Hapus semua elemen
    void clear() {
        Node* ptr = head;
        while (ptr != NIL) {
            Node* temp = ptr;
            ptr = ptr->next;
            delete temp;
        }
        head = NIL;
    }

    // Salin isi list ke list lain
    void copyTo(LinkedList &dest) {
        dest.clear();
        Node* ptr = head;
        while (ptr != NIL) {
            dest.addBack(ptr->data);
            ptr = ptr->next;
        }
    }

    // Destruktor
    ~LinkedList() {
        clear();
    }
};

// Main program
int main() {
    LinkedList L;

    cout << "=== Program Linked List C++ (Versi Beda) ===\n";

    L.addFront(10);
    L.addFront(5);
    L.addBack(15);
    L.addBack(20);

    L.show();
    cout << "Jumlah elemen: " << L.count() << endl;

    cout << "Hapus depan...\n";
    L.removeFront();
    L.show();

    cout << "Hapus belakang...\n";
    L.removeBack();
    L.show();

    cout << "Cari nilai 10...\n";
    Node* found = L.find(10);
    if (found) cout << "Ditemukan: " << found->data << endl;
    else cout << "Tidak ditemukan\n";

    cout << "Balik urutan list...\n";
    L.reverse();
    L.show();

    cout << "Hapus semua elemen...\n";
    L.clear();
    L.show();

    return 0;
}
```
Program ini membuat singly linked list dengan class. Setiap node menyimpan data dan alamat node berikutnya. Pointer head menandai awal list. Program memiliki fungsi untuk menambah data di depan atau belakang, menyisipkan setelah node tertentu, menghapus node di depan, belakang, atau sesuai nilai, mencari data, menghitung jumlah elemen, menampilkan isi list, membalik urutan list, dan menghapus semua data. Semua operasi dilakukan dengan mengatur pointer antar node. Program utama hanya mendemonstrasikan cara kerja fungsi-fungsi tersebut.

> Output

## Unguided

### Soal 1

```c++
#include <iostream>
#include <string>
using namespace std;

// Struktur node untuk menyimpan data pembeli
struct Node {
    string namaPembeli;
    string menu;
    Node* next;
};

// Pointer depan dan belakang antrian
Node* front = nullptr;
Node* rear = nullptr;

// Mengecek apakah antrian kosong
bool isEmpty() {
    return front == nullptr;
}

// Menambah pembeli ke dalam antrian (enqueue)
void tambahAntrian(const string& nama, const string& pesanan) {
    Node* nodeBaru = new Node{nama, pesanan, nullptr};

    if (isEmpty()) {
        front = rear = nodeBaru;
    } else {
        rear->next = nodeBaru;
        rear = nodeBaru;
    }

    cout << "Pembeli \"" << nama << "\" berhasil masuk ke antrian.\n";
}

// Melayani pembeli pertama (dequeue)
void layaniAntrian() {
    if (isEmpty()) {
        cout << "Tidak ada pembeli yang menunggu.\n";
        return;
    }

    Node* hapus = front;
    cout << "Sedang melayani: " << hapus->namaPembeli
         << " - Pesanan: " << hapus->menu << endl;

    front = front->next;
    if (front == nullptr) rear = nullptr;

    delete hapus;
}

// Menampilkan seluruh pembeli dalam antrian
void tampilAntrian() {
    if (isEmpty()) {
        cout << "Antrian kosong.\n";
        return;
    }

    cout << "\n=== DAFTAR ANTRIAN ===\n";
    Node* bantu = front;
    int posisi = 1;
    while (bantu != nullptr) {
        cout << posisi << ". " << bantu->namaPembeli 
             << " - " << bantu->menu << endl;
        bantu = bantu->next;
        posisi++;
    }
    cout << endl;
}

// Mencari pembeli berdasarkan nama
void cariPembeli(const string& namaCari) {
    if (isEmpty()) {
        cout << "Antrian kosong.\n";
        return;
    }

    Node* temp = front;
    int urutan = 1;
    bool ditemukan = false;

    while (temp != nullptr) {
        if (temp->namaPembeli == namaCari) {
            cout << "\nPembeli ditemukan!\n";
            cout << "Urutan : " << urutan << endl;
            cout << "Nama   : " << temp->namaPembeli << endl;
            cout << "Pesanan: " << temp->menu << endl;
            ditemukan = true;
            break;
        }
        temp = temp->next;
        urutan++;
    }

    if (!ditemukan) {
        cout << "Pembeli \"" << namaCari << "\" tidak ditemukan dalam antrian.\n";
    }
}

// Program utama
int main() {
    int pilihan;
    string nama, pesanan;

    do {
        cout << "=============================\n";
        cout << "    SISTEM ANTRIAN PEMBELI   \n";
        cout << "=============================\n";
        cout << "1. Tambah Antrian\n";
        cout << "2. Layani Pembeli\n";
        cout << "3. Lihat Antrian\n";
        cout << "4. Cari Pembeli\n";
        cout << "5. Keluar\n";
        cout << "=============================\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "Masukkan Nama Pembeli : ";
                getline(cin, nama);
                cout << "Masukkan Menu Pesanan : ";
                getline(cin, pesanan);
                tambahAntrian(nama, pesanan);
                break;
            case 2:
                layaniAntrian();
                break;
            case 3:
                tampilAntrian();
                break;
            case 4:
                cout << "Nama pembeli yang dicari: ";
                getline(cin, nama);
                cariPembeli(nama);
                break;
            case 5:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }

        cout << endl;
    } while (pilihan != 5);

    return 0;
}

```
Program ini merupakan implementasi sistem antrian pembeli menggunakan struktur data singly linked list dalam bahasa C++. Setiap pembeli direpresentasikan sebagai node yang menyimpan nama dan menu pesanan, serta pointer yang menghubungkan ke pembeli berikutnya. Program ini memiliki empat fitur utama, yaitu menambah pembeli ke dalam antrian, melayani pembeli terdepan, menampilkan seluruh daftar antrian, dan mencari pembeli berdasarkan nama. Proses penambahan dilakukan di bagian belakang antrian, sedangkan pelayanan menghapus data dari bagian depan dengan prinsip FIFO (First In First Out). Dengan penggunaan pointer, program ini memungkinkan pengelolaan antrian secara dinamis tanpa batasan ukuran tetap seperti array.
       
> Output
> ![Screenshot bagian x](ssmodul5unguided1.png)

### Soal 2

```c++
#include <iostream>
#include <string>
using namespace std;

struct Buku {
    string isbn, judul, penulis;
    Buku* next;
};

class DaftarBuku {
private:
    Buku* head;

public:
    DaftarBuku() { head = nullptr; }

    bool kosong() { return head == nullptr; }

    void tambahBuku(const string& isbn, const string& judul, const string& penulis) {
        Buku* baru = new Buku{isbn, judul, penulis, nullptr};
        if (kosong()) {
            head = baru;
        } else {
            Buku* temp = head;
            while (temp->next) temp = temp->next;
            temp->next = baru;
        }
        cout << "Buku berhasil ditambahkan!\n";
    }

    void tampilBuku() {
        if (kosong()) {
            cout << "Tidak ada data buku.\n";
            return;
        }
        cout << "\nDaftar Buku:\n";
        for (Buku* t = head; t; t = t->next) {
            cout << "ISBN    : " << t->isbn << "\n"
                 << "Judul   : " << t->judul << "\n"
                 << "Penulis : " << t->penulis << "\n"
                 << "-------------------------\n";
        }
    }

    void hapusBuku(const string& isbn) {
        if (kosong()) {
            cout << "Daftar buku kosong.\n";
            return;
        }
        Buku* temp = head;
        Buku* prev = nullptr;

        while (temp && temp->isbn != isbn) {
            prev = temp;
            temp = temp->next;
        }

        if (!temp) {
            cout << "Buku tidak ditemukan.\n";
            return;
        }

        if (!prev) head = head->next;
        else prev->next = temp->next;

        delete temp;
        cout << "Buku berhasil dihapus!\n";
    }

    void ubahBuku(const string& isbn) {
        Buku* temp = head;
        while (temp && temp->isbn != isbn) temp = temp->next;
        if (!temp) {
            cout << "Buku tidak ditemukan.\n";
            return;
        }
        cout << "Masukkan judul baru: ";
        getline(cin, temp->judul);
        cout << "Masukkan penulis baru: ";
        getline(cin, temp->penulis);
        cout << "Data buku diperbarui!\n";
    }

    void cariISBN(const string& isbn) {
        for (Buku* t = head; t; t = t->next) {
            if (t->isbn == isbn) {
                cout << "\nBuku ditemukan:\n"
                     << "ISBN    : " << t->isbn << "\n"
                     << "Judul   : " << t->judul << "\n"
                     << "Penulis : " << t->penulis << "\n";
                return;
            }
        }
        cout << "Buku tidak ditemukan.\n";
    }

    void cariJudul(const string& judul) {
        bool ketemu = false;
        for (Buku* t = head; t; t = t->next) {
            if (t->judul == judul) {
                if (!ketemu) cout << "\nBuku dengan judul \"" << judul << "\" ditemukan:\n";
                cout << "ISBN    : " << t->isbn << "\n"
                     << "Penulis : " << t->penulis << "\n"
                     << "-------------------------\n";
                ketemu = true;
            }
        }
        if (!ketemu) cout << "Buku tidak ditemukan.\n";
    }

    void cariPenulis(const string& penulis) {
        bool ketemu = false;
        for (Buku* t = head; t; t = t->next) {
            if (t->penulis == penulis) {
                if (!ketemu) cout << "\nBuku karya \"" << penulis << "\" ditemukan:\n";
                cout << "ISBN  : " << t->isbn << "\n"
                     << "Judul : " << t->judul << "\n"
                     << "-------------------------\n";
                ketemu = true;
            }
        }
        if (!ketemu) cout << "Buku tidak ditemukan.\n";
    }
};

int main() {
    DaftarBuku list;
    int pilihan;
    string isbn, judul, penulis;

    do {
        cout << "\n=== MENU DATA BUKU ===\n"
             << "1. Tambah Buku\n"
             << "2. Hapus Buku\n"
             << "3. Ubah Buku\n"
             << "4. Lihat Semua Buku\n"
             << "5. Cari ISBN\n"
             << "6. Cari Judul\n"
             << "7. Cari Penulis\n"
             << "8. Keluar\n"
             << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore();

        switch (pilihan) {
            case 1:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                cout << "Masukkan Judul: "; getline(cin, judul);
                cout << "Masukkan Penulis: "; getline(cin, penulis);
                list.tambahBuku(isbn, judul, penulis);
                break;
            case 2:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                list.hapusBuku(isbn);
                break;
            case 3:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                list.ubahBuku(isbn);
                break;
            case 4:
                list.tampilBuku();
                break;
            case 5:
                cout << "Masukkan ISBN: "; getline(cin, isbn);
                list.cariISBN(isbn);
                break;
            case 6:
                cout << "Masukkan Judul: "; getline(cin, judul);
                list.cariJudul(judul);
                break;
            case 7:
                cout << "Masukkan Penulis: "; getline(cin, penulis);
                list.cariPenulis(penulis);
                break;
            case 8:
                cout << "Program selesai.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 8);

    return 0;
}

```
Program di atas merupakan program manajemen data buku menggunakan struktur data Singly Linked List dalam bahasa C++. Setiap data buku disimpan dalam node yang berisi informasi ISBN, judul, dan penulis, serta pointer menuju node berikutnya. Program ini menyediakan berbagai fitur seperti menambah buku baru, menghapus data berdasarkan ISBN, memperbarui informasi buku, menampilkan seluruh daftar buku, serta mencari buku berdasarkan ISBN, judul, atau penulis. Semua operasi dilakukan secara dinamis tanpa batas ukuran, karena data disimpan menggunakan linked list. Melalui menu interaktif di fungsi main(), pengguna dapat mengelola data buku dengan mudah, dan setiap perubahan langsung diterapkan pada struktur linked list.


> Output
> ![Screenshot bagian x](ssmodul5unguided2.png)


## Referensi

1. https://en.wikipedia.org/wiki/Data_structure
