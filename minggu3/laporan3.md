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


Output:
```bash
_apt
backup
bin
daemon
dhcpcd
fwupd-refresh
games
irc
landscape
list
lp
mail
man
messagebus
news
nobody
polkitd
pollinate
proxy
reyhandhika
root
sshd
sync
sys
syslog
systemd-network
systemd-resolve
systemd-timesync
tcpdump
tss
usbmux
uucp
uuidd
www-data
```

## Latihan 3.3

Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file

### Jawaban    
kode:
```bash
LOGFILE="system-monitor-$(date +%Y%m%d-%H%M%S).log"
ITERATIONS=12
COUNTER=1

echo "===== SYSTEM MONITORING LOG =====" | tee -a "$LOGFILE"
echo "Start time: $(date)" | tee -a "$LOGFILE"
echo "Monitoring setiap 5 detik selama 1 menit" | tee -a "$LOGFILE"
echo "===================================" | tee -a "$LOGFILE"
echo "" | tee -a "$LOGFILE"

while [ $COUNTER -le $ITERATIONS ]; do
    TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S")

    echo "[$TIMESTAMP] Iterasi ke-$COUNTER" | tee -a "$LOGFILE"
    echo "-----------------------------------" | tee -a "$LOGFILE"

    echo "CPU Usage:" | tee -a "$LOGFILE"
    top -bn1 | grep "Cpu(s)" | tee -a "$LOGFILE"

    echo "Memory Usage:" | tee -a "$LOGFILE"
    free -h | tee -a "$LOGFILE"

    echo "Load Average:" | tee -a "$LOGFILE"
    uptime | tee -a "$LOGFILE"

    echo "" | tee -a "$LOGFILE"

    COUNTER=$((COUNTER + 1))

    if [ $COUNTER -le $ITERATIONS ]; then
        sleep 5
    fi
done

echo "===================================" | tee -a "$LOGFILE"
echo "Monitoring selesai: $(date)" | tee -a "$LOGFILE"
echo "Log disimpan di: $LOGFILE"
```
Output:
```bash
===== SYSTEM MONITORING LOG =====
Start time: Tue Mar 10 10:43:48 AM UTC 2026
Monitoring setiap 5 detik selama 1 menit
===================================

[2026-03-10 10:43:48] Iterasi ke-1
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 26.7 sy,  0.0 ni, 40.0 id,  6.7 wa,  0.0 hi, 26.7 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       399Mi       903Mi       1.1Mi       826Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:43:49 up 2 days,  4:45,  3 users,  load average: 0.01, 2.19, 10.43

[2026-03-10 10:43:54] Iterasi ke-2
-----------------------------------
CPU Usage:
%Cpu(s): 11.1 us,  0.0 sy,  0.0 ni, 77.8 id,  0.0 wa,  0.0 hi, 11.1 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       398Mi       903Mi       1.1Mi       827Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:43:54 up 2 days,  4:45,  3 users,  load average: 0.01, 2.15, 10.38

[2026-03-10 10:43:59] Iterasi ke-3
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 10.0 sy,  0.0 ni, 60.0 id,  0.0 wa,  0.0 hi, 30.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       398Mi       903Mi       1.1Mi       827Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:00 up 2 days,  4:45,  3 users,  load average: 0.01, 2.12, 10.32

[2026-03-10 10:44:05] Iterasi ke-4
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 75.0 id,  0.0 wa,  0.0 hi, 25.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       397Mi       903Mi       1.1Mi       827Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:05 up 2 days,  4:45,  3 users,  load average: 0.09, 2.10, 10.27

[2026-03-10 10:44:10] Iterasi ke-5
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 11.1 sy,  0.0 ni, 77.8 id,  0.0 wa,  0.0 hi, 11.1 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       397Mi       903Mi       1.1Mi       828Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:11 up 2 days,  4:45,  3 users,  load average: 0.08, 2.06, 10.22

[2026-03-10 10:44:16] Iterasi ke-6
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  9.1 sy,  0.0 ni, 63.6 id,  0.0 wa,  0.0 hi, 27.3 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       396Mi       903Mi       1.1Mi       828Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:16 up 2 days,  4:45,  3 users,  load average: 0.08, 2.03, 10.16

[2026-03-10 10:44:21] Iterasi ke-7
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 11.1 sy,  0.0 ni, 77.8 id,  0.0 wa,  0.0 hi, 11.1 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       396Mi       903Mi       1.1Mi       829Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:22 up 2 days,  4:45,  3 users,  load average: 0.07, 1.99, 10.11

[2026-03-10 10:44:27] Iterasi ke-8
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni, 87.5 id,  0.0 wa,  0.0 hi, 12.5 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       396Mi       903Mi       1.1Mi       829Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:27 up 2 days,  4:45,  3 users,  load average: 0.06, 1.96, 10.05

[2026-03-10 10:44:32] Iterasi ke-9
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 11.1 sy,  0.0 ni, 77.8 id,  0.0 wa,  0.0 hi, 11.1 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       395Mi       903Mi       1.1Mi       830Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:32 up 2 days,  4:45,  3 users,  load average: 0.05, 1.89, 9.94

[2026-03-10 10:44:37] Iterasi ke-10
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 11.1 sy,  0.0 ni, 77.8 id,  0.0 wa,  0.0 hi, 11.1 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       395Mi       903Mi       1.1Mi       830Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:38 up 2 days,  4:46,  3 users,  load average: 0.05, 1.86, 9.89

[2026-03-10 10:44:43] Iterasi ke-11
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 11.1 sy,  0.0 ni, 66.7 id,  0.0 wa,  0.0 hi, 22.2 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       394Mi       903Mi       1.1Mi       830Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:43 up 2 days,  4:46,  3 users,  load average: 0.04, 1.83, 9.84

[2026-03-10 10:44:48] Iterasi ke-12
-----------------------------------
CPU Usage:
%Cpu(s):  0.0 us, 10.0 sy,  0.0 ni, 80.0 id,  0.0 wa,  0.0 hi, 10.0 si,  0.0 st
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       394Mi       903Mi       1.1Mi       831Mi       1.5Gi
Swap:          2.0Gi          0B       2.0Gi
Load Average:
 10:44:49 up 2 days,  4:46,  3 users,  load average: 0.04, 1.80, 9.78

===================================
Monitoring selesai: Tue Mar 10 10:44:49 AM UTC 2026
Log disimpan di: system-monitor-20260310-104348.log
```

## Latihan 3.4
Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file

### Jawaban :

Kode :  
```bash
find / -name "*.conf" 2> /dev/null | tee all-config-files.txt | wc -l
```
Output :  
```bash
397
```
## Latihan 3.5

Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry

### Jawaban :  

Kode :  
```bash
tar -cvf backup.tar praktikum-os 2> backup-error.log | while read line; do echo "$(date '+%F %T') $line"; done | tee backup-success.log
```
Output :  
```bash
2026-03-10 10:50:54 praktikum-os/
2026-03-10 10:50:54 praktikum-os/week02/
2026-03-10 10:50:54 praktikum-os/week02/server.log
2026-03-10 10:50:54 praktikum-os/week02/data.log
2026-03-10 10:50:54 praktikum-os/week02/note.txt
2026-03-10 10:50:54 praktikum-os/week02/server1.log
2026-03-10 10:50:55 praktikum-os/week02/server1.logbak
2026-03-10 10:50:55 praktikum-os/week02/config.txt
```


