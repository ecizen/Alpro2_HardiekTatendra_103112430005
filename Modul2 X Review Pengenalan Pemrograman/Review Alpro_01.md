# <h1 align="center">Laporan Praktikum 02 <br> Review Pengenalan Pemograman</h1>
<p align="center">HARDIEK TATENDRAA-103112430005</p>

## Dasar Teori

Dasar teori  yang digunakan dalam praktikum ini, penggunaan variable, perhitungan matematis seperti penggunaan logika, dan struktur kontrol(if-else, for-loop while-loop, repeat-until ) dalam bahasa pemrograman Go.

## Unguided

### Soal 1

Telusuri program berikut dengan cara mengkompilasi dan mengeksekusi program. Silakan masukan data yang sesuai sebanyak yang diminta program. Perhatikan keluaran yang diperoleh. Coba terangkan apa sebenarnya yang dilakukan program tersebut?

```go
package main

import "fmt"

func main() {

    var (

    satu, dua, tiga string

    temp string

    )

        fmt.Print("Masukan input string: ")

        fmt.Scanln(&satu)

        fmt.Print("Masukan input string: ")

        fmt.Scanln(&dua)

        fmt.Print("Masukan input string: ")

        fmt.Scanln(&tiga)

        fmt.Println("Output awal = " + satu + " " + dua + " " + tiga)

        temp = satu

        satu = dua

        dua = tiga

        tiga = temp

        fmt.Println("Output akhir = " + satu + " " + dua + " " + tiga)

}
```

> Output
> ![[/output/outputsoal_1.png]]


Penjelasan code diatas kenapa output awal dan akhir beda, pertama kita review dari variable nya itu ada satu, dua , tiga dan temp. variable satu,dua dan tiga menerima input user sehinga ketika masuk ke print output satu + dua + tiga maka akan menghasilkan output yang urut sesuai inputanya sementara next baris disini ada perubahan nilai variable yang dimana temp disini mengambil inputan satu, satu = inputan dua , dua inputan 3 dan tiga di sini mengambil temp yang memiliki nilai dari inputan satu sehingga output akhir berbeda

### Soal 2

Tahun kabisat adalah tahun yang habis dibagi 400 atau habis dibagi 4 tetapi tidak habis dibagi 100. Buatlah sebuah program yang menerima input sebuah bilangan bulat dan memeriksa apakah bilangan tersebut merupakan tahun kabisat (true) atau bukan (false).

```go
package main

  
import "fmt"


func main() {

    var kabisat bool

    var tahun int


    fmt.Println("Masukkan tahun: ")

    fmt.Scan(&tahun)


    kabisat = tahun % 4 == 0 && tahun % 100 != 0 || tahun % 400 == 0


    fmt.Print(kabisat)

}
```

> Output
> ![[outputSoal_2.png]]

Code diatas adalah program cek apakah tahun tersebut kabisat atau bukan, kita bedah code nya nah disini saya mendekelrasikan variable dengan tipe data boolean agar nanti bisa menentukan nilai kebenaran apakah true yang artinya kabisat dan false bukan, kemudian variable tahun dengan tipe data integer yang dimana variable inilah yang nanti akan menamoung nilai dari inputan user. Masuk ke algoritma nya disini kita bisa lihat syarat dikatakan bahwa tahun tersebut kabisat yaitu tahun habis di bagi 4 dan tidak habis dibagi 100 nah kita coba bedah disini jadi misal tahun tersebut habis di bagi 4 dan habis dibagi 100 maka kondisi ini true atau  tahun mod 400 = 0 ini juga true.

### Soal 3

Buat program Bola yang menerima input jari-jari suatu bola (bilangan bulat). Tampilkan Volume dan Luas kulit bola. 𝑣𝑜𝑙𝑢𝑚𝑒𝑏𝑜𝑙𝑎 = 4 3 𝜋𝑟 3 dan 𝑙𝑢𝑎𝑠𝑏𝑜𝑙𝑎 = 4𝜋𝑟 2 (π ≈ 3.1415926535). (Contoh input/output, Teks bergaris bawah adalah input dari user):

