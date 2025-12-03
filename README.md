# Jarkom-Modul-5-2025-K35

 Nama | NRP |
|---|---|
| Tiara Putri Prasetya | 5027241013 |
| Naufal Ardhana | 5027241118 |

# Topologi Jaringan
<img width="1253" height="775" alt="image" src="https://github.com/user-attachments/assets/28c9c837-624b-4985-a56a-2943a74d1faa" />


# Identifikasi Perangkat

| Perangkat | Tipe | Fungsi Utama | Keterangan |
| :--- | :--- | :--- | :--- |
| **Narya** | Server | **DNS Server** | Menangani resolusi nama domain jaringan. |
| **Vilya** | Server | **DHCP Server** | Server pusat pemberi alamat IP otomatis. |
| **Palantir** | Server | Web Server | Layanan HTTP/Web Internal 1. |
| **IronHills** | Server | Web Server | Layanan HTTP/Web Internal 2. |
| **Osgiliath** | Router | Core Router | Penghubung utama antar area dan ke NAT. |
| **Minastir** | Router | **DHCP Relay** | Meneruskan request IP dari Elendil/Isildur ke Vilya. |
| **AnduinBanks**| Router | **DHCP Relay** | Meneruskan request IP dari Gilgalad/Cirdan ke Vilya. |

---

# Tabel Kalkulasi VLSM

Perhitungan subnetting dilakukan berdasarkan alamat IP dasar **10.81.0.0** dengan urutan kebutuhan host terbesar ke terkecil.

| Nama Pasukan | Kebutuhan Host | Prefix | Subnet Mask | Network ID | Range IP Usable | Broadcast Address |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Elendil** | 200 | **/24** | 255.255.255.0 | `10.81.0.0` | 10.81.0.1 - 10.81.0.254 | 10.81.0.255 |
| **Gilgalad** | 100 | **/25** | 255.255.255.128 | `10.81.1.0` | 10.81.1.1 - 10.81.1.126 | 10.81.1.127 |
| **Durin** | 50 | **/26** | 255.255.255.192 | `10.81.1.128` | 10.81.1.129 - 10.81.1.190 | 10.81.1.191 |
| **Isildur** | 30 | **/26** | 255.255.255.192 | `10.81.1.192` | 10.81.1.193 - 10.81.1.254 | 10.81.1.255 |
| **Cirdan** | 20 | **/27** | 255.255.255.224 | `10.81.2.0` | 10.81.2.1 - 10.81.2.30 | 10.81.2.31 |
| **Khamul** | 5 | **/29** | 255.255.255.248 | `10.81.2.32` | 10.81.2.33 - 10.81.2.38 | 10.81.2.39 |
| *Server/Links* | - | **/29** | - | `10.81.2.40` | *Reserved for Servers* | - |


> **Catatan Teknis:** Kelompok **Isildur** menggunakan prefix **/26** (kapasitas 62 host) meskipun kebutuhannya 30 host. Hal ini karena prefix **/27** hanya menyediakan tepat 30 IP Usable. Karena 1 IP harus digunakan untuk Gateway Router, maka total yang dibutuhkan adalah 31 IP, sehingga wajib naik ke /26.

---
<img width="5204" height="3204" alt="VLSM MODUL 5 (1)" src="https://github.com/user-attachments/assets/350d3208-54e1-4d6b-9211-cd6734d6726a" />

<img width="5204" height="2736" alt="TREE VLSM MODUL 5 (1)" src="https://github.com/user-attachments/assets/7589b388-f3e1-4ecb-9709-e9f4f178271b" />


# Tabel Perencanaan Subnet & Kebutuhan Host

