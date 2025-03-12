# <h1 align="center">Laporan Praktikum 02 <br> MODUL 3. FUNGSI</h1>
<p align="center">HARDIEK TATENDRAA-103112430005</p>

## Dasar Teori

Dalam pemrograman Go, fungsi adalah blok kode yang digunakan untuk melakukan tugas tertentu dan dapat dipanggil berulang kali. Penggunaan fungsi dalam suatu program bertujuan untuk meningkatkan modularitas, keterbacaan, dan efisiensi kode. Fungsi biasanya memiliki parameter dan mengembalikan nilai

## Unguided

### Soal 1

Minggu ini, mahasiswa Fakultas Informatika mendapatkan tugas dari mata kuliah matematika diskrit untuk mempelajari kombinasi dan permutasi. Jonas salah seorang mahasiswa, iseng untuk mengimplementasikannya ke dalam suatu program. Oleh karena itu bersediakah kalian membantu Jonas? (tidak tentunya ya :p) Masukan terdiri dari empat buah bilangan asli 𝑎, 𝑏, 𝑐, dan 𝑑 yang dipisahkan oleh spasi, dengan syarat 𝑎 ≥ 𝑐 dan 𝑏 ≥ 𝑑. Keluaran terdiri dari dua baris. Baris pertama adalah hasil permutasi dan kombinasi 𝒂 terhadap 𝑐, sedangkan baris kedua adalah hasil permutasi dan kombinasi 𝑏 terhadap 𝑑. Catatan: permutasi (P) dan kombinasi (C) dari 𝑛 terhadap 𝑟 (𝑛 ≥ 𝑟) dapat dihitung dengan menggunakan persamaan berikut!

```go
package main

  

import (

    "fmt"

)

  

func factorial(n int) int {

    if n == 0 || n == 1 {

        return 1

    }

    result := 1

    for i := 2; i <= n; i++ {

        result *= i

    }

    return result

}

  

func permutasi(n, r int) int {

    return factorial(n) / factorial(n-r)

}

  

func combination(n, r int) int {

    return factorial(n) / (factorial(r) * factorial(n-r))

}

  

func main() {

    var a, b, c, d int

    fmt.Scan(&a, &b, &c, &d)

  

    permutasi1 := permutasi(a, c)

    combinasi1 := combination(a, c)

    permutasi2 := permutasi(b, d)

    combinasi2 := combination(b, d)

  

    fmt.Println(permutasi1, combinasi1)

    fmt.Println(permutasi2, combinasi2)

}
```

> Output
> ![[soal1.png]]


Program diatas  bertujuan untuk menghitung permutasi dan kombinasi dengan inputan user. pertama kita mendefinisikan function factorial dengan parameter n dengan tipe data integer, kemudian function ini mengembalikan tipe data integer. Masuk ke if disini jika n = 1 atau n = 0 maka akan mengembalikan 1, sesuai dengan aturan faktorial 0! atau 1! sama dengan 1. Result result disini digunakan untuk menyimpan nilai dan disi nilai awal 1 , masuk ke loop disini loop dimulai dari 2 hingga n setiap literasi result akan dikali dengan i. Function permutasi disini memiliki parameter n dan r dengan tipe data integer, kemudian return disini function faktroial digunakan yg dimana factorial/ faktroial(n-r), sama halnya kombinasi hanya beda di return saja. Lanjut ke fungsi utama kita memiliki variable a b c dan d dengan tipe data int kemudian ada input untuk user nah kemudian kita bisa inialisasi lagi variabe permutasi1 ,permutasi 2, kombinasi1 dan kombinasi 2 yg dimana ini nantinya digunakan untuk mencari 2 permutasi dan 2 kombinasi ,kemudian yg terakhir ada print untuk menampilkan output

### Soal 2

Diberikan tiga buah fungsi matematika yaitu 𝑓 (𝑥) = 𝑥 2 , 𝑔 (𝑥) = 𝑥 − 2 dan ℎ (𝑥) = 𝑥 + 1. Fungsi komposisi (𝑓𝑜𝑔𝑜ℎ)(𝑥) artinya adalah 𝑓(𝑔(ℎ(𝑥))). Tuliskan 𝑓(𝑥), 𝑔(𝑥) dan ℎ(𝑥) dalam bentuk function. Masukan terdiri dari sebuah bilangan bulat 𝑎, 𝑏 dan 𝑐 yang dipisahkan oleh spasi. Keluaran terdiri dari tiga baris. Baris pertama adalah (𝑓𝑜𝑔𝑜ℎ)(𝑎), baris kedua (𝑔𝑜ℎ𝑜𝑓)(𝑏), dan baris ketiga adalah (ℎ𝑜𝑓𝑜𝑔)(𝑐)!