```go
package main
  
import "fmt"


func main() {

    var (

        luasBola,

        volumeBola,

        r float64

        phi float64

    )


    fmt.Print("Masukkan jejari bola: ")

    fmt.Scan(&r)

  
    phi = 3.1415926535
    luasBola = 4 * phi * r * r
    volumeBola = 4.0 / 3.0 * phi * r * r * r
  

    fmt.Println("jari-jari bola:", r)

    fmt.Printf("Luas bola: %.4f\n", luasBola)

    fmt.Printf("Volume bola: %.4f\n", volumeBola)

  

}
```

> Output
> ![[outputSoal_3.png]]

Code diatas adalah code untuk mencari luas dan volume dimana program diatas memiliki 4 variable diantara nya luasBola, volumeBola yang dimana untuk inialisasi rumus nya , phi ini merupakan diameter nya dan ditetapkan nilai  3.1415926535, kemudian ada variable r untuk menerima input user nah kita masuk ke inialisasi nilai dimana phi tadi kita isi dengan 3,14 , kemudian luasBola, dan keliling bola kita masukan rumus yg sudah ada di soal, nah kenapa kita gunakan 4.0 dan 3.0 di rumus volume karena kita menggunakan tipe data float sehingga tidak ada pembulatan seperti tipe data integer sehingga hasilnya lebih akurat, terkhir output kita gunakan %.4f untuk menampilkan output hanya 4 angka dibelakang koma
### Soal 4

Dibaca nilai temperatur dalam derajat Celsius. Nyatakan temperatur tersebut dalam Fahrenheit 𝐶𝑒𝑙𝑠𝑖𝑢𝑠 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 − 32) × 5 9 𝑅𝑒𝑎𝑚𝑢𝑟 = 𝐶𝑒𝑙𝑐𝑖𝑢𝑠 × 4 5 𝐾𝑒𝑙𝑣𝑖𝑛 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 + 459.67) × 5 9 (Contoh input/output, Teks bergaris bawah adalah input dari user):

```go
package main

import "fmt"

func main() {

    var reamur, celcius,farenheit, kelvin float64

    fmt.Println("Masukkan suhu dalam celcius: ")

    fmt.Scan(&celcius)


    reamur = celcius * 4 / 5

    farenheit = celcius * 9 / 5 + 32

    kelvin = (farenheit + 459.67) * 5 / 9


    fmt.Println("Temperaturcelcius:", celcius)

    fmt.Println("Drajat reamur:", reamur)

    fmt.Println("Drajat farenheit:", farenheit)

    fmt.Printf("Drajat kelvin: %.0f", kelvin)
}
```

> Output
> ![[outputSoal_4.png]]

Code di atas adalah program untuk mengonversi suhu dari Celcius ke Reamur, Fahrenheit, dan Kelvin. Jadi, pertama kita deklarasikan beberapa variabel, yaitu reamur, celcius, kelvin, farenheit
dengan tipe data float, kemudian kita inialisasi variable reamur, farenheit dan kelvin sesuai rumusnya, kemudian kita print variable tersebut nah dibagian kelvin kita berikan batas dibelakang koma tidak ada angka karena di rumusnya ada tipe data float

### Soal 5

Dibaca nilai temperatur dalam derajat Celsius. Nyatakan temperatur tersebut dalam Fahrenheit 𝐶𝑒𝑙𝑠𝑖𝑢𝑠 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 − 32) × 5 9 𝑅𝑒𝑎𝑚𝑢𝑟 = 𝐶𝑒𝑙𝑐𝑖𝑢𝑠 × 4 5 𝐾𝑒𝑙𝑣𝑖𝑛 = (𝐹𝑎ℎ𝑟𝑒𝑛ℎ𝑒𝑖𝑡 + 459.67) × 5 9 (Contoh input/output, Teks bergaris bawah adalah input dari user):

```go
package main

import "fmt"

func main(){


    var c1, c2, c3, c4, c5 byte

    var b1, b2, b3 int

    fmt.Scan(&c1, &c2, &c3, &c4, &c5)

    fmt.Scanf("%c",&b1)

    fmt.Scanf("%c",&b2)

    fmt.Scanf("%cc",&b3)

  
    fmt.Printf("%c%c%c%c%c",c1, c2, c3, c4, c5)

    fmt.Printf("%c%c%c",b1+1, b2+1, b3+1)

}
```

> Output
> ![[outputSoal_5.png]]

