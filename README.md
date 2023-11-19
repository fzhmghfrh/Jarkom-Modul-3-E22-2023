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
Instalasi bind9
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt update
apt install bind9 -y
```
Masukkan konfigurasi pada file /etc/bind/named.conf.local
```
mkdir /etc/bind/jarkom
echo '
zone "granz.channel.e22.com" {
        type master;
        notify yes;
        file "/etc/bind/jarkom/granz.channel.e22.com";
};
' > /etc/bind/named.conf.local
```
Konfigurasi file /etc/bind/jarkom/granz.channel.e22.com
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.217.com. root.granz.channel.217.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.e22.com.
@       IN      A       192.217.2.2
www     IN      CNAME   granz.channel.e22.com.
@       IN      AAAA    ::1' > /etc/bind/jarkom/granz.channel.e22.com
```
Tambahkan zone pada file /etc/bind/named.conf.local untuk mendaftarkan domain riegel.canyon.e22.com untuk IP Frieren Laravel Worker pada node Heiter DNS Server.
```
echo 'zone "riegel.canyon.e22.com" {
        type master;
        notify yes;
        file "/etc/bind/jarkom/riegel.canyon.e22.com";
};
' > /etc/bind/named.conf.local
```
Konfigurasi dalam file /etc/bind/jarkom/riegel.canyon.e22.com
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.e22.com. root.riegel.canyon.e22.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.e22.com.
@       IN      A       192.217.2.2
www     IN      CNAME   riegel.canyon.e22.com.
@       IN      AAAA    ::1' > /etc/bind/jarkom/riegel.canyon.e22.com
```
Restart pada bind9
```
service bind9 start
```


## Soal 1
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
### Jawab
Instalasi dhcp relay
```
apt update -y
apt-get install isc-dhcp-relay -y
Service isc-dhcp-relay start
```
Konfigurasi /etc/default/isc-dhcp-relay
```
echo '
SERVERS="192.217.1.2" #ip dari dhcp server
INTERFACES="eth1 eth2 eth3 eth4" #nextserverDHCP
OPTIONS=""
' > /etc/default/isc-dhcp-relay
```
Konfigurasi /etc/sysctl.conf
```
net.ipv4.ip_forward=1
```
Restart DHCP Relay
```
service isc-dhcp-relay restart
```

## Soal 2
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80
### Jawab
Instalasi dhcp server pada Himmel
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
```
```
apt update
apt-get install isc-dhcp-server -y
```
Konfigurasi /etc/default/isc-dhcp-server
```
# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
#DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPDv4_PID=/var/run/dhcpd.pid
#DHCPDv6_PID=/var/run/dhcpd6.pid

# Additional options to start dhcpd with.
#       Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#       Separate multiple interfaces with spaces, e.g. "eth0 eth1"

INTERFACESv4="eth0"
#INTERFACESv6=""
```
Konfigurasi /etc/dhcp/dhcp.conf
```
subnet 192.217.1.0 netmask 255.255.255.0 {
    option routers 192.217.1.212;
    option broadcast-address 192.217.1.255;
    option domain-name-servers 192.217.1.3, 192.168.122.1;
}

subnet 192.217.3.0 netmask 255.255.255.0 {
    range 192.217.3.16 192.217.3.32;
    range 192.217.3.64 192.217.3.80;
    option routers 192.217.3.212;
    option broadcast-address 192.217.3.255;
}
```

## Soal 3
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168
### Jawab
Konfigurasi /etc/dhcp/dhcpd.conf
```
subnet 192.217.4.0 netmask 255.255.255.0 {
    range 192.217.4.12 192.217.4.20;
    range 192.217.4.160 192.217.4.168;
    option routers 192.217.4.212;
    option broadcast-address 192.217.4.255;
}
```

## Soal 4
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut
### Jawab
```
subnet 192.217.3.0 netmask 255.255.255.0 {
    range 192.217.3.16 192.217.3.32;
    range 192.217.3.64 192.217.3.80;
    option routers 192.217.3.212;
    option broadcast-address 192.217.3.255;
    option domain-name-servers 192.217.1.3, 192.168.122.1;
}

subnet 192.217.4.0 netmask 255.255.255.0 {
    range 192.217.4.12 192.217.4.20;
    range 192.217.4.160 192.217.4.168;
    option routers 192.217.4.212;
    option broadcast-address 192.217.4.255;
    option domain-name-servers 192.217.1.3, 192.168.122.1;
}
```

