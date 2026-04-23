### Laporan Praktikum 7

<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## Praktikum 7.1 Script Pertama: Laporan Sistem
Tujuan: membuat, menyimpan, dan menjalankan script Bash pertama.

1. Buat workspace praktikum:
```bash
mkdir -p ~/praktikum-os/week09/{scripts,logs,data}
cd ~/praktikum-os/week09/scripts
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ mkdir -p ~/praktikum-os/week09/{scripts,logs,data}
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ cd ~/praktikum-os/week09/scripts
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ pwd
/home/reyhandhika/praktikum-os/week09/scripts
```
2. Buat script dengan nano:
```bash
nano laporan-sistem.sh
```
3. Ketik isi berikut, simpan ( Ctrl+O Enter ), lalu keluar ( Ctrl+X ):
```bash
#!/bin/bash
# Script : laporan-sistem.sh

echo "================================"
echo "LAPORAN SISTEM"
echo "================================"
echo "Tanggal : $(date '+%A, %d %B %Y')"
echo "Jam : $(date '+%H:%M:%S')"
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "CPU core : $(nproc)"
echo "RAM bebas : $(free -h | awk '/^Mem/ {print $4}')"
echo "Disk / : $(df -h / | awk 'NR==2 {print $5}') terpakai"
echo "================================"
```
Output:
```bash
  GNU nano 7.2                                              laporan-sistem.sh
#!/bin/bash
# Script : laporan-sistem.sh

echo "================================"
echo "LAPORAN SISTEM"
echo "================================"
echo "Tanggal : $(date '+%A, %d %B %Y')"
echo "Jam : $(date '+%H:%M:%S')"
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "CPU core : $(nproc)"
echo "RAM bebas : $(free -h | awk '/^Mem/ {print $4}')"
echo "Disk / : $(df -h / | awk 'NR==2 {print $5}') terpakai"
echo "================================"


















^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy
```
4. Beri izin dan jalankan:
```bash
chmod +x laporan-sistem.sh
./laporan-sistem.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x laporan-sistem.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./laporan-sistem.sh
================================
LAPORAN SISTEM
================================
Tanggal : Wednesday, 22 April 2026
Jam : 05:00:58
Hostname : reyhandhika
User : reyhandhika
CPU core : 1
RAM bebas : 1.3Gi
Disk / : 53% terpakai
================================
```
## Latihan Latihan 9.1
Modifikasi laporan-sistem.sh agar menyimpan output ke file laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk: gunakan tee yang sudah dipelajari di bab sebelumnya.

Jawaban:
```bash
  GNU nano 7.2                                              laporan-sistem.sh
#!/bin/bash
# Script : laporan-sistem.sh

FILE="laporan-$(date +%F).txt"
{
echo "================================"
echo "LAPORAN SISTEM"
echo "================================"
echo "Tanggal : $(date '+%A, %d %B %Y')"
echo "Jam : $(date '+%H:%M:%S')"
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "CPU core : $(nproc)"
echo "RAM bebas : $(free -h | awk '/^Mem/ {print $4}')"
echo "Disk / : $(df -h / | awk 'NR==2 {print $5}') terpakai"
echo "================================"
} | tee "$FILE"















^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy

```
Jadi Modifikasi dilakukan untuk menyimpan output laporan sistem ke file dengan nama berdasarkan tanggal, serta tetap menampilkan output di terminal menggunakan perintah tee.

## Praktikum 7.2 Script Info Sistem dengan Argumen
Tujuan: berlatih variabel, substitusi perintah, parameter posisional, dan nilai default.

1. Buat script:
nano ~/praktikum-os/week09/scripts/info-sistem.sh