| Kode | Nama Subnet / Rute | Jumlah Host Asli | Total IP Dibutuhkan (+Gateway) | Total IP Tersedia (Prefix) |
| :--- | :--- | :--- | :--- | :--- |
| **A1** | Switch2 > **IronHills** (Web Server) | 1 | 2 | 4 (/30) |
| **A2** | Winderland > **Durin** (50) | 50 | 51 | 64 (/26) |
| **A3** | Winderland > **Khamul** (5) | 5 | 6 | 8 (/29) |
| **A4** | Inter-Router (**Winderland** - **Moria**) | - | 2 (Router Interfaces) | 4 (/30) |
| **A5** | Inter-Router (**Moria** - **Osgiliath**) | - | 2 (Router Interfaces) | 4 (/30) |
| **A6** | Rivendell > **Vilya** (DHCP), **Narya** (DNS) | 2 | 3 | 8 (/29) |
| **A7** | Inter-Router (**Rivendell** - **Osgiliath**) | - | 2 (Router Interfaces) | 4 (/30) |
| **A8** | Inter-Router (**Osgiliath** - **Minastir**) | - | 2 (Router Interfaces) | 4 (/30) |
| **A9** | Switch4 > **Elendil** (200), **Isildur** (30) | 230 | 231 | 256 (/24) |
| **A10** | Inter-Router (**Minastir** - **Pelargir**) | - | 2 (Router Interfaces) | 4 (/30) |
| **A11** | Pelargir > **Palantir** (Web Server) | 1 | 2 | 4 (/30) |
| **A12** | Inter-Router (**Pelargir** - **AnduinBanks**) | - | 2 (Router Interfaces) | 4 (/30) |
| **A13** | Switch5 > **Gilgalad** (100), **Cirdan** (20) | 120 | 121 | 128 (/25) |

# Tabel VLSM Lengkap (Network ID: 10.81.0.0)

| Kode | Subnet (Nama) | Prefix | Network ID | Netmask | Broadcast | Range IP (Usable) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **A9** | Client Elendil & Isildur | **/24** | 10.81.0.0 | 255.255.255.0 | 10.81.0.255 | 10.81.0.1 - 10.81.0.254 |
| **A13** | Client Gilgalad & Cirdan | **/25** | 10.81.1.0 | 255.255.255.128 | 10.81.1.127 | 10.81.1.1 - 10.81.1.126 |
| **A2** | Client Durin | **/26** | 10.81.1.128 | 255.255.255.192 | 10.81.1.191 | 10.81.1.129 - 10.81.1.190 |
| **A3** | Client Khamul | **/29** | 10.81.1.192 | 255.255.255.248 | 10.81.1.199 | 10.81.1.193 - 10.81.1.198 |
| **A6** | Server Farm (Vilya/Narya) | **/29** | 10.81.1.200 | 255.255.255.248 | 10.81.1.207 | 10.81.1.201 - 10.81.1.206 |
| **A1** | Web Server IronHills | **/30** | 10.81.1.208 | 255.255.255.252 | 10.81.1.211 | 10.81.1.209 - 10.81.1.210 |
| **A11** | Web Server Palantir | **/30** | 10.81.1.212 | 255.255.255.252 | 10.81.1.215 | 10.81.1.213 - 10.81.1.214 |
| **A4** | Backbone (Winderland-Moria) | **/30** | 10.81.1.216 | 255.255.255.252 | 10.81.1.219 | 10.81.1.217 - 10.81.1.218 |
| **A5** | Backbone (Moria-Osgiliath) | **/30** | 10.81.1.220 | 255.255.255.252 | 10.81.1.223 | 10.81.1.221 - 10.81.1.222 |
| **A7** | Backbone (Osgiliath-Rivendell) | **/30** | 10.81.1.224 | 255.255.255.252 | 10.81.1.227 | 10.81.1.225 - 10.81.1.226 |
| **A8** | Backbone (Osgiliath-Minastir) | **/30** | 10.81.1.228 | 255.255.255.252 | 10.81.1.231 | 10.81.1.229 - 10.81.1.230 |
| **A10** | Backbone (Minastir-Pelargir) | **/30** | 10.81.1.232 | 255.255.255.252 | 10.81.1.235 | 10.81.1.233 - 10.81.1.234 |
| **A12** | Backbone (Pelargir-Anduin) | **/30** | 10.81.1.236 | 255.255.255.252 | 10.81.1.239 | 10.81.1.237 - 10.81.1.238 |

# Misi Firewall
## Konfigurasi routing menggunakan IPtables (di osgilath)
<img width="1356" height="702" alt="image" src="https://github.com/user-attachments/assets/bf888573-aebc-48b9-b180-307ac3db49ec" />

Gunakan perintah
`iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.122.229`

## Konfigurasi Service di beberapa routing
<img width="810" height="396" alt="image" src="https://github.com/user-attachments/assets/775cee45-a295-480d-b7c7-2a4d4e7f37db" />

Kita akan setting dhcp server di vilya, diisni saya menggunakan contoh durin untuk memeragakan aktivasi server
<img width="796" height="344" alt="image" src="https://github.com/user-attachments/assets/7b1f6ef2-fac8-48e8-88b6-cbdbc53ddaae" />

Druin berhasil mendapatkan ip dynamicnya dari vilya
<img width="1367" height="551" alt="image" src="https://github.com/user-attachments/assets/ff77a830-a95e-4230-835b-53c20169b076" />

