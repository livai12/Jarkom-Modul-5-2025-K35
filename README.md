# Jarkom-Modul-5-2025-K35-

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
