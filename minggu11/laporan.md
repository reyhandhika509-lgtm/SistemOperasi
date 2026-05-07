<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

### Praktikum 9.1 — Permissions
Tujuan: membaca permission, mengubahnya dengan aman, dan memahami efek chmod,chown, serta umask pada file nyata.

Langkah 1: Buat direktori kerja dan dua file uji
```bash
mkdir ~/lab-permissions && cd ~/lab-permissions
echo "data rahasia" > secret.txt
echo '#!/bin/bash' > myscript.sh
echo 'echo Hello' >> myscript.sh
ls -la
```
Output:
```bash
reyhandhika@reyhandhika:~$ mkdir ~/lab-permissions && cd ~/lab-permissions
reyhandhika@reyhandhika:~/lab-permissions$ echo "data rahasia" > secret.txt
reyhandhika@reyhandhika:~/lab-permissions$ echo '#!/bin/bash' > myscript.sh
reyhandhika@reyhandhika:~/lab-permissions$ echo 'echo Hello' >> myscript.sh
reyhandhika@reyhandhika:~/lab-permissions$
reyhandhika@reyhandhika:~/lab-permissions$ ls -la
total 16
drwxrwxr-x  2 reyhandhika reyhandhika 4096 May  6 06:22 .
drwxr-x--- 10 reyhandhika reyhandhika 4096 May  6 06:22 ..
-rw-rw-r--  1 reyhandhika reyhandhika   23 May  6 06:22 myscript.sh
-rw-rw-r--  1 reyhandhika reyhandhika   13 May  6 06:22 secret.txt
reyhandhika@reyhandhika:~/lab-permissions$
```
Perhatikan permission awal kedua file. Biasanya file baru tidak memiliki bit execute.

Langkah 2: Jadikan secret.txt privat hanya untuk owner
```bash
chmod 600 secret.txt
ls -l secret.txt
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-permissions$ ls -l secret.txt
-rw------- 1 reyhandhika reyhandhika 13 May  6 06:22 secret.txt
reyhandhika@reyhandhika:~/lab-permissions$

```
Permission 600 berarti owner dapat membaca dan menulis, sedangkan group dan others tidak memiliki akses.

Langkah 3: Jadikan myscript.sh dapat dijalankan
```bash
chmod 755 myscript.sh
ls -l myscript.sh
./myscript.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-permissions$ ls -l myscript.sh
-rwxr-xr-x 1 reyhandhika reyhandhika 23 May  6 06:22 myscript.sh
reyhandhika@reyhandhika:~/lab-permissions$ ./myscript.sh
Hello
reyhandhika@reyhandhika:~/lab-permissions$
```
Permission 755 memberi hak penuh ke owner, dan hak baca+execute ke group serta others. Tanpa bit execute, file skrip tidak bisa dijalankan langsung.

Langkah 4: Buat direktori bersama dan amati efek SGID sederhana
```bash
mkdir shared-dir
chmod g+s shared-dir
ls -ld shared-dir
```
output:
```bash
reyhandhika@reyhandhika:~/lab-permissions$ mkdir shared-dir
reyhandhika@reyhandhika:~/lab-permissions$ chmod g+s shared-dir
reyhandhika@reyhandhika:~/lab-permissions$ ls -ld shared-dir
drwxrwsr-x 2 reyhandhika reyhandhika 4096 May  6 06:26 shared-dir
reyhandhika@reyhandhika:~/lab-permissions$
```
Jika output menampilkan huruf s pada posisi group execute, berarti SGID aktif.

Langkah 5: Uji efek umask pada file baru.
```bash
umask
umask 027
touch testfile-027
ls -l testfile-027
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-permissions$ umask
0002
reyhandhika@reyhandhika:~/lab-permissions$ umask 027
reyhandhika@reyhandhika:~/lab-permissions$ touch testfile-027
reyhandhika@reyhandhika:~/lab-permissions$ ls -l testfile-027
-rw-r----- 1 reyhandhika reyhandhika 0 May  6 06:27 testfile-027
reyhandhika@reyhandhika:~/lab-permissions$
```
Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?  
Jawaban: Artinya hanya pemilik file (owner) yang memiliki hak membaca (r) dan menulis (w), sedangkan group dan others tidak memiliki izin apa pun. Oleh sebab itu user lain selain owner tidak dapat membuka maupun membaca secret.txt.
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?  
Jawaban: Permission 600 digunakan untuk file privat karena hanya owner yang memiliki akses, sedangkan 755 digunakan agar file dapat dijalankan karena memiliki izin execute.
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?  
Jawaban: Setelah umask 027, file baru memiliki permission 640 karena file reguler Linux default-nya dimulai dari 666, bukan 777, sehingga izin execute tidak otomatis diberikan.