```go
package main

  

import "fmt"

  

func f(x int) int {

    return x * x

}

  

func g(x int) int {

    return x - 2

}

  

func h(x int) int {

    return x + 1

}

  

func fogoh(x int) int {

    return f(g(h(x)))

}

  

func gohof(x int) int {

    return g(h(f(x)))

}

  

func hofog(x int) int {

    return h(f(g(x)))

}

  

func main() {

    var x, y, z int

    fmt.Scan(&x, &y, &z)

  

    fmt.Println(fogoh(x))

    fmt.Println(gohof(y))

    fmt.Println(hofog(z))

}
```

> Output
> ![[soal2.png]]

Penjelasan code diatas, pertama kita punya 3 function f(x), g(x,) ,h(x)  dengan parameter x tipe data integer yang dimana mengembalikan nilai nah return ini kita bisa masukan ketiga rumus nya yg dimana f(x) = x^2, g(x) = x- 2, dan h(x) = x + 1. lanjut kita punya function fogoh mengembalikan nilai h(x) =x+1  kemudian ke g(h(x)) =(x + 1) - 2 = x - 1 dan terakhir f(g(h(x))) = (x - 1)², lanjut function gohof(x) yg dimana mengembalikan nilai return pertama f(x) = x²,  kemudian h(f(x)) = (x²) + 1 = x² + 1, dan terakhir g(h(f(x))) = (x² + 1) - 2 = x² - 1, lanjut function terakhir hofog(x) mengembalikan nilai g(x) = x - 2 kemudian (x - 2)², dan terakhir h(f(g(x))) = (x - 2)² + 1. Masuk ke fungsi utama atau main disini kita dekelrasikan variable x, y,z dengan tipe data integer yg digunakan untuk menampung inputan user, dan terakhir kita panggil function fogoh(x), gohof(x) dan hofog(x) untuk di print

### Soal 3

 Suatu lingkaran didefinisikan dengan koordinat titik pusat (𝑐𝑥, 𝑐𝑦) dengan radius 𝑟. Apabila diberikan dua buah lingkaran, maka tentukan posisi sebuah titik sembarang (𝑥, 𝑦) berdasarkan dua lingkaran tersebut. Masukan terdiri dari beberapa tiga baris. Baris pertama dan kedua adalah koordinat titik pusat dan radius dari lingkaran 1 dan lingkaran 2, sedangkan baris ketiga adalah koordinat titik sembarang. Asumsi sumbu x dan y dari semua titik dan juga radius direpresentasikan dengan bilangan bulat. Keluaran berupa string yang menyatakan posisi titik "Titik di dalam lingkaran 1 dan 2", "Titik di dalam lingkaran 1", "Titik di dalam lingkaran 2", atau "Titik di luar lingkaran 1 dan 2".

```go
package main

  

import (

    "fmt"

    "math"

)

  

func jarak(a, b, c, d float64) float64 {

    return math.Sqrt(math.Pow(a-c, 2) + math.Pow(b-d, 2))

}

  

func didalam(cx, cy, r, x, y float64) bool {

    return jarak(cx, cy, x, y) <= r

}

  

func main() {

    var cx1, cy1, r1 float64

    var cx2, cy2, r2 float64

    var x, y float64

  

    fmt.Scan(&cx1, &cy1, &r1)

    fmt.Scan(&cx2, &cy2, &r2)

    fmt.Scan(&x, &y)

  

    diDalam1 := didalam(cx1, cy1, r1, x, y)

    diDalam2 := didalam(cx2, cy2, r2, x, y)

  

    if diDalam1 && diDalam2 {

        fmt.Println("Titik di dalam lingkaran 1 dan 2")

    } else if diDalam1 {

        fmt.Println("Titik di dalam lingkaran 1")

    } else if diDalam2 {

        fmt.Println("Titik di dalam lingkaran 2")

    } else {

        fmt.Println("Titik di luar lingkaran 1 dan 2")

    }

}
```

> Output
> ![[soal3.png]]

Kode di atas digunakan untuk menentukan posisi sebuah titik terhadap dua lingkaran berdasarkan koordinat pusat dan radius masing-masing lingkaran. Fungsi jarak(a, b, c, d) digunakan untuk menghitung jarak antara dua titik dalam koordinat kartesian dengan rumus Euclidean distance, yaitu akar kuadrat dari jumlah kuadrat selisih masing-masing koordinat. Kemudian, fungsi didalam(cx, cy, r, x, y) digunakan untuk mengecek apakah titik (x, y) berada di dalam lingkaran yang memiliki pusat (cx, cy) dan radius r, dengan cara membandingkan jaraknya terhadap radius lingkaran.Pada fungsi main(), pertama-tama dideklarasikan variabel untuk menyimpan input koordinat pusat dan radius kedua lingkaran, serta titik yang akan diperiksa. Setelah membaca input dari pengguna, program memeriksa apakah titik tersebut berada di dalam lingkaran pertama, lingkaran kedua, atau keduanya menggunakan fungsi didalam(). Berdasarkan hasil pengecekan, program kemudian mencetak output yang menyatakan apakah titik berada di dalam lingkaran pertama dan kedua, hanya di lingkaran pertama, hanya di lingkaran kedua, atau di luar kedua lingkaran.


