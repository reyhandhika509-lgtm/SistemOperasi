<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## Praktikum 10.1 Melihat Penggunaan Memori
Tujuan: mengenali struktur dan penggunaan memori pada sistem Linux.

Langkah 1: Jalankan free -h untuk melihat ringkasan RAM dan swap.
```bash
free -h
```
Output:
```bash
reyhandhika@reyhandhika:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       317Mi       1.4Gi       1.1Mi       336Mi       1.6Gi
Swap:          2.0Gi          0B       2.0Gi
```
Langkah 2: Lihat detail memori dari kernel melalui /proc/meminfo
```bash
cat /proc/meminfo | head -n 20
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat /proc/meminfo | head -n 20
MemTotal:        2015316 kB
MemFree:         1495484 kB
MemAvailable:    1690144 kB
Buffers:           19992 kB
Cached:           307676 kB
SwapCached:            0 kB
Active:           330980 kB
Inactive:          49808 kB
Active(anon):      62960 kB
Inactive(anon):        0 kB
Active(file):     268020 kB
Inactive(file):    49808 kB
Unevictable:       27444 kB
Mlocked:           27444 kB
SwapTotal:       2097148 kB
SwapFree:        2097148 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 4 kB
Writeback:             0 kB
```
Analisis:
1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya
di bawah 10%, sistem mulai kekurangan memori.
2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah
pernah memindahkan data ke disk karena RAM tidak cukup.
3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai
dengan kolom buff/cache pada free -h.

Jawaban: 

1.  Rumus :
available / total × 100%

Data dari Output:
```bash
MemTotal:        2015316 kB
MemAvailable:    1690144 kB
```
Memasukkan angka Output dengan rumus
```bash
1690144 / 2015316 × 100%
1690144 ÷ 2015316 = 0.8386
0.8386 × 100 = 83.86%
```
Jadi Persentase memori tersedia dihitung menggunakan rumus available / total × 100%. Berdasarkan data, MemAvailable sebesar 1690144 kB dan MemTotal sebesar 2015316 kB, sehingga diperoleh persentase sebesar 83.86%. Karena nilainya di atas 10%, maka sistem berada dalam kondisi normal dan masih memiliki memori yang cukup.

2.  Data dari output:
```bash 
SwapTotal: 2097148 kB
SwapFree:  2097148 kB
```
jadi Nilai swap used adalah 0 kB, yang berarti kernel belum menggunakan swap karena RAM masih mencukupi untuk menjalankan proses.

3.  Data Dari Output:
```bash
Buffers: 19992 kB
Cached:  307676 kB
```
Jadi Nilai Cached dan Buffers menunjukkan memori yang digunakan sebagai cache oleh sistem untuk mempercepat akses file. Nilai ini sesuai dengan kolom buff/cache pada perintah free -h dan dapat dibebaskan secara otomatis jika dibutuhkan aplikasi.

### Studi Kasus 10.1 Server Lambat karena Memori
Skenario: Server aplikasi terasa lambat saat banyak pengguna aktif. Administrator perlu menentukan apakah penyebabnya adalah kekurangan memori.

Langkah 1: Periksa kondisi memori secara keseluruhan.
```bash
free -h
```
Output:
```bash
reyhandhika@reyhandhika:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       317Mi       1.4Gi       1.1Mi       337Mi       1.6Gi
Swap:          2.0Gi          0B       2.0Gi
```
Langkah 2: Pantau proses secara real-time
```bash
top
```
Output:
```bash
reyhandhika@reyhandhika:~$ top
top - 12:17:22 up 30 min,  2 users,  load average: 0.28, 0.07,
Tasks: 100 total,   1 running,  99 sleeping,   0 stopped,   0 z
%Cpu(s):  0.0 us,  4.5 sy,  0.0 ni, 90.7 id,  0.0 wa,  0.0 hi,
MiB Mem :   1968.1 total,   1459.0 free,    317.6 used,    337.
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   1650.

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM
   1053 reyhand+  20   0   14964   7108   5148 S   3.7   0.4
    483 root      20   0       0      0      0 I   1.3   0.0
     16 root      20   0       0      0      0 S   0.3   0.0
      1 root      20   0   22084  13304   9560 S   0.0   0.7
      2 root      20   0       0      0      0 S   0.0   0.0
      3 root      20   0       0      0      0 S   0.0   0.0
      4 root       0 -20       0      0      0 I   0.0   0.0
      5 root       0 -20       0      0      0 I   0.0   0.0
      6 root       0 -20       0      0      0 I   0.0   0.0
```
Analisis:
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server
dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang
menggunakan swap, yang berarti performa menurun.
3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut
menjadi kandidat utama penyebab lambatnya server.

Jawaban:
1. Nilai available masih sangat besar yaitu sekitar 1.6 GB. Hal ini menunjukkan bahwa sistem tidak mengalami kekurangan memori dan kondisi RAM masih mencukupi untuk
2. Nilai swap used adalah 0B, yang berarti kernel tidak menggunakan swap. Hal ini menunjukkan bahwa RAM masih mencukupi dan tidak terjadi tekanan memori pada sistem.
3. Proses dengan penggunaan memori terbesar adalah proses dengan PID 1 dengan nilai %MEM sebesar 0.7%. Nilai ini tergolong sangat kecil sehingga tidak menyebabkan beban memori yang signifikan pada sistem.

## Praktikum 10.2 Mengamati Aktivitas Paging
Tujuan: memahami aktivitas memori virtual melalui kolom swap pada vmstat.

