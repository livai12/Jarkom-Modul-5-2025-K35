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
| **A1** | Web Server IronHills | **/30** | 10.81.1.208 | 255.255.255.252 | 10.81.1.211 | 10.81.1.209 - 10.81.1.210 |
| **A2** | Client Durin | **/26** | 10.81.1.128 | 255.255.255.192 | 10.81.1.191 | 10.81.1.129 - 10.81.1.190 |
| **A3** | Client Khamul | **/29** | 10.81.1.192 | 255.255.255.248 | 10.81.1.199 | 10.81.1.193 - 10.81.1.198 |
| **A4** | Backbone (Winderland-Moria) | **/30** | 10.81.1.216 | 255.255.255.252 | 10.81.1.219 | 10.81.1.217 - 10.81.1.218 |
| **A5** | Backbone (Moria-Osgiliath) | **/30** | 10.81.1.220 | 255.255.255.252 | 10.81.1.223 | 10.81.1.221 - 10.81.1.222 |
| **A6** | Server Farm (Vilya/Narya) | **/29** | 10.81.1.200 | 255.255.255.248 | 10.81.1.207 | 10.81.1.201 - 10.81.1.206 |
| **A7** | Backbone (Osgiliath-Rivendell) | **/30** | 10.81.1.224 | 255.255.255.252 | 10.81.1.227 | 10.81.1.225 - 10.81.1.226 |
| **A8** | Backbone (Osgiliath-Minastir) | **/30** | 10.81.1.228 | 255.255.255.252 | 10.81.1.231 | 10.81.1.229 - 10.81.1.230 |
| **A9** | Client Elendil & Isildur | **/24** | 10.81.0.0 | 255.255.255.0 | 10.81.0.255 | 10.81.0.1 - 10.81.0.254 |
| **A10** | Backbone (Minastir-Pelargir) | **/30** | 10.81.1.232 | 255.255.255.252 | 10.81.1.235 | 10.81.1.233 - 10.81.1.234 |
| **A11** | Web Server Palantir | **/30** | 10.81.1.212 | 255.255.255.252 | 10.81.1.215 | 10.81.1.213 - 10.81.1.214 |
| **A12** | Backbone (Pelargir-Anduin) | **/30** | 10.81.1.236 | 255.255.255.252 | 10.81.1.239 | 10.81.1.237 - 10.81.1.238 |
| **A13** | Client Gilgalad & Cirdan | **/25** | 10.81.1.0 | 255.255.255.128 | 10.81.1.127 | 10.81.1.1 - 10.81.1.126 |
