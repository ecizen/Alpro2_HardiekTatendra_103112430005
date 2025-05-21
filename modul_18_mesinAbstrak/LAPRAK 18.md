# <h1 align="center">Laporan Praktikum 18 <br> MODUL 17. MESIN ABSTRAK </h1>
<p align="center">HARDIEK TATENDRA-103112430005</p>

## Dasar Teori

Mesin abstrak adalah model komputasi yang dirancang di atas model mesin komputasi yang telah ada, yaitu tipe data dan operasi-operasi dasarnya dibuat menggunakan tipe data dan operasi-operasi yang tersedia di mesin di bawahnya. Teknik ini merupakan salah satu cara untuk membangun perangkat lunak.
## Unguided

### Soal 1

Implementasi operasi dasar mesin domino sebagai sebuah subprogram: a) Buat tipe data kartu domino (Domino) yang menyimpan informasi ➢ gambar (suit) kedua sisi kartu ➢ nilai kartu ➢ Boolean data yang menyatakan kartu ini balak atau bukan ➢ Buat tipe data satu set kartu domino (Dominoes) ➢ Array menyimpan 28 kartu Domino ➢ Jumlah kartu tersisa dalam array tersebut b) prosedur kocokKartu(Dominoes) c) fungsi ambilKartu(Dominoes) → Domino d) fungsi gambarKartu(Domino,suit int) → int e) fungsi nilaiKartu(Domino) → int

```go

  

type Domino struct {

    side1   int

    side2   int

    isBalak bool

}

  

type Dominoes struct {

    cards [28]Domino

    count int

}
  

func inisialisasiKartu(D *Dominoes) {

    idx := 0

    for i := 0; i <= 6; i++ {

        for j := i; j <= 6; j++ {

            D.cards[idx] = Domino{

                side1:   i,

                side2:   j,

                isBalak: i == j,

            }

            idx++

        }

    }

    D.count = 28

}

  

func kocokKartu(D *Dominoes) {

    var i, j int

    var temp Domino

  

    for i = 0; i < 28; i++ {

        j = rand.Intn(28)

        temp = D.cards[i]

        D.cards[i] = D.cards[j]

        D.cards[j] = temp

    }

}

  

func ambilKartu(D *Dominoes) Domino {

    var ambil Domino

    if D.count > 0 {

        ambil = D.cards[D.count-1]

        D.count--

    }

    return ambil

}

  

func gambarKartu(D Domino, suit int) int {

    var gambar int

    if D.side1 == suit {

        gambar = D.side2

    } else if D.side2 == suit {

        gambar = D.side1

    } else {

        gambar = -1

    }

    return gambar

}

func nilaiKartu(D Domino) int {

    var nilai int

    nilai = D.side1 + D.side2

    return nilai

}
```

> Output
> ![[modul_18_mesinAbstrak/output/soal1.png]]

