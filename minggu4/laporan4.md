<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## TUGAS PENDAHULUAN

Jawablah pertanyaan-pertanyaan di bawah ini :

1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.

2. Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)

3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).

4. Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.

Jawaban : 

1. Perintah-perintah direktori: pwd, cd, mkdir, rmdir

* pwd (Print Working Directory) : Perintah direktori digunakan untuk mengelola folder (directory) dalam sistem operasi Linux.
* cd (Change Directory) : Perintah cd digunakan untuk berpindah dari satu direktori ke direktori lain.
* mkdir (Make Directory) : Perintah mkdir digunakan untuk membuat direktori baru.
* rmdir (Remove Directory): Perintah rmdir digunakan untuk menghapus direktori yang kosong.

2. Perintah manipulasi file : cp, mv, rm (beserta format)
* cp (Copy) : Perintah cp digunakan untuk menyalin file atau direktori.
format : cp [opsi] sumber tujuan

* mv (move): Perintah mv digunakan untuk memindahkan file atau mengganti nama file. 
format: mv sumber tujuan

* rm (remove) : Perintah rm digunakan untuk menghapus file atau direktori.
format : rm [opsi] file

3. Perbedaan Hard Link dan Soft Link (Symbolic Link)

* Hard Link :

* Hard link merupakan tautan langsung ke inode dari sebuah file.

* File asli dan hard link memiliki inode yang sama, sehingga keduanya menunjuk ke data yang sama di disk.

* Jika salah satu file diubah, maka perubahan tersebut akan terlihat pada semua hard link karena mereka mengacu pada data yang sama.

* Jika file asli dihapus, data masih tetap dapat diakses melalui hard link yang lain.

* Hard link tidak dapat dibuat pada filesystem yang berbeda dan tidak dapat digunakan untuk direktori.

* Soft Link (Symbolic Link)

* Soft link atau symbolic link adalah file khusus yang berisi path atau alamat menuju file target.

* Soft link hanya berfungsi sebagai penunjuk (pointer) ke file asli.

* Jika file asli dihapus atau dipindahkan, maka symbolic link akan menjadi tautan rusak (dangling link).

* Soft link dapat dibuat pada filesystem yang berbeda dan dapat menunjuk ke direktori.

 * Ketika dilihat menggunakan perintah ls -l, symbolic link ditandai dengan huruf l pada permission serta simbol panah -> yang menunjuk ke file target.

4. Maksud Perintah: file, find, which, locate, grep
*1. file

* Perintah file digunakan untuk menentukan tipe atau jenis suatu file berdasarkan isi file tersebut, bukan hanya dari ekstensi file.
Contoh: file dokumen.txt

Output: dokumen.txt: ASCII text
2. find

* Perintah find digunakan untuk mencari file atau direktori di dalam suatu struktur direktori berdasarkan kriteria tertentu, seperti nama, ukuran, atau waktu modifikasi.

Contoh: find /home -name "*.txt"
Artinya: mencari semua file dengan ekstensi .txt di direktori /home.

3. which

* Perintah which digunakan untuk menampilkan lokasi absolut dari suatu program atau perintah yang akan dijalankan, berdasarkan variabel lingkungan PATH.

Contoh: which ls

Output: /bin/ls
4. locate

* Perintah locate digunakan untuk mencari file dengan cepat menggunakan database indeks yang sudah dibuat sebelumnya.
Database ini biasanya diperbarui menggunakan perintah updatedb.

Contoh: locate passwd

* Perintah tersebut akan menampilkan semua file bernama passwd yang terdapat dalam sistem.

5. grep (Global Regular Expression Print)

* Perintah grep digunakan untuk mencari teks atau pola tertentu dalam sebuah file menggunakan regular expression.

Contoh:

grep "error" log.txt

Artinya: menampilkan semua baris pada file log.txt yang mengandung kata "error"

## LATIHAN

