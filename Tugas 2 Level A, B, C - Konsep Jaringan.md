# Jawaban Latihan Bab 2 — Model Referensi OSI dan TCP/IP

## Level A — Ingatan dan Pemahaman

### 1. Jelaskan alasan komunikasi jaringan disusun berlapis.
Komunikasi jaringan disusun berlapis agar masalah yang kompleks dapat dibagi menjadi fungsi-fungsi yang lebih kecil dan jelas. Pendekatan ini memberikan modularitas, interoperabilitas, evolusi teknologi yang lebih mudah, pengujian dan penelusuran gangguan yang lebih terarah, serta penggunaan kembali protokol.

### 2. Bedakan layanan, antarmuka, dan protokol.
- **Layanan**: kemampuan yang diberikan suatu lapisan kepada lapisan di atasnya.
- **Antarmuka**: cara lapisan di atas mengakses layanan lapisan di bawah pada sistem yang sama.
- **Protokol**: aturan komunikasi antara entitas sejawat pada lapisan yang sama di sistem berbeda.

### 3. Sebutkan tujuh lapisan OSI dari bawah ke atas beserta fungsi utamanya.
1. **Physical** — membawa bit melalui media dalam bentuk sinyal.
2. **Data Link** — mengatur frame, alamat lokal, akses media, dan deteksi kesalahan.
3. **Network** — menyediakan pengalamatan logis dan pengantaran paket antarjaringan.
4. **Transport** — menyediakan komunikasi logis antaraplikasi, termasuk multiplexing dan demultiplexing.
5. **Session** — mengelola pembentukan, pemeliharaan, sinkronisasi, dan pengakhiran sesi.
6. **Presentation** — menangani representasi data, serialisasi, encoding, kompresi, dan transformasi kriptografis.
7. **Application** — menyediakan protokol dan layanan jaringan yang digunakan proses aplikasi.

### 4. Sebutkan empat lapisan model TCP/IP.
1. Application
2. Transport
3. Internet
4. Network Access/Link

### 5. Mengapa model TCP/IP kadang disajikan sebagai lima lapisan?
Karena model lima lapisan memisahkan **Network Access/Link** menjadi **Data Link** dan **Physical**. Pemisahan ini membantu pembelajaran karena framing dan switching dapat dibedakan dari karakteristik sinyal dan media.

### 6. Apa perbedaan frame, IP packet, TCP segment, dan UDP datagram?
- **Frame**: PDU pada Data Link, digunakan untuk pengiriman pada tautan lokal.
- **IP packet/datagram**: PDU pada Internet layer, digunakan untuk pengantaran antarjaringan.
- **TCP segment**: PDU TCP yang membawa aliran byte secara andal.
- **UDP datagram**: PDU UDP yang membawa datagram tanpa keandalan bawaan seperti TCP.

### 7. Definisikan header, trailer, dan payload.
- **Header**: informasi kendali yang ditempatkan sebelum payload.
- **Trailer**: informasi kendali yang ditempatkan setelah payload.
- **Payload**: data yang dibawa oleh suatu PDU, biasanya berupa PDU dari lapisan di atas.

### 8. Jelaskan enkapsulasi dan dekapsulasi.
**Enkapsulasi** adalah proses penambahan informasi kendali ketika data bergerak dari lapisan atas ke lapisan bawah pada pengirim.  
**Dekapsulasi** adalah proses pemeriksaan dan pelepasan informasi kendali ketika data bergerak dari lapisan bawah menuju aplikasi pada penerima.

### 9. Apa fungsi multiplexing dan demultiplexing?
**Multiplexing** memungkinkan banyak aplikasi atau aliran menggunakan layanan transport dan jaringan yang sama. **Demultiplexing** menggunakan pengenal seperti nomor port untuk menentukan aplikasi atau proses yang harus menerima data.

### 10. Mengapa OSI tidak boleh dianggap sebagai spesifikasi implementasi?
Karena OSI merupakan **model referensi** yang menyediakan kerangka untuk standardisasi dan analisis komunikasi. Model ini tidak menentukan bahwa setiap implementasi harus diwujudkan persis sebagai tujuh komponen perangkat lunak.

---

## Level B — Penerapan dan Analisis