Langkah 1: Jalankan vmstat dengan interval 1 detik, 5 sampel.
```bash
vmstat 1 5
```
Output:
```bash
reyhandhika@reyhandhika:~$ vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 1  0      0 1494012  20932 325128    0    0   150    14  995    0  0  3 96  0  0  0
 0  0      0 1494012  20932 325168    0    0     0     0 1069  147  0 11 89  0  0  0
 0  0      0 1494012  20932 325168    0    0     0     0 1033  116  0  9 91  0  0  0
 0  0      0 1494012  20932 325168    0    0     0     0  983   46  0  3 97  0  0  0
 0  0      0 1494012  20932 325168    0    0     0     0  997   69  0  1 99  0  0  0
 ```
 Analisis:
1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM cukup, kedua nilai ini selalu 0.
2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas
swap. Ini masih wajar jika tidak terus-menerus.
3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory pressure serius — performa turun drastis karena akses disk jauh lebih lambat dari RAM.
4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami kondisi keseluruhan RAM saat itu.

Jawaban:
1. Nilai si dan so pada seluruh baris adalah 0. Hal ini menunjukkan bahwa tidak terjadi aktivitas swap, sehingga RAM masih mencukupi untuk menjalankan proses.
2. Jika nilai si atau so sesekali lebih dari 0, maka artinya pernah terjadi aktivitas swap. Kondisi ini masih wajar selama tidak terjadi terus-menerus.
3. Jika nilai si dan so terus-menerus lebih dari 0, maka sistem mengalami tekanan memori (memory pressure) yang serius dan performa sistem dapat menurun karena akses disk lebih lambat dibanding RAM.
4. Nilai free masih besar yaitu sekitar 1.49 GB, sehingga sistem memiliki cukup memori bebas. Nilai buffer dan cache menunjukkan memori yang digunakan untuk mempercepat akses data, dan kondisi ini masih dalam batas normal.

## Praktikum 10.3 Membuat dan Mengonfigurasi Swap File
Tujuan: menambahkan swap space dan memahami parameter swappiness.
Langkah 1: Buat file berukuran 512 MB sebagai calon swap.
```bash
sudo fallocate -l 512M /swapfile-week10
```
Output: 
```bash
reyhandhika@reyhandhika:~$ sudo fallocate -l 512M /swapfile-week10
[sudo] password for reyhandhika:
reyhandhika@reyhandhika:~$
```
Langkah 2: Atur permission file menjadi 600 — hanya root yang boleh membaca
dan menulis.
```bash
sudo chmod 600 /swapfile-week10
```
Langkah 3: Format file sebagai area swap, lalu aktifkan.
```bash
sudo mkswap /swapfile-week10
sudo swapon /swapfile-week10
```
Langkah 4: Verifikasi swap aktif. Anda akan melihat entri /swapfile-week10
dengan ukuran 512M, dan nilai total pada baris Swap di free -h bertambah 512M.
```bash
swapon --show
free -h
```
Langkah 5: Periksa nilai swappiness, ubah sementara, dan verifikasi perubahan.
```bash
cat /proc/sys/vm/swappiness
sudo sysctl vm.swappiness=10
cat /proc/sys/vm/swappiness
```
Output:
```bash
reyhandhika@reyhandhika:~$ sudo chmod 600 /swapfile-week10
reyhandhika@reyhandhika:~$ sudo mkswap /swapfile-week10
Setting up swapspace version 1, size = 512 MiB (536866816 bytes)
no label, UUID=b16ebfa2-25ff-45ec-b788-07dae5d6b0fa
reyhandhika@reyhandhika:~$ sudo swapon /swapfile-week10
reyhandhika@reyhandhika:~$ swapon --show
NAME             TYPE SIZE USED PRIO
/swap.img        file   2G   0B   -2
/swapfile-week10 file 512M   0B   -3
reyhandhika@reyhandhika:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       318Mi       1.4Gi       1.1Mi       340Mi       1.6Gi
Swap:          2.5Gi          0B       2.5Gi
reyhandhika@reyhandhika:~$ cat /proc/sys/vm/swappiness
60
reyhandhika@reyhandhika:~$ sudo sysctl vm.swappiness=10
vm.swappiness = 10
reyhandhika@reyhandhika:~$ cat /proc/sys/vm/swappiness
10
reyhandhika@reyhandhika:~$
```
Analisis:
1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam
menggunakan swap?
2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa
dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
3. Apakah entri /swapfile-week10 muncul di swapon –show? Jika tidak,
pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3.

Jawaban:
1. Nilai swappiness default adalah 60. Nilai ini menunjukkan bahwa kernel cukup aktif dalam menggunakan swap meskipun RAM masih tersedia.
2. Setelah nilai swappiness diubah menjadi 10, kernel akan lebih jarang menggunakan swap dan lebih mengutamakan penggunaan RAM. Hal ini dapat meningkatkan performa sistem karena RAM lebih cepat dibandingkan disk.
3. Ya, entri /swapfile-week10 muncul pada output swapon --show dengan ukuran 512 MB. Hal ini menunjukkan bahwa swap file berhasil dibuat dan diaktifkan.

## Praktikum 10.4 Monitoring Memory
Tujuan: mengidentifikasi proses dengan penggunaan memori terbesar

