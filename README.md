# UAS - Pengolahan Citra

Kelompok: 
- Arie Miftah Budiman  | 312210350
+ Moh. Restu Nur Rizki | 312210496
* Ridwan Ahri          | 312210647

### Penjelasan Algoritme K-means Clustering untuk Segmentasi Gambar

#### 1. Memuat Gambar

```
image = cv2.imread('images/helmet.jpg')
if image is None:
    raise FileNotFoundError("File gambar tidak ditemukan. Periksa kembali jalur file.")
```
> Memuat gambar helmet.jpg menggunakan OpenCV. Jika gambar tidak ditemukan, akan muncul pesan kesalahan.

#### 2. Mengubah Warna Gambar
```
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
> Mengubah format warna gambar dari BGR (Biru, Hijau, Merah) ke RGB (Merah, Hijau, Biru).

#### 3. Mengubah Bentuk Gambar
```
pixel_vals = image.reshape((-1, 3))
```
> Mengubah gambar menjadi array 2D di mana setiap baris adalah satu piksel dengan tiga nilai warna (R, G, B).

#### 4. Mengkonversikan Tipe Data
```
pixel_vals = np.float32(pixel_vals)
```
> Mengubah tipe data nilai piksel menjadi float (angka desimal).

#### 5. Menentukan Kriteria Penghentian
```
criteria = (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 100, 0.85)
```
> Menetapkan kriteria penghentian untuk algoritme k-means: 100 iterasi atau perubahan posisi pusat cluster kurang dari 0.85.

#### 6. Menentukan Jumlah Cluster
```
k = 3
```
> Menetapkan jumlah cluster (kelompok warna) menjadi 3.

#### 7. Melakukan K-means Clustering
```
retval, labels, centers = cv2.kmeans(pixel_vals, k, None, criteria, 10, cv2.KMEANS_RANDOM_CENTERS)
```
> Menjalankan algoritme k-means untuk mengelompokkan piksel menjadi 3 cluster berdasarkan kemiripan warna.
> labels menunjukkan cluster setiap piksel.
> centers adalah warna rata-rata dari setiap cluster.

#### 8. Mengkonversi Nilai Pusat Cluster
```
centers = np.uint8(centers)
```
> Mengubah nilai warna pusat cluster kembali ke format 8-bit (0-255).

#### 9. Memetakan Label ke Warna Pusat Cluster
```
segmented_data = centers[labels.flatten()]
```
> Memetakan setiap piksel ke warna pusat cluster yang sesuai.

#### 10. Membentuk Ulang Data
```
segmented_image = segmented_data.reshape((image.shape))
```
> Membentuk ulang data piksel yang telah tersegmentasi menjadi dimensi gambar asli.

#### 11. Menampilkan Gambar
```
plt.figure(figsize=(12, 6))

plt.subplot(1, 2, 1)
plt.imshow(image)
plt.title('Gambar Asli')

plt.subplot(1, 2, 2)
plt.imshow(segmented_image)
plt.title('Gambar Tersegmentasi')

plt.show()
```
> Menampilkan gambar asli dan gambar tersegmentasi berdampingan menggunakan Matplotlib.

#### 12. Menampilkan Pusat Cluster dan Distribusi Label
```
print("Pusat cluster:\n", centers)
unique_labels, counts = np.unique(labels, return_counts=True)
print("Distribusi label:\n", dict(zip(unique_labels, counts)))
```
> Menampilkan nilai warna pusat cluster.
> Menampilkan distribusi label untuk mengetahui jumlah piksel dalam setiap cluster.

Dan begitulah! Dengan langkah-langkah ini, kita berhasil mengelompokkan warna dalam gambar helm menjadi tiga kelompok utama, menyederhanakan gambar, dan melihat hasilnya dalam bentuk visual.

## Output
![](images/Output.png)