Pertama tama-tama saya buat tipe data record dengen record dimana struk pertama domino yg menyimpan side1, side 2 dan is balak, selanjutnya tipe bentukan dominoes dimana menyimpan cards dengan tipe data domino dengan panjang array 28 sesuai jumlah kartu domino. Masuk ke sub program: 
	-Pertama yaitu procdeure kocokKartu dimana memiliki parameter D dengan pointer tipe data Dominoes, dimana di procedure ini memiliki variable i, j sebagai integer dan variable temp dgn tipe data domino lanjut saya punya perulangan dimana i = 0 ; i< 28 artinya perulangan dilakukan sebanyak 28 kali sesuai dgn jumlah array nya, lanjut j kita inisailisasi dgn random karena agar kocokan kartu berbeda beda, lalu saya punya D.cards[j] = temp yg artinya menukar isi
	-Kedua fungsi ambilKartu degn parameter sama namun mengembalikan Domino lanjut difungsi ini saya punya variable ambil dgn tipe data domino, lanjut ke percabangan if saya cek d.count > 0 artinya apakah masih ada kartu nya kalu iya maka ambil kartu array paling  kiri lalu   D.count-- kita kurangi yg artinya kartu diambil sisa 27 jika 28 diambil 1 
	-Fungsi gambarKartu memiliki parameter D bertipe Domino dan suit bertipe int, lalu mengembalikan nilai bertipe int. Di dalam fungsi ini, saya mendeklarasikan variabel gambardengan tipe data int untuk menyimpan hasil sementara. Selanjutnya, saya menggunakan percabangan if untuk memeriksa apakah salah satu sisi kartu D (yaitu side1 atau side2) memiliki nilai yang sama dengan suit. Jika side1 sama dengan suit, maka variabel gambar diisi dengan nilai dari sisi lainnya, yaitu side2. Sebaliknya, jika side2 yang cocok dengan suit, maka gambar diisi dengan side1. Tapi jika tidak ada sisi kartu yang cocok dengan suit, berarti kartu tersebut tidak bisa digunakan dalam konteks ini, sehingga saya isi gambar = -1 sebagai penanda bahwa tidak cocok. Terakhir, nilai `gambar` dikembalikan sebagai hasil dari fungsi ini.
	-ungsi nilaiKartu memiliki parameter D dengan tipe data Domino dan mengembalikan sebuah nilai bertipe int. Di dalam fungsi ini, saya membuat variabel `nilai` bertipe `int` untuk menampung hasil penjumlahan. Selanjutnya, saya jumlahkan kedua sisi dari kartu domino yaitu D.side1 dan D.side2, lalu hasilnya saya simpan ke dalam variabel nilai. Fungsi ini berguna untuk menghitung total nilai dari sebuah kartu domino, misalnya [3|5] akan menghasilkan nilai 8.

### Soal 2
Realisasi aksi berikut menggunakan operasi-operasi dasar mesin domino: a) prosedur galiKartu(Dominoes,Domino) yang mengambil kartu dari tumpukan sampai diperoleh kartu dengan gambar (suit) yang sama dengan kartu yang diberikan fungsi sepasangKartu(Domino,Domino) → boolean; yang memberikan nilai true jika total nilai kartu adalah 12 dan false jika tidak.

```go
package main

  

import (

    "fmt"

    "math/rand"

    "time"

)

  

type Domino struct {

    side1   int

    side2   int

    isBalak bool

}

  

type Dominoes struct {

    cards [28]Domino

    count int

}

  

func inisialisasiKartu(D *Dominoes) {

    idx := 0

    for i := 0; i <= 6; i++ {

        for j := i; j <= 6; j++ {

            D.cards[idx] = Domino{

                side1:   i,

                side2:   j,

                isBalak: i == j,

            }

            idx++

        }

    }

    D.count = 28

}

  

func kocokKartu(D *Dominoes) {

    for i := 0; i < 28; i++ {

        j := rand.Intn(28)

        D.cards[i], D.cards[j] = D.cards[j], D.cards[i]

    }

}

  

func ambilKartu(D *Dominoes) Domino {

    if D.count > 0 {

        D.count--

        return D.cards[D.count]

    }

    return Domino{}

}

  

func nilaiKartu(D Domino) int {

    return D.side1 + D.side2

}

  

func galiKartu(D *Dominoes, refCard Domino) Domino {

    var d Domino

    for D.count > 0 {

        d = ambilKartu(D)


        if d.side1 == refCard.side1 || d.side1 == refCard.side2 ||

            d.side2 == refCard.side1 || d.side2 == refCard.side2 {

            return d

        }

    }

    return Domino{}

}

  

func sepasangKartu(A, B Domino) bool {

    return nilaiKartu(A)+nilaiKartu(B) == 12

}

  

func main() {

    rand.Seed(time.Now().UnixNano())

  

    var deck Dominoes

    inisialisasiKartu(&deck)

    kocokKartu(&deck)

  

    refCard := ambilKartu(&deck)

    fmt.Printf("Kartu Referensi: [%d|%d]\n", refCard.side1, refCard.side2)

  

    cocok := galiKartu(&deck, refCard)

    if cocok.side1 != 0 || cocok.side2 != 0 {

        fmt.Printf("Kartu hasil gali: [%d|%d] cocok dengan kartu referensi\n", cocok.side1, cocok.side2)

    } else {

        fmt.Println("Tidak ditemukan kartu yang cocok.")

    }

  

    if sepasangKartu(refCard, cocok) {

        fmt.Println("Kedua kartu membentuk sepasang (total = 12)")

    } else {

        fmt.Println("Kedua kartu tidak membentuk sepasang (total ≠ 12)")

    }

}
```

