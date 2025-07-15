# Proses Pewarnaan HSV Aliran Air

```markdown
# 🌊 Visualisasi Aliran Sungai Berbasis HSV dan Bernoulli

## 📘 Bagaimana Mengonversi Data Kecepatan ke HSV?

Aplikasi ini memvisualisasikan aliran air dengan menggunakan model pewarnaan **HSV (Hue, Saturation, Value)** berdasarkan:

- Elevasi (DEM – Digital Elevation Model)
- Kecepatan aliran antar grid (menggunakan rumus Bernoulli)

### ⚙️ Proses Konversi Ke HSV

1. **Hitung Kecepatan Aliran (v)**  
   Menggunakan rumus Bernoulli:
   \[
   v = \sqrt{2g(H_1 - H_2)}
   \]
   di mana:
   - \(H_1\) adalah elevasi asal (lebih tinggi)
   - \(H_2\) adalah elevasi tetangga yang lebih rendah

2. **Normalisasi Kecepatan ke Rentang 0–1**  
   \[
   v_{\text{norm}} = \frac{v - v_{\text{min}}}{v_{\text{max}} - v_{\text{min}}}
   \]

3. **Konversi ke Nilai Saturation dan Value**
   - Saturation (S):
     \[
     S = 0.1 + 0.9 \times v_{\text{norm}}
     \]
   - Value (V):
     \[
     V = 0.1 + 0.9 \times v_{\text{norm}}
     \]
   - Nilai kecepatan tinggi → warna cerah & tajam  
     Nilai kecepatan rendah → warna redup & pucat

4. **Hue (H) Berdasarkan Ketinggian**
   - Elevasi diklasifikasikan ke dalam 20 kelas warna
   - Hue diberikan dari merah (tinggi) → biru/ungu (rendah)

---

## 🧪 Contoh Implementasi

Misalnya grid elevasi (5x5):

```

88  55  12  30  20 

60  45  25  15  10

70  50  20  12   5

80  65  55  35   3

90  75  60  40   1

```

- Titik A = (0,0), elevasi = 88  
- Titik B = (0,1), elevasi = 55  
  \[
  v = \sqrt{2 \times 9.8 \times (88 - 55)} \approx 25.42 \text{ m/s}
  \]

- Misal \(v_{\text{min}} = 5\) dan \(v_{\text{max}} = 30\), maka:
  \[
  v_{\text{norm}} = \frac{25.42 - 5}{30 - 5} = 0.8168
  \]

- Maka:
  - \(S = 0.1 + 0.9 \times 0.8168 \approx 0.8351\)
  - \(V = 0.1 + 0.9 \times 0.8168 \approx 0.8351\)

- Hue (H) ditentukan dari kelas elevasi, misalnya hue = 0.9 (kemerahan)

---

## 🎯 Hasil Akhir

Visualisasi akhir akan menunjukkan:
- **Aliran utama** → warna cerah, kontras, jelas
- **Area tanpa aliran** → gelap & pucat
- Setiap piksel mewakili nilai HSV yang dikonversi ke RGB & HEX dan ditampilkan pada peta interaktif serta tabel hasil

---

📌 Penjelasan lengkap dan script tersedia pada folder:
- `modules/algoritma_d8.py`
- `modules/pewarnaan.py`
- `app.py`

---
© 2025 — Universitas Hasanuddin & Universitas Sulawesi Barat  
```

