# laporan Praktikum 1

<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## 1.10 Latihan

### 1.101 Latihan Konseptual

#### Latihan 1.1

jelaskan 5 fungsi utama sistem operasi dengan konkret dari minimal 2 OS berbeda (windows, atau Linux).

>Jawaban    :
Sistem Operasi Modern Memiliki lima fungsi utama    :   
>1.Process Management  
<b>Sistem operasi bertanggung jawab untuk:</b>  
• Process scheduling — Menentukan proses mana yang mendapat CPU time  
• Process creation dan termination — Membuat dan mengakhiri proses  
• Process synchronization — Mengkoordinasikan multiple processes  
• Inter-process communication (IPC) — Memfasilitasi komunikasi antar
proses  
<b>Contoh implementasi: </b> 
• Windows: Task Manager menampilkan proses yang berjalan dan penggunaan
sumber daya   
• Linux: Perintah ps, top, dan htop untuk memantau proses  
• macOS: Activity Monitor untuk mengelola proses
>
>2.Memory Management  
<b>Fungsi memory management meliputi:</b>  
• Memory allocation — Memberikan memori ke proses yang membutuhkan  
• Virtual memory — Menggunakan disk sebagai extension dari RAM  
• Memory protection — Mencegah satu proses mengakses memori proses lain  
• Paging dan swapping — Teknik untuk optimasi penggunaan memori  
>
>3.File Management  
<b>Sistem operasi menyediakan:</b>  
• Organisasi file system — Struktur hirarkis (direktori, subdirektori)
• Operasi file — Membuat, membaca, menulis, menghapus file  
• Kontrol akses — Izin (permissions) untuk keamanan  
• Mounting file system — Mengintegrasikan perangkat penyimpanan ke sistem  
<b>Contoh file systems:</b>  
• Windows: NTFS (New Technology File System)  
• macOS: APFS (Apple File System)  
• Linux: ext4, XFS, Btrfs
>
>4.I/O Management  
<b>Manajemen Input/Output mencakup:</b>  
• Device drivers — Perangkat lunak untuk berkomunikasi dengan perangkat
keras  
• Buffering — Penyimpanan sementara untuk kelancaran operasi I/O  
• Interrupt handling — Merespon sinyal dari perangkat keras  
• Spooling — Antrean untuk perangkat seperti printer
Security dan Protection  
<b>Contoh Impelentasi:</b>
* Windows: Saat kita memasukkan flashdisk USB, Windows secara otomatis mendeteksi perangkat tersebut dan menggunakan driver yang sesuai (misalnya usbstor.sys) untuk berkomunikasi dengan perangkat keras. Proses ini terjadi di latar belakang tanpa perlu campur tangan pengguna.  
* Linux: Di Linux, ketika perangkat baru seperti printer atau scanner terhubung melalui USB, kernel menggunakan driver seperti usbcore dan usb-storage untuk mengakses perangkat. Pengguna juga bisa melihat daftar driver yang digunakan melalui perintah lsmod atau melihat perangkat di /dev.
>5. Aspek keamanan meliputi:  
• Authentication — Verifikasi identitas pengguna (password, biometrik)  
• Authorization — Kontrol akses ke sumber daya berdasarkan izin (permissions)  
• Encryption — Proteksi data (BitLocker di Windows, FileVault di macOS)  
• Auditing — Pencatatan aktivitas sistem untuk pemantauan keamanan
<b>Contoh Impelemntasi:</b>  
• Windows: Windows memiliki fitur BitLocker yang digunakan untuk mengenkripsi seluruh drive. Misalnya, jika laptop dicuri, data di dalamnya tetap aman karena tidak bisa diakses tanpa kunci pemulihan atau password.  
• Linux: Di Linux, pengguna bisa menggunakan LUKS (Linux Unified Key Setup) untuk enkripsi disk. Saat instalasi Ubuntu, pengguna bisa memilih opsi Encrypt the entire disk untuk melindungi data.
>
#### Latihan 1.2

Kapan sebaiknya menggunakan Windows vs Linux vs macOS?  
Analisis berdasarkan use case: gaming, development, server, creative work, dan enterprise.

