# 🚀 The Semantic Gap: Limits of Cross-Modal Metric Learning

## 📖 Overview
This repository contains an experimental research project investigating the feasibility of **Cross-Modal Metric Learning** on biologically uncorrelated data. Using the Face-Fingerprint Dataset, we attempted to map a person's face and fingerprint into a 256-dimensional **Shared Embedding Space** using a Dual-ResNet Siamese architecture and Contrastive Loss.

This project serves as a valuable **Negative Result** in Deep Learning and Computer Vision, mathematically proving the "Semantic Gap" and demonstrating why feature-level fusion fails when there is no underlying latent correlation between the modalities.

## 🧠 The Hypothesis vs. Biological Reality
**The Goal:** To train a neural network to push the embeddings of the *same person's* face and fingerprint closer together ($L2$ distance approaching $0$), while pushing *different people's* biometrics apart.

**The Reality:** There is no visual, structural, or genetic correlation between the shape of a person's face and the minutiae patterns on their fingerprints. We tested whether a deep learning model could somehow bridge this gap.

## 📊 Results & The Mathematical Proof
After training the model for 15 epochs, the training loss decreased steadily, creating the illusion of learning. However, evaluating the distance distributions on an unseen test set revealed the truth:

![Distance Distribution Graph](graph_image.png)

### Key Findings:
1. **Complete Overlap:** The distance distribution of Positive Pairs (Same Person) and Negative Pairs (Different People) perfectly overlapped. The model possessed zero discriminative power.
2. **The $\sqrt{2}$ Mystery:** Both distributions peaked exactly between $1.40$ and $1.50$. In high-dimensional space, the expected Euclidean distance between two completely **random and independent vectors** on a unit hypersphere (due to $L2$ Normalization) is exactly $\sqrt{2}$ ($\approx 1.414$). 

**Conclusion:** The neural network found absolutely zero correlation. It resorted to mapping all inputs to completely random, independent locations in the latent space.

## 🛠️ Tech Stack & Architecture
* **Framework:** PyTorch
* **Models:** Pre-trained ResNet18 (Dual-Branch)
* **Loss Function:** Contrastive Loss (Margin = 2.0)
* **Optimization:** L2 Normalized Embeddings
* **Visualization:** Matplotlib & Seaborn

## 🚀 How to Run Locally
1. Clone the repository:
   ```bash
   git clone https://github.com/goktani/face-fingerprint-semantic-gap.git)
   cd face-fingerprint-semantic-gap
   
2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the training script (ensure your dataset path is correctly set in the script):

```Bash
python why-face-fingerprint-fusion-fails.ipynb
```
## 💡 What's the Correct Approach?
For completely uncorrelated multimodal biometric datasets like this, Score-Level Fusion or Decision-Level Fusion should be used instead of Feature-Level Fusion (Metric Learning).

## 👨‍💻 Author
Göktan İren