Tantangan
Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan perubahan output ls -l sebelum dan sesudahnya.
```bash
reyhandhika@reyhandhika:~/lab-permissions$ sudo useradd -m userA
[sudo] password for reyhandhika:
reyhandhika@reyhandhika:~/lab-permissions$ sudo chown userA secret.txt
reyhandhika@reyhandhika:~/lab-permissions$ ls -l secret.txt
-rw------- 1 userA reyhandhika 13 May  6 06:37 secret.txt
reyhandhika@reyhandhika:~/lab-permissions$ ls -l
total 12
-rwxr-xr-x 1 reyhandhika reyhandhika   23 May  6 06:22 myscript.sh
-rw------- 1 userA       reyhandhika   13 May  6 06:37 secret.txt
drwxrwsr-x 2 reyhandhika reyhandhika 4096 May  6 06:26 shared-dir
-rw-r----- 1 reyhandhika reyhandhika    0 May  6 06:27 testfile-027
reyhandhika@reyhandhika:~/lab-permissions$
```

### Praktikum 9.2 — ACL
Tujuan: memahami ACL dari nol: melihat kondisi awal, menambah akses untuk satu user, lalu membuat direktori yang mewariskan ACL otomatis.

dilangkah ini saya belum menginstal installl ACL Terlebih dahulu
```bash
sudo apt install -y acl
```
Langkah 1: Siapkan file dan lihat permission standar tanpa ACL tambahan.
```bash
mkdir ~/lab-acl && cd ~/lab-acl
echo "Data penting" > confidential.txt
chmod 640 confidential.txt
ls -l confidential.txt
getfacl confidential.txt
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo apt install -y acl
[sudo] password for reyhandhika:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
acl is already the newest version (2.3.2-1build1.1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
reyhandhika@reyhandhika:~$ mkdir ~/lab-acl && cd ~/lab-acl
mkdir: cannot create directory ‘/home/reyhandhika/lab-acl’: File exists
reyhandhika@reyhandhika:~$ echo "Data penting" > confidential.txt
reyhandhika@reyhandhika:~$ chmod 640 confidential.txt
reyhandhika@reyhandhika:~$ ls -l confidential.txt
-rw-r----- 1 reyhandhika reyhandhika 13 May  7 02:03 confidential.txt
reyhandhika@reyhandhika:~$ getfacl confidential.txt
# file: confidential.txt
# owner: reyhandhika
# group: reyhandhika
user::rw-
group::r--
other::---

reyhandhika@reyhandhika:~$
```
Pada tahap ini, getfacl hanya menampilkan tiga entri dasar: owner, group, dan others. Belum ada named user atau named group.
Langkah 2: Beri akses baca ke satu user tertentu tanpa mengubah owner atau group.
```bash
setfacl -m u:userA:r confidential.txt
ls -l confidential.txt
getfacl confidential.txt
```
Output:
```bash
reyhandhika@reyhandhika:~$ setfacl -m u:userA:r confidential.txt
reyhandhika@reyhandhika:~$ ls -l confidential.txt
-rw-r-----+ 1 reyhandhika reyhandhika 13 May  7 02:03 confidential.txt
reyhandhika@reyhandhika:~$ getfacl confidential.txt
# file: confidential.txt
# owner: reyhandhika
# group: reyhandhika
user::rw-
user:userA:r--
group::r--
mask::r--
other::---
reyhandhika@reyhandhi
```
Perhatikan dua perubahan:
• output ls -l menampilkan tanda +;
• output getfacl kini memiliki entri user:userA:r–.

