# Demo-Komnum-Praktikum-1
|    NRP     |           Nama             |
| :--------: |       :------------:       |
| 5025251218 | Mushallina Dzikri Rozana   |
| 5025251228 | Raden Roro Fabronita Sectia Farela                    |

# Laporan Praktikum Komputasi Numerik - 1
## 1. Pendahuluan & Penjelasan Soal
   Metode Regula Falsi (Metode Posisi Salah) adalah salah satu metode tertutup (akolade) yang digunakan untuk mencari akar-akar persamaan non-linier. Metode ini bekerja dengan cara menarik garis lurus yang menghubungkan dua titik fungsi $(x_1, f(x_1))$ dan $(x_2, f(x_2))$. Titik potong garis tersebut dengan sumbu X kemudian dijadikan sebagai estimasi akar baru ($x_3$).  Pada laporan ini, fokus utama adalah menyelesaikan persamaan:
    $$f(x) = \sin(x) - 5x + 2$$
 Tujuannya adalah mencari nilai $x$ yang menyebabkan nilai fungsi tersebut mendekati nol menggunakan iterasi numerik.  

## 2. Algoritma & Rumus Utama
Langkah-langkah yang diimplementasikan dalam kode program adalah:
.Syarat Bolzano: Memastikan bahwa $f(x_1) \cdot f(x_2) < 0$, yang artinya terdapat perubahan tanda sehingga dipastikan ada akar di antara rentang tersebut. 
.Rumus Regula Falsi: Menghitung nilai $x_3$ menggunakan interpolasi linier:
$$x_3 = \frac{x_1 \cdot f(x_2) - x_2 \cdot f(x_1)}{f(x_2) - f(x_1)}$$  
.Update Interval: Mengevaluasi $f(x_3)$. Jika $f(x_1) \cdot f(x_3) < 0$, maka $x_2$ digantikan oleh $x_3$. Jika tidak, maka $x_1$ yang digantikan. 
.Kriteria Berhenti: Iterasi berhenti jika $|f(x_3)| < \text{Toleransi Error}$.  

## 3. Implementasi Kode (C++)
``` cpp
// Bagian inti algoritma Regula Falsi dalam program:
for (int i = 1; i <= max_iter; i++) {
    // Menghitung x3 berdasarkan kemiringan garis antara dua titik
    x3 = (x1 * f(x2, pilihan) - x2 * f(x1, pilihan)) / (f(x2, pilihan) - f(x1, pilihan));

    double fx3 = f(x3, pilihan);
    // Menampilkan progres setiap langkah perhitungan
    cout << setw(5) << i << fixed << setprecision(6) << setw(12) << x1 
         << setw(12) << x2 << setw(12) << x3 << setw(15) << fx3 << endl;

    if (abs(fx3) < error_tol) {
        cout << "AKAR DITEMUKAN: " << x3 << " pada iterasi ke-" << i << endl;
        break;
    }

    // Pemilihan sub-interval baru berdasarkan teorema antara
    if (f(x1, pilihan) * fx3 < 0) x2 = x3;
    else x1 = x3;
}
```

## 4. Analisis Output & Grafik
Berdasarkan hasil eksekusi program untuk Case 3:

Input: $x_1 = 0, x_2 = 1, \text{Error} = 0.00001$. 

Visualisasi Grafik: Grafik terminal menunjukkan kurva memotong sumbu Y=0 (garis |) di antara nilai $0.4$ dan $0.6$. Hal ini memberikan validasi visual awal sebelum perhitungan dilakukan.  Hasil Perhitungan: Akar ditemukan pada 0.495007 dalam 4 iterasi. 

Kesimpulan: Metode Regula Falsi terbukti sangat efisien untuk fungsi ini karena hanya memerlukan sedikit iterasi untuk mencapai presisi tinggi dibandingkan metode Bagi Dua (Bisection).  






# Laporan Praktikum Komputasi Numerik - #1

## 1. Pendahuluan

Pada materi Komputasi Numerik Pertemuan III, dibahas metode pencarian akar persamaan menggunakan Metode Terbuka, yaitu metode numerik yang tidak memerlukan interval pembatas akar seperti metode akolade. Nilai awal iterasi pada metode terbuka biasanya berupa satu atau dua tebakan awal, kemudian nilai tersebut diperbaiki terus-menerus hingga mendekati akar sebenarnya.

