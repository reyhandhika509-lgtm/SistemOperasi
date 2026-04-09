### Laporan Praktikum 7

<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## Praktikum 6.1 — Mengenali Bash dan Menyiapkan Workspace
Tujuan: mengenali shell aktif dan menyiapkan area kerja yang aman untuk seluruh
praktikum bab ini
1. Lihat shell login dan shell aktif saat ini:
```bash
echo " Shell login : $SHELL "
echo " Shell aktif : $0"
bash -- version | head -n 1
```
Output:
```bash
reyhandhika@reyhandhika:~$ echo "Shell login : $SHELL"
Shell login : /bin/bash
reyhandhika@reyhandhika:~$ echo "Shell aktif : $0"
Shell aktif : -bash
reyhandhika@reyhandhika:~$ bash --version | head -n 1
GNU bash, version 5.2.21(1)-release (x86_64-pc-linux-gnu)
```
2. Lihat proses shell yang sedang berjalan:
```bash
echo $$
ps -p $$ -o pid , ppid , args =
```
Output:
```bash
reyhandhika@reyhandhika:~$ echo $$
1065
reyhandhika@reyhandhika:~$ ps -p $$ -o pid,ppid,args=
    PID    PPID
   1065    1064 -bash
```
3. Buat workspace praktikum:
```bash
mkdir -p ~/ praktikum - os / week07 - bash /{ bin , backup , logs ,
sampel , ruang - nama }
cd ~/ praktikum - os / week04 - bash
pwd
```
Output:
```bash
reyhandhika@reyhandhika:~$ mkdir -p ~/ praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
reyhandhika@reyhandhika:~$ cd ~/praktikum-os/week07-bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ pwd
/home/reyhandhika/praktikum-os/week07-bash
```
4. Buat beberapa file contoh yang akan dipakai pada praktikum berikutnya:
```bash
touch sample - app . conf
touch logs / app -01. log logs / app -02. log logs / app -03. log
touch sampel / catatan - a . txt sampel / catatan - b . txt
touch sampel / backup -01. tar sampel / backup -02. tar
touch sampel / laporan - harian . log sampel / laporan -
mingguan . log sampel / laporan - bulanan . log
touch "ruang - nama / laporan server april .txt"
touch "ruang - nama / backup [ mingguan ] server . conf "
ls -R
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch sample-app.conf
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch logs/app-01.log logs/app-02.log logs/app-03.log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch sampel/catatan-a.txt sampel/catatan-b.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch sampel/backup-01.tar sampel/backup-02.tar
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch sampel/laporan-harian.log sampel/laporan-mingguan.log sampel/laporan-bulanan.log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch "ruang-nama/laporan server april.txt"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch "ruang-nama/backup [mingguan] server.conf"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls -R
.:
backup  bin  logs  ruang-nama  sampel  sample-app.conf

./backup:

./bin:

./logs:
app-01.log  app-02.log  app-03.log

./ruang-nama:
'backup [mingguan] server.conf'  'laporan server april.txt'

./sampel:
backup-01.tar  catatan-b.txt        laporan-mingguan.log
backup-02.tar  laporan-bulanan.log
catatan-a.txt  laporan-harian.log
```
## Praktikum 6.2 — Membuat Ringkasan Sesi Terminal
Tujuan: membiasakan administrator memverifikasi konteks kerja sebelum melakukan
maintenance.
1. Masuk ke workspace praktikum:
```bash
cd ~/ praktikum - os / week04 - bash
```
2. Simpan informasi sesi terminal ke file laporan:
```bash
{
echo "=== RINGKASAN SESI BASH ==="
date
echo " User : $( whoami )"
echo " Hostname : $( hostname )"
echo " Shell login : $SHELL "
echo " Shell aktif : $0"
echo "PID shell : $$"
echo " Direktori : $(pwd)"
} | tee session - info . txt
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week04-bash$ {
> echo "=== RINGKASAN SESI BASH ==="
> date
> echo "User        : $(whoami)"
> echo "Hostname    : $(hostname)"
> echo "Shell login : $SHELL"
> echo "Shell aktif : $0"
> echo "PID shell   : $$"
> echo "Direktori   : $(pwd)"
> } | tee session-info.txt
=== RINGKASAN SESI BASH ===
Wed Apr  8 05:08:11 AM UTC 2026
User        : reyhandhika
Hostname    : reyhandhika
Shell login : /bin/bash
Shell aktif : -bash
PID shell   : 1316
Direktori   : /home/reyhandhika/praktikum-os/week04-bash
```
3. Verifikasi isi file laporan:
```bash
cat session - info . txt
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week04-bash$ cat session-
info.txt
=== RINGKASAN SESI BASH ===
Wed Apr  8 05:08:11 AM UTC 2026
User        : reyhandhika
Hostname    : reyhandhika
Shell login : /bin/bash
Shell aktif : -bash
PID shell   : 1316
Direktori   : /home/reyhandhika/praktikum-os/week04-bash
```
## Praktikum 6.3 — Menambahkan Konfigurasi Aman pada .bashrc
Tujuan: memahami peran .bashrc dan menerapkan perubahan secara aman
1. Lihat file konfigurasi Bash pada home directory:
```bash
ls - la ~ | grep -E 'bashrc | bash_profile | profile '
```
Output:
```bash
reyhandhika@reyhandhika:~$ ls -la ~ | grep -E 'bashrc|bash_profile|profile'
-rw-r--r-- 1 reyhandhika reyhandhika  3771 Mar 31  2024 .bashrc
-rw-r--r-- 1 reyhandhika reyhandhika   807 Mar 31  2024 .profil
```
2. Buat backup .bashrc:
```bash
cp ~/. bashrc ~/. bashrc . bak - praktikum
```
Output:
```bash
reyhandhika@reyhandhika:~$ cp ~/.bashrc ~/.bashrc.bak-praktikum
reyhandhika@reyhandhika:~$
```
3. Tambahkan blok konfigurasi praktikum:
```bash
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum Bash Shell ---
export PRAKTIKUM_BASH_DIR =" $HOME / praktikum -os/week04 -
bash "
export EDITOR = nano
# --- End Praktikum Bash Shell ---
EOF
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat <<'EOF' >> ~/.bashrc
> # --- Praktikum Bash Shell ---
> export PRAKTIKUM_BASH_DIR="$HOME/praktikum-os/week04-bash"
> export EDITOR=nano
> # --- End Praktikum Bash Shell ---
>
> EOF
```
4. Terapkan konfigurasi tanpa logout:
```bash
source ~/. bashrc
echo " $PRAKTIKUM_BASH_DIR "
echo " $EDITOR "
```
Output:
```bash
reyhandhika@reyhandhika:~$ source ~/.bashrc
reyhandhika@reyhandhika:~$ echo "$PRAKTIKUM_BASH_DIR"
/home/reyhandhika/praktikum-os/week04-bash
reyhandhika@reyhandhika:~$ echo "$EDITOR"
nano
```
## Praktikum 6.4 — Menyiapkan .bash_profile untuk Shell Login
Tujuan: memahami hubungan .bash_profile dan .bashrc pada skenario login
shell
1. Backup .bash_profile jika sudah ada:
```bash
[ -f ~/. bash_profile ] && cp ~/. bash_profile ~/.
bash_profile . bak - praktikum
Kode 1.12: Backup .bash_profi
```
Output:
```bash
reyhandhika@reyhandhika:~$ [ -f ~/.bash_profile ] && cp ~/.bash_profile ~/.bash_profile.bak-praktikum
```
2. Tambahkan konfigurasi login shell:
```bash
cat <<'EOF ' >> ~/. bash_profile
# --- Praktikum Bash Login Shell ---
if [ -f ~/. bashrc ]; then
. ~/. bashrc
fi
echo " Login Bash pada $( date '+%F %T ')" >> " $HOME /
praktikum -os/week07 - bash /login - audit .log"
# --- End Praktikum Bash Login Shell ---
EOF
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat <<'EOF' >> ~/.bash_profile
> # --- Praktikum Bash Login Shell ---
> if [ -f ~/. bashrc ]; then
> . ~/. bashrc
> fi
>
> echo " Login Bash pada $(date '+%F %T ')" >> "$HOME/praktikum
-os/week07-bash/login-audit.log"
> # --- End Praktikum Bash Login Shell ---
>
> EOF
```
3. Uji dengan membuka login shell baru:
```bash
bash -l
tail -n 3 ~/ praktikum - os / week07 - bash / login - audit . log
exit
```
Output:
```bash
reyhandhika@reyhandhika:~$ bash -l
reyhandhika@reyhandhika:~$ tail -n 3 ~/praktikum-os/week07-bash/login-audit.log
Login Bash pada 2026-04-08 06:42:23
Login Bash pada 2026-04-08 06:42:36
Login Bash pada 2026-04-08 06:44:34
reyhandhika@reyhandhika:~$
```
## Praktikum 6.5 — Membedakan Variabel Shell dan Environment Variable
Tujuan: memahami perbedaan variabel lokal dan variabel lingkungan
1. Buat variabel lokal:
```bash
KELAS_OS=" Sistem Operasi A"
echo "$KELAS_OS"
```
Output:
```bash
KELAS_OS: command not found
reyhandhika@reyhandhika:~$ KELAS_OS=" Sistem Operasi A"
reyhandhika@reyhandhika:~$ echo "$KELAS_OS"
 Sistem Operasi A
```
2. Buka subshell dan cek apakah variabel masih ada:
```bash
bash
echo "$KELAS_OS"
exit
```
Output:
```bash
reyhandhika@reyhandhika:~$ bash
reyhandhika@reyhandhika:~$ echo "$KELAS_OS"

reyhandhika@reyhandhika:~$ exit
exit
```
3. Sekarang ubah menjadi environment variable:
```bash
export KELAS_OS =" Sistem Operasi A"
bash
echo " $KELAS_OS "
exit
```
Output:
```bash
reyhandhika@reyhandhika:~$ export KELAS_OS="Sistem Operasi A"
reyhandhika@reyhandhika:~$ bash
reyhandhika@reyhandhika:~$ echo "$KELAS_OS"
Sistem Operasi A
reyhandhika@reyhandhika:~$ exit
exit
```
4. Lihat isi PATH dan lokasi beberapa perintah:
```bash
echo " $PATH "
which bash
type ls\
```
Output:
```bash
reyhandhika@reyhandhika:~$ echo "$PATH"
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
reyhandhika@reyhandhika:~$ which bash
/usr/bin/bash
reyhandhika@reyhandhika:~$ type ls
ls is aliased to `ls --color=auto'
```
## Praktikum 6.6 — Menambahkan Direktori Script Pribadi ke PATH
Tujuan: membuat perintah administrasi sederhana yang bisa dipanggil dari mana
saja
1. Pastikan direktori bin praktikum tersedia:
```bash
mkdir -p ~/ praktikum - os / week07 - bash / bin
```
Output:
```bash
reyhandhika@reyhandhika:~$ mkdir -p ~/praktikum-os/week07-bash/bin
```
2. Tambahkan direktori tersebut ke PATH melalui .bashrc:
```bash
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum PATH ---
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
# --- End Praktikum PATH ---
EOF
source ~/.bashrc
echo "$PATH"
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat <<'EOF' >> ~/.bashrc
> # --- Praktikum PATH ---
> export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
> # --- End Praktikum PATH ---
> EOF
reyhandhika@reyhandhika:~$ source ~/.bashrc
reyhandhika@reyhandhika:~$ echo "$PATH"
/home/reyhandhika/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```
3. Buat script ringkasan sistem:
```bash
cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
#!/usr/bin/env bash
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "Uptime : $(uptime -p)"
echo "Disk / :"
df -h /
EOF
chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
> #!/usr/bin/env bash
> echo "Hostname : $(hostname)"
> echo "User : $(whoami)"
> echo "Uptime : $(uptime -p)"
> echo "Disk / :"
> df -h /
> EOF
reyhandhika@reyhandhika:~$ chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
```
4. Jalankan script dari direktori yang berbeda:
```bash
cd ~
ringkas - sistem
```
Output:
```bash
reyhandhika@reyhandhika:~$ cd ~
reyhandhika@reyhandhika:~$ ringkas-sistem
Hostname : reyhandhika
User : reyhandhika
Uptime : up 3 hours, 16 minutes
Disk / :
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.6G  5.1G  53% /
```
## Praktikum 6.7 — Membuat Alias Produktivitas Dasar
Tujuan: membuat shortcut perintah yang sering dipakai.
1. Tambahkan alias ke .bashrc:
```bash
cat <<'EOF' >> ~/.bashrc
# --- Praktikum Alias ---
alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias cdbashlab='cd $HOME/praktikum-os/week04-bash'
# --- End Praktikum Alias ---
EOF
source ~/.bashrc
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat <<'EOF' >> ~/.bashrc
> # --- Praktikum Alias ---
> alias ll='ls -lah --color=auto'
> alias hist10='history | tail -n 10'
> alias cdbashlab='cd $HOME/praktikum-os/week04-bash'
> # --- End Praktikum Alias ---
> EOF
reyhandhika@reyhandhika:~$ source ~/.bashrc
reyhandhika@reyhandhika:~$
```
2. Uji alias:
```bash
ll
hist10
cdbashlab
pwd
type ll
```
Output:
```bash
reyhandhika@reyhandhika:~$ ll
total 152K
drwxr-x--- 8 reyhandhika reyhandhika 4.0K Apr  8 06:43  .
drwxr-xr-x 3 root        root        4.0K Feb 22 05:18  ..
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  8 04:18 '}'
-rw-rw-r-- 1 reyhandhika reyhandhika  17K Mar 10 10:50  all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Mar 10 10:50  backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika  140 Mar 11 04:56  backup-laporan.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  382 Mar 10 10:50  backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika  10K Mar 10 10:50  backup.tar
-rw------- 1 reyhandhika reyhandhika  12K Apr  8 07:30  .bash_history
-rw-r--r-- 1 reyhandhika reyhandhika  220 Mar 31  2024  .bash_logout
-rw-rw-r-- 1 reyhandhika reyhandhika  212 Apr  8 06:44  .bash_profile
-rw-rw-r-- 1 reyhandhika reyhandhika  429 Apr  8 06:43  .bash_profile.bak-error
-rw-r--r-- 1 reyhandhika reyhandhika 4.2K Apr  8 07:44  .bashrc
-rw-r--r-- 1 reyhandhika reyhandhika 3.7K Apr  8 06:16  .bashrc.bak-praktikum
drwx------ 2 reyhandhika reyhandhika 4.0K Feb 22 05:21  .cache
drwx------ 4 reyhandhika reyhandhika 4.0K Apr  4 02:53  .config
-rw-rw-r-- 1 reyhandhika reyhandhika   48 Mar 10 10:40  error.log
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Feb 25 03:49  file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  792 Mar 11 05:00  hasil.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  734 Mar 11 04:56  laporan.txt
-rw-rw-r-- 1 reyhandhika reyhandhika 1.5K Mar 10 10:40  large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Mar  4 04:05  large-logs.txt5
-rw------- 1 reyhandhika reyhandhika   20 Mar  3 06:44  .lesshst
drwxrwxr-x 3 reyhandhika reyhandhika 4.0K Mar 10 14:46  play
drwxrwxr-x 5 reyhandhika reyhandhika 4.0K Apr  8 04:37  praktikum-os
-rw-r--r-- 1 reyhandhika reyhandhika  807 Mar 31  2024  .profile
-rw-rw-r-- 1 reyhandhika reyhandhika  835 Mar 11 04:59  proses.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  835 Mar 11 04:31  proses.txt~
-rw-rw-r-- 1 reyhandhika reyhandhika  254 Mar 10 10:41  sorted-users.txt
drwx------ 2 reyhandhika reyhandhika 4.0K Feb 22 05:18  .ssh
-rw-r--r-- 1 reyhandhika reyhandhika    0 Feb 22 05:22  .sudo_as_admin_successful
-rw-rw-r-- 1 reyhandhika reyhandhika 5.8K Mar 10 10:44  system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$ hist10
  527  EOF
  528  bash -l
  529  bash -l
  530  cat <<'EOF' >> ~/.bashrc