Dapat kita lihat hasil ip a yang menunjukkan ip vilya pada durin

## Tidak ada perangkat lain yang dapat ping ke vilya
kita set menggunakan perintah
`iptables -A INPUT -p icmp --icmp-type echo-request -j DROP`
<img width="989" height="248" alt="image" src="https://github.com/user-attachments/assets/73803a64-9e3c-431b-bdcc-b1fdd719049f" />

Dan apabila kita jalankan ping ke durin vilya dapat melakukannya, sedangkan apabila durin mencoba melakukan pingnya tidak akan bisa
<img width="835" height="133" alt="image" src="https://github.com/user-attachments/assets/414dfb81-4a7f-418e-a222-df05e570f530" />

## Hanya Vilya yang dapat mengakses Nalya
Pertama di dalam Narya kita akan melakukan konfigurasi iptables untuk firewall
```
# 1. Pastikan bersih dulu
iptables -F

# 2. IZINKAN VILYA (IP 10.81.0.50) - WAJIB DI ATAS
iptables -A INPUT -p udp --dport 53 -s 10.81.0.50 -j ACCEPT

# 3. BLOKIR SISANYA (Semua IP selain Vilya) - WAJIB DI BAWAH
iptables -A INPUT -p udp --dport 53 -j DROP
```
<img width="763" height="507" alt="image" src="https://github.com/user-attachments/assets/f03e9a01-8dae-4967-b7d4-96b3029dbab0" />

Saat sudah kita pastikan bahwa aturan firewaal tereksekusi dengan baik kita dapat mencoba nya di vilay dan durin untuk testing
<img width="1417" height="140" alt="image" src="https://github.com/user-attachments/assets/637d0572-6d27-45d1-b9bc-abfa02b1414a" />
<img width="937" height="100" alt="image" src="https://github.com/user-attachments/assets/3f4dc625-b9db-488c-9ce8-7d6846f3c997" />

## IronHills hanya boleh diakses pada Akhir Pekan (Sabtu & Minggu).
Pertama kita harus atur firewall pada ironhills untuk memastikan bahwa hanya hari senin paket bisa dikirimkan melalui command
```
# IZINKAN HANYA HARI SENIN (Mon)
iptables -A INPUT -p tcp --dport 80 -s 10.81.0.64/26 -m time --weekdays Mon -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -s 10.81.0.56/29 -m time --weekdays Mon -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -s 10.81.1.0/24 -m time --weekdays Mon -j ACCEPT

# BLOKIR SISANYA (Termasuk hari ini/Minggu)
iptables -A INPUT -p tcp --dport 80 -j DROP
```
<img width="825" height="58" alt="image" src="https://github.com/user-attachments/assets/3f2bbcca-b9bf-4cc2-8b43-713a298a7e94" />
Selanjutnya kita aplikasikan rule ke-2, dimana kita sesuaikan untuk hari minggu karena date yang saya gunakan tidak bisa mengganti hari, dan saya mengerjakan di hari minggu

```
iptables -F
# Izinkan Sat,Sun (Sabtu Minggu)
iptables -A INPUT -p tcp --dport 80 -s 10.81.0.64/26 -m time --weekdays Sat,Sun -j ACCEPT
# (dan seterusnya...)
iptables -A INPUT -p tcp --dport 80 -j DROP
```
<img width="740" height="49" alt="image" src="https://github.com/user-attachments/assets/89ef2a4b-1d4c-4091-ae3a-0ad6fba71a87" />

# REVISI NO 5 DAN 6
## Pembatasan Akses untuk palantir di jam jam tertentu
Melalu pembatasan firewall di jam tersebut dengan command sebagai berikut
```
# Hapus aturan lama
iptables -F

# (Karena sekarang jam 16:00, otomatis GAK MASUK)
iptables -A INPUT -p tcp --dport 80 -s 10.81.0.128/25 -m time --timestart 07:00 --timestop 10:00 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -s 10.81.0.130 -m time --timestart 07:00 --timestop 10:00 -j ACCEPT

# Blokir sisanya
iptables -A INPUT -p tcp --dport 80 -j DROP
```
dan command berikut untuk pembatasan jam di sesi kedua lebih tepatnya elendil
```
# Hapus aturan lama
iptables -F

iptables -A INPUT -p tcp --dport 80 -s 10.81.1.0/24 -m time --timestart 20:00 --timestop 23:00 -j ACCEPT

# Blokir sisanya
iptables -A INPUT -p tcp --dport 80 -j DROP
```
Testing di node palantir untuk aturan sebagai berikut
<img width="1466" height="414" alt="image" src="https://github.com/user-attachments/assets/57c072c7-1931-40e0-8a60-5ad0211bd74a" />