2. Ketik isi berikut:
```bash
#!/bin/bash
# Penggunaan : ./info-sistem.sh [nama-admin] [batas-disk-persen]

ADMIN=${1:-"Tidak dikenal"}
BATAS=${2:-80}

TANGGAL=$(date '+%F %T')

DISK_PERSEN=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Admin : $ADMIN"
echo "Tanggal : $TANGGAL"
echo "Disk / : ${DISK_PERSEN}% terpakai"
echo "Batas : ${BATAS}%"

if [ "$DISK_PERSEN" -gt "$BATAS" ]; then
echo "STATUS : PERINGATAN - disk melebihi batas!"
else
SISA=$(( BATAS - DISK_PERSEN ))
echo "STATUS : Normal (sisa toleransi ${SISA}%)"
fi
```
Output:
```bash
  GNU nano 7.2                         /home/reyhandhika/praktikum-os/week09/scripts/info-sistem.sh
#!/bin/bash
# Penggunaan : ./info-sistem.sh [nama-admin] [batas-disk-persen]

ADMIN=${1:-"Tidak dikenal"}
BATAS=${2:-80}

TANGGAL=$(date '+%F %T')

DISK_PERSEN=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Admin : $ADMIN"
echo "Tanggal : $TANGGAL"
echo "Disk / : ${DISK_PERSEN}% terpakai"
echo "Batas : ${BATAS}%"

if [ "$DISK_PERSEN" -gt "$BATAS" ]; then
echo "STATUS : PERINGATAN - disk melebihi batas!"
else
SISA=$(( BATAS - DISK_PERSEN ))
echo "STATUS : Normal (sisa toleransi ${SISA}%)"
fi











^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy
```
3. Simpan, beri izin, uji dengan berbagai kombinasi argumen:
```bash
chmod +x ~/praktikum-os/week09/scripts/info-sistem.sh
./info-sistem.sh
./info-sistem.sh " Reyhan " 50
./info-sistem.sh " Reyhan " 10
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./info-sistem.sh
Admin : Tidak dikenal
Tanggal : 2026-04-22 05:22:28
Disk / : 53% terpakai
Batas : 80%
STATUS : Normal (sisa toleransi 27%)
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./info-sistem.sh " Reyhan " 50
Admin :  Reyhan
Tanggal : 2026-04-22 05:23:10
Disk / : 53% terpakai
Batas : 50%
STATUS : PERINGATAN - disk melebihi batas!
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./info-sistem.sh " Reyhan " 10
Admin :  Reyhan
Tanggal : 2026-04-22 05:23:21
Disk / : 53% terpakai
Batas : 10%
STATUS : PERINGATAN - disk melebihi batas!
```
Latihan Latihan 9.2
Buat script kalkulator.sh yang menerima tiga argumen: <angka1> <operator> <angka2> dengan operator +, -, *, atau /. Contoh: ./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih operasi, dan validasi jika argumen tidak lengkap.

Output:
```bash
 GNU nano 7.2                                                kalkulator.sh
# Validasi jumlah argumen
if [ $# -ne 3 ]; then
echo "Penggunaan: $0 <angka1> <operator> <angka2>"
exit 1
fi

ANGKA1=$1
OPERATOR=$2
ANGKA2=$3

case $OPERATOR in
+)
HASIL=$((ANGKA1 + ANGKA2))
;;

-)
HASIL=$((ANGKA1 - ANGKA2))
;;

\*)
HASIL=$((ANGKA1 * ANGKA2))
;;

 /)
if [ "$ANGKA2" -eq 0 ]; then
echo "Error: pembagian dengan nol"
exit 1
fi
HASIL=$((ANGKA1 / ANGKA2))
;;


^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy

```
langkah selanjutnya
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x kalkulator.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./kalkulator.sh 20 + 5
Hasil: 25
```
Script kalkulator.sh digunakan untuk melakukan operasi aritmetika dasar (+, -, *, /) berdasarkan tiga argumen yang diberikan melalui command line.

## Praktikum 7.3 Script Grading dan Menu Interaktif
Tujuan: menggabungkan if, for, while, dan case dalam satu session

1. Buat script grading (menggunakan if dan for):
```bash
nano ~/praktikum-os/week09/scripts/grading-batch.sh
```
2. Ketik isi berikut:
```bash
#!/bin/bash
# Script : grading-batch.sh

# Daftar mahasiswa dan nilai
MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")

echo "=== HASIL GRADING ==="

for ENTRI in "${MAHASISWA[@]}"; do

NAMA=$(echo "$ENTRI" | cut -d: -f1)
NILAI=$(echo "$ENTRI" | cut -d: -f2)

if [ "$NILAI" -ge 85 ]; then
GRADE="A"

elif [ "$NILAI" -ge 75 ]; then
GRADE="B"

elif [ "$NILAI" -ge 65 ]; then
GRADE="C"

elif [ "$NILAI" -ge 55 ]; then
GRADE="D"

else
GRADE="E"

fi

printf "%-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"

done

echo "====================="
```

Output:
```bash
  GNU nano 7.2                                                             /home/reyhandhika/praktikum-os/week09/scripts/grading-batch.sh
#!/bin/bash
# Script : grading-batch.sh

# Daftar mahasiswa dan nilai
MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")

echo "=== HASIL GRADING ==="

for ENTRI in "${MAHASISWA[@]}"; do

NAMA=$(echo "$ENTRI" | cut -d: -f1)
NILAI=$(echo "$ENTRI" | cut -d: -f2)

if [ "$NILAI" -ge 85 ]; then
GRADE="A"

elif [ "$NILAI" -ge 75 ]; then
GRADE="B"

elif [ "$NILAI" -ge 65 ]; then
GRADE="C"

elif [ "$NILAI" -ge 55 ]; then
GRADE="D"

else
GRADE="E"

fi

printf "%-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"

done

echo "====================="















