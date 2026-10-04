# Tugas Kelompok - Latihan 1 (Kasir Diskon)

Latihan pertemuan ke 2 **DART** untuk menghitung total pembayaran pelanggan berdasarkan jumlah belanja dan status keangotaan (member).

## Deskripsi Aturan Bisnis (Business Rule)
Program ini menerapkan beberapa aturan diskon sebagai berikut:
- Belanja minimal **100.000** mendapatkan diskon dasar 10%.
- Pelanggan dengan status **member** mendapatkan tambahan diskon 5%.
- Potongan diskon maksmimal yang bisa di dapatkan pelanggan adalah **25.000**.

# Anggota kelompok
1. M anggara (1124160219)
2. Kenzie Gabriel (1124160008)

```dart

// fungsi enum adalah untuk memilih tipe pelanggan

enum TipePelanggan {member, nonMember }

// bagian class untuk model pembelajaannya bro
class Transaksi {
  int id;
  double belanja;
  TipePelanggan tipe;
  
  Transaksi(this.id, this.belanja, this.tipe);
}

// ini fungsinya buat mencari sebuah persen diskon
int hitungPersenDiskon(Transaksi data) {
  int diskon = 0;
  if (data.belanja >= 100000) {
    diskon = 10;
    if (data.tipe == TipePelanggan.member) {
      diskon = diskon + 5;
    }
  }
  return diskon;
}

// ini fungsinya untuk bisa mencari sebuah nomial potongan
double hitungPotongan(Transaksi data, int persen) {
  double potongan = (persen / 100) * data.belanja;
  
  // batas max potongannya bro
  if (potongan > 25000) {
    potongan = 25000;
  }
  return potongan;
}

// fungsinya adalah untuk menghitung dari sebuah hasil akhir
double hitungTotalBayar(Transaksi data) {
  int persen = hitungPersenDiskon(data);
  double potongan = hitungPotongan(data, persen);
  return data.belanja - potongan;
}

// fungsinya untuk ngeloop dari sebuah pengulangan dari semua transaksi yang ada ----->
void jalankankasir (List<Transaksi> daftarBeli) {
  for (var data in daftarBeli) {
    double total = hitungTotalBayar(data);
    print("Skenario ${data.id} - Total Bayar: Rp${total.toInt()}");
  }
}

void main() {
  
  List<Transaksi> tesSkenario = [
    Transaksi(1, 80000, TipePelanggan.nonMember),
    Transaksi(2, 150000, TipePelanggan.nonMember),
    Transaksi(3, 150000, TipePelanggan.member),
    Transaksi(4, 300000, TipePelanggan.member),
  ];
  
  print("=== HASIL PROGRAM DARI KASIR ===");
  jalankankasir(tesSkenario);
}
```
