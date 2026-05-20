# Refleksi Tim

> Jawaban dalam Bahasa Indonesia. Maksimal 1 halaman (~500 kata). Yang dinilai adalah **kedalaman pemahaman**, bukan panjang tulisan.

---

## 1. Parameter vs Hyperparameter

Berdasarkan eksperimen yang kalian lakukan, jelaskan dengan **kata-kata kalian sendiri**:
- Apa yang termasuk **parameter** dalam model kalian, dan apa yang termasuk **hyperparameter**?
- Manakah yang berubah saat training berjalan, dan manakah yang ditentukan oleh kalian sebelum training?

**Jawaban:**
> **Parameter** adalah nilai yang dipelajari dan diperbarui secara otomatis oleh model dari data selama *training* berlangsung (contoh: bobot/weights dan bias pada neuron). Sedangkan **Hyperparameter** adalah pengaturan yang kita tentukan manual sebelum *training* dimulai (contoh: jenis *optimizer*, *learning rate*, jumlah *hidden layer*, jumlah *neuron*, *batch size*, *epoch*, dan nilai *dropout*). 
> 
> Kesimpulannya: Parameter **berubah** saat *training* berjalan, sedangkan *hyperparameter* **ditentukan sebelum** *training* dan nilainya tetap selama proses tersebut.

---

## 2. Hyperparameter dengan Dampak Terbesar

Dari semua hyperparameter yang kalian eksperimen, mana yang menurut kalian memberikan **dampak paling besar** terhadap akurasi? Mengapa demikian — apa yang kalian amati pada kurva loss/accuracy?

**Jawaban:**
> Mengubah **Optimizer** (dari SGD ke Adam) memberikan dampak terbesar. Pada Eksperimen #1, akurasi langsung naik signifikan (~85% ke ~88%) tanpa mengubah arsitektur model sama sekali. Pada kurva *loss* dan *accuracy*, penggunaan Adam membuat penurunan *loss* jauh lebih cepat, tajam, dan stabil sejak *epoch-epoch* awal karena Adam memiliki mekanisme adaptif untuk menyesuaikan *learning rate* pada tiap parameter secara otomatis.

---

## 3. Learning Rate

Coba set `LEARNING_RATE = 1.0` (atau bahkan lebih besar) dan jalankan sekali. Apa yang terjadi pada kurva loss? Hubungkan jawaban kalian dengan rumus:

$$W_j = W_j - \lambda \frac{\partial F(W_j)}{\partial W_j}$$

**Jawaban:**
> Jika `LEARNING_RATE = 1.0`, kurva *loss* akan sangat berosilasi (naik-turun secara ekstrem) atau bahkan *diverging* (menghasilkan nilai NaN) dan gagal konvergen. 
> 
> Berdasarkan rumus di atas, $\lambda$ merepresentasikan *learning rate*. Jika nilai $\lambda$ terlalu besar (1.0), langkah pengurangan atau penambahan bobot ($W_j$) menjadi terlalu drastis. Akibatnya, model akan terus-menerus melompati (*overshooting*) titik minimum *loss* yang ideal dan tidak akan bisa menemukan titik konvergensi yang tepat.

---

## 4. Batch Size & Trade-off

Bandingkan eksperimen dengan **batch size kecil** (misal 16) vs **batch size besar** (misal 256). Apa yang kalian amati dari sisi:
- Waktu training?
- Stabilitas kurva loss?
- Akurasi akhir?

Apakah pengamatan ini sesuai dengan teori di slide kuliah?

**Jawaban:**
> 1. **Waktu training:** *Batch size* kecil membuat waktu *training* lebih lambat per *epoch* karena pembaruan bobot terjadi sangat sering. *Batch size* besar jauh lebih cepat karena mengoptimalkan komputasi paralel pada memori.
> 2. **Stabilitas kurva loss:** Kurva pada *batch size* kecil sangat fluktuatif/berisik. Pada *batch size* besar, pergerakan kurva jauh lebih stabil dan mulus.
> 3. **Akurasi akhir:** *Batch size* yang moderat (misal 64) memberikan generalisasi terbaik. Terlalu besar berisiko terjebak di *local minima*, terlalu kecil rentan *overfitting*.
> 
> Pengamatan ini sangat sesuai dengan teori *trade-off* di kuliah: efisiensi waktu komputasi berbanding terbalik dengan kualitas konvergensi.

---

## 5. Feed Forward & Back Propagation

Pada saat kalian menekan `model.fit(...)`, sebenarnya proses feed forward dan back propagation berjalan **ribuan kali**. Hitung kira-kira berapa kali back propagation terjadi pada salah satu eksperimen kalian.

> Petunjuk: `(jumlah_sample_training / batch_size) × epochs`

Jelaskan apa yang terjadi pada **bobot** dan **bias** model kalian di antara iterasi pertama dan terakhir.

**Jawaban:**
> Asumsi dataset Fashion-MNIST memiliki 60.000 sampel latih. Menggunakan konfigurasi terbaik kami (Batch size = 64, Epochs = 20):
> **Jumlah iterasi = (60.000 / 64) × 20 = 937.5 × 20 = 18.750 kali.**
> 
> Di iterasi pertama, nilai bobot dan bias diinisialisasi secara acak, sehingga prediksi awal model sangat buruk. Melalui 18.750 kali siklus *feed forward* dan *back propagation*, model menghitung error dan terus mengoreksi/memperbarui nilai bobot dan bias tersebut sedikit demi sedikit. Pada iterasi terakhir, bobot dan bias telah terkalibrasi secara optimal untuk mengenali pola khusus pada gambar dengan *loss* seminimal mungkin.

---

## 6. Kapan Deep Learning Tepat Digunakan?

Berdasarkan pengalaman kalian dengan Fashion-MNIST, menurut kalian apakah masalah ini *benar-benar* membutuhkan deep learning, atau bisa diselesaikan dengan machine learning klasik (misal Logistic Regression atau Random Forest)? Beri argumen.

**Jawaban:**
> Kasus klasifikasi gambar Fashion-MNIST sebenarnya bisa diselesaikan oleh *Machine Learning* klasik (seperti Random Forest atau SVM) dengan akurasi yang cukup baik, asalkan dilakukan *feature engineering* manual. Namun, *Deep Learning* menjadi **sangat tepat digunakan** di sini karena kemampuannya mengekstrak fitur hierarkis (seperti tekstur, bentuk, tepi pakaian) secara otomatis langsung dari piksel mentah. Hal ini membuat *Deep Learning* mampu menembus batas akurasi ML klasik (mencapai ~90%) dengan prapemrosesan data yang jauh lebih efisien.

---

## 7. Refleksi Tim

- Tantangan apa yang paling sulit?
- Apa pelajaran terpenting yang kalian dapat dari aktivitas ini?
- Jika diberi waktu lebih, apa yang ingin kalian coba lagi?

**Jawaban:**
> - **Tantangan tersulit:** Menemukan keseimbangan (*sweet spot*) agar model tidak *overfitting*. Saat kami menambah neuron, akurasi *train* naik drastis tapi akurasi validasi tertinggal, sehingga kami harus melakukan *tuning* menggunakan *Dropout*.
> - **Pelajaran terpenting:** *Hyperparameter* sangat bergantung satu sama lain. Mengubah *batch size* ternyata menuntut penyesuaian jumlah *epoch* agar model bisa belajar dengan optimal.
> - **Jika diberi waktu lebih:** Kami ingin mencoba arsitektur *Convolutional Neural Network* (CNN) karena secara teori jauh lebih tangguh untuk mengekstrak fitur spasial pada data citra dibandingkan model *Dense* (MLP) biasa.
