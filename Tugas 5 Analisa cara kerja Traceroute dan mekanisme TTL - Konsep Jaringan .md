# LAPORAN PRAKTIKUM KONSEP JARINGAN
## MEKANISME TRACEROUTE DAN PERAN TIME-TO-LIVE (TTL)

**Disusun oleh:**  
* **Nama:** Muhammad Fariid Maulana  
* **NRP:** 3125600055  
* **Dosen Pengampu:** Dr. Ferry Astika Saputra, ST, M.Sc  
* **Program Studi:** D4 Teknik Informatika  
* **Institusi:** Politeknik Elektronika Negeri Surabaya  
* **Tahun:** 2026  

---

## I. Maksud dan Tujuan

1. Mengamati cara kerja utilitas `tracert` (traceroute) saat mengidentifikasi jalur perlintasan paket data.
2. Memverifikasi fungsi parameter *Time-to-Live* (TTL) pada *header* IP sebagai mekanisme pencegah perputaran paket tanpa henti (*routing loop*).
3. Menganalisis variasi respons *Internet Control Message Protocol* (ICMP) yang dikirimkan oleh node perantara maupun node tujuan.
4. Membandingkan alur pengiriman data pada rute langsung (*direct link*) dan rute alternatif (*indirect link*).

---

## II. Topologi & Skema Pengalamatan IP

Praktikum ini menggunakan konfigurasi 3 unit Router Cisco (membentuk topologi segitiga) dan 2 unit PC:

* **Struktur Koneksi Jaringan:**
  * Link Utama (Bawah): Router0 $\leftrightarrow$ Router2 (`10.10.10.0/30`)
  * Link Jalur Atas 1: Router0 $\leftrightarrow$ Router Atas (`10.10.20.0/30`)
  * Link Jalur Atas 2: Router Atas $\leftrightarrow$ Router2 (`10.10.30.0/30`)
  * Subnet LAN asal (PC0): `192.168.10.0/24` via Router0
  * Subnet LAN tujuan (PC1): `192.168.20.0/24` via Router2

### Informasi Konfigurasi Interface

| Perangkat | Interface | IP Address | Subnet Mask | Default Gateway | Function / Link |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PC0** | Fa0 | `192.168.10.10` | `255.255.255.0` | `192.168.10.1` | Endpoint Pengirim |
| **PC1** | Fa0 | `192.168.20.10` | `255.255.255.0` | `192.168.20.1` | Endpoint Penerima |
| **Router0** | Fa0/0 | `192.168.10.1` | `255.255.255.0` | - | Gateway Subnet PC0 |
| | Gig2/0 | `10.10.20.2` | `255.255.255.252` | - | Interkoneksi Router Atas |
| | Gig3/0 | `10.10.10.2` | `255.255.255.252` | - | Interkoneksi Router2 (Link Bawah) |
| **Router Atas** | Gig2/0 | `10.10.20.1` | `255.255.255.252` | - | Interkoneksi Router0 |
| | Gig3/0 | `10.10.30.1` | `255.255.255.252` | - | Interkoneksi Router2 |
| **Router2** | Fa0/0 | `192.168.20.1` | `255.255.255.0` | - | Gateway Subnet PC1 |
| | Gig2/0 | `10.10.30.2` | `255.255.255.252` | - | Interkoneksi Router Atas |
| | Gig3/0 | `10.10.10.1` | `255.255.255.252` | - | Interkoneksi Router0 (Link Bawah) |

---

## III. Pengujian traceroute & Hasil Pelacakan

### 1. Jalur Utama / Langsung (3 Hop)

Uji coba diawali dengan mengarahkan trafik langsung melintasi jalur bawah (Router0 $\to$ Router2):

```text
C:\>tracert 192.168.20.10

Tracing route to 192.168.20.10 over a maximum of 30 hops:

  1     0 ms     0 ms     0 ms  192.168.10.1
  2     0 ms     0 ms     0 ms  10.10.10.1
  3     0 ms     0 ms     0 ms  192.168.20.10

Trace complete.
```