### 1. Cobalah urutan perintah berikut :
```bash
$ cd
$ pwd
$ ls –al
$ cd .
$ pwd
$ cd ..
$ pwd
$ ls -al
$ cd ..
$ pwd
$ ls -al
$ cd /etc
$ ls –al | more
$ cat passwd
$ cd –
$ pwd
```
Output:
```bash
reyhandhika@reyhandhika:~$ $cd
reyhandhika@reyhandhika:~$ $pwd
reyhandhika@reyhandhika:~$ $ls -al
Command '-al' not found, did you mean:
  command 'pal' from deb pal (0.4.3-9)
  command 'al' from deb mono-devel (6.8.0.105+dfsg-3.5ubuntu1)
  command 'cal' from deb ncal (12.1.8)
Try: sudo apt install <deb name>
reyhandhika@reyhandhika:~$ $ cd .
$: command not found
reyhandhika@reyhandhika:~$ cd
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$ ls -al
total 100
drwxr-x--- 6 reyhandhika reyhandhika  4096 Mar 10 10:50 .
drwxr-xr-x 3 root        root         4096 Feb 22 05:18 ..
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw------- 1 reyhandhika reyhandhika  2599 Mar  4 04:41 .bash_history
-rw-r--r-- 1 reyhandhika reyhandhika   220 Mar 31  2024 .bash_logout
-rw-r--r-- 1 reyhandhika reyhandhika  3771 Mar 31  2024 .bashrc
drwx------ 2 reyhandhika reyhandhika  4096 Feb 22 05:21 .cache
drwx------ 3 reyhandhika reyhandhika  4096 Feb 23 06:05 .config
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
-rw------- 1 reyhandhika reyhandhika    20 Mar  3 06:44 .lesshst
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-r--r-- 1 reyhandhika reyhandhika   807 Mar 31  2024 .profile
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
drwx------ 2 reyhandhika reyhandhika  4096 Feb 22 05:18 .ssh
-rw-r--r-- 1 reyhandhika reyhandhika     0 Feb 22 05:22 .sudo_as_admin_successful
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$ cd .
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$ ls -al
total 100
drwxr-x--- 6 reyhandhika reyhandhika  4096 Mar 10 10:50 .
drwxr-xr-x 3 root        root         4096 Feb 22 05:18 ..
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw------- 1 reyhandhika reyhandhika  2599 Mar  4 04:41 .bash_history
-rw-r--r-- 1 reyhandhika reyhandhika   220 Mar 31  2024 .bash_logout
-rw-r--r-- 1 reyhandhika reyhandhika  3771 Mar 31  2024 .bashrc
drwx------ 2 reyhandhika reyhandhika  4096 Feb 22 05:21 .cache
drwx------ 3 reyhandhika reyhandhika  4096 Feb 23 06:05 .config
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
-rw------- 1 reyhandhika reyhandhika    20 Mar  3 06:44 .lesshst
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-r--r-- 1 reyhandhika reyhandhika   807 Mar 31  2024 .profile
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
drwx------ 2 reyhandhika reyhandhika  4096 Feb 22 05:18 .ssh
-rw-r--r-- 1 reyhandhika reyhandhika     0 Feb 22 05:22 .sudo_as_admin_successful
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$ cd ..
reyhandhika@reyhandhika:/home$ pwd
/home
reyhandhika@reyhandhika:/home$ ls -al
total 12
drwxr-xr-x  3 root        root        4096 Feb 22 05:18 .
drwxr-xr-x 23 root        root        4096 Feb 22 04:58 ..
drwxr-x---  6 reyhandhika reyhandhika 4096 Mar 10 10:50 reyhandhika
reyhandhika@reyhandhika:/home$ cd /etc
reyhandhika@reyhandhika:/etc$ ls -al | more
total 964
drwxr-xr-x 112 root root       4096 Feb 23 08:35 .
drwxr-xr-x  23 root root       4096 Feb 22 04:58 .
.
-rw-r--r--   1 root root       3444 Jul  5  2023 a
dduser.conf
drwxr-xr-x   2 root root       4096 Feb 22 05:35 a
lternatives
drwxr-xr-x   2 root root       4096 Feb 22 05:30 a
pparmor
drwxr-xr-x   9 root root      12288 Feb 22 05:30 a
pparmor.d
drwxr-xr-x   3 root root       4096 Aug  5  2025 a
reyhandhika@reyhandhika:/etc$ cat psswd
cat: psswd: No such file or directory
reyhandhika@reyhandhika:/etc$ cd -
/home
reyhandhika@reyhandhika:/home$ pwd
/home
reyhandhika@reyhandhika:/home$
```
### 2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls, pwd dan cat. Telusuri direktory /bin, /usr/bin, /sbin, /tmp dan /boot.