Berbeda dengan metode tertutup, metode terbuka memiliki kemungkinan:

Konvergen, yaitu hasil iterasi semakin mendekati akar sebenarnya
Divergen, yaitu hasil iterasi justru menjauh dari akar sebenarnya

Salah satu metode terbuka yang cukup populer adalah Metode Secant.

Metode Secant digunakan untuk mencari akar persamaan non-linier tanpa menggunakan turunan fungsi, sehingga menjadi alternatif dari metode Newton-Raphson yang membutuhkan turunan pertama.

## 2. Dasar Teori Metode Secant

Menurut materi perkuliahan, kelemahan metode Newton-Raphson adalah perlunya turunan fungsi yang kadang sulit dicari. Oleh karena itu, metode Secant menawarkan pendekatan lain, yaitu menggunakan beda hingga untuk mendekati gradien garis singgung.

Jika diketahui dua tebakan awal:

- $x_{i-1}$
- $x_i$

Maka akar berikutnya dihitung dengan rumus:

$$
x_{i+1} = x_i - \frac{f(x_i)(x_{i-1} - x_i)}{f(x_{i-1}) - f(x_i)}
$$

Rumus di atas berasal dari persamaan garis secant yang menghubungkan dua titik:

- $(x_{i-1}, f(x_{i-1}))$
- $(x_i, f(x_i))$

Lalu dicari titik potong garis tersebut terhadap sumbu-X.

---

## 3. Kelebihan Metode Secant

Berdasarkan materi PPT, metode **Secant** memiliki beberapa kelebihan:

- Tidak memerlukan turunan fungsi
- Lebih cepat dibanding metode Bisection jika konvergen
- Cocok untuk fungsi kompleks
- Iterasi relatif sedikit jika tebakan awal baik

---

## 4. Algoritma Program

Langkah program yang dibuat:

1. User memasukkan fungsi `f(x)`
2. User memasukkan dua tebakan awal `x0` dan `x1`
3. User memasukkan toleransi error
4. User memasukkan maksimum iterasi
5. Program menghitung akar baru `x2` dengan rumus Secant:

$$
x_2 = x_1 - \frac{f(x_1)(x_1 - x_0)}{f(x_1)-f(x_0)}
$$

6. Menghitung error:

$$
Error = |x_2 - x_1|
$$

7. Jika error lebih kecil dari toleransi, iterasi berhenti  
8. Jika belum, proses diulangi
---

## 5. Implementasi Program Python

```python
import math

print("====================================")
print("     KALKULATOR METODE SECANT")
print("====================================")

# Input data dari user
# Contoh fungsi:
# x**3 - x - 2
# math.exp(-x) - x
# math.sin(x) - 5*x + 2

fungsi = input("Masukkan fungsi f(x): ")

# Dua tebakan awal
x0 = float(input("Masukkan x0: "))
x1 = float(input("Masukkan x1: "))

# Toleransi error
tol = float(input("Masukkan toleransi: "))

# Maksimum iterasi
maks = int(input("Masukkan maksimum iterasi: "))

def f(x):
    return eval(fungsi)

print("\n-------------------------------------------------------------")
print("{:<5} {:<12} {:<12} {:<12} {:<12}".format(
    "Iter", "x0", "x1", "x2", "Error"))
print("-------------------------------------------------------------")

# Iterasi metode Secant

for i in range(1, maks + 1):

    fx0 = f(x0)
    fx1 = f(x1)

    # Cek pembagi nol
    if (fx1 - fx0) == 0:
        print("Pembagi nol!")
        break

    # Rumus Secant
    x2 = x1 - (fx1 * (x1 - x0)) / (fx1 - fx0)

    # Hitung error
    error = abs(x2 - x1)

    # Tampilkan iterasi
    print("{:<5} {:<12.6f} {:<12.6f} {:<12.6f} {:<12.6f}".format(
        i, x0, x1, x2, error))

    # Jika konvergen
    if error < tol:
        print("\nAkar ditemukan =", round(x2, 6))
        break

    # Update nilai
    x0 = x1
    x1 = x2

