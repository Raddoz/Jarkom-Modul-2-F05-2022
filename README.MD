|     Nama    |     NRP    |
| :--------- |:--------    |
|Muhammad Amin | 5025201251 |
|Aiffah Kiysa Waafi | 5025201202 |
|Elthan Ramanda B | 5025201092 |

## 1. Membuat Topologi sesuai gambar dibawah. WISE akan dijadikan sebagai DNS Master, Berlint akan dijadikan DNS Slave, dan Eden akan digunakan sebagai Web Server. Terdapat 2 Client yaitu SSS, dan Garden. Semua node terhubung pada router Ostania, sehingga dapat mengakses internet 
<img src="image\imageTopologiSoal.png">

### Network configuration for node (router) Ostania
<img src="image\ostania.png>

### Network configuration for node WISE
<img src="image\wise.png">

Untuk node yang lain tinggal diganti address dan gateway sesuai dengan eth dari ostania (gateway) dan address juga sesuai dari gatewaynya.

### Hasil Topologi F05
<img src="image\topologiHasil.png">

Untuk mengakses internet, yang pertama kita perlu setup NAT di Ostania
```
echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
sudo sysctl -p
```
kemudian jalankan command berikut
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.31.0.0/16
```
Untuk mengetahui IP DNS dapat dilihat pada file resolv.conf
```
cat /etc/resolv.conf
```

Pada node-node yang lain, agar dapat mengakses internet, jalankan command berikut sesuai IP DNS
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
Kemudian kita sudah dapat melakukan ping ke google
```
ping google.com -c 2
```

### Hasil ping google pada garden
<img src="image\ping_google_garden.png">

### Hasil ping google pada eden
<img src="image\ping_google_eden.png">

### Hasil ping google pada sss
<img src="image\ping_google_sss.png">

### Hasil ping google pada berlint
<img src="image\ping_google_berlint.png">

## 2. Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, bantulah Loid membuat website utama dengan akses wise.yyy.com dengan alias www.wise.yyy.com pada folder wise



## 3. Setelah itu ia juga ingin membuat subdomain eden.wise.yyy.com dengan alias www.eden.wise.yyy.com yang diatur DNS-nya di WISE dan mengarah ke Eden

## 4. Buat juga reverse domain untuk domain utama 

## 5. Agar dapat tetap dihubungi jika server WISE bermasalah, buatlah juga Berlint sebagai DNS Slave untuk domain utama 

## 6. Karena banyak informasi dari Handler, buatlah subdomain yang khusus untuk operation yaitu operation.wise.yyy.com dengan alias www.operation.wise.yyy.com yang didelegasikan dari WISE ke Berlint dengan IP menuju ke Eden dalam folder operation 

## 7. Untuk informasi yang lebih spesifik mengenai Operation Strix, buatlah subdomain melalui Berlint dengan akses strix.operation.wise.yyy.com dengan alias www.strix.operation.wise.yyy.com yang mengarah ke Eden

## 8. Setelah melakukan konfigurasi server, maka dilakukan konfigurasi Webserver. Pertama dengan webserver www.wise.yyy.com. Pertama, Loid membutuhkan webserver dengan DocumentRoot pada /var/www/wise.yyy.com

## 9. Setelah itu, Loid juga membutuhkan agar url www.wise.yyy.com/index.php/home dapat menjadi menjadi www.wise.yyy.com/home