Langkah 3: Buat direktori bersama yang mewariskan ACL ke file baru.
```bash
mkdir shared
setfacl -d -m u:userA:rwx shared
setfacl -d -m u:userB:r-x shared
getfacl shared
touch shared/inherited.txt
getfacl shared/inherited.txt
```
Output:
```bash
reyhandhika@reyhandhika:~$ mkdir shared
reyhandhika@reyhandhika:~$ setfacl -d -m u:userA:rwx shared
reyhandhika@reyhandhika:~$ setfacl -d -m u:userB:r-x shared
setfacl: Option -m: Invalid argument near character 3
reyhandhika@reyhandhika:~$ getfacl shared
# file: shared
# owner: reyhandhika
# group: reyhandhika
user::rwx
group::rwx
other::r-x
default:user::rwx
default:user:userA:rwx
default:group::rwx
default:mask::rwx
default:other::r-x

reyhandhika@reyhandhika:~$ touch shared/inherited.txt
reyhandhika@reyhandhika:~$ getfacl shared/inherited.txt
# file: shared/inherited.txt
# owner: reyhandhika
# group: reyhandhika
user::rw-
user:userA:rwx                  #effective:rw-
group::rwx                      #effective:rw-
mask::rw-
other::r--

reyhandhika@reyhandhika:~$
```
Analisis
1.  Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?    
jawaban:Karena file confidential.txt awalnya hanya menggunakan permission standar Linux sehingga getfacl hanya menampilkan owner, group, dan others tanpa ACL tambahan untuk user tertentu.

2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?    
jawaban: Setelah ACL ditambahkan, output ls -l menampilkan tanda + di akhir permission yang menandakan adanya ACL tambahan. Sedangkan getfacl menampilkan entri baru berupa permission khusus untuk userA.

3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?    
jawaban: Karena direktori shared memiliki default ACL (setfacl -d) sehingga setiap file baru yang dibuat di dalam direktori tersebut otomatis mewarisi aturan ACL yang sudah ditetapkan.

Tantangan 
Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt. Setelah itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.

```bash
# tambahkan ACL untuk group readonly-group
setfacl -m g:readonly-group:r confidential.txt
# cek hasil ACL
getfacl confidential.txt
# hapus ACL untuk userA
setfacl -x u:userA confidential.txt
# Verifikasi hasil akhir
getfacl confidential.txt
```
Jawaban: Setelah ACL ditambahkan, group readonly-group hanya memiliki izin membaca file confidential.txt. Kemudian ACL milik userA dihapus sehingga hanya ACL group yang tersisa pada file tersebut.

### Praktikum 9.3A — Membuat dan Mengelola User
Tujuan: membuat user baru, memodifikasi propertinya, dan memahami perbedaan opsi useradd dan usermod.
```bash
# buat dua user
sudo useradd -m -s /bin/bash userA
sudo useradd -m -s /bin/bash userB
sudo passwd userA
sudo passwd userB

# verifikasi
id userA
getent passwd userA

# modifikasi shell userA
sudo usermod -s /bin/zsh userA
getent passwd userA

#lock dan unlock userB
sudo usermod -L userB
sudo passwd -S userB
sudo usermod -U userB
sudo passwd -S userB
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo useradd -m -s /bin/bash userA
[sudo] password for reyhandhika:
useradd: user 'userA' already exists
reyhandhika@reyhandhika:~$ sudo useradd -m -s /bin/bash userA
sudo useradd -m -s /bin/bash userB
useradd: user 'userA' already exists
reyhandhika@reyhandhika:~$ sudo passwd userA
New password:
Retype new password:
passwd: password updated successfully
reyhandhika@reyhandhika:~$ sudo passwd userB
New password:
Retype new password:
passwd: password updated successfully
reyhandhika@reyhandhika:~$ id userA
uid=1001(userA) gid=1001(userA) groups=1001(userA)
reyhandhika@reyhandhika:~$ getent passwd userA
userA:x:1001:1001::/home/userA:/bin/sh
reyhandhika@reyhandhika:~$ sudo usermod -s /bin/zsh userA
usermod: Warning: missing or non-executable shell '/bin/zsh'
reyhandhika@reyhandhika:~$ getent passwd userA
userA:x:1001:1001::/home/userA:/bin/zsh
reyhandhika@reyhandhika:~$ sudo usermod -L userB
reyhandhika@reyhandhika:~$ sudo passwd -S userB
userB L 2026-05-07 0 99999 7 -1
reyhandhika@reyhandhika:~$ sudo usermod -U userB
reyhandhika@reyhandhika:~$ sudo passwd -S userB
userB P 2026-05-07 0 99999 7 -1
reyhandhika@reyhandhika:~$
```
Pertanyaan:
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?  
Jawaban: Sebelum ditambahkan ke group lain, output id userA hanya menampilkan primary group milik userA. Setelah ditambahkan ke group tambahan, output id userA menampilkan beberapa group yang diikuti userA sehingga hak akses user menjadi lebih banyak sesuai group yang dimiliki.
2. Bagaimana status passwd -S userB berubah saat akun di-lock?  
Jawaban: Saat akun di-lock menggunakan usermod -L atau passwd -l, status pada passwd -S userB berubah menjadi terkunci yang menandakan user tidak dapat melakukan login sampai akun di-unlock kembali.

