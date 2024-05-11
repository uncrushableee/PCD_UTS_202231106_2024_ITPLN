
# Project UTS

Nama: Achmad Farhan Islamy 

nim : 202231106

untuk membuat project ini kita perlu mengimport gambar dengan cara:

import cv2
import numpy as np
from matplotlib import pyplot as plt

penjelasan:
- OpenCV (cv2): Pustaka yang kuat untuk pemrosesan gambar secara real-time.
- NumPy (np): Pustaka fundamental untuk komputasi ilmiah yang menyediakan array dan fungsi matematika untuk keperluan pemrosesan gambar.
- Matplotlib (plt): Pustaka populer untuk membuat visualisasi seperti plot dan gambar di Python.

import cv2
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.image as img

%matplotlib inline

penjelasan:
- Gambar dibaca menggunakan fungsi cv2.imread dari OpenCV.
- Kanal warna (merah, hijau, biru) dipisahkan dari citra warna menggunakan pengindeksan pada array NumPy.
- Kanal warna individual (merah, hijau, biru) ditampilkan sebagai plot terpisah menggunakan Matplotlib.
- ini commend yang berfungsi untuk menampilkan output secara langsung (%matplotlib inline)

color_image = img.imread('frhn.jpeg')
plt.imshow(color_image)

penjelasan:
- memanggil foto/gambar yang ada pada folder (img.imread)
- menampilkan gambar yang telah dipanggil (plt.imshow)

# DETEKSI WARNA PADA CITRA
r = color_image[:, :, 0] 
g = color_image[:, :, 1] 
b = color_image[:, :, 2]

f, (c1, c2, c3, c4) = plt.subplots(1, 4, figsize = (20,10))

c1.set_title('GAMBAR ASLI')
c1.imshow(color_image) 
c1.axis('off')

c2.set_title('MERAH') 
c2.imshow(r, cmap="gray") 
c2.axis('off')

c3.set_title('HIJAU') 
c3.imshow(g, cmap="gray") 
c3.axis('off')

c4.set_title('BIRU') 
c4.imshow(b, cmap="gray")
c4.axis('off')

penjelasan:
-color_image adalah sebuah array numpy yang mewakili gambar berwarna Anda.
- Pemotongan dengan [:, :, n] memilih semua baris ([:, :]) dan semua kolom ([:, :]) untuk kanal warna tertentu n.
n = 0 menunjukkan kanal merah.
n = 1 menunjukkan kanal hijau.
n = 2 menunjukkan kanal biru.
- plt.subplots(1, 4, figsize = (20,10)) membuat sebuah figure (f) dengan satu baris (1) yang berisi empat subplot (4) dan mengatur ukuran figure menjadi lebar 20 inci dan tinggi 10 inci.
- Pembongkaran (c1, c2, c3, c4) menetapkan subplot individual ke variabel c1 sampai c4 untuk memudahkan pemanggilan nanti.
- c1.set_title('GAMBAR ASLI') memberi judul 'GAMBAR ASLI' pada subplot ke-1.
- c1.imshow(color_image) menampilkan gambar asli pada subplot ke-1.
- c1.axis('off') menyembunyikan axis (sumbu) pada subplot ke-1. Proses serupa dilakukan pada subplot ke-2 sampai ke-4, dengan menampilkan gambar hasil pemisahan kanal merah (r), hijau (g), dan biru (b) masing-masing, serta diberi judul sesuai kanalnya. Perhatikan penggunaan cmap="gray" untuk menampilkan gambar kanal warna yang biasanya berupa skala abu-abu.
- c2.axis('off') sampai c4.axis('off') juga menyembunyikan axis pada subplot ke-2 sampai ke-4.

# Teori Terkait: Representasi Warna dalam Gambar Digital
Gambar digital umumnya disimpan dalam format RGB (Red, Green, Blue). Setiap piksel dalam gambar RGB memiliki tiga nilai yang merepresentasikan intensitas warna merah, hijau, dan biru. Intensitas ini biasanya berupa nilai antara 0 (hitam) sampai 255 (putih). Dengan mengkombinasikan ketiga warna tersebut, terbentuklah spektrum warna yang luas untuk menampilkan objek dalam gambar. [Sumber: R. Gonzalez dan R. E. Woods, "Digital Image Processing," Pearson Education, 2008]