^G Help          ^O Write Out     ^W Where Is      ^K Cut           ^T Execute       ^C Location      M-U Undo         M-A Set Mark     M-] To Bracket   M-Q Previous     ^B Back          ^◂ Prev Word
^X Exit          ^R Read File     ^\ Replace       ^U Paste         ^J Justify       ^/ Go To Line    M-E Redo         M-6 Copy         ^Q Where Was     M-W Next         ^F Forward       ^▸ Next Word
```
3. Simpan, beri izin, dan jalankan:
```bash
chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
./grading-batch.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./grading-batch.sh
=== HASIL GRADING ===
Andi        92 A
Budi        73 C
Citra       55 D
Deni        80 B
Eka         45 E
=====================
```
4. Buat script menu interaktif (while + case):
```bash
nano ~/praktikum-os/week09/scripts/menu-sistem.sh
```
5. Ketik isi berikut:
```bash
#!/bin/bash
# Menu interaktif pemantauan sistem

while true; do

echo ""
echo "===== MENU MONITOR ====="
echo "1) Info disk"
echo "2) Info memori"
echo "3) Proses teratas"
echo "4) Keluar"
echo -n "Pilih [1-4]: "

read PILIHAN

case $PILIHAN in

1)
df -h
;;

2)
free -h
;;

3)
ps aux --sort=-%cpu | head -6
;;

4)
echo "Sampai jumpa!"
exit 0
;;

*)
echo "Pilihan tidak valid."
;;

esac

done
```

Output:
```bash
  GNU nano 7.2                                                              /home/reyhandhika/praktikum-os/week09/scripts/menu-sistem.sh
#!/bin/bash
# Menu interaktif pemantauan sistem

while true; do

echo ""
echo "===== MENU MONITOR ====="
echo "1) Info disk"
echo "2) Info memori"
echo "3) Proses teratas"
echo "4) Keluar"
echo -n "Pilih [1-4]: "

read PILIHAN

case $PILIHAN in

1)
df -h
;;

2)
free -h
;;

3)
ps aux --sort=-%cpu | head -6
;;

4)
echo "Sampai jumpa!"
exit 0
;;

*)
echo "Pilihan tidak valid."
;;

esac

done









^G Help          ^O Write Out     ^W Where Is      ^K Cut           ^T Execute       ^C Location      M-U Undo         M-A Set Mark     M-] To Bracket   M-Q Previous     ^B Back          ^◂ Prev Word
^X Exit          ^R Read File     ^\ Replace       ^U Paste         ^J Justify       ^/ Go To Line    M-E Redo         M-6 Copy         ^Q Where Was     M-W Next         ^F Forward       ^▸ Next Word
```
6. Beri izin dan jalankan, coba setiap opsi:
```bash
chmod +x ~/praktikum-os/week09/scripts/menu-sistem.sh
./menu-sistem.sh
```
## Latihan Latihan 9.3
Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah
yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan
perulangan for kedua yang mengiterasi array MAHASISWA.

Output:
```bash
  GNU nano 7.2                                                                                                                                        grading-batch.sh *
#!/bin/bash
# Script : grading-batch.sh

# Daftar mahasiswa dan nilai
MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")

# Counter grade
A_COUNT=0
B_COUNT=0
C_COUNT=0
D_COUNT=0
E_COUNT=0

echo "=== HASIL GRADING ==="

for ENTRI in "${MAHASISWA[@]}"; do

NAMA=$(echo "$ENTRI" | cut -d: -f1)
NILAI=$(echo "$ENTRI" | cut -d: -f2)

if [ "$NILAI" -ge 85 ]; then
GRADE="A"
((A_COUNT++))

elif [ "$NILAI" -ge 75 ]; then
GRADE="B"
((B_COUNT++))

elif [ "$NILAI" -ge 65 ]; then
GRADE="C"
((C_COUNT++))

elif [ "$NILAI" -ge 55 ]; then
GRADE="D"
((D_COUNT++))

else
GRADE="E"
((E_COUNT++))

fi

printf "%-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"

done

echo "====================="

echo ""
echo "=== RINGKASAN ==="
echo "Grade A : $A_COUNT"
echo "Grade B : $B_COUNT"
echo "Grade C : $C_COUNT"
echo "Grade D : $D_COUNT"
echo "Grade E : $E_COUNT"

























^G Help           ^O Write Out      ^W Where Is       ^K Cut            ^T Execute        ^C Location       M-U Undo          M-A Set Mark      M-] To Bracket    M-Q Previous      ^B Back           ^◂ Prev Word      ^A Home           ^P Prev Line      M-▴ Scroll Up     ^▴ Prev Block     M-( Begin of Paragr.
^X Exit           ^R Read File      ^\ Replace        ^U Paste          ^J Justify        ^/ Go To Line     M-E Redo          M-6 Copy          ^Q Where Was      M-W Next          ^F Forward        ^▸ Next Word      ^E End            ^N Next Line      M-▾ Scroll Down   ^▾ Next Block     M-) End of Paragraph
```
## Praktikum 7.4 Library Fungsi Validasi
Tujuan: membuat file library fungsi yang dapat dimuat (source) oleh script lain konsep serupa dengan import di Java.
1. Buat file library:
```bash
nano ~/praktikum-os/week09/scripts/lib-validasi.sh