### Praktikum 9.3B — Group Management
Tujuan: membuat group, menambahkan user ke group, dan memverifikasi keanggotaan
```bash
# buat dua group
sudo groupadd labgroup
sudo groupadd readonly-group

# tambahkan userA kedua group
sudo usermod -aG labgroup,readonly-group userA

# tambahkan userB hanya ke readonly-group
sudo usermod -aG readonly-group userB

# verifikasi
id userA
id userB
getent group labgroup
getent group readonly-group
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo groupadd labgroup
reyhandhika@reyhandhika:~$ sudo groupadd readonly-group
reyhandhika@reyhandhika:~$ sudo usermod -aG labgroup,readonly-group userA
reyhandhika@reyhandhika:~$ sudo usermod -aG readonly-group userB
reyhandhika@reyhandhika:~$ id userA
uid=1001(userA) gid=1001(userA) groups=1001(userA),1003(labgroup),1004(readonly-group)
reyhandhika@reyhandhika:~$ id userB
uid=1002(userB) gid=1002(userB) groups=1002(userB),1004(readonly-group)
reyhandhika@reyhandhika:~$ getent group labgroup
labgroup:x:1003:userA
reyhandhika@reyhandhika:~$ getent group readonly-group
readonly-group:x:1004:userA,userB
reyhandhika@reyhandhika:~$
```
Pertanyaan:
1. Apa yang ditampilkan id userA vs groups userA?  
Jawaban:  Perintah id userA menampilkan informasi lengkap user seperti UID, GID, dan seluruh group yang dimiliki user. Sedangkan groups userA hanya menampilkan daftar group yang diikuti oleh user tersebut.
2. Mengapa -a pada usermod -aG penting?  
Jawaban: Karena opsi -a berfungsi menambahkan group baru tanpa menghapus group lama. Jika hanya menggunakan -G tanpa -a, maka seluruh group sebelumnya akan terganti oleh group baru yang dimasukkan.

### Praktikum 9.3C — Password Aging Policy
Tujuan: menerapkan kebijakan umur password dan mengamati efeknya.
```bash
# set aging policy untuk userA
sudo chage -M 60 -W 7 -m 1 userA
sudo chage -l userA
# paksa userA ganti password saat login pertama
sudo chage -d 0 userA

# kunci password userB
sudo passwd -l userB
sudo passwd -S userB

# unlock kembali
sudo passwd -u userB
sudo passwd -S userB
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo chage -M 60 -W 7 -m 1 userA
reyhandhika@reyhandhika:~$ sudo chage -l userA
Last password change                                    : May 07, 2026
Password expires                                        : Jul 06, 2026
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 1
Maximum number of days between password change          : 60
Number of days of warning before password expires       : 7
reyhandhika@reyhandhika:~$ sudo chage -d 0 userA
reyhandhika@reyhandhika:~$ sudo passwd -l userB
passwd: password changed.
reyhandhika@reyhandhika:~$ sudo passwd -S userB
userB L 2026-05-07 0 99999 7 -1
reyhandhika@reyhandhika:~$ sudo passwd -u userB
passwd: password changed.
reyhandhika@reyhandhika:~$ sudo passwd -S userB
userB P 2026-05-07 0 99999 7 -1
reyhandhika@reyhandhika:~$
```

Pertanyaan:
1. Apa arti nilai yang ditampilkan chage -l userA?  
Jawaban: Output chage -l userA menampilkan informasi kebijakan password seperti tanggal terakhir ganti password, masa berlaku password, batas minimum pergantian password, waktu peringatan sebelum expired, dan tanggal akun berakhir.
2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?   
Jawaban: Saat akun dikunci, output passwd -S userB akan menunjukkan status L (Locked). Status tersebut menandakan password akun dinonaktifkan sehingga user tidak dapat login.
3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?  
jawaban: chage -d 0 digunakan untuk memaksa user mengganti password pada login berikutnya melalui pengaturan tanggal password terakhir menjadi nol. Sedangkan passwd -e digunakan untuk langsung membuat password menjadi expired. Keduanya memiliki tujuan serupa tetapi chage lebih sering digunakan dalam administrasi kebijakan password.