### 11. Petakan HTTP, TLS, TCP, UDP, QUIC, IPv6, ICMP, Ethernet, Wi-Fi, dan DNS ke model TCP/IP. Tandai protokol yang pemetaannya memerlukan penjelasan.
| Protokol/Teknologi | Lapisan TCP/IP | Keterangan |
|---|---|---|
| HTTP | Application | Protokol layanan web |
| TLS | Application / di antara Application dan Transport | Pemetaan praktis bergantung sudut analisis |
| TCP | Transport | Menyediakan transport berorientasi koneksi dan andal |
| UDP | Transport | Menyediakan layanan datagram sederhana |
| QUIC | Transport secara fungsional | Menggunakan UDP sebagai pembawa, tetapi menyediakan fungsi transport |
| IPv6 | Internet | Pengalamatan dan pengantaran datagram |
| ICMP | Internet | Mendukung pelaporan kesalahan dan diagnostik |
| Ethernet | Network Access/Link | Mencakup fungsi Data Link dan Physical |
| Wi-Fi | Network Access/Link | Mencakup akses media radio dan fungsi link |
| DNS | Application | Layanan penamaan; dapat menggunakan beberapa transport |

QUIC dan TLS memerlukan penjelasan karena batas lapisan nyata tidak selalu sama dengan pembungkus protokolnya.

### 12. Gambarkan enkapsulasi permintaan DNS melalui UDP, IPv4, dan Ethernet. Sebutkan pengenal yang digunakan pada setiap batas.
Urutan enkapsulasi:

```text
DNS message
    ↓
UDP datagram
    ↓
IPv4 packet/datagram
    ↓
Ethernet frame
    ↓
Bits/symbols
```

Pengenal pada setiap batas:
- **DNS**: nama domain dan informasi layanan/permintaan.
- **UDP**: nomor port sumber dan tujuan.
- **IPv4**: alamat IP sumber dan tujuan serta field Protocol.
- **Ethernet**: alamat MAC sumber dan tujuan serta EtherType.
- **Physical**: karakteristik sinyal dan antarmuka.

### 13. Ulangi soal sebelumnya untuk HTTP/3 melalui QUIC. Jelaskan mengapa QUIC tetap dapat dianggap transport meskipun menggunakan UDP.
Urutannya:

```text
HTTP/3 message
    ↓
QUIC
    ↓
UDP datagram
    ↓
IP packet
    ↓
Ethernet/Wi-Fi frame
    ↓
Bits/symbols
```

QUIC tetap dianggap sebagai protokol **transport secara fungsional** karena menyediakan layanan seperti aliran yang dikendalikan, pembentukan koneksi, kontrol kemacetan, multiplexing, dan integrasi TLS. UDP hanya menjadi pembawa di bawah QUIC.

### 14. Dua host berada pada subnet berbeda. Jelaskan header mana yang berubah dan tetap ketika paket melewati satu router, dengan mengabaikan NAT.
Pada router:
- Header/trailer **Layer 2** dari tautan masuk dilepas.
- Router membuat **frame Layer 2 baru** untuk tautan keluar.
- Alamat **MAC sumber dan tujuan berubah** sesuai tautan berikutnya.
- Alamat **IP sumber dan tujuan umumnya tetap**.
- **TTL IPv4 atau Hop Limit IPv6 berkurang**.
- Header transport seperti TCP biasanya tidak diubah oleh router biasa.

### 15. Jelaskan perubahan analisis apabila router tersebut juga melakukan NAT/PAT.
Jika router melakukan NAT/PAT, alamat IP dapat diubah dan nomor port juga dapat diterjemahkan. Karena itu, asumsi bahwa alamat IP dan port selalu tetap sepanjang jalur tidak lagi berlaku. Analisis harus membandingkan paket sebelum dan sesudah perangkat NAT.

### 16. Sebuah capture menunjukkan checksum TCP salah pada paket keluar, tetapi tidak ada gangguan komunikasi. Ajukan hipotesis yang berkaitan dengan NIC offload.
Kemungkinan penyebabnya adalah **checksum offload** pada NIC. Sistem operasi dapat menyerahkan perhitungan checksum kepada kartu jaringan. Akibatnya, capture yang diambil sebelum paket benar-benar dikirim melalui media dapat menunjukkan checksum yang tampak salah, walaupun NIC mengisinya dengan benar saat transmisi.

