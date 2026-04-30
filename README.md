# Demo-Komnum-Praktikum-1
|    NRP     |           Nama             |
| :--------: |       :------------:       |
| 5025251218 | Mushallina Dzikri Rozana   |
| xxxxxxxxxx | xxxxxxx                    |

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
