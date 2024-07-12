# PA-PC_202231058_ADISTHIHAFIZHAH_B

## UAS Pengolahan Citra


#### Tahapan menyelesaikan projek:
  Pertama-tama saya mengambil potret diri saya. kemudian saya masukkan kedalam folder yang sama dengan notebook yang akan saya buat. kemudian saya mengolah citra tersebut dan berikut adalah langkah-langkahnya:

#### Import Library
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import skimage
```
  Pada codingan diatas saya mengimport library yaitu cv2, numpy, matplotlib, dan skimage.
Library cv2 digunakan untuk memanipulasi citra seperti membaca, menulis, menampilkan, menganalisis gambar.
Library numpy digunakan untuk numerik seperti mengubah warna pada gambar menjadi sebuah matrix angka yang akan merepresentasikan warna tersebut. Library ini dugunakan bersama dengan library lain seperti OpenCV untuk memanipulasi dat gambar sebagai array.
Library matplotlib digunakan untuk  membuat plot seperti memvisualisasikan gambar, data, dan animasi. library ini sering digunakan untuk menampilkan gambar, histogram, grafik garis, grafik batang, dan visualisasi data lainnya.
Library skimage adalah library untuk pemrosesan gambar yang dibangun diatas SciPy. Library ini menyediakan berbagai alat untuk transformasi gambar seperti filter, segmentasi, morfologi, dan deteksi tepi.

#### Mengimport gambar
```bash
image = cv2.imread('adis4.jpg')