>Jawaban :  
>1. Untuk gaming,   
Windows masih menjadi pilihan yang tidak terbantahkan karena mendukung DirectX 12, kompatibilitas dengan hampir semua game AAA, serta dukungan driver GPU terbaik dari NVIDIA dan AMD, sementara Linux hanya bisa dipertimbangkan untuk game-game ringan dengan catatan harus siap bereksperimen dengan Proton, dan macOS sama sekali tidak direkomendasikan karena katalog game sangat terbatas serta Apple Silicon tidak mendukung dual-boot Windows.
>
>2. Untuk pengembangan perangkat lunak,   
pilihan OS sangat bergantung pada jenis development yang dilakukan. Linux unggul untuk pengembangan backend, infrastruktur cloud, dan pekerjaan yang berkaitan dengan kontainer seperti Docker, karena lingkungannya mirip dengan production server dan manajemen paketnya efisien. macOS menjadi keharusan jika Anda mengembangkan aplikasi iOS atau bekerja di ekosistem Apple, selain itu sistem berbasis UNIX dengan pengalaman pengguna premium ini juga sangat cocok untuk web development dan frontend. Windows tetap menjadi pilihan utama untuk pengembangan aplikasi .NET dan teknologi Microsoft, ditambah dengan kehadiran WSL yang memungkinkan pengembangan Linux berjalan mulus di atas Windows.
>
>3. Dalam ranah server,   
Linux mendominasi dengan pangsa pasar sekitar 80% karena alasan biaya yang gratis, stabilitas tinggi yang mampu berjalan bertahun-tahun tanpa reboot, keamanan yang baik, serta kemudahan manajemen jarak jauh melalui SSH. Windows Server hanya relevan untuk organisasi yang sudah terikat dengan ekosistem Microsoft seperti Active Directory, Exchange, atau aplikasi berbasis .NET, namun konsekuensinya harus siap dengan biaya lisensi yang mahal dan kebutuhan hardware lebih besar. macOS Server praktis sudah tidak relevan karena Apple menghentikan produk ini sejak 2022.
>
>4. Untuk pekerjaan kreatif,  
Seperti desain grafis, video editing, dan produksi musik, macOS menjadi pilihan utama profesional karena keunggulan akurasi warna, aplikasi eksklusif seperti Final Cut Pro dan Logic Pro, serta performa Apple Silicon yang luar biasa untuk rendering. Windows tetap menjadi alternatif kuat terutama untuk 3D rendering dan animasi yang membutuhkan GPU high-end, serta untuk aplikasi seperti 3ds Max yang eksklusif di platform ini. Linux sangat terbatas untuk kebutuhan kreatif karena tidak mendukung Adobe Creative Cloud dan tools profesional lainnya, meskipun memiliki alternatif open source seperti GIMP dan Blender.
>
>5. Di lingkungan enterprise atau perusahaan,   
Windows menjadi pilihan paling aman untuk organisasi besar dengan ribuan karyawan non-teknis karena kemudahan manajemen terpusat melalui Active Directory dan Group Policy, serta kompatibilitas dengan aplikasi bisnis legacy. macOS cocok untuk perusahaan kreatif atau startup teknologi dimana karyawan lebih produktif dengan ekosistem Apple, serta dapat dikelola melalui solusi MDM seperti Jamf. Linux dipilih untuk workstation teknis, tim data science, dan tentu saja untuk seluruh kebutuhan server, namun jarang digunakan sebagai desktop pengguna umum karena kurva pembelajaran yang curam dan keterbatasan aplikasi perkantoran.


### 1.10.2 Latihan Praktikal

#### Latihan 1.3

Install Ubuntu Server 22.04 LTS di VirtualBox dengan langkah berikut:
1. Download Ubuntu Server ISO dari website resmi
2. Create VM baru di VirtualBox (RAM: 2GB, Disk: 25GB)
3. Install dengan automatic partitioning (guided)
4. Buat user account dengan password yang kuat
5. Reboot dan login ke sistem
6. Dokumentasikan proses instalasi dengan screenshot key step

>Jawaban    : 
>1. Step 1.
![alt text](image/Virtualbox-1.png) 
>2. Step 2.
![alt text](image/Virtualbox-2.png)
>3. Step 3.
![alt text](image/Virtualbox-3.png)
>4. Step 4.
![alt text](image/Virtualbox-4.png)
>5. Step 5.
![alt text](image/Virtualbox-5.png)
>6. Step 6.
![alt text](image/Virtualbox-6.png)
>7. Step 7.
![alt text](image/Virtualbox-7.png)
>8. Step 8.
![alt text](image/Virtualbox-8.png)
>9. Step 9.
![alt text](image/Virtualbox-9.png)
>10. Step 10.
![alt text](image/Ubuntu-1.png)
>11. Step 11.
![alt text](image/Ubuntu-2.png)
>12. Step 12.
![alt text](image/ubuntu-3.png)
>13. Step 13.
![alt text](image/ubuntu-4.png)
>14. Step 14.
![alt text](image/ubuntu-5.png)
>15. Step 15.
![alt text](image/Ubuntu-6.png)
>16. Step 16.
![alt text](image/Ubuntu-7.png)
>17. Step 17.
![alt text](image/Ubuntu-8.png)

