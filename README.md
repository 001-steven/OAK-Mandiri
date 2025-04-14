# NAMA : Moh. Yusril
# NIM : 09011382429124
# KELAS : SKU2B

![image](https://github.com/user-attachments/assets/835d5245-7d94-41c7-a719-b869c936ed75)

section .data
    pesan db    'Hasil dari 3 + 1 adalah: ', 0xA, 0xD
    panjang_pesan equ $ - pesan
    segment .bss
    hasil resb 1  ; buffer untuk hasil

section .text
    global _start

_start:
    ; Konversi '3' ke integer
    mov     eax, '3'  
    sub     eax, '0'    ; '3' - '0' = 3

    ; Konversi '1' ke integer
    mov     ebx, '1'  
    sub     ebx, '0'    ; '1' - '0' = 1

    ; Tambahkan angka
    add     eax, ebx    ; 3 + 1 = 4

    ; Konversi hasil kembali ke ASCII (menambahkan '0' kembali)
    add     eax, '0'    ; 4 + '0' = '4' (karakter ASCII)

    ; Simpan hasil ke dalam buffer hasil
    mov     [hasil], al ; Simpan byte hasil ke dalam hasil

    ; Tampilkan pesan
    mov     eax, 4      ; syscall SYS_WRITE
    mov     ebx, 1      ; file descriptor STDOUT
    mov     ecx, pesan  ; pesan yang akan ditampilkan
    mov     edx, panjang_pesan  ; panjang pesan
    int     0x80        ; panggil sistem untuk menulis

    ; Tampilkan hasil penjumlahan
    mov     eax, 4      ; syscall SYS_WRITE
    mov     ebx, 1      ; file descriptor STDOUT
    mov     ecx, hasil  ; hasil yang akan ditampilkan
    mov     edx, 1      ; panjang hasil (1 byte)
    int     0x80        ; panggil sistem untuk menulis

    ; Keluar dari program
    mov     eax, 1      ; syscall SYS_EXIT
    xor     ebx, ebx    ; kode keluar 0
    int     0x80        ; panggil sistem untuk keluar


## Bagian Data
Pada bagian ini, kita mendefinisikan data yang akan digunakan dalam program. pesan adalah string yang berisi teks "Hasil dari 3 + 1 adalah: " diikuti dengan karakter newline (0xA) dan carriage return (0xD). panjang_pesan dihitung sebagai selisih antara alamat saat ini ($) dan alamat awal dari pesan, yang memberikan panjang total dari string tersebut. Di bagian .bss, kita mendeklarasikan hasil sebagai buffer yang akan menyimpan satu byte untuk hasil penjumlahan.

## Bagian Teks dan Entry Point
Di bagian .text, kita mendeklarasikan _start sebagai titik masuk program. Ini adalah label yang menunjukkan di mana eksekusi program dimulai. Semua instruksi yang mengikuti label ini akan dieksekusi saat program dijalankan.

## Konversi Karakter ke Integer
Di bagian ini, kita melakukan konversi karakter ASCII '3' dan '1' menjadi integer. Pertama, kita memindahkan nilai ASCII dari karakter '3' ke register eax, kemudian menguranginya dengan nilai ASCII dari '0' untuk mendapatkan nilai integer 3. Proses yang sama dilakukan untuk karakter '1', yang disimpan di register ebx, menghasilkan nilai integer 1.

## Penjumlahan
Setelah mendapatkan kedua angka dalam bentuk integer, kita melakukan penjumlahan dengan instruksi add. Hasil dari penjumlahan (3 + 1) disimpan kembali di register eax, yang sekarang berisi nilai 4.

## Konversi Hasil Kembali ke ASCII
Setelah penjumlahan, kita perlu mengonversi hasil kembali ke bentuk karakter ASCII agar bisa ditampilkan. Kita menambahkan nilai ASCII dari '0' ke eax, sehingga nilai 4 diubah menjadi karakter '4'. Hasil ini kemudian disimpan ke dalam buffer hasil.

## Menampilkan Pesan
Di sini, kita menggunakan syscall untuk menampilkan pesan ke layar. Kita mengatur register eax dengan nilai 4 untuk syscall SYS_WRITE, ebx dengan 1 untuk file descriptor STDOUT, ecx dengan alamat dari pesan, dan edx dengan panjang pesan. Kemudian, kita memanggil interrupt 0x80 untuk mengeksekusi syscall dan menampilkan pesan.

## Menampilkan Hasil Penjumlahan 
Setelah menampilkan pesan, kita melakukan langkah yang sama untuk menampilkan hasil penjumlahan. Kita mengatur register dengan nilai yang sesuai untuk menampilkan buffer hasil, yang berisi karakter '4'. Kita menggunakan syscall SYS_WRITE lagi untuk menampilkan hasil ke layar.

## Keluar dari Program
Akhirnya, kita menyiapkan program untuk keluar dengan mengatur register eax ke 1 untuk syscall SYS_EXIT dan ebx ke 0 sebagai kode keluar. Kita kemudian memanggil interrupt 0x80 untuk mengeksekusi syscall dan mengakhiri program dengan sukses.

* Dengan demikian, program ini melakukan penjumlahan sederhana antara dua angka yang diwakili sebagai karakter ASCII, menampilkan hasilnya di layar, dan kemudian keluar dengan kode status 0.