/bin : 
```bash
reyhandhika@reyhandhika:~$ cd /bin
reyhandhika@reyhandhika:/bin$ pwd
/bin
reyhandhika@reyhandhika:/bin$ ls -l | head -15
total 132692
-rwxr-xr-x 1 root root       55744 Jun 22  2025 [
-rwxr-xr-x 1 root root       14640 Mar 31  2024 411toppm
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-enabled
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-exec
-rwxr-xr-x 1 root root       18736 Aug 15  2025 aa-features-abi
-rwxr-xr-x 1 root root        1622 Feb  6 17:52 acpidbg
-rwxr-xr-x 1 root root       16422 Jul  2  2025 add-apt-repository
-rwxr-xr-x 1 root root       14720 Sep 16 00:08 addpart
lrwxrwxrwx 1 root root          25 Mar 31  2024 animate -> /etc/alternatives/animate
lrwxrwxrwx 1 root root          29 Mar 31  2024 animate-im6 -> /etc/alternatives/animate-im6
-rwxr-xr-x 1 root root       14656 Mar 31  2024 animate-im6.q16
-rwxr-xr-x 1 root root       12556 Mar 31  2024 anytopnm
-rwxr-xr-x 1 root root        2322 Apr 18  2024 apport-bug
-rwxr-xr-x 1 root root       13625 Jul  8  2025 apport-cli

```
/usr/bin : 
```bash
reyhandhika@reyhandhika:/bin$ /usr/bin
-bash: /usr/bin: Is a directory
reyhandhika@reyhandhika:/bin$ cd /usr/bin
reyhandhika@reyhandhika:/usr/bin$ pwd
/usr/bin
reyhandhika@reyhandhika:/usr/bin$ ls -l | head -15
total 132692
-rwxr-xr-x 1 root root       55744 Jun 22  2025 [
-rwxr-xr-x 1 root root       14640 Mar 31  2024 411toppm
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-enabled
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-exec
-rwxr-xr-x 1 root root       18736 Aug 15  2025 aa-features-abi
-rwxr-xr-x 1 root root        1622 Feb  6 17:52 acpidbg
-rwxr-xr-x 1 root root       16422 Jul  2  2025 add-apt-repository
-rwxr-xr-x 1 root root       14720 Sep 16 00:08 addpart
lrwxrwxrwx 1 root root          25 Mar 31  2024 animate -> /etc/alternatives/animate
lrwxrwxrwx 1 root root          29 Mar 31  2024 animate-im6 -> /etc/alternatives/animate-im6
-rwxr-xr-x 1 root root       14656 Mar 31  2024 animate-im6.q16
-rwxr-xr-x 1 root root       12556 Mar 31  2024 anytopnm
-rwxr-xr-x 1 root root        2322 Apr 18  2024 apport-bug
-rwxr-xr-x 1 root root       13625 Jul  8  2025 apport-cli
```
/sbin :
```bash
reyhandhika@reyhandhika:/usr/bin$ cd /sbin
reyhandhika@reyhandhika:/sbin$ pwd
/sbin
reyhandhika@reyhandhika:/sbin$ ls -l | head -15
total 33140
-rwxr-xr-x 1 root root     39680 Aug 15  2025 aa-load
-rwxr-xr-x 1 root root      3225 Aug 15  2025 aa-remove-unknown
-rwxr-xr-x 1 root root     40000 Aug 15  2025 aa-status
-rwxr-xr-x 1 root root       137 Apr 12  2024 aa-teardown
-rwxr-xr-x 1 root root     14904 Aug  5  2025 accessdb
-rwxr-xr-x 1 root root      3075 Jan  5 22:01 addgnupghome
lrwxrwxrwx 1 root root         7 Jul  5  2023 addgroup -> adduser
-rwxr-xr-x 1 root root      1053 Mar 31  2024 add-shell
-rwxr-xr-x 1 root root     55191 Jul  5  2023 adduser
-rwxr-xr-x 1 root root     60992 Sep 16 00:08 agetty
-rwxr-xr-x 1 root root   1629848 Aug 15  2025 apparmor_parser
lrwxrwxrwx 1 root root         9 Aug 15  2025 apparmor_status -> aa-status
-rwxr-xr-x 1 root root      2217 Jan  5 22:01 applygnupgdefaults
-rwxr-xr-x 1 root root     36862 Apr 16  2024 argdist-bpfcc
```
/tmp :
```bash
reyhandhika@reyhandhika:/sbin$ cd /tmp
reyhandhika@reyhandhika:/tmp$ pwd
/tmp
reyhandhika@reyhandhika:/tmp$ ls  -l | head -15
total 32
drwx------ 2 root root 4096 Mar  4 03:25 snap-private-tmp
drwx------ 3 root root 4096 Mar 10 11:39 systemd-private-f4c73744be82491db37ccff73c10d5bc-fwupd.service-fI0XGb
drwx------ 3 root root 4096 Mar  4 03:25 systemd-private-f4c73744be82491db37ccff73c10d5bc-ModemManager.service-fAxvs1
drwx------ 3 root root 4096 Mar  4 03:25 systemd-private-f4c73744be82491db37ccff73c10d5bc-polkit.service-26v0pj
drwx------ 3 root root 4096 Mar  9 02:56 systemd-private-f4c73744be82491db37ccff73c10d5bc-systemd-logind.service-69NWWp
drwx------ 3 root root 4096 Mar  9 02:56 systemd-private-f4c73744be82491db37ccff73c10d5bc-systemd-resolved.service-g6w6zq
drwx------ 3 root root 4096 Mar  9 02:56 systemd-private-f4c73744be82491db37ccff73c10d5bc-systemd-timesyncd.service-OaPwlN
drwx------ 3 root root 4096 Mar  4 04:22 systemd-private-f4c73744be82491db37ccff73c10d5bc-upower.service-lgPx7s
```
/boot :
```bash
reyhandhika@reyhandhika:/tmp$ cd /boot
reyhandhika@reyhandhika:/boot$ pwd
/boot
reyhandhika@reyhandhika:/boot$ ls -l | head -15
total 195224
-rw-r--r-- 1 root root   287599 Jan 13 13:56 config-6.8.0-100-generic
-rw-r--r-- 1 root root   287599 Feb  6 17:52 config-6.8.0-101-generic
drwxr-xr-x 5 root root     4096 Mar 10 11:37 grub
lrwxrwxrwx 1 root root       28 Mar 10 11:37 initrd.img -> initrd.img-6.8.0-101-generic
-rw-r--r-- 1 root root 74667295 Feb 22 05:31 initrd.img-6.8.0-100-generic
-rw-r--r-- 1 root root 76325274 Mar 10 11:38 initrd.img-6.8.0-101-generic
lrwxrwxrwx 1 root root       28 Feb 22 04:58 initrd.img.old -> initrd.img-6.8.0-100-generic
drwx------ 2 root root    16384 Feb 22 04:38 lost+found
-rw------- 1 root root  9120274 Jan 13 13:56 System.map-6.8.0-100-generic
-rw------- 1 root root  9120274 Feb  6 17:52 System.map-6.8.0-101-generic
lrwxrwxrwx 1 root root       25 Mar 10 11:37 vmlinuz -> vmlinuz-6.8.0-101-generic
-rw------- 1 root root 15030664 Jan 13 14:42 vmlinuz-6.8.0-100-generic
-rw------- 1 root root 15030664 Feb  6 18:21 vmlinuz-6.8.0-101-generic
lrwxrwxrwx 1 root root       25 Feb 22 04:58 vmlinuz.old -> vmlinuz-6.8.0-100-generic
reyhandhika@reyhandhika:/boot$

### 3. Telusuri direktory /dev. Identifikasi perangkat yang tersedia. Identifikasi tty  (termninal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls –l).

Output :
```bash
reyhandhika@reyhandhika:/boot$ cd /dev
reyhandhika@reyhandhika:/dev$ ls -l | head -15
total 0
crw-r--r--  1 root        root     10, 235 Mar  4 03:25 autofs
drwxr-xr-x  2 root        root         320 Mar  4 03:25 block
drwxr-xr-x  2 root        root          80 Mar  4 03:24 bsg
crw-rw----  1 root        disk     10, 234 Mar  4 03:25 btrfs-control
drwxr-xr-x  3 root        root          60 Mar  4 03:25 bus
lrwxrwxrwx  1 root        root           3 Mar  4 03:25 cdrom -> sr0
drwxr-xr-x  2 root        root        3720 Mar 10 11:33 char
crw--w----  1 root        tty       5,   1 Mar  4 03:25 console
lrwxrwxrwx  1 root        root          11 Mar  4 03:24 core -> /proc/kcore
drwxr-xr-x  3 root        root          60 Mar  4 03:25 cpu
crw-------  1 root        root     10, 123 Mar  4 03:25 cpu_dma_latency
crw-------  1 root        root     10, 203 Mar  4 03:25 cuse
drwxr-xr-x  8 root        root         160 Mar  4 03:25 disk
brw-rw----  1 root        disk    252,   0 Mar  4 03:25 dm-0
reyhandhika@reyhandhika:/dev$

