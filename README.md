# Jarkom-Modul-3-F09-2022

## Anggota Kelompok

<table>
    <tr>
        <th>NRP</th>
	<th>Nama</th>
    </tr>
    <tr>
        <td>Muhammad Lintang Panjerino</td>
        <td>5025201045</td>
    </tr>
    <tr>
        <td>Sayid Ziyad Ibrahim Alaydrus</td>
	<td>5025201147</td>
    </tr>
    <tr>
        <td>Wahyu Tri Saputro</td>
	<td>5025201217</td>
    </tr>
<table>

## NO 1 & 2

### Loid bersama Franky berencana membuat peta tersebut dengan kriteria WISE sebagai DNS Server, Westalis sebagai DHCP Server, Berlint sebagai Proxy Server, dan Ostania sebagai DHCP Relay

### **Jawab :**

Pertama kita membuat topologi seperti pada soal :

![NO1](img/no1a.png)

Kemudian, edit network configuration Ostania dengan mengubah script menjadi :

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.33.1.1
	netmask 255.255.255.0

auto eth2
	iface eth2 inet static
	address 10.33.2.1
	netmask 255.255.255.0

auto eth3
	iface eth3 inet static
	address 10.33.3.1
	netmask 255.255.255.0
```

Setelah mengedit network configuration Ostania, selanjutnya tinggal mengedit network configuration node yang lainnya dengan mengubah script menjadi :

WISE	
```
auto eth0
iface eth0 inet static
	address 10.33.2.2
	netmask 255.255.255.0
	gateway 10.33.2.1
```

Berlint	
```
auto eth0
iface eth0 inet static
	address 10.33.2.3
	netmask 255.255.255.0
	gateway 10.33.2.1
```

Westalis	
```
auto eth0
iface eth0 inet static
	address 10.33.2.4
	netmask 255.255.255.0
	gateway 10.33.2.1
```	

Eden	
```
auto eth0
iface eth0 inet static
	address 10.33.3.2
	netmask 255.255.255.0
	gateway 10.33.3.1
```	

NewstonCastle	
```
auto eth0
iface eth0 inet static
	address 10.33.3.3
	netmask 255.255.255.0
	gateway 10.33.3.1
```	

KemonoPark	
```
auto eth0
iface eth0 inet static
	address 10.33.3.4
	netmask 255.255.255.0
	gateway 10.33.3.1
```	

SSS	
```
auto eth0
iface eth0 inet static
	address 10.33.1.2
	netmask 255.255.255.0
	gateway 10.33.1.1
```	

Garden	
```
auto eth0
iface eth0 inet static
	address 10.33.1.3
	netmask 255.255.255.0
	gateway 10.33.1.1
