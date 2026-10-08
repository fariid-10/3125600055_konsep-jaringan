# Tugas 1: Konsep Jaringan Komputer dan Internet

* **Nama:** Muhammad Fariid Maulana
* **NRP:** 3125600055
* **Kelas:** 2 D4 IT B

---

## Jawaban Latihan Bab 1 — Pengantar Jaringan Komputer dan Internet

### Level A — Ingatan dan Pemahaman

#### 1. Jelaskan pengertian jaringan komputer dengan menyebutkan empat unsur pokoknya.
**Jawaban:**
Jaringan komputer adalah sekumpulan perangkat otonom yang saling terhubung melalui media komunikasi untuk bertukar data dan berbagi sumber daya berdasarkan aturan komunikasi. Empat unsur pokoknya adalah:
1. Perangkat akhir (*host*)
2. Media komunikasi
3. Perangkat perantara
4. Protokol

#### 2. Apa yang dimaksud dengan perangkat otonom dalam definisi jaringan?
**Jawaban:**
Perangkat otonom adalah perangkat yang tetap memiliki fungsi, kendali komputasi, sumber daya, dan statusnya sendiri meskipun terhubung ke jaringan.

#### 3. Bedakan data, sinyal, dan paket.
**Jawaban:**
* **Data:** Representasi informasi.
* **Sinyal:** Bentuk fisik yang membawa data melalui media.
* **Paket:** Unit data yang lebih kecil yang dikirim melalui jaringan dan diberi informasi kendali sesuai protokol.

#### 4. Jelaskan perbedaan PAN, LAN, MAN, dan WAN tanpa hanya menggunakan ukuran jarak.
**Jawaban:**
* **PAN:** Berorientasi pada perangkat personal dan ruang sangat terbatas.
* **LAN:** Mencakup area lokal seperti rumah, gedung, atau kampus dengan pengelolaan relatif terpadu.
* **MAN:** Menghubungkan beberapa lokasi dalam kawasan metropolitan.
* **WAN:** Menghubungkan lokasi yang berjauhan dan biasanya melibatkan infrastruktur operator.

*Perbedaannya juga terkait wilayah layanan, teknologi, kepemilikan, dan pola operasi.*

#### 5. Apa perbedaan intranet, ekstranet, dan Internet publik?
**Jawaban:**
* **Intranet:** Jaringan atau layanan internal yang aksesnya dibatasi anggota organisasi.
* **Ekstranet:** Membuka sebagian layanan internal kepada pihak luar yang diberi otorisasi.
* **Internet Publik:** Menyediakan keterhubungan terbuka antarbanyak jaringan.

#### 6. Mengapa Wi-Fi tidak dapat disamakan dengan Internet?
**Jawaban:**
Wi-Fi menyediakan akses lokal nirkabel, sedangkan Internet adalah interkoneksi global berbagai jaringan. Perangkat dapat terhubung ke Wi-Fi tetapi belum tentu memiliki jalur ke Internet.

#### 7. Jelaskan perbedaan client, server, dan peer.
**Jawaban:**
* **Client:** Meminta layanan.
* **Server:** Menyediakan layanan.
* **Peer:** Dapat bertindak sebagai peminta sekaligus penyedia sumber daya dalam arsitektur Peer-to-Peer (P2P).

#### 8. Apa perbedaan bandwidth, throughput, dan goodput?
**Jawaban:**
* **Bandwidth:** Kapasitas nominal kanal.
* **Throughput:** Laju data aktual yang dipindahkan.
* **Goodput:** Laju muatan aplikasi yang berguna setelah tidak menghitung *header* dan pengiriman ulang (*retransmission*).

#### 9. Sebutkan empat komponen nodal delay.
**Jawaban:**
1. *Processing delay*
2. *Queuing delay*
3. *Transmission delay*
4. *Propagation delay*

#### 10. Mengapa Web tidak sama dengan Internet?
**Jawaban:**
Internet adalah infrastruktur jaringan dan protokol global, sedangkan Web adalah salah satu layanan aplikasi yang berjalan di atas Internet.

---

### Level B — Penerapan dan Analisis

