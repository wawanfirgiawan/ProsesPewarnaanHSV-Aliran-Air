# Proses Pewarnaan HSV Aliran Air

Nilai **HSV (Hue, Saturation, Value)** dalam tabel hasil program **tidak langsung berasal dari dataset asli**, melainkan merupakan **hasil pemetaan dari dua jenis data: elevasi dan kecepatan aliran air**.

#### 📌 Rinciannya:

1. **Hue (H)** didapat dari **elevasi (ketinggian)**.

   * Elevasi dibagi ke dalam sejumlah kelas (misalnya 20 kelas warna).
   * Setiap kelas memiliki warna berbeda (dari **merah** untuk elevasi tinggi ke **biru/ungu** untuk elevasi rendah).
   * Contoh: jika sebuah titik memiliki elevasi 20 dan range elevasi dibagi rata dari 0–100, maka nilai 20 masuk kelas ke-4, yang mewakili warna hijau → hue ≈ 0.8.

2. **Saturation (S)** dan **Value (V)** berasal dari **kecepatan aliran air** yang dihitung menggunakan **rumus Bernoulli**:

   $$
   v = \sqrt{2g(H_1 - H_2)}
   $$

   * Setelah kecepatan dihitung, nilainya dinormalisasi ke skala 0–1:

     $$
     v_{\text{norm}} = \frac{v - v_{\text{min}}}{v_{\text{max}} - v_{\text{min}}}
     $$
   * Kemudian nilai ini dikonversi menjadi nilai S dan V:

     $$
     S = 0.1 + 0.9 \times v_{\text{norm}} \\
     V = 0.1 + 0.9 \times v_{\text{norm}}
     $$
   * Artinya: kecepatan yang **lebih besar** → warna yang **lebih tajam dan terang**, kecepatan rendah → warna **lebih pudar**.

---

### 🧪 **Contoh Implementasi**

Misalnya ada data elevasi berikut (5x5):

```
88  55  12  30  20
60  45  25  15  10
70  50  20  12  5
80  65  55  35  3
90  75  60  40  1
```

* Titik A = (0,0), elevasi = 88

* Titik B = (0,1), elevasi = 55 → maka dihitung kecepatan aliran dari A → B:

  $$
  v = \sqrt{2 \times 9.8 \times (88 - 55)} ≈ \sqrt{646} ≈ 25.42 \text{ m/s}
  $$

* Setelah semua kecepatan dihitung, akan dicari nilai kecepatan **terendah dan tertinggi** untuk normalisasi.

* Misal nilai normalisasi $v_{\text{norm}} = 0.7$, maka:

  $$
  S = 0.1 + 0.9 \times 0.7 = 0.73 \\
  V = 0.1 + 0.9 \times 0.7 = 0.73
  $$

* Titik A (elevasi 88) misalnya berada pada **kelas warna ke-2** → Hue = 0.9 (merah-kejinggaan)

Jadi untuk titik A:

* **Hue = 0.9**
* **Saturation = 0.73**
* **Value = 0.73**
  → Hasil akhir HSV-nya = (0.9, 0.73, 0.73) → kemudian dikonversi ke warna RGB dan HEX untuk ditampilkan di tabel.

---

### 🎯 **Kesimpulan**

Nilai HSV dihasilkan dari **pemrosesan dua jenis data**:

* **H dari elevasi** (diklasifikasi)
* **S dan V dari kecepatan aliran** (hasil rumus Bernoulli → dinormalisasi)

Pemetaan ini membuat jalur aliran terlihat lebih jelas, informatif, dan kontras secara visual dibanding peta elevasi biasa.

Jika Anda ingin, saya bisa bantu buat ilustrasi grid warna kecil dengan nilai elevasi dan HSV-nya juga.