# MENAMPILKAN HISTOGRAM
color_image = cv2.imread('frhn.jpeg')
color_image = cv2.cvtColor(color_image, cv2.COLOR_BGR2RGB)
histogram_biru = cv2.calcHist([b], [0], None, [256], [0, 256])
histogram_hijau = cv2.calcHist([g],[0], None,[256],[0,256])
histogram_merah = cv2.calcHist([r], [0], None,[256],[0,256])
histogram_warna = cv2.calcHist([color_image], [0,1,2],None, [256, 256, 256], [0, 256, 0, 256, 0, 256])

penjelasan:
- library OpenCV (cv2.imread) untuk membaca gambar dari file 'frhn.jpeg' dan menyimpannya ke dalam variable color_image.
- OpenCV secara default menggunakan format warna BGR (Biru, Hijau, Merah). Baris ini mengkonversi format warna gambar dari BGR ke RGB (Merah, Hijau, Biru) menggunakan fungsi cv2.cvtColor agar sesuai dengan pemrosesan selanjutnya.
- pada line ini histogram untuk setiap kanal warna (biru, hijau, merah) secara terpisah.
- cv2.calcHist adalah fungsi untuk menghitung histogram.
1. Parameter pertama [b], [g], dan [r] merujuk pada array berisi masing-masing kanal warna (biru, hijau, merah) yang sebelumnya telah dipisahkan menggunakan kode yang Anda berikan sebelumnya.
2. Parameter kedua [0] menunjukkan bahwa histogram hanya dihitung untuk channel ke-0 (dalam hal ini indeks 0 merujuk pada kanal warna yang dimasukkan pada parameter pertama).
3. Parameter ketiga None menunjukkan tidak digunakannya mask (penutup area tertentu pada gambar).
4. Parameter keempat [256] mendefinisikan jumlah bin (interval) dalam histogram, yaitu 256 (sesuai dengan skala warna 0-255).
5. Parameter kelima [0, 256] mendefinisikan range nilai untuk bin, yaitu dari 0 sampai 255 (sesuai dengan skala warna).


plt.figure(figsize=(12, 8))

plt.subplot (2, 2, 3) 
plt.plot(histogram_merah, color='r')
plt.title( 'HISTOSGRAM MERAH')
plt.xlim([0, 256])

plt.subplot(2, 2, 1) 
plt.plot(histogram_biru, color='b')
plt.title( 'HISTOGRAM BIRU')
plt.xlim([0, 256])

plt.subplot (2, 2, 2)
plt.plot(histogram_hijau, color='g')
plt.title( 'HISTOGRAM HIJAU')
plt.xlim([0, 256])

plt.subplot (2, 2, 4)
plt.plot(histogram_warna.flatten(), color='gray')
plt.title('HISTOSGRAM WARNA')
plt.xlim([0, 256])

penjelasan:
- plt.figure menggunakan fungsi plt.figure dari Matplotlib.
- Parameter figsize=(12, 8) mengatur lebar figure menjadi 12 inci dan tingginya menjadi 8 inci.
- subplot dalam figure dan menampilkan histogram untuk setiap kanal warna (merah, hijau, biru).
- plt.subplot(2, 2, 3) membuat subplot pada posisi ke-3 dalam grid subplot 2x2.
- plt.plot(histogram_merah, color='r') memplot histogram kanal merah menggunakan garis merah.
- plt.title('HISTOSGRAM MERAH') mengatur judul subplot menjadi "HISTOSGRAM MERAH".
- plt.xlim([0, 256]) mengatur batas sumbu x dari 0 hingga 255, sesuai dengan rentang intensitas piksel yang mungkin. Langkah serupa dilakukan untuk histogram kanal biru dan hijau di subplot yang sesuai.
- histogram_warna ini menampilkan histogram untuk keseluruhan gambar RGB.
- plt.subplot(2, 2, 4) membuat subplot pada posisi ke-4 dalam grid subplot 2x2.
- histogram_warna.flatten() mengubah bentuk array histogram 3D menjadi array 1D yang sesuai untuk plotting.
- plt.plot(histogram_warna.flatten(), color='gray') memplot histogram yang telah diratakan menggunakan garis abu-abu.
- plt.title('HISTOSGRAM WARNA') mengatur judul subplot menjadi "HISTOSGRAM WARNA".
- plt.xlim([0, 256]) mengatur batas sumbu x dari 0 hingga 256, sama seperti histogram kanal individual.