#### Latihan 1.4

Setelah instalasi Ubuntu Server, lakukan tasks berikut:
1. Update package list: sudo apt update
2. Upgrade packages: sudo apt upgrade
3. Install neofetch: sudo apt install neofetch
4. Jalankan neofetch dan screenshot hasilnya
5. Check disk usage dengan df -h
6. Check memory dengan free -h
7. Dokumentasikan output dari setiap command

>Jawaban    :
>1. Step 1.
![alt text](image/Update-1.png)
>2. Step 2.
![alt text](image/Update_2.png)
>3. Step 3.
![alt text](image/Update-3.png)
>4. Step 4.
![alt text](image/Update-4.png)
>5. Step 5.
![alt text](image/Update-5.png)
>6. Step 6.
![alt text](image/Update-6.png)
>7. Step 7.
![alt text](image/Update-7.png)


#### Latihan 1.5

Eksplorasi sistem yang baru diinstall:
1. Tampilkan informasi OS: cat /etc/os-release
2. Tampilkan versi kernel: uname -r
3. List partisi: lsblk
4. Check network connectivity: ping -c 4 google.com
5. Install dan jalankan htop untuk melihat resource usage
6. Buat laporan singkat tentang konfigurasi sistem Anda

>Jawaban
>
><b>LAPORAN KONFIGURASI SISTEM Ubuntu Server 22.04 LTS</b>  
>Hostname:ubuntuser
><b> A. Spesifikasi Sistem
>
><b>Sistem operasi yang digunakan adalah:</b>  
>Nama OS: Ubuntu Server 22.04 LTS (Jammy Jellyfish)
>
>Kernel Linux: 5.15.x-generic
>
>Arsitektur: x86_64 (64-bit)
>
>Ubuntu Server 22.04 merupakan distribusi Linux berbasis Debian yang dirancang untuk kebutuhan server, stabil, dan mendapatkan dukungan jangka panjang (LTS) selama 5 tahun.
>
><b>B. Konfigurasi Hardware (Virtual Machine)</b>
>
>Sistem dijalankan menggunakan VirtualBox dengan konfigurasi:
>RAM: 2 GB  >CPU: 2 Core  
>Storage: 20 GB (VDI, SATA Controller)
>Tipe Disk: Dynamically Allocated
>Paravirtualization: KVM
>EFI: Nonaktif
><b>Struktur partisi standar instalasi otomatis:</b>  
>(root) → sistem utama  
>boot atau /boot/efi → bootloader
>swap → memori virtual (opsional tergantung konfigurasi)
>Konfigurasi ini cukup untuk kebutuhan server ringan seperti web server, database kecil, atau praktikum jaringan.
>  
><b>C. Konektivitas Jaringan</b>
>
>Konfigurasi jaringan menggunakan:
>Mode Adapter: NAT
>Interface: enp0s3
>IP Address: DHCP (otomatis dari VirtualBox)
>Pengujian konektivitas dilakukan menggunakan:
>ping -c 4 google.com
>Hasil menunjukkan:
>0% packet loss
>Respon normal
>Artinya:
>Koneksi internet aktif
>DNS berfungsi dengan baik
>Gateway berjalan normal
>
><b>D. LAYANAN DAN PROSES</b>  
>Jumlah proses berjalan: 125 proses
>
>Proses dengan penggunaan CPU tertinggi: kworker/1:1-events
>
>Proses dengan penggunaan memori tertinggi: sbin/multipathd -d -s
>
>Package manager: APT dengan repository Ubuntu 22.04
>
><b>E. APLIKASI TERINSTAL</b>  
>Neofetch: Untuk menampilkan informasi sistem
>
>htop: Monitor proses interaktif
>
>Lainnya: Paket dasar Ubuntu Server
>
><b>F. Kesimpulan Tentang Ubuntu Server</b>
>Ubuntu Server 22.04 LTS adalah sistem operasi server yang:
>Stabil dan ringan
>Cocok untuk virtualisasi
>Efisien dalam penggunaan resource
>Mudah dikonfigurasi melalui CLI
>Mendukung berbagai layanan server (web, database, file server, DNS, dll.)
>Dalam konfigurasi VirtualBox dengan 2GB RAM dan 2 core CPU, sistem berjalan normal tanpa kendala performa. Konektivitas jaringan stabil dan layanan inti berjalan dengan baik.
>Secara keseluruhan, Ubuntu Server sangat layak digunakan untuk:
>Praktikum jaringan
>Pembelajaran administrasi server
>Hosting aplikasi skala kecil-menengah
>Implementasi layanan berbasis Linux