>Direktori /proc disebut pseudo-filesystem (atau filesistem virtual) karena file-file di dalamnya tidak benar-benar tersimpan di disk. Sebaliknya, file-file tersebut dibuat secara dinamis oleh kernel saat diakses. Setiap kali kita membaca file di /proc, kernel mengambil data dari struktur data internalnya (seperti daftar proses, informasi hardware, statistik sistem) dan menyajikannya dalam format teks. Hal ini memungkinkan pengguna dan program untuk dengan mudah mengakses informasi kernel tanpa harus menggunakan system call khusus atau antarmuka pemrograman yang rumit.  
Output

```bash
reyhandhika@reyhandhika:/dev$ cd /proc
reyhandhika@reyhandhika:/proc$ cat interrupts
           CPU0
  0:        159   IO-APIC   2-edge      timer
  1:        655   IO-APIC   1-edge      i8042
  8:          0   IO-APIC   8-edge      rtc0
  9:          0   IO-APIC   9-fasteoi   acpi
 12:        158   IO-APIC  12-edge      i8042
 14:      44127   IO-APIC  14-edge      ata_piix
 15:          0   IO-APIC  15-edge      ata_piix
 18:          0   IO-APIC  18-fasteoi   vmwgfx
 19:     399143   IO-APIC  19-fasteoi   ehci_hcd:usb2, enp0s3
 20:          0   IO-APIC  20-fasteoi   vboxguest
 21:     120969   IO-APIC  21-fasteoi   ahci[0000:00:0d.0], snd_intel8x0
 22:         49   IO-APIC  22-fasteoi   ohci_hcd:usb1
NMI:          0   Non-maskable interrupts
LOC:   43589178   Local timer interrupts
SPU:          0   Spurious interrupts
PMI:          0   Performance monitoring interrupts
IWI:          0   IRQ work interrupts
RTR:          0   APIC ICR read retries
RES:          0   Rescheduling interrupts
CAL:          0   Function call interrupts
TLB:          0   TLB shootdowns
TRM:          0   Thermal event interrupts
THR:          0   Threshold APIC interrupts
DFR:          0   Deferred Error APIC interrupts
MCE:          0   Machine check exceptions
MCP:        154   Machine check polls
ERR:          0
MIS:          0
PIN:          0   Posted-interrupt notification event
NPI:          0   Nested posted-interrupt event
PIW:          0   Posted-interrupt wakeup event
reyhandhika@reyhandhika:/proc$

reyhandhika@reyhandhika:/proc$ cat devices
Character devices:
  1 mem
  4 /dev/vc/0
  4 tty
  4 ttyS
  5 /dev/tty
  5 /dev/console
  5 /dev/ptmx
  5 ttyprintk
  7 vcs
 10 misc
 13 input
 21 sg
 29 fb
 89 i2c
108 ppp
116 alsa
128 ptm
136 pts
180 usb
189 usb_device
202 cpu/msr
203 cpu/cpuid
204 ttyMAX
226 drm
241 hidraw
242 ttyDBC
243 bsg
244 watchdog
245 remoteproc
246 ptp
247 pps
248 rtc
249 dma_heap
250 dax
251 dimmctl
252 ndctl
253 tpm
254 gpiochip
261 accel

Block devices:
  7 loop
  8 sd
  9 md
 11 sr
 65 sd
 66 sd
 67 sd
 68 sd
 69 sd
 70 sd
 71 sd
128 sd
129 sd
130 sd
131 sd
132 sd
133 sd
134 sd
135 sd
252 device-mapper
253 virtblk
254 mdp
259 blkext
reyhandhika@reyhandhika:/proc$
reyhandhika@reyhandhika:/proc$ cat meminfo
MemTotal:        2015316 kB
MemFree:          386036 kB
MemAvailable:    1611936 kB
Buffers:          125532 kB
Cached:          1137092 kB
SwapCached:          348 kB
Active:           252976 kB
Inactive:        1056928 kB
Active(anon):      56616 kB
Inactive(anon):      176 kB
Active(file):     196360 kB
Inactive(file):  1056752 kB
Unevictable:       27312 kB
Mlocked:           27312 kB
SwapTotal:       2097148 kB
SwapFree:        2096624 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:                 4 kB
Writeback:             0 kB
AnonPages:         74244 kB
Mapped:            82216 kB
Shmem:               760 kB
KReclaimable:     160732 kB
Slab:             216580 kB
SReclaimable:     160732 kB
SUnreclaim:        55848 kB
KernelStack:        2128 kB
PageTables:         2868 kB
SecPageTables:         0 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     3104804 kB
Committed_AS:     354448 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       22460 kB
VmallocChunk:          0 kB
Percpu:              708 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
Unaccepted:            0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
DirectMap4k:      108480 kB
DirectMap2M:     1988608 kB
reyhandhika@reyhandhika:/proc$
reyhandhika@reyhandhika:/proc$ cat uptime
202207.13 40482.26
```
### 5. Ubahlah direktory home ke user lain secara langsung menggunakan cd ~username.