Langkah 1: Ambil snapshot proses diurutkan dari penggunaan memori terbesar
```bash
ps aux --sort=-%mem | head
```
Langkah 2: Pantau secara real-time dengan top
```bash
top
```
Output:
```bash
reyhandhika@reyhandhika:~$ ps aux --sort=-%mem | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1071  0.0  2.0 552232 42268 ?        Ssl  11:51   0:01 /usr/libexec/fwupd/fwupd
fwupd-r+    1166  0.1  1.3 513104 27816 ?        Ssl  12:31   0:00 /usr/bin/fwupdmgr refresh
root         351  0.0  1.3 289116 27452 ?        SLsl 11:47   0:00 /sbin/multipathd -d -s
root         689  0.0  1.1 109684 23080 ?        Ssl  11:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         297  0.0  0.8  66836 17272 ?        S<s  11:46   0:01 /usr/lib/systemd/systemd-journald
root         669  0.0  0.6 468980 13672 ?        Ssl  11:47   0:00 /usr/libexec/udisks2/udisksd
root           1  0.2  0.6  22084 13308 ?        Ss   11:46   0:06 /sbin/init
systemd+     532  0.0  0.6  21592 13064 ?        Ss   11:47   0:00 /usr/lib/systemd/systemd-resolved
root         714  0.0  0.6 392100 12860 ?        Ssl  11:47   0:00 /usr/sbin/ModemManager
reyhandhika@reyhandhika:~$ top
top - 12:39:34 up 52 min,  2 users,  load average: 0.02, 0.02,
Tasks: 100 total,   1 running,  99 sleeping,   0 stopped,   0 z
%Cpu(s):  0.0 us,  3.6 sy,  0.0 ni, 92.3 id,  0.4 wa,  0.0 hi,
MiB Mem :   1968.1 total,   1455.3 free,    317.9 used,    341.
MiB Swap:   2560.0 total,   2560.0 free,      0.0 used.   1650.

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM
   1053 reyhand+  20   0   14964   7108   5148 S   2.6   0.4
   1095 root      20   0       0      0      0 I   1.0   0.0
     18 root      rt   0       0      0      0 S   0.3   0.0
   1147 root       0 -20       0      0      0 I   0.3   0.0
   1179 root      20   0       0      0      0 I   0.3   0.0
   1189 reyhand+  20   0   11920   5924   3748 R   0.3   0.3
      1 root      20   0   22084  13308   9560 S   0.0   0.7
      2 root      20   0       0      0      0 S   0.0   0.0
      3 root      20   0       0      0      0 S   0.0   0.0
```
Analisis:
1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses menggunakan 512 MB RAM. Apakah wajar untuk jenis program
tersebut?
3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan
berdasarkan %MEM?

Jawaban:
1. Proses yang berada di urutan pertama adalah fwupd dengan nilai %MEM sebesar 2.0% dan RSS sebesar 42268 kB. Proses ini menggunakan memori terbesar dibandingkan proses lainnya pada saat pengamatan.
2. RSS sebesar 42268 kB setara dengan sekitar 41 MB, yang masih tergolong kecil dan wajar untuk proses sistem seperti fwupd.
3. VSZ selalu lebih besar dari RSS karena VSZ menunjukkan total memori virtual yang dialokasikan oleh proses, termasuk memori yang belum digunakan secara fisik, sedangkan RSS menunjukkan jumlah memori fisik yang benar-benar digunakan di RAM.
4. Urutan proses pada ps relatif konsisten dengan tampilan pada top, karena keduanya menunjukkan bahwa penggunaan memori pada sistem masih rendah dan didominasi oleh proses sistem dengan nilai %MEM yang kecil.

## Praktikum 10.5 Script Monitor Memori
Tujuan: mengotomasi pemantauan memori menggunakan Bash script

1. masukan kode berikut:
```bash
cd ~/praktikum-os/week10-memory
nano monitor-memori.sh
```
2. ketik script Berikut:
```bash
#!/bin/bash
set -euo pipefail

THRESHOLD=20

echo "=== Monitor Memori ==="
date
echo

free -h
echo

AVAIL=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')

if [ "$AVAIL" -lt "$THRESHOLD" ]; then
    echo "PERINGATAN: Memori tersedia hanya ${AVAIL}%!"
else
    echo "Status: Memori tersedia ${AVAIL}% (normal)"
fi

echo
echo "--- 5 Proses Memori Tertinggi ---"

ps aux --sort=-%mem | head -n 6 | tail -n 5
```
3. Jalankan:
```bash
chmod +x monitor-memori.sh
bash monitor-memori.sh
```
Output:
```bash
reyhandhika@reyhandhika:~$ chmod +x monitor-memori.sh
reyhandhika@reyhandhika:~$ bash monitor-memori.sh
=== Monitor Memori ===
Thu Apr 30 01:00:23 PM UTC 2026

               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       362Mi       1.4Gi       1.1Mi       344Mi       1.6Gi
Swap:          2.5Gi          0B       2.5Gi

Status: Memori tersedia 81% (normal)

--- 5 Proses Memori Tertinggi ---
root        1071  0.0  2.0 552232 42268 ?        Ssl  11:51   0:01 /usr/libexec/fwupd/fwupd
fwupd-r+    1166  0.0  1.4 513616 28264 ?        Ssl  12:31   0:01 /usr/bin/fwupdmgr refresh
root         351  0.0  1.3 289116 27452 ?        SLsl 11:47   0:01 /sbin/multipathd -d -s
root         689  0.0  1.1 109684 23080 ?        Ssl  11:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         297  0.0  0.8  66836 17300 ?        S<s  11:46   0:01 /usr/lib/systemd/systemd-journald
```

Analisis:
1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagi kolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan persentase bilangan bulat.
2. Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] bernilai benar jika persentase memori tersedia di bawah 20.
3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada
output? Mengapa demikian?