#### 11. Sebuah paket berukuran 1.000 byte dikirim melalui tautan 10 Mbps. Hitung transmission delay ideal paket tersebut. Jelaskan komponen delay yang belum tercakup.
**Jawaban:**
* $1.000 \text{ byte} = 8.000 \text{ bit}$
* $d_{\text{trans}} = \frac{L}{R} = \frac{8.000}{10.000.000} = 0,0008 \text{ detik} = 0,8 \text{ ms}$

Komponen yang belum tercakup adalah *processing delay*, *queuing delay*, dan *propagation delay*.

#### 12. Sebuah kampus memiliki koneksi Internet 2 Gbps, tetapi pengguna di satu lantai hanya memperoleh throughput rendah. Susun sedikitnya lima hipotesis yang tidak langsung menyalahkan koneksi ISP.
**Jawaban:**
Kemungkinan penyebab:
1. Kualitas atau interferensi Wi-Fi buruk.
2. Access Point (AP) terlalu padat.
3. *Uplink* lantai terlalu kecil.
4. Kabel fisik bermasalah.
5. Loop atau salah konfigurasi pada Layer 2.
6. Perangkat akhir menjadi *bottleneck*.
7. Kebijakan akses membatasi *throughput*.
8. Server/tujuan aplikasi sedang lambat.

#### 13. Bandingkan kebutuhan jaringan untuk transfer berkas cadangan dan panggilan video. Metrik apa yang paling penting bagi masing-masing aplikasi?
**Jawaban:**
* **Transfer berkas cadangan:** Terutama membutuhkan *throughput* tinggi dan *packet loss* sangat rendah; *latency* dan *jitter* relatif longgar.
* **Panggilan video:** Membutuhkan *latency* dan *jitter* rendah serta *throughput* yang memadai; sedikit *packet loss* masih dapat ditoleransi dengan adaptasi.

#### 14. Sebuah organisasi mempunyai dua koneksi Internet dari dua operator. Keduanya melewati tiang dan jalur ducting yang sama. Evaluasi kualitas redundansinya.
**Jawaban:**
Redundansinya lemah karena kedua koneksi masih memiliki *failure domain* fisik yang sama. Kerusakan pada tiang atau *ducting* dapat memutus kedua koneksi sekaligus.

#### 15. Jelaskan mengapa penambahan bandwidth tidak selalu mengurangi waktu akses ke server yang sangat jauh.
**Jawaban:**
*Bandwidth* tidak menghilangkan *propagation delay* yang dipengaruhi jarak dan kecepatan rambat sinyal. Waktu akses juga dapat dipengaruhi oleh *processing*, *queuing*, Round Trip Time (RTT), server lambat, DNS, atau *bottleneck* lainnya.

#### 16. Sebuah layanan tersedia 99,9% selama satu tahun. Hitung perkiraan maksimum durasi ketidaktersediaannya. Bandingkan dengan target 99,99%.
**Jawaban:**
* **Ketersediaan 99,9%:**
  $$\text{Downtime} = 0,1\% \times 365 \text{ hari} = 0,365 \text{ hari} = 8 \text{ jam } 45,6 \text{ menit } (\approx 8 \text{ jam } 46 \text{ menit/tahun})$$
* **Ketersediaan 99,99%:**
  $$\text{Downtime} = 0,01\% \times 365 \text{ hari} = 0,0365 \text{ hari} \approx 52,6 \text{ menit/tahun}$$

#### 17. Analisis kelebihan dan kelemahan client–server serta P2P untuk distribusi berkas berukuran besar kepada ribuan pengguna.
**Jawaban:**
* **Client–Server:**
  * *Kelebihan:* Unggul dalam kendali terpusat, autentikasi, konsistensi, pencadangan, dan pengelolaan.
  * *Kelemahan:* Server/infrastruktur dapat menjadi *bottleneck* dan *single point of failure*.
* **Peer-to-Peer (P2P):**
  * *Kelebihan:* Meningkatkan skalabilitas karena *peer* ikut menyediakan sumber daya dan tidak bergantung pada satu server pusat.
  * *Kelemahan:* Lebih sulit dalam penemuan *peer*, konsistensi, keamanan, kepercayaan, dan pengelolaan *node*.

