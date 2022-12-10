# Jarkom-Modul-5-C06-2022

## Anggota Kelompok
1. 5025201050 - Elshe Erviana Angely
2. 5025201051 - Muhammad Fath Mushaffa Azhar
3. 5025201076 - Raul Ilma Rajasa

### (A.) Topologi
![Topologi.png](assets/C06_Topologi.png)

### (B.) VLSM Subnetting
Untuk membuat VLSM, pertama-tama, kita perlu membuat tabel yang berisi jumlah IP pada setiap subnet beserta totalnya

#### Tabel Subnet
| Subnet | Jumlah IP | Netmask |
| --- | --- | --- |
| A1 | 4 | /29 |
| A2 | 63 | /25 |
| A3 | 701 | /22 |
| A4 | 2 | /30 |
| A5 | 2 | /30 |
| A6 | 256 | /23 |
| A7 | 201 | /24 |
| A8 | 4 | /29 |
| Total | 1233 | /21 |

#### Konfigurasi IP dengan VLSM (Variable Length Subnet Masking)
![VLSM_Konfigurasi IP.png](assets/C06_VLSM_Konfigurasi%20IP.png)

#### VLSM Tree
Sehingga proyeksi tree dari VLSM-nya adalah sebagai berikut:
![VLSM_Tree.png](assets/C06_VLSM_Subnetting%20Tree.jpg)

#### Pembagian IP
| Subnet | Network ID | Netmask | Broadcast |
| --- | --- | --- | --- |
| A1 | 192.182.0.8 | 255.255.255.248 | 192.182.0.15 |
| A2 | 192.182.0.128 | 255.255.255.128 | 192.182.0.255 |
| A3 | 192.182.4.0 | 255.255.252.0 | 192.182.7.255 |
| A4 | 192.182.0.0 | 255.255.255.252 | 192.182.0.3 |
| A5 | 192.182.0.4 | 255.255.255.252 | 192.182.0.7 |
| A6 | 192.182.2.0 | 255.255.254.0 | 192.182.3.255 |
| A7 | 192.182.1.0 | 255.255.255.0 | 192.182.1.255 |
| A8 | 192.182.0.16 | 255.255.255.248 | 192.182.0.23 |

### Konfigurasi GNS
#### Eden
```
auto eth0
iface eth0 inet static
	address 192.182.0.11
	netmask 255.255.255.248
	gateway 192.182.0.9
```

### WISE
```
auto eth0
iface eth0 inet static
	address 192.182.0.12
	netmask 255.255.255.248
	gateway 192.182.0.9
```

### Garden
```
auto eth0
iface eth0 inet static
	address 192.182.0.18
	netmask 255.255.255.248
	gateway 192.182.0.17
```

### SSS
```
auto eth0
iface eth0 inet static
	address 192.182.0.19
	netmask 255.255.255.248
	gateway 192.182.0.17
```

### Strix
```
#Strix
auto eth0
iface eth0 inet static
       address 192.168.122.2
       netmask 255.255.255.252
       gateway 192.168.122.1
       up echo nameserver 192.168.122.1 > /etc/resolv.conf

#A5
auto eth1
iface eth1 inet static
	address 192.182.0.1
	netmask 255.255.255.252

#A4
auto eth2
iface eth2 inet static
	address 192.182.0.5
	netmask 255.255.255.252
```

### Westalis
```
#Westalis
#A4
auto eth0
iface eth0 inet static
	address 192.182.0.6
	netmask 255.255.255.252
	gateway 192.182.0.5
#A1
auto eth1
iface eth1 inet static
	address 192.182.0.9
	netmask 255.255.255.248

#A3
auto eth2
iface eth2 inet static
	address 192.182.4.1
	netmask 255.255.252.0

#A2
auto eth3
iface eth3 inet static
	address 192.182.0.129
	netmask 255.255.255.128
```

### Ostania
```
#Ostania
auto eth0
iface eth0 inet static
	address 192.182.0.2
	netmask 255.255.255.252
	gateway 192.182.0.1

#A8
auto eth1
iface eth1 inet static
	address 192.182.0.17
	netmask 255.255.255.248

#A6
auto eth2
iface eth2 inet static
	address 192.182.2.1
	netmask 255.255.255.254

#A7
auto eth3
	iface eth3 inet static
	address 192.182.1.1
	netmask 255.255.255.0
```

