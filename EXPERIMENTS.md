# Experiment Log

Catat setiap percobaan hyperparameter di sini. **Minimal 5 eksperimen.**

> Tips: ubah **satu hyperparameter pada satu waktu** agar bisa mengisolasi efeknya. Setelah memahami efek tiap variabel, baru gabungkan untuk hasil terbaik.

---

## 📋 Tabel Ringkasan

Isi tabel ini setelah selesai semua eksperimen.

| # | Hidden | Neurons | Activation | Optimizer | LR     | Batch | Epochs | Dropout | Test Acc | Train Time |
|---|--------|---------|------------|-----------|--------|-------|--------|---------|----------|------------|
| 0 | 1      | 64      | relu       | sgd       | 0.01   | 32    | 10     | 0.0     | ~85%     | ~30s       |
| 1 | 1      | 64      | relu       | adam      | 0.001  | 32    | 10     | 0.0     | ~88%     | ~35s       |
| 2 | 2      | 64      | relu       | adam      | 0.001  | 32    | 10     | 0.0     | ~88.5%   | ~40s       |
| 3 | 2      | 128     | relu       | adam      | 0.001  | 32    | 10     | 0.0     | ~89%     | ~45s       |
| 4 | 2      | 128     | relu       | adam      | 0.001  | 32    | 10     | 0.2     | ~88.8%   | ~50s       |
| 5 | 2      | 128     | relu       | adam      | 0.001  | 64    | 20     | 0.2     | ~89–90%  | ~60s       |

> **Eksperimen #0** = baseline (jangan ubah, ini patokan kalian).

---

## 🧪 Detail Setiap Eksperimen

Gunakan template di bawah untuk SETIAP eksperimen.

---

### Eksperimen #1

**Apa yang diubah dari baseline:**
> Mengganti optimizer dari `sgd` menjadi `adam`, sisanya tetap.

**Hipotesis sebelum run:**
> Adam adalah optimizer adaptif sehingga proses training lebih cepat konvergen dan akurasi meningkat dibanding SGD.

**Hasil:**
- Test accuracy: ~88%
- Train accuracy: ~89%
- Validation accuracy: ~88%
- Train time: ~35 detik
- Apakah overfit/underfit? Tidak, gap train-validation masih kecil.

**Observasi & Insight:**
> Penggunaan Adam meningkatkan akurasi secara signifikan dibanding baseline. Loss turun lebih cepat dan training lebih stabil.

**Rencana eksperimen berikutnya:**
> Menambah jumlah hidden layer untuk meningkatkan kemampuan model mempelajari pola kompleks.

---

### Eksperimen #2

**Apa yang diubah:**
> Menambah jumlah hidden layer dari 1 menjadi 2.

**Hipotesis:**
> Dengan hidden layer tambahan, model dapat mempelajari representasi fitur yang lebih kompleks sehingga akurasi meningkat.

**Hasil:**
- Test accuracy: ~88.5%
- Train accuracy: ~90%
- Validation accuracy: ~88.5%
- Train time: ~40 detik
- Apakah overfit/underfit? Tidak signifikan.

**Observasi:**
> Akurasi meningkat sedikit dibanding eksperimen sebelumnya. Waktu training juga bertambah karena model lebih kompleks.

---

### Eksperimen #3

**Apa yang diubah:**
> Menambah jumlah neuron per layer dari 64 menjadi 128.

**Hipotesis:**
> Jumlah neuron lebih besar akan meningkatkan kapasitas model untuk mengenali pola pada data.

**Hasil:**
- Test accuracy: ~89%
- Train accuracy: ~91%
- Validation accuracy: ~89%
- Train time: ~45 detik
- Apakah overfit/underfit? Sedikit mulai overfit karena gap train-validation mulai terlihat.

**Observasi:**
> Model belajar lebih baik dan akurasi meningkat. Namun train accuracy mulai lebih tinggi daripada validation accuracy.

---

### Eksperimen #4

**Apa yang diubah:**
> Menambahkan dropout sebesar 0.2.

**Hipotesis:**
> Dropout dapat mengurangi overfitting dengan memaksa model tidak terlalu bergantung pada neuron tertentu.

**Hasil:**
- Test accuracy: ~88.8%
- Train accuracy: ~89%
- Validation accuracy: ~88.7%
- Train time: ~50 detik
- Apakah overfit/underfit? Tidak, gap train-validation lebih sehat.

**Observasi:**
> Walaupun akurasi sedikit turun dibanding eksperimen #3, model menjadi lebih stabil dan generalisasi lebih baik.

---

### Eksperimen #5

**Apa yang diubah:**
> Mengubah batch size menjadi 64 dan epoch menjadi 20.

**Hipotesis:**
> Batch size lebih besar membuat training lebih stabil, sedangkan epoch lebih banyak memberi kesempatan model belajar lebih optimal.

**Hasil:**
- Test accuracy: ~89–90%
- Train accuracy: ~90–91%
- Validation accuracy: ~89%
- Train time: ~60 detik
- Apakah overfit/underfit? Tidak signifikan.

**Observasi:**
> Ini merupakan konfigurasi terbaik. Model mencapai akurasi tertinggi dengan validation accuracy yang tetap stabil.

---

## 🏆 Konfigurasi Terbaik

Setelah semua eksperimen, salin konfigurasi terbaik kalian ke sini:

```python
HIDDEN_LAYERS     = 2
NEURONS_PER_LAYER = 128
ACTIVATION        = 'relu'
DROPOUT_RATE      = 0.2
OPTIMIZER         = 'adam'
LEARNING_RATE     = 0.001
BATCH_SIZE        = 64
EPOCHS            = 20
```

**Test accuracy final: ~89–90%**
