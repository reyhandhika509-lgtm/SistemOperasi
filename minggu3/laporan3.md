# laporan Praktikum 3

<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

# Latihan 

## Latihan 3.1


Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log

### Jawaban  

Kode :  
```bash
echo "===== Mencari 10 file terbesar di /var/log/ ====="
echo "Waktu: $(date)"
echo "----------------------------------------"

find /var/log/ -type f -exec ls -lh {} \; 2> error.log | sort -k5 -rh | head -10 | tee large-logs.txt

echo "----------------------------------------"
echo "Hasil disimpan di: large-logs.txt"
echo "Error disimpan di: error.log"
```

Output :
'''bash
===== Mencari 10 file terbesar di /var/log/ =====
Waktu: Sun Mar  1 02:53:00 AM UTC 2026
----------------------------------------
-rw-r-----+ 1 root systemd-journal 8.0M Mar  4 03:55 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/user-1000.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  4 03:55 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/system.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  4 03:23 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/system@00064c2a5d87cb03-606cda5a20a776ed.journal~
-rw-r-----+ 1 root systemd-journal 8.0M Mar  4 03:20 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/user-1000@00064c2a5f389196-2eedd43e93acd206.journal~
-rw-r-----+ 1 root systemd-journal 8.0M Mar  3 06:47 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/user-1000@c20e50f0bf7548feaeac68240958d6fe-00000000000025ea-00064c19128abd8e.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  3 06:47 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/system@c20e50f0bf7548feaeac68240958d6fe-0000000000002279-00064c191086ada3.journal
-rw-r-----+ 1 root systemd-journal 8.0M Mar  3 06:47 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/system@00064c2a486a43ad-b4ef30551834e3e7.journal~
-rw-r-----+ 1 root systemd-journal 8.0M Mar  3 06:45 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/system@00064c1910a3f151-6a7d8d0a2304264d.journal~
-rw-r-----+ 1 root systemd-journal 8.0M Mar  3 06:44 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/user-1000@00064c19128ac587-3e6d4c711a66150a.journal~
-rw-r-----+ 1 root systemd-journal 8.0M Mar  3 06:43 /var/log/journal/c06b54c3aaac4285a49bbeb4cecc6fed/user-1000@826085e1cda847cbb25c43de54150b31-0000000000002248-00064c19062d47a1.journal
----------------------------------------
Hasil disimpan di: large-logs.txt
Error disimpan di: error.log
```

## Latihan 3.2

Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.

### Jawaban :    

Kode :  
```bash
cat /etc/passwd | cut -d: -f1 | sort | tee sorted-users.txt
```