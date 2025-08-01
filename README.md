# AstroSpectra-MNIST_benchmark：
[点击查看 PDF 文件](https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/AstroSpectra-MNIST_benchmark.pdf)

# Download：
You can download the dataset at this URL：[Download](https://www.kaggle.com/datasets/zzuygs/astrospectra-mnist-dataset/data).
# Description:
AstroSpectra-MNIST is a novel dataset designed to benchmark machine learning models on astronomical spectral classification tasks. We provide a lightweight, easily storable, and processable dataset.Through a series of processes including data preprocessing and normalization, the astronomical spectral data from LAMOST are converted into lightweight grayscale images in the format of 28*28 pixels. AstroSpectra-MNIST maintains the same image structure as MNIST but differs in storage format. It is characterized by its small size, ease of storage and accessibility. It includes two versions: AstroSpectra-MNIST-v1 and AstroSpectra-MNIST-v2. v1 includes three categories: Star, Galaxy, and QSO, which are labeled with the numbers 1, 2, and 3, respectively. v2 covers three subcategories of stars, namely F-type, G-type, and K-type, which are also labeled with the numbers 1, 2, and 3.

Dataset Structure:
AstroSpectra-MNIST/
├── AstroSpectra-MNIST-v1/
│   ├── train_imagesv1/
│   ├── test_imagesv1/
│   ├── train_labelsv1.csv
│   └── test_labelsv1.csv
├── AstroSpectra-MNIST-v2/
│   ├── train_imagesv2/
│   ├── test_imagesv2/
│   ├── train_labelsv2.csv
│   └── test_labelsv2.csv
└── README.md

- **AstroSpectra-MNIST-v1**(stars, galaxies, quasars)

![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F27013442%2Faf12f069bd2fa5a08bd448352343d0b5%2FIMG_202508013580_568x169.png?generation=1754018243177992&alt=media)

| File Name            | Description                   | Format | Size    |
| -------------------- | ----------------------------- | ------ | ------- |
| `train_imagesv1/`    | 8000 grayscale images  | PNG    | 4.42 MB |
| `test_imagesv1/`     | 1000 grayscale images         | PNG    | 564 KB  |
| `train_labelsv1.csv` | Labels for v1 training set       | CSV    | 131 KB  |
| `test_labelsv1.csv`  | Labels for v1 test set           | CSV    | 16.5 KB |

- **AstroSpectra-MNIST-v2**(F-type, G-type, K-type stars)
![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F27013442%2F2ba92853b609ea4297ccd71968918c38%2FIMG2_202508019717_568x169.jpg?generation=1754018331698593&alt=media)

| File Name            | Description                   | Format | Size    |
| -------------------- | ----------------------------- | ------ | ------- |
| `train_imagesv2/`    | 42454 grayscale images        | PNG    | 25.9 MB |
| `test_imagesv2/`     | 7546 grayscale images         | PNG    | 4.56 MB |
| `train_labelsv2.csv` | Labels for v2 training set    | CSV    | 776 KB  |
| `test_labelsv2.csv`  | Labels for v2 test set        | CSV    | 124 KB  |

# Visualization and Analysis: 
<img src="https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F27013442%2F793bfcc0e1f1b4204cd6960a9c3d9de2%2Fb4cd842b5059ed8b7c405d1d6891029.png?generation=1754015363119559&alt=media" alt="AstroSpectra-MNIST Sample" style="margin-right: 20px">

-**AstroSpectra-MNIST-v1**: PCA shows partial split among Star, Galaxy, and QSO classes, suggesting distinguishable spectral patterns. t-SNE offers clearer class separation and reveals subclusters within the stellar class, indicating internal heterogeneity and supporting the need for secondary classification.

<img src="https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F27013442%2Fa1fde7f039b9d6c0605bb5acd66b05af%2Fd7c16f68e5ee1d39f302c5671d2c5af.png?generation=1754015398742400&alt=media" alt="AstroSpectra-MNIST Sample" style="margin-right: 20px">

-**AstroSpectra-MNIST-v2**: PCA shows significant overlap among F, G,and K subclasses, highlighting classification difficulty. t-SNE improves separation and shows discernible subclass clusters despite some overlap, demonstrating its advantage in visualizing complex spectroscopic data.

# Benchmark：

Classical models (e.g., AlexNet) are adapted by converting input channels to grayscale (single-channel), adjusting the output layer to 3 classes, and standardizing images through upsampling to 224×224 resolution. Additionally, we created two custom CNN models, SimpleCNN1 and SimpleCNN2, each processing 28×28 grayscale images through dual convolution pool blocks and fully connected layers to output three class predictions.  

![](https://www.googleapis.com/download/storage/v1/b/kaggle-user-content/o/inbox%2F27013442%2Feda312eb5756e823880b0d5000b3240c%2FIMG_202508016628_576x301.png?generation=1754035851976237&alt=media)

We obtain 3601-dimensional raw spectrum vectors from LAMOST DR1 and compress them into 721-dimensional feature vectors using a mean filter. This new dataset is named LineAstroSpectra and includes two versions: LineAstroSpectra-v1 and LineAstroSpectra-v2. Models and hyperparameters identical to the AstroSpectra-MNIST benchmark were applied to LineAstroSpectra. The results provide a direct comparison between the raw spectral and the corresponding AstroSpectra-MNIST version. For machine learning methods, only the best-performing results are presented in the main text(full experimental details and model parameters are available at [https://github.com/zzuwqk/AstroSpectra-MNIST_benchmark](https://github.com/zzuwqk/AstroSpectra-MNIST_benchmark)

-**Machine Learning**
**Table 1 ：Comparative analysis of classification performance of different models on AstroSpectra-MNIST**(Partial display, average accuracy and variance derived from all results)

| **Classifier** | **Line-Astrov1** | **Line-Astrov2** | **Astro-MNISTv1** | **Astro-MNISTv2** | **Fashion-MNIST** |
|----------------|------------------|------------------|-------------------|-------------------|-------------------|
| DecisionTreeClassifier | 0.795 | 0.657 | 0.795 | 0.742 | 0.799 |
| ExtraTreeClassifier | 0.661 | 0.507 | 0.787 | 0.680 | 0.729 |
| GaussianNB | 0.359 | 0.303 | 0.642 | 0.597 | 0.564 |
| GradientBoostingClassifier | 0.899 | 0.735 | 0.877 | 0.806 | 0.888 |
| KNeighborsClassifier | 0.760 | 0.599 | 0.812 | 0.674 | 0.847 |
| LinearSVC | 0.457 | 0.640 | 0.806 | 0.733 | 0.827 |
| LogisticRegression | 0.524 | 0.657 | 0.808 | 0.741 | 0.838 |
| MLPClassifier | 0.590 | 0.777 | 0.874 | 0.791 | 0.874 |
| PassiveAggressiveClassifier | 0.431 | 0.646 | 0.794 | 0.708 | 0.782 |
| Perceptron | 0.506 | 0.579 | 0.792 | 0.720 | 0.771 |
| RandomForestClassifier | 0.877 | 0.712 | 0.878 | 0.785 | 0.877 |
| SGDClassifier | 0.499 | 0.534 | 0.802 | 0.719 | 0.827 |
| **Average Accuracy** | **0.680** | **0.640** | **0.798** | **0.732** | **0.800** |
| **Overall Variance** | **0.02650** | **0.00505** | **0.00225** | **0.00112** | **0.00768** |



-**Deep Learning**
 **Table 2：Comparison of classification performance of deep learning models on AstroSpectra-MNIST**

| **Model** | **AstroSpectra-MNIST-v1** | **AstroSpectra-MNIST-v2** | **Fashion-MNIST** |
|-----------|---------------------------|---------------------------|-------------------|
| SimpleCNN1 | 0.905 | 0.816 | 0.919 |
| SimpleCNN2 | 0.910 | 0.832 | 0.939 |
| AlexNet | 0.902 | 0.808 | 0.899 |
| VGG16 | 0.909 | 0.835 | 0.935 |
| LeNet | 0.889 | 0.813 | 0.899 |
| GoogLeNet | 0.887 | 0.837 | 0.937 |
| ResNet18 | 0.876 | 0.842 | 0.949 |
| MobileNetv2 | 0.852 | 0.802 | 0.950 |
| **Average Accuracy** | **0.891** | **0.823** | **0.928** |
| **Overall Variance** | **0.000346** | **0.000200** | **0.000367** |
# 📌 Citation：

If you use this dataset, please cite:

<pre style="background-color: rgba(244, 244, 244, 1); padding: 12px; border-radius: 6px; font-size: 14px; line-height: 1.4; white-space: pre-wrap; word-wrap: break-word">@misc{astrospectra-mnist,
  title={AstroSpectra-MNIST: An Astronomical Spectral Dataset for Benchmarking Machine Learning Algorithms},
  author={Wu, Qiankun and Shi, Yungao and Wang, Ke and Guo, Ping},
  year={2025},
  url={https://www.kaggle.com/datasets/zzuygs/astrospectra-mnist-dataset}
}
</pre>