# --- Praktikum Alias ---\

  531  cat <<'EOF' >> ~/.bashrc
  532  source ~/.bashrc
  533  ll
  534  hist10
reyhandhika@reyhandhika:~$ cdbashlab
reyhandhika@reyhandhika:~/praktikum-os/week04-bash$ pwd
/home/reyhandhika/praktikum-os/week04-bash
reyhandhika@reyhandhika:~/praktikum-os/week04-bash$ type ll
ll is aliased to `ls -lah --color=auto'
```
## Praktikum 6.8 — Membuat Fungsi Backup Konfigurasi
Tujuan: membuat fungsi shell yang dapat dipakai berulang untuk backup file
konfigurasi.

```bash
1. Siapkan file konfigurasi contoh:
echo "PORT=8080" > ~/praktikum-os/week07-bash/sample-app.conf
cat ~/praktikum-os/week07-bash/sample-app.conf
```
Output:
```bash
reyhandhika@reyhandhika:~$ echo "PORT=8080" > ~/praktikum-os/week07-bash/sample-app.conf
reyhandhika@reyhandhika:~$ cat ~/praktikum-os/week07-bash/sample-app.conf
PORT=8080
```
2. Tambahkan fungsi ke .bashrc:
```bash
cat <<'EOF' >> ~/.bashrc
# --- Praktikum Fungsi Shell ---
backup_conf() {
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>"
        return 1
    fi

    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"

    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src"
        return 2
    fi

    mkdir -p "$dst"
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"
    echo "Backup selesai di $dst"
}
# --- End Praktikum Fungsi Shell ---
EOF
```
Output:
```bash
reyhandhika@reyhandhika:~$ cat <<'EOF' >> ~/.bashrc
> # --- Praktikum Fungsi Shell ---
> backup_conf() {
> if [ $# -ne 1 ]; then
> echo "Usage: backup_conf <file>"
> return 1
> fi
> local src="$1"
> local dst="$HOME/praktikum-os/week07-bash/backup"
> if [ ! -f "$src" ]; then
> echo "File tidak ditemukan: $src"
> return 2
> fi
> mkdir -p "$dst"
> cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"
> echo "Backup selesai di $dst"
> }
> # --- End Praktikum Fungsi Shell ---
> EOF
reyhandhika@reyhandhika:~$ source ~/.bashrc
reyhandhika@reyhandhika:~$
```
3. Uji fungsi:
```bash
backup_conf ~/praktikum-os/week07-bash/sample-app.conf
ls -lah ~/praktikum-os/week07-bash/backup
type backup_conf
```
Output:
```bash
reyhandhika@reyhandhika:~$ backup_conf ~/praktikum-os/week07-bash/sample-app.conf
Backup selesai di /home/reyhandhika/praktikum-os/week07-bash/backup
reyhandhika@reyhandhika:~$ ls -lah ~/praktikum-os/week07-bash/backup
total 12K
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  8 08:01 .
drwxrwxr-x 7 reyhandhika reyhandhika 4.0K Apr  8 06:42 ..
-rw-rw-r-- 1 reyhandhika reyhandhika   10 Apr  8 08:01 sample-app.conf.2026-04-08-080142.bak
reyhandhika@reyhandhika:~$ type backup_conf
backup_conf is a function
backup_conf ()
{
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>";
        return 1;
    fi;
    local src="$1";
    local dst="$HOME/praktikum-os/week07-bash/backup";
    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src";
        return 2;
    fi;
    mkdir -p "$dst";
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak";
    echo "Backup selesai di $dst"
}
```
3. Uji fungsi:
```bash
backup_conf ~/praktikum-os/week07-bash/sample-app.conf
ls -lah ~/praktikum-os/week07-bash/backup
type backup_conf
```
Output:
```bash
reyhandhika@reyhandhika:~$ backup_conf ~/praktikum-os/week07-bash/sample-app.conf
Backup selesai di /home/reyhandhika/praktikum-os/week07-bash/backup
reyhandhika@reyhandhika:~$ ls -lah ~/praktikum-os/week07-bash/backup
total 16K
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  8 08:06 .
drwxrwxr-x 7 reyhandhika reyhandhika 4.0K Apr  8 06:42 ..
-rw-rw-r-- 1 reyhandhika reyhandhika   10 Apr  8 08:01 sample-app.conf.2026-04-08-080142.bak
-rw-rw-r-- 1 reyhandhika reyhandhika   10 Apr  8 08:06 sample-app.conf.2026-04-08-080618.bak
reyhandhika@reyhandhika:~$ type backup_conf
backup_conf is a function
backup_conf ()
{
    if [ $# -ne 1 ]; then
        echo "Usage: backup_conf <file>";
        return 1;
    fi;
    local src="$1";
    local dst="$HOME/praktikum-os/week07-bash/backup";
    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src";
        return 2;
    fi;
    mkdir -p "$dst";
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak";
    echo "Backup selesai di $dst"
}
```
## Praktikum 6.9 — Menggunakan Completion Dasar dan Melihat History
Tujuan: menggunakan fitur Tab dan history untuk mempercepat kerja
1. Pastikan file contoh tersedia:
```bash
cd ~/praktikum-os/week07-bash/sampel
touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
ls
```
Output:
```bash
reyhandhika@reyhandhika:~$ cd ~/praktikum-os/week07-bash/sampel
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ ls
backup-01.tar  catatan-b.txt        laporan-mingguan.log
backup-02.tar  laporan-bulanan.log
catatan-a.txt  laporan-harian.log
```
2. Uji completion file:
```bash
a) Ketik cat lap lalu tekan Tab dua kali.
b) Amati daftar file yang memiliki prefix lap.
c) Ketik lebih spesifik, misalnya cat laporan-h lalu tekan Tab.
```
Jadi pada Percobaan ini menguji fitur auto-completion pada shell Linux menggunakan tombol Tab. Saat mengetik:
```bash
cat lap
```
kemudian menekan Tab dua kali, sistem menampilkan daftar file yang memiliki awalan “lap”. Fitur ini membantu pengguna melengkapi nama file secara otomatis. Setelah nama file dilengkapi menjadi laporan.txt dan menekan Enter, perintah cat menampilkan isi file tersebut. Hal ini menunjukkan bahwa auto-completion mempermudah penulisan perintah dan mengurangi kesalahan input.
Output:
```bash
reyhandhika@reyhandhika:~$ cat laporan.txt
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.5G  5.2G  52% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  198M  1.6G  11% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       394Mi       360Mi       760Ki       1.4Gi       1.5Gi
Swap:          2.0Gi       524Ki       2.0Gi
 04:56:34 up 2 days, 15:21,  4 users,  load average: 0.05, 0.03, 0.00
reyhandhika@reyhandhika:~$
```
3. Jalankan beberapa perintah sederhana:
```bash
pwd
ls - lah
date
whoami
history | tail -n 10
```
Output:
```bash
reyhandhika@reyhandhika:~$ pwd
/home/reyhandhika
reyhandhika@reyhandhika:~$ ls -lah
total 152K
drwxr-x--- 8 reyhandhika reyhandhika 4.0K Apr  8 06:43  .
drwxr-xr-x 3 root        root        4.0K Feb 22 05:18  ..
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  8 04:18 '}'
-rw-rw-r-- 1 reyhandhika reyhandhika  17K Mar 10 10:50  all-config-files.txt
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Mar 10 10:50  backup-error.log
-rw-rw-r-- 1 reyhandhika reyhandhika  140 Mar 11 04:56  backup-laporan.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  382 Mar 10 10:50  backup-success.log
-rw-rw-r-- 1 reyhandhika reyhandhika  10K Mar 10 10:50  backup.tar
-rw------- 1 reyhandhika reyhandhika  12K Apr  8 07:48  .bash_history
-rw-r--r-- 1 reyhandhika reyhandhika  220 Mar 31  2024  .bash_logout
-rw-rw-r-- 1 reyhandhika reyhandhika  212 Apr  8 06:44  .bash_profile
-rw-rw-r-- 1 reyhandhika reyhandhika  429 Apr  8 06:43  .bash_profile.bak-error
-rw-r--r-- 1 reyhandhika reyhandhika 4.5K Apr  8 07:59  .bashrc
-rw-r--r-- 1 reyhandhika reyhandhika 3.7K Apr  8 06:16  .bashrc.bak-praktikum
drwx------ 2 reyhandhika reyhandhika 4.0K Feb 22 05:21  .cache
drwx------ 4 reyhandhika reyhandhika 4.0K Apr  4 02:53  .config
-rw-rw-r-- 1 reyhandhika reyhandhika   48 Mar 10 10:40  error.log
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Feb 25 03:49  file.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  792 Mar 11 05:00  hasil.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  734 Mar 11 04:56  laporan.txt
-rw-rw-r-- 1 reyhandhika reyhandhika 1.5K Mar 10 10:40  large-logs.txt
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Mar  4 04:05  large-logs.txt5
-rw------- 1 reyhandhika reyhandhika   20 Mar  3 06:44  .lesshst
drwxrwxr-x 3 reyhandhika reyhandhika 4.0K Mar 10 14:46  play
drwxrwxr-x 5 reyhandhika reyhandhika 4.0K Apr  8 04:37  praktikum-os
-rw-r--r-- 1 reyhandhika reyhandhika  807 Mar 31  2024  .profile
-rw-rw-r-- 1 reyhandhika reyhandhika  835 Mar 11 04:59  proses.txt
-rw-rw-r-- 1 reyhandhika reyhandhika  835 Mar 11 04:31  proses.txt~
-rw-rw-r-- 1 reyhandhika reyhandhika  254 Mar 10 10:41  sorted-users.txt
drwx------ 2 reyhandhika reyhandhika 4.0K Feb 22 05:18  .ssh
-rw-r--r-- 1 reyhandhika reyhandhika    0 Feb 22 05:22  .sudo_as_admin_successful
-rw-rw-r-- 1 reyhandhika reyhandhika 5.8K Mar 10 10:44  system-monitor-20260310-104348.log
reyhandhika@reyhandhika:~$ date
Thu Apr  9 12:39:59 PM UTC 2026
reyhandhika@reyhandhika:~$ whoami
reyhandhika
reyhandhika@reyhandhika:~$ history | tail -n 10
  538  type ll
  539  exit
  540  cat lap
  541  clear
  542  cat laporan.txt
  543  pwd
  544  ls -lah
  545  date
  546  whoami
  547  history | tail -n 10
reyhandhika@reyhandhika:~$
```
## Praktikum 6.10 — Menelusuri Perintah Diagnostik dengan History
Tujuan: menggunakan history untuk mengulang langkah diagnosis sistem secara cepat