2. Ketik isi berikut:
```bash
#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
[[ "$1" =~ ^[0-9]+$ ]]
}

file_bisa_dibaca() {
[ -f "$1" ] && [ -r "$1" ]
}

error_exit() {
echo "ERROR: $1" >&2
exit 1
}

info() {
echo "[INFO] $1"
}

sukses() {
echo "[OK] $1"
}
```
Output:
```bash
  GNU nano 7.2                                 /home/reyhandhika/praktikum-os/week09/scripts/lib-validasi.sh *
#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
[[ "$1" =~ ^[0-9]+$ ]]
}

file_bisa_dibaca() {
[ -f "$1" ] && [ -r "$1" ]
}

error_exit() {
echo "ERROR: $1" >&2
exit 1
}

info() {
echo "[INFO] $1"
}

sukses() {
echo "[OK] $1"
}











^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark    M-] To Bracket
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy        ^Q Where Was
```
3. Buat script yang menggunakan library:
```bash
nano ~/praktikum-os/week09/scripts/pakai-library.sh
```
4. Ketik isi berikut:
```bash
#!/bin/bash

# Load library
source ~/praktikum-os/week09/scripts/lib-validasi.sh

ANGKA=$1
FILE=$2

# Validasi argumen
[ -z "$ANGKA" ] || [ -z "$FILE" ] && \
error_exit "Penggunaan: $0 <angka> <path-file>"

# Cek angka
if adalah_angka "$ANGKA"; then
sukses "Input '$ANGKA' adalah angka valid"
else
error_exit "'$ANGKA' bukan angka"
fi

# Cek file
if file_bisa_dibaca "$FILE"; then
sukses "File '$FILE' bisa dibaca"
info "Jumlah baris: $(wc -l < "$FILE")"
else
error_exit "File '$FILE' tidak ada atau tidak bisa dibaca"
fi
```

Output:
```bash
  GNU nano 7.2                                 /home/reyhandhika/praktikum-os/week09/scripts/pakai-library.sh
#!/bin/bash

# Load library
source ~/praktikum-os/week09/scripts/lib-validasi.sh

ANGKA=$1
FILE=$2

# Validasi argumen
[ -z "$ANGKA" ] || [ -z "$FILE" ] && \
error_exit "Penggunaan: $0 <angka> <path-file>"

# Cek angka
if adalah_angka "$ANGKA"; then
sukses "Input '$ANGKA' adalah angka valid"
else
error_exit "'$ANGKA' bukan angka"
fi

# Cek file
if file_bisa_dibaca "$FILE"; then
sukses "File '$FILE' bisa dibaca"
info "Jumlah baris: $(wc -l < "$FILE")"
else
error_exit "File '$FILE' tidak ada atau tidak bisa dibaca"
fi







                                                                  [ Wrote 26 lines ]
^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark    M-] To Bracket
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy        ^Q Where Was
```
5. Beri izin dan uji semua skenario:
```bash
chmod +x ~/praktikum-os/week09/scripts/pakai-library.sh
./pakai-library.sh 42 /etc/hostname
./pakai-library.sh abc /etc/hostname
./pakai-library.sh 42 /tidak-ada.txt
./pakai-library.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./pakai-library.sh 42 /etc/hostname
[OK] Input '42' adalah angka valid
[OK] File '/etc/hostname' bisa dibaca
[INFO] Jumlah baris: 1
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./pakai-library.sh abc /etc/hostname
ERROR: 'abc' bukan angka
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./pakai-library.sh 42 /tidak-ada.txt
[OK] Input '42' adalah angka valid
ERROR: File '/tidak-ada.txt' tidak ada atau tidak bisa dibaca
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./pakai-library.sh
ERROR: Penggunaan: ./pakai-library.sh <angka> <path-file>
```
## Latihan Latihan 9.4
Tambahkan fungsi konfirmasi() ke lib-validasi.sh.Fungsi ini menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan 0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum menghapus sebuah file.