### Forger(62Host)
```
auto eth0
iface eth0 inet static
	address 192.182.0.130
	netmask 255.255.255.128
	gateway 192.182.0.129
```

### Desmond(700Host)
```
auto eth0
iface eth0 inet static
	address 192.182.4.2
	netmask 255.255.255.0
	gateway 192.182.4.1
```

### Blackbell(255Host)
```
auto eth0
iface eth0 inet static
	address 192.182.2.2
	netmask 255.255.254.0
	gateway 192.182.2.1
```

### Briar(200Host)
```
auto eth0
iface eth0 inet static
	address 192.182.1.2
	netmask 255.255.255.0
	gateway 192.182.1.1
```

### (C.) Routing
#### Strix
```
route add -net 192.182.0.8 netmask 255.255.255.248 gw 192.182.0.2
route add -net 192.182.0.128 netmask 255.255.255.128 gw 192.182.0.2
route add -net 192.182.4.0 netmask 255.255.252.0 gw 192.182.0.2

route add -net 192.182.2.0 netmask 255.255.254.0 gw 192.182.0.6
route add -net 192.182.1.0 netmask 255.255.255.0 gw 192.182.0.6
route add -net 192.182.0.16 netmask 255.255.255.248 gw 192.182.0.6
```

#### Ostania
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.182.0.5
```

#### Westalis
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.182.0.1
```

### (D.) Tugas berikutnya adalah memberikan ip pada subnet Forger, Desmond, Blackbell, dan Briar secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

1. Install `apt-get install isc-dhcp-relay -y` pada Ostania, Strix, dan Westalis, `apt-get install isc-dhcp-server` pada WISE
2. Pada Router (Ostania, Strix, dan Westalis) jalankan command berikut
    ```
    net.ipv4.ip_forward=1
    net.ipv4.conf.all.accept_source_route = 1
    ```
3. Lakukan sysctl -p
4. Buka `file /etc/default/isc-dhcp-relay` dan edit server dengan mengarahkan dchp-relay menuju WISE `192.182.0.12` lalu `service isc-dhcp-relay restart` pada Ostania, Strix, dan Westalis
```
echo '
SERVERS="192.182.0.12"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=
' > /etc/default/isc-dhcp-relay
```
5. Pada Jipangu edit file `/etc/default/isc-dhcp-server` dengan menambahkan:
`INTERFACES="eth0"`
6. Pada dhcp-server isikan data pada `/etc/dhcp/dhcpd.conf` di WISE, lalu lakukan `service isc-dhcp-server restart`
```
# Subnet A1
subnet 192.182.0.8 netmask 255.255.255.248 {
}

# Subnet A2
subnet 192.182.0.128 netmask 255.255.255.128 {
    range 192.182.0.130 192.182.0.255;
    option routers 192.182.0.129;
    option broadcast-address 192.182.0.255;

    option domain-name-servers 192.182.0.10;

    default-lease-time 360;
    max-lease-time 7200;
}

# Subnet A3
subnet 192.182.4.0 netmask 255.255.252.0 {
    range 192.182.4.2 192.182.7.255;
    option routers 192.182.4.1;
    option broadcast-address 192.182.7.255;

    option domain-name-servers 192.182.0.10;

    default-lease-time 360;
    max-lease-time 7200;
}

# Subnet A6
subnet 192.182.2.0 netmask 255.255.254.0 {
    range 192.182.2.2 192.182.3.255;
    option routers 192.182.2.1;
    option broadcast-address 192.182.3.255;

    option domain-name-servers 192.182.0.10;

    default-lease-time 360;
    max-lease-time 7200;
}

# Subnet A7
subnet 192.182.1.0 netmask 255.255.255.0 {
    range 192.182.1.2 192.182.1.255;
    option routers 192.182.1.1;
    option broadcast-address 192.182.1.255;

    option domain-name-servers 192.182.0.10;

    default-lease-time 360;
    max-lease-time 7200;
```
7. Lakukan restart di node yang dijadikan ip dhcp