1. Jalankan beberapa perintah diagnostik:
```bash
df -h
free -h
uptime
ps aux | head
```
Output:
```bash
reyhandhika@reyhandhika:~$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.6G  5.1G  53% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  198M  1.6G  11% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000
reyhandhika@reyhandhika:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       338Mi       1.3Gi       1.1Mi       404Mi       1.6Gi
Swap:          2.0Gi          0B       2.0Gi
reyhandhika@reyhandhika:~$ uptime
 12:45:16 up 1 day,  2:13,  2 sers,  load average: 0.00, 0.00, 0.00
reyhandhika@reyhandhika:~$ ps ax | head
USER         PID %CPU %MEM    VS   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.6  22240 13344 ?        Ss   Apr08   0:17 /sbin/init
root           2  0.0  0.0      0     0 ?        S    Apr08   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    Apr08   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   Apr08   0:00 [kworker/R-rcu_g]
root           5  0.0  0.0      0     0 ?        I<   Apr08   0:00 [kworker/R-rcu_p]
root           6  0.0  0.0      0     0 ?        I<   Apr08   0:00 [kworker/R-slub_]
root           7  0.0  0.0      0     0 ?        I<   Apr08   0:00 [kworker/R-netns]
root          12  0.0  0.0      0     0 ?        I<   Apr08   0:00 [kworker/R-mm_pe]
root          13  0.0  0.0      0     0 ?        I    Apr08   0:00 [rcu_tasks_kthread]
```
2. Cari ulang perintah diagnostik dari history:
```bash
history | grep -E 'df -h|free -h|uptime |ps aux '
```
Output:
```bash
reyhandhika@reyhandhika:~$ history | grep -E 'df -h|free -h|uptime|ps aux'
   73  while [ $COUNTER -le $ITERATIONS ]; do     TIMESTAMP=$(date +"%Y-%m-%d %H:%M:%S");      echo "[$TIMESTAMP] Iterasi ke-$COUNTER" | tee -a "$LOGFILE";     echo "-----------------------------------" | tee -a "$LOGFILE";      echo "CPU Usage:" | tee -a "$LOGFILE";     top -bn1 | grep "Cpu(s)" | tee -a "$LOGFILE";      echo "Memory Usage:" | tee -a "$LOGFILE";     free -h | tee -a "$LOGFILE";      echo "Load Average:" | tee -a "$LOGFILE";     uptime | tee -a "$LOGFILE";      echo "" | tee -a "$LOGFILE";      COUNTER=$((COUNTER + 1));      if [ $COUNTER -le $ITERATIONS ]; then         sleep 5;     fi; done
  149  cat uptime
  231  ps aux | grep sleep | grep -v grep
  234  ps aux | grep sleep | grep -v grep
  235  df -h | tee laporan.txt
  236  free -h | tee -a laporan.txt
  237  uptime | tee -a laporan.txt backup-laporan.txt
  238  ps aux | grep -v grep | head -10
  239  ps aux | grep -v grep | head -10 | tee proses.txt~
  241  ps aux | grep sshd > hasil.txt
  242  ps aux | grep sshd >> hasil.txt
  243  ps aux
  244  ps aux -L
  249  ps aux
  253  ps aux | grep sleep
  268  ps aux | grep sleep
  270  ps aux | grep sleep
  273  ps aux | grep sleep
  278  ps aux | grep sleep
  292  ps aux | grep -v grep | grep sleep
  295  ps aux | grep -v grep | grep sleep
  299  ps aux | grep -v grep | grep sleep
  301  ps aux | grep -v grep | grep sleep
  306  ps aux | grep sleep
  308  ps aux | grep sleep
  310  ps aux | grep -v grep | grep sleep
  339  ps aux -- sort = -% cpu | head -10
  340  ps aux -- sort = -% mem | head -10
  341  ps aux --sort=-%cpu | head -10
  342  ps aux --sort=-%mem | head -10
  350  ps aux -sort=%mem
  351  ps aux --sort=%mem
  354  ps aux --forest
  357  ps aux --forest
  471  echo "Uptime : $(uptime -p)"
  473  df -h /
  480  echo "Uptime : $(uptime -p)"
  482  df -h /
  548  df -h
  549  free -h
  550  uptime
  551  ps aux | head
  552  history | grep -E 'df -h|free -h|uptime|ps aux'
```
3. Jalankan ulang salah satu perintah berdasarkan nomor history:
```bash
!<NOMOR_HISTORY_ANDA>
```
Output:
```bash
reyhandhika@reyhandhika:~$ !548
df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.1M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.6G  5.1G  53% /
tmpfs                              985M     0  985M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          2.0G  198M  1.6G  11% /boot
tmpfs                              197M   12K  197M   1% /run/user/1000
```
4. Simpan potongan history ke file dokumentasi:
```bash
history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
cat ~/praktikum-os/week07-bash/diag-history.txt
```
Output:
```bash
reyhandhika@reyhandhika:~$ history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
reyhandhika@reyhandhika:~$ cat ~/praktikum-os/week07-bash/diag-history.txt
  539  exit
  540  cat lap
  541  clear
  542  cat laporan.txt
  543  pwd
  544  ls -lah
  545  date
  546  whoami
  547  history | tail -n 10
  548  df -h
  549  free -h
  550  uptime
  551  ps aux | head
  552  history | grep -E 'df -h|free -h|uptime|ps aux'
  553  df -h
  554  4. Simpan potongan history ke file dokumentasi:
  555  history | tail -n 20 > ~/ praktikum - os / week07 - bash / diag
  556  - history . txt
  557  cat ~/ praktikum - os / week07 - bash / diag - history . txt
  558  history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
```
## Praktikum 6.11 — Mencoba Wildcard Dasar
Tujuan: memahami pola wildcard dan ekspansi nama file.

