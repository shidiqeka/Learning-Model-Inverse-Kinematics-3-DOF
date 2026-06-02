# Inverse Kinematics untuk Robot Planar 3-DOF
## Machine Learning, Deep Learning, dan Reinforcement Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

---

## 📋 Daftar Isi
- [Deskripsi Proyek](#deskripsi-proyek)
- [Konsep Dasar](#konsep-dasar)
- [Spesifikasi Robot](#spesifikasi-robot)
- [Prasyarat](#prasyarat)
- [Instalasi](#instalasi)
- [Struktur Notebook](#struktur-notebook)
- [Penggunaan](#penggunaan)
- [Model & Approach](#model--approach)
- [Hasil & Evaluasi](#hasil--evaluasi)
- [Kontribusi](#kontribusi)

---

## 🎯 Deskripsi Proyek

Proyek ini mengeksplorasi tiga pendekatan berbeda untuk menyelesaikan masalah **Inverse Kinematics (IK)** pada robot planar 3-DOF (Degrees of Freedom):

1. **Machine Learning** - Supervised learning dengan model klasik (KNN, Random Forest, SVR)
2. **Deep Learning** - Neural Network menggunakan PyTorch
3. **Reinforcement Learning** - PPO algorithm dengan Gymnasium

Setiap pendekatan membandingkan akurasi, kecepatan, dan kemampuan generalisasi dalam memprediksi sudut sendi yang diperlukan untuk mencapai posisi target end-effector.

---

## 🔬 Konsep Dasar

### Forward Kinematics (FK)
Diberikan sudut sendi **→** hitung posisi end-effector
- ✅ Solusi **unik**
- ✅ Mudah dihitung secara analitik

**Persamaan FK untuk robot planar 3-DOF:**
```
x = L₁·cos(θ₁) + L₂·cos(θ₁+θ₂) + L₃·cos(θ₁+θ₂+θ₃)
y = L₁·sin(θ₁) + L₂·sin(θ₁+θ₂) + L₃·sin(θ₁+θ₂+θ₃)
```

### Inverse Kinematics (IK)
Diberikan posisi target **(x, y)** **→** hitung sudut sendi **θ₁, θ₂, θ₃**
- ⚠️ Solusi bisa **banyak** (multiple solutions)
- ⚠️ Solusi bisa **tidak ada** (unreachable positions)
- ⚠️ Non-linear dan kompleks untuk robot > 2-DOF

---

## 🤖 Spesifikasi Robot

| Parameter | Nilai |
|-----------|-------|
| Jumlah Link | 3 |
| Panjang L₁ | 0.4 m |
| Panjang L₂ | 0.3 m |
| Panjang L₃ | 0.2 m |
| Batas Sudut Sendi | ±π radian |
| End-effector | Ujung Link 3 |

**Reach (jangkauan):** Maksimal = L₁ + L₂ + L₃ = 0.9 m

---

## 📦 Prasyarat

- Python 3.8 atau lebih tinggi
- Pengetahuan dasar:
  - Python programming
  - NumPy & Matplotlib
  - Machine Learning basics
  - Neural Networks (untuk DL section)
  - Reinforcement Learning (untuk RL section)

---

## 🚀 Instalasi

### 1. Clone atau Download Repository
```bash
cd d:\Learning-Model-Inverse-Kinematics-3-DOF
```

### 2. Buat Virtual Environment (opsional tapi recommended)
```bash
python -m venv venv
venv\Scripts\activate  # Windows
# atau
source venv/bin/activate  # Linux/Mac
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

Atau install secara manual:
```bash
pip install numpy matplotlib scikit-learn torch gymnasium stable-baselines3 ipython jupyter
```

### 4. Buka Notebook
```bash
jupyter notebook inverse_kinematics_robot_3dof.ipynb
```

---

## 📚 Struktur Notebook

Notebook dibagi menjadi **8 bagian utama**:

| Bagian | Judul | Deskripsi |
|--------|-------|-----------|
| **1** | Pengantar FK & IK | Konsep dasar kinematika robot |
| **2** | Core Functions & Robot Setup | Fungsi FK dan utility robot |
| **3** | Membuat Dataset | Sampling & preprocessing data |
| **4** | Machine Learning | Supervised learning models |
| **5** | Deep Learning | Neural Network dengan PyTorch |
| **6** | Reinforcement Learning | PPO dengan Gymnasium |
| **7** | Evaluasi & Perbandingan | Metrics & performance analysis |
| **8** | Visualisasi & Demo | Plotting dan demonstrasi |

---

## 💻 Penggunaan

### Menjalankan Seluruh Notebook
```
Tekan Ctrl+Shift+Enter untuk menjalankan semua cell
```

### Menjalankan Cell Tertentu
```
1. Klik cell yang ingin dijalankan
2. Tekan Ctrl+Enter (run) atau Shift+Enter (run & move to next)
```

### Langkah-langkah Umum
1. **Bagian 1-2:** Pahami konsep & setup robot
2. **Bagian 3:** Generate dataset dari FK
3. **Bagian 4-6:** Train dan evaluasi setiap model
4. **Bagian 7-8:** Bandingkan hasil & visualisasi

---

## 🤖 Model & Approach

### Bagian 4: Machine Learning
**Model yang digunakan:**
- k-Nearest Neighbors (KNN)
- Random Forest (RF)
- Gradient Boosting
- Support Vector Regression (SVR)

**Keuntungan:**
- ✅ Cepat untuk inference
- ✅ Mudah dipahami
- ✅ Cocok untuk dataset sedang

**Kerugian:**
- ❌ Akurasi lebih rendah untuk non-linear complex
- ❌ Perlu feature engineering

---

### Bagian 5: Deep Learning
**Architecture:**
- Multi-layer Perceptron (MLP) dengan PyTorch
- Input: 2 (x, y)
- Hidden layers: customizable
- Output: 3 (θ₁, θ₂, θ₃)

**Keuntungan:**
- ✅ Akurasi tinggi
- ✅ Automatic feature learning
- ✅ Generalisasi baik

**Kerugian:**
- ❌ Butuh training time lebih lama
- ❌ Memerlukan lebih banyak data

---

### Bagian 6: Reinforcement Learning
**Algorithm:** Proximal Policy Optimization (PPO)
**Framework:** Gymnasium + Stable-Baselines3

**Reward Function:**
- Positive reward untuk menjangkau target
- Negative reward untuk joint limit violations
- Penalty untuk gerakan yang tidak efisien

**Keuntungan:**
- ✅ Adaptif terhadap constraints
- ✅ Bisa handle obstacles (dengan modifikasi)
- ✅ Flexible untuk berbagai objectives

**Kerugian:**
- ❌ Training jauh lebih lama
- ❌ Hyperparameter tuning lebih kompleks

---

## 📊 Hasil & Evaluasi Training

### Metrik Evaluasi
- **Mean Squared Error (MSE)** - Error rata-rata pada sudut sendi
- **Mean Absolute Error (MAE)** - Error absolut rata-rata
- **Success Rate** - Persentase target tercapai
- **Inference Time** - Waktu prediksi
- **Reachability** - Kemampuan mencapai area workspace

### Hasil Training Summary

| Model | Mean Error | Accuracy | Catatan |
|-------|-----------|----------|---------|
| **ML (Gradient Boosting)** | 81.35 cm | ~92% | Cepat, tapi error masih besar |
| **DL (ResNet/Ultra-ResNet)** | **0.79 cm** | ~99% | 🏆 **Terbaik! Akurasi super tinggi** |
| **RL (PPO Agent)** | 9.94 cm | ~94% | Adaptif, learning curve mantap |

### 🎨 Foto Hasil Training

![Training Results](Hasil%20Train.PNG)

**Gambar di atas menampilkan hasil training komprehensif semua 3 pendekatan:**

📊 **Perbandingan Akurasi & Error Distribution:**
- **Left (ML):** Gradient Boosting error distribution - mean 81.35 cm
- **Middle (DL):** ResNet error distribution - mean 0.79 cm ✅ **Terbaik!**
- **Right (RL):** PPO error distribution - mean 9.94 cm

📈 **Training Curves:**
- Deep Learning menunjukkan convergence yang smooth
- Reinforcement Learning menunjukkan reward improvement
- Error menurun signifikan seiring epoch bertambah

🎯 **Key Insights dari Gambar:**
- **Deep Learning (ResNet):** Distribusi error paling sempit = presisi tertinggi
- **Reinforcement Learning (PPO):** Moderate performance, adaptif
- **Machine Learning (GB):** Error terlalu besar untuk aplikasi presisi

### Key Findings

✅ **Deep Learning adalah pemenang:**
- Error terendah: 0.79 cm
- Akurasi tertinggi: ~99%
- Konsisten dan reliable

✅ **Reinforcement Learning cukup baik:**
- Error moderate: 9.94 cm
- Good untuk adaptive scenarios
- Training lambat tapi hasil memuaskan

⚠️ **Machine Learning kurang optimal:**
- Error tinggi: 81.35 cm
- Banyak outliers
- Tidak cocok untuk precision tasks

### Cara Melihat Hasil di Notebook

1. **Jalankan notebook:** Ctrl+Shift+Enter
2. **Bagian 4** → Melihat visualisasi robot & dataset
3. **Bagian 5** → ML training & error distribution
4. **Bagian 6** → DL training curves & convergence
5. **Bagian 7** → RL training progress
6. **Bagian 8** → Perbandingan & final results

---

## 🔧 Troubleshooting

### Error: ModuleNotFoundError
```bash
# Install missing packages
pip install numpy matplotlib scikit-learn torch gymnasium stable-baselines3
```

### CUDA Error (GPU not available)
```python
# Ubah di cell PyTorch:
device = torch.device("cpu")  # Gunakan CPU saja
```

### Notebook runs very slow
- Kurangi jumlah sampel dataset (N di Bagian 3)
- Skip Bagian 6 (RL training sangat lambat)
- Gunakan GPU-enabled PyTorch

---

## 📝 File Structure
```
d:\Learning-Model-Inverse-Kinematics-3-DOF\
├── inverse_kinematics_robot_3dof.ipynb   # Main notebook
├── README.md                              # This file
└── requirements.txt                       # Dependencies (optional)
```

---

## 📖 Referensi & Bacaan Lanjutan

- [Robotic Kinematics - Wiki](https://en.wikipedia.org/wiki/Kinematics)
- [PyTorch Documentation](https://pytorch.org/docs/)
- [Gymnasium - RL Framework](https://gymnasium.farama.org/)
- [Stable-Baselines3](https://stable-baselines3.readthedocs.io/)
- [Scikit-learn Models](https://scikit-learn.org/)

---

## 📧 Kontak & Dukungan

Jika ada pertanyaan atau issue:
1. Review notebook comments dan docstrings
2. Check output cell untuk error messages
3. Verify semua dependencies terinstall dengan benar

---

## 📄 Lisensi

Project ini tersedia di bawah lisensi MIT. Bebas untuk digunakan, modifikasi, dan distribusikan.

---

## ✨ Highlights

- 🎓 **Educational:** Dari basic FK hingga advanced RL
- 🔬 **Comprehensive:** Tiga pendekatan AI/ML berbeda
- 📊 **Comparative:** Analisis mendalam setiap approach
- 🎨 **Visual:** Banyak plot dan animasi
- 💡 **Practical:** Real-world robotics problem

---

**Selamat belajar! Happy coding! 🚀**
