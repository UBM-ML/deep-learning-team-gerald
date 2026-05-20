# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 | 1      | 64      | relu       | adam      | 0.01   | 32    | 10     | 0.0     | ~84.34%  | ~52.3s     |
| 2 | 2      | 64      | relu       | adam      | 0.01   | 32    | 10     | 0.0     | ~84.67%  | ~57.2s     |
| 3 | 2      | 128     | relu       | adam      | 0.01   | 32    | 10     | 0.0     | ~84.10%  | ~74.4s     |
| 4 | 2      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85.73%  | ~47s       |
| 5 | 1      | 128     | relu       | sgd       | 0.01   | 32    | 20     | 0.0     | ~86.22%  | ~104.6s    |

> **Eksperimen #0** = baseline (jangan ubah, ini patokan kalian).

---

## 🧪 Detail Setiap Eksperimen

---

### Eksperimen #1

**Apa yang diubah dari baseline:**
> Mengganti optimizer dari `sgd` menjadi `adam`.

**Hipotesis sebelum run:**
> Adam merupakan optimizer adaptif sehingga kami menduga training akan lebih cepat konvergen dan akurasi meningkat.

**Hasil:**
- Test accuracy: ~84.34%
- Train time: ~52.3 detik
- Apakah overfit/underfit? Sedikit underfitting.

**Observasi & Insight:**
> Hasil ternyata lebih rendah dibanding baseline. Kemungkinan learning rate 0.01 terlalu besar untuk optimizer Adam sehingga training menjadi kurang stabil.

**Rencana eksperimen berikutnya:**
> Menambah hidden layer untuk melihat apakah kapasitas model mempengaruhi performa.

---

### Eksperimen #2

**Apa yang diubah:**
> Menambah jumlah hidden layer dari 1 menjadi 2 dengan optimizer Adam.

**Hipotesis:**
> Hidden layer tambahan dapat membantu model mempelajari pola yang lebih kompleks.

**Hasil:**
- Test accuracy: ~84.67%
- Train time: ~57.2 detik
- Apakah overfit/underfit? Masih cenderung underfitting.

**Observasi:**
> Akurasi meningkat sedikit dibanding eksperimen #1, tetapi belum melampaui baseline. Waktu training juga meningkat karena model lebih kompleks.

---

### Eksperimen #3

**Apa yang diubah:**
> Menambah neuron dari 64 menjadi 128 pada model 2 hidden layer dengan Adam.

**Hipotesis:**
> Jumlah neuron lebih besar dapat meningkatkan kemampuan model mengenali pola.

**Hasil:**
- Test accuracy: ~84.10%
- Train time: ~74.4 detik
- Apakah overfit/underfit? Cenderung tidak stabil.

**Observasi:**
> Penambahan neuron tidak meningkatkan akurasi. Training menjadi lebih lama dan kemungkinan learning rate terlalu besar sehingga optimizer kesulitan mencapai konvergensi optimal.

---

### Eksperimen #4

**Apa yang diubah:**
> Menggunakan optimizer SGD kembali dengan 2 hidden layer dan 64 neuron.

**Hipotesis:**
> SGD mungkin lebih stabil pada learning rate 0.01 dibanding Adam.

**Hasil:**
- Test accuracy: ~85.73%
- Train time: ~47 detik
- Apakah overfit/underfit? Tidak signifikan.

**Observasi:**
> Hasil meningkat dibanding eksperimen Adam sebelumnya dan sedikit lebih baik dari baseline. SGD terlihat lebih stabil untuk konfigurasi learning rate ini.

---

### Eksperimen #5

**Apa yang diubah:**
> Menambah neuron menjadi 128 dan epoch menjadi 20 menggunakan SGD.

**Hipotesis:**
> Epoch lebih banyak memberi model waktu belajar lebih lama sehingga akurasi meningkat.

**Hasil:**
- Test accuracy: ~86.22%
- Train time: ~104.6 detik
- Apakah overfit/underfit? Sedikit mulai overfit tetapi masih wajar.

**Observasi:**
> Ini menjadi hasil terbaik dari seluruh eksperimen. Penambahan epoch membantu model belajar lebih optimal walaupun waktu training meningkat cukup besar.

---

## 🏆 Konfigurasi Terbaik

```python
HIDDEN_LAYERS     = 1
NEURONS_PER_LAYER = 128
ACTIVATION        = 'relu'
DROPOUT_RATE      = 0.0
OPTIMIZER         = 'sgd'
LEARNING_RATE     = 0.01
BATCH_SIZE        = 32
EPOCHS            = 20