1. Masuk ke direktori sampel:
```bash
cd ~/praktikum-os/week07-bash/sampel
ls
```
Output:
```bash
reyhandhika@reyhandhika:~$ cd ~/praktikum-os/week07-bash/sampel
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ ls
backup-01.tar  catatan-b.txt        laporan-mingguan.log
backup-02.tar  laporan-bulanan.log
catatan-a.txt  laporan-harian.log
```
2. Coba beberapa pola wildcard:
```bash
ls *.log
ls catatan-?.txt
ls backup-0[12].tar
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ ls *.log
laporan-bulanan.log  laporan-harian.log  laporan-mingguan.log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ ls catatan-?.txt
catatan-a.txt  catatan-b.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ ls backup-0[12].tar
backup-01.tar  backup-02.tar
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$
```
3. Coba beberapa ekspansi lain:
```bash
echo log-{pagi,siang,malam}.txt
echo ~
echo ~/praktikum-os/week04-bash
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ echo log-{pagi,siang,malam}.txt
log-pagi.txt log-siang.txt log-malam.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ echo ~
/home/reyhandhika
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ echo ~/praktikum-os/week04-bash
/home/reyhandhika/praktikum-os/week04-bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$
```
## Praktikum 6.12 — Mengarsipkan Banyak Log Sekaligus
Tujuan: menggunakan wildcard secara aman untuk pekerjaan rutin administrator.