> Output
> ![[modul_18_mesinAbstrak/output/soal2.png]]

 langsugn masuk ke Prosedur galiKartu memiliki parameter D bertipe pointer ke Dominoes dan refCard bertipe Domino**, lalu mengembalikan sebuah nilai bertipe Domino. Di dalam prosedur ini, saya mendeklarasikan variabel d bertipe Domino yang akan digunakan untuk menyimpan kartu yang diambil dari tumpukan. Selanjutnya, saya menggunakan perulangan while bergaya Go yaitu dengan for yang berjalan selama jumlah kartu dalam tumpukan D.count masih lebih dari 0. Dalam setiap iterasi, saya mengambil satu kartu dari tumpukan menggunakan fungsi ambilKartu, lalu saya periksa apakah salah satu sisi dari kartu yang diambil side1 atau side2 **cocok** dengan salah satu sisi dari kartu referensi refCard. Jika ada kecocokan di salah satu sisi, maka kartu tersebut dianggap cocok dan langsung dikembalikan sebagai hasil dari prosedur ini. Jika tidak ada kartu yang cocok hingga tumpukan habis, maka prosedur akan mengembalikan kartu kosong (Domino{}) sebagai penanda bahwa tidak ditemukan kartu yang sesuai dengan referensi. Fungsi sepasangKartu memiliki dua parameter, yaitu A dan B, yang keduanya bertipe Domino, dan mengembalikan nilai bertipe boolean. Di dalam fungsi ini, saya tidak mendeklarasikan variabel tambahan karena perhitungannya cukup langsung. Saya menggunakan fungsi nilaiKartu untuk menjumlahkan nilai dari masing-masing kartu yaitu side1 + side2 dari A dan B, lalu saya jumlahkan kedua hasil tersebut. Jika total nilai dari kedua kartu sama dengan 12, maka fungsi ini akan mengembalikan nilai true, menandakan bahwa kartu A dan B membentuk sepasang. Sebaliknya, jika hasil penjumlahan tidak sama dengan 12, maka fungsi akan mengembalikan false.
### Soal 3
Implementasi salah satu permainan domino. Lihat lampiran untuk deskripsi permainan Gapleh.