## Soal 5
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit
### Jawab
```
subnet 192.217.4.0 netmask 255.255.255.0 {
    range 192.217.4.12 192.217.4.20;
    range 192.217.4.160 192.217.4.168;
    option routers 192.217.4.212;
    option broadcast-address 192.217.4.255;
    option domain-name-servers 192.217.1.3, 192.168.122.1;
    default-lease-time 720;
    max-lease-time 5760;
}
subnet 192.217.3.0 netmask 255.255.255.0 {
    range 192.217.3.16 192.217.3.32;
    range 192.217.3.64 192.217.3.80;
    option routers 192.217.3.212;
    option broadcast-address 192.217.3.255;
    option domain-name-servers 192.217.1.3, 192.168.122.1;
    default-lease-time 180;
    max-lease-time 5760;
}
```

## Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.
### Jawab
Instalasi nginx, wget, php pada semua php worker
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get update && apt install nginx wget zip htop php7.3 php7.3-fpm -y
```
Download file website statis php
```wget -O '/var/www/jarkom.zip' 'https://drive.google.com/uc?id=1ViSkRq7SmwZgdK64e
Rbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/jarkom.zip -d /var/www/
rm /var/www/jarkom.zip
```
Buat file index.php pada masing-masing PHP Worker
- Lawine
```
<!DOCTYPE html>
<html>
<head>
    <title>Granz Channel Map</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to Granz Channel</h1>
        <p><?php
            $hostname = gethostname();
            echo "Request ini dihandle oleh: $hostname<br>"; ?> </p>
        <p>Enter your name to validate:</p>
        <form method="POST" action="index.php">
            <input type="text" name="name" id="nameInput">
            <button type="submit" id="submitButton">Submit</button>
        </form>
        <p id="greeting"><?php
            if(isset($_POST[name])) {
                $name = $_POST[name];
                echo "Hello, $name!";
            }
        ?></p>
    </div>

    <script src="js/script.js"></script>
</body>
</html>
```
- Liene
```
<!DOCTYPE html>
<html>
<head>
    <title>Granz Channel Map</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to Granz Channel</h1>
        <p><?php
            $hostname = gethostname();
            echo "Request ini dihandle oleh: $hostname<br>"; ?> </p>
        <p>Enter your name to validate:</p>
        <form method="POST" action="index.php">
            <input type="text" name="name" id="nameInput">
            <button type="submit" id="submitButton">Submit</button>
        </form>
        <p id="greeting"><?php
            if(isset($_POST[name])) {
                $name = $_POST[name];
                echo "Hello, $name!";
            }
        ?></p>
    </div>

    <script src="js/script.js"></script>
</body>
</html>
```
- Lugner
```
<!DOCTYPE html>
<html>
<head>
    <title>Granz Channel Map</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to Granz Channel</h1>
        <p><?php
            $hostname = gethostname();
            echo "Request ini dihandle oleh: $hostname<br>"; ?> </p>
        <p>Enter your name to validate:</p>
        <form method="POST" action="index.php">
            <input type="text" name="name" id="nameInput">
            <button type="submit" id="submitButton">Submit</button>
        </form>
        <p id="greeting"><?php
            if(isset($_POST[name])) {
                $name = $_POST[name];
                echo "Hello, $name!";
            }
        ?></p>
    </div>

    <script src="js/script.js"></script>
</body>
</html>
```

Tambahkan ip dns server ke nameserver ke semua php worker
```
echo nameserver '192.217.1.3' > /etc/resolv.conf
```
Setup load balancer pada semua php worker
```
	server {

        listen 80;

        root /var/www/modul-3;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        }

    location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }

ln -s /etc/nginx/sites-available/modul-3 /etc/nginx/sites-enabled/modul-3