### 17. Pengguna dapat membuka portal dengan alamat IP, tetapi tidak dengan nama. Gunakan model lapisan untuk menyusun diagnosis.
Diagnosis dapat dilakukan dari atas ke bawah:
1. Periksa konfigurasi dan resolver DNS.
2. Periksa apakah kueri DNS dikirim dan mendapat respons.
3. Periksa cache DNS.
4. Pastikan nama domain menghasilkan alamat yang benar.
5. Bandingkan hasil DNS dengan alamat IP yang dapat diakses.
6. Jika akses menggunakan IP berhasil tetapi nama gagal, DNS menjadi kandidat utama masalah.

### 18. Ping ke server berhasil, tetapi HTTPS gagal. Susun sedikitnya enam hipotesis pada lapisan Transport hingga Application.
Hipotesis:
1. Port TCP HTTPS tertutup.
2. Firewall memblokir koneksi TCP.
3. Service HTTPS pada server tidak berjalan.
4. Handshake TCP gagal atau mengalami reset.
5. Handshake TLS gagal.
6. Sertifikat TLS tidak valid atau tidak sesuai nama.
7. Waktu sistem salah sehingga validasi sertifikat gagal.
8. Konfigurasi server atau virtual host HTTPS bermasalah.
9. Autentikasi atau sesi aplikasi gagal.
10. Aplikasi web/server mengalami gangguan.

Ping berhasil hanya memberikan bukti terbatas tentang jalur IP/ICMP dan tidak membuktikan HTTPS sehat.

### 19. Bandingkan sesi aplikasi dengan koneksi TCP. Berikan contoh ketika sesi bertahan setelah koneksi berubah.
Koneksi TCP merupakan hubungan transport antara endpoint. Sesi aplikasi merupakan konteks komunikasi pada tingkat aplikasi dan dapat memiliki state sendiri.

Contohnya, pengguna sudah login ke portal melalui HTTPS. Koneksi TCP dapat berakhir, tetapi sesi login tetap berlaku melalui cookie atau token ketika browser membuat koneksi baru.

### 20. Jelaskan mengapa enkripsi tidak dapat selalu ditempatkan secara mutlak pada Presentation layer.
Enkripsi dapat diterapkan pada berbagai tingkat. Contohnya:
- **MACsec** melindungi komunikasi pada Layer 2.
- **IPsec** bekerja pada fungsi Internet layer.
- **TLS** berada di antara aplikasi dan transport dalam pemetaan tradisional.
- Enkripsi aplikasi dapat dilakukan sebelum data diberikan ke jaringan.

Karena itu, posisi enkripsi bergantung pada aset yang dilindungi, titik terminasi, cakupan kepercayaan, dan ancaman yang dihadapi.

---

## Level C — Evaluasi dan Sintesis

### 21. Evaluasi pernyataan: “Model OSI tidak lagi relevan karena Internet menggunakan TCP/IP.”
Pernyataan tersebut terlalu sederhana. TCP/IP memang merupakan arsitektur dan keluarga protokol yang digunakan secara luas pada Internet, sedangkan OSI merupakan model referensi.

OSI tetap relevan sebagai kerangka konseptual untuk memahami fungsi komunikasi, membedakan lapisan, menganalisis gangguan, dan menjelaskan protokol. Model OSI juga membantu pembelajaran karena memisahkan Physical, Data Link, Network, Transport, Session, Presentation, dan Application.

TCP/IP lebih dekat dengan implementasi Internet nyata, tetapi tidak berarti OSI menjadi tidak berguna. Keduanya memiliki tujuan berbeda dan dapat digunakan bersama. OSI membantu menjawab **fungsi apa yang terjadi**, sedangkan TCP/IP membantu menghubungkan konsep tersebut dengan protokol Internet nyata.

### 22. Analisis keuntungan dan kerugian strict layering. Kapan cross-layer information dapat membantu dan kapan ia merusak modularitas?
**Keuntungan strict layering:**
- Modul lebih mudah dipahami.
- Perubahan pada satu lapisan tidak selalu memengaruhi lapisan lain.
- Interoperabilitas lebih mudah dicapai.
- Pengujian dan diagnosis lebih terarah.

**Kerugian:**
- Dapat menambah overhead.
- Informasi penting dapat tersembunyi dari lapisan lain.
- Fungsi tertentu dapat terduplikasi.
- Optimasi yang sebenarnya berguna dapat terhambat.

**Cross-layer information** membantu ketika informasi dari lapisan lain diperlukan untuk optimasi, misalnya aplikasi real-time membutuhkan informasi kapasitas, loss, atau kondisi jaringan.

Namun, cross-layer dapat merusak modularitas apabila terlalu banyak ketergantungan antar-lapisan. Perubahan satu lapisan kemudian memaksa perubahan lapisan lain dan membuat sistem lebih sulit dipelihara.