```go
package main

  

import (

    "fmt"

    "math/rand"

)

  

type Domino struct {

    side1   int

    side2   int

    isBalak bool

}

  

type Dominoes struct {

    cards [28]Domino

    count int

}

  

type Pemain struct {

    kartu []Domino

}

  

var meja []Domino

  

func inisialisasiKartu(D *Dominoes) {

    idx := 0

    for i := 0; i <= 6; i++ {

        for j := i; j <= 6; j++ {

            D.cards[idx] = Domino{

                side1:   i,

                side2:   j,

                isBalak: i == j,

            }

            idx++

        }

    }

    D.count = 28

}

  

func kocokKartu(D *Dominoes) {

    var i, j int

    var temp Domino

  

    for i = 0; i < 28; i++ {

        j = rand.Intn(28)

        temp = D.cards[i]

        D.cards[i] = D.cards[j]

        D.cards[j] = temp

    }

}

  

func ambilKartu(D *Dominoes) Domino {

    var ambil Domino

    if D.count > 0 {

        ambil = D.cards[D.count-1]

        D.count--

    }

    return ambil

}

  

func gambarKartu(D Domino, suit int) int {

    var gambar int

    if D.side1 == suit {

        gambar = D.side2

    } else if D.side2 == suit {

        gambar = D.side1

    } else {

        gambar = -1

    }

    return gambar

}

func nilaiKartu(D Domino) int {

    var nilai int

    nilai = D.side1 + D.side2

    return nilai

}

  

func galiKartu(D *Dominoes, refCard Domino) {

    var found bool

    var d Domino

    found = false

    for (D.count > 0) && (found == false) {

        d = ambilKartu(D)

        if (d.side1 == refCard.side1) || (d.side1 == refCard.side2) ||

            (d.side2 == refCard.side1) || (d.side2 == refCard.side2) {

            found = true

        }

    }

}

  

func sepasangKartu(A, B Domino) bool {

    return (nilaiKartu(A) + nilaiKartu(B)) == 12

}

  

func bagiKartu(D *Dominoes, jumlahPemain int) []Pemain {

    pemain := make([]Pemain, jumlahPemain)

    for i := 0; i < 7; i++ {

        for j := 0; j < jumlahPemain; j++ {

            pemain[j].kartu = append(pemain[j].kartu, ambilKartu(D))

        }

    }

    return pemain

}

  

func cekSisiKartu(kartu Domino, ujungKiri int, ujungKanang int) bool {

    return (kartu.side1 == ujungKiri || kartu.side2 == ujungKiri) || (kartu.side1 == ujungKanang || kartu.side2 == ujungKanang)

}

  

func mainkanKartu(meja *[]Domino, kartu Domino, keKanan bool) {

    if keKanan {

        *meja = append(*meja, kartu)

    } else {

        *meja = append([]Domino{kartu}, *meja...)

    }

}

func main() {

    var deck Dominoes

    inisialisasiKartu(&deck)

    kocokKartu(&deck)

    pemain := bagiKartu(&deck, 2)

    var ujungKiri, ujungKanan int

  

    var meja []Domino

  

    kartuAwal := pemain[0].kartu[0]

  

    meja = append(meja, kartuAwal)

    pemain[0].kartu = pemain[0].kartu[1:]

  

    giliran := 1

    drawCount := 0

  

    for {

        ujungKiri = meja[0].side1

        ujungKanan = meja[len(meja)-1].side2

  

        fmt.Println("========== GILIRAN ==========")

        fmt.Println("Giliran Pemain", giliran)

        fmt.Print("Meja: ")

        for _, d := range meja {

            fmt.Printf("[%d|%d] ", d.side1, d.side2)

        }

        fmt.Println()

        fmt.Println("Pemain", giliran, "memegang", len(pemain[giliran].kartu), "kartu")

  

        berhasilMain := false

        for i, kartu := range pemain[giliran].kartu {

            if cekSisiKartu(kartu, ujungKiri, ujungKanan) {

                if kartu.side1 == ujungKanan || kartu.side2 == ujungKanan {

                    mainkanKartu(&meja, kartu, true)

                } else {

                    mainkanKartu(&meja, kartu, false)

                }

                pemain[giliran].kartu = append(pemain[giliran].kartu[:i], pemain[giliran].kartu[i+1:]...)

                berhasilMain = true

                break

            }

        }

  

        if !berhasilMain {

            if deck.count > 0 {

                dapat := ambilKartu(&deck)

                pemain[giliran].kartu = append(pemain[giliran].kartu, dapat)

            } else {

                fmt.Println("Pemain", giliran, "tidak bisa jalan.")

                drawCount++

            }

        } else {

            drawCount = 0

        }

  

        if len(pemain[giliran].kartu) == 0 {

            fmt.Println("Pemain", giliran, "MENANG!")

            break

        }

  

        if drawCount >= 2 {

            fmt.Println("Permainan berakhir imbang, tidak ada pemain yang bisa jalan.")

            totalPoinP0 := 0

            totalPoinP1 := 0

            for _, k := range pemain[0].kartu {

                totalPoinP0 += nilaiKartu(k)

            }

            for _, k := range pemain[1].kartu {

                totalPoinP1 += nilaiKartu(k)

            }

            fmt.Println("Pemain 0:", totalPoinP0)

            fmt.Println("Pemain 1:", totalPoinP1)

            if totalPoinP0 < totalPoinP1 {

                fmt.Println("Pemain 0 menang berdasarkan nilai kartu terkecil:", totalPoinP0)

            } else if totalPoinP1 < totalPoinP0 {

                fmt.Println("Pemain 1 menang berdasarkan nilai kartu terkecil:", totalPoinP1)

            } else {

                fmt.Println("Seri, kedua pemain memiliki nilai kartu sama:", totalPoinP0)

            }

            break

        }

        giliran = (giliran + 1) % 2

    }

}
```

