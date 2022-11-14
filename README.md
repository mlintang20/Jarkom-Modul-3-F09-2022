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

SS Topologi

Kemudian, edit network configuration Ostania dengan mengubah script menjadi :

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.175.1.1
	netmask 255.255.255.0

auto eth2
	iface eth2 inet static
	address 192.175.2.1
	netmask 255.255.255.0

auto eth3
	iface eth3 inet static
	address 192.175.3.1
	netmask 255.255.255.0
```

Setelah mengedit network configuration Ostania, selanjutnya tinggal mengedit network configuration node sisanya dengan mengubah script menjadi :

```
auto eth0
iface eth0 inet static
	address 192.175.1.3
	netmask 255.255.255.0
	gateway 192.175.1.1
```

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
