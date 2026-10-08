# LAPORAN KONSEP JARINGAN

* **Nama:** Muhammad Fariid Maulana
* **NRP:** 3125600055
* **Dosen Pengampu:** Dr. Ferry Astika Saputra, ST, M.Sc
* **Program Studi:** D4 Teknik Informatika
* **Institusi:** Politeknik Elektronika Negeri Surabaya
* **Tahun:** 2026

---

## Perhitungan Subnetting

### Soal 1: `192.168.1.0/24` Dibagi Menjadi 4 Subnet

* **Kebutuhan Subnet:** 4 subnet $\to 2^n \ge 4 \implies n = 2$ bit subnet dipinjam.
* **Prefix Baru:** $/24 + 2 = /26$ (Netmask: `255.255.255.192`).
* **Blok Subnet (Interval):** $256 - 192 = 64$.
* **Host per Subnet:** $2^6 - 2 = 62$ *usable host*.

| Subnet | Network ID | Usable Host Range | Broadcast IP |
| :--- | :--- | :--- | :--- |
| **Subnet 1** | `192.168.1.0/26` | `192.168.1.1` – `192.168.1.62` | `192.168.1.63` |
| **Subnet 2** | `192.168.1.64/26` | `192.168.1.65` – `192.168.1.126` | `192.168.1.127` |
| **Subnet 3** | `192.168.1.128/26` | `192.168.1.129` – `192.168.1.190` | `192.168.1.191` |
| **Subnet 4** | `192.168.1.192/26` | `192.168.1.193` – `192.168.1.254` | `192.168.1.255` |

#### Topologi & Pengujian Ping (Soal 1)

![Topologi Soal 1](./soal1_topologi.png)

```text
C:\>ping 192.168.1.62

Pinging 192.168.1.62 with 32 bytes of data:

Request timed out.
Reply from 192.168.1.62: bytes=32 time<1ms TTL=127
Reply from 192.168.1.62: bytes=32 time<1ms TTL=127
Reply from 192.168.1.62: bytes=32 time=21ms TTL=127

Ping statistics for 192.168.1.62:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 21ms, Average = 7ms
```

---

### Soal 2: `132.10.0.0/16` Dibagi Menjadi 10 Segment

* **Kebutuhan Subnet:** 10 segment $\to 2^n \ge 10 \implies n = 4$ bit subnet dipinjam ($2^4 = 16$ subnet tersedia).
* **Prefix Baru:** $/16 + 4 = /20$ (Netmask: `255.255.240.0`).
* **Blok Subnet Oktet ke-3:** $256 - 240 = 16$.
* **Host per Subnet:** $2^{12} - 2 = 4.094$ *usable host*.

| Segment | Network ID | Usable Host Range | Broadcast IP |
| :--- | :--- | :--- | :--- |
| **Segment 1** | `132.10.0.0/20` | `132.10.0.1` – `132.10.15.254` | `132.10.15.255` |
| **Segment 2** | `132.10.16.0/20` | `132.10.16.1` – `132.10.31.254` | `132.10.31.255` |
| **Segment 3** | `132.10.32.0/20` | `132.10.32.1` – `132.10.47.254` | `132.10.47.255` |
| **Segment 4** | `132.10.48.0/20` | `132.10.48.1` – `132.10.63.254` | `132.10.63.255` |
| **Segment 5** | `132.10.64.0/20` | `132.10.64.1` – `132.10.79.254` | `132.10.79.255` |
| **Segment 6** | `132.10.80.0/20` | `132.10.80.1` – `132.10.95.254` | `132.10.95.255` |
| **Segment 7** | `132.10.96.0/20` | `132.10.96.1` – `132.10.111.254` | `132.10.111.255` |
| **Segment 8** | `132.10.112.0/20` | `132.10.112.1` – `132.10.127.254` | `132.10.127.255` |
| **Segment 9** | `132.10.128.0/20` | `132.10.128.1` – `132.10.143.254` | `132.10.143.255` |
| **Segment 10** | `132.10.144.0/20` | `132.10.144.1` – `132.10.159.254` | `132.10.159.255` |