Output 
```bash
reyhandhika@reyhandhika:/proc$ cd ~reyhandhika
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$

### 6. Ubah kembali ke direktory home Anda
Output 
```bash
reyhandhika@reyhandhika:/proc$ cd ~reyhandhika
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$ cd
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$
*cd → kembali ke home (tidak berubah karena sudah di sana)
```

### 7. Buat subdirektory work dan play.
Output 
```bash
reyhandhika@reyhandhika:~$ # mkdir work play
reyhandhika@reyhandhika:~$ ls -l
total 60
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$
```
### 8. Hapus subdirektory work.
Output 
```bash
reyhandhika@reyhandhika:~$ rmdir work
reyhandhika@reyhandhika:~$ ls -l
total 60
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$
```

### 9. Copy file /etc/passwd ke direktory home Anda.

Output 
```bash
reyhandhika@reyhandhika:~$ cp /etc/passwd ~
reyhandhika@reyhandhika:~$ cp /etc/passwd .
reyhandhika@reyhandhika:~$ ls -l
total 64
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
-rw-r--r-- 1 reyhandhika reyhandhika  1798 Mar 10 14:34 passwd
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$
```
### 10. Pindahkan ke subdirektory play
Output 
```bash
reyhandhika@reyhandhika:~$ mv passwd play/
mv: cannot move 'passwd' to 'play/': Not a directory
reyhandhika@reyhandhika:~$ cd play
-bash: cd: play: No such file or directory
reyhandhika@reyhandhika:~$ cd play
-bash: cd: play: No such file or directory
reyhandhika@reyhandhika:~$ ls
all-config-files.txt  large-logs.txt
backup-error.log      large-logs.txt5
backup-success.log    passwd
backup.tar            praktikum-os
error.log             sorted-users.txt
file.txt              system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$ mkdir play
reyhandhika@reyhandhika:~$ cd play
reyhandhika@reyhandhika:~/play$ pwd
/home/reyhandhika/play
reyhandhika@reyhandhika:~/play$ mkdir play
reyhandhika@reyhandhika:~/play$ ls
play
reyhandhika@reyhandhika:~/play$ mv passwd play/
mv: cannot stat 'passwd': No such file or directory
reyhandhika@reyhandhika:~/play$ mv ../passwd
mv: missing destination file operand after '../passwd'
Try 'mv --help' for more information.
reyhandhika@reyhandhika:~/play$ cd ..
reyhandhika@reyhandhika:~$ mv passwd play/
reyhandhika@reyhandhika:~$ ls -l play
total 8
-rw-r--r-- 1 reyhandhika reyhandhika 1798 Mar 10 14:34 passwd
drwxrwxr-x 2 reyhandhika reyhandhika 4096 Mar 10 14:38 play
reyhandhika@reyhandhika:~$

### 11. Ubahlah ke subdirektory play dan buat symbolic link dengan nama terminal yang menunjuk ke perangkat tty. Apa yang terjadi jika melakukan hard link ke perangkat tty ?