Jawaban:
1. Variabel THRESHOLD=20 berfungsi sebagai batas minimum persentase memori tersedia. Jika nilai memori tersedia berada di bawah 20%, maka script akan menampilkan peringatan bahwa kondisi memori sistem rendah.
Perintah free | awk digunakan untuk mengambil nilai memori available dan total, kemudian menghitung persentase memori tersedia dengan rumus available dibagi total dikali 100.

2. Kondisi if digunakan untuk membandingkan persentase memori tersedia dengan nilai threshold. Karena nilai memori tersedia sebesar 81% lebih besar dari 20%, maka sistem berada dalam kondisi normal.

3. Proses dengan penggunaan memori terbesar adalah fwupd dengan 
penggunaan sekitar 2.0% memori. Nilai ini masih tergolong kecil sehingga tidak memberikan beban signifikan pada sistem.

### Studi Kasus 10.2 Gagal Akses File
Skenario: Program tidak dapat membaca file konfigurasi. Penyebab umum: file tidak ada, path salah, atau permission tidak sesuai. Kita akan mensimulasikan kondisi ini dan mengamati pesan error yang dihasilkan.

Langkah 1: Buat direktori dan file konfigurasi contoh.
```bash
mkdir -p ~/praktikum-os/week10-memory/syscall-case
cd ~/praktikum-os/week10-memory/syscall-case
echo "PORT=8080" > app.conf
ls -l app.conf
cat app.conf
```

Langkah 2: Simulasikan permission bermasalah
```bash
chmod 000 app.conf
cat app.conf
```
Langkah 3: Kembalikan permission dan verifikasi.
```bash
chmod 644 app.conf
cat app.conf
```
Output:
```bash
reyhandhika@reyhandhika:~$ mkdir -p ~/praktikum-os/week10-memory/syscall-case
reyhandhika@reyhandhika:~$ cd ~/praktikum-os/week10-memory/syscall-case
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ echo "PORT=8080" > app.conf
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ ls -l app.conf
-rw-rw-r-- 1 reyhandhika reyhandhika 10 Apr 30 23:24 app.conf
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ cat app.conf
PORT=8080
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ chmod 000 app.conf
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ cat app.conf
cat: app.conf: Permission denied
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ chmod 644 app.conf
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ cat app.conf
PORT=8080
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ ls -l app.conf
-rw-r--r-- 1 reyhandhika reyhandhika 10 Apr 30 23:24 app.conf
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ cat app.conf
PORT=8080
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$
```

Analisis:
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System
call apa yang gagal?
2. Apa perbedaan pesan error Permission denied vs No such file or directory?
Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
3. Permission 644 berarti apa untuk owner, group, dan others?

Jawaban:
1. Pesan "Permission denied" muncul setelah dilakukan chmod 000 karena file tidak memiliki izin akses baca, tulis, maupun eksekusi. System call yang gagal adalah open(), karena kernel menolak permintaan untuk membuka file akibat tidak adanya izin baca.
2. Pesan "Permission denied" terjadi ketika file ada tetapi tidak memiliki izin akses, sedangkan "No such file or directory" terjadi ketika file tidak ditemukan atau telah dihapus dari sistem.
3. Permission 644 berarti pemilik file memiliki izin membaca dan menulis (rw-), sedangkan group dan pengguna lain hanya memiliki izin membaca (r--).

## Praktikum 10.6 Mengamati System Call dengan strace
Tujuan: melihat dan menganalisis system call yang dilakukan suatu perintah.

Langkah 1: Lihat 30 baris pertama system call dari perintah ls
```bash
strace ls 2>&1 | head -n 30
```
Langkah 2: Lihat ringkasan statistik dan bandingkan dua direktori berbeda
```bash
strace -c ls
strace -c ls /etc 2>&1 | tail -5
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ strace ls 2>&1 | head -n 30
execve("/usr/bin/ls", ["ls"], 0x7ffedadbd1a0 /* 25 vars */) = 0
brk(NULL)                               = 0x55c626ce2000
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x73b6f1b39000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=32431, ...}) = 0
mmap(NULL, 32431, PROT_READ, MAP_PRIVATE, 3, 0) = 0x73b6f1b31000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=174472, ...}) = 0
mmap(NULL, 181960, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x73b6f1b04000
mmap(0x73b6f1b0a000, 118784, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x73b6f1b0a000
mmap(0x73b6f1b27000, 24576, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x23000) = 0x73b6f1b27000
mmap(0x73b6f1b2d000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x29000) = 0x73b6f1b2d000
mmap(0x73b6f1b2f000, 5832, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x73b6f1b2f000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220\243\2\0\0\0\0\0"..., 832) = 832
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
fstat(3, {st_mode=S_IFREG|0755, st_size=2125328, ...}) = 0
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
mmap(NULL, 2170256, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x73b6f1800000
mmap(0x73b6f1828000, 1605632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x28000) = 0x73b6f1828000
mmap(0x73b6f19b0000, 323584, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b0000) = 0x73b6f19b0000
mmap(0x73b6f19ff000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1fe000) = 0x73b6f19ff000
mmap(0x73b6f1a05000, 52624, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x73b6f1a05000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ strace -c ls
app.conf
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 69.60    0.003894        1947         2           getdents64
 22.31    0.001248        1248         1           execve
  2.22    0.000124           6        18           mmap
  1.04    0.000058           8         7           openat
  0.97    0.000054          54         1           write
  0.80    0.000045           5         9           close
  0.66    0.000037           7         5           mprotect
  0.52    0.000029           3         8           fstat
  0.45    0.000025           5         5           read
  0.29    0.000016           5         3           brk
  0.27    0.000015          15         1           munmap
  0.27    0.000015           7         2         2 statfs
  0.18    0.000010           5         2         2 access
  0.11    0.000006           3         2           ioctl
  0.11    0.000006           3         2           pread64
  0.05    0.000003           3         1           prlimit64
  0.05    0.000003           3         1           getrandom
  0.04    0.000002           2         1           arch_prctl
  0.04    0.000002           2         1           set_tid_address
  0.04    0.000002           2         1           set_robust_list
  0.02    0.000001           1         1           rseq
------ ----------- ----------- --------- --------- ----------------
100.00    0.005595          75        74         4 total
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ strace -c ls /etc 2>&1 | tail -5
  0.23    0.000001           1         1           rseq
  0.00    0.000000           0         1           execve
  0.00    0.000000           0         1           prlimit64
------ ----------- ----------- --------- --------- ----------------
100.00    0.000444           6        74         5 total
```