Tantangan
Buat user bernama intern yang:
• memiliki shell /bin/bash;
• menjadi anggota labgroup;
• dipaksa ganti password pada login pertama;
• password expired setelah 45 hari dengan warning 7 hari sebelumnya
```bash
# Buat user intern
sudo useradd -m -s /bin/bash intern
# Tambahkan ke group labgroup
sudo usermod -aG labgroup intern
# Buat password
sudo passwd intern
# Paksa ganti password saat login pertama
sudo chage -d 0 intern
# Atur password expired 45 hari dan warning 7 hari
sudo chage -M 45 -W 7 intern
# verifikasi
sudo chage -l intern
id intern
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo useradd -m -s /bin/bash intern
[sudo] password for reyhandhika:
reyhandhika@reyhandhika:~$ sudo usermod -aG labgroup intern
reyhandhika@reyhandhika:~$ sudo passwd intern
New password:
Retype new password:
passwd: password updated successfully
reyhandhika@reyhandhika:~$ sudo chage -d 0 intern
reyhandhika@reyhandhika:~$ sudo chage -M 45 -W 7 intern
reyhandhika@reyhandhika:~$ sudo chage -l intern
Last password change                                    : password must be changed
Password expires                                        : password must be changed
Password inactive                                       : password must be changed
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 7
reyhandhika@reyhandhika:~$ id intern
uid=1003(intern) gid=1005(intern) groups=1005(intern),1003(labgroup)
reyhandhika@reyhandhika:~$
```
Jawaban: User intern dibuat menggunakan shell /bin/bash dan ditambahkan ke group labgroup menggunakan perintah usermod -aG. Setelah itu password user diatur agar wajib diganti saat login pertama menggunakan chage -d 0. Kebijakan password juga diterapkan dengan masa berlaku password selama 45 hari dan peringatan 7 hari sebelum password expired menggunakan chage -M 45 -W 7. Konfigurasi tersebut bertujuan meningkatkan keamanan akun serta memastikan user mengikuti kebijakan password sistem.

### Praktikum 9.4 — Konfigurasi sudo
Tujuan: membuat aturan sudo terbatas, memverifikasi hak akses, dan membaca log.
Langkah 1: Buat file konfigurasi sudo khusus untuk userA.
```bash
sudo visudo -f /etc/sudoers.d/lab-userA
```
perintah ini membuka editor aman khusus untuk file sudoers baru. Jika sintaks salah, visudo akan memperingatkan sebelum file disimpan.
Isi file dengan aturan berikut:
```bash
userA ALL=(root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
userA ALL=(root) /bin/systemctl status *
# verifikasi
sudo -l -U userA
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo visudo -f /etc/sudoers.d/lab-userA
reyhandhika@reyhandhika:~$ sudo -l -U userA
Matching Defaults entries for userA on reyhandhika:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User userA may run the following commands on reyhandhika:
    (root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
    (root) /bin/systemctl status *
reyhandhika@reyhandhika:~$
```
Baris pertama berarti userA boleh menjalankan dua perintah apt tanpa password. Baris kedua berarti userA boleh melihat status service apa pun, tetapi tetap mengikuti kebijakan autentikasi normal.

Langkah 2: Verifikasi aturan yang aktif dan uji hasilnya.
```bash
sudo -l -U userA
sudo grep "userA" /var/log/auth.log | tail -10
```
sudo -l -U userA dipakai untuk mengecek aturan yang aktif dari sudut pandang akun userA. Log di
/var/log/auth.log membantu memverifikasi bahwa pemakaian sudo benar-benar tercatat.

