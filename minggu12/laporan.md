<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## Praktek 10.1: Amati Layanan Aktif Saat Boot
Periksa layanan yang berjalan di sistem dan identifikasi layanan yang paling lambat saat boot.
1. Lihat semua layanan yang sedang berjalan.
```bash
systemctl list-units --type=service --state=running
# catat berapa banyak layanan yang aktif
```
Output:
```bash
  UNIT                        LOAD   ACTIVE SUB     DESCRIPTION>
  cron.service                loaded active running Regular bac>
  dbus.service                loaded active running D-Bus Syste>
  fwupd.service               loaded active running Firmware up>
  getty@tty1.service          loaded active running Getty on tt>
  ModemManager.service        loaded active running Modem Manag>
  multipathd.service          loaded active running Device-Mapp>
  polkit.service              loaded active running Authorizati>
  rsyslog.service             loaded active running System Logg>
  ssh.service                 loaded active running OpenBSD Sec>
  systemd-journald.service    loaded active running Journal Ser>
  systemd-logind.service      loaded active running User Login >
  systemd-networkd.service    loaded active running Network Con>
  systemd-resolved.service    loaded active running Network Nam>
  systemd-timesyncd.service   loaded active running Network Tim>
```

Amati: Setiap baris menampilkan nama unit, status aktif/tidaknya, status dari sudut pandang
systemd, dan deskripsi singkat.
2. Lihat semua unit service yang ada (aktif maupun tidak).

```bash
systemctl list-unit-files --type=service | head -30
# enabled = akan start otomatis saat boot
# disabled = tidak start otomatis , bisa dijalankan manual
# static = tidak bisa di - enable / disable , hanya dipanggil oleh layanan lain

```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl list-unit-files --type=service | head -30
UNIT FILE                                    STATE           PRESET
apparmor.service                             enabled         enabled
apport-autoreport.service                    static          -
apport-coredump-hook@.service                static          -
apport-forward@.service                      static          -
apport.service                               enabled         enabled
apt-daily-upgrade.service                    static          -
apt-daily.service                            static          -
apt-news.service                             static          -
autovt@.service                              alias           -
blk-availability.service                     enabled         enabled
bolt.service                                 static          -
cloud-config.service                         enabled         enabled
cloud-final.service                          enabled         enabled
cloud-init-hotplugd.service                  static          -
cloud-init-local.service                     enabled         enabled
cloud-init.service                           enabled         enabled
console-getty.service                        disabled        disabled
console-setup.service                        enabled         enabled
container-getty@.service                     static          -
cron.service                                 enabled         enabled
cryptdisks-early.service                     masked          enabled
cryptdisks.service                           masked          enabled
dbus-org.freedesktop.hostname1.service       alias           -
dbus-org.freedesktop.locale1.service         alias           -
dbus-org.freedesktop.login1.service          alias           -
dbus-org.freedesktop.ModemManager1.service   alias           -
dbus-org.freedesktop.resolve1.service        alias           -
dbus-org.freedesktop.thermald.service        alias           -
dbus-org.freedesktop.timedate1.service       alias           -
reyhandhika@reyhandhika:~/lab-os/chapter10-services$
```

3. Analisis waktu boot dan temukan layanan paling lambat
```bash
systemd-analyze
systemd-analyze blame | head -15
```
Output: 
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemd-analyze blame
1min 7.024s motd-news.service
    12.518s man-db.service
    10.031s snapd.seeded.service
     9.757s snapd.service
     7.679s logrotate.service
     6.169s dev-mapper-ubuntu\x2d\x2dvg\x2dubuntu\x2d\x2dlv.dev>
     5.586s systemd-networkd-wait-online.service
     5.014s apport.service
     4.726s apt-daily-upgrade.service
     4.711s rsyslog.service
     3.628s ModemManager.service
     3.184s apparmor.service
     3.118s fstrim.service
     3.007s udisks2.service
     2.991s polkit.service

reyhandhika@reyhandhika:~/lab-oschapter10-services$ systemd-analyze blame | head -15
1min 7.024s motd-news.service
    12.518s man-db.service
    10.031s snapd.seeded.service
     9.757s snapd.service
     7.679s logrotate.service
     6.169s dev-mapper-ubuntu\x2d\x2dvg\x2dubuntu\x2d\x2dlv.device
     5.586s systemd-networkd-wait-online.service
     5.014s apport.service
     4.726s apt-daily-upgrade.service
     4.711s rsyslog.service
     3.628s ModemManager.service
     3.184s apparmor.service
     3.118s fstrim.service
     3.007s udisks2.service
     2.991s polkit.service
```

# Tantangan
Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan.
Tuliskan nama layanan, waktu inisialisasinya  dan penjelasan singkat fungsinya.

```bash
systemd-analyze blame | sort -rh | head -3
systemctl cat snapd.service
systemd-analyze blame | head -10
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemd-analyze blame | sort -rh | head -3
        996ms modprobe@configfs.service
        920ms upower.service
        916ms multipathd.service
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl cat snapd.service
# /usr/lib/systemd/system/snapd.service
[Unit]
Description=Snap Daemon
After=snapd.socket
After=time-set.target
After=snapd.mounts.target
Wants=time-set.target
Wants=snapd.mounts.target
Requires=snapd.socket
OnFailure=snapd.failure.service
# This is handled by snapd
# X-Snapd-Snap: do-not-start

[Service]
# Disabled because it breaks lxd

reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemd-analyze blame | head -10
22min 20.064s apt-daily.service
  1min 7.024s motd-news.service
      12.518s man-db.service
      10.031s snapd.seeded.service
       9.757s snapd.service
       7.679s logrotate.service
       6.169s dev-mapper-ubuntu\x2d\x2dvg\x2dubuntu\x2d\x2dlv.device
       5.586s systemd-networkd-wait-online.service
       5.014s apport.service
       4.726s apt-daily-upgrade.service
       
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemd-analyze blame | head -3
22min 20.064s apt-daily.service
  1min 7.024s motd-news.service
      12.518s man-db.service
```
jadi
1. apt-daily.service
Waktu inisialisasi: 22 menit 20.064 detik
Fungsi:
Service yang menjalankan pembaruan paket APT otomatis pada Ubuntu.
2. motd-news.service
Waktu inisialisasi: 1 menit 7.024 detik
Fungsi:
Menampilkan informasi berita dan update sistem pada Message of the Day (MOTD) saat login terminal.
3. man-db.service
Waktu inisialisasi: 12.518 detik
Fungsi:
Mengelola database dokumentasi manual Linux (man command) agar pencarian dokumentasi lebih cepat.