#### 18. Berikan contoh ketika topologi fisik dan topologi logis pada jaringan kampus berbeda.
**Jawaban:**
Secara fisik, seluruh komputer di beberapa ruang dapat terhubung berbentuk *star* ke *switch*. Secara logis, komputer tersebut dapat dibagi menjadi beberapa VLAN dan subnet dengan jalur *routing* berbeda. Jadi bentuk fisiknya *star*, sedangkan hubungan logisnya terbagi dalam beberapa jaringan terpisah.

---

### Level C — Evaluasi dan Sintesis

#### 19. Rancang klasifikasi kebutuhan jaringan kampus untuk mahasiswa, staf administrasi, tamu, kamera pengawas, dan laboratorium riset. Jelaskan alasan segmentasi dan aturan komunikasi utamanya.
**Jawaban:**
* **Mahasiswa:** Ditempatkan pada VLAN/subnet mahasiswa dengan akses ke Internet dan layanan akademik.
* **Staf Administrasi:** Pada VLAN terpisah dengan akses ke sistem administrasi yang sensitif.
* **Tamu:** Berada pada jaringan tamu yang hanya mengakses Internet.
* **Kamera Pengawas:** Berada pada VLAN khusus yang hanya dapat berkomunikasi dengan server perekam dan layanan yang diperlukan.
* **Laboratorium Riset:** Berada pada VLAN/subnet khusus dengan akses sesuai kebutuhan eksperimen.

*Alasan Segmentasi:* Membatasi pergerakan lateral (*lateral movement*), memperkecil domain gangguan (*broadcast/failure domain*), dan memudahkan penerapan kebijakan keamanan.

#### 20. Evaluasi pernyataan: “Jaringan internal tidak memerlukan enkripsi karena sudah dilindungi firewall.” Gunakan prinsip kerahasiaan, integritas, dan ketersediaan.
**Jawaban:**
Pernyataan tersebut **tidak tepat**. *Firewall* hanya salah satu kontrol keamanan di batas jaringan (*perimeter*) dan tidak menjamin kerahasiaan atau integritas data jika komunikasi internal disadap atau dimodifikasi. Enkripsi tetap diperlukan untuk menjaga kerahasiaan (*confidentiality*) dan integritas (*integrity*) komunikasi. Ketersediaan (*availability*) juga harus dijaga melalui redundansi, pemantauan, dan pemulihan. Ancaman dapat berasal dari perangkat internal, kredensial yang dicuri, salah konfigurasi, atau pihak ketiga.

#### 21. Diskusikan mengapa Internet dapat berkembang tanpa otoritas teknis pusat tunggal. Jelaskan manfaat serta risikonya.
**Jawaban:**
Internet berkembang melalui interkoneksi jaringan yang dikelola secara mandiri dengan aturan dan standar terbuka. IETF, IANA, RIR, operator, dan organisasi lain memiliki peran masing-masing.
* **Manfaat:** Fleksibilitas, interoperabilitas, skalabilitas, dan tidak bergantung pada satu pengelola.
* **Risiko:** Koordinasi lebih kompleks dan gangguan/kesalahan satu operator dapat berdampak ke jaringan lain (misalnya kesalahan *routing*, DNS, serangan, atau gangguan kabel fisik).

#### 22. Bandingkan circuit switching dan packet switching untuk layanan suara. Jelaskan mengapa suara modern tetap dapat berjalan pada jaringan paket.
**Jawaban:**
* **Circuit Switching:** Mengalokasikan sumber daya jalur selama sesi sehingga kapasitas relatif konsisten dan dapat diprediksi, tetapi kapasitas dapat menganggur (*inefficient*).
* **Packet Switching:** Membagi suara menjadi paket yang berbagi kapasitas secara dinamis sehingga lebih efisien, tetapi dapat mengalami antrean, *delay*, *jitter*, dan *loss*.

Suara modern tetap dapat berjalan di jaringan paket karena protokol dan aplikasi *real-time* (seperti VoIP, WebRTC) memiliki teknik untuk mengelola variasi *delay*, *jitter*, serta toleransi terhadap sedikit *packet loss*.

