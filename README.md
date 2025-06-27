# Proyek Topik Khusus Teknik Kendali: Prediksi Nilai Tukar Mata Uang Asing ke Rupiah Menggunakan Neural Network

Proyek ini dibuat untuk mata kuliah **Topik Khusus Teknik Kendali**. Dalam proyek ini, kami membandingkan performa model neural network, khususnya BPNN, CNN, dan LSTM untuk memprediksi nilai tukar mata uang asing terhadap Rupiah (IDR). Proyek ini berdasarkan eksperimen pemodelan satu dimensi pada data nilai jual mata uang CNY terhadap Rupiah menggunakan pendekatan deret waktu dan deep learning. Dataset diperoleh dari website Bank Indonesia.

## Permasalahan dalam Penelitian

Penelitian ini mengangkat beberapa pertanyaan penting:

• Menentukan jumlah epoch yang optimal dalam pelatihan model neural network untuk memprediksi nilai tukar jual mata uang China (CNY) terhadap Rupiah (IDR), agar model dapat belajar secara efektif tanpa overfitting maupun underfitting.  
• Mengidentifikasi nilai learning rate yang paling sesuai untuk menghasilkan proses pelatihan model yang efisien dan konvergen.  
• Menentukan jumlah neuron tersembunyi (hidden neurons) yang optimal agar model mampu menangkap pola-pola kompleks pada data nilai tukar.  
• Menganalisis fungsi aktivasi (activation function) terbaik agar model dapat mengenali hubungan non-linier input-output.  
• Membandingkan performa model CNN, BPNN, dan LSTM untuk menemukan metode terbaik dalam memprediksi nilai tukar jual CNY terhadap IDR menggunakan metrik RMSE dan test loss.

## Deskripsi Dataset

Dataset berisi data historis nilai tukar jual CNY ke IDR dari tahun 2019 hingga 2024, dengan satu fitur utama yaitu nilai *sell exchange rate*. Dataset bersifat time series dan diambil dari sumber resmi (Bank Indonesia). Dataset digunakan dalam format satu dimensi untuk eksperimen time windowing dan prediksi berurutan.

### Penjelasan Data Training

| **Nama Kolom** | **Deskripsi**                                              |
|----------------|------------------------------------------------------------|
| **Time**       | Waktu (dalam hari) ketika data dicatat                    |
| **Sell**       | Nilai tukar jual CNY terhadap IDR                         |

### *Data Preparation* untuk Training Model

Data disusun dalam bentuk window input-output untuk supervised learning, dengan format:

| *i* | *Time* | *d₁ᵢ* | *d₂ᵢ* | ... | *dₘᵢ* | *Output* |
|-----|--------|--------|--------|-----|--------|-----------|
| 0   | t₀     | X₀     | X₁     | ... | Xₘ     | Xₘ₊₁     |
| 1   | t₁     | X₁     | X₂     | ... | Xₘ₊₁   | Xₘ₊₂     |
| ... | ...    | ...    | ...    | ... | ...    | ...       |

Dimana:
- *n* adalah jumlah total data,
- *m* adalah jumlah titik historis dalam satu window input.

## Eksperimen dan Evaluasi Model

Eksperimen dilakukan dengan variasi:
- Epoch: 500, 750, 1000, 2000
- Learning Rate: 0.00001, 0.002, 0.005, 0.01
- Jumlah Neuron: 32, 64, 128, 256
- Fungsi Aktivasi: Linear vs Sigmoid
- Arsitektur: BPNN, CNN, LSTM, Hybrid CNN-LSTM

Model dievaluasi menggunakan metrik:
- **Validation Loss**
- **Test Loss**
- **RMSE**

## Hasil

- Model LSTM dan CNN menghasilkan prediksi yang lebih akurat dibandingkan BPNN.
- Model Hybrid CNN-LSTM memiliki validation loss terendah, namun sedikit overfit.
- Fungsi aktivasi linear lebih cocok untuk regresi nilai tukar dibandingkan sigmoid.
- Kombinasi optimal ditemukan pada 32 neuron, learning rate 0.002, dan epoch 750–1000.

## Kesimpulan

Model berbasis sekuensial seperti LSTM dan CNN terbukti lebih unggul dalam memprediksi nilai tukar mata uang asing terhadap Rupiah. Penentuan parameter seperti jumlah epoch, learning rate, dan jumlah neuron sangat memengaruhi akurasi model. Arsitektur hybrid CNN-LSTM memberikan hasil terbaik dalam validation loss namun memerlukan perhatian terhadap overfitting.