Code diatas adalah program ascii yg dimana awalnya kita punya lima variabel `c1` sampai `c5` yang bertipe `byte`, terus ada `b1`, `b2`, `b3` yang pakai `int`. Nah, yang pertama dilakukan program ini itu baca lima karakter lewat `fmt.Scan()`, jadi misalnya kita masukin `hello`, masing-masing huruf bakal masuk ke variabel `c1` sampai `c5`. kemduain ada tiga `fmt.Scanf()` yang baca input lagi, tapi formatnya agak unik. Dua pertama pakai `"%c"`, artinya dia bakal baca satu karakter masing-masing buat `b1` dan `b2`. Terus ada `"%c"` buat `b3`

### Soal 6

Siswa kelas IPA di salah satu sekolah menengah atas di Indonesia sedang mengadakan praktikum kimia. Di setiap percobaan akan menggunakan 4 tabung reaksi, yang mana susunan warna cairan di setiap tabung akan menentukan hasil percobaan. Siswa diminta untuk mencatat hasil percobaan tersebut. Percobaan dikatakan berhasil apabila susunan warna zat cair pada gelas 1 hingga gelas 4 secara berturutan adalah ‘merah’, ‘kuning’, ‘hijau’, dan ‘ungu’ selama 5 kali percobaan berulang. Buatlah sebuah program yang menerima input berupa warna dari ke 4 gelas reaksi sebanyak 5 kali percobaan. Kemudian program akan menampilkan true apabila urutan warna sesuai dengan informasi yang diberikan pada paragraf sebelumnya, dan false untuk urutan warna lainnya.

```go
package main

import "fmt"

func main() {

    var warna1, warna2, warna3, warna4 string

    var berhasil bool = true

    i := 0  

    for i < 5 {

        fmt.Printf("Percobaan %d: ", i+1)

        fmt.Scan(&warna1, &warna2, &warna3, &warna4)

  

        if !(warna1 == "merah" && warna2 == "kuning" && warna3 == "hijau" && warna4 == "ungu") {

            berhasil = false

        }

        i++  

    }

    if berhasil {

        fmt.Println("BERHASIL: true")

    } else {

        fmt.Println("BERHASIL: false")

    }

}
```

> Output
> ![[outputSoal_6.png]]

Program diatas adalah program untuk mengecek apakah inputan sesuai dalam 5 kali percobaan jika iya true jika tidak false, program dimulai dari mendeklerasikan variable warna1-4 untuk inputan user nantinya kemudian mendeklerasikan variable berhasil dengan nilai awal true, next kita punya variable i untuk nilai awal 0 yg akan kita gunakan di perulangan nanti nah di for kita kasih kondisi jika i < 5 maka program akan terus dijalankan, masuk di blok for kita membuat inputan warna, selanjutnya ada if yg dimana if ini digunakan untuk mengecek jika warna nya tidak sesua maka berhasil akan false, selanjutnya i++ maka i tadi yg mulainya 0 akan terus bertambah sehingga mempeengaruhi perulangan sehinga misal i nya lebih dari 5 maka akan berhenti programnya, kemudian nilai hasil blok perulangan tadi kita terima di kondisi if berikutnya apakah false atau true

## Soal 7

Suatu pita (string) berisi kumpulan nama-nama bunga yang dipisahkan oleh spasi dan ‘– ‘, contoh pita diilustrasikan seperti berikut ini. Pita: mawar – melati – tulip – teratai – kamboja – anggrek Buatlah sebuah program yang menerima input sebuah bilangan bulat positif (dan tidak nol) N, kemudian program akan meminta input berupa nama bunga secara berulang sebanyak N kali dan nama tersebut disimpan ke dalam pita. (Petunjuk: gunakan operasi penggabungan string dengan operator “+” ). Tampilkan isi pita setelah proses input selesai.

```go
package main

import (

    "fmt"

)

func main() {

    var n int

    var pita string

    var bunga string

    count := 0


    fmt.Print("N: ")

    fmt.Scan(&n)

    if n <= 0 {

        fmt.Println("Pita:")

        fmt.Println("Bunga: 0")

        return

    }

  

    for i := 1; i <= n; i++ {

        fmt.Printf("Bunga %d: ", i)

        fmt.Scan(&bunga)

  

        if bunga == "SELESAI" {

            break

        }


        if pita == "" {

            pita = bunga

        } else {

            pita += " - " + bunga

        }

  

        count++

    }

    fmt.Println("Pita:", pita)

    fmt.Println("Bunga:", count)

}
```