#### 23. Ambil satu keluhan nyata atau hipotetis berupa “Internet lambat”. Susun prosedur pengumpulan bukti, pengujian hipotesis, dan kriteria keberhasilan perbaikannya.
**Jawaban:**
1. **Ruang Lingkup:** Tentukan ruang lingkup dan waktu terjadinya gangguan.
2. **Isolasi Masalah:** Pisahkan masalah akses lokal dari layanan tujuan.
3. **Pengukuran:** Ukur RTT, *packet loss*, *throughput*, utilisasi, kualitas sinyal, dan periksa log.
4. **Pembandingan:** Bandingkan hasil dengan data acuan (*baseline*).
5. **Pengujian:** Uji satu hipotesis pada satu waktu (misalnya: *access point* padat vs *uplink* penuh).
6. **Dokumentasi & Evaluasi:** Dokumentasikan hasil perbaikan. Perbaikan dianggap berhasil jika metrik kembali ke/mendekati *baseline* dan keluhan pengguna berkurang pada kondisi beban yang sama.

#### 24. Kunjungi statistik IPv6 Google atau sumber pengukuran APNIC. Catat tanggal, definisi metrik, populasi yang diukur, dan nilai untuk Indonesia. Jelaskan mengapa angka dari dua sumber dapat berbeda.
**Jawaban:**
Statistik IPv6 dicatat sebagai *snapshot* bersama tanggal akses, definisi metrik, populasi pengukuran, dan sumber. Angka dari Google dan APNIC dapat berbeda karena metode eksperimen dan populasi yang diukur tidak sama (misalnya Google mengukur *user* yang mengakses layanan Google, sedangkan APNIC menguji keterhubungan IPv6 melalui iklan sampel pada halaman *web*).

#### 25. Buat argumen mengenai penggunaan satelit orbit rendah sebagai koneksi utama atau cadangan bagi kampus di wilayah terpencil. Nilai kinerja, biaya, ketergantungan cuaca, pengelolaan, dan keamanan.
**Jawaban:**
Satelit orbit rendah (LEO) dapat menjadi pilihan utama atau cadangan karena memperluas akses ke wilayah yang sulit dijangkau jaringan terestrial dan memiliki *propagation delay* jauh lebih rendah daripada satelit geostasioner (GEO). 

* **Kinerja:** Cukup baik namun dipengaruhi kondisi radio, kepadatan pelanggan, *gateway*, dan jalur antarjaringan.
* **Cuaca & Pengelolaan:** Masih dipengaruhi oleh kondisi cuaca ekstrim; biaya operasional serta pengelolaan perlu dibandingkan dengan solusi terestrial.
* **Keamanan:** Memerlukan mekanisme keamanan standar seperti autentikasi, enkripsi, *firewall*, pemantauan, dan pengelolaan akses.

#### 26. Jelaskan bagaimana otomatisasi jaringan dapat meningkatkan konsistensi sekaligus memperbesar dampak kesalahan. Usulkan kontrol teknis dan proses untuk mengurangi risiko tersebut.
**Jawaban:**
* **Dampak Otomatisasi:** Mengurangi kesalahan manual dan menerapkan konfigurasi secara konsisten. Namun, jika terdapat kesalahan pada templat atau skrip otomasi, kesalahan tersebut akan langsung tersebar ke banyak perangkat secara bersamaan.
* **Kontrol Risiko:**
  1. Menetapkan *Single Source of Truth*.
  2. Melakukan validasi dan pengujian bertahap (*canary deployment*).
  3. Pembatasan hak akses (*least privilege*).
  4. Pencatatan audit (*audit logging*) dan pemantauan real-time.
  5. Menyediakan mekanisme pembatalan cepat (*rollback*).
  6. Perubahan berdampak besar tetap memerlukan validasi dari teknisi/manusia.

---

## TUGAS KONSEP JARINGAN