# Teori Terkait: Analisis Citra dengan Histogram
Histogram merupakan representasi grafis dari distribusi intensitas pixel pada gambar. Sumbu horizontal menampilkan level intensitas (0-255), sedangkan sumbu vertikal menampilkan jumlah pixel yang memiliki intensitas tersebut. Analisa histogram berguna untuk memahami distribusi warna pada gambar, membantu dalam proses segmentasi objek, dan koreksi intensitas citra. [Sumber: L. Shapiro dan J. P. Hacker, "Computer Vision: Theory and Applications," Springer Science+Business Media, 2001]


# MENAMPILKAN HASIL

import cv2
import numpy as np
from matplotlib import pyplot as plt
def make_image_invisible(image):
    height, width = image.shape[:2]
    return np.zeros((height, width, 3), dtype=np.uint8)

def increase_brightness(image, value=30):
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    h, s, v = cv2.split(hsv)
    v += value
    v = np.clip(v, 0, 255)
    final_hsv = cv2.merge((h, s, v))
    return cv2.cvtColor(final_hsv, cv2.COLOR_HSV2BGR)

def detect_and_highlight_blue(image):
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    lower_blue = np.array([100, 50, 50])
    upper_blue = np.array([130, 255, 255])
    blue_mask = cv2.inRange(hsv, lower_blue, upper_blue)
    
    result = cv2.bitwise_and(image, image, mask=blue_mask)
    return result

def detect_and_highlight_red_blue(image):
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    lower_red1 = np.array([0, 50, 50])
    upper_red1 = np.array([10, 255, 255])
    red_mask1 = cv2.inRange(hsv, lower_red1, upper_red1)
    lower_red2 = np.array([170, 50, 50])
    upper_red2 = np.array([180, 255, 255])
    red_mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
    red_mask = cv2.bitwise_or(red_mask1, red_mask2)
    
    lower_blue = np.array([100, 50, 50])
    upper_blue = np.array([130, 255, 255])
    blue_mask = cv2.inRange(hsv, lower_blue, upper_blue)
    
    combined_mask = cv2.bitwise_or(red_mask, blue_mask)
    result = cv2.bitwise_and(image, image, mask=combined_mask)
    return result

def detect_and_highlight_red_green_blue(image):
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    lower_red1 = np.array([0, 50, 50])
    upper_red1 = np.array([10, 255, 255])
    red_mask1 = cv2.inRange(hsv, lower_red1, upper_red1)
    lower_red2 = np.array([170, 50, 50])
    upper_red2 = np.array([180, 255, 255])
    red_mask2 = cv2.inRange(hsv, lower_red2, upper_red2)
    red_mask = cv2.bitwise_or(red_mask1, red_mask2)
    
    lower_green = np.array([40, 50, 50])
    upper_green = np.array([200, 255, 255])
    green_mask = cv2.inRange(hsv, lower_green, upper_green)
    
    lower_blue = np.array([100, 50, 50])
    upper_blue = np.array([130, 255, 255])
    blue_mask = cv2.inRange(hsv, lower_blue, upper_blue)
    
    combined_mask = cv2.bitwise_or(red_mask, cv2.bitwise_or(green_mask, blue_mask))
    result = cv2.bitwise_and(image, image, mask=combined_mask)
    return result

image = cv2.imread('frhn.jpeg')
invisible_image = make_image_invisible(image)
brightened_image = increase_brightness(image)
blue_detection = detect_and_highlight_blue(brightened_image)
red_blue_detection = detect_and_highlight_red_blue(brightened_image)
red_green_blue_detection = detect_and_highlight_red_green_blue(brightened_image)

plt.figure(figsize=(10, 8))

