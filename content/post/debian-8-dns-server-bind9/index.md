---
categories:
  - tutorial
comment:
date: 2021-02-19T09:41:53+08:00
description: 
hidden: false
image: thumbnail.jpg
keywords:
  - Konfigurasi DNS Server Bind9 Debian 8
  - Konfigurasi DNS Server Bind9 Debian 8 VirtualBox
  - Cara mengkonfigurasi DNS Server Bind9 Debian 8
  - Cara mengkonfigurasi DNS Server Bind9 Debian 8 VirtualBox
  - Instalasi DNS Server Bind9 Debian 8
  - Instalasi DNS Server Bind9 Debian 8 VirtualBox
  - Cara menginstall DNS Server Bind9 Debian 8
  - Cara menginstall DNS Server di Debian 8 VirtualBox
  - Konfigurasi DNS Server di Debian 8
  - Konfigurasi DNS Server di Debian 8 VirtualBox
  - Cara mengkonfigurasi DNS Server di Debian 8
  - Cara mengkonfigurasi DNS Server di Debian 8 VirtualBox
  - Instalasi DNS Server di Debian 8
  - Instalasi DNS Server di Debian 8 VirtualBox
  - Cara menginstall DNS Server di Debian 8
  - Cara menginstall DNS Server di Debian 8 VirtualBox
math:
slug: debian-8-dns-server-bind9
tags:
  - administrasi sistem jaringan
  - debian 8
  - virtualbox
title: Konfigurasi DNS Server Bind9 Debian 8 VirtualBox
---

{{< youtube id="vfAJNNv4aYU" autoplay="false" >}}

> Sebelum eksekusi, pastikan kalian sudah:
> - [x] [Menginstall Debian 8 di VirtualBox](/p/install-debian-8-virtualbox/)
> - [x] Menclone Debian 8]
> - [x] Memiliki koneksi internet
> - [x] Mengkonfigurasi network pada Debian 8 (Bridged)
> - [x] Login sebagai root

#### 1. Update repository `apt update`

#### 2. Install Bind9 `apt install bind9`

Tekan enter saat ada konfirmasi `Do you want to continue?  [Y/n]`.

#### 3. Pindah ke direktori konfigurasi Bind9 `cd /etc/bind9`

#### 4. Cek IP `ip a s eth0`

![IP saya 192.168.42.205](image001.jpg)

#### 5. Konfigurasi Bind9 (`named.conf.default-zones`)

```
nano named.conf.default-zones
```

Tambahkan konfigurasi ini dibagian paling bawah

```
zone "yasser.local" {
    type master;
    file "/etc/bind/db.yasser.local";
};

zone "42.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/db.192";
};
```

> - Selalu ubah `yasser.local` menjadi nama domain yang ingin kalian gunakan
> - Ubah `42.168.192` menjadi kebalikan dari IP kalian, IP saya `192.168.42.205` maka disana dimasukkan `42.168.192`.

#### 6. Konfigurasi Bind9 (db)

Copy dulu db-nya.

```
cp db.local db.yasser.local
cp db.127 db.192
```

Setelah itu ubah domain-nya.

```
sed -i 's/localhost/yasser.local/g' db.yasser.local
sed -i 's/localhost/yasser.local/g' db.192
```

Lalu edit.

```
nano db.yasser.local
```

![Before](image002.jpg) ![After](image003.jpg)

Ubah `192.168.42.205` menjadi IP kalian.

```
nano db.192
```

![Before](image004.jpg) ![After](image005.jpg)

#### 7. Restart layanan Bind9 `/etc/init.d/bind9 restart`

#### 8. Konfigurasi DNS Server yang digunakan

```
nano /etc/resolve.conf
```

Lalu tambahkan IP kalian dibagian paling atas.

![Before](image006.jpg) ![After](image007.jpg)

#### 9. Ujicoba konfigurasi Bind9

Jalankan perintah dibawah, jika tidak error maka konfigurasi Bind9 sudah benar.

```
dig yasser.local
nslookup yasser.local
ping yasser.local
```

![Contoh dig tidak error](image008.jpg)

![Contoh nslookup tidak error](image009.jpg)

![Contoh ping tidak error](image010.jpg)

Setelah itu ujicoba pada Windows 10. Pergi ke konfigurasi adapter lalu klik kanan pada network yang dibridge pada VirtualBox lalu klik Status.

![Klik Details untuk mengecek DNS Server yang sudah digunakan sebelumnya, liat 'IPv4 DNS Server' setelah itu close](image011.jpg)

DNS Server saya `192.168.42.129`.

![Klik Properties lalu klik dua kali pada (TCP/IPv4)](image012.jpg)

![Klik pada Use the following DNS... lalu isi IP Debian pada kolom yang berada diatas dan isi DNS Server yang tadi pada kolom yang dibawah](image013.jpg)

Setelah itu buka Run lalu isi dengan `ping yasser.local -t`.

![Jika hasilnya seperti diatas berarti DNS Server sudah bekerja dengan baik](image014.jpg)

> - Kalau ada kesalahan tolong beri tahu melalui komentar
> - Kalau kurang jelas atau kurang paham silahkan tanyakan melalui komentar

#### [Thumbnail image source](https://www.zerochan.net/1533595)