> Output
> ![[outputSoal_7.png]]

Program di atas digunakan untuk menerima input jumlah bunga dari user, jika inputan `n` adalah 0 maka program langsung menampilkan pita kosong dan jumlah bunga 0. Program dimulai dengan mendeklarasikan variabel `n` untuk jumlah bunga, pita sebagai tempat menyimpan bunga dalam bentuk string, `bunga` untuk input user, dan `count` sebagai penghitung jumlah bunga.
Selanjutnya, program meminta input `n`. Jika `n <= 0`, program langsung menampilkan hasil kosong dan selesai. Jika `n > 0`, program masuk ke perulangan `for` yang berjalan `n` kali untuk meminta input bunga. Jika user mengetik `"SELESAI"`, program langsung berhenti lebih awal.
Setiap bunga yang valid akan ditambahkan ke dalam `pita`, jika `pita` masih kosong maka langsung diisi, jika tidak maka ditambahkan dengan pemisah `" - "`. Setelah perulangan selesai, program menampilkan hasil akhir berupa pita berisi bunga yang telah dimasukkan dan jumlah bunga yang berhasil ditambahkan sebelum `"SELESAI"` atau batas `n` tercapai.


## Soal 8

Setiap hari Pak Andi membawa banyak barang belanjaan dari pasar dengan mengendarai sepeda motor. Barang belanjaan tersebut dibawa dalam kantong terpal di kiri-kanan motor. Sepeda motor tidak akan oleng jika selisih berat barang di kedua kantong sisi tidak lebih dari 9 kg. Buatlah program Pak Andi yang menerima input dua buah bilangan real positif yang menyatakan berat total masing-masing isi kantong terpal. Program akan terus meminta input bilangan tersebut hingga salah satu kantong terpal berisi 9 kg atau lebih. program akan menampilkan true jika selisih kedua isi kantong lebih dari atau sama dengan 9 kg. Program berhenti memproses apabila total berat isi kedua kantong melebihi 150 kg atau salah satu kantong beratnya negatif.

```go
package main

  

import "fmt"

  

func main() {

    var kantongKanan, kantongKiri, totalBerat float64

  

    for {

        fmt.Print("Masukan berat belanjaan di kedua kantong: ")

        fmt.Scan(&kantongKanan, &kantongKiri)

        totalBerat += kantongKanan + kantongKiri

  

        var selisih float64

        if kantongKanan > kantongKiri {

            selisih = kantongKanan - kantongKiri

        } else {

            selisih = kantongKiri - kantongKanan

        }

  

        if selisih > 9 {

            fmt.Println("Sepeda motor pak Andi akan oleng: true")

        } else {

            fmt.Println("Sepeda motor pak Andi akan oleng: false")

        }

  

        if totalBerat >= 150 {

            fmt.Println("Proses selesai.")

            break

        }

    }

}
```

> Output
> ![[outputSoal_8.png]]

Program diatas digunakan untuk cek apakah pak akan oleng atau tidak , pertama saya mendeklerasikan variable '**kantongKanan**' , '**kantongKiri**' untuk menampung inputan **user** **totalBerat**' untuk menghitung berat ,kemudian masuk ke for tanpa kondisi jadi disini kita melakukan aksi yg dimana user menginputkan kantong kanan dan kiri, kemudian inputan user tadi akan melakukan operasi disini  **totalBerat = totalBerat + kantongKanan + kantongKiri**, yang bakal digunakan nanti untuk menghitung totalBerat, selanjutnya kita saya dekelrasikan selisih , masuk ke if  dengan kondisi kantong kanan > kantong kiri selisihnya  = kantong kanan - kantong kiri dan else nya itu sebaliknya, kemudian saya buat if untuk menentukan nilai selsih apakah salah satu kantong lebih dari 9kg kalau iya berarti true kalau tidak false. Masuk ke code terakhir kita panggil totalBerat tadi apakah lebih dari 150kg jika ya maka program akan berhenti

## Soal 9