Output
```bash
reyhandhika@reyhandhika:~$ cd play
reyhandhika@reyhandhika:~/play$ pwd
/home/reyhandhika/play
reyhandhika@reyhandhika:~/play$ who am i
reyhandhika pts/0        2026-03-10 13:52 (192.168.18.105)
reyhandhika@reyhandhika:~/play$ ln -s /dev/tty terminal
reyhandhika@reyhandhika:~/play$ ls -l
total 8
-rw-r--r-- 1 reyhandhika reyhandhika 1798 Mar 10 14:34 passwd
drwxrwxr-x 2 reyhandhika reyhandhika 4096 Mar 10 14:38 play
lrwxrwxrwx 1 reyhandhika reyhandhika    8 Mar 10 14:42 terminal -> /dev/tty
reyhandhika@reyhandhika:~/play$ ln /dev/tty terminal
ln: failed to create hard link 'terminal': File exists
reyhandhika@reyhandhika:~/play$

### 12. Buatlah file bernama hello.txt yang berisi kata ”hello word”. Dapatkah Anda gunakan ”cp” menggunakan ”terminal” sebagai file asal untuk menghasilkan efek yang sama ?

>Tidak. Mencoba cp terminal hello2.txt akan membaca dari terminal (input keyboard) dan menulis ke file. Hasilnya tergantung apa yang diketik, bukan "hello word". 

Output:
```bash
reyhandhika@reyhandhika:~/play$ echo "hello word" > hello.txt
reyhandhika@reyhandhika:~/play$ cat hello.txt
hello word
reyhandhika@reyhandhika:~/play$
```
### 13. Copy hello.txt ke terminal. Apa yang terjadi ?
>Tidak ada file baru, hanya output ke terminal.

Output 
```bash
reyhandhika@reyhandhika:~/play$ cp hello.txt terminal
hello word
```
### 14. Masih direktory home, copy keseluruhan direktory play ke direktory bernama work menggunakan symbolic link

Output 
```bash
reyhandhika@reyhandhika:~/play$ cd ..
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$ ln -s play work
reyhandhika@reyhandhika:~$ ls -l
total 64
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Mar 10 14:46 play
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
lrwxrwxrwx 1 reyhandhika reyhandhika     4 Mar 10 14:50 work -> play
reyhandhika@reyhandhika:~$
```
### 15. Hapus direktory work dan isinya dengan satu perintah

Output 
```bash
reyhandhika@reyhandhika:~$ rm -rf work
reyhandhika@reyhandhika:~$ ls -l
total 64
-rw-rw-r-- 1 reyhandhika reyhandhika 16638 Mar 10 10:50 all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar 10 10:50 backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika   382 Mar 10 10:50 backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika 10240 Mar 10 10:50 backup.tar
-rw-rw-r-- 1 reyhandhika reyhandhika    48 Mar 10 10:40 error.log
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Feb 25 03:49 file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  1530 Mar 10 10:40 large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika     0 Mar  4 04:05 large-logs.txt5
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Mar 10 14:46 play
drwxrwxr-x 3 reyhandhika reyhandhika  4096 Feb 23 02:57 praktikum-os
-rw-rw-r-- 1 reyhandhika reyhandhika   254 Mar 10 10:41 sorted-users.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  5883 Mar 10 10:44 system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$
```

## LAPORAN RESMI

### 1. Analisis Hasil Percobaan

### Percobaan 1: Direktory

### a. Analisis Setiap Hasil Tampilan   
* $ pwd  
Menampilkan direktori aktif saat ini, yaitu /home/user (home user).

* $ echo $HOME  
Menampilkan variabel lingkungan HOME yang berisi path home user, sama dengan hasil pwd.

* $ cd .  
Perintah cd . berpindah ke direktori saat ini (titik berarti direktori sendiri). Tidak ada perubahan direktori.

* $ pwd  
Masih /home/user.

* $ cd ..  
Berpindah ke parent direktori, yaitu /home.

* $ pwd  
Menampilkan /home.

* $ cd  
Tanpa argumen, cd kembali ke home user, yaitu /home/user.

* $ mkdir A B C A/D A/E B/F A/D/A  
Perintah ini membuat struktur direktori:

    * A, B, C di level pertama.

    * Di dalam A dibuat D dan E.

    * Di dalam B dibuat F.

    * Di dalam A/D dibuat A.
    Tidak ada output jika berhasil.

* $ ls -l  
Menampilkan daftar direktori A, B, C beserta atributnya.

* $ ls -l A  
Menampilkan isi direktori A, yaitu D dan E.

* $ ls -l A/D  
Menampilkan isi A/D, yaitu subdirektori A.

* $ rmdir B   
Mencoba menghapus direktori B. Error: rmdir: failed to remove 'B': Directory not empty karena B masih berisi subdirektori F.

* $ ls -l B  
Menampilkan isi B, yaitu F.

* $ rmdir B/F B  
Perintah ini menghapus B/F terlebih dahulu, kemudian B. Setelah B/F dihapus, B menjadi kosong sehingga rmdir B berhasil. Tidak ada output.

* $ ls -l B  
Error: ls: cannot access 'B': No such file or directory karena B sudah dihapus.

* Navigasi dengan cd:

    * $ cd A → pindah ke A, pwd menjadi /home/user/A.

    * $ cd . → tetap di A.

    * $ cd /home/user/C → pindah ke C dengan path absolut, berhasil jika C ada.

    * $ cd /user/C → Error: bash: cd: /user/C: No such file or directory karena path yang benar adalah /home/user/C, bukan /user/C.

### b. Pohon Struktur File dan Direktori (Percobaan 1 point 3)  

```bash
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── reyhandhika
│       ├── play
│       │   ├── passwd
│       │   └── terminal -> /dev/tty
│       ├── hello.txt
│       └── praktikum-os
├── lib
├── media
├── opt
├── proc
├── root
├── sbin
├── tmp
├── usr
└── var

