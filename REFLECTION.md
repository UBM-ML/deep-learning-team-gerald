# Refleksi Tim

> Jawaban dalam Bahasa Indonesia. Maksimal 1 halaman (~500 kata). Yang dinilai adalah **kedalaman pemahaman**, bukan panjang tulisan.

---

## 1. Parameter vs Hyperparameter

Berdasarkan eksperimen yang kalian lakukan, jelaskan dengan **kata-kata kalian sendiri**:
- Apa yang termasuk **parameter** dalam model kalian, dan apa yang termasuk **hyperparameter**?
- Manakah yang berubah saat training berjalan, dan manakah yang ditentukan oleh kalian sebelum training?

**Jawaban:**
> Parameter adalah nilai yang dipelajari otomatis oleh model selama training, yaitu bobot (weights) dan bias pada setiap neuron. Nilai parameter berubah terus saat proses feed forward dan back propagation berjalan untuk meminimalkan loss.  
>
> Hyperparameter adalah pengaturan yang ditentukan sebelum training dimulai, seperti jumlah hidden layer, jumlah neuron, activation function, optimizer, learning rate, batch size, epoch, dan dropout. Hyperparameter tidak dipelajari otomatis oleh model, tetapi dipilih oleh kami untuk mengontrol cara model belajar.  
>
> Jadi, parameter berubah selama training berlangsung, sedangkan hyperparameter ditentukan oleh kami sebelum training dimulai.

---

## 2. Hyperparameter dengan Dampak Terbesar

Dari semua hyperparameter yang kalian eksperimen, mana yang menurut kalian memberikan **dampak paling besar** terhadap akurasi? Mengapa demikian — apa yang kalian amati pada kurva loss/accuracy?

**Jawaban:**
> Hyperparameter yang paling berdampak menurut kami adalah optimizer dan jumlah neuron/layer. Saat optimizer diubah dari SGD menjadi Adam, akurasi meningkat cukup besar dan kurva loss turun lebih cepat serta lebih stabil. Adam mampu menyesuaikan learning rate secara adaptif sehingga proses training lebih efisien.  
>
> Penambahan neuron dan hidden layer juga meningkatkan akurasi karena model dapat mempelajari pola yang lebih kompleks. Pada kurva accuracy terlihat train dan validation accuracy meningkat lebih cepat dibanding baseline. Namun jika neuron terlalu banyak, gap antara train dan validation mulai membesar sehingga muncul tanda overfitting.

---

## 3. Learning Rate

Coba set `LEARNING_RATE = 1.0` (atau bahkan lebih besar) dan jalankan sekali. Apa yang terjadi pada kurva loss? Hubungkan jawaban kalian dengan rumus:

$$W_j = W_j - \lambda \frac{\partial F(W_j)}{\partial W_j}$$

**Jawaban:**
> Saat learning rate diatur menjadi 1.0, kurva loss menjadi tidak stabil dan bahkan bisa meningkat sangat besar. Accuracy juga sulit naik karena proses update bobot terlalu ekstrem.  
>
> Pada rumus:
>
> $begin:math:display$
W\_j \= W\_j \- \\lambda \\frac\{\\partial F\(W\_j\)\}\{\\partial W\_j\}
$end:math:display$
>
> nilai λ (learning rate) mengontrol seberapa besar perubahan bobot setiap iterasi. Jika λ terlalu besar, update bobot akan “melompat-lompat” melewati titik minimum sehingga model gagal konvergen. Karena itu learning rate harus dipilih dengan hati-hati agar training stabil.

---

## 4. Batch Size & Trade-off

Bandingkan eksperimen dengan **batch size kecil** (misal 16) vs **batch size besar** (misal 256). Apa yang kalian amati dari sisi:
- Waktu training?
- Stabilitas kurva loss?
- Akurasi akhir?

Apakah pengamatan ini sesuai dengan teori di slide kuliah?