### 23. Buat prosedur penelusuran gangguan untuk kasus video konferensi yang tersendat hanya pada Wi-Fi kampus saat jam sibuk. Hubungkan bukti pada sedikitnya empat lapisan.
Prosedur:

1. **Physical**
   - Periksa kekuatan sinyal Wi-Fi.
   - Periksa interferensi radio dan kualitas kanal.
   - Periksa apakah masalah terjadi pada lokasi tertentu.

2. **Data Link**
   - Periksa asosiasi access point.
   - Periksa retransmisi/error frame.
   - Periksa kepadatan pengguna dan penggunaan kanal.
   - Periksa VLAN dan kualitas koneksi wireless.

3. **Network**
   - Periksa packet loss, latency, routing, dan gateway.
   - Bandingkan jalur saat jam sibuk dan tidak sibuk.

4. **Transport**
   - Periksa loss, jitter, retransmisi, dan perilaku TCP/UDP/QUIC.
   - Pastikan port dan protokol konferensi tidak diblokir.

5. **Application**
   - Periksa kualitas video/audio, codec, bitrate, dan statistik aplikasi.
   - Periksa apakah server konferensi mengalami beban tinggi.

Kesimpulan harus berdasarkan bukti. Karena masalah hanya muncul saat jam sibuk dan melalui Wi-Fi, kepadatan kanal, antrean, loss, dan kapasitas merupakan hipotesis penting.

### 24. Rancang skenario laboratorium perekaman paket yang menunjukkan Ethernet, IP, TCP atau UDP, TLS, dan protokol aplikasi tanpa mengumpulkan data sensitif.
Skenario:
1. Gunakan komputer laboratorium dan jaringan yang memiliki izin.
2. Jalankan Wireshark pada interface Ethernet.
3. Akses server laboratorium yang memang disediakan untuk praktikum.
4. Gunakan layanan HTTPS sederhana yang tidak memerlukan data pribadi.
5. Lakukan satu koneksi TCP dan satu kueri UDP yang aman, misalnya DNS ke resolver laboratorium.
6. Rekam hanya lalu lintas selama waktu praktikum.
7. Filter paket berdasarkan host laboratorium.
8. Identifikasi Ethernet, IP, TCP/UDP, TLS, dan protokol aplikasi.
9. Jangan memasukkan username, password, token, cookie, atau data pribadi.
10. Hapus capture setelah praktikum atau simpan hanya data yang diperlukan.

### 25. Sebuah organisasi menggunakan VXLAN di atas UDP dan IPsec tunnel. Gambarkan kemungkinan urutan header dan jelaskan risiko MTU.
Salah satu urutan konseptualnya:

```text
Outer Ethernet
  → Outer IP
    → IPsec header/trailer
      → UDP
        → VXLAN
          → Inner Ethernet
            → Inner IP
              → TCP/UDP
                → Data aplikasi
```

VXLAN menambahkan enkapsulasi UDP/IP dan IPsec dapat menambahkan header/trailer keamanan. Akibatnya ukuran paket bertambah.

Risiko utamanya adalah **MTU menjadi lebih kecil untuk payload internal**. Jika ukuran paket melebihi kemampuan jalur, dapat terjadi fragmentasi, drop, atau Path MTU black hole. Karena itu, MTU harus diperhitungkan pada desain overlay dan underlay.

### 26. Bandingkan perlindungan MACsec, IPsec, TLS, dan enkripsi end-to-end aplikasi dari sisi cakupan kepercayaan dan titik terminasi.
| Mekanisme | Cakupan utama | Titik terminasi |
|---|---|---|
| MACsec | Perlindungan pada tautan Layer 2 | Endpoint/port pada link yang dilindungi |
| IPsec | Perlindungan lalu lintas IP | Host atau gateway IPsec |
| TLS | Perlindungan komunikasi aplikasi selama sesi TLS | Endpoint TLS, misalnya client dan server/proxy |
| Enkripsi end-to-end aplikasi | Perlindungan data dari aplikasi pengirim sampai aplikasi penerima | Aplikasi pengirim dan aplikasi penerima |

Semakin dekat enkripsi diterapkan ke aplikasi dan endpoint akhir, semakin kecil ketergantungannya pada kepercayaan terhadap perangkat perantara. Sebaliknya, perlindungan link seperti MACsec hanya melindungi bagian tertentu dari jalur.