### 1. Mencatat tentang kabel UTP Cat 1 sampai Cat 9
**Jawaban:**
Kabel UTP (*Unshielded Twisted Pair*) terdiri dari pasangan kabel tembaga yang dipilin untuk mengurangi gangguan elektromagnetik (crosstalk). Kategori kabel:
* **Cat 1:** Digunakan untuk komunikasi telepon analog.
* **Cat 2 – Cat 4:** Kategori lama untuk jaringan data kecepatan rendah (Legacy).
* **Cat 5:** Mendukung Fast Ethernet (hingga 100 Mbps).
* **Cat 5e:** Mendukung Gigabit Ethernet (1 Gbps).
* **Cat 6:** Mendukung Gigabit Ethernet hingga 10 Gbps pada jarak pendek.
* **Cat 6a:** Mendukung 10 Gigabit Ethernet (10 Gbps) hingga 100 meter.
* **Cat 7 / Cat 7a:** Memiliki spesifikasi frekuensi lebih tinggi dan menggunakan pelindung (*shielding*) tambahan.
* **Cat 8:** Ditujukan untuk kecepatan sangat tinggi (25/40 Gbps) pada jarak pendek (seperti di *data center*).
* **Cat 9:** **Bukan** merupakan standar resmi Ethernet *twisted-pair* dari ISO/IEC atau TIA/EIA, melainkan sering kali hanya berupa istilah/label pemasaran.

---

### 2. Standard Wi-Fi yang ada (a/b/g/n/ac/ax/be)
**Jawaban:**
Standar Wi-Fi dikembangkan oleh IEEE dalam keluarga 802.11:
* **802.11a:** Frekuensi 5 GHz (hingga 54 Mbps).
* **802.11b:** Frekuensi 2.4 GHz (hingga 11 Mbps).
* **802.11g:** Frekuensi 2.4 GHz (hingga 54 Mbps).
* **802.11n (Wi-Fi 4):** Frekuensi 2.4 GHz & 5 GHz, mendukung teknologi MIMO.
* **802.11ac (Wi-Fi 5):** Frekuensi 5 GHz dengan bandwidth lebih lebar.
* **802.11ax (Wi-Fi 6 / Wi-Fi 6E):** Frekuensi 2.4 GHz, 5 GHz, dan 6 GHz, efisiensi tinggi pada area padat.
* **802.11be (Wi-Fi 7):** Generasi terbaru dengan bandwidth hingga 320 MHz dan latensi sangat rendah.

---

### 3. Detail Sejarah dan Timeline Internet
**Jawaban:**
1. **Akhir 1960-an:** Pengembangan ARPANET sebagai pionir jaringan *packet switching*.
2. **1983:** ARPANET secara resmi mengadopsi protokol **TCP/IP** yang menjadi basis utama Internet modern.
3. **1980-an:** Pengenalan *Domain Name System* (DNS) untuk mempermudah pemetaan nama domain ke alamat IP.
4. **1989–1991:** Tim Berners-Lee menciptakan *World Wide Web* (WWW).
5. **1990-an:** Komersialisasi Internet secara luas, perkembangan peramban web (browser), dan perluasan penyedia jasa Internet (ISP).
6. **2000-an – Sekarang:** Era broadband, seluler (3G/4G/5G), layanan komputasi awan (*cloud*), media sosial, dan Internet of Things (IoT).

---

### 4. Menginterpretasikan detail Internet yang muncul pada FAST.com
**Jawaban:**
Pemeriksaan kecepatan Internet melalui FAST.com mengukur beberapa parameter utama:
* **Download Speed:** Laju data yang diterima dari server (kecepatan unduh).
* **Upload Speed:** Laju data yang dikirim ke server (kecepatan unggah).
* **Unloaded Latency:** Waktu respon (*ping*) ketika jaringan tidak sedang digunakan secara intensif.
* **Loaded Latency:** Waktu respon (*ping*) ketika jaringan sedang dimanfaatkan untuk lalu lintas data berat (mengidentifikasi adanya *bufferbloat*).

#### Hasil Pengujian FAST.com:
* **Kecepatan Internet (Download):** $9.6 \text{ Mbps}$
* **Latensi (Unloaded):** $27 \text{ ms}$
* **Latensi (Loaded):** $169 \text{ ms}$
* **Upload Speed:** $0 \text{ Mbps}$
* **Klien:** Surabaya, ID (`2a09:bac5:3a1c:1d0f:0:0:2e5:39`)
* **Server:** Singapore, SG | Tsuen Wan, HK

![Hasil Pengukuran Fast.com](https://raw.githubusercontent.com/placeholder/fastcom_result.png)