Analisis:
1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan fungsi singkat masing-masing berdasarkan argumen yang terlihat.
2. Dari ringkasan strace -c, system call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti
program bermasalah, ataukah bagian normal dari logika program?
4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang menyebabkan perbedaan tersebut?

Jawaban:

1. Berdasarkan hasil pengamatan menggunakan strace, ditemukan beberapa system call seperti execve(), openat(), read(), dan close(). System call execve() digunakan untuk menjalankan program ls. System call openat() digunakan untuk membuka file atau library yang dibutuhkan program. System call read() digunakan untuk membaca isi file, sedangkan close() digunakan untuk menutup file setelah selesai digunakan.

2. System call yang paling sering dipanggil adalah mmap() dengan jumlah 18 pemanggilan. Hal ini terjadi karena mmap() digunakan untuk memetakan file dan library ke dalam memori sehingga dapat digunakan oleh program.

3. Terdapat beberapa system call yang menghasilkan error, namun hal ini merupakan bagian normal dari proses program. Error tersebut biasanya terjadi saat sistem mencoba mengakses file yang tidak ada atau tidak diperlukan.

4.  Jumlah system call antara perintah ls dan ls /etc relatif sama, namun waktu eksekusi pada ls /etc sedikit lebih besar karena direktori /etc memiliki lebih banyak file yang harus dibaca.

# 1.6 Tugas Praktikum
Instruksi Umum: Kerjakan seluruh tugas pada direktori berikut:
1. Buka file dengan nano
```bash
mkdir -p ~/praktikum-os/week10-memory
cd ~/praktikum-os/week10-memory
nano ~/praktikum-os/week10-memory/memory-audit.sh
```
2. Isi file memory-audit.sh
```bash
#!/bin/bash
set -euo pipefail

LAPORAN="memory-report.txt"

{
echo "=== LAPORAN MEMORI SISTEM ==="
date
echo

echo "--- Ringkasan free -h ---"
free -h
echo

echo "--- /proc/meminfo ---"
cat /proc/meminfo | head -n 20

} > "$LAPORAN"

echo "Laporan disimpan ke: $LAPORAN"

cat "$LAPORAN"
```
3. Jalankan script audit
```bash
chmod +x ~/praktikum-os/week10-memory/memory-audit.sh
cd ~/praktikum-os/week10-memory
bash memory-audit.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ mkdir -p ~/praktikum-os/week10-memory
reyhandhika@reyhandhika:~/praktikum-os/week10-memory/syscall-case$ cd ~/praktikum-os/week10-memory
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ nano ~/praktikum-os/week10-memory/memory-audit.sh
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ chmod +x ~/praktikum-os/week10-memory/memory-audit.sh
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ cd ~/praktikum-os/week10-memory
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ bash memory-audit.sh
Laporan disimpan ke: memory-report.txt
=== LAPORAN MEMORI SISTEM ===
Thu Apr 30 11:51:48 PM UTC 2026

--- Ringkasan free -h ---
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       330Mi       1.4Gi       1.1Mi       374Mi       1.6Gi
Swap:          2.5Gi          0B       2.5Gi

--- /proc/meminfo ---
MemTotal:        2015316 kB
MemFree:         1444644 kB
MemAvailable:    1677320 kB
Buffers:           25324 kB
Cached:           338696 kB
SwapCached:            0 kB
Active:           352324 kB
Inactive:          65232 kB
Active(anon):      63372 kB
Inactive(anon):        0 kB
Active(file):     288952 kB
Inactive(file):    65232 kB
Unevictable:       27444 kB
Mlocked:           27444 kB
SwapTotal:       2621432 kB
SwapFree:        2621432 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 0 kB
Writeback:             0 kB
```
Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah
sistem dalam kondisi normal?
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut
pandang ketersediaan untuk aplikasi?
3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai
SwapFree?

Jawaban:
1. Persentase memori tersedia dihitung menggunakan rumus available dibagi total dikali 100%. Berdasarkan data, MemAvailable sebesar 1677320 kB dan MemTotal sebesar 2015316 kB, sehingga diperoleh persentase sebesar 83%. Nilai ini menunjukkan bahwa sistem berada dalam kondisi normal karena memori yang tersedia masih cukup besar.

2. Buffers dan cache tidak dihitung sebagai memori terpakai karena memori tersebut digunakan sebagai cache untuk mempercepat akses data. Jika aplikasi membutuhkan memori tambahan, sistem dapat membebaskan memori dari buff/cache secara otomatis.

