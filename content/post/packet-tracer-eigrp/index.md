---
categories:
  - tugas
  - tutorial
comment:
date: 2021-02-18T16:28:14+08:00
description: 
hidden: false
image: thumbnail.jpg
keywords:
  - Routing EIGRP
  - Konfigurasi Routing EIGRP
  - Konfigurasi Routing EIGRP di Cisco Packet Tracer
  - Cara Konfigurasi Routing EIGRP
  - Cara Konfigurasi Routing EIGRP di Cisco Packet Tracer
  - Langkah-langkah Konfigurasi Routing EIGRP
  - Langkah-langkah Konfigurasi Routing EIGRP di Cisco Packet Tracer
math:
slug: packet-tracer-eigrp
tags:
  - administrasi infrastruktur jaringan
  - cisco packet tracer
title: Konfigurasi Routing EIGRP di Cisco Packet Tracer
---

{{< youtube id="-vnrnOuYroI" autoplay="false" title="Versi Video" >}}

#### 1. Masukkan 3 buah router

![Router yang dipakai adalah jenis 1841](image001.jpg)

#### 2. Tambahkan module HWIC-2T pada tiap router

![1 Klik dua kali pada router](image002.jpg)

![2 Klik 'HWIC-2T' pada daftar module](image003.jpg)

![3 Matikan router](image004.jpg)

![4 Klik tahan pada module yang ada dibawah](image005.jpg)

![5 Geser ke kotak kosong yang berada di kanan](image006.jpg)

![6 Nyalakan router](image007.jpg)

Lakukan hal yang sama pada 2 router lainnya.

#### 3. Hubungkan semua router

Kabel yang digunakan adalah kabel 'Serial DCE', urutan menghubungkannya:

| No  | Port yang dihubungkan                            |
| --- | ------------------------------------------------ |
| 1   | Serial 0/0/0 Router0 dengan Serial 0/0/0 Router1 |
| 2   | Serial 0/0/1 Router1 dengan Serial 0/0/0 Router2 |
| 3   | Serial 0/0/1 Router2 dengan Serial 0/0/1 Router0 |

![](image008.jpg)

#### 4. Masukkan 1 laptop disamping tiap router

![](image009.jpg)

#### 5. Hubungkan laptop dengan router

Kabel yang digunakan adalah kabel 'Copper Cross-Over', port yang dihubungkan adalah 'FastEthernet 0/0' pada router dengan 'FastEthernet0' pada laptop.

![](image010.jpg)

#### 6. Beri keterangan Network pada tiap kabel

![Klik pada icon nota](image011.jpg) ![Beri keterangan seperti ini](image012.jpg)

#### 7. Konfigurasi Router0

![1 Klik dua kali pada Router0](image013.jpg)

![2 Klik tab config lalu ubah Hostname menjadi Router0](image014.jpg)

![3 Klik pada FastEthernet0/0 lalu ubah seperti diatas](image015.jpg)

![4 Klik pada Serial0/0/0 lalu ubah seperti diatas](image016.jpg)

![5 Klik pada Serial0/0/1 lalu ubah seperti diatas](image017.jpg)

![6 Klik tab CLI lalu ketik 'exit'](image018.jpg)

![7 Ketik 'ip dhcp exclude 192.168.1.1'](image019.jpg)

![8 Ketik 'ip dhcp pool local'](image020.jpg)

![9 Ketik 'net 192.168.1.0 255.255.255.252'](image021.jpg)