plt.subplot(221), plt.imshow(cv2.cvtColor(invisible_image, cv2.COLOR_BGR2RGB)), plt.title('Invisible Image')
plt.subplot(222), plt.imshow(cv2.cvtColor(blue_detection, cv2.COLOR_BGR2RGB)), plt.title('Blue Color Detection')
plt.subplot(223), plt.imshow(cv2.cvtColor(red_blue_detection, cv2.COLOR_BGR2RGB)), plt.title('Red-Blue Color Detection')
plt.subplot(224), plt.imshow(cv2.cvtColor(red_green_blue_detection, cv2.COLOR_BGR2RGB)), plt.title('Red-Green-Blue Color Detection')

plt.show()

penjelasan:

> -Kode mengimpor library OpenCV (cv2) untuk pemrosesan gambar, library NumPy (numpy) untuk komputasi numerik, dan Matplotlib (plt) untuk visualisasi.

> -make_image_invisible(image): Fungsi ini membuat gambar baru dengan ukuran yang sama seperti gambar asli (image), namun seluruh pixel diisi warna hitam (nilai 0). Hasilnya adalah gambar yang seolah-olah tidak terlihat.

> -increase_brightness(image, value=30): Fungsi ini meningkatkan kecerahan gambar. Konversi gambar ke ruang warna HSV (Hue, Saturation, Value) dilakukan terlebih dahulu. Nilai pada channel Value dinaikkan sebesar value (default 30) dan kemudian dibatasi antara 0 sampai 255 (batas intensitas piksel). Terakhir, gambar dikonversi kembali ke ruang warna BGR (default OpenCV) sebelum dikembalikan.

> -detect_and_highlight_blue(image): Fungsi ini mendeteksi dan menyorot objek berwarna biru pada gambar.

- Konversi gambar ke ruang warna HSV dilakukan terlebih dahulu.
- Batas warna biru bawah (lower_blue) dan atas (upper_blue) ditetapkan berdasarkan nilai Hue, Saturation, dan Value.
- Fungsi cv2.inRange digunakan untuk membuat mask (penutup) yang hanya menyeleksi area gambar yang berada dalam rentang warna biru yang ditentukan.
- Terakhir, fungsi cv2.bitwise_and digunakan untuk "menyorot" objek biru dengan cara mengalikan gambar asli dengan mask, sehingga hanya bagian yang berwarna biru yang terlihat jelas, sedangkan area lainnya menjadi gelap.

> -detect_and_highlight_red_blue(image): Fungsi ini mendeteksi dan menyorot objek berwarna merah dan biru pada gambar. Prosesnya serupa dengan fungsi detect_and_highlight_blue, namun menggunakan dua mask terpisah untuk warna merah (dua rentang Hue yang berbeda) dan biru. Mask kemudian digabungkan menggunakan cv2.bitwise_or sebelum digunakan untuk "menyorot" objek berwarna merah dan biru pada gambar asli.

> -detect_and_highlight_red_green_blue(image): Fungsi ini mendeteksi dan menyorot objek berwarna merah, hijau, dan biru pada gambar. Prosesnya serupa dengan fungsi sebelumnya, namun menambahkan mask untuk warna hijau. Mask untuk masing-masing warna digabungkan sebelum digunakan untuk "menyorot" objek berwarna merah, hijau, dan biru pada gambar asli.

> -pembacaan gambar asli (image) dari file 'frhn.jpeg'.
> -Selanjutnya, berbagai fungsi manipulasi gambar diaplikasikan:
- invisible_image menyimpan hasil fungsi make_image_invisible (gambar tidak terlihat).
- brightened_image menyimpan hasil fungsi increase_brightness (gambar dengan kecerahan dinaikkan).
- blue_detection,'

# Teori Terkait: Ruang Warna HSV dan Deteksi Warna
Ruang warna HSV lebih intuitif untuk deteksi warna dibandingkan dengan RGB. Hue merepresentasikan warna (misalnya merah pada sudut 0), Saturation menunjukkan saturasi warna (0 untuk abu-abu, 255 untuk warna murni), dan Value menunjukkan kecerahan warna. Dengan memanipulasi nilai Hue, Saturation, dan Value, kita dapat melakukan deteksi warna secara lebih selektif. [Sumber: A. K. Jain, "Fundamentals of Digital Image Processing," Springer Science+Business Media, 1989].

