3. Nilai SwapTotal lebih besar dari 0 yaitu sebesar 2621432 kB, yang menunjukkan bahwa sistem memiliki ruang swap. Nilai SwapFree sebesar 2621432 kB menunjukkan bahwa swap belum digunakan karena RAM masih mencukupi.

## Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
Instruksi: Simpan daftar 10 proses pengguna memori terbesar ke file
```bash
ps aux --sort=-%mem | head -n 10 > top-memory-process.txt
cat top-memory-process.txt
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ ps aux --sort=-%mem | head -n 10 > top-memory-process.txt
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ cat top-memory-process.txt
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1071  0.0  2.0 552232 42268 ?        Ssl  11:51   0:02 /usr/libexec/fwupd/fwupd
fwupd-r+    1166  0.0  1.4 513616 28264 ?        Ssl  12:31   0:02 /usr/bin/fwupdmgr refresh
root         351  0.0  1.3 289116 27452 ?        SLsl 11:47   0:02 /sbin/multipathd -d -s
root         689  0.0  1.1 109684 23080 ?        Ssl  11:47   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         669  0.0  0.6 468980 13672 ?        Ssl  11:47   0:00 /usr/libexec/udisks2/udisksd
root           1  0.0  0.6  22084 13348 ?        Ss   11:46   0:13 /sbin/init
systemd+     532  0.0  0.6  21592 13072 ?        Ss   11:47   0:00 /usr/lib/systemd/systemd-resolved
root         714  0.0  0.6 392100 12864 ?        Ssl  11:47   0:00 /usr/sbin/ModemManager
root        1616  0.0  0.5  33944 12060 ?        S<s  23:18   0:00 /usr/lib/systemd/systemd-journald
```

Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka
gunakan bersama?

Jawaban:  
1. Proses yang berada di urutan pertama adalah fwupd dengan nilai penggunaan memori sebesar 2.0% dan RSS sebesar 42268 kB. Proses ini merupakan layanan sistem yang digunakan untuk pembaruan firmware perangkat.

2. Nilai RSS sebesar 42268 kB setara dengan sekitar 41 MB, yang masih tergolong kecil dan wajar untuk proses sistem.

3. Total penggunaan memori dari lima proses teratas adalah 6.4%, yang menunjukkan bahwa penggunaan memori oleh proses utama masih tergolong rendah.

## Tugas 10.3 Membuat dan Memverifikasi Swap File
Instruksi: Buat swap file khusus tugas sebesar 256 MB dan verifikasi.
1. Buat dan aktifkan swap file tugas
```bash
sudo fallocate -l 256M /swapfile-tugas-week10
sudo chmod 600 /swapfile-tugas-week10
sudo mkswap /swapfile-tugas-week10
sudo swapon /swapfile-tugas-week10
```
Ouput:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ sudo fallocate -l 256M /swapfile-tugas-week10
[sudo] password for reyhandhika:
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ sudo chmod 600 /swapfile-tugas-week10
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ sudo mkswap /swapfile-tugas-week10
Setting up swapspace version 1, size = 256 MiB (268431360 bytes)
no label, UUID=7b7924f4-dc9e-488d-9ce7-577848e76731
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ sudo swapon /swapfile-tugas-week10
```
2. Verifikasi dan simpan hasil
```bash
{
echo "=== VERIFIKASI SWAP ==="
swapon --show
echo
free -h 
} > swap-check.txt
cat swap-check.txt
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ {
echo "=== VERIFIKASI SWAP ==="
swapon --show
echo
free -h
} > swap-check.txt
cat swap-check.txt
=== VERIFIKASI SWAP ===
NAME                   TYPE SIZE USED PRIO
/swap.img              file   2G   0B   -2
/swapfile-week10       file 512M   0B   -3
/swapfile-tugas-week10 file 256M   0B   -4

               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       322Mi       1.4Gi       1.1Mi       376Mi       1.6Gi
