---
categories:
  - tutorial
comment:
date: 2021-02-11T20:48:21+08:00
description: Konfigurasi Mail Server di Debian 8 dengan menggunakan SquirrelMail dan Dovecot
hidden: false
image: 
math:
slug: "debian-8-mail-server-squirrelmail-dan-dovecot"
tags:
  - ASJ
  - deb8
  - vbox
title: "Menginstall Mail Server Squirrelmail Dan Dovecot di VirtualBox"
---

{{< youtube id="rTHNtSHwUxg" autoplay="false" title="Versi Video" >}}

> Sebelum eksekusi, pastikan kalian sudah:
> - [x] [Menginstall Debian 8 di VirtualBox](/p/install-debian-8-virtualbox/)
> - [x] Menclone Debian 8]
> - [x] Memiliki koneksi internet
> - [x] Mengkonfigurasi network pada Debian 8 (Bridged)
> - [x] Login sebagai root

#### 1. Edit `/etc/apt/sources.list`

```
nano /etc/apt/sources.list
```

Ubah seperti dibawah

![Before](image001.jpg) ![After](image002.jpg)

#### 2. Update repository `apt update`
#### 3. Install software yang diperlukan

```
apt install postfix squirrelmail dovecot-{imap,pop3}d
```

Tekan enter saat ada konfirmasi `Do you want to continue?  [Y/n]`. Jika disuruh masukkan DVD Debian 8, maka masukkan dengan cara klik kanan pada icon kaset yang berada dikanan bawah VirtualBox.

![Klik kanan pada ikon kaset](image003.jpg) ![Pilih DVD Debian 8](image004.jpg)

Pada prekonfigurasi paket cukup tekan enter saja, tidak usah diubah-ubah.

![Klik enter](image005.jpg) ![Klik enter](image006.jpg)

#### 4. Tambahkan `home_mailbox = Maildir/` pada `/etc/postfix/main.cf`

```bash
echo "home_mailbox = Maildir/" >> /etc/postfix/main.cf
```

#### 5. Konfigurasi ulang postfix `dpkg-reconfigure postfix`

![1](image007.jpg) ![2](image008.jpg)

![3](image009.jpg) ![4](image010.jpg)

![5](image011.jpg) ![6](image012.jpg)

![7](image013.jpg) ![8](image014.jpg)

![9](image015.jpg) ![10](image016.jpg)

Ket: Hanya nomor 7 dan 10 yang perlu diubah, yang lain langsung tekan enter saja.

#### 6. Edit `/etc/dovecot/conf.d/10-mail.conf`

```
nano /etc/dovecot/conf.d/10-mail.conf
```

Ubah seperti dibawah.

![Before](image017.jpg) ![After](image018.jpg)

#### 7. Tambahkan `Include /etc/squirrelmail/apache.conf` pada `/etc/apache2/apache2.conf`

```bash
echo "Include /etc/squirrelmail/apache.conf" >> /etc/apache2/apache2.conf
```

#### 8. Edit `/etc/squirrelmail/apache.conf`

```
nano /etc/squirrelmail/apache.conf
```

Ubah seperti dibawah.

![Before](image019.jpg) ![After](image020.jpg)

#### 9. Tambah dua user baru

```
adduser m1
```

Ikuti intruksi-nya (Biodata bisa dibiarkan kosong), lakukan hal yang sama pada user kedua

```
adduser m2
```

#### 10. Restart layanan

```bash
for i in apache2 postfix dovecot; do /etc/init.d/$i restart; done
```

#### 11. Cek IP `ip a s eth0`

![IP saya 192.168.42.3](image021.jpg)

#### 12. Ujicoba

![1 Buka browser lalu masukkan IP tadi ditambah dengan /mail dibelakangnya](image022.jpg)

![2 Login dengan user m1](image023.jpg) ![3 Klik Compose](image024.jpg)

![4 Isi seperti diatas](image025.jpg) ![5 Klik Sign Out](image026.jpg)

![6 Login dengan user m2](image027.jpg) ![7 Jika mendapat mail maka konfigurasi sudah benar](image028.jpg)

Jika tidak mendapat mail... Silahkan mengulang dari awal.

> - Kalau ada kesalahan tolong beri tahu melalui komentar
> - Kalau kurang jelas atau kurang paham silahkan tanyakan melalui komentar