cv2.imshow("Adis", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
  Codingan diatas adalah code untuk membaca gambar. Gambar yang ingin dibaca harus berada di folder yang sama dengan notebook agar dapat dibaca. code 'image' merupakan inisialisasi untuk gambar sedangkan 'imread' digunakan untuk membaca gambar. code 'imshow' digunakan untuk menampilkan gambar pada sebuat window baru dengan judul 'Adis'. untuk code 'cv2.waitkey(0)' dimaksudkan untuk menunggu sampai user menekan tombol apapun pada keyboard. sedangkan untuk code 'cv2.destroyAllWindows' digunakan untuk menutup semua jendela yang dibuat oleh OpenCV dan hal ini juga berguna untuk membersihkan dan menghindari penggunaan memori yang tidak perlu setelah gambar ditampilkan.
#### Menaikkan kontras
```bash
alpha = 2 
beta = 0 

new_image = cv2.convertScaleAbs(image, alpha=alpha, beta=beta)
```
  untuk parameter 'alpha' dan 'beta' digunakan untuk mengubah kecerahan dan kontras gambar.
'alpha' digunakan untuk mengontrol nilai kontras.
sedangkan 'beta' digunakan untuk meningkatkan kecerahan.
fungsi dari code 'new_image = cv2.convertScaleAbs(image, alpha=alpha, beta=beta)' digunakan untuk mengubah skala dan  mengkonversi array elemen gambar. dalam halini, 'alpha' adalah 2 dan 'beta' adalah 0. setiap piksel dalam 'image' akan dikali dengan 2. hal ini digunakan untuk meningkatkan kontras gambar.
#### Menampilkan gambar setelah ditingkatkan kontras
```bash
cv2.imwrite('image_contrast.jpg', new_image)
cv2.imshow('Image', new_image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
  Codingan diatas adalah code untuk membaca gambar. code 'cv2.imwrite('image_contrast.jpg', new_image)' digunakan untuk menampilkan gambar pada jendela baru. parameter pertama adalah 'Image' dan parameter kedua adalah 'new_image'. code 'imshow' digunakan untuk menampilkan gambar pada jendela baru dan menampilkan gambar'new_image'. untuk code 'cv2.waitkey(0)' dimaksudkan untuk menunggu sampai user menekan tombol apapun pada keyboard. sedangkan untuk code 'cv2.destroyAllWindows' digunakan untuk menutup semua jendela yang dibuat oleh OpenCV dan hal ini juga berguna untuk membersihkan dan menghindari penggunaan memori yang tidak perlu setelah gambar ditampilkan.

#### Deteksi Tepi
```bash
gray = cv2.cvtColor(new_image, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(new_image, 10, 170)

```
  code pertama dimaksudkan untuk mengkonversi gambar dari rgb ke gray scale. parameter yang dikonversi adalah 'new_image'.
  code kedua adalah code untuk mendeteksi tepi menggunakan algoritma canny. gambar pada parameter 'new_image' yang akan diproses untuk deteksi tepi. parameter kedua dan ketiga adalah nilai ambang batas bawah yaitu 10 dan ambang batas atas adalah 170. 

#### Menampilkan gambar setelah dideteksi tepi
```bash
cv2.imshow("Gambar Adis", edges)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
  code 'edge' merupakan inisialisasi untuk gambar sedangkan 'imread' digunakan untuk membaca gambar. code 'imshow' digunakan untuk menampilkan gambar pada sebuat window baru dengan judul 'Gambar Adis'. untuk code 'cv2.waitkey(0)' dimaksudkan untuk menunggu sampai user menekan tombol apapun pada keyboard. sedangkan untuk code 'cv2.destroyAllWindows' digunakan untuk menutup semua jendela yang dibuat oleh OpenCV dan hal ini juga berguna untuk membersihkan dan menghindari penggunaan memori yang tidak perlu setelah gambar ditampilkan.
#### Menampilkan gambar dengan subplot
  ```bash
fig, axs = plt.subplots(1,2, figsize =(10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap = "gray")
ax[0].set_title("Original Image")

ax[1].imshow(edges, cmap = "gray")
ax[1].set_title("Canny Edge Detection")
  ```
  Fungsi dari 'plt.subplots' digunakan untuk membuat beberapa subplot dalam satu gambar. parameter pertama adalah jumlah baris yaitu 1 dan parameter kedua adalah jumlah kolom yaitu 2 yang berarti akan ada dua subplot dalam satu baris.
untuk code 'ravel' digunakan untuk mengubah array 2D menjadi array 1D.
code 'ax[0].imshow' digunakan untuk menampilkan gabar 'gray' pada subplot pertama. sedangkan untuk code 'ax[1].imshow' digunakan untuk menampilkan gambar 'edges' pada subplot kedua. code 'ax[1].set_title' adalah code untuk menetapkan judul untuk subplotnya. 
#### Deteksi Tepi dengan Transformasi Hough
```bash
lines = cv2.HoughLinesP(edges, 1, np.pi/250, 20, maxLineGap = -50)
image_line = new_image.copy()
```
  Fungsi 'cv2.HoughLinesP' digunakan untuk mendeteksi tepi garis dalam gambar biner. parameter pertama yaitu 'edges' adalah gambar biner yang akan diproses. parameter kedua adalah resolusi rho dalam piksel, sedangkan parameter ketiga adalah resolusi theta dalam radian. untuk parameter keempat adalah ambang batas. sedangkan untuk code 'maxLineGap' adalah jarak maksimum antara dua titik yang dianggap berada pada satu garis yang sama.
  untuk fungsi 'copy()' adalah untuk membuat salinan dari 'new_image'. salinan ini akan digunakann untuk menambahkan dan menampilkan garis garis yang terdeteksi tanpa mengubah gambar asli.

  #### Membuat garis pada gambar
```bash 
for line in lines:
    x1, y1, x2, y2 = line[0]
    cv2.line(image_line, (x1, y1), (x2, y2), (0, 255, 0), 3)
```
  inti dari code ini adalah untuk membuat garis pada gambar yang sebelumnya sudah terdeteksi. garis yang dibuat berwarna hijau karena sebelumnya kita sudah atur untuk membuatnya menjadi hijau. 
#### Menampilkan gambar dalam subplot
```bash
fig, axs = plt.subplots(1, 3, figsize=(15, 5))  
ax = axs.ravel()

ax[0].imshow(gray, cmap="gray")
ax[0].set_title("Original Image")

ax[1].imshow(edges, cmap="gray")
ax[1].set_title("Canny Edges Image")

ax[2].imshow(image_line, cmap="gray")
ax[2].set_title("Contours Image")

plt.show()
```
  Fungsi dari 'plt.subplots' digunakan untuk membuat beberapa subplot dalam satu gambar. parameter pertama adalah jumlah baris yaitu 1 dan parameter kedua adalah jumlah kolom yaitu 2 yang berarti akan ada dua subplot dalam satu baris.
untuk code 'ravel' digunakan untuk mengubah array 2D menjadi array 1D.
code 'ax[0].imshow' digunakan untuk menampilkan gabar 'gray' pada subplot pertama. sedangkan untuk code 'ax[1].imshow' digunakan untuk menampilkan gambar 'edges' pada subplot kedua.
code 'ax[2].imshow' digunakan untuk menampilkan gambar 'image_line' pada subplot ketiga. code 'ax[1].set_title' adalah code untuk menetapkan judul untuk subplotnya. 

#### Teori yang mendukung
  Operator Canny adalah salah satu metode deteksi tepi yang paling populer dan canggih. Algoritma ini dikembangkan oleh John F. Canny pada tahun 1986 dan dirancang untuk menjadi algoritma deteksi tepi yang optimal dalam hal tiga kriteria utama: deteksi yang baik, lokalisasi yang baik, dan hanya satu respon tepi untuk setiap tepi.  Proses deteksi tepi Canny melibatkan beberapa langkah:
1. Pengaburan gambar untuk mengurangi noise menggunakan Gaussian filter.
2. Menghitung gradien intensitas menggunakan operator Sobel atau Prewitt.
3. Non-maximum suppression untuk menipiskan tepi.
4. Hysteresis thresholding untuk menentukan tepi yang sebenarnya berdasarkan dua ambang batas (high threshold dan low threshold).