Swap:          2.7Gi          0B       2.7Gi
```
Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644

Jawaban:
1. Kolom NAME menunjukkan nama swap file yang digunakan, TYPE menunjukkan jenis swap yaitu file, SIZE menunjukkan ukuran swap sebesar 256MB, dan USED menunjukkan jumlah swap yang sedang digunakan, yaitu 0B.

2. Nilai total swap pada perintah free -h bertambah sekitar 256MB setelah swap file dibuat. Hal ini menunjukkan bahwa swap file berhasil ditambahkan dan dikenali oleh sistem.

3. Permission 600 penting untuk menjaga keamanan data karena swap dapat berisi data sensitif dari memori sistem. Jika permission diatur ke 644, pengguna lain dapat membaca isi swap yang berpotensi membocorkan data penting.

## Tugas 10.4 Analisis System Call dengan strace
Instruksi: Analisis system call yang dipanggil perintah ls
1. Simpan ringkasan dan detail system call
```bash
strace -c ls 2> strace-summary.txt
strace ls /etc 2> strace-ls-etc.txt
cat strace-summary.txt
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ strace -c ls 2> strace-summary.txt
memory-audit.sh    strace-summary.txt  syscall-case
memory-report.txt  swap-check.txt      top-memory-process.txt
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ strace ls /etc 2> strace-ls-etc.txt
adduser.conf            mtab
alternatives            multipath
apparmor                multipath.conf
apparmor.d              nanorc
apport                  needrestart
apt                     netconfig
bash.bashrc             netplan
bash_completion         network
bash_completion.d       networkd-dispatcher
bindresvport.blacklist  networks
binfmt.d                newt
byobu                   nftables.conf
ca-certificates         nsswitch.conf
ca-certificates.conf    opt
cloud                   os-release
console-setup           overlayroot.conf
credstore               PackageKit
credstore.encrypted     pam.conf
cron.d                  pam.d
cron.daily              papersize
cron.hourly             passwd
cron.monthly            passwd-
crontab                 perl
cron.weekly             pki
cron.yearly             plymouth
cryptsetup-initramfs    pm
crypttab                polkit-1
dbus-1                  pollinate
debconf.conf            profile
debian_version          profile.d
default                 protocols
deluser.conf            python3
depmod.d                python3.12
dhcp                    rc0.d
dhcpcd.conf             rc1.d
dpkg                    rc2.d
e2scrub.conf            rc3.d
environment             rc4.d
ethertypes              rc5.d
fonts                   rc6.d
fstab                   rcS.d
fuse.conf               resolv.conf
fwupd                   rmt
gai.conf                rpc
ghostscript             rsyslog.conf
gnutls                  rsyslog.d
groff                   screenrc
group                   security
group-                  selinux
grub.d                  sensors3.conf
gshadow                 sensors.d
gshadow-                services
gss                     sgml
hdparm.conf             shadow
host.conf               shadow-
hostname                shells
hosts                   skel
hosts.allow             sos
hosts.deny              ssh
ImageMagick-6           ssl
init.d                  subgid
initramfs-tools         subgid-
inputrc                 subuid
iproute2                subuid-
iscsi                   sudo.conf
issue                   sudoers
issue.net               sudoers.d
kernel                  sudo_logsrvd.conf
landscape               supercat
ldap                    sysctl.conf
ld.so.cache             sysctl.d
ld.so.conf              sysstat
ld.so.conf.d            systemd
legal                   terminfo
libaudit.conf           thermald
libblockdev             timezone
libibverbs.d            tmpfiles.d
libnl-3                 ubuntu-advantage
libpaper.d              ucf.conf
locale.alias            udev
locale.conf             udisks2
locale.gen              ufw
localtime               update-manager
logcheck                update-motd.d
login.defs              update-notifier
logrotate.conf          UPower
logrotate.d             usb_modeswitch.conf
lsb-release             usb_modeswitch.d
lvm                     vconsole.conf
machine-id              vim
magic                   vmware-tools
magic.mime              vtrgb
manpath.config          w3m
mdadm                   wgetrc
mime.types              X11
mke2fs.conf             xattr.conf
ModemManager            xdg
modprobe.d              xml
modules                 zsh_command_not_found
modules-load.d
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ cat strace-summary.txt
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 42.14    0.000579         289         2           ioctl
 25.33    0.000348          19        18           mmap
  8.22    0.000113          16         7           openat
  8.08    0.000111          55         2           getdents64
  3.71    0.000051           5         9           close
  2.62    0.000036           7         5           mprotect
  2.26    0.000031           3         8           fstat
  2.04    0.000028           5         5           read
  1.46    0.000020          10         2           write
  0.95    0.000013          13         1           munmap
  0.87    0.000012           6         2           pread64
  0.73    0.000010           5         2         2 statfs
  0.44    0.000006           2         3           brk
  0.44    0.000006           3         2         2 access
  0.15    0.000002           2         1           set_robust_list
  0.15    0.000002           2         1           prlimit64
  0.15    0.000002           2         1           getrandom
  0.15    0.000002           2         1           rseq
  0.07    0.000001           1         1           arch_prctl
  0.07    0.000001           1         1           set_tid_address
  0.00    0.000000           0         1           execve
------ ----------- ----------- --------- --------- ----------------
100.00    0.001374          18        75         4 total
```
Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
2. System call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?

Jawaban:
1.  5 system call dan fungsinya
- execve()
Fungsi: execve() digunakan untuk menjalankan program baru, dalam hal ini menjalankan perintah ls dari sistem.
- openat()
Fungsi: openat() digunakan untuk membuka file atau direktori yang diperlukan oleh program sebelum dibaca.
- read()
Fungsi: read() digunakan untuk membaca isi file atau direktori yang telah dibuka sebelumnya.
- close()
Fungsi: close() digunakan untuk menutup file setelah selesai digunakan oleh program.
- mmap()
Fungsi: mmap() digunakan untuk memetakan file atau library ke dalam memori agar dapat digunakan oleh program dengan lebih efisien.

2. System call yang paling sering dipanggil adalah mmap() dengan jumlah 18 pemanggilan. Hal ini terjadi karena mmap() digunakan untuk memetakan file dan library ke dalam memori sehingga program dapat berjalan dengan efisien.

3. Terdapat beberapa system call yang menghasilkan error

## Tugas 10.5 Studi Kasus Diagnosa Server Lambat
Skenario: Server terasa lambat. Buat script diagnosa yang menggabungkan semua
pemeriksaan dari bab ini menggunakan fungsi Bash.

1. Buka file dengan nano
```bash
nano ~/praktikum-os/week10-memory/diagnosa-server.sh
```
2. isi file diagnosa-server.sh
```bash
#!/bin/bash
set -euo pipefail

LAPORAN="diagnosa-server-lambat.txt"

WARN_MEM=false
WARN_SWAP=0

cek_memori() {
echo "--- Kondisi Memori ---"
free -h
echo

AVAIL_PCT=$(free | awk '/Mem/ { printf "%d", $7/$2 *100 }')

if [ "$AVAIL_PCT" -lt 20 ]; then
echo "PERINGATAN: Memori tersedia hanya ${AVAIL_PCT}%"
WARN_MEM=true
fi
}