### 27. Jelaskan bagaimana firewall, proxy, dan load balancer menantang anggapan bahwa setiap perangkat hanya membaca header lapisannya.
Perangkat modern dapat memproses beberapa lapisan sekaligus:
- **Firewall** dapat memeriksa informasi jaringan, transport, dan dalam beberapa kasus protokol aplikasi.
- **Proxy** mengakhiri komunikasi aplikasi kemudian membuat komunikasi baru, sehingga tidak sekadar meneruskan paket.
- **Load balancer** dapat bekerja pada transport maupun application, termasuk mengakhiri TLS atau HTTP.

Karena itu, pemetaan perangkat ke satu layer hanya menunjukkan fungsi dominannya, bukan batas mutlak kemampuan perangkat.

### 28. Gunakan prinsip end-to-end untuk mengevaluasi penempatan fungsi pemeriksaan integritas berkas pada router, transport, atau aplikasi.
Pemeriksaan integritas berkas paling tepat dijamin pada **aplikasi/endpoints** karena hanya endpoint yang mengetahui apakah keseluruhan berkas yang diterima benar-benar identik dengan yang dimaksud pengirim.

Router dapat membantu pemeriksaan pada bagian tertentu, tetapi tidak memiliki pengetahuan lengkap mengenai tujuan akhir berkas. Transport seperti TCP menyediakan pemeriksaan dan keandalan aliran, tetapi tujuan TCP bukan membuktikan integritas semantik seluruh berkas aplikasi.

Dengan prinsip end-to-end, pemeriksaan pada aplikasi tetap diperlukan meskipun router dan transport memiliki mekanisme integritas masing-masing.

### 29. Analisis potensi retry storm ketika aplikasi, service mesh, dan client sama-sama melakukan pengulangan. Jelaskan mengapa masalah ini bersifat lintas lapisan.
Retry storm terjadi ketika beberapa komponen melakukan retry terhadap permintaan yang sama secara bersamaan.

Contoh:
```text
Client
  ↓ retry
Service Mesh
  ↓ retry
Application
  ↓ retry
Server
```

Jika setiap lapisan melakukan retry tanpa koordinasi, satu kegagalan dapat menghasilkan banyak permintaan tambahan. Beban server meningkat dan kondisi kegagalan semakin parah.

Masalah ini bersifat lintas lapisan karena retry dapat dilakukan oleh client/application, proxy atau service mesh, serta mekanisme transport atau jaringan. Solusinya membutuhkan koordinasi timeout, jumlah retry, backoff, jitter, dan batas keseluruhan.

### 30. Susun argumen apakah materi jaringan pemula sebaiknya memakai model OSI tujuh lapisan, TCP/IP empat lapisan, atau model lima lapisan. Nyatakan tujuan pembelajaran, manfaat, dan keterbatasan pilihan Anda.
Untuk materi jaringan pemula, **model OSI tujuh lapisan sebaiknya digunakan sebagai kerangka utama**, kemudian dikaitkan dengan model TCP/IP dan model lima lapisan.

**Tujuan pembelajaran:**
- Memahami pembagian fungsi jaringan.
- Mengenali hubungan antar-lapisan.
- Memahami PDU, enkapsulasi, dan dekapsulasi.
- Mempermudah penelusuran gangguan.

**Manfaat OSI tujuh lapisan:**
- Pemisahan fungsi paling rinci.
- Mudah digunakan sebagai bahasa bersama saat menjelaskan gangguan.
- Membantu mahasiswa memahami perbedaan Physical, Data Link, Network, Transport, Session, Presentation, dan Application.

**Keterbatasan:**
- Tidak semua protokol Internet cocok dipetakan secara satu banding satu.
- Model dapat membuat mahasiswa menganggap setiap perangkat hanya bekerja pada satu lapisan.
- Beberapa fungsi modern seperti QUIC, TLS, tunnel, dan service mesh melintasi batas lapisan.

**Model TCP/IP empat lapisan** lebih dekat dengan arsitektur Internet nyata, tetapi beberapa fungsi OSI digabung. **Model lima lapisan** menjadi kompromi yang baik untuk pembelajaran karena Physical dan Data Link dipisahkan.

Jadi, pendekatan terbaik adalah menggunakan OSI untuk memahami konsep secara rinci, lalu menggunakan model lima lapisan dan TCP/IP untuk menghubungkan konsep tersebut dengan implementasi Internet nyata.