Output:
```bash
reyhandhika@reyhandhika:~$ sudo -l -U userA
Matching Defaults entries for userA on reyhandhika:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User userA may run the following commands on reyhandhika:
    (root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
    (root) /bin/systemctl status *
reyhandhika@reyhandhika:~$ sudo grep "userA" /var/log/auth.log | tail -10
2026-05-07T02:15:19.139395+00:00 reyhandhika usermod[3026]: add 'userA' to shadow group 'labgroup'
2026-05-07T02:15:19.140219+00:00 reyhandhika usermod[3026]: add 'userA' to shadow group 'readonly-group'
2026-05-07T02:16:24.379043+00:00 reyhandhika sudo: reyhandhika : TTY=pts/0 ; PWD=/home/reyhandhika ; USER=root ; COMMAND=/usr/bin/chage -M 60 -W 7 -m 1 userA
2026-05-07T02:16:24.445689+00:00 reyhandhika chage[3048]: changed password expiry for userA
2026-05-07T02:16:29.288783+00:00 reyhandhika sudo: reyhandhika : TTY=pts/0 ; PWD=/home/reyhandhika ; USER=root ; COMMAND=/usr/bin/chage -l userA
2026-05-07T02:16:38.272592+00:00 reyhandhika sudo: reyhandhika : TTY=pts/0 ; PWD=/home/reyhandhika ; USER=root ; COMMAND=/usr/bin/chage -d 0 userA
2026-05-07T02:16:38.340717+00:00 reyhandhika chage[3057]: changed password expiry for userA
2026-05-07T02:21:40.554899+00:00 reyhandhika sudo: reyhandhika : TTY=pts/1 ; PWD=/home/reyhandhika ; USER=root ; COMMAND=/usr/sbin/visudo -f /etc/sudoers.d/lab-userA
2026-05-07T02:23:32.109924+00:00 reyhandhika sudo: reyhandhika : TTY=pts/1 ; PWD=/home/reyhandhika ; USER=root ; COMMAND=/usr/sbin/visudo -f /etc/sudoers.d/lab-userA
2026-05-07T02:24:50.400612+00:00 reyhandhika sudo: reyhandhika : TTY=pts/1 ; PWD=/home/reyhandhika ; USER=root ; COMMAND=/usr/bin/grep userA /var/log/auth.log
reyhandhika@reyhandhika:~$
```
Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?  
Jawaban: Karena penyimpanan aturan di /etc/sudoers.d/ lebih aman dan rapi untuk memisahkan konfigurasi tambahan tanpa mengubah file utama /etc/sudoers. Cara ini juga memudahkan pengelolaan dan mengurangi risiko kerusakan konfigurasi utama.
2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?  
Jawaban: Perintah apt update dan apt upgrade dapat dijalankan tanpa password karena menggunakan opsi NOPASSWD. Sedangkan systemctl status tetap memerlukan autentikasi sesuai kebijakan sudo normal.
3. Informasi apa saja yang dicatat di log sudo?  
Jawaban: Log sudo mencatat informasi seperti nama user yang menjalankan perintah, waktu eksekusi, terminal yang digunakan, direktori kerja, dan perintah yang dijalankan menggunakan sudo.

Tantangan
Tambahkan satu aturan baru agar userA boleh menjalankan /bin/systemctl restart ssh tetapi tidak boleh
menjalankan reboot.
```bash
sudo visudo -f /etc/sudoers.d/lab-userA
userA ALL=(root) /bin/systemctl restart ssh
sudo -l -U userA
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo visudo -f /etc/sudoers.d/lab-userA
reyhandhika@reyhandhika:~$ sudo -l -U userA
Matching Defaults entries for userA on reyhandhika:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User userA may run the following commands on reyhandhika:
    (root) NOPASSWD: /usr/bin/apt update, /usr/bin/apt upgrade
    (root) /bin/systemctl status *
    (root) /bin/systemctl restart ssh
reyhandhika@reyhandhika:~$
```
### Praktikum 9.5 — Disk Quota
Tujuan: memahami alur quota secara aman pada loopback filesystem tanpa mengubah filesystem utama.