cek_swap() {
echo "--- Penggunaan Swap ---"

swapon --show 2>/dev/null || echo "Tidak ada swap aktif"
echo

WARN_SWAP=$(free | awk '/Swap/ { print $3 }')

if [ "$WARN_SWAP" -gt 0 ]; then
echo "INFO: Swap digunakan (${WARN_SWAP} kB)"
fi
}

cek_proses() {
echo "--- 10 Proses Memori Tertinggi ---"
ps aux --sort=-%mem | head -n 11
echo
}

cek_paging() {
echo "--- Aktivitas Paging (5 sampel) ---"
vmstat 1 5
echo
}

ringkasan() {
echo "=== RINGKASAN ==="

if [ "$WARN_MEM" = true ]; then
echo "- Memori: KRITIS - perlu tindakan segera"
else
echo "- Memori: normal"
fi

if [ "$WARN_SWAP" -gt 0 ]; then
echo "- Swap: aktif - pantau aktivitas paging"
else
echo "- Swap: tidak digunakan"
fi
}

{
echo "=== LAPORAN DIAGNOSA SERVER ==="
date
echo

cek_memori
cek_swap
cek_proses
cek_paging
ringkasan

} | tee "$LAPORAN"

echo
echo "Laporan disimpan ke: $LAPORAN"
```

3. Jalankan script diagnosa
```bash
chmod +x ~/praktikum-os/week10-memory/diagnosa-server.sh
cd ~/praktikum-os/week10-memory
bash diagnosa-server.sh
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ nano ~/praktikum-os/week10-memory/diagnosa-server.sh
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ chmod +x ~/praktikum-os/week10-memory/diagnosa-server.sh
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ cd ~/praktikum-os/week10-memory
reyhandhika@reyhandhika:~/praktikum-os/week10-memory$ bash diagnosa-server.sh
=== LAPORAN DIAGNOSA SERVER ===
Fri May  1 12:16:12 AM UTC 2026

--- Kondisi Memori ---
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       322Mi       1.4Gi       1.1Mi       376Mi       1.6Gi
Swap:          2.7Gi          0B       2.7Gi

--- Penggunaan Swap ---
NAME                   TYPE SIZE USED PRIO
/swap.img              file   2G   0B   -2
/swapfile-week10       file 512M   0B   -3
/swapfile-tugas-week10 file 256M   0B   -4

--- 10 Proses Memori Tertinggi ---
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1071  0.0  2.0 552232 42268 ?        Ssl  Apr30   0:02 /usr/libexec/fwupd/fwupd
fwupd-r+    1166  0.0  1.4 513616 28264 ?        Ssl  Apr30   0:02 /usr/bin/fwupdmgr refresh
root         351  0.0  1.3 289116 27452 ?        SLsl Apr30   0:02 /sbin/multipathd -d -s
root         689  0.0  1.1 109684 23080 ?        Ssl  Apr30   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root        1616  0.0  0.7  50332 14588 ?        S<s  Apr30   0:00 /usr/lib/systemd/systemd-journald
root         669  0.0  0.6 468980 13672 ?        Ssl  Apr30   0:01 /usr/libexec/udisks2/udisksd
root           1  0.0  0.6  22084 13348 ?        Ss   Apr30   0:13 /sbin/init
systemd+     532  0.0  0.6  21592 13072 ?        Ss   Apr30   0:00 /usr/lib/systemd/systemd-resolved
root         714  0.0  0.6 392100 12864 ?        Ssl  Apr30   0:00 /usr/sbin/ModemManager
reyhand+     927  0.0  0.5  20332 11516 ?        Ss   Apr30   0:00 /usr/lib/systemd/systemd --user

--- Aktivitas Paging (5 sampel) ---
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 2  0      0 1450272  25960 360092    0    0     7     1  242    0  0  2 97  0  0  0
 0  0      0 1450272  25960 360092    0    0     0     0 1068  161  0  9 91  0  0  0
 0  0      0 1450272  25960 360092    0    0     0     0 1002   44  0  1 99  0  0  0
 0  0      0 1450272  25960 360092    0    0     0     0 1002   53  0  3 98  0  0  0
 0  0      0 1450272  25960 360092    0    0     0     4  998   48  0  3 98  0  0  0

=== RINGKASAN ===
- Memori: normal
- Swap: tidak digunakan

Laporan disimpan ke: diagnosa-server-lambat.txt
```
Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses,
cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi
terpisah?
2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis?
Jelaskan berdasarkan nilai threshold yang digunakan script.
3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa >
"$LAPORAN"? Apa keuntungannya?
4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa
implikasinya terhadap performa server?

Jawaban:
1. Fungsi cek_memori() digunakan untuk memeriksa kondisi memori sistem menggunakan perintah free -h serta menghitung persentase memori tersedia. Jika memori tersedia kurang dari 20%, maka sistem akan memberikan peringatan.

2. Berdasarkan hasil ringkasan, kondisi sistem berada dalam keadaan normal karena memori tersedia masih besar dan swap tidak digunakan.

3. Script menggunakan perintah tee karena dapat menampilkan output ke layar sekaligus menyimpannya ke file laporan. Jika menggunakan tanda >, output hanya akan disimpan ke file tanpa ditampilkan di layar.

4. Berdasarkan hasil vmstat, nilai si dan so bernilai 0 pada semua sampel. Hal ini menunjukkan bahwa tidak terjadi aktivitas paging dan sistem memiliki memori yang cukup.