**Jawaban:**
> Batch size kecil membuat training lebih lambat karena update dilakukan lebih sering. Kurva loss terlihat lebih “berisik” atau tidak stabil, tetapi kadang menghasilkan generalisasi yang lebih baik.  
>
> Batch size besar membuat training lebih cepat dan kurva loss lebih halus karena gradien dihitung dari lebih banyak data sekaligus. Namun jika terlalu besar, model kadang kurang optimal dalam generalisasi sehingga akurasi akhir sedikit lebih rendah.  
>
> Pengamatan ini sesuai dengan teori di slide kuliah bahwa batch size kecil memberikan noise yang membantu generalisasi, sedangkan batch size besar lebih stabil dan efisien secara komputasi.

---

## 5. Feed Forward & Back Propagation

Pada saat kalian menekan `model.fit(...)`, sebenarnya proses feed forward dan back propagation berjalan **ribuan kali**. Hitung kira-kira berapa kali back propagation terjadi pada salah satu eksperimen kalian.

> Petunjuk: `(jumlah_sample_training / batch_size) × epochs`

Jelaskan apa yang terjadi pada **bobot** dan **bias** model kalian di antara iterasi pertama dan terakhir.

**Jawaban:**
> Pada eksperimen terbaik kami:
>
> - Jumlah sample training = 54.000 (karena 10% dipakai validation)
> - Batch size = 64
> - Epoch = 20
>
> Maka jumlah back propagation kira-kira:
>
> $begin:math:display$
\\left\(\\frac\{54000\}\{64\}\\right\) \\times 20 \\approx 16880
$end:math:display$
>
> Jadi back propagation terjadi sekitar 16.880 kali.  
>
> Pada iterasi awal, bobot dan bias masih acak sehingga prediksi model buruk. Setelah ribuan iterasi, bobot dan bias terus diperbarui menggunakan gradient descent sehingga loss menurun dan accuracy meningkat. Di akhir training, parameter model menjadi lebih optimal dalam mengenali pola pada dataset.

---

## 6. Kapan Deep Learning Tepat Digunakan?

Berdasarkan pengalaman kalian dengan Fashion-MNIST, menurut kalian apakah masalah ini *benar-benar* membutuhkan deep learning, atau bisa diselesaikan dengan machine learning klasik (misal Logistic Regression atau Random Forest)? Beri argumen.

**Jawaban:**
> Menurut kami, Fashion-MNIST masih bisa diselesaikan menggunakan machine learning klasik seperti Logistic Regression atau Random Forest karena ukuran gambar relatif kecil dan jumlah kelas hanya 10.  
>
> Namun deep learning memberikan keunggulan karena mampu mempelajari representasi fitur secara otomatis tanpa feature engineering manual. Deep learning juga lebih mudah dikembangkan untuk dataset gambar yang lebih kompleks.  
>
> Jadi untuk kasus sederhana, machine learning klasik mungkin sudah cukup, tetapi deep learning lebih fleksibel dan powerful untuk skala besar serta data yang lebih rumit.

---

## 7. Refleksi Tim

- Tantangan apa yang paling sulit?
- Apa pelajaran terpenting yang kalian dapat dari aktivitas ini?
- Jika diberi waktu lebih, apa yang ingin kalian coba lagi?

**Jawaban:**
> Tantangan paling sulit adalah menentukan kombinasi hyperparameter yang optimal karena perubahan kecil dapat memberikan hasil yang berbeda cukup besar. Kami juga perlu memahami apakah model mengalami overfitting atau underfitting dari kurva loss dan accuracy.  
>
> Pelajaran terpenting yang kami dapat adalah bahwa hyperparameter sangat mempengaruhi performa model deep learning. Kami juga belajar bahwa akurasi tinggi saja tidak cukup; generalisasi model juga penting.  
>
> Jika diberi waktu lebih, kami ingin mencoba activation function lain seperti ELU atau SELU, menambah hidden layer, menggunakan learning rate scheduler, dan mencoba arsitektur CNN agar performa pada data gambar menjadi lebih baik.
