---
categories:
  - Tugas
comment:
date: 2021-02-05T15:24:52+08:00
description: Diagram VoIP serta Proses kerja dalam komponen diagram VoIP
hidden: false
image: sip-trunking-VoIP-phone-system-diagram.jpg
math:
slug: memahami-diagram-rangkaian-operasi-komunikasi-VoIP
tags:
  - teknologi layanan jaringan
title: Memahami Diagram Rangkaian Operasi Komunikasi VoIP
---

- [A. Voice Over Internet Protocol (VoIP)](#a-voice-over-internet-protocol-voip)
  - [Kelebihan VoIP](#kelebihan-voip)
  - [Kekurangan VoIP](#kekurangan-voip)
  - [Kendala dalam VoIP](#kendala-dalam-voip)
  - [Data yang ditransmisikan dalam VoIP](#data-yang-ditransmisikan-dalam-voip)
  - [Proses kerja dalam komponen diagram VoIP](#proses-kerja-dalam-komponen-diagram-voip)
- [Source](#source)

## A. Voice Over Internet Protocol (VoIP)

Perbedaan mendasar antara rangkaian dan metode pengiringan data jaringan telepon analog dan VoIP adalah terletak pada jenis data yang ditransmisikan serta format datanya. Pada jaringan telepon analog, pesawat telepon (di Indonesia melalui Telkom) akan diregistrasikan terlebih dahulu dalam STO (Sentral Telepon Otomatis) yang berperan menyimpan dan mengelola penomoran pesawat telepon yang terhubung dengannya berdasarkan wilayah. Data yang ditransmisikan merupakan data suara dalam bentuk analog yang dikirimkan secara privat dari satu telepon ke telepon lainnya melalui PSTN. 

Adapun VoIP bekerja berdasarkan paket data dalam bentuk sinyal digital yang membawa data suara (voice) menggunakan mekanisme data packet yang diterapkan dalam jaringan berbasis IP (komputer). Meskipun awalnya hanya berupa penggunaan aplikasi softphone sebagai basis perangkat komunikasi, tetapi berkembang dalam bentuk hardware seperti IP phone dan bahkan dapat terhubung dengan jaringan telepon analog. Hebatnya lagi, VoIP tidak hanya dapat mentransmisikan data suara, tetapi juga dapat berupa ﬁle, teks, video, gambar, dan lainnya. Contoh aplikasi VoIP generasi awal adalah Skype. 

![Struktur Jaringan VoIP](struktur-jaringan-VoIP.png)

### Kelebihan VoIP

1. Dengan sistem VoIP, biaya investasi awal membangun komunikasi akan lebih murah jika dibandingkan jaringan analog. 
2. Tidak terkena biaya roaming untuk koneksi jarak jauh, misalnya antar provinsi bahkan tingkat internasional. Selama terkoneksi dengan internet, yang digunakan adalah jalur bandwidth-nya. 
3. Infrastruktur VoIP dapat berjalan pada sistem jaringan analog. Sebagai contoh, sambungan internet yang saat ini bekerja dalam jalur yang sama dengan kabel analog telepon, seperti Telkom yang menyatukan koneksi jalur telepon dengan VoIP. 
4. Kapasitas bandwidth lebih kecil dibandingkan dengan sambungan analog. 
5. Memungkinkan terjadinya integrasi dengan sistem komunikasi analog melalui perangkat PBX gateway. 
6. Mudah untuk diintegrasikan menjadi jaringan berskala besar. Jika bagian-bagian jaringan VoIP disatukan, setiap pengguna di belahan dunia lain dapat saling terhubung. 
7. Penggunaan perangkat tidak hanya terbatas pada perangkat keras berupa pesawat telepon, tetapi dalam bentuk komputer dengan aplikasi yang terinstal di dalamnya. 

### Kekurangan VoIP

1. Kualitas dan kejernihan suara sering menjadi kendala utama. Namun pada perkembangan terakhir, potensi kendala tersebut telah diatasi dengan mengembargokan beberapa teknik kompresi data yang diterapkan pada jenis protokol yang akan dibahas selanjutnya. 
2. Terkadang muncul delay yang menyebabkan komunikasi terputus-putus atau bergema. 
3. Sistem komunikasi dengan memanfaatkan jalur internet terkadang mengalami down, crash, dan lost yang mengakibatkan kegagalan komunikasi. 
4. Untuk membangun jaringan skala besar yang menghubungkan jalur analog dengan VoIP membutuhkan perangkat berspesiﬁkasi tinggi dan kerja sama dengan provider bersangkutan sehingga biaya yang ditimbulkan relatif mahal. 
5. Diperlukan pengaturan kanal atau virtual network untuk memisahkan data suara dan data jaringan agar tidak terjadi stuck. 
6. Integrasi antarsistem jaringan VoIP yang berbeda protokol dan network terkadang akan menimbulkan gangguan dalam jaringan itu sendiri. 

### Kendala dalam VoIP

Kendala yang dialami oleh teknologi VolP pada masa perkembangannya adalah sering terjadinya packet loss yang disebabkan oleh penumpukan data pada jalur internet, meski sekarang sudah diatasi dengan teknologi Signalling System No. 7 atau SS7. Sistem panggilan VoIP memiliki dua tipe komunikasi yang terjadi antara perangkat yang melakukan panggilan atau calling party dan perangkat penerima atau called party, antara lain sebagai berikut. 

1. Aliran informasi pembicaraan, protokol yang bertugas membawa informasi ini adalah RTP atau Real Time Protocol. 
2. Signalling message, yang berperang mengontrol koneksi dan karakteristik aliran media. 

![Signalling Message](signalling-message.png)

### Data yang ditransmisikan dalam VoIP

1. Bagian header

- IP Header

IP Header memiliki fungsi mencatat dan menyimpan setiap informasi routing. Tujuannya agar setiap paket data yang ditransmisikan dapat segera sampai pada tujuan dengan cepat. Kelebihan lain dari komponen IP header adalah dilengkapi dengan tipe layanan yang disebut dengan TOS (Type of Service) yang dapat mentransmisikan paket data tertentu, misalnya data suara yang bersifat no real time. 

- Real-time Transport Protocol (RTP)

Header Real-time Transport Protocol Header bertugas sebagai tanda paket agar dilakukan framing dan segmentasi data real time. Karakteristik RTP mirip dengan UDP, yang bersifatless connection yang tidak mendukung reabilitas paket agar benar-benar sampai pada alamat tujuan. Dalam prosesnya RTP dikontrol dan dikendalikan oleh Real-time Transport Control Protocol (RTCP) untuk menjamin QoS (Quality of Service) dan proses sinkronisasi media stream di antara dua perangkat yang sedang berkomunikasi. 

- User Datagram Protocol (UDP) Header

Karateristik utama dari UDP adalah tidak adanya jaminan bahwa paket akan sampai dengan utuh sampai tujuan dengan baik. Hal ini yang menyebabkan pada beberapa komunikasi, suara yang terputus-putus dan data yang hilang tersebut tidak dapat didengarkan lagi. Oleh karena itu, VoIP sangat sensitif terhadap kondisi delay dan Iatency. 

- Link Header

Ukuran bytes yang disertakan dalam header ini tergantung dari tipe media transmisi yang digunakan

| Media       | Ukuran Link Header | Bit Rate   |
| ----------- | ------------------ | ---------- |
| PPP         | 6 Bytes            | 26, 4 Kbps |
| Ethernet    | 14 Bytes           | 29, 6 Kbps |
| Frame Relay | 4 Bytes            | 26, 5 Kbps |
| ATM         | 5 Bytes            | 42, 4 Kbps |

2. Bagian Payload

Berdasarkan standar Cisco dan Codec (standar G. 723. 1 dengan kapasitas 5, 3 Kbps), besar kapasitas payload voice adalah 20 Byte. 

### Proses kerja dalam komponen diagram VoIP

Prinsip kerja VoIP adalah mengubah suara analog yang didapatkan dari mikrofon pada komputer menjadi paket data digital yang kemudian diteruskan melalui sistem jaringan intranet maupun internet dan diterima oleh tempat tujuan melalui media yang sama. Bisa juga melalui media telepon diteruskan keperangkat VoIP yang disambungkan dan bisa diterima oleh telepon yang dituju. 

Konsep dan Proses Kerja VoIP disetiap Blok

- TCP/IP

TCP/IP(Transfer Control Protocol/Internet Protocol) merupakan sebuah protokol yang digunakan pada jaringan internet. Protokol ini terdiri dari dua bagian besar, yaitu TCP dan IP. 

- Application Layer

Fungsi utama pada layer ini adalah pemindahan file. Perpindahan file dari sebuah sistem ke sistem lainnya yang berbeda memerlukan suatu sistem pengendalian untuk menanggani adanya ketidak kompatibelan sistem yang berbeda–beda. Protokol ini berhubungan dengan aplikasi. 

- TCP (Transmission Control Protocol)

Dalam mentransmisikan data pada layer transport ada dua protokol yang berperan yaitu TCP dan UDP. TCP merupakan protokol yang connection-oriented yang artinya menjaga hubungan komunikasi end to end. Konsep dasar cara kerja TCP adalah mengirim dan menerima seqment–seqment informasi dengan panjang data bervariasi pada suatu datagram internet. TCP menjamin realibilitas hubungan komunikasi karena melakukan perbaikan data yang rusak, hilang, atau kesalahan kirim. Dalam hubungan VoIP, TCP digunakan pada saat signaling untuk menjamin setup suatu call pada sesi signaling. TCP tidak digunakan dalam pengiriman data suara pada VoIP karena pada suatu komunikasi data VoIP penangganan data yang mengalami keterlambatan lebih penting dari penangganan paket yang hilang

- UDP (User Datagram Protocol)

UDP merupakan salah satu protokol utama diatas IP merupakan transport protocol yang lebih sederhana dibandingkan dengan TCP. UDP digunakan untuk situasi yang tidak mementingkan mekanisme realibilitas. UDP pada VoIP digunakan untuk mengirimkan audio streaming yang berlangsung terus meneruslebih mementingkan kecepatan pengiriman data agar tiba ditujuan tanpa memperhatikan adanya paket yang hilang walaupun mencapai 50% dari jumlah paket yang dikirimkan. Karena UDP mampu mengirimkan data streaming dengan cepat. 

- SIP (Session Initiation Protocol)

SIP merupakan signalling protokol pada layer aplikasi yang berguna untuk membangun, memodifikasi, dan menghakhiri suatu sesi multimedia(suara, video, dan text) yang melibatkan satu atau beberapa pengguna. 

## Source

- [Music and IT Make it Perfect - Memahami diagram rangkaian operasi komunikasi VoIP](https://rozkysoftwarekandangan.blogspot.com/2021/02/blog-post.html)
- [Music and IT Make it Perfect - Proses kerja dalam komponen diagram VoIP](https://rozkysoftwarekandangan.blogspot.com/2021/02/proses-kerja-dalam-komponen-diagram-voip.html)