Output:
```bash

  GNU nano 7.2                                                        lib-validasi.sh

error_exit() {
echo "ERROR: $1" >&2
exit 1
}

info() {
echo "[INFO] $1"
}

sukses() {
echo "[OK] $1"
}

konfirmasi() {
echo -n "$1 (Y/N): "
read JAWABAN

case "$JAWABAN" in
Y|y)
return 0
;;

N|n)
return 1
;;

*)
echo "Masukkan Y atau N."
return 1
;;
esac
}

^G Help         ^O Write Out    ^W Where Is     ^K Cut          ^T Execute      ^C Location     M-U Undo        M-A Set Mark    M-] To Bracket
^X Exit         ^R Read File    ^\ Replace      ^U Paste        ^J Justify      ^/ Go To Line   M-E Redo        M-6 Copy        ^Q Where Was
```
langkah selanjutnya
```bash
nano hapus-file.sh
```
input:
```bash
#!/bin/bash

# Load library
source ~/praktikum-os/week09/scripts/lib-validasi.sh

FILE=$1

# Cek apakah argumen ada
[ -z "$FILE" ] && error_exit "Penggunaan: $0 <nama-file>"

# Cek apakah file ada
if [ ! -f "$FILE" ]; then
error_exit "File '$FILE' tidak ditemukan"
fi

# Konfirmasi sebelum hapus
if konfirmasi "Apakah Anda yakin ingin menghapus '$FILE'?"; then

rm "$FILE"
sukses "File '$FILE' berhasil dihapus"

else

info "Penghapusan dibatalkan"

fi
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x hapus-file.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ touch test.txt
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ls
grading-batch.sh  hapus-file.sh  info-sistem.sh  kalkulator.sh  laporan-sistem.sh  lib-validasi.sh  menu-sistem.sh  pakai-library.sh  sh  test.txt
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./hapus-file.sh test.txt
Apakah Anda yakin ingin menghapus 'test.txt'? (Y/N): y
[OK] File 'test.txt' berhasil dihapus
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ls
grading-batch.sh  hapus-file.sh  info-sistem.sh  kalkulator.sh  laporan-sistem.sh  lib-validasi.sh  menu-sistem.sh  pakai-library.sh  sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ cat hapus-file.sh
#!/bin/bash

# Load library
source ~/praktikum-os/week09/scripts/lib-validasi.sh

FILE=$1

# Cek apakah argumen ada
[ -z "$FILE" ] && error_exit "Penggunaan: $0 <nama-file>"

# Cek apakah file ada
if [ ! -f "$FILE" ]; then
error_exit "File '$FILE' tidak ditemukan"
fi

# Konfirmasi sebelum hapus
if konfirmasi "Apakah Anda yakin ingin menghapus '$FILE'?"; then

rm "$FILE"
sukses "File '$FILE' berhasil dihapus"

else

info "Penghapusan dibatalkan"

fi
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ cat lib-validasi.sh
#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
[[ "$1" =~ ^[0-9]+$ ]]
}

file_bisa_dibaca() {
[ -f "$1" ] && [ -r "$1" ]
}

error_exit() {
echo "ERROR: $1" >&2
exit 1
}

info() {
echo "[INFO] $1"
}

sukses() {
echo "[OK] $1"
}

konfirmasi() {
echo -n "$1 (Y/N): "
read JAWABAN

case "$JAWABAN" in
Y|y)
return 0
;;

N|n)
return 1
;;

*)
echo "Masukkan Y atau N."
return 1
;;
esac
}
```

## Praktikum 7.5 Script Backup dengan Opsi
Tujuan: membuat script yang memproses opsi getopts dan mengintegrasikan semua konsep sebelumnya.

1. Buat script:
```bash
nano ~/ praktikum-os/week09/scripts/backup-data.sh
```
2. ketik isi berikut:
```bash
#!/bin/bash
# Penggunaan: ./backup-data.sh [-v] [-c] [-l logfile] <sumber> <tujuan>

VERBOSE=false
COMPRESS=false
LOG_FILE=""

# Membaca opsi
while getopts "vcl:" OPSI; do
    case $OPSI in
        v)
            VERBOSE=true
            ;;
        c)
            COMPRESS=true
            ;;
        l)
            LOG_FILE="$OPTARG"
            ;;
        *)
            echo "Penggunaan: $0 [-v] [-c] [-l logfile] <sumber> <tujuan>"
            exit 1
            ;;
    esac
done

shift $((OPTIND - 1))

SUMBER="$1"
TUJUAN="$2"

# Fungsi log
log() {
    local MSG="[$(date '+%T')] $1"
    echo "$MSG"

    if [ -n "$LOG_FILE" ]; then
        echo "$MSG" >> "$LOG_FILE"
    fi
}

# Validasi input
if [ -z "$SUMBER" ] || [ -z "$TUJUAN" ]; then
    echo "ERROR: sumber dan tujuan wajib diisi"
    exit 1
fi

if [ ! -d "$SUMBER" ]; then
    log "ERROR: $SUMBER tidak ada"
    exit 2
fi

mkdir -p "$TUJUAN"

TANGGAL=$(date '+%F-%H%M%S')

if [ "$VERBOSE" = true ]; then
    log "Sumber: $SUMBER | Tujuan: $TUJUAN"
fi

# Jika compress
if [ "$COMPRESS" = true ]; then

    ARSIP="$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL.tar.gz"

    tar -czf "$ARSIP" \
        -C "$(dirname "$SUMBER")" \
        "$(basename "$SUMBER")"

    log "Arsip dibuat: $ARSIP"

else

    cp -r "$SUMBER" \
        "$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL"

    log "Backup selesai."

fi
```