1. Siapkan file log tambahan:
```bash
cd ~/praktikum-os/week07-bash/logs
touch access-01.log access-02.log access-03.log
ls
```
Output: 
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/sampel$ cd ~/praktikum-os/week07-bash/logs
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ touch access-01.log access-02.log access-03.log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ ls
access-01.log  access-03.log  app-02.log
access-02.log  app-01.log     app-03.log
```
2. Preview file yang akan diproses:
```bash
echo *.log
echo access-0?.log
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ echo *.log
access-01.log access-02.log access-03.log app-01.log app-02.log app-03.log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ echo access-0?.log
access-01.log access-02.log access-03.log
```

3. Pindahkan semua file log ke folder arsip:
```bash
mkdir -p arsip-log
mv *.log arsip-log/
ls arsip-log
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ mkdir -p arsip-log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ mv *.log arsip-log/
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ ls arsip-log
access-01.log  access-03.log  app-02.log
access-02.log  app-01.log     app-03.log
```
4. Kompres folder arsip:
```bash
tar -czf arsip-log-$(date +%F).tar.gz arsip-log
ls -lah
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ tar -czf arsip-log-$(date +%F).tar.gz arsip-log
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ ls -lah
total 16K
drwxrwxr-x 3 reyhandhika reyhandhika 4.0K Apr  9 13:56 .
drwxrwxr-x 7 reyhandhika reyhandhika 4.0K Apr  9 13:01 ..
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  9 13:49 arsip-log
-rw-rw-r-- 1 reyhandhika reyhandhika  227 Apr  9 13:56 arsip-log-2026-04-09.tar.gz
```
## Praktikum 6.13 — Membedakan Single Quote, Double Quote, dan Escape
Tujuan: memahami efek tanda kutip terhadap ekspansi Bash.

1. Uji single quote dan double quote:
```bash
echo '$USER bekerja di $HOME'
echo "$USER bekerja di $HOME"
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ echo '$USER bekerja di $HOME'
$USER bekerja di $HOME
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ echo "$USER bekerja di $HOME"
reyhandhika bekerja di /home/reyhandhika
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$
```
2. Uji escape karakter spasi:
```bash
cd ~/praktikum-os/week07-bash/ruang-nama
ls laporan\ server\ april.txt
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/logs$ cd ~/praktikum-os/week07-bash/ruang-nama
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ ls laporan\ server\ april.txt
'laporan server april.txt'
```
3. Uji akses file yang sama dengan double quote:
```bash
cat "laporan server april.txt"
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cat "laporan server april.txt"
```
## Praktikum 6.14 — Menangani File dengan Nama Sulit Secara Aman
Tujuan: memproses file yang mengandung spasi dan karakter khusus tanpa error.

1. Pastikan file target tersedia:
```bash
cd ~/praktikum-os/week07-bash/ruang-nama
ls -lah
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ ls -lah
total 8.0K
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  8 04:33  .
drwxrwxr-x 7 reyhandhika reyhandhika 4.0K Apr  9 13:01  ..
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Apr  8 04:33 'backup [mingguan] server.conf'
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Apr  8 04:33 'laporan server april.txt'
```
2. Salin file dengan nama kompleks ke folder backup:
```bash
cp -- "backup [mingguan] server.conf" \
"$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server.conf"
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cp -- "backup [mingguan] server.conf" \
> "$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server.conf"
```
3. Gunakan variabel untuk memproses path dengan aman:
```bash
file_asli="$HOME/praktikum-os/week07-bash/ruang-nama/backup [mingguan] server.conf"
file_salinan="$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server-v2.conf"
cp -- "$file_asli" "$file_salinan"
ls -lah "$HOME/praktikum-os/week07-bash/backup"
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ file_asli="$HOME/praktikum-os/week07-bash/ruang-nama/backup [mingguan] server.conf"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ file_salinan="$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server-v2.conf"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cp -- "$file_asli" "$file_salinan"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ ls -lah "$HOME/praktikum-os/week07-bash/backup"
total 16K
drwxrwxr-x 2 reyhandhika reyhandhika 4.0K Apr  9 14:25 .
drwxrwxr-x 7 reyhandhika reyhandhika 4.0K Apr  9 13:01 ..
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Apr  9 14:22 backup-mingguan-server.conf
-rw-rw-r-- 1 reyhandhika reyhandhika    0 Apr  9 14:25 backup-mingguan-server-v2.conf
-rw-rw-r-- 1 reyhandhika reyhandhika   10 Apr  8 08:01 sample-app.conf.2026-04-08-080142.bak
-rw-rw-r-- 1 reyhandhika reyhandhika   10 Apr  8 08:06 sample-app.conf.2026-04-08-080618.bak
```
4. Tampilkan daftar file hasil backup
```bash
for file in "$HOME"/praktikum-os/week07-bash/backup/*;
do
printf 'Hasil backup: %s\n' "$file"
done
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ for file in "$HOME"/praktikum-os/week07-bash/backup/*;
> do
> printf 'Hasil backup: %s\n' "$file"
> done
Hasil backup: /home/reyhandhika/praktikum-os/week07-bash/backup/backup-mingguan-server.conf
Hasil backup: /home/reyhandhika/praktikum-os/week07-bash/backup/backup-mingguan-server-v2.conf
Hasil backup: /home/reyhandhika/praktikum-os/week07-bash/backup/sample-app.conf.2026-04-08-080142.bak
Hasil backup: /home/reyhandhika/praktikum-os/week07-bash/backup/sample-app.conf.2026-04-08-080618.bak
```

## Tugas Praktikum 1 — Toolkit Bash Administrator Pribadi
Tujuan: Membuat toolkit Bash pribadi yang berisi konfigurasi PATH, alias, fungsi shell, dan script sederhana yang dapat digunakan untuk membantu pekerjaan administrasi sistem.

Langkah 1 — Menambahkan PATH, Alias, dan Fungsi
```bash
cat <<'EOF' >> ~/.bashrc

# --- Toolkit Bash Pribadi ---

export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"

alias cekdisk='df -h'
alias cekmem='free -h'

backup_file() {
if [ $# -ne 1 ]; then
echo "Usage: backup_file <file>"
return 1
fi

cp "$1" "$1.bak"
echo "Backup selesai: $1.bak"
}

# --- End Toolkit Bash ---

EOF
kemudian jalankan
source ~/.bashrc
echo "$PATH"
```
Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cat <<'EOF' >> ~/.bashrc
> # --- Toolkit Bash Pribadi ---
> export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
> alias cekdisk='df -h'
> alias cekmem='free -h'
> backup_file() {
> if [ $# -ne 1 ]; then
> echo "Usage: backup_file <file>"
> return 1
> fi
> cp "$1" "$1.bak"
> echo "Backup selesai: $1.bak"
> }
> # --- End Toolkit Bash ---
> EOF
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ source ~/.bashrc
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ echo "$PATH"
/home/reyhandhika/praktikum-os/week07-bash/bin:/home/reyhandhika/praktikum-os/week07-bash/bin:/home/reyhandhika/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ type cekdisk
cekdisk is aliased to `df -h'
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ type cekmem
cekmem is aliased to `free -h'
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ type backup_file
backup_file is a function
backup_file ()
{
    if [ $# -ne 1 ]; then
        echo "Usage: backup_file <file>";
        return 1;
    fi;
    cp "$1" "$1.bak";
    echo "Backup selesai: $1.bak"
}
```
Pada praktikum ini dilakukan penambahan konfigurasi pada file .bashrc dengan menambahkan direktori bin ke dalam variabel PATH agar script dapat dijalankan dari direktori mana saja. Selain itu, dibuat dua alias yaitu cekdisk untuk melihat penggunaan disk dan cekmem untuk melihat penggunaan memori, serta fungsi backup_file() untuk membuat salinan file dengan ekstensi .bak. Selanjutnya dibuat direktori bin sebagai tempat penyimpanan script pribadi, kemudian dibuat script info-sistem yang berisi informasi dasar sistem seperti tanggal, pengguna, hostname, uptime, dan penggunaan disk. Perintah chmod +x digunakan untuk memberikan izin eksekusi pada script. Script kemudian diuji dari direktori yang berbeda untuk memastikan bahwa konfigurasi PATH telah berhasil. Terakhir, hasil konfigurasi disimpan ke dalam file toolkit-bash-report.txt sebagai bukti bahwa alias, fungsi, dan script telah berjalan dengan baik.

## Tugas Praktikum 2 — Audit File Konfigurasi dan Logging Aman
Tujuan: Melakukan pencarian file konfigurasi pada direktori sistem serta memisahkan output normal dan pesan error ke dalam file yang berbeda.
1. Membuat nama file laporan
```bash
laporan="audit-konfigurasi-$(date +%F).txt"
errorlog="audit-error.log"
```
Pada langkah ini dibuat variabel laporan dan errorlog untuk menyimpan nama file hasil audit dan file log error secara otomatis berdasarkan tanggal.

Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ laporan="audit-konfigurasi-$(date +%F).txt"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ errorlog="audit-error.log"
```
2. Mencari file *.conf
```bash
find /etc -name "*.conf" > "$laporan" 2> "$errorlog"
```
find /etc -name "*.conf" > "$laporan" 2> "$errorlog"

Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ find /etc -name "*.conf" > "$laporan" 2> "$errorlog"
```
3. Menghitung jumlah file
```bash
jumlah=$(wc -l < "$laporan")

echo "Jumlah file konfigurasi: $jumlah" >> "$laporan"
```
Perintah wc -l digunakan untuk menghitung jumlah baris pada file laporan yang menunjukkan jumlah file konfigurasi yang ditemukan.

Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ jumlah=$(wc -l < "$laporan")
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ echo "Jumlah file konfigurasi: $jumlah" >> "$laporan"
```
4. Menampilkan dan menyimpan laporan
```bash
cat "$laporan" | tee hasil-audit.txt
```
Perintah tee digunakan untuk menampilkan isi laporan ke terminal sekaligus menyimpannya ke file lain.

Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cat "$laporan" | tee hasil-audit.txt
/etc/sudo_logsrvd.conf
/etc/ld.so.conf
/etc/depmod.d/ubuntu.conf
/etc/mke2fs.conf
/etc/initramfs-tools/update-initramfs.conf
/etc/initramfs-tools/initramfs.conf
/etc/sensors3.conf
/etc/resolv.conf
/etc/apt/apt.conf.d/20snapd.conf
/etc/apt/apt.conf.d/20apt-esm-hook.conf
/etc/apparmor/parser.conf
/etc/sos/sos.conf
/etc/security/faillock.conf
/etc/security/pam_env.conf
/etc/security/access.conf
/etc/security/time.conf
/etc/security/capability.conf
/etc/security/pwhistory.conf
/etc/security/sepermit.conf
/etc/security/namespace.conf
/etc/security/group.conf
/etc/security/limits.conf
/etc/debconf.conf
/etc/tmpfiles.d/screen-cleanup.conf
/etc/dhcpcd.conf
/etc/udisks2/udisks2.conf
/etc/iscsi/iscsid.conf
/etc/libaudit.conf
/etc/fuse.conf
/etc/ld.so.conf.d/libc.conf
/etc/ld.so.conf.d/x86_64-linux-gnu.conf
/etc/locale.conf
/etc/ldap/ldap.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-korea1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-gb1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-cns1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-japan1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-japan2.conf
/etc/ghostscript/fontmap.d/10fonts-urw-base35.conf
/etc/vconsole.conf
/etc/udev/udev.conf
/etc/udev/iocost.conf
/etc/pam.conf
/etc/selinux/semanage.conf
/etc/PackageKit/Vendor.conf
/etc/PackageKit/PackageKit.conf
/etc/host.conf
/etc/nsswitch.conf
/etc/overlayroot.conf
/etc/ubuntu-advantage/uaclient.conf
/etc/deluser.conf
/etc/modprobe.d/blacklist-rare-network.conf
/etc/modprobe.d/blacklist-firewire.conf
/etc/modprobe.d/intel-microcode-blacklist.conf
/etc/modprobe.d/iwlwifi.conf
/etc/modprobe.d/amd64-microcode-blacklist.conf
/etc/modprobe.d/blacklist.conf
/etc/modprobe.d/blacklist-ath_pci.conf
/etc/modprobe.d/mdadm.conf
/etc/modprobe.d/blacklist-framebuffer.conf
/etc/sysctl.conf
/etc/sysctl.d/10-zeropage.conf
/etc/sysctl.d/10-bufferbloat.conf
/etc/sysctl.d/10-console-messages.conf
/etc/sysctl.d/99-sysctl.conf
/etc/sysctl.d/10-kernel-hardening.conf
/etc/sysctl.d/10-ptrace.conf
/etc/sysctl.d/10-network-security.conf
/etc/sysctl.d/10-ipv6-privacy.conf
/etc/sysctl.d/10-magic-sysrq.conf
/etc/sysctl.d/10-map-count.conf
/etc/modules-load.d/modules.conf
/etc/ucf.conf
/etc/mdadm/mdadm.conf
/etc/ca-certificates.conf
/etc/nftables.conf
/etc/needrestart/needrestart.conf
/etc/needrestart/notify.conf
/etc/UPower/UPower.conf
/etc/lvm/lvm.conf
/etc/lvm/lvmlocal.conf
/etc/vmware-tools/vgauth.conf
/etc/vmware-tools/tools.conf
/etc/sudo.conf
/etc/hdparm.conf
/etc/logrotate.conf
/etc/gai.conf
/etc/adduser.conf
/etc/apport/crashdb.conf
/etc/systemd/networkd.conf
/etc/systemd/timesyncd.conf
/etc/systemd/journald.conf
/etc/systemd/user.conf
/etc/systemd/sleep.conf
/etc/systemd/logind.conf
/etc/systemd/system.conf
/etc/systemd/resolved.conf
/etc/systemd/pstore.conf
/etc/fonts/conf.d/45-latin.conf
/etc/fonts/conf.d/90-synthetic.conf
/etc/fonts/conf.d/65-nonlatin.conf
/etc/fonts/conf.d/20-unhint-small-dejavu-sans-mono.conf
/etc/fonts/conf.d/58-dejavu-lgc-sans.conf
/etc/fonts/conf.d/60-latin.conf
/etc/fonts/conf.d/20-unhint-small-dejavu-lgc-serif.conf
/etc/fonts/conf.d/61-urw-z003.conf
/etc/fonts/conf.d/10-hinting-slight.conf
/etc/fonts/conf.d/61-urw-p052.conf
/etc/fonts/conf.d/51-local.conf
/etc/fonts/conf.d/49-sansserif.conf
/etc/fonts/conf.d/65-droid-sans-fallback.conf
/etc/fonts/conf.d/20-unhint-small-dejavu-lgc-sans.conf
/etc/fonts/conf.d/61-urw-fallback-generics.conf
/etc/fonts/conf.d/57-dejavu-sans.conf
/etc/fonts/conf.d/61-urw-nimbus-mono-ps.conf
/etc/fonts/conf.d/57-dejavu-sans-mono.conf
/etc/fonts/conf.d/61-urw-fallback-backwards.conf
/etc/fonts/conf.d/50-user.conf
/etc/fonts/conf.d/58-dejavu-lgc-serif.conf
/etc/fonts/conf.d/10-yes-antialias.conf
/etc/fonts/conf.d/30-metric-aliases.conf
/etc/fonts/conf.d/58-dejavu-lgc-sans-mono.conf
/etc/fonts/conf.d/20-unhint-small-dejavu-serif.conf
/etc/fonts/conf.d/61-urw-gothic.conf
/etc/fonts/conf.d/61-urw-c059.conf
/etc/fonts/conf.d/20-unhint-small-vera.conf
/etc/fonts/conf.d/45-generic.conf
/etc/fonts/conf.d/61-urw-d050000l.conf
/etc/fonts/conf.d/11-lcdfilter-default.conf
/etc/fonts/conf.d/70-no-bitmaps-except-emoji.conf
/etc/fonts/conf.d/20-unhint-small-dejavu-sans.conf
/etc/fonts/conf.d/48-spacing.conf
/etc/fonts/conf.d/60-generic.conf
/etc/fonts/conf.d/10-scale-bitmap-fonts.conf
/etc/fonts/conf.d/80-delicious.conf
/etc/fonts/conf.d/65-fonts-persian.conf
/etc/fonts/conf.d/57-dejavu-serif.conf
/etc/fonts/conf.d/69-unifont.conf
/etc/fonts/conf.d/10-sub-pixel-rgb.conf
/etc/fonts/conf.d/61-urw-nimbus-sans.conf
/etc/fonts/conf.d/40-nonlatin.conf
/etc/fonts/conf.d/20-unhint-small-dejavu-lgc-sans-mono.conf
/etc/fonts/conf.d/61-urw-standard-symbols-ps.conf
/etc/fonts/conf.d/61-urw-bookman.conf
/etc/fonts/conf.d/61-urw-nimbus-roman.conf
/etc/fonts/fonts.conf
/etc/fonts/conf.avail/30-droid-noto-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-sans-mono.conf
/etc/fonts/conf.avail/58-dejavu-lgc-sans.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-serif.conf
/etc/fonts/conf.avail/65-droid-sans-fallback.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-sans.conf
/etc/fonts/conf.avail/57-dejavu-sans.conf
/etc/fonts/conf.avail/57-dejavu-sans-mono.conf
/etc/fonts/conf.avail/58-dejavu-lgc-serif.conf
/etc/fonts/conf.avail/58-dejavu-lgc-sans-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-serif.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-sans.conf
/etc/fonts/conf.avail/57-dejavu-serif.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-sans-mono.conf
/etc/xattr.conf
/etc/multipath.conf
/etc/rsyslog.d/21-cloudinit.conf
/etc/rsyslog.d/20-ufw.conf
/etc/rsyslog.d/50-default.conf
/etc/usb_modeswitch.conf
/etc/rsyslog.conf
/etc/fwupd/fwupd.conf
/etc/fwupd/remotes.d/vendor-directory.conf
/etc/fwupd/remotes.d/lvfs.conf
/etc/fwupd/remotes.d/lvfs-testing.conf
/etc/dbus-1/system.d/com.ubuntu.SoftwareProperties.conf
/etc/ufw/sysctl.conf
/etc/ufw/ufw.conf
/etc/xdg/user-dirs.conf
/etc/e2scrub.conf
```
Pemisahan output normal dan error penting dalam audit sistem karena memungkinkan administrator mengetahui file yang berhasil ditemukan serta kesalahan yang terjadi tanpa mencampur kedua informasi tersebut. Hal ini memudahkan proses analisis dan troubleshoot

## Tugas Praktikum 3 — Mini Health Check Harian
Tujuan: Membuat script pemeriksaan kondisi dasar sistem secara otomatis.
1. Membuat script
```bash
cat <<'EOF' > ~/praktikum-os/week07-bash/bin/daily-healthcheck

#!/usr/bin/env bash

LOGFILE="$HOME/praktikum-os/week07-bash/healthcheck-$(date +%F).log"

{
echo "=== DAILY HEALTH CHECK ==="
date
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "Shell : $0"
echo "Uptime : $(uptime -p)"

echo "Memory Usage:"
free -h

echo "Disk Usage:"
df -h /

echo "History Terakhir:"
history | tail -n 10

} | tee "$LOGFILE"

EOF

kemudian 
chmod +x ~/praktikum-os/week07-bash/bin/daily-healthcheck
```
Script daily-healthcheck dibuat untuk menampilkan kondisi sistem seperti uptime, memori, disk, dan history terakhir. Hasil ditampilkan ke terminal dan disimpan ke file log harian menggunakan tee.

2. Menjalankan Script
```bash
daily-healthcheck
```
Script dijalankan untuk memastikan bahwa semua informasi sistem dapat ditampilkan dengan benar dan disimpan ke dalam file log.

Output:
```
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cat <<'EOF' > ~/praktikum-os/week07-bash/bin/daily-healthcheck

#!/usr/bin/env bash

LOGFILE="$HOME/praktikum-os/week07-bash/healthcheck-$(date +%F).log"

{
echo "=== DAILY HEALTH CHECK ==="
date
echo "Hostname : $(hostname)"
echo "User : $(whoami)"
echo "Shell : $0"
echo "Uptime : $(uptime -p)"

EOF tee "$LOGFILE"10ir:"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ chmod +x ~/praktikum-os/week07-bash/bin/daily-healthcheck
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ daily-healthcheck
=== DAILY HEALTH CHECK ===
Thu Apr  9 02:59:13 PM UTC 2026
Hostname : reyhandhika
User : reyhandhika
Shell : /home/reyhandhika/praktikum-os/week07-bash/bin/daily-healthcheck
Uptime : up 1 day, 4 hours, 27 minutes
Memory Usage:
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       359Mi       1.3Gi       1.1Mi       408Mi       1.6Gi
Swap:          2.0Gi          0B       2.0Gi
Disk Usage:
Filesystem                         Size  Used Avail Use% Mounted on
/dev/mapper/ubuntu--vg-ubuntu--lv   12G  5.6G  5.1G  53% /
History Terakhir:

echo "History Terakhir:"
history | tail -n 10

} | tee "$LOGFILE"

EOF

  607  chmod +x ~/praktikum-os/week07-bash/bin/daily-healthcheck
  608  daily-healthcheck
  ```

## Tugas Praktikum 4 — Penanganan File Kompleks
Tujuan: Memproses file dengan nama kompleks serta membuat arsip backup secara aman.
1. Membuat file
```bash
touch "laporan harian april.txt"
touch "backup [mingguan] data.conf"
touch log-01.txt
touch log-02.txt
```
File dibuat dengan berbagai variasi nama, termasuk nama dengan spasi dan karakter khusus untuk menguji penggunaan quoting dan wildcard.

2. Preview wildcard
```bash
echo log-*.txt
```
Perintah echo digunakan untuk melihat file yang cocok dengan pola wildcard sebelum dilakukan operasi sebenarnya.
3. Membuat folder backup
```bash
Membuat folder backup
```
4. Menyalin file
```bash
cp "laporan harian april.txt" backup-tugas/
cp "backup [mingguan] data.conf" backup-tugas/
cp log-*.txt backup-tugas/
```
5. Membuat arsip
```bash
tar -czf backup-tugas-$(date +%F).tar.gz backup-tugas
```
6. Menyimpan riwayat
```bash
history | tail -n 30 > riwayat-arsip.txt
```
Penggunaan quoting sangat penting dalam Bash karena nama file yang mengandung spasi atau karakter khusus dapat menyebabkan kesalahan pembacaan oleh sistem. Dengan menggunakan wildcard dan quoting secara benar, proses pengelolaan file menjadi lebih aman dan efisien.

Output:
```bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash/ruang-nama$ cd ~/praktikum-os/week07-bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ pwd
/home/reyhandhika/praktikum-os/week07-bash
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch "laporan harian april.txt"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch "backup [mingguan] data.conf"
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch log-01.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ touch log-02.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls
 backup                         log-02.txt
'backup [mingguan] data.conf'   login-audit.log
 bin                            logs
 diag-history.txt               ruang-nama
 healthcheck-2026-04-09.log     sampel
'laporan harian april.txt'      sample-app.conf
 log-01.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls laporan harian april.txt
ls: cannot access 'laporan': No such file or directory
ls: cannot access 'harian': No such file or directory
ls: cannot access 'april.txt': No such file or directory
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls "laporan harian april.txt"
'laporan harian april.txt'
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ echo log-*.txt
log-01.txt log-02.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ mkdir backup-tugas
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls
 backup                         log-01.txt
'backup [mingguan] data.conf'   log-02.txt
 backup-tugas                   login-audit.log
 bin                            logs
 diag-history.txt               ruang-nama
 healthcheck-2026-04-09.log     sampel
'laporan harian april.txt'      sample-app.conf
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ cp "laporan harian april.txt" backup-tugas/
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ cp "backup [mingguan] data.conf" backup-tugas/
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ cp "backup [mingguan] data.conf" backup-tugas/
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls backup-tugas
'backup [mingguan] data.conf'  'laporan harian april.txt'
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ tar -czf backup-tugas-$(date +%F).tar.gz backup-tugas
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ ls
 backup                           log-01.txt
'backup [mingguan] data.conf'     log-02.txt
 backup-tugas                     login-audit.log
 backup-tugas-2026-04-09.tar.gz   logs
 bin                              ruang-nama
 diag-history.txt                 sampel
 healthcheck-2026-04-09.log       sample-app.conf
'laporan harian april.txt'
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ history | tail -n 30 > riwayat-arsip.txt
reyhandhika@reyhandhika:~/praktikum-os/week07-bash$ cat riwayat-arsip.txt
  609  touch "laporan harian april.txt"
  610  touch "backup [mingguan] data.conf"
  611  touch log-01.txt
  612  touch log-02.txt
  613  echo log-*.txt
  614  mkdir backup-tugas
  615  cp "laporan harian april.txt" backup-tugas/
  616  cp "backup [mingguan] data.conf" backup-tugas/
  617  cp log-*.txt backup-tugas/
  618  tar -czf backup-tugas-$(date +%F).tar.gz backup-tugas
  619  history | tail -n 30 > riwayat-arsip.txt
  620  type cekdisk
  621  cd ~/praktikum-os/week07-bash
  622  pwd
  623  touch "laporan harian april.txt"
  624  touch "backup [mingguan] data.conf"
  625  touch log-01.txt
  626  touch log-02.txt
  627  ls
  628  ls laporan harian april.txt
  629  ls "laporan harian april.txt"
  630  echo log-*.txt
  631  mkdir backup-tugas
  632  ls
  633  cp "laporan harian april.txt" backup-tugas/
  634  cp "backup [mingguan] data.conf" backup-tugas/
  635  ls backup-tugas
  636  tar -czf backup-tugas-$(date +%F).tar.gz backup-tugas
  637  ls
  638  history | tail -n 30 > riwayat-arsip.txt
```