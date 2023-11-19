# Jarkom-Modul-3-E22-2023

| Nama                       | NRP        |
| ---------------------------| -----------|
| Anggara Saputra            | 5025211241 |
| Faizah Nurdianti Maghfirah | 5025211134 |


## Topologi

## Configuration
* Aura
```
auto eth0
iface eth0 inet dhcp
up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.217.0.0/16

auto eth1
iface eth1 inet static
	address 192.217.1.200
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.217.2.200
	netmask 255.255.255.0


auto eth3
iface eth3 inet static
	address 192.217.3.200
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.217.4.200
	netmask 255.255.255.00
```
* Himmel
```
auto eth0
iface eth0 inet static
	address 192.217.1.2
	netmask 255.255.255.0
	gateway 192.217.1.200
```
*Heiter
```
auto eth0
iface eth0 inet static
	address 192.217.1.3
	netmask 255.255.255.0
	gateway 192.217.1.200
```
* Denken
```
auto eth0
iface eth0 inet static
	address 192.217.2.1
	netmask 255.255.255.0
	gateway 192.217.2.200
```
* Eisen
```
auto eth0
iface eth0 inet static
	address 192.217.2.2
	netmask 255.255.255.0
	gateway 192.217.2.200
```
* Lawine
```
auto eth0
iface eth0 inet static
	address 192.217.3.1
	netmask 255.255.255.0
	gateway 192.217.3.200
```
* Linie
```
auto eth0
iface eth0 inet static
	address 192.217.3.2
	netmask 255.255.255.0
	gateway 192.217.3.200
```
* Lugner
```
auto eth0
iface eth0 inet static
	address 192.217.3.3
	netmask 255.255.255.0
	gateway 192.217.3.200

```
* Richter
```
auto eth0
iface eth0 inet dhcp
hwaddress ether be:e3:82:dd:21:11
```
* Revolte
```
auto eth0
#iface eth0 inet dhcp
iface eth0 inet static
	address 192.217.3.69
	netmask 255.255.255.0
	gateway 192.217.3.200

```
* Sein
```
auto eth0
iface eth0 inet dhcp
hwaddress ether b2:c6:fc:0e:91:de
```
* Stark
```
auto eth0
iface eth0 inet dhcp
hwaddress ether 22:12:33:c2:ec:b7
```
* Frieren
```
auto eth0
iface eth0 inet static
	address 192.217.4.1
	netmask 255.255.255.0
	gateway 192.217.4.200
```
* Flamme
```
auto eth0
iface eth0 inet static
	address 192.217.4.2
	netmask 255.255.255.0
	gateway 192.217.4.200
```
* Fern
```
auto eth0
iface eth0 inet static
	address 192.217.4.3
	netmask 255.255.255.0
	gateway 192.217.4.200
```


## Soal 0
Melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP (0) mengarah pada worker yang memiliki IP [prefix IP].x.1.
### Jawab

## Soal 1
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
### Jawab

## Soal 2
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80
### Jawab

## Soal 3
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168
### Jawab

## Soal 4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut
### Jawab

## Soal 5
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit
### Jawab

## Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.
### Jawab

## Soal 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
- Lawine, 4GB, 2vCPU, dan 80 GB SSD.
- Linie, 2GB, 2vCPU, dan 50 GB SSD.
- Lugner 1GB, 1vCPU, dan 25 GB SSD.

Aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

### Jawab

## Soal 8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- Nama Algoritma Load Balancer
- Report hasil testing pada Apache Benchmark
- Grafik request per second untuk masing masing algoritma.
- Analisis

### Jawab

## Soal 9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.
### Jawab


## Soal 10
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/
### Jawab

## Soal 11
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. hint: (proxy_pass)

### Jawab

## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. hint: (fixed in dulu clinetnya)
### Jawab


## Soal 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern
### Jawab


## Soal 14
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer
### Jawab


## Soal 15
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
POST /auth/register

### Jawab

## Soal 16
POST /auth/login (16)

### Jawab


## Soal 17
GET /me
### Jawab


## Soal 18
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.
### Jawab


## Soal 19
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire

### Jawab


## Soal 20
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.
### Jawab

## Kendala
