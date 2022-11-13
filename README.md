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
