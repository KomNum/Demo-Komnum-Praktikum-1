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

##2. Algoritma & Rumus Utama
Langkah-langkah yang diimplementasikan dalam kode program adalah:
`.Syarat Bolzano: Memastikan bahwa $f(x_1) \cdot f(x_2) < 0$, yang artinya terdapat perubahan tanda sehingga dipastikan ada akar di antara rentang tersebut. 
'.Rumus Regula Falsi: Menghitung nilai $x_3$ menggunakan interpolasi linier:$$x_3 = \frac{x_1 \cdot f(x_2) - x_2 \cdot f(x_1)}{f(x_2) - f(x_1)}$$  
.Update Interval: Mengevaluasi $f(x_3)$. Jika $f(x_1) \cdot f(x_3) < 0$, maka $x_2$ digantikan oleh $x_3$. Jika tidak, maka $x_1$ yang digantikan. 
'Kriteria Berhenti: Iterasi berhenti jika $|f(x_3)| < \text{Toleransi Error}$.  