## Praktek 10.2: Kelola Layanan SSH
Praktikkan semua operasi dasar systemctl pada layanan SSH yang tersedia di sistem.

1. Periksa status SSH secara menyeluruh.
```bash
systemctl status ssh
systemctl is-active ssh
systemctl is-enabled ssh
```
Amati: Output systemctl status menampilkan banyak informasi: status aktif/inactive, PID
proses utama, waktu mulai, penggunaan memori, dan beberapa baris log terbaru. Ini adalah
perintah pertama yang harus dijalankan ketika ada masalah layanan.

2. Lakukan restart dan pantau perubahannya.

```bash
sudo systemctl restart ssh
systemctl status ssh
# perhatikan : Loaded , Active , dan Main PID bisa berubah setelah restart

```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disab>
     Active: active (running) since Thu 2026-05-14 04:20:39 UTC>
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 4863 ExecStartPre=/usr/sbin/sshd -t (code=exited, >
   Main PID: 4865 (sshd)
      Tasks: 1 (limit: 2263)
     Memory: 1.2M (peak: 1.5M)
        CPU: 117ms
     CGroup: /system.slice/ssh.service
             └─4865 "sshd: /usr/sbin/sshd -D [listener] 0 of 10>

May 14 04:20:39 reyhandhika systemd[1]: Starting ssh.service - >
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl is-active ssh
active
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl is-enabled ssh
disabled
reyhandhika@reyhandhika:~/lab-os/chapter10-services$
```
3. Lihat dependensi SSH.

```bash
systemctl list-dependencies ssh
# layanan lain yang harus aktif sebelum SSH bisa berjalan
```
Output:
```bash
reyhandhika@reyhandhika:~$  systemctl list-dependencies ssh
ssh.service
● ├─-.mount
● ├─ssh.socket
● ├─system.slice
● └─sysinit.target
●   ├─apparmor.service
●   ├─blk-availability.service
●   ├─dev-hugepages.mount
●   ├─dev-mqueue.mount
●   ├─finalrd.service
●   ├─keyboard-setup.service
●   ├─kmod-static-nodes.service
○   ├─ldconfig.service
●   ├─lvm2-lvmpolld.socket
●   ├─lvm2-monitor.service
reyhandhika@reyhandhika:~$
```

4. Cek semua unit yang gagal di sistem.
```bash
systemctl --failed
# jika ada , ini adalah daftar layanan yang butuh perhatian
```
Output:
```bash
reyhandhika@reyhandhika:~$ systemctl --failed
  UNIT LOAD ACTIVE SUB DESCRIPTION

0 loaded units listed.
```

# Tantangan
Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi
minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.

```bash
#buat file daftar layanan
nano daftar-layanan.txt
#ketik 
ssh
cron
rsyslog
#buat cek layanan
nano cek-layanan.sh
#ketik isi script

#!/bin/bash

FILE_DAFTAR="daftar-layanan.txt"
FILE_LOG="laporan-layanan.log"

while read layanan
do
    STATUS=$(systemctl is-active $layanan)

    if [ "$STATUS" = "active" ]; then
        HASIL="ACTIVE"
    else
        HASIL="INACTIVE"
    fi

    echo "[$(date)] $layanan: $HASIL" >> $FILE_LOG

done < $FILE_DAFTAR

# Beri permission execute
chmod +x cek-layanan.sh
# jalankan Script
./cek-layanan.sh
#lihat hasil
cat laporan-layanan.log
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ ./cek-layanan.sh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ cat laporan-layanan.log
[Thu May 14 05:32:00 AM UTC 2026] ssh: ACTIVE
[Thu May 14 05:32:00 AM UTC 2026] cron: ACTIVE
[Thu May 14 05:32:00 AM UTC 2026] rsyslog: ACTIVE
```
## Praktek 10.3: Buat Layanan Sederhana dari Skrip Bash
Buat layanan systemd yang menjalankan server HTTP sederhana berbasis Python.
1. Siapkan konten yang akan dilayani.

```bash
cd ~/lab-os/chapter10-services
mkdir -p situs-demo
nano situs-demo/index.html
# Tulis isi berkas berikut
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>
```
2. Buat skrip wrapper untuk server HTTP

```bash
nano jalankan-server.sh
# Tulis isi berkas berikut
#!/bin/bash

DIREKTORI="$HOME/lab-os/chapter10-services/situs-demo"
PORT=9090

echo "Memulai server di port $PORT..."

exec python3 -m http.server $PORT --directory "$DIREKTORI"
chmod +x ~/lab-os/chapter10-services/jalankan-server.sh
```
3. Buat berkas unit systemd untuk layanan ini.

```bash
nano ~/lab-os/chapter10-services/demo-web.service
# Tulis isi berkas berikut
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=reyhandhika
WorkingDirectory=/home/reyhandhika/lab-os/chapter10-services/situs-demo
ExecStart=/usr/bin/python3 -m http.server 9090
Restart=on-failure
RestartSec=3s

[Install]
WantedBy=multi-user.target

# salin ke lokasi unit systemd
sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service
# minta systemd membaca ulang berkas unit yang baru dibuat
sudo systemctl daemon-reload
```
Amati: Perintah daemon-reload tidak me-restart layanan yang sedang berjalan. Perintah
ini hanya memberi tahu systemd untuk membaca ulang definisi unit dari disk. Harus selalu
dijalankan setiap kali berkas unit diubah.

4. Jalankan layanan dan verifikasi.
```bash
sudo systemctl start demo-web
systemctl status demo-web
# coba akses layanan
curl http://localhost:9090
```
5. Uji fitur restart otomatis.
```bash
# lihat PID proses saat ini
systemctl status demo-web | grep "Main PID"
# hentikan proses secara paksa ( simulasi crash )
sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
# tunggu beberapa detik lalu cek -- systemd harus menghidupkannya kembali
sleep 5
systemctl status demo-web
# PID akan berubah karena proses baru dijalankan
```
Amati: Berkat Restart=on-failure, systemd secara otomatis menjalankan ulang layanan
setelah proses mati secara tidak normal. Ini adalah fitur penting untuk layanan produksi.
6. Bersihkan layanan uji setelah selesai.
```bash
sudo systemctl disable --now demo-web
sudo rm /etc/systemd/system/demo-web.service
sudo systemctl daemon-reload
systemctl status demo-web
```

Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ mkdir -p situs-demo
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ nano situs-demo/index.html
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ nano jalankan-server.sh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ chmod +x ~/lab-os/chapter10-services/jalankan-server.sh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ nano ~/lab-os/chapter10-services/demo-web.service
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ nano ~/lab-os/chapter10-services/demo-web.service
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service
[sudo] password for reyhandhika:
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl daemon-reload
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl start demo-web
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; disa>
     Active: active (running) since Thu 2026-05-14 05:48:00 UTC>
   Main PID: 5417 (python3)
      Tasks: 1 (limit: 2263)
     Memory: 9.3M (peak: 9.5M)
        CPU: 193ms
     CGroup: /system.slice/demo-web.service
             └─5417 /usr/bin/python3 -m http.server 9090

May 14 05:48:00 reyhandhika systemd[1]: Started demo-web.servic>
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ curl http://localhost:9090
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>

reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status demo-web | grep "Main PID"
   Main PID: 5417 (python3)
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sleep 5
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; disa>
     Active: active (running) since Thu 2026-05-14 05:54:42 UTC>
   Main PID: 5435 (python3)
      Tasks: 1 (limit: 2263)
     Memory: 9.3M (peak: 9.5M)
        CPU: 158ms
     CGroup: /system.slice/demo-web.service
             └─5435 /usr/bin/python3 -m http.server 9090

May 14 05:54:42 reyhandhika systemd[1]: demo-web.service: Sched>
May 14 05:54:42 reyhandhika systemd[1]: Started demo-web.servic>
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl disable --now demo-web
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo rm /etc/systemd/system/demo-web.service
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl daemon-reload
```
# Tantangan
Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan
RestartSec=10s agar sistemmenunggu 10 detik sebelum mencoba restart, dan tambahkan Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut. Aktifkan layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif setelah systemctl daemon-reload. Dokumentasikan perbedaan perilaku dibanding versi sebelumnya

```bash
#buat file Service
nano ~/lab-os/chapter10-services/demo-web.service
# isi Baru
[Unit]
Description=Demo Web Server Praktek Bab 10
After=network.target

[Service]
Type=simple
User=reyhandhika
WorkingDirectory=/home/reyhandhika/lab-os/chapter10-services/situs-demo

Environment="PORT=9091"

ExecStart=/usr/bin/python3 -m http.server ${PORT}

Restart=on-failure
RestartSec=10s

[Install]
WantedBy=multi-user.target

#copy ke systemd
sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service

#realod systemd
sudo systemctl daemon-reload

#Enable dan Jalankan
sudo systemctl enable --now demo-web
# cek status
systemctl status demo-web

#test Port Baru
curl http://localhost:9091

#uji Restart Delay
sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ nano ~/lab-os/chapter10-services/demo-web.service
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp ~/lab-os/chapter10-services/demo-web.service /etc/systemd/system/demo-web.service
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl daemon-reload
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl enable --now demo-web
Created symlink /etc/systemd/system/multi-user.target.wants/demo-web.service → /etc/systemd/system/demo-web.service.
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enab>
     Active: active (running) since Thu 2026-05-14 06:01:05 UTC>
   Main PID: 5642 (python3)
      Tasks: 1 (limit: 2263)
     Memory: 9.3M (peak: 9.4M)
        CPU: 178ms
     CGroup: /system.slice/demo-web.service
             └─5642 /usr/bin/python3 -m http.server 9091

May 14 06:01:05 reyhandhika systemd[1]: Started demo-web.servic>
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ curl http://localhost:9091
<!DOCTYPE html>
<html>
<body>
<h1>Halo dari layanan systemd kustom!</h1>
<p>Layanan ini dibuat pada praktek Bab 10.</p>
</body>
</html>
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo kill -9 $(systemctl show demo-web --property=MainPID --value)
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status demo-web
● demo-web.service - Demo Web Server Praktek Bab 10
     Loaded: loaded (/etc/systemd/system/demo-web.service; enab>
     Active: activating (auto-restart) (Result: signal) since T>
    Process: 5642 ExecStart=/usr/bin/python3 -m http.server ${P>
   Main PID: 5642 (code=killed, signal=KILL)
        CPU: 212ms
```
Jawaban :
1. Berkas demo-web.service berhasil dimodifikasi dengan:
- RestartSec=10s
- Environment="PORT=9091"
2. Service berhasil diaktifkan menggunakan:
sudo systemctl enable --now demo-web
3. Web server berhasil berjalan pada port 9091.
4. Setelah proses dihentikan paksa menggunakan kill -9, systemd tidak langsung menjalankan ulang service, tetapi menunggu sekitar 10 detik sesuai konfigurasi RestartSec=10s.
5. Perbedaan dengan versi sebelumnya:
- versi lama restart lebih cepat (3s)
- versi baru restart lebih lambat (10s)
- konfigurasi port lebih fleksibel karena menggunakan variabel environment PORT.

## Praktek 10.4: Filter dan Analisis Log Layanan
Gunakan berbagai opsi journalctl untuk mencari informasi spesifik dalam log sistem.
1. Lihat log SSH dari satu jam terakhir.
```bash
journalctl -u ssh --since "1 hour ago" --no-pager
# jika tidak ada log SSH , gunakan layanan lain yang aktif
journalctl -u cron --since "1 hour ago" --no-pager
```
2. Filter log berprioritas error ke atas
```bash
journalctl -b -p err --no-pager
# ini menampilkan semua error dan yang lebih serius sejak boot
```
Amati: Log dengan prioritas err ke atas biasanya perlu diperhatikan. Catat layanan mana yang
menghasilkan error dan bacalah pesannya.

3. Ikuti log secara real-time sambil memicu aktivitas.
```bash
# jalankan di terminal pertama :
journalctl -u ssh -f
# di terminal kedua , coba login SSH ke localhost
# ssh localhost
# lalu lihat apa yang muncul di terminal pertama
```
4. Ekstrak log ke berkas untuk analisis.
```bash
cd ~/lab-os/chapter10-services
# simpan semua log layanan ssh dari hari ini ke berkas
journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
# hitung jumlah baris log
wc -l log-ssh-hari-ini.txt
# jika ada , cari baris yang mengandung kata " error " atau " failed "
grep -i "error\|failed" log-ssh-hari-ini.txt | head -20
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -u ssh --since "1 hour ago" --no-pager
-- No entries --
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -u cron --since "1 hour ago" --no-pager
May 14 05:25:01 reyhandhika CRON[5274]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 05:25:01 reyhandhika CRON[5275]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 05:25:01 reyhandhika CRON[5274]: pam_unix(cron:session): session closed for user root
May 14 05:35:01 reyhandhika CRON[5344]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 05:35:01 reyhandhika CRON[5345]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 05:35:01 reyhandhika CRON[5344]: pam_unix(cron:session): session closed for user root
May 14 05:45:01 reyhandhika CRON[5354]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 05:45:01 reyhandhika CRON[5355]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 05:45:01 reyhandhika CRON[5354]: pam_unix(cron:session): session closed for user root
May 14 05:55:01 reyhandhika CRON[5439]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 05:55:01 reyhandhika CRON[5440]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 05:55:01 reyhandhika CRON[5439]: pam_unix(cron:session): session closed for user root
May 14 06:05:01 reyhandhika CRON[5656]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 06:05:01 reyhandhika CRON[5657]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 06:05:01 reyhandhika CRON[5656]: pam_unix(cron:session): session closed for user root
May 14 06:15:01 reyhandhika CRON[5675]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 06:15:01 reyhandhika CRON[5676]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 06:15:01 reyhandhika CRON[5675]: pam_unix(cron:session): session closed for user root
May 14 06:17:01 reyhandhika CRON[5680]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
May 14 06:17:01 reyhandhika CRON[5681]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
May 14 06:17:01 reyhandhika CRON[5680]: pam_unix(cron:session): session closed for user root
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -b -p err --no-pager
Apr 30 11:47:05 reyhandhika kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* vmwgfx seems to be running on an unsupported hypervisor.
Apr 30 11:47:05 reyhandhika kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* This configuration is likely broken.
Apr 30 11:47:05 reyhandhika kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* Please switch to a supported graphics device to avoid problems.
Apr 30 11:47:29 reyhandhika login[760]: PAM unable to dlopen(pam_lastlog.so): /usr/lib/security/pam_lastlog.so: cannot open shared object file: No such file or directory
Apr 30 11:47:29 reyhandhika login[760]: PAM adding faulty module: pam_lastlog.so
Apr 30 12:31:22 reyhandhika systemd[1]: Failed to start fwupd-refresh.service - Refresh fwupd metadata and update motd.
Apr 30 13:26:46 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 221s! [swapper/0:0]
Apr 30 13:26:46 reyhandhika systemd[1]: systemd-logind.service: Watchdog timeout (limit 3min)!
Apr 30 13:26:46 reyhandhika systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
Apr 30 17:10:20 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 11435s! [swapper/0:0]
Apr 30 23:02:05 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 19495s! [(ostnamed):1423]
Apr 30 23:02:05 reyhandhika systemd[1]: systemd-udevd.service: Watchdog timeout (limit 3min)!
Apr 30 23:02:05 reyhandhika systemd[1]: systemd-logind.service: Watchdog timeout (limit 3min)!
Apr 30 23:02:05 reyhandhika systemd[1]: systemd-networkd.service: Watchdog timeout (limit 3min)!
Apr 30 23:02:05 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 154s! [apport:1435]
Apr 30 23:02:05 reyhandhika systemd[1]: Failed to start systemd-hostnamed.service - Hostname Service.
Apr 30 17:10:21 reyhandhika systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
Apr 30 23:02:07 reyhandhika systemd[1]: Failed to start systemd-journald.service - Journal Service.
Apr 30 23:18:43 reyhandhika systemd[1]: systemd-networkd.service: Watchdog timeout (limit 3min)!
Apr 30 23:18:34 reyhandhika systemd[1]: systemd-udevd.service: Watchdog timeout (limit 3min)!
Apr 30 23:18:34 reyhandhika systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
May 06 11:52:57 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 8408s! [apport:2591]
May 06 09:22:23 reyhandhika systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
May 13 14:06:23 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 4635s! [kworker/0:2:4312]
May 13 14:06:24 reyhandhika systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
May 14 05:07:19 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 703s! [swapper/0:0]
May 14 05:07:19 reyhandhika systemd[1]: systemd-journald.service: Watchdog timeout (limit 3min)!
May 14 05:16:37 reyhandhika kernel: watchdog: BUG: soft lockup - CPU#0 stuck for 88s! [swapper/0:0]
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -u ssh -f
May 14 04:20:39 reyhandhika systemd[1]: Stopping ssh.service - OpenBSD Secure Shell server...
May 14 04:20:39 reyhandhika systemd[1]: ssh.service: Deactivated successfully.
May 14 04:20:39 reyhandhika systemd[1]: Stopped ssh.service - OpenBSD Secure Shell server.
May 14 04:20:39 reyhandhika systemd[1]: ssh.service: Consumed 2.300s CPU time, 8.7M memory peak, 0B memory swap peak.
May 14 04:20:39 reyhandhika systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 14 04:20:39 reyhandhika sshd[4865]: Server listening on 0.0.0.0 port 22.
May 14 04:20:39 reyhandhika sshd[4865]: Server listening on :: port 22.
May 14 04:20:39 reyhandhika systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 14 05:16:53 reyhandhika sshd[5142]: Accepted password for reyhandhika from 10.104.10.114 port 51743 ssh2
May 14 05:16:53 reyhandhika sshd[5142]: pam_unix(sshd:session): session opened for user reyhandhika(uid=1000) by reyhandhika(uid=0)
ssh localhhost
^C
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ cd ~/lab-os/chapter10-services
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -u ssh --since today --no-pager > log-ssh-hari-ini.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ wc -l log-ssh-hari-ini.txt
13 log-ssh-hari-ini.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ grep -i "error\|failed" log-ssh-hari-ini.txt | head -20
reyhandhika@reyhandhika:~/lab-os/chapter10-services$
```
# Tantangan
Ekstrak semua log dengan prioritas error (-p err) dari 24 jam terakhir untuk layanan SSH, simpan ke berkas error-ssh-24jam.txt. Gunakan pipeline dari Bab 3 untuk menghitung total jumlah baris error dengan wc -l, lalu tampilkan 10 pesan error yang paling sering muncul menggunakan sort | uniq -c | sort -rn | head -10. Tuliskan perintah lengkap yang kamu gunakan.

```bash
# Menyimpan log error SSH 24 jam terakhir
journalctl -u ssh -p err --since "24 hours ago" --no-pager > error-ssh-24jam.txt
# hitung jumlah Error
wc -l error-ssh-24jam.txt
# tampilkan 10 Error Paling sering
sort error-ssh-24jam.txt | uniq -c | sort -rn | head -10
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -u ssh -p err --since "24 hours ago" --no-pager > error-ssh-24jam.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ wc -l error-ssh-24jam.txt
1 error-ssh-24jam.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sort error-ssh-24jam.txt | uniq -c | sort -rn | head -10
      1 -- No entries --
```
Kesimpulan: 
 Tidak ditemukan log error pada layanan SSH dalam 24 jam terakhir. Sistem SSH berjalan normal tanpa error yang tercatat di journalctl.

## Praktek 10.5: Konfigurasi SSH Server
Ubah port SSH ke port non-standar, validasi konfigurasi, dan verifikasi perubahan dengan ss.
1. Periksa konfigurasi SSH saat ini
```bash
sudo grep -n "^Port \|^#Port " /etc/ssh/sshd_config
ss -tlnp | grep ssh
```
2. Buat backup dan ubah port SSH.
```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.lab12
# ubah port dari 22 ke 2222 ( atau port lain yang belum dipakai )
sudo sed -i 's/^#Port 22/Port 2222/' /etc/ssh/sshd_config
# jika baris Port 22 tidak dikomentari :
# sudo sed -i 's/^ Port 22/ Port 2222/ ' /etc/ssh/ sshd_config
# verifikasi perubahan
grep "^Port" /etc/ssh/sshd_config
```
3. Validasi konfigurasi dan restart layanan.
```bash
# WAJIB : validasi sintaks sebelum restart
sudo sshd -t
echo "Kode keluar sshd -t: $?"
# kode 0 berarti sintaks valid
# restart layanan
sudo systemctl restart ssh
systemctl status ssh

```
Amati: Langkah validasi dengan sshd -t adalah kebiasaan penting. Pada server produksi yang
hanya bisa diakses lewat SSH, kesalahan konfigurasi yang menyebabkan SSH tidak bisa restart
berarti kamu terkunci dari server sendiri.

4. Verifikasi port baru dengan ss.
```bash
ss -tlnp | grep ssh
# seharusnya menampilkan port 2222 , bukan 22
# simpan hasil ke berkas bukti
ss -tlnp | grep ssh > ~/lab-os/chapter10-services/bukti-port-ssh.txt
cat ~/lab-os/chapter10-services/bukti-port-ssh.txt

```
5. Kembalikan port SSH ke 22 setelah praktek

```bash
sudo cp /etc/ssh/sshd_config.backup.lab12 /etc/ssh/sshd_config
sudo sshd -t
sudo systemctl restart ssh
ss -tlnp | grep ssh
# harus kembali ke port 22
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo grep -n "^Port \|^#Port " /etc/ssh/sshd_config
[sudo] password for reyhandhika:
23:#Port 22
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ ss -tlnp | grep ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.lab12
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sed -i 's/^#Port 22/Port 2222/' /etc/ssh/sshd_config
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ grep "^Port" /etc/ssh/sshd_config
Port 2222
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ grep "^Port" /etc/ssh/sshd_config
Port 2222
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ echo "Kode keluar sshd -t: $?"
Kode keluar sshd -t: 0
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl restart ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disab>
     Active: active (running) since Thu 2026-05-14 07:31:52 UTC>
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 5901 ExecStartPre=/usr/sbin/sshd -t (code=exited, >
   Main PID: 5903 (sshd)
      Tasks: 1 (limit: 2263)
     Memory: 1.2M (peak: 1.5M)
        CPU: 86ms
     CGroup: /system.slice/ssh.service
             └─5903 "sshd: /usr/sbin/sshd -D [listener] 0 of 10>

May 14 07:31:51 reyhandhika systemd[1]: Starting ssh.service - >
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ ss -tlnp | grep ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ ss -tlnp | grep ssh > ~/lab-os/chapter10-services/bukti-port-ssh.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ cat ~/lab-os/chapter10-services/bukti-port-ssh.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config.backup.lab12 /etc/ssh/sshd_config
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sshd -t
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl restart ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ ss -tlnp | grep ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$

reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo ss -tlnp | grep :22
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=5924,fd=3),("systemd",pid=1,fd=200))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=5924,fd=4),("systemd",pid=1,fd=201))
reyhandhika@reyhandhika:~/lab-os/chapter10-services$
```
# Tantangan
Ubah konfigurasi SSH untuk menambahkan dua pengaturan keamanan: PermitRootLogin no (larang login root langsung) dan MaxAuthTries 3 (maksimal tiga kali percobaan). Lakukan dengan urutan yang aman: backup, edit, validasi dengan sshd -t, reload. Verifikasi perubahan dengan grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config. Kemudian periksa log SSH untuk memastikan tidak ada error setelah perubahan dengan journalctl -u ssh -n 20. Referensi Bab 2 untuk penggunaan ss dan Bab 9 untuk keamanan pengguna.

```bash
# backup Konfigurasi
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.security
# Tambahkan Konfigurasi Keamanan
sudo nano /etc/ssh/sshd_config
#Validasi Konfigurasi
sudo sshd -t
echo $?
#Reload SSH
sudo systemctl reload ssh
# Verifikasi Konfigurasi
grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config
#Pastikan SSh Tetap Jalan
systemctl status ssh
#Cek Port SSH
sudo ss -tlnp | grep :22
#Periksa Log SSH
journalctl -u ssh -n 20 --no-pager
#Kembalikan Konfigurasi Semula
sudo cp /etc/ssh/sshd_config.backup.security /etc/ssh/sshd_config
#Validasi Lagi
sudo sshd -t
sudo systemctl reload ssh
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config.backup.lab12 /etc/ssh/sshd_config
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sshd -t
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl restart ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ ss -tlnp | grep ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo ss -tlnp | grep :22
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=5924,fd=3),("systemd",pid=1,fd=200))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=5924,fd=4),("systemd",pid=1,fd=201))
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.security
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo nano /etc/ssh/sshd_config






reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sshd -t
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ echo $?
0
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl reload ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config
#PermitRootLogin prohibit-password
#MaxAuthTries 6
# the setting of "PermitRootLogin prohibit-password".
PermitRootLogin no
MaxAuthTries 3
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Thu 2026-05-14 07:33:30 UTC; 14min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 5922 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 5961 ExecReload=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 5963 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
   Main PID: 5924 (sshd)
      Tasks: 1 (limit: 2263)
     Memory: 1.2M (peak: 2.7M)
        CPU: 168ms
     CGroup: /system.slice/ssh.service
             └─5924 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

May 14 07:33:30 reyhandhika systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 14 07:33:30 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:33:30 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:33:30 reyhandhika systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 14 07:47:30 reyhandhika systemd[1]: Reloading ssh.service - OpenBSD Secure Shell server...
May 14 07:47:30 reyhandhika sshd[5924]: Received SIGHUP; restarting.
May 14 07:47:30 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:47:30 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:47:30 reyhandhika systemd[1]: Reloaded ssh.service - OpenBSD Secure Shell server.
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo ss -tlnp | grep :22
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=5924,fd=3),("systemd",pid=1,fd=200))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=5924,fd=4),("systemd",pid=1,fd=201))
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -u ssh -n 20 --no-pager
May 14 07:31:51 reyhandhika sshd[4865]: Received signal 15; terminating.
May 14 07:31:51 reyhandhika systemd[1]: Stopping ssh.service - OpenBSD Secure Shell server...
May 14 07:31:51 reyhandhika systemd[1]: ssh.service: Deactivated successfully.
May 14 07:31:51 reyhandhika systemd[1]: Stopped ssh.service - OpenBSD Secure Shell server.
May 14 07:31:51 reyhandhika systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 14 07:31:52 reyhandhika sshd[5903]: Server listening on 0.0.0.0 port 22.
May 14 07:31:52 reyhandhika sshd[5903]: Server listening on :: port 22.
May 14 07:31:52 reyhandhika systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 14 07:33:30 reyhandhika systemd[1]: Stopping ssh.service - OpenBSD Secure Shell server...
May 14 07:33:30 reyhandhika systemd[1]: ssh.service: Deactivated successfully.
May 14 07:33:30 reyhandhika systemd[1]: Stopped ssh.service - OpenBSD Secure Shell server.
May 14 07:33:30 reyhandhika systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
May 14 07:33:30 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:33:30 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:33:30 reyhandhika systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
May 14 07:47:30 reyhandhika systemd[1]: Reloading ssh.service - OpenBSD Secure Shell server...
May 14 07:47:30 reyhandhika sshd[5924]: Received SIGHUP; restarting.
May 14 07:47:30 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:47:30 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:47:30 reyhandhika systemd[1]: Reloaded ssh.service - OpenBSD Secure Shell server.
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config.backup.security /etc/ssh/sshd_config
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sshd -t
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl reload ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$
```
Kesimpulan:  
Konfigurasi keamanan SSH berhasil ditambahkan dengan menonaktifkan login root langsung (PermitRootLogin no) dan membatasi percobaan login (MaxAuthTries 3). Konfigurasi berhasil divalidasi menggunakan sshd -t, layanan SSH tetap berjalan normal setelah reload, dan tidak ditemukan error pada log SSH.

# 1.7 Latihan
Instruksi Umum: Kerjakan seluruh latihan secara mandiri. Catat langkah penting, simpan tangkapan layar bila diperlukan, lalu rangkum hasilnya sebagai dokumentasi pribadi.

### Latihan 10.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.
```bash
systemctl list-units --type=service --state=running
systemctl status ssh
# Fungsi: Layanan untuk koneksi remote menggunakan protokol Secure Shell (SSH).
systemctl status cron
#Fungsi : Menjalankan tugas otomatis terjadwal di Linux.
systemctl status rsyslog
#fungsi: Mengelola dan menyimpan log sistem Linux.
```
Output:
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl list-units --type=service --state=running
  UNIT                        LOAD   ACTIVE SUB     DESCRIPTION
  cron.service                loaded active running Regular background program processing daemon
  dbus.service                loaded active running D-Bus System Message Bus
  demo-web.service            loaded active running Demo Web Server Praktek Bab 10
  fwupd.service               loaded active running Firmware update daemon
  getty@tty1.service          loaded active running Getty on tty1
  ModemManager.service        loaded active running Modem Manager
  multipathd.service          loaded active running Device-Mapper Multipath Device Controller
  polkit.service              loaded active running Authorization Manager
  rsyslog.service             loaded active running System Logging Service
  ssh.service                 loaded active running OpenBSD Secure Shell server
  systemd-journald.service    loaded active running Journal Service
  systemd-logind.service      loaded active running User Login Management
  systemd-networkd.service    loaded active running Network Configuration
  systemd-resolved.service    loaded active running Network Name Resolution
  systemd-timesyncd.service   loaded active running Network Time Synchronization
  systemd-udevd.service       loaded active running Rule-based Manager for Device Events and Files
  udisks2.service             loaded active running Disk Manager
  unattended-upgrades.service loaded active running Unattended Upgrades Shutdown
  upower.service              loaded active running Daemon for power management
  user@1000.service           loaded active running User Manager for UID 1000

Legend: LOAD   → Reflects whether the unit definition was properly loaded.
        ACTIVE → The high-level unit activation state, i.e. generalization of SUB.
        SUB    → The low-level unit activation state, values depend on unit type.

20 loaded units listed.
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Thu 2026-05-14 07:33:30 UTC; 27min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 5922 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 5990 ExecReload=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 5992 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
   Main PID: 5924 (sshd)
      Tasks: 1 (limit: 2263)
     Memory: 1.2M (peak: 2.7M)
        CPU: 250ms
     CGroup: /system.slice/ssh.service
             └─5924 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

May 14 07:47:30 reyhandhika systemd[1]: Reloading ssh.service - OpenBSD Secure Shell server...
May 14 07:47:30 reyhandhika sshd[5924]: Received SIGHUP; restarting.
May 14 07:47:30 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:47:30 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:47:30 reyhandhika systemd[1]: Reloaded ssh.service - OpenBSD Secure Shell server.
May 14 07:50:15 reyhandhika systemd[1]: Reloading ssh.service - OpenBSD Secure Shell server...
May 14 07:50:15 reyhandhika sshd[5924]: Received SIGHUP; restarting.
May 14 07:50:15 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:50:15 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:50:15 reyhandhika systemd[1]: Reloaded ssh.service - OpenBSD Secure Shell server.
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status cron
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-04-30 11:47:14 UTC; 1 week 6 days ago
       Docs: man:cron(8)
   Main PID: 723 (cron)
      Tasks: 1 (limit: 2263)
     Memory: 492.0K (peak: 2.9M)
        CPU: 4.287s
     CGroup: /system.slice/cron.service
             └─723 /usr/sbin/cron -f -P

May 14 06:35:01 reyhandhika CRON[5721]: pam_unix(cron:session): session closed for user root
May 14 07:35:01 reyhandhika CRON[5928]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=>
May 14 07:35:01 reyhandhika CRON[5929]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 07:35:01 reyhandhika CRON[5928]: pam_unix(cron:session): session closed for user root
May 14 07:45:01 reyhandhika CRON[5950]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=>
May 14 07:45:01 reyhandhika CRON[5951]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 07:45:01 reyhandhika CRON[5950]: pam_unix(cron:session): session closed for user root
May 14 07:55:01 reyhandhika CRON[5995]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=>
May 14 07:55:01 reyhandhika CRON[5996]: (root) CMD (command -v debian-sa1 > /dev/null && debian-sa1 1 1)
May 14 07:55:01 reyhandhika CRON[5995]: pam_unix(cron:session): session closed for user root
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status rsyslog
● rsyslog.service - System Logging Service
     Loaded: loaded (/usr/lib/systemd/system/rsyslog.service; enabled; preset: enabled)
     Active: active (running) since Thu 2026-04-30 11:47:15 UTC; 1 week 6 days ago
TriggeredBy: ● syslog.socket
       Docs: man:rsyslogd(8)
             man:rsyslog.conf(5)
             https://www.rsyslog.com/doc/
   Main PID: 694 (rsyslogd)
      Tasks: 4 (limit: 2263)
     Memory: 3.4M (peak: 5.1M)
        CPU: 2.044s
     CGroup: /system.slice/rsyslog.service
             └─694 /usr/sbin/rsyslogd -n -iNONE

Apr 30 11:47:10 reyhandhika systemd[1]: Starting rsyslog.service - System Logging Service...
Apr 30 11:47:14 reyhandhika rsyslogd[694]: imuxsock: Acquired UNIX socket '/run/systemd/journal/syslog' (fd 3) f>
Apr 30 11:47:14 reyhandhika rsyslogd[694]: rsyslogd's groupid changed to 104
Apr 30 11:47:14 reyhandhika rsyslogd[694]: rsyslogd's userid changed to 103
Apr 30 11:47:14 reyhandhika rsyslogd[694]: [origin software="rsyslogd" swVersion="8.2312.0" x-pid="694" x-info=">
Apr 30 11:47:15 reyhandhika systemd[1]: Started rsyslog.service - System Logging Service.
May 13 11:14:17 reyhandhika systemd[1]: rsyslog.service: Sent signal SIGHUP to main process 694 (rsyslogd) on cl>
May 13 11:14:17 reyhandhika rsyslogd[694]: [origin software="rsyslogd" swVersion="8.2312.0" x-pid="694" x-info=">

```
2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.
```bash
systemd-analyze blame | head -5
```
Output: 
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemd-analyze blame | head -5
22min 20.064s apt-daily.service
  1min 7.024s motd-news.service
      12.518s man-db.service
      10.127s demo-web.service
      10.031s snapd.seeded.service
```
```bash
Jawaban:
Penjelasan layanan
1. apt-daily.service
Waktu: 22 menit 20.064 detik
Fungsi: Menjalankan pembaruan paket APT otomatis pada Ubuntu.

2. motd-news.service
Waktu: 1 menit 7.024 detik
Fungsi: Menampilkan informasi berita dan update sistem pada Message of the Day (MOTD).

3. man-db.service
Waktu: 12.518 detik
Fungsi: Mengelola database dokumentasi manual Linux (man).

4. demo-web.service
Waktu: 10.127 detik
Fungsi: Layanan web server kustom berbasis Python HTTP server yang dibuat pada praktikum.
5. snapd.seeded.service
Waktu: 10.031 detik
Fungsi: Mengelola inisialisasi dan konfigurasi awal paket Snap pada Ubuntu.
```

3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, caritahu penyebabnya dengan journalctl -u nama-layanan -n 30.
```bash
systemctl --failed
journalctl -u nama-layanan -n 30
```

Output:

```bash
reyhandhika@reyhandhika:~$ systemctl --failed
  UNIT LOAD ACTIVE SUB DESCRIPTION

0 loaded units listed.
reyhandhika@reyhandhika:~$ journalctl -u nama-layanan -n 30
```
Jawaban:  
journalctl -u nama-layanan -n 30

### Latihan 10.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.

1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
```bash
# Membuat Script Monitoring Disk
nano monitor-disk.sh
# isi Script 

#!/bin/bash

while true
do
    echo "===== $(date) =====" >> disk-monitor.log
    df -h >> disk-monitor.log
    echo "" >> disk-monitor.log

    sleep 30
done

chmod +x monitor-disk.sh
```
2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip
tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.

```bash
# Membuat Berkas Unit systemd
nano monitor-disk.service
# isi File Service
[Unit]
Description=Monitor Disk Service
After=network.target

[Service]
Type=simple
User=reyhandhika
WorkingDirectory=/home/reyhandhika/lab-os/chapter10-services
ExecStart=/home/reyhandhika/lab-os/chapter10-services/monitor-disk.sh
Restart=always
RestartSec=5s

[Install]
WantedBy=multi-user.target

#Copy ke Systemd
sudo cp monitor-disk.service /etc/systemd/system/monitor-disk.service
#Reload Systemd
sudo systemctl daemon-reload
```
3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk
ke journal.

```bash
sudo systemctl enable --now monitor-disk
systemctl status monitor-disk
```
4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan
verifikasi bahwa layanan hidup kembali secara otomatis.

```bash
sudo kill -9 $(systemctl show monitor-disk --property=MainPID --value)
sleep 10
systemctl status monitor-disk
```
5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.

```bash
sudo systemctl disable --now monitor-disk
sudo rm /etc/systemd/system/monitor-disk.service
sudo systemctl daemon-reload
```
Kesimpulan

Layanan monitor-disk.service berhasil dibuat menggunakan systemd dan dapat berjalan otomatis di background. Fitur Restart=always memungkinkan layanan aktif kembali secara otomatis setelah crash.

### Latihan 10.3 Investigasi Log dan Keamanan SSH
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.
1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l.

```bash
cd ~/lab-os/chapter10-services
journalctl -b -p err --no-pager > error-boot.txt
wc -l error-boot.txt
```

2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin
no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd
-t, reload.

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.latihan
sudo nano /etc/ssh/sshd_config
# tambahkan di bagian Bawan 
PermitRootLogin no
MaxAuthTries 3
LoginGraceTime 30

sudo sshd -t
echo $?
sudo systemctl reload ssh
```
3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
```bash
systemctl status ssh
sudo ss -tlnp | grep :22
grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config
```

4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
```bash
sudo cp /etc/ssh/sshd_config.backup.latihan /etc/ssh/sshd_config
sudo sshd -t
sudo systemctl reload ssh
```
Output: 
```bash
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ cd ~/lab-os/chapter10-services
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ journalctl -b -p err --no-pager > error-boot.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ wc -l error-boot.txt
36 error-boot.txt
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup.latihan
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo nano /etc/ssh/sshd_config
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sshd -t
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ echo $?
0
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl reload ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
     Active: active (running) since Thu 2026-05-14 07:33:30 UTC; 5h 36min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 6559 ExecReload=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
    Process: 6562 ExecReload=/bin/kill -HUP $MAINPID (code=exited, status=0/SUCCESS)
   Main PID: 5924 (sshd)
      Tasks: 1 (limit: 2263)
     Memory: 3.0M (peak: 4.5M)
        CPU: 773ms
     CGroup: /system.slice/ssh.service
             └─5924 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

May 14 07:50:15 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 07:50:15 reyhandhika sshd[5924]: Server listening on :: port 22.
May 14 07:50:15 reyhandhika systemd[1]: Reloaded ssh.service - OpenBSD Secure Shell server.
May 14 12:30:07 reyhandhika sshd[6152]: Accepted password for reyhandhika from 10.104.10.114 port 59099 ssh2
May 14 12:30:07 reyhandhika sshd[6152]: pam_unix(sshd:session): session opened for user reyhandhika(uid=1000) by reyhandhika(uid=0)
May 14 13:10:01 reyhandhika systemd[1]: Reloading ssh.service - OpenBSD Secure Shell server...
May 14 13:10:01 reyhandhika systemd[1]: Reloaded ssh.service - OpenBSD Secure Shell server.
May 14 13:10:01 reyhandhika sshd[5924]: Received SIGHUP; restarting.
May 14 13:10:01 reyhandhika sshd[5924]: Server listening on 0.0.0.0 port 22.
May 14 13:10:01 reyhandhika sshd[5924]: Server listening on :: port 22.
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo ss -tlnp | grep :22
LISTEN 0      4096         0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=5924,fd=3),("systemd",pid=1,fd=195))
LISTEN 0      4096            [::]:22           [::]:*    users:(("sshd",pid=5924,fd=4),("systemd",pid=1,fd=196))
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config
#LoginGraceTime 2m
#PermitRootLogin prohibit-password
#MaxAuthTries 6
# the setting of "PermitRootLogin prohibit-password".
PermitRootLogin no
MaxAuthTries 3
LoginGraceTime 30
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo cp /etc/ssh/sshd_config.backup.latihan /etc/ssh/sshd_config
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo sshd -t
reyhandhika@reyhandhika:~/lab-os/chapter10-services$ sudo systemctl reload ssh
reyhandhika@reyhandhika:~/lab-os/chapter10-services$
```

Kesimpulan

Pada latihan ini berhasil dilakukan investigasi log sistem menggunakan journalctl serta konfigurasi keamanan SSH menggunakan sshd_config. Konfigurasi keamanan berhasil ditambahkan dan divalidasi tanpa error menggunakan sshd -t. Setelah reload, layanan SSH tetap berjalan normal dan tetap listening pada port 22. Konfigurasi kemudian berhasil dikembalikan ke kondisi awal menggunakan file backup.