#### Topologi & Pengujian Ping (Soal 2)

![Topologi Soal 2](./soal2_topologi.png)

```text
C:\>ping 132.10.144.10

Pinging 132.10.144.10 with 32 bytes of data:

Request timed out.
Reply from 132.10.144.10: bytes=32 time<1ms TTL=127
Reply from 132.10.144.10: bytes=32 time<1ms TTL=127
Reply from 132.10.144.10: bytes=32 time<1ms TTL=127

Ping statistics for 132.10.144.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

---

### Soal 3: `17.8.0.0/16` (Kelas A) Dibagi Menjadi 4 Subnet

* **Kebutuhan Subnet:** 4 subnet $\to 2^n \ge 4 \implies n = 2$ bit subnet dipinjam.
* **Prefix Baru:** $/16 + 2 = /18$ (Netmask: `255.255.192.0`).
* **Blok Subnet Oktet ke-3:** $256 - 192 = 64$.
* **Host per Subnet:** $2^{14} - 2 = 16.382$ *usable host*.

| Subnet | Network ID | Usable Host Range | Broadcast IP |
| :--- | :--- | :--- | :--- |
| **Subnet 1** | `17.8.0.0/18` | `17.8.0.1` – `17.8.63.254` | `17.8.63.255` |
| **Subnet 2** | `17.8.64.0/18` | `17.8.64.1` – `17.8.127.254` | `17.8.127.255` |
| **Subnet 3** | `17.8.128.0/18` | `17.8.128.1` – `17.8.191.254` | `17.8.191.255` |
| **Subnet 4** | `17.8.192.0/18` | `17.8.192.1` – `17.8.255.254` | `17.8.255.255` |

#### Topologi & Pengujian Ping (Soal 3)

![Topologi Soal 3](./soal3_topologi.png)

```text
C:\>ping 17.8.0.10

Pinging 17.8.0.10 with 32 bytes of data:

Request timed out.
Reply from 17.8.0.10: bytes=32 time<1ms TTL=127
Reply from 17.8.0.10: bytes=32 time<1ms TTL=127
Reply from 17.8.0.10: bytes=32 time<1ms TTL=127

Ping statistics for 17.8.0.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

---

### Soal 4: `8.32.0.0/12` (Kelas A) Dibagi Menjadi 6 Subnet

* **Kebutuhan Subnet:** 6 subnet $\to 2^n \ge 6 \implies n = 3$ bit subnet dipinjam ($2^3 = 8$ subnet tersedia).
* **Prefix Baru:** $/12 + 3 = /15$ (Netmask: `255.254.0.0`).
* **Blok Subnet Oktet ke-2:** $256 - 254 = 2$.
* **Host per Subnet:** $2^{17} - 2 = 131.070$ *usable host*.

| Subnet | Network ID | Usable Host Range | Broadcast IP |
| :--- | :--- | :--- | :--- |
| **Subnet 1** | `8.32.0.0/15` | `8.32.0.1` – `8.33.255.254` | `8.33.255.255` |
| **Subnet 2** | `8.34.0.0/15` | `8.34.0.1` – `8.35.255.254` | `8.35.255.255` |
| **Subnet 3** | `8.36.0.0/15` | `8.36.0.1` – `8.37.255.254` | `8.37.255.255` |
| **Subnet 4** | `8.38.0.0/15` | `8.38.0.1` – `8.39.255.254` | `8.39.255.255` |
| **Subnet 5** | `8.40.0.0/15` | `8.40.0.1` – `8.41.255.254` | `8.41.255.255` |
| **Subnet 6** | `8.42.0.0/15` | `8.42.0.1` – `8.43.255.254` | `8.43.255.255` |

#### Topologi & Pengujian Ping (Soal 4)

![Topologi Soal 4](./soal4_topologi.png)

```text
C:\>ping 8.32.0.10

Pinging 8.32.0.10 with 32 bytes of data:

Reply from 8.32.0.10: bytes=32 time<1ms TTL=127
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127
Reply from 8.32.0.10: bytes=32 time<1ms TTL=127

Ping statistics for 8.32.0.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
