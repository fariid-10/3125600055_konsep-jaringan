# LAPORAN KONSEP JARINGAN

* **Nama:** Muhammad Fariid Maulana
* **NRP:** 3125600055
* **Dosen Pengampu:** Dr. Ferry Astika Saputra, ST, M.Sc
* **Program Studi:** D4 Teknik Informatika
* **Institusi:** Politeknik Elektronika Negeri Surabaya
* **Tahun:** 2026

---

## A. Perhitungan Alokasi IP Address

Tentukan parameter jaringan (*IP Gateway*, *Host Pertama*, *Host Terakhir*, *Broadcast*, dan *IP Network*) untuk alamat IP berikut:
1. `21.26.8.5`
2. `212.6.8.3`
3. `103.24.56.32`
4. `1.1.1.1`
5. `172.31.16.8`

### Tabel Hasil Analisis IP Address

| No | IP Address | Kelas | Network Address | Gateway | Host Pertama | Host Terakhir | Broadcast Address |
| :-: | :--- | :-: | :--- | :--- | :--- | :--- | :--- |
| **1** | `21.26.8.5` | A | `21.0.0.0` | `21.0.0.1` | `21.0.0.2` | `21.255.255.254` | `21.255.255.255` |
| **2** | `212.6.8.3` | C | `212.6.8.0` | `212.6.8.1` | `212.6.8.2` | `212.6.8.254` | `212.6.8.255` |
| **3** | `103.24.56.32` | A | `103.0.0.0` | `103.0.0.1` | `103.0.0.2` | `103.255.255.254` | `103.255.255.255` |
| **4** | `1.1.1.1` | A | `1.0.0.0` | `1.0.0.1` | `1.0.0.2` | `1.255.255.254` | `1.255.255.255` |
| **5** | `172.31.16.8` | B | `172.31.0.0` | `172.31.0.1` | `172.31.0.2` | `172.31.255.254` | `172.31.255.255` |

---

## B. Harmonisasi 1, 3, 5, 7, 9, 10 (Fourier Series)

Simulasi berikut menggambarkan pembentukan sinyal digital di *Physical Layer* dengan menjumlahkan beberapa komponen harmonik gelombang.

### Kode Program Python

```python
import matplotlib.pyplot as plt
import numpy as np

# Inisialisasi domain waktu dan parameter frekuensi
t = np.linspace(0, 2, 2000)
f = 1
harmonics = [1, 3, 5, 7, 9, 10]
cumulative_signal = np.zeros_like(t)

plt.figure(figsize=(10, 6))

for h in harmonics:
    component = (1 / h) * np.sin(2 * np.pi * h * f * t)
    cumulative_signal += component
    label = (
        f"Harmonik 1 s/d {h}"
        if h != 10
        else "Harmonik 1 s/d 10 (komponen genap)"
    )
    plt.plot(t, cumulative_signal, label=label, alpha=0.8)

plt.title("Simulasi Pembentukan Sinyal Digital di Physical Layer (Fourier Series)")
plt.xlabel("Waktu (detik)")
plt.ylabel("Amplitudo")
plt.axhline(0, color="black", linestyle="--", linewidth=0.7)
plt.grid(True, linestyle=":", alpha=0.6)
plt.legend(loc="upper right")
plt.tight_layout()
plt.show()
```

### Grafik Hasil Simulasi

![Simulasi Pembentukan Sinyal Digital di Physical Layer](./grafik_fourier.png)

### Analisis Hasil Simulation

1. **Harmonik 1 (Frekuensi Fundamental):**
   Menghasilkan gelombang sinus murni. Sinyal belum memiliki transisi biner diskret yang jelas.
2. **Harmonik 3, 5, 7, dan 9:**
   Bertahap meratakan puncak gelombang dan membuat lereng transisi naik-turun menjadi curam, sehingga sinyal mendekati bentuk pulsa kotak digital. Ini membuktikan bahwa semakin lebar *bandwidth* kanal yang mampu melewatkan spektrum harmonik tinggi, semakin presisi bentuk pulsa digital yang diterima.
3. **Harmonik 10:**
   Menunjukkan dampak masuknya frekuensi genap yang menghasilkan riak asimetris pada sinyal (representasi distorsi bentuk gelombang di media nyata).