### c. Penjelasan Pesan Error
* rmdir B error karena direktori tidak kosong. rmdir hanya dapat menghapus direktori kosong. Untuk menghapus direktori berisi, harus menggunakan rm -r.

* ls -l B setelah dihapus error karena direktori sudah tidak ada.

* cd /user/C error karena path absolut salah. Root (/) tidak memiliki direktori user; yang benar adalah /home/user/C.


### Percobaan 2: Manipulasi File

### a. Analisis Hasil Tampilan

* $ cat > contoh  
Membuat file contoh dengan input keyboard. Akhiri dengan Ctrl+D.

* $ cp contoh contoh1  
Menyalin contoh menjadi contoh1.

* $ ls -l  
Menampilkan kedua file.

* $ cp contoh A  
Menyalin contoh ke dalam direktori A (menjadi A/contoh).

* $ ls -l A  
Isi A sekarang ada file contoh dan subdirektori D, E.

* $ cp contoh contoh1 A/D  
Menyalin dua file ke dalam A/D.

* $ ls -l A/D  
Di A/D sekarang terdapat file contoh, contoh1, dan subdirektori A.

* $ mv contoh contoh2  
Memindahkan (rename) contoh menjadi contoh2.

* $ ls -l  
File contoh hilang, muncul contoh2.

* $ mv contoh1 contoh2 A/D  
Memindahkan contoh1 dan contoh2 ke dalam direktori A/D.

* $ ls -l A/D  
Di A/D sekarang terdapat file contoh, contoh1, contoh2, dan subdirektori A.

* $ mv contoh contoh1 C  
Error: mv: cannot stat 'contoh': No such file or directory (mungkin salah satu atau kedua file sudah tidak ada karena sudah dipindah ke A/D).

* $ ls -l C  
Direktori C kosong.

* $ rm contoh2  
Error: rm: cannot remove 'contoh2': No such file or directory karena file sudah dipindah.

* $ ls -l  
Hanya tersisa direktori A dan C.

* $ rm -i contoh  
Error: file tidak ada.

* $ rm -rf A C   
Menghapus seluruh direktori A dan C beserta isinya. Perintah -rf memaksa penghapusan rekursif tanpa konfirmasi.


### Percobaan 3 : Symbolic Link

### a. Analisis Hasil Tampilan

* $ echo "Hallo apa khabar" > halo.txt  
Membuat file teks.

* $ ls -l  
File halo.txt muncul.

* $ ln halo.txt z  
Membuat hard link z ke halo.txt.

* $ ls -l  
Dua file dengan ukuran sama dan link count menjadi 2 (kolom ketiga).

* $ cat z  
Menampilkan isi yang sama.

* $ mkdir mydir  
Membuat direktori.

* $ ln z mydir/halo.juga  
Membuat hard link lain di dalam mydir.
* $ cat mydir/halo.juga  
Isi sama.

* $ ln -s z bye.txt  
Membuat soft link bye.txt yang menunjuk ke z.

* $ ls -l bye.txt  
Menampilkan bye.txt -> z.

* $ cat bye.txt  
Membaca isi bye.txt (mengikuti link) dan menampilkan teks.

### Percobaan 4: Melihat Isi File

### a. Analisis Hasil Tampilan

* $ file halo.txt → output: halo.txt: ASCII text

* $ file bye.txt → output: bye.txt: symbolic link to z

### Percobaan 5: Mencari File

### a. Analisis Hasil Tampilan

*  $ find /home -name "*.txt" -print > myerror.txt  
Mencari semua file .txt di bawah /home, hasil disimpan ke myerror.txt.

* $ cat myerror.txt  
Menampilkan daftar file yang ditemukan.

* $ find . -name "*.txt" -exec wc -l '{}' ';'  
Menghitung jumlah baris setiap file .txt di direktori saat ini.

* $ which ls  
Menampilkan lokasi program ls, misal /bin/ls.

* $ locate "*.txt"  
Mencari semua file .txt menggunakan database locate.

### Percobaan 6: Mencari Teks pada File

### a. Analisis Hasil Tampilan

* $ grep Hallo *.txt  
Mencari kata "Hallo" di semua file .txt. Output menampilkan baris yang mengandung kata tersebut beserta nama file.



### Analisis Hasil Latihan

### Latihan 1: Urutan Perintah Navigasi