#### Deskripsi Proses Tiap Hop:
* **Hop 1 (`192.168.10.1`):** PC0 melepas paket dengan nilai $\text{TTL} = 1$. Ketika menyentuh Router0, nilai TTL berkurang menjadi 0. Router0 membuang paket tersebut dan membalas pengirim menggunakan pesan **ICMP Time Exceeded (Type 11)**.
* **Hop 2 (`10.10.10.1`):** PC0 mengirimkan paket berikutnya dengan $\text{TTL} = 2$. Router0 meneruskannya ($\text{TTL} = 1$) menuju Router2. Di Router2, nilai TTL habis ($0$), paket di-*drop*, dan Router2 merespons dengan **ICMP Time Exceeded (Type 11)**.
* **Hop 3 (`192.168.20.10`):** PC0 memancarkan paket bernilai $\text{TTL} = 3$. Paket berhasil melintasi Router0 dan Router2 hingga mendarat di PC1. Karena telah mencapai tujuan akhir, PC1 membalasnya dengan **ICMP Echo Reply (Type 0)**.

---

### 2. Jalur Pengalihan / Memutar (4 Hop)

Selanjutnya, rute statis diubah sedemikian rupa sehingga paket diarahkan melewati Router Atas sebelum masuk ke Router2:

#### Tahap 1: Pengujian Awal (Kendala Asymmetric Routing)
```text
C:\>tracert 192.168.20.10

Tracing route to 192.168.20.10 over a maximum of 30 hops:

  1     0 ms    16 ms     0 ms  192.168.10.1
  2     0 ms     0 ms     0 ms  10.10.20.1
  3     0 ms     *        0 ms  10.10.30.2
  4     *        0 ms     *     Request timed out.

Trace complete.
```

> **Pembahasan:** Kegagalan (*Request timed out*) di hop 4 disebabkan oleh ketidaksesuaian rute balik pada Router2 (terdapat *dual route* yang ambigu), sehingga sinyal balasan dari PC1 gagal dipandu kembali menuju PC0.

#### Tahap 2: Hasil Setelah Pembenahan Tabel Rute
Usai tabel routing balik pada Router2 dirapikan, pelacakan rute memutar berhasil terselesaikan secara menyeluruh:

```text
C:\>tracert 192.168.20.10

Tracing route to 192.168.20.10 over a maximum of 30 hops:

  1     0 ms     0 ms     0 ms  192.168.10.1
  2     0 ms     0 ms     0 ms  10.10.20.1
  3     0 ms     0 ms     0 ms  10.10.30.2
  4     0 ms     0 ms     0 ms  192.168.20.10

Trace complete.
```

#### Deskripsi Proses Tiap Hop:
* **Hop 1 (`192.168.10.1`):** Gateway awal merespons menggunakan **ICMP Type 11** saat paket awal dengan $\text{TTL} = 1$ kedaluwarsa.
* **Hop 2 (`10.10.20.1`):** Router Atas mengirim **ICMP Type 11** ketika menerima paket dengan $\text{TTL} = 2$ yang nilainya habis di interface tersebut.
* **Hop 3 (`10.10.30.2`):** Router2 memberikan laporan **ICMP Type 11** untuk paket ber-TTL $3$ yang telah melintasi dua router sebelumnya.
* **Hop 4 (`192.168.20.10`):** Paket dengan $\text{TTL} = 4$ sukses tiba di PC1, kemudian dijawab dengan **ICMP Echo Reply (Type 0)** yang mengakhiri proses *tracing*.

---

## IV. Kesimpulan

1. **Prinsip Inkremental TTL:** Perintah `traceroute` bekerja secara eksplisit dengan menaikkan nilai TTL paket ICMP bertahap mulai dari 1. Setiap router transit yang menerima paket ber-TTL 0 wajib mengabaikannya dan melaporkan kembali ke pengirim via balasan **ICMP Time Exceeded (Type 11)**.
2. **Diferensiasi Respon ICMP:** Terdapat batas tegas antara peran node transit dan destination host. Node intermediate memicu sinyal **ICMP Type 11**, sedangkan target destination menghasilkan sinyal **ICMP Type 0 (Echo Reply)**.
3. **Sensitivitas Terhadap Perubahan Topologi:** Penambahan atau pengalihan rute statis pada tabel *routing* router secara instan tecermin pada output `tracert`, di mana rute yang tadinya 3 hop berkembang menjadi 4 hop secara akurat.