3. beri izin dan uji
```bash
chmod +x ~/praktikum-os/week09/scripts/backup-data.sh
cd ~/praktikum-os/week09/scripts
#tanpa opsi
./backup-data.sh \
~/praktikum-os/week09/data \
~/praktikum-os/week09/logs
#dengan verbose dan kompresi + log ke file

./backup-data.sh -v -c -l ../logs/backup.log \
~/praktikum-os/week09/data \
~/praktikum-os/week09/logs

cat ../logs/backup.log
```
Output:
```bash
reyhandhika@reyhandhika:~$ chmod +x ~/praktikum-os/week09/scripts/backup-data.sh
reyhandhika@reyhandhika:~$ cd ~/praktikum-os/week09/scripts
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./backup-data.sh \
> ~/praktikum-os/week09/data \
> ~/praktikum-os/week09/logs
[14:20:37] Backup selesai.
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./backup-data.sh -v -c -l ../logs/backup.log \
> ~/praktikum-os/week09/data \
> ~/praktikum-os/week09/logs
[14:21:01] Sumber: /home/reyhandhika/praktikum-os/week09/data | Tujuan: /home/reyhandhika/praktikum-os/week09/logs
[14:21:01] Arsip dibuat: /home/reyhandhika/praktikum-os/week09/logs/backup-data-2026-04-23-142101.tar.gz
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ cat ../logs/backup.log
[14:21:01] Sumber: /home/reyhandhika/praktikum-os/week09/data | Tujuan: /home/reyhandhika/praktikum-os/week09/logs
[14:21:01] Arsip dibuat: /home/reyhandhika/praktikum-os/week09/logs/backup-data-2026-04-23-142101.tar.gz
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$

```
## Praktikum 7.6 Debugging Script
Tujuan: menggunakan teknik debugging untuk menganalisis dan memperbaiki script.
1. Buat script untuk dianalisis:
```bash
nano ~/ praktikum-os/week09/scripts/debug-latihan.sh
```
2. ketik isi berikut:
```bash
#!/bin/bash
# Script: debug-latihan.sh
# Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>

DIREKTORI=$1
BATAS=$2

if [ $# -ne 2 ]; then
    echo "Penggunaan: $0 <direktori> <batas-MB>"
    exit 1
fi

UKURAN=$(du -sm "$DIREKTORI" | cut -f1)

echo "Direktori : $DIREKTORI"
echo "Ukuran    : ${UKURAN} MB"
echo "Batas     : ${BATAS} MB"

if [ "$UKURAN" -gt "$BATAS" ]; then
    echo "PERINGATAN: Ukuran melebihi batas!"
    echo "Kelebihan : $(( UKURAN - BATAS )) MB"
else
    echo "Status: Normal (sisa: $(( BATAS - UKURAN )) MB)"
fi
```
33. Cek sintaks, lalu jalankan dengan tracing:
```bash
chmod +x ~/praktikum-os/week09/scripts/debug-latihan.sh
bash -n debug-latihan.sh && echo " Sintaks OK"
bash -x debug-latihan.sh / etc 10
./debug-latihan.sh /var 50
./debug-latihan.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ nano ~/ praktikum-os/week09/scripts/debug-latihan.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x debug-latihan.sh
chmod: cannot access 'debug-latihan.sh': No such file or directory
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ls
backup-data.sh    info-sistem.sh     lib-validasi.sh   sh
grading-batch.sh  kalkulator.sh      menu-sistem.sh
hapus-file.sh     laporan-sistem.sh  pakai-library.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ nano ~/ praktikum-os/week09/scripts/debug-latihan.sh


reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ pwd
/home/reyhandhika/praktikum-os/week09/scripts
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ cd ~/praktikum-os/week09/scripts
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ nano ~/ praktikum-os/week09/scripts/debug-latihan.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ pwd
/home/reyhandhika/praktikum-os/week09/scripts
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ nano ~/ praktikum-os/week09/scripts/debug-latihan.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ls
backup-data.sh    info-sistem.sh     menu-sistem.sh
debug-latihan.sh  kalkulator.sh      pakai-library.sh
grading-batch.sh  laporan-sistem.sh  sh
hapus-file.sh     lib-validasi.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/debug-latihan.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ bash -n debug-latihan.sh && echo "Sintaks OK"
Sintaks OK
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ bash -x debug-latihan.sh /etc 10
+ DIREKTORI=/etc
+ BATAS=10
+ '[' 2 -ne 2 ']'
++ du -sm /etc
++ cut -f1
du: cannot read directory '/etc/credstore': Permission denied
du: cannot read directory '/etc/credstore.encrypted': Permission denied
du: cannot read directory '/etc/polkit-1/rules.d': Permission denied
du: cannot read directory '/etc/multipath': Permission denied
du: cannot read directory '/etc/ssl/private': Permission denied
+ UKURAN=7
+ echo 'Direktori : /etc'
Direktori : /etc
+ echo 'Ukuran    : 7 MB'
Ukuran    : 7 MB
+ echo 'Batas     : 10 MB'
Batas     : 10 MB
+ '[' 7 -gt 10 ']'
+ echo 'Status: Normal (sisa: 3 MB)'
Status: Normal (sisa: 3 MB)
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./debug-latihan.sh /var 50
du: cannot read directory '/var/log/private': Permission denied
du: cannot read directory '/var/cache/apt/archives/partial': Permission denied
du: cannot read directory '/var/cache/apparmor/2693c843.0': Permission denied
du: cannot read directory '/var/cache/ldconfig': Permission denied
du: cannot read directory '/var/cache/pollinate': Permission denied
du: cannot read directory '/var/cache/private': Permission denied
du: cannot read directory '/var/lib/update-notifier/package-data-downloads/partial': Permission denied
du: cannot read directory '/var/lib/snapd/cookie': Permission denied
du: cannot read directory '/var/lib/snapd/void': Permission denied
du: cannot read directory '/var/lib/apt/lists/partial': Permission denied
du: cannot read directory '/var/lib/udisks2': Permission denied
du: cannot read directory '/var/lib/polkit-1': Permission denied
du: cannot read directory '/var/lib/ubuntu-advantage/apt-esm/var/lib/apt/lists/partial': Permission denied
du: cannot read directory '/var/lib/private': Permission denied
du: cannot read directory '/var/lib/fwupd/gnupg': Permission denied
du: cannot read directory '/var/spool/rsyslog': Permission denied
du: cannot read directory '/var/spool/cron/crontabs': Permission denied
du: cannot read directory '/var/tmp/systemd-private-43ad115b8b61447fa66d1c9c499868de-systemd-timesyncd.service-Jmm5Zr': Permission denied
du: cannot read directory '/var/tmp/systemd-private-43ad115b8b61447fa66d1c9c499868de-polkit.service-wuS1k6': Permission denied
du: cannot read directory '/var/tmp/systemd-private-43ad115b8b61447fa66d1c9c499868de-systemd-logind.service-wc9Xtt': Permission denied
du: cannot read directory '/var/tmp/systemd-private-43ad115b8b61447fa66d1c9c499868de-systemd-resolved.service-x55xUu': Permission denied
du: cannot read directory '/var/tmp/systemd-private-43ad115b8b61447fa66d1c9c499868de-ModemManager.service-g8y3Jn': Permission denied
Direktori : /var
Ukuran    : 1057 MB
Batas     : 50 MB
PERINGATAN: Ukuran melebihi batas!
Kelebihan : 1007 MB
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./debug-latihan.sh
Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$
```
## Latihan Latihan 9.5
Script debug-latihan.sh tidak menangani direktori yang tidak ada. Perbaiki
dengan menambahkan:
• set -e di baris kedua
• Pengecekan -d "$DIREKTORI" sebelum memanggil du
• Pesan error yang informatif jika direktori tidak ditemukan
Uji dengan direktori yang tidak ada

