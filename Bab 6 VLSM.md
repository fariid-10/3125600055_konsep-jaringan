# LAPORAN PRAKTIKUM KONSEP JARINGAN
## PERHITUNGAN DAN IMPLEMENTASI VLSM (VARIABLE LENGTH SUBNET MASK)

**Nama:** Muhammad Fariid Maulana  
**NRP:** 3125600055  
**Dosen Pengampu:** Dr. Ferry Astika Saputra, ST, M.Sc  
**Program Studi:** D4 Teknik Informatika  
**Institusi:** Politeknik Elektronika Negeri Surabaya  
**Tahun:** 2026  

---

### A. Parameter Soal

* **Alokasi IP Network Awal:** `10.252.108.0/24` (Total 256 Alamat IP)
* **Kebutuhan Subnet:**
  1. **Lab A:** 90 Host
  2. **Lab B:** 60 Host
  3. **Administrasi:** 14 Host
  4. **End-point (Point-to-Point Link):** 2 Host

---

### B. Langkah-Langkah Perhitungan VLSM

Dalam metode VLSM, pengalokasian IP dilakukan berdasarkan **kebutuhan host terbesar ke yang terkecil** untuk menghindari *overlap* alokasi IP.

#### 1. Subnet Lab A (Kebutuhan: 90 Host)
* **Hitung Kebutuhan Alamat IP:** $\text{Host} + 2 = 90 + 2 = 92 \text{ IP}$
* **Cari Alokasi $2^n$ Terdekat:** $2^7 = 128 \text{ IP} \ge 92$ ($n = 7 \text{ bit host}$)
* **Prefix Baru:** $32 - 7 = \mathbf{/25}$
* **Netmask:** `255.255.255.128`
* **Rincian Alokasi:**
  * **Network Address:** `10.252.108.0`
  * **Usable Host Range:** `10.252.108.1` – `10.252.108.126`
  * **Broadcast Address:** `10.252.108.127`

#### 2. Subnet Lab B (Kebutuhan: 60 Host)
* **Hitung Kebutuhan Alamat IP:** $\text{Host} + 2 = 60 + 2 = 62 \text{ IP}$
* **Cari Alokasi $2^n$ Terdekat:** $2^6 = 64 \text{ IP} \ge 62$ ($n = 6 \text{ bit host}$)
* **Prefix Baru:** $32 - 6 = \mathbf{/26}$
* **Netmask:** `255.255.255.192`
* **Rincian Alokasi:**
  * **Network Address:** `10.252.108.128`
  * **Usable Host Range:** `10.252.108.129` – `10.252.108.186`
  * **Broadcast Address:** `10.252.108.187`

#### 3. Subnet Administrasi (Kebutuhan: 14 Host)
* **Hitung Kebutuhan Alamat IP:** $\text{Host} + 2 = 14 + 2 = 16 \text{ IP}$
* **Cari Alokasi $2^n$ Terdekat:** $2^4 = 16 \text{ IP} \ge 16$ ($n = 4 \text{ bit host}$)
* **Prefix Baru:** $32 - 4 = \mathbf{/28}$
* **Netmask:** `255.255.255.240`
* **Rincian Alokasi:**
  * **Network Address:** `10.252.108.188`
  * **Usable Host Range:** `10.252.108.189` – `10.252.108.202`
  * **Broadcast Address:** `10.252.108.203`

#### 4. Subnet End-point (Kebutuhan: 2 Host)
* **Hitung Kebutuhan Alamat IP:** $\text{Host} + 2 = 2 + 2 = 4 \text{ IP}$
* **Cari Alokasi $2^n$ Terdekat:** $2^2 = 4 \text{ IP} \ge 4$ ($n = 2 \text{ bit host}$)
* **Prefix Baru:** $32 - 2 = \mathbf{/30}$
* **Netmask:** `255.255.255.252`
* **Rincian Alokasi:**
  * **Network Address:** `10.252.108.204`
  * **Usable Host Range:** `10.252.108.205` – `10.252.108.206`
  * **Broadcast Address:** `10.252.108.207`

---

### C. Ringkasan Tabel VLSM

| Nama Subnet | Kebutuhan Host | Prefix | Netmask | Network Address | Range Host Valid | Broadcast Address |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Lab A** | 90 Host | `/25` | `255.255.255.128` | `10.252.108.0` | `10.252.108.1` – `10.252.108.126` | `10.252.108.127` |
| **Lab B** | 60 Host | `/26` | `255.255.255.192` | `10.252.108.128` | `10.252.108.129` – `10.252.108.186` | `10.252.108.187` |
| **Administrasi** | 14 Host | `/28` | `255.255.255.240` | `10.252.108.188` | `10.252.108.189` – `10.252.108.202` | `10.252.108.203` |
| **End-point** | 2 Host | `/30` | `255.255.255.252` | `10.252.108.204` | `10.252.108.205` – `10.252.108.206` | `10.252.108.207` |

> **Ruang Alamat IP Tersisa:**  
> Rentang IP dari `10.252.108.208` hingga `10.252.108.255` (sebanyak 48 IP) masih belum terpakai dan dapat diekspansi untuk kebutuhan subnet lain di masa depan.