dikarenakan saya belum menginstall quota
```bash
sudo apt install -y quota quotatool
```
Langkah 1: Buat image filesystem kecil dan mount dengan opsi quota.
```bash
sudo dd if=/dev/zero of=/tmp/quota-test.img bs=1M count=100
sudo mkfs.ext4 /tmp/quota-test.img
sudo mkdir -p /mnt/quota-test
sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo dd if=/dev/zero of=/tmp/quota-test.img bs=1M count=100
100+0 records in
100+0 records out
104857600 bytes (105 MB, 100 MiB) copied, 0.539186 s, 194 MB/s
reyhandhika@reyhandhika:~$ sudo mkfs.ext4 /tmp/quota-test.img
mke2fs 1.47.0 (5-Feb-2023)
Discarding device blocks: done
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done
Writing inode tables: done
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done

reyhandhika@reyhandhika:~$ sudo mkdir -p /mnt/quota-test
reyhandhika@reyhandhika:~$ sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
reyhandhika@reyhandhika:~$
```
Image file dipakai agar praktikum aman: Anda tidak perlu memodifikasi filesystem utama seperti /home/. Opsi
usrquota,grpquota mengaktifkan dua jenis quota sekaligus.
Langkah 2: Buat database quota dan aktifkan enforcement.
```bash
sudo quotacheck -cug /mnt/quota-test
sudo quotaon -v /mnt/quota-test
sudo repquota /mnt/quota-test
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo mkdir -p /mnt/quota-test
reyhandhika@reyhandhika:~$ sudo mount -o loop,usrquota,grpquota /tmp/quota-test.img /mnt/quota-test
reyhandhika@reyhandhika:~$ sudo quotacheck -cug /mnt/quota-test
reyhandhika@reyhandhika:~$ sudo quotaon -v /mnt/quota-test
quotaon: Your kernel probably supports ext4 quota feature but you are using external quota files. Please switch your filesystem to use ext4 quota feature as external quota files on ext4 are deprecated.
/dev/loop0 [/mnt/quota-test]: group quotas turned on
/dev/loop0 [/mnt/quota-test]: user quotas turned on
reyhandhika@reyhandhika:~$ sudo repquota /mnt/quota-test
*** Report for user quotas on device /dev/loop0
Block grace time: 7days; Inode grace time: 7days
                        Block limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
----------------------------------------------------------------------
root      --      20       0       0              2     0     0  


reyhandhika@reyhandhika:~$
```
quotacheck -cug membuat database user dan group quota. Setelah itu, quotaon mengaktifkan enforcement,
dan repquota menampilkan laporan awal.
Langkah 3: Tetapkan quota untuk user uji dan amati hasilnya.
```bash
sudo edquota -u userA
# contoh : soft block 5120 , hard block 10240
sudo repquota /mnt/quota-test
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo edquota -u userA
reyhandhika@reyhandhika:~$ sudo repquota /mnt/quota-test
*** Report for user quotas on device /dev/loop0
Block grace time: 7days; Inode grace time: 7days
                        Block limits                File limits
User            used    soft    hard  grace    used  soft  hard  grace
----------------------------------------------------------------------
root      --      20       0       0              2     0     0  


reyhandhika@reyhandhika:~$
```
Nilai di atas memakai satuan KB. Jadi 5120 berarti sekitar 5 MB, dan 10240 berarti sekitar 10 MB.
Langkah 4: Bersihkan lingkungan uji setelah selesai.
```bash
sudo quotaoff /mnt/quota-test
sudo umount /mnt/quota-test
sudo rm /tmp/quota-test.img
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo quotaoff /mnt/quota-test
reyhandhika@reyhandhika:~$ sudo umount /mnt/quota-test
reyhandhika@reyhandhika:~$ sudo rm /tmp/quota-test.img
reyhandhika@reyhandhika:~$
```
Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?  
Jawaban: Soft limit masih dapat dilampaui sementara selama masa grace period, sedangkan hard limit tidak dapat dilampaui sama sekali karena sistem langsung menolak penggunaan tambahan ruang disk atau inode.
2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?  
Jawaban: Karena loopback filesystem lebih aman untuk percobaan sehingga tidak memengaruhi filesystem utama sistem. Dengan cara ini konfigurasi quota dapat diuji tanpa risiko merusak data pengguna pada /home/.
3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?  
Jawaban: Quota dianggap aktif apabila output repquota menampilkan daftar penggunaan block dan inode user beserta batas soft limit dan hard limit yang berlaku pada filesystem tersebut.

Tantangan
Coba atur quota baru untuk userA dengan batas inode yang sangat kecil, kemudian jelaskan kapan pembatasan
inode lebih penting daripada pembatasan block
```bash
sudo setquota -u userA 5120 10240 5 10 /mnt/quota-test
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo setquota -u userA 5120 10240 5 10 /mnt/quota-test
setquota: Mountpoint (or device) /mnt/quota-test not found or has no quota enabled.
setquota: Not all specified mountpoints are using quota.
reyhandhika@reyhandhika:~$
```
## Latihan Latihan 9.A — Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan
tiga file yang Anda kenali beserta alasannya.
```bash
find / -perm -4000 -type f 2>/dev/null
```
Output:
```bash
reyhandhika@reyhandhika:~$ find / -perm -4000 -type f 2>/dev/null







^Z
[1]+  Stopped                 find / -perm -4000 -type f 2> /dev/null
```
jawaban: File SUID memungkinkan program dijalankan menggunakan hak akses owner file, biasanya root. Contoh file yang umum ditemukan adalah:
/usr/bin/passwd digunakan agar user biasa dapat mengubah password pada file sistem.
/usr/bin/sudo digunakan untuk menjalankan perintah dengan hak administrator.
/usr/bin/su digunakan untuk berpindah user atau menjadi root.