```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./debug-latihan.sh /tidak-ada 10
ERROR: Direktori tidak ditemukan: /tidak-ada
```
## 1.8 Tugas Praktikum
Peringatan
Kerjakan tugas di $HOME/praktikum-os/week09/. Script di scripts/, output di logs/.

### TUGAS
Tugas 1 Script Absensi Kelas
Konteks: instruktur mencatat kehadiran mahasiswa dari command line.
Instruksi:
1. Buat script absensi.sh yang:
• Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)
• Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM]
NAMA - STATUS
• Opsi -r: tampilkan rekapitulasi (jumlah per status)
• Opsi -h: tampilkan bantuan
2. Rekam minimal 5 entri dan tampilkan rekapitulasinya.
Konsep wajib: variabel, parameter posisional, getopts, if, for, fungsi, dan
redirection ke file.

Jawab:

```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ nano absensi.sh
```
skripnya:
```bash

#!/bin/bash

TANGGAL=$(date '+%F')
FILE="$HOME/praktikum-os/week09/logs/absensi-$TANGGAL.txt"

usage() {
    echo "Penggunaan:"
    echo "./absensi.sh <nama> <hadir|izin|alpha>"
    echo "./absensi.sh -r   (rekap absensi)"
    echo "./absensi.sh -h   (bantuan)"
}

# Jika -h
if [ "$1" = "-h" ]; then
    usage
    exit 0
fi

# Jika -r (rekap)
if [ "$1" = "-r" ]; then

    if [ ! -f "$FILE" ]; then
        echo "Belum ada data absensi."
        exit 1
    fi

    echo "=== REKAP ABSENSI ==="

    HADIR=$(grep -c "hadir" "$FILE")
    IZIN=$(grep -c "izin" "$FILE")
    ALPHA=$(grep -c "alpha" "$FILE")

    echo "Hadir : $HADIR"
    echo "Izin  : $IZIN"
    echo "Alpha : $ALPHA"

    exit 0
fi

NAMA=$1
STATUS=$2

# Validasi input kosong
if [ -z "$NAMA" ] || [ -z "$STATUS" ]; then
    usage
    exit 1
fi

# Validasi status
if [[ "$STATUS" != "hadir" &&
      "$STATUS" != "izin" &&
      "$STATUS" != "alpha" ]]; then
    echo "Status harus: hadir / izin / alpha"
    exit 1
fi

JAM=$(date '+%H:%M')

echo "[$JAM] $NAMA - $STATUS" >> "$FILE"

echo "Absensi berhasil dicatat."
```
Output:
```bash

reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ chmod +x absensi.sh
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./absensi.sh Budi hadir
Absensi berhasil dicatat.
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./absensi.sh Andi izin
Absensi berhasil dicatat.
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./absensi.sh Citra alpha
Absensi berhasil dicatat.
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./absensi.sh Deni hadir
Absensi berhasil dicatat.
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./absensi.sh Eka hadir
Absensi berhasil dicatat.
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ cat ~/praktikum-os/week09/logs/absensi-$(date +%F).txt
[14:59] Budi - hadir
[14:59] Andi - izin
[14:59] Citra - alpha
[15:00] Deni - hadir
[15:00] Eka - hadir
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./absensi.sh -r
=== REKAP ABSENSI ===
Hadir : 3
Izin  : 1
Alpha : 1
```
## Tugas 2 Script Health Check Sistem
Konteks: administrator membuat pemeriksaan kondisi server sebelum maintenance.
Instruksi:
1. Buat script healthcheck.sh menggunakan template profesional dari bagian
Best Practices.
2. Script menampilkan: tanggal/waktu, hostname, uptime, penggunaan CPU,
memori, dan disk untuk setiap filesystem yang terpasang.
3. Jika penggunaan disk mana pun melebihi 80%, tampilkan peringatan.
4. Simpan hasil ke healthcheck-YYYY-MM-DD.log dan tampilkan ke terminal
sekaligus menggunakan tee.
5. Opsi -t <persen> mengubah batas peringatan disk (default 80).
Konsep wajib: set -euo pipefail, trap, getopts, fungsi dengan local,
for, if, dan tee.