### 1.10.3 Latihan Latihan Refleksi

#### Latihan 1.6
Ceritakan pengalaman Anda dengan sistem operasi:
1. Sistem operasi apa yang Anda gunakan sehari-hari? (Windows, macOS,
Linux, atau lainnya)
2. Berapa lama Anda menggunakan sistem operasi tersebut?
3. Apa yang Anda sukai dari sistem operasi tersebut?
4. Apa tantangan atau masalah yang pernah Anda hadapi?
5. Apakah Anda pernah menggunakan sistem operasi lain? Bandingkan
pengalaman Anda.
6. Setelah mempelajari bab ini, apakah ada sistem operasi lain yang ingin
Anda coba? Mengapa?
Tulis refleksi Anda dalam 300-500 kata disertai dengan dokumentasi.

>Jawaban:
>
>1. Sistem operasi yang digunakan sehari-hari
Saya menggunakan Windows 10/11 sebagai sistem operasi utama untuk aktivitas harian seperti perkuliahan, pemrograman, dan penggunaan aplikasi produktivitas.
>
>2. Lama penggunaan
Saya telah menggunakan Windows selama kurang lebih 5–7 tahun, sejak masa sekolah hingga perkuliahan.
>
>3. Hal yang disukai
Saya menyukai kemudahan penggunaan (user-friendly), kompatibilitas software yang luas, dukungan driver otomatis, serta kemudahan instalasi aplikasi tanpa konfigurasi yang kompleks.
>
>4. Tantangan atau masalah yang pernah dihadapi
Beberapa kendala yang pernah dialami antara lain pembaruan sistem otomatis yang memakan waktu, performa yang menurun jika RAM terbatas, serta risiko keamanan seperti virus apabila tidak dilindungi antivirus.
>
>5. Pengalaman menggunakan sistem operasi lain dan perbandingan
Saya pernah menggunakan Ubuntu Server 22.04 LTS di VirtualBox. Linux lebih ringan, stabil, dan jarang mengalami crash. Namun, pengoperasiannya berbasis command line sehingga membutuhkan pemahaman teknis lebih mendalam dibandingkan Windows yang lebih grafis dan mudah bagi pengguna umum.
Refleksi Pengalaman Menggunakan Sistem Operasi
Sistem operasi yang saya gunakan sehari-hari adalah Windows 10/11. Saya telah menggunakannya selama kurang lebih 5–7 tahun untuk berbagai kebutuhan, mulai dari mengerjakan tugas perkuliahan, mengakses internet, hingga belajar pemrograman. Windows menjadi sistem operasi utama karena kompatibilitasnya yang luas terhadap berbagai aplikasi dan perangkat keras.
Keunggulan utama Windows terletak pada kemudahan penggunaan serta tampilan antarmuka grafis yang intuitif. Hampir seluruh software yang dibutuhkan untuk kegiatan akademik dapat berjalan dengan baik tanpa konfigurasi tambahan. Instalasi driver perangkat keras juga relatif otomatis, sehingga memudahkan pengguna dalam mengoperasikan sistem tanpa perlu pengetahuan teknis mendalam.
Namun demikian, terdapat beberapa tantangan dalam penggunaannya. Pembaruan sistem yang berjalan otomatis terkadang mengganggu aktivitas karena memerlukan waktu restart yang cukup lama. Selain itu, sistem juga memerlukan spesifikasi perangkat keras yang cukup agar dapat berjalan optimal. Risiko keamanan seperti malware juga menjadi perhatian jika sistem tidak diperbarui atau tidak menggunakan perlindungan yang memadai.
Selain Windows, saya juga memiliki pengalaman menggunakan Ubuntu Server 22.04 LTS melalui VirtualBox. Pengalaman tersebut memberikan perspektif berbeda mengenai sistem operasi berbasis Linux. Ubuntu Server lebih ringan dan stabil, serta memberikan kontrol yang lebih besar kepada pengguna melalui command line interface. Namun, penggunaannya membutuhkan pemahaman teknis yang lebih tinggi dibandingkan Windows yang lebih berorientasi pada pengguna umum.
Melalui pembelajaran tentang sistem operasi, saya menyadari bahwa setiap sistem memiliki kelebihan dan kekurangan sesuai dengan kebutuhan pengguna. Windows cocok untuk penggunaan sehari-hari dan produktivitas umum, sedangkan Linux lebih unggul dalam stabilitas dan administrasi server. Pengalaman ini memperluas pemahaman saya mengenai konsep manajemen sistem, kernel, proses, serta manajemen sumber daya pada sistem operasi.  
<b>Dokumentasi :</b>
![alt text](image/Ubuntu-8.png)