![10 Ketik 'def 192.168.1.1](image022.jpg)

#### 8. Ujicoba konfigurasi Router0

![1 Klik dua kali pada Laptop yang berada didekat Router0](image023.jpg)

![2 Klik pada tab Desktop > IP Configuration lalu klik 'DHCP' lalu tunggu sebentar, jika hasilnya seperti diatas maka konfigurasinya sudah benar](image024.jpg)

![3 Klik pada tab Desktop > Command Prompt lalu ketik 'ping 192.168.1.1', jika hasilnya seperti diatas maka laptop sudah dapat terhubung dengan Router0](image025.jpg)

#### 9. Konfigurasi router lainnya

Konfigurasi router lainnya kurang lebih sama saja caranya, hanya berbeda pada data yang diubah. Berikut adalah perbandingannya: 

| Jenis                                             | Router0     | Router1     | Router2     |
| ------------------------------------------------- | ----------- | ----------- | ----------- |
| [Hostname](image014.jpg)                          | Router0     | Router1     | Router2     |
| [FastEthernet0/0 - IPv4 Address](image015.jpg)    | 192.168.1.1 | 192.168.2.1 | 192.168.3.1 |
| [Serial 0/0/0 - IPv4 Address](image016.jpg)       | 1.1.1.1     | 1.1.1.2     | 2.2.2.2     |
| [Serial 0/0/1 - IPv4 Address](image017.jpg)       | 3.3.3.1     | 2.2.2.1     | 3.3.3.2     |
| ['ip dhcp exclude 192.168.x.1'](image019.jpg)     | 192.168.1.1 | 192.168.2.1 | 192.168.3.1 |
| ['net 192.168.x.0 255.255.255.252'](image021.jpg) | 192.168.1.0 | 192.168.2.0 | 192.168.3.0 |
| ['def 192.168.x.1'](image022.jpg)                 | 192.168.1.1 | 192.168.2.1 | 192.168.3.1 |

Untuk ujicoba-nya sama saja dengan ujicoba konfigurasi Router0, kalian pasti bisa berimprovisasi.

#### 10. Ujicoba hubungan router

![1 Klik dua kali pada Router2](image026.jpg)

![2 Ketik 'exit'](image027.jpg)

![3 Ketik 'ping 1.1.1.1' untuk mengecek hubungan dengan Router0](image028.jpg)

![4 Ketik 'ping 2.2.2.1' untuk mengecek hubungan dengan Router1](image029.jpg)

Jika hasilnya seperti pada gambar maka router sudah terhubung dengan baik.

#### 11. Konfigurasi routing EIGRP pada tiap router

Untuk menkonfigurasi routing EIGRP, klik dua kali pada router yang ingin dikonfigurasi lalu pada tab CLI...

Sebagai contoh saya mengkonfigurasi Router0.

![1 Ketik 'route eigrp 100'](image030.jpg)

![2 Ketik 'no auto-sum'](image031.jpg)

![3 Ketik 'net {network}'](image032.jpg)

> Network yang dimaksud pada tahap ke-3 adalah network yang terhubung dengan router.
> 
> - Router0: 192.168.1.0, 1.1.1.0, 3.3.3.0
> - Router1: 192.168.2.0, 1.1.1.0, 2.2.2.0
> - Router2: 192.168.3.0, 2.2.2.0, 3.3.3.0
> 
> Pada contoh diatas saya mengetik-nya 3 kali, `net 192.168.1.0` lalu `net 1.1.1.0` lalu yang terakhir `net 3.3.3.0`, lakukan hal yang sama pada 2 router lainnya.
> 
> Untuk Router2 karena tadi dipakai untuk mengetes hubungan router, ketik `conf t` terlebih dahulu untuk masuk ke mode konfigurasi sebelum mengkonfigurasi routing EIGRP.

#### 12. Cek daftar route

Klik dua kali pada router mana saja lalu ketik `exit` jika masih dalam mode konfigurasi, setelah itu.

![Ketik 'show ip route'](image033.jpg)

Jika hasilnya seperti diatas maka konfigurasi routing EIGRP sudah benar.

#### 13. Ujicoba konfigurasi EIGRP

Klik dua kali pada laptop yang berada di dekat Router1 lalu.

![1 Klik pada tab Desktop > Command Prompt](image034.jpg)

![2 Ketik 'ping 192.168.1.2' untuk mengecek hubungan dengan laptop yang berada di dekat Router0](image035.jpg)

![3 Ketik 'tracert 192.168.1.2' untuk mengecek rute yang digunakan](image036.jpg)

![4 Hapus kabel yang menghubungkan Router0 dengan Router1](image037.jpg)

![5 Ketik 'tracert 192.168.1.2' lagi untuk mengecek rute yang digunakan](image038.jpg)

#### [Thumbnail image source](https://www.zerochan.net/1533595)