√2 merupakan bilangan irasional. Meskipun demikian, nilai tersebut dapat dihampiri dengan rumus berikut: √2 = ∏ (4𝑘 + 2) 2 (4𝑘 + 1)(4𝑘 + 3) ∞ 𝑘=0 Modifikasi program sebelumnya yang menerima input integer 𝐾 dan menghitung √2 untuk 𝐾 tersebut. Hampiran √2 dituliskan dalam ketelitian 10 angka di belakang koma. Perhatikan contoh sesi interaksi program seperti di bawah ini (teks bergaris bawah

```go
package main

  

import (

    "fmt"

    "math"

)

  

func main() {

    var k int

  

    fmt.Print("Nilai K = ")

    fmt.Scan(&k)

  

    result := 1.0

  

    for i := 0; i <= k; i++ {

        numerator := math.Pow(float64(4*i+2), 2)

        denominator := float64((4*i + 1) * (4*i + 3))

        result *= numerator / denominator

    }

  

    fmt.Printf("Nilai akar 2 = %.10f\n", result)

}
```

> Output
> ![[outputSoal_9_new.png]]

Program di atas digunakan untuk menghitung nilai aproksimasi akar 2 menggunakan metode deret tak hingga. Pertama, saya deklarasikan variabel K, yang nantinya bakal menampung inputan user sebagai jumlah iterasi atau banyaknya perhitungan dalam deret. Setelah itu, saya inisialisasi result dengan nilai 1.0, karena nanti bakal dikalikan dalam perhitungan.Masuk ke looping for, di sini saya pakai variabel k yang jalan dari 0 sampai kurang dari K. Nah, di setiap iterasi, saya hitung nilai n yang rumusnya 4k + 2, lalu d yang merupakan hasil kali dari (4k + 1) dan (4k + 3). Kedua nilai ini kemudian digunakan untuk memperbarui result, di mana setiap iterasi result bakal dikalikan dengan (n * n) / d.

## Soal 10

PT POS membutuhkan aplikasi perhitungan biaya kirim berdasarkan berat parsel. Maka, buatlah program BiayaPos untuk menghitung biaya pengiriman tersebut dengan ketentuan sebagai berikut! Dari berat parsel (dalam gram), harus dihitung total berat dalam kg dan sisanya (dalam gram). Biaya jasa pengiriman adalah Rp. 10.000,- per kg. Jika sisa berat tidak kurang dari 500 gram, maka tambahan biaya kirim hanya Rp. 5,- per gram saja. Tetapi jika kurang dari 500 gram, maka tambahan biaya akan dibebankan sebesar Rp. 15,- per gram. Sisa berat (yang kurang dari 1kg) digratiskan biayanya apabila total berat ternyata lebih dari 10kg.

```go
package main

  

import "fmt"

  

func main() {

    var beratGram, beratKg, totalBiaya int

  

    fmt.Scan(&beratGram)

    beratKg = beratGram / 1000

    beratGram = beratGram % 1000

    totalBiayaSementara := beratKg * 10000


    if beratKg >= 10 {

        totalBiaya = totalBiayaSementara

    } else {

        if beratGram >= 500 {

            totalBiaya = totalBiayaSementara + (beratGram * 5)

        } else {

            totalBiaya = totalBiayaSementara + (beratGram * 15)

        }

    }

  

    fmt.Println("Berat parsel (gram):", beratGram)

    fmt.Println("Detail Berat: ", beratKg, "+", beratGram)

    fmt.Println("Total biaya: ", totalBiaya)

}
```

> Output
> ![[outputSoal_10.png]]

Program di atas digunakan untuk menghitung totalBiaya, program dimulai dari mendeklerasikan variable  kemudian masuk ke input user dalam gram ,  beratKg kita bagi dengan 1000 yang dimana nanti hasilnya dikali 10.000, kemudian gram kita mod untuk mendapat sisa gram nya, kemudian kita masuk logika if  dimana program bakal cek dulu apakah berat dalam kg melebihi 10kg kalau iya tidak ada biaya tambahan, jika kurang maka akan menjalankan blok kode else nah di else terdapat if jika berat gram lebih besar sama dengan 500 maka akan ada tambahan 5 rupiah per gram nya jika tidak terpenuhi atau gram kurang dari 500 maka biaya tambahanya 15 rupiah.

## Soal 11

PT POS membutuhkan aplikasi perhitungan biaya kirim berdasarkan berat parsel. Maka, buatlah program BiayaPos untuk menghitung biaya pengiriman tersebut dengan ketentuan sebagai berikut! Dari berat parsel (dalam gram), harus dihitung total berat dalam kg dan sisanya (dalam gram). Biaya jasa pengiriman adalah Rp. 10.000,- per kg. Jika sisa berat tidak kurang dari 500 gram, maka tambahan biaya kirim hanya Rp. 5,- per gram saja. Tetapi jika kurang dari 500 gram, maka tambahan biaya akan dibebankan sebesar Rp. 15,- per gram. Sisa berat (yang kurang dari 1kg) digratiskan biayanya apabila total berat ternyata lebih dari 10kg.

```go
package main


import "fmt"

func main() {

    var nam float64

    var nmk string


    fmt.Print("Nilai akhir mata kuliah: ")

    fmt.Scanln(&nam)


    if nam > 80 {

        nmk = "A"

    }

    if nam > 72.5 && nam <= 80 {

        nmk = "AB"

    }

    if nam > 65 && nam <= 72.5 {

        nmk = "B"

    }

    if nam > 57.5 && nam <= 65 {

        nmk = "BC"

    }

    if nam > 50 && nam <= 57.5 {

        nmk = "C"

    }

    if nam > 40 && nam <= 50 {

        nmk = "D"

    }

    if nam <= 40 {

        nmk = "E"

    }

    fmt.Println("Nilai mata kuliah:", nmk)

}
```

> Output
> ![[outputSoal_11.png]]

A. Harusnya program diatas mengeluarkan output 80.1 itu adalah a karena disini program dari study case menggunakan if saja disini membuatnya ambigu jadi progam membaca if terakhir yg terpenhui kenpapa tidak e karena kondisi e itu kurang dari sedangkan kalau kita lihat d saja d > 40 jadi terpenuhi begitu pula dengan kode lainya setelha kode saya perbaiki baru betul output nya.
B. Kesalahan program nya itu kita lihat paling simpel disitu output nya untuk predikat mengunakan nam yg jelas jelas float sedangakan nam di if tersebut dipaksa menmpung nam = "predikat" atau string, kesalahan kedua yaitu if nya terlalu ambigu seharusnya kita perlu kasih kondisi batasan masing masing yg sesuai
C. Dengan menambah logika dan jadi ada batas atas dan bawah sehingga kondisinya tidak ambigu karena program cek kedua kondisi haru terpenuhi agar blok if dapat di eksekusi


## Soal 12

Sebuah bilangan bulat b memiliki faktor bilangan f > 0 jika f habis membagi b. Contoh: 2 merupakan faktor dari bilangan 6 karena 6 habis dibagi 2. Buatlah program yang menerima input sebuah bilangan bulat b dan b > 1. Program harus dapat mencari dan menampilkan semua faktor dari bilangan tersebut!

```go
package main

  

import "fmt"

  

func main() {

    var b int

    fmt.Print("Bilangan: ")

    fmt.Scan(&b)

  

    fmt.Print("Faktor: ")

    count := 0

    for i := 1; i <= b; i++ {

        if b%i == 0 {

            fmt.Print(i, " ")

            count++

        }

    }

    fmt.Println()

  

    tesPrima := count == 2

    fmt.Println("Prima:", tesPrima)

}
```

> Output
> ![[outputSoal_12.png]]

Program di atas digunakan untuk mencari faktor dari sebuah bilangan dan menentukan apakah bilangan tersebut adalah bilangan prima. Program dimulai dengan mendeklarasikan variabel b untuk menyimpan input bilangan dari pengguna. Setelah itu, program masuk ke proses perulangan menggunakan for, di mana i akan berjalan dari 1 hingga b.Di dalam perulangan, terdapat percabangan if yang mengecek apakah b habis dibagi i. Jika iya, maka i akan dicetak sebagai faktor dan nilai count akan bertambah satu untuk menghitung jumlah faktor yang ditemukan. Setelah proses perulangan selesai, program masuk ke logika pengecekan bilangan prima.Di bagian ini, program mengecek apakah jumlah faktor yang ditemukan (count) adalah 2. Jika iya, maka bilangan tersebut dianggap sebagai bilangan prima dan variabel isPrima diatur ke true. Jika tidak, maka bilangan tersebut bukan prima. Terakhir, program mencetak hasil pengecekan bilangan prima berdasarkan nilai isPrima.