Selanjutnya kita set beberapa time untuk kondisi
<img width="579" height="140" alt="image" src="https://github.com/user-attachments/assets/4986dcb5-9f63-4763-bcb5-c7ed510a7207" />

Dan dapat terlihat kita tes melalui firewall di waktu tertentu pada gilgalad dan elendil
<img width="886" height="195" alt="image" src="https://github.com/user-attachments/assets/58f58bb5-5db5-4f62-af6c-1f4733871426" />
<img width="848" height="300" alt="image" src="https://github.com/user-attachments/assets/fdf3c7b2-4389-4859-b4b0-e3c06460ca68" />

## Uji Keamanan Palantir memlalui nmap scan port dan pemblokiran IP
Pertama kita set iptables kedalam palantir
```
#!/bin/bash
# Reset Firewall dulu biar bersih
iptables -F

# -----------------------------------------------------------------------
# ATURAN 1: BLOKIR TOTAL (The Bouncer)
# Cek apakah IP pengirim sudah ada di daftar "BLACKLIST".
# Jika ada, DROP semua paket (TCP, UDP, ICMP/Ping).
# --update: Setiap paket baru akan memperpanjang durasi hukuman (60 detik).
# -----------------------------------------------------------------------
iptables -A INPUT -m recent --name BLACKLIST --update --seconds 60 -j DROP

# -----------------------------------------------------------------------
# ATURAN 2: PENCATAT (The Counter)
# Setiap ada koneksi baru (SYN) ke port TCP manapun, catat IP-nya.
# Kita pakai daftar terpisah "SCAN_COUNTER" untuk menghitung.
# -----------------------------------------------------------------------
iptables -A INPUT -p tcp --syn -m recent --name SCAN_COUNTER --set

# -----------------------------------------------------------------------
# ATURAN 3: DETEKSI & LOG (The Alarm)
# Cek apakah di daftar "SCAN_COUNTER" sudah ada >15 hits dalam 20 detik?
# Jika YA, catat ke LOG sistem.
# -----------------------------------------------------------------------
iptables -A INPUT -p tcp --syn -m recent --name SCAN_COUNTER --rcheck --seconds 20 --hitcount 15 -j LOG --log-prefix "PORT_SCAN_DETECTED: " --log-level 4

# -----------------------------------------------------------------------
# ATURAN 4: EKSEKUSI HUKUMAN (The Judge)
# Jika >15 hits dalam 20 detik, masukkan IP tersangka ke daftar "BLACKLIST".
# Mulai detik ini, dia akan kena Aturan No. 1 (Blokir Total).
# -----------------------------------------------------------------------
iptables -A INPUT -p tcp --syn -m recent --name SCAN_COUNTER --rcheck --seconds 20 --hitcount 15 -m recent --name BLACKLIST --set -j DROP

# -----------------------------------------------------------------------
# ATURAN 5: IZINKAN TRAFFIC NORMAL
# Kalau belum kena limit, izinkan masuk (misal Web Server 80)
# -----------------------------------------------------------------------
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
# Izinkan Ping normal (sebelum kena blokir)
iptables -A INPUT -p icmp -j ACCEPT

echo "🔥 JEBAKAN PORT SCAN AKTIF!"
echo "Ketentuan: > 15 Port / 20 Detik = BANNED 60 Detik"
```

Kemudian kita dapatkan hasil jebakan, dan kita lakukan scan nmap di elendil, sebelumnya kita lakukan dulu tes ping ke ip elendil agar membuktikan jika awalnya routing berjalan
<img width="777" height="152" alt="image" src="https://github.com/user-attachments/assets/8be66119-30c4-4a5e-ba35-5d67dff67c53" />

<img width="858" height="484" alt="image" src="https://github.com/user-attachments/assets/96346190-3ffd-4dd1-8757-49cbf99f7112" />

Yang terakhir karena kita memang memberikan hasil untuk blokir ip apabila kita diserang, kita tidak akan bisa melanjutkannya dan ping dari elendil sudah tidak bisa karena elendil sudah terblacklist sebagai penyerang
<img width="804" height="166" alt="image" src="https://github.com/user-attachments/assets/ce4fc892-85ad-4b3b-b4d8-de15b9cb4983" />





