```	
	
Setelah semua node sudah diedit network configurationnya, sekarang kita akan menjadikan WISE sebagai DNS Server dengan cara menginstall bind9.
	
```
apt-get update
apt-get install bind9 -y
```
	
Kemudian bisa kita ping ke google.com untuk mengecek apakah sudah tersambung ke internet atau belum.
	
SS ping google.com WISE
	
Selanjutnya, kita buat Westalis menjadi DHCP Server dengan cara install ISC-DHCP-SERVER.
	
```
apt-get update
apt-get install isc-dhcp-server -y
```
	
Kemudian edit file konfigurasi pada `/etc/default/isc-dhcp-server`. Lalu tambahkan baris `INTERFACE="eth0"` di dalamnya. Kemudian bisa di ping ke google.com
	
SS ping google.com Westalis
	
Selanjutnya adalah menjadikan Berlint sebagai Proxy Server dengan cara menginstall squid.

```
apt-get update
apt-get install squid -y
```
	
Kemudian bisa di ping ke google.com

SS ping google.com Berlint
	
Terakhir adalah menjadikan Ostania sebagai DHCP Relay dengan cara menginstall ISC-DHCP-RELAY.
	
```
apt-get update
apt-get install isc-dhcp-relay -y
```
	
Kemudian edit file konfigurasi pada `/etc/default/isc-dhcp-relay`. Lalu tambahkan baris `10.33.2.4` dan `INTERFACES="eth1 eth2 eth3"` di dalamnya, kemudian restart service `service isc-dhcp-relay restart`.
	
SS konfigurasi dhcp relay
		
	
## NO 3
	
### Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.50 - [prefix IP].1.88 dan [prefix IP].1.120 - [prefix IP].1.155.
	
### **Jawab :**
	
Edit file konfigurasi Westalis pada `/etc/dhcp/dhcpd.conf`. Lalu tambahkan script seperti berikut :
	
```
subnet 10.33.1.0 netmask 255.255.255.0 {
	range 10.33.1.50 10.33.1.88;
	range 10.33.1.120 10.33.1.155;
	option routers 10.33.1.1;
	option broadcast-address 10.33.1.255;
	option domain-name-servers 10.33.2.2;
	default-lease-time 300;
	max-lease-time 6900;
}
```
	
Setelah itu, restart sevice dengan perintah `service isc-dhcp-server restart`. Setelah direstart, cek status apakah dhcp server berjalan atau tidak dengan perintah `service isc-dhcp-server status`	
	
Selanjutnya edit konfigurasi `/etc/network/interfaces` pada SSS dan Garden. Tambahkan baris berikut di dalamnya :

```
auto eth0
iface eth0 inet dhcp
```		

Selanjutnya testing menggunakan perintah `ip a`, jika berhasil maka hasilnya akan seperti berikut :	
	
![NO3](img/no3a.png)
![NO3](img/no3b.png)
	
## NO 4
	
### Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.10 - [prefix IP].3.30 dan [prefix IP].3.60 - [prefix IP].3.85.
	
### **Jawab :**	
	
Kurang lebih sama seperti nomor 3, Edit file konfigurasi Westalis pada `/etc/dhcp/dhcpd.conf`. Lalu tambahkan script seperti berikut :
	
```
subnet 10.33.1.0 netmask 255.255.255.0 {
	range 10.33.3.10 10.33.3.30;
	range 10.33.3.50 10.33.3.85;
	option routers 10.33.3.1;
	option broadcast-address 10.33.3.255;
	option domain-name-servers 10.33.2.2;
	default-lease-time 600;
	max-lease-time 6900;
}
```	
	
Setelah itu, restart sevice dengan perintah `service isc-dhcp-server restart`. Setelah direstart, cek status apakah dhcp server berjalan atau tidak dengan perintah `service isc-dhcp-server status`
	
Selanjutnya edit konfigurasi `/etc/network/interfaces` pada Eden, NewstonCastle, dan KemonoPark. Tambahkan baris berikut di dalamnya :

```
auto eth0
iface eth0 inet dhcp
```		
	
Selanjutnya testing menggunakan perintah `ip a`, jika berhasil maka hasilnya akan seperti berikut :	
	
![NO4](img/no4a.png)
![NO4](img/no4b.png)
![NO4](img/no4c.png)	
	
## NO 8

### SSS, Garden, dan Eden digunakan sebagai client Proxy agar pertukaran informasi dapat terjamin keamanannya, juga untuk mencegah kebocoran data.

### **Jawab :**

#### I. Konfigurasi pada SSS, Garden, dan Eden

Untuk menjadikan SSS, Garden, dan Eden sebagai client Proxy, maka akan dilakukan pengaktifan proxy pada masing-masing client.

```
export http_proxy="http://10.33.2.3:9009"
```

10.33.2.3 adalah IP dari Proxy Server dan 9009 adalah port yang digunakan.

#### II. Testing

Lakukan pengecekan dengan cara mencari apakah sudah ada proxy pada client proxy.

```
env | grep -i proxy
```

![NO8](img/no8a.png)
![NO8](img/no8b.png)
![NO8](img/no8c.png)