Jawab:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ nano healthcheck.sh
```
skripnya
```bash
#!/bin/bash

set -euo pipefail

BATAS=80

# Membaca opsi
while getopts "t:" OPSI; do
    case $OPSI in
        t)
            BATAS="$OPTARG"
            ;;
        *)
            echo "Penggunaan: $0 [-t persen]"
            exit 1
            ;;
    esac
done

shift $((OPTIND - 1))

TANGGAL=$(date '+%F')
LOGFILE="$HOME/praktikum-os/week09/logs/healthcheck-$TANGGAL.log"

echo "=== HEALTH CHECK SYSTEM ==="

{
echo "Tanggal   : $(date)"
echo "Hostname  : $(hostname)"
echo "Uptime    : $(uptime -p)"

echo ""
echo "=== CPU ==="
nproc

echo ""
echo "=== MEMORY ==="
free -h

echo ""
echo "=== DISK ==="

df -h | while read line
do
    echo "$line"
done

echo ""
echo "=== CEK BATAS DISK ==="

df -h --output=pcent,target | tail -n +2 | while read persen mount
do
    persen_angka=$(echo "$persen" | tr -d '%')

    if [ "$persen_angka" -gt "$BATAS" ]; then
        echo "PERINGATAN: Disk $mount melebihi ${BATAS}%"
    fi

done

} | tee "$LOGFILE"
```
```bash
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./healthcheck.sh
=== HEALTH CHECK SYSTEM ===
Tanggal   : Thu Apr 23 03:08:09 PM UTC 2026
Hostname  : reyhandhika
Uptime    : up 1 hour, 13 minutes

=== CPU ===
1

=== MEMORY ===
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       308Mi       1.5Gi       1.1Mi       288Mi       1.6Gi
Swap:          2.0Gi          0B       2.0Gi

=== DISK ===
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.7G  5.0G  54% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  198M  1.6G  11% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

=== CEK BATAS DISK ===
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ~/praktikum-os/week09/logs/
-bash: /home/reyhandhika/praktikum-os/week09/logs/: Is a directory
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ls ~/praktikum-os/week09/logs
absensi-2026-04-23.txt
backup-data-2026-04-23-142037
backup-data-2026-04-23-142101.tar.gz
backup.log
healthcheck-2026-04-23.log
reyhandhika@reyhandhika:~/praktikum-os/week09/scripts$ ./healthcheck.sh -t 50
=== HEALTH CHECK SYSTEM ===
Tanggal   : Thu Apr 23 03:10:03 PM UTC 2026
Hostname  : reyhandhika
Uptime    : up 1 hour, 14 minutes

=== CPU ===
1

=== MEMORY ===
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       308Mi       1.5Gi       1.1Mi       288Mi       1.6Gi
Swap:          2.0Gi          0B       2.0Gi

=== DISK ===
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.7G  5.0G  54% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  198M  1.6G  11% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000

=== CEK BATAS DISK ===
PERINGATAN: Disk / melebihi 50%
```