rm /etc/nginx/sites-enabled/default
```
Restart nginx dan apache2-utils di semua php worker
```
service nginx restart
service php7.3-fpm stop
service php7.3-fpm start
```
Instalasi load balancer
```
nameserver 192.217.1.3
nameserver 192.168.122.1
```
Konfigurasi /etc/nginx/sites-available/lb-proxy
```
 upstream granz  {
        #least_conn;
        #ip_hash;
        #hash $request_uri consistent;
        #server 192.217.3.1 weight=4;
        #server 192.217.3.2 weight=2;
        #server 192.217.3.3 weight=1;

        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }

 upstream riegel {
        server 192.217.4.1;
        server 192.217.4.2;
        server 192.217.4.3;
 }

 server {
        listen 80;
        server_name granz.channel.e22.com www.granz.channel.e22.com;

        allow 192.217.3.69;
        allow 192.217.3.70;
        allow 192.217.4.167;
        allow 192.217.4.168;
        deny all;

        auth_basic "Authorization";
        auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

        location / {
        proxy_pass http://granz;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        }

        location /its {
        proxy_pass https://its.ac.id;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    }


        location ~ /\.ht {
            deny all;
        }

error_log /var/log/nginx/lb_error.log;
access_log /var/log/nginx/lb_access.log;

 }

server {
        listen 80;
        server_name riegel.canyon.e22.com www.riegel.canyon.e22.com;

        allow 192.217.3.69;
        allow 192.217.3.70;
        allow 192.217.4.167;
        allow 192.217.4.168;
        deny all;

        auth_basic "Authorization";
        auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

        location / {
        proxy_pass http://riegel;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        }

        location /its {
        proxy_pass https://its.ac.id;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
    }


        location ~ /\.ht {
            deny all;
        }

error_log /var/log/nginx/lb_error2.log;
access_log /var/log/nginx/lb_access2.log;

 }
```
Symbolic link
```
ln -s /etc/nginx/sites-available/lb-proxy /etc/nginx/sites-enabled/lb-proxy

rm /etc/nginx/sites-enabled/default
```
Restart nginx
```
service nginx restart
```

## Soal 7
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
- Lawine, 4GB, 2vCPU, dan 80 GB SSD.
- Linie, 2GB, 2vCPU, dan 50 GB SSD.
- Lugner 1GB, 1vCPU, dan 25 GB SSD.

Aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.

### Jawab
Instalasi pada client untuk melakukan benchmarking
```
apt-get -y install lynx
apt-get install apache2-utils jq -y
```
Jalankan script benchmarking
```
ab -n 1000 -c 100 http://granz.channel.com/
```

## Soal 8
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- Nama Algoritma Load Balancer
- Report hasil testing pada Apache Benchmark
- Grafik request per second untuk masing masing algoritma.
- Analisis

### Jawab
Algoritma Round Robin (Default):
```
 upstream granz  {
        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
Algoritma Least Connection:
```
 upstream granz  {
        least_conn;
        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
Hasil Testing
```
ab -n 200 -c 10 http://granz.channel.e22.com/
```
Algoritma IP Hash:
```
 upstream granz  {
        ip_hash;
        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
Hasil Testing
```
ab -n 200 -c 10 http://granz.channel.e22.com/
```

Algoritma Generic Hash:
```
 upstream granz  {
        hash $request_uri consistent;
        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
Hasil Testing
```
ab -n 200 -c 10 http://granz.channel.e22.com/
```

Algoritma Weighted Round Robin:
```
 upstream granz  {
        server 192.217.3.1 weight=1;
        server 192.217.3.2 weight=2;
        server 192.217.3.3 weight=3;
 }
```
Hasil Testing
```
ab -n 200 -c 10 http://granz.channel.e22.com/
```
Hasil Grafik


## Soal 9
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.
### Jawab
- Hasil testing 3 Worker dengan round robin:
```
upstream granz  {
        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
- Hasil Testing
```
ab -n 100 -c 10 http://granz.channel.e22.com/
Hasil testing 2 Worker dengan round robin:
 upstream granz  {
        #server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
- Hasil Testing
```
ab -n 100 -c 10 http://granz.channel.e22.com/
```
- Hasil testing 1 Worker dengan round robin:
```
 upstream granz  {
        #server 192.217.3.1; #IP Lawine
        #server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }
```
- Hasil Testing
```
ab -n 100 -c 10 http://granz.channel.e22.com/
```
- Hasil Grafik


## Soal 10
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/
### Jawab
Lakukan instalasi apache2-utils
```
apt-get update && apt install nginx apache2-utils -y
mkdir /etc/nginx/rahasiakita
```
Buat password dengan username netics dan password ajke22:
```
htpasswd -c -b /etc/nginx/rahasiakita/.htpasswd netics ajke22
```
Tambahkan konfigurasi berikut pada /etc/nginx/sites-available/lb-proxy di Eisen Load balancer
```
 server {
        listen 80;
        server_name _;

        auth_basic "Authorization";
        auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

        location / {
                proxy_pass http://granz;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location ~ /\.ht {
            deny all;
        }

        error_log /var/log/nginx/lb_error.log;
        access_log /var/log/nginx/lb_access.log;
}
```
Testing pada salah satu Client:
- Masukkan username
- Masukkan password
- Tampilan website


## Soal 11
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. hint: (proxy_pass)
### Jawab
Tambahkan konfigurasi berikut pada /etc/nginx/sites-available/lb-proxy di Eisen Load Balancer
```
 server {
        listen 80;
        server_name _;

        auth_basic "Authorization";
        auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

        location / {
                proxy_pass http://granz;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location ~ /its {
                proxy_pass https://its.ac.id;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location ~ /\.ht {
            deny all;
        }

        error_log /var/log/nginx/lb_error.log;
        access_log /var/log/nginx/lb_access.log;
}
```
Testing pada salah satu client yaitu Revolte Client:
```
lynx granz.channel.e22.com/its
```


## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168. hint: (fixed in dulu clinetnya)
### Jawab
Tambahkan konfigurasi berikut pada Himmel DHCP Server di /etc/dhcp/dhcpd.conf untuk memberikan fixed address pada client
```
host Revolte{
    hardware ethernet 16:42:37:9f:51:41;
    fixed-address 192.217.3.69;
}

host Richter{
    hardware ethernet be:e3:82:dd:21:11;
    fixed-address 192.217.3.70;
}

host Sein{
    hardware ethernet b2:c6:fc:0e:91:de;
    fixed-address 192.217.4.167;
}

host Stark{
   hardware ethernet 22:12:33:c2:ec:b7;
   fixed-address 192.217.4.168;
}
```

Tambahkan konfigurasi berikut pada Eisen Load Balander pada /etc/nginx/sites-available/lb-proxy
```
 server {
        listen 80;
        server_name _;

        allow 192.217.3.69;
        allow 192.217.3.70;
        allow 192.217.4.167;
        allow 192.217.4.168;
        deny all;

        auth_basic "Authorization";
        auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

        location / {
                proxy_pass http://granz;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location ~ /its {
                proxy_pass https://its.ac.id;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location ~ /\.ht {
            deny all;
        }

        error_log /var/log/nginx/lb_error.log;
        access_log /var/log/nginx/lb_access.log;
}
```

- Revolte
- Ritcher
- Sein
- Stark


## Soal 13
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern
### Jawab
Lakukan instalasi mariadb-server
```
echo "nameserver 192.217.1.3
nameserver 192.168.122.1
" > /etc/resolv.conf

apt-get update

apt-get install mariadb-server -y
```
Buat user pada database
```
echo '
[client-server]

[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf

service mysql restart

echo "
CREATE USER IF NOT EXISTS 'kelompoke22'@'%' IDENTIFIED BY 'passworde22';
CREATE USER IF NOT EXISTS 'kelompoke22'@'localhost' IDENTIFIED BY 'passworde22';
CREATE DATABASE IF NOT EXISTS dbkelompoke22;
GRANT ALL PRIVILEGES ON *.* TO 'kelompoke22'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompoke22'@'localhost';
FLUSH PRIVILEGES;
" > ~/script.sql

mysql < ~/script.sql
```

## Soal 14
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer
### Jawab
Jalankan script berikut pada Eisen Load Balancer untuk mengconfig balancer pada riegel.canyon.e22.com dan sekaligus granz.channel.e22.com
```
echo ' # Default menggunakan Round Robin
 upstream granz  {
        #least_conn;
        #ip_hash;
        #hash $request_uri consistent;
        #server 192.217.3.1 weight=4;
        #server 192.217.3.2 weight=2;
        #server 192.217.3.3 weight=1;

        server 192.217.3.1; #IP Lawine
        server 192.217.3.2; #IP Linie
        server 192.217.3.3; #IP Lugner
 }

 upstream riegel {
        least_conn;
        server 192.217.4.1;
        server 192.217.4.2;
        server 192.217.4.3;
 }

 server {
        listen 80;
        server_name _;

        allow 192.217.3.69;
        allow 192.217.3.70;
        allow 192.217.4.167;
        allow 192.217.4.168;
        deny all;

        auth_basic "Authorization";
        auth_basic_user_file /etc/nginx/rahasiakita/.htpasswd;

        location / {
                proxy_pass http://granz;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location ~ /its {
                proxy_pass https://its.ac.id;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location ~ /\.ht {
            deny all;
        }

        error_log /var/log/nginx/lb_error.log;
        access_log /var/log/nginx/lb_access.log;
}

server {
        listen 80;
        server_name riegel.canyon.e22.com www.riegel.canyon.e22.com;

        allow 192.217.3.69;
        allow 192.217.3.70;
        allow 192.217.4.167;
        allow 192.217.4.168;
        deny all;

        location / {
                proxy_pass http://riegel;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
        }

        location /its {
                proxy_pass https://its.ac.id;
                proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        }


        location ~ /\.ht {
            deny all;
        }

        error_log /var/log/nginx/lb_error2.log;
        access_log /var/log/nginx/lb_access2.log;
}' > /etc/nginx/sites-available/lb-proxy

ln -s /etc/nginx/sites-available/lb-proxy /etc/nginx/sites-enabled/lb-proxy

rm /etc/nginx/sites-enabled/default
```
Jalankan script berikut untuk melakukan instalasi package-package yang diperlukan oleh masing-masing Laravel Worker.
```
echo "nameserver 192.217.1.3
nameserver 192.168.122.1
" > /etc/resolv.conf

apt-get update && apt install nginx php8.0 php8.0-fpm wget zip htop mariadb-clie
nt -y
apt-get install -y lsb-release ca-certificates apt-transport-https software-prop
erties-common gnupg2

curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/ph
p/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://pa
ckages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
'

apt-get update

apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl
php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl -y

wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer
```
Clone github repository untuk websitenya pada masing-masing Laravel Worker
```
wget -O '/var/www/jarkom.zip' 'https://github.com/martuafernando/laravel-praktik
um-jarkom/archive/refs/heads/main.zip'
unzip -o /var/www/jarkom.zip -d /var/www/
rm /var/www/jarkom.zip
```
Tambahkan file .env pada file laravelnya:
```
echo '
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.217.2.1
DB_PORT=3306
DB_DATABASE=dbkelompoke22
DB_USERNAME=kelompoke22
DB_PASSWORD=passworde22

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=217.0.0.1

REDIS_HOST=217.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
' > /var/www/laravel-praktikum-jarkom-main/.env
```
Jalankan script berikut untuk melakukan migration and seeding pada node Frieren Laravel Worker:
```
cd /var/www/laravel-praktikum-jarkom-main

composer update
php artisan migrate:fresh
php artisan db:seed --class=AiringsTableSeeder
php artisan key:generate
php artisan jwt:secret
```
Jalankan script berikut untuk konfigurasi load balancer pada masing-masing Laravel Worker:
```
cd ~

echo '
 server {

        listen 80;

        root /var/www/laravel-praktikum-jarkom-main/public;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
        }

    location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }
' > /etc/nginx/sites-available/laravel-praktikum-jarkom-main
ln -s /etc/nginx/sites-available/laravel-praktikum-jarkom-main /etc/nginx/sites-
enabled/laravel-praktikum-jarkom-main

chown -R www-data.www-data /var/www/laravel-praktikum-jarkom-main/storage

rm /etc/nginx/sites-enabled/default
```
Jalankan script berikut untuk melakukan restart nginx dan php-fpm
```
service nginx restart
service php8.0-fpm stop
service php8.0-fpm start
```

- Migrasi database
- Data database
- lynx riegel.canyon.e22.com


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