2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
```bash
find / -type d -perm -0002 2>/dev/null
```
Output:
```bash
reyhandhika@reyhandhika:~$ find / -type d -perm -0002 2>/dev/null
/run/screen
/run/lock
/var/tmp
/var/crash
/tmp
/tmp/.X11-unix
/tmp/.ICE-unix
/tmp/.XIM-unix
/tmp/.font-unix
/dev/mqueue
/dev/shm
reyhandhika@reyhandhika:~$
```
Jawaban: Direktori world-writable adalah direktori yang dapat ditulis semua user. Direktori seperti /tmp termasuk valid karena digunakan untuk file sementara dan biasanya memiliki sticky bit. Namun direktori world-writable tanpa sticky bit berisiko karena user lain dapat menghapus atau memodifikasi file milik pengguna lain.

3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar
group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi
group proyek
```bash
#Membuat direktori
sudo mkdir -p /srv/webapp
# Set owner dan group
sudo chown root:webapp-team /srv/webapp
# Set permission SGID
sudo chmod 2775 /srv/webapp
# Tambahkan ACL deploy hanya baca
sudo setfacl -m u:deploy:r-x /srv/webapp

# Default ACL agar file baru mewarisi ACL
sudo setfacl -d -m g:webapp-team:rwx /srv/webapp
sudo setfacl -d -m u:deploy:r-x /srv/webapp

# verifikasi
getfacl /srv/webapp
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo groupadd webapp-team
reyhandhika@reyhandhika:~$ sudo useradd -m deploy
reyhandhika@reyhandhika:~$ sudo chown root:webapp-team /srv/webapp
reyhandhika@reyhandhika:~$ sudo setfacl -m u:deploy:r-x /srv/webapp
reyhandhika@reyhandhika:~$ sudo setfacl -d -m g:webapp-team:rwx /srv/webapp
reyhandhika@reyhandhika:~$ sudo setfacl -d -m u:deploy:r-x /srv/webapp
reyhandhika@reyhandhika:~$ getfacl /srv/webapp
getfacl: Removing leading '/' from absolute path names
# file: srv/webapp
# owner: root
# group: webapp-team
# flags: -s-
user::rwx
user:deploy:r-x
group::rwx
mask::rwx
other::r-x
default:user::rwx
default:user:deploy:r-x
default:group::rwx
default:group:webapp-team:rwx
default:mask::rwx
default:other::r-x

reyhandhika@reyhandhika:~$
```
jawaban: Konfigurasi tersebut membuat group webapp-team dapat membaca, menulis, dan mengakses direktori proyek. User deploy hanya memiliki akses baca dan execute. Penggunaan SGID memastikan seluruh file baru otomatis menggunakan group proyek yang sama sehingga kolaborasi lebih konsisten dan aman.
## Latihan Latihan 9.B — Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan
menetapkan quota ruang serta inode sederhana pada /home/.
```bash
# Membuat user intern
sudo useradd -m -s /bin/bash intern
# Menambahkan user ke group labgroup
sudo usermod -aG labgroup intern
# Membuat password user
sudo passwd intern
# Memaksa ganti password saat login pertama
sudo chage -d 0 intern
# Mengatur password expired 45 hari dan warning 7 hari
sudo chage -M 45 -W 7 intern
# Memberikan akses sudo hanya untuk systemctl status
# Membuka file sudoers
sudo visudo -f /etc/sudoers.d/intern
# Isi konfigurasi
intern ALL=(root) /bin/systemctl status *
# Verifikasi hak sudo
sudo -l -U intern
# Menetapkan quota ruang dan inode pada /home
# Edit quota user
sudo edquota -u intern
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo useradd -m -s /bin/bash intern
useradd: user 'intern' already exists
reyhandhika@reyhandhika:~$ sudo usermod -aG labgroup intern
reyhandhika@reyhandhika:~$ sudo passwd intern
New password:
Retype new password:
passwd: password updated successfully
reyhandhika@reyhandhika:~$ sudo chage -d 0 intern


reyhandhika@reyhandhika:~$ sudo -l -U intern
Matching Defaults entries for intern on reyhandhika:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User intern may run the following commands on reyhandhika:
    (root) /bin/systemctl status *
reyhandhika@reyhandhika:~$ sudo edquota -u intern
No filesystems with quota detected.
reyhandhika@reyhandhika:~$
```
Jawaban: Konfigurasi ini membuat user intern memiliki shell /bin/bash, tergabung dalam labgroup, wajib mengganti password saat login pertama, memiliki kebijakan password 45 hari dengan warning 7 hari sebelum expired, hanya dapat menjalankan systemctl status menggunakan sudo, serta memiliki pembatasan penggunaan ruang disk dan jumlah file melalui quota.