* $cd → pindah ke home.

* pwd → /home/user.

* ls -al → menampilkan semua file termasuk yang tersembunyi.

* cd . → tetap.

* pwd → /home/user.

* cd .. → pindah ke /home.

* pwd → /home.

* ls -al → menampilkan isi /home (direktori user).

* cd .. → pindah ke root (/).

* pwd → /.

* ls -al → menampilkan isi root.

* cd /etc → pindah ke /etc.

* ls -al | more → menampilkan isi /etc per halaman.

* cat passwd → menampilkan isi file /etc/passwd.

* cd - → kembali ke direktori sebelumnya, yaitu /.

* pwd → /.

### Latihan 2: Penelusuran Direktori Sistem

* /bin → berisi perintah dasar (binary) untuk semua user.

* /usr/bin → berisi lebih banyak perintah dan aplikasi.

* /sbin → berisi perintah untuk administrasi sistem (biasanya hanya root).

* /tmp → direktori sementara, dapat diakses semua user.

* /boot → berisi file boot seperti kernel dan initrd.

Semua direktori ditelusuri dengan cd, ls, dan cat untuk file teks (misal config di /boot).

### Latihan 3: Direktori /dev dan Terminal

* ls -l /dev menampilkan banyak file device.

* who am i menunjukkan terminal yang digunakan, misal pts/0.

* ls -l /dev/pts/0 menunjukkan pemilik terminal adalah user yang login (misal ubuntuser) dan group tty.

### Latihan 4: Direktori /proc

* cat /proc/interrupts, devices, cpuinfo, meminfo, uptime menampilkan informasi kernel.

* /proc disebut pseudo-filesystem karena file-file di dalamnya tidak tersimpan di disk, melainkan dibuat dinamis oleh kernel saat diakses.

### Latihan 5: cd ~username

* Jika user lain ada dan diizinkan, pindah ke home-nya. Biasanya user biasa tidak bisa karena izin, hanya root yang bisa.

### Latihan 6: cd kembali ke home sendiri.

### Latihan 7–8: Membuat dan menghapus direktori work dan play.

### Latihan 9–10: Menyalin /etc/passwd ke home lalu memindah ke play.

### Latihan 11: Symbolic link ke terminal

* ln -s /dev/pts/0 terminal berhasil.

* Hard link ke device gagal karena device file tidak mendukung hard link (berbeda filesystem dan tipe khusus).

### Latihan 12–13: File hello.txt

* cp terminal hello2.txt tidak menghasilkan efek sama karena membaca input.

* cp hello.txt /dev/pts/0 mencetak isi file ke layar.

### Latihan 14: Membuat symbolic link work ke play

* ln -s play work membuat link, bukan copy.

### Latihan 15: Menghapus link work

* rm -rf work hanya menghapus link, bukan direktori play.


### 3. Kesimpulan

Berdasarkan praktikum yang telah dilakukan, dapat disimpulkan bahwa sistem operasi Linux memiliki struktur sistem file yang bersifat hierarkis (berbentuk pohon) yang dimulai dari direktori root / dan bercabang ke berbagai direktori sistem seperti /bin, /usr, /sbin, /boot, /dev, /tmp, dan /home. Setiap direktori memiliki fungsi tertentu dalam pengelolaan sistem, misalnya /bin berisi perintah dasar, /boot berisi file yang digunakan saat proses booting, dan /dev berisi representasi perangkat keras dalam bentuk file.

Praktikum ini juga menunjukkan bagaimana pengguna dapat melakukan navigasi direktori menggunakan perintah seperti pwd, cd, dan ls untuk mengetahui lokasi direktori saat ini, berpindah direktori, serta melihat isi direktori. Selain itu, pengguna dapat mengelola direktori dan file menggunakan perintah seperti mkdir, rmdir, cp, mv, dan rm untuk membuat, menghapus, menyalin, memindahkan, atau mengganti nama file dan direktori.

Selanjutnya, praktikum ini memperkenalkan konsep link pada sistem file Linux, yaitu hard link dan symbolic link. Hard link menunjuk langsung ke inode file yang sama sehingga perubahan pada satu file akan mempengaruhi file lainnya, sedangkan symbolic link hanya berupa penunjuk (path) menuju file asli. Jika file asli dihapus maka symbolic link akan menjadi rusak. Pada percobaan juga terlihat bahwa symbolic link dapat menunjuk ke perangkat seperti terminal (/dev/tty), sehingga ketika file disalin ke link tersebut, isi file akan ditampilkan langsung pada terminal.

Selain itu, melalui direktori khusus seperti /dev dan /proc, pengguna dapat melihat bahwa Linux memperlakukan perangkat keras dan informasi kernel sebagai file. Direktori /dev berisi device file yang merepresentasikan perangkat sistem, sedangkan /proc merupakan pseudo-filesystem yang menyajikan informasi sistem secara dinamis dari kernel.

Dengan demikian, praktikum ini memberikan pemahaman mengenai struktur sistem file Linux, navigasi direktori, manipulasi file, serta konsep link dan device file, yang merupakan dasar penting dalam pengelolaan sistem operasi berbasis Linux.