> Output
> ![[modul_18_mesinAbstrak/output/soal3.png]]

program diatas adalah permainan gapleh mungkin subprogram seperti kocokKartu ambilKartu, gambarKartu nilaiKartu tidak saya jelaskan karena mirip dgn no 1 tinggal implementasi lalu gali kartu dan spasang kartu sama no 2. Lanjut saja masuk ke Fungsi bagiKartu memiliki parameter D bertipe pointer ke Dominoes dan jumlahPemain bertipe int. Di dalam fungsi ini saya mendeklarasikan variabel pemain sebagai slice bertipe Pemain dengan panjang sesuai jumlahPemain. Selanjutnya saya menggunakan nested loop, dimana loop pertama i dari 0 sampai 6, yang artinya setiap pemain akan mendapatkan 7 kartu. Di dalam loop kedua j dari 0 sampai jumlahPemain-1, setiap pemain akan mengambil satu kartu dari deck dengan memanggil fungsi ambilKartu(D) dan kartu tersebut ditambahkan ke slice kartu milik pemain tersebut menggunakan fungsi append. Setelah semua kartu dibagikan, fungsi mengembalikan slice pemain yang berisi data kartu masing-masing pemain. fungsi cekSisiKartu yang memiliki parameter kartu bertipe Domino, ujungKiri dan ujungKanang bertipe int. Di dalam fungsi ini saya menggunakan satu pernyataan return yang langsung memeriksa apakah side1 atau side2 dari kartu sama dengan ujungKiri atau ujungKanang. Jika salah satu kondisi benar maka fungsi akan mengembalikan nilai true yang menandakan kartu dapat dimainkan. Jika tidak ada yang cocok maka fungsi mengembalikan false.Untuk fungsi **mainkanKartu** yang memiliki parameter meja bertipe pointer ke slice Domino, kartu bertipe Domino, dan keKanan bertipe boolean. Di dalam fungsi ini saya menggunakan percabangan if untuk menentukan posisi penambahan kartu ke meja. Jika keKanan bernilai true maka saya menambahkan kartu ke ujung kanan meja dengan menggunakan fungsi append biasa. Namun jika keKanan false maka saya menambahkan kartu ke ujung kiri meja dengan cara membuat slice baru yang berisi kartu lalu menggabungkannya dengan isi meja saat ini menggunakan append. Dengan cara ini kartu akan berada di posisi paling depan meja.Pertama saya mendeklarasikan variabel deck dengan tipe data Dominoes. Lalu saya panggil fungsi inisialisasiKartu dengan parameter alamat dari deck untuk membuat set kartu domino lengkap dari [0|0] sampai [6|6]. Setelah itu saya panggil fungsi kocokKartu dengan parameter alamat deck agar kartu-kartu dalam deck diacak urutannya.Selanjutnya saya panggil fungsi bagiKartu dengan parameter alamat deck dan jumlah pemain 2, hasilnya saya simpan ke variabel pemain yang berisi potongan kartu untuk masing-masing pemain.Saya deklarasikan variabel ujungKiri dan ujungKanan bertipe integer untuk menampung nilai ujung kiri dan kanan dari deretan kartu di meja.Kemudian saya buat variabel meja berupa slice dari Domino yang kosong, sebagai tempat kartu dimainkan.Saya ambil kartu pertama dari tangan pemain 0, lalu saya masukkan kartu tersebut ke meja menggunakan append. Setelah itu kartu pertama pemain 0 saya hapus dari tangan dia dengan mengambil slice dari index ke-1 sampai akhir. Saya buat variabel giliran yang diinisialisasi dengan nilai 1, menandakan giliran pemain ke-1 yang akan bermain selanjutnya. Variabel drawCount saya buat dan inisialisasi 0, untuk menghitung berapa kali pemain gagal main kartu.Selanjutnya saya buat loop for tanpa kondisi, yang artinya loop ini berjalan terus sampai ada perintah break.Di dalam loop saya isi ujungKiri dengan nilai side1 dari kartu pertama di meja, dan ujungKanan dengan nilai side2 dari kartu terakhir di meja.Lalu saya tampilkan informasi giliran pemain, isi meja dalam bentuk kartu yang dimainkan, dan jumlah kartu yang dimiliki pemain yang sedang giliran.Saya buat variabel berhasilMain bertipe boolean dan inisialisasi dengan false. Variabel ini digunakan untuk menandai apakah pemain berhasil main kartu di giliran ini.
Kemudian saya lakukan loop pada semua kartu yang dimiliki pemain giliran sekarang. Jika kartu tersebut bisa dipasang di ujung meja (diperiksa dengan fungsi cekSisiKartu), maka saya cek sisi mana yang cocok dengan ujung kanan meja. Jika cocok dengan ujung kanan, saya panggil fungsi mainkanKartu dengan parameter meja, kartu yang dimainkan, dan true untuk main ke kanan. Jika tidak, berarti mainnya ke kiri, maka saya panggil mainkanKartu dengan parameter yang sama tapi false.Setelah kartu dimainkan, saya hapus kartu tersebut dari tangan pemain dengan menggunakan slicing dan gabung ulang slice tanpa kartu yang sudah dimainkan. Saya set berhasilMain menjadi true dan keluar dari loop karena sudah main kartu. Jika setelah loop tidak ada kartu yang bisa dimainkan (berhasilMain == false), maka saya cek apakah masih ada kartu tersisa di deck. Jika masih ada, saya panggil ambilKartu dari deck dan kartu tersebut ditambahkan ke tangan pemain giliran sekarang. Jika deck sudah kosong, saya cetak pesan pemain tidak bisa jalan dan menambah `drawCount` sebanyak 1. Jika pemain berhasil main kartu, saya reset drawCount menjadi 0. Selanjutnya saya cek apakah pemain sudah habis kartu, jika ya maka pemain tersebut menang dan saya keluar dari loop utama. Saya cek juga apakah drawCount sudah mencapai 2, yang berarti kedua pemain tidak bisa main kartu secara berurutan. Jika kondisi ini terpenuhi, maka permainan berakhir imbang. Saya hitung total poin kartu yang dimiliki masing-masing pemain dengan menjumlahkan nilai kartu menggunakan fungsi nilaiKartu. Saya tampilkan poin total kedua pemain, lalu saya tentukan pemenang berdasarkan poin terkecil. Jika poin sama, saya cetak hasil seri.Terakhir saya ganti giliran pemain dengan rumus (giliran + 1) % 2 agar giliran berganti antara pemain 0 dan 1 secara bergantian.

### Soal 4
Implementasi mesin abstrak karakter yang bekerja terhadap untaian karakter (yang diakhiri dengan penanda titik (".") dan mempunyai sejumlah operasi dasar. a) Operasi dasar mesin karakter: ➢ Prosedur start(); yang menyiapkan mesin karakter di awal rangkaian karakter. ➢ Prosedur maju(); yang memajukan pembaca ke posisi karakter berikutnya. ➢ Fungsi eop(); yang mengembalikan nilai true apabila sudah mencapai akhir rangkaian, sampai ke penanda titik ("."). ➢ Fungsi cc(); yang mengembalikan karakter yang sedang terbaca, atau berada pada posisi pembacaan mesin. b) Dengan operasi dasar di atas buat algoritma untuk: ➢ Membaca seluruh karakter yang diberikan ke mesin karakter tersebut. ➢ Menghitung berapa banyak karakter yang terbaca. ➢ Menghitung ada berapa huruf "A" yang terbaca. ➢ Menghitung frekuensi kemunculan huruf "A" terhadap seluruh karakter terbaca. ➢ Menghitung ada berapa kata "LE" (pasangan berturutan huruf "L" dan "E") yang terbaca.

```go
package main

import "fmt"
  
var input string

var pos int
 

func start() {

    pos = 0

}  

func maju() {

    pos++

}


func cc() byte {

    return input[pos]

}


func eop() bool {

    return cc() == '.'

}

func main() {

    input = "KALEA TERNAK IKAN LELE."

    start()
  

    jumlahKarakter := 0

    jumlahA := 0

    jumlahLE := 0

    var prevChar byte = 0


    for !eop() {

        currentChar := cc()

        jumlahKarakter++


        if currentChar == 'A' {

            jumlahA++

        }


        if prevChar == 'L' && currentChar == 'E' {

            jumlahLE++

        }

        prevChar = currentChar

        maju()

    }

    frekuensiA := float64(jumlahA) / float64(jumlahKarakter)

    fmt.Println("Jumlah karakter terbaca:", jumlahKarakter)

    fmt.Println("Jumlah huruf A:", jumlahA)

    fmt.Println("Frekuensi huruf A:", frekuensiA)

    fmt.Println("Jumlah kata 'LE':", jumlahLE)

}
```

> Output
> ![[modul_18_mesinAbstrak/output/soal4.png]]


Program ini digunakan untuk mencari jumlah karakater terbaca, jumlah huruf dan frequensi. Pertama saya punya deklarasi global yaitu input sebagai string dan pos sebagai integer, yang nanti dipakai untuk menyimpan untaian karakter dan posisi karakter yang sedang dibaca.
Lalu ada procedure start() yang isinya pos = 0, artinya saya mengatur posisi pembacaan karakter agar dimulai dari awal string, yaitu index ke-0.Selanjutnya ada procedure maju() yang isinya pos++, artinya ini berfungsi untuk memajukan posisi pembacaan satu karakter ke kanan tiap kali dipanggil. Lalu ada function cc() yang mengembalikan karakter yang sedang dibaca saat ini, yaitu input[pos], atau dengan kata lain karakter pada posisi ke-pos. Kemudian ada function eop() yang ngecek apakah pembacaan sudah sampai akhir. Di sini saya cek apakah karakter sekarang cc() itu sama dengan titik (.), karena dalam soal dikatakan penanda akhir adalah titik. Masuk ke main(), saya isi input = "KALEA TERNAK IKAN LELE." sebagai contoh untaian karakter yang ingin dibaca. Jangan lupa ada titik di akhir karena itu penting sebagai penanda berhenti. Lalu saya panggil start() untuk mulai pembacaan dari awal. Saya deklarasi tiga variabel penghitung: jumlahKarakter buat menghitung total karakter terbaca, jumlahA buat menghitung jumlah huruf A yang ditemukan, dan jumlahLE buat menghitung berapa kali pasangan huruf "LE" muncul. Saya juga pakai prevChar sebagai penyimpan karakter sebelumnya, karena untuk mendeteksi "LE" saya butuh tau huruf sebelumnya adalah 'L' dan huruf sekarang 'E'. Selanjutnya saya pakai perulangan for !eop() artinya perulangan dilakukan selama belum ketemu titik. Di dalamnya saya ambil karakter saat ini lewat cc(), lalu saya tambah jumlahKarakter karena satu karakter terbaca. Kalau karakter itu huruf A, saya tambahkan jumlahA. Untuk menghitung "LE", saya cek kalau prevChar adalah 'L' dan currentChar adalah 'E', maka jumlahLE++. Setelah itu saya simpan currentChar ke prevChar untuk digunakan di iterasi berikutnya, lalu saya panggil maju() untuk pindah ke karakter berikutnya. Setelah loop selesai, saya hitung frekuensi huruf A yaitu dengan float64(jumlahA) / float64(jumlahKarakter) biar hasilnya dalam bentuk pecahan. Terakhir saya tampilkan semua hasil yaitu jumlah karakter, jumlah huruf A, frekuensi kemunculan A, dan jumlah pasangan "LE".

