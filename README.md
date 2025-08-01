# AstroSpectra-MNIST_benchmark：
[点击查看 PDF 文件](https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/AstroSpectra-MNIST_benchmark.pdf)

# Download：
You can download the dataset at this URL：[Download](https://www.kaggle.com/datasets/zzuygs/astrospectra-mnist-dataset/data).
# Description:
AstroSpectra-MNIST is a novel dataset designed to benchmark machine learning models on astronomical spectral classification tasks. We provide a lightweight, easily storable, and processable dataset.Through a series of processes including data preprocessing and normalization, the astronomical spectral data from LAMOST are converted into lightweight grayscale images in the format of 28*28 pixels. AstroSpectra-MNIST maintains the same image structure as MNIST but differs in storage format. It is characterized by its small size, ease of storage and accessibility. It includes two versions: AstroSpectra-MNIST-v1 and AstroSpectra-MNIST-v2. v1 includes three categories: Star, Galaxy, and QSO, which are labeled with the numbers 1, 2, and 3, respectively. v2 covers three subcategories of stars, namely F-type, G-type, and K-type, which are also labeled with the numbers 1, 2, and 3.

**Dataset Structure** :
<pre>
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
</pre>

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

We obtain 3601-dimensional raw spectrum vectors from LAMOST DR1 and compress them into 721-dimensional feature vectors using a mean filter. This new dataset is named LineAstroSpectra and includes two versions: LineAstroSpectra-v1 and LineAstroSpectra-v2. Models and hyperparameters identical to the AstroSpectra-MNIST benchmark were applied to LineAstroSpectra. The results provide a direct comparison between the raw spectral and the corresponding AstroSpectra-MNIST version.

-**Machine Learning**
**Table 1-1：Test Accuracy of Machine Learning Classifiers**


| **Classifier** | **Parameters** | **AstroSpectra-MNIST-v1** | **AstroSpectra-MNIST-v2** | **Fashion-MNIST** |
|---|---|---|---|---|
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"random"` | 0.778 | 0.724 | 0.794 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"random"` | 0.774 | 0.745 | 0.795 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"random"` | 0.784 | 0.734 | 0.792 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"random"` | 0.780 | 0.728 | 0.794 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"random"` | 0.768 | 0.711 | 0.784 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"random"` | 0.764 | 0.713 | 0.784 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"best"` | 0.782 | 0.742 | 0.801 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"best"` | 0.795 | 0.742 | 0.799 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"best"` | 0.771 | 0.715 | 0.789 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"best"` | 0.768 | 0.717 | 0.789 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"best"` | 0.758 | 0.727 | 0.797 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"best"` | 0.750 | 0.729 | 0.797 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"random"` | 0.755 | 0.699 | 0.734 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"random"` | 0.787 | 0.680 | 0.729 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"best"` | 0.763 | 0.715 | 0.776 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"random"` | 0.755 | 0.693 | 0.752 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"random"` | 0.754 | 0.694 | 0.751 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"random"` | 0.756 | 0.687 | 0.753 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"random"` | 0.772 | 0.697 | 0.756 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"best"` | 0.750 | 0.695 | 0.771 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"best"` | 0.782 | 0.704 | 0.780 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"best"` | 0.753 | 0.694 | 0.771 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"best"` | 0.776 | 0.695 | 0.778 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"best"` | 0.731 | 0.701 | 0.779 |
| **GaussianNB** | `"priors":[1/classnum,1/classnum,1/classnum]` | 0.642 | 0.597 | 0.564 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":10,"n_estimators":100` | 0.877 | 0.806 | 0.888 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":50,"n_estimators":10` | 0.780 | 0.742 | 0.804 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":50,"n_estimators":50` | 0.786 | 0.740 | 0.836 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":50,"n_estimators":100` | 0.779 | 0.740 | 0.838 |
| **KNeighborsClassifier** | `"n_neighbors":1,"p":2,"weights":"uniform"` | 0.812 | 0.674 | 0.847 |
| **KNeighborsClassifier** | `"n_neighbors":9,"p":1,"weights":"uniform"` | 0.853 | 0.730 | 0.856 |
| **KNeighborsClassifier** | `"n_neighbors":5,"p":1,"weights":"distance"` | 0.852 | 0.723 | 0.860 |
| **LinearSVC** | `"C":1,"loss":"squared_hinge","multi_class":"ovr","penalty":"l2"` | 0.806 | 0.733 | 0.827 |
| **LinearSVC** | `"C":1,"loss":"hinge","multi_class":"ovr","penalty":"l2"` | 0.802 | 0.739 | 0.837 |
| **LinearSVC** | `"C":10,"loss":"hinge","multi_class":"ovr","penalty":"l2"` | 0.772 | 0.696 | 0.783 |
| **LinearSVC** | `"C":100,"loss":"squared_hinge","multi_class":"ovr","penalty":"l2"` | 0.805 | 0.709 | 0.788 |
| **LinearSVC** | `"C":10,"loss":"squared_hinge","multi_class":"ovr","penalty":"l2"` | 0.806 | 0.689 | 0.793 |
| **LinearSVC** | `"C":100,"loss":"hinge","multi_class":"crammer_singer","penalty":"l2"` | 0.712 | 0.718 | 0.466 |
| **LinearSVC** | `"C":100,"loss":"squared_hinge","multi_class":"crammer_singer","penalty":"l2"` | 0.713 | 0.718 | 0.458 |
| **LinearSVC** | `"C":100,"loss":"hinge","multi_class":"crammer_singer","penalty":"l1"` | 0.695 | 0.703 | 0.460 |
| **LinearSVC** | `"C":100,"loss":"squared_hinge","multi_class":"crammer_singer","penalty":"l1"` | 0.704 | 0.708 | 0.444 |
| **LogisticRegression** | `"C":100,"multi_class":"ovr","penalty":"l2"` | 0.808 | 0.741 | 0.838 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[10]` | 0.840 | 0.765 | 0.850 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[10,10]` | 0.829 | 0.773 | 0.851 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[10]` | 0.826 | 0.756 | 0.841 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[10,10]` | 0.825 | 0.768 | 0.840 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[100,10]` | 0.874 | 0.791 | 0.874 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[100]` | 0.872 | 0.782 | 0.877 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[100,10]` | 0.864 | 0.775 | 0.865 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[100]` | 0.867 | 0.785 | 0.870 |
| **PassiveAggressiveClassifier** | `"C":1` | 0.776 | 0.713 | 0.791 |
| **PassiveAggressiveClassifier** | `"C":10` | 0.767 | 0.712 | 0.794 |
| **PassiveAggressiveClassifier** | `"C":100` | 0.794 | 0.708 | 0.782 |
| **Perceptron** | `"penalty":"l2"` | 0.762 | 0.706 | 0.753 |
| **Perceptron** | `"penalty":"l1"` | 0.792 | 0.720 | 0.771 |
| **Perceptron** | `"penalty":"elasticnet"` | 0.751 | 0.692 | 0.759 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":10,"n_estimators":10` | 0.836 | 0.751 | 0.834 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":100,"n_estimators":10` | 0.847 | 0.752 | 0.851 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":10,"n_estimators":10` | 0.836 | 0.748 | 0.837 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":50,"n_estimators":10` | 0.843 | 0.757 | 0.850 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":50,"n_estimators":10` | 0.834 | 0.755 | 0.853 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":100,"n_estimators":10` | 0.862 | 0.763 | 0.856 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":10,"n_estimators":50` | 0.835 | 0.760 | 0.843 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":10,"n_estimators":50` | 0.836 | 0.757 | 0.845 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":100,"n_estimators":50` | 0.872 | 0.780 | 0.873 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":50,"n_estimators":50` | 0.871 | 0.781 | 0.873 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":10,"n_estimators":100` | 0.854 | 0.758 | 0.844 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":100,"n_estimators":100` | 0.870 | 0.784 | 0.876 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":100,"n_estimators":50` | 0.873 | 0.780 | 0.875 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":50,"n_estimators":50` | 0.867 | 0.785 | 0.874 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":10,"n_estimators":100` | 0.846 | 0.759 | 0.846 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":100,"n_estimators":100` | 0.878 | 0.785 | 0.877 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":50,"n_estimators":100` | 0.869 | 0.785 | 0.879 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":50,"n_estimators":100` | 0.873 | 0.782 | 0.876 |
| **SGDClassifier** | `"loss":"squared_hinge","penalty":"l2"` | 0.793 | 0.720 | 0.826 |
| **SGDClassifier** | `"loss":"hinge","penalty":"l2"` | 0.800 | 0.728 | 0.826 |
| **SGDClassifier** | `"loss":"modified_huber","penalty":"l2"` | 0.792 | 0.719 | 0.827 |
| **SGDClassifier** | `"loss":"perceptron","penalty":"l2"` | 0.780 | 0.711 | 0.826 |
| **SGDClassifier** | `"loss":"hinge","penalty":"elasticnet"` | 0.791 | 0.727 | 0.829 |
| **SGDClassifier** | `"loss":"log_loss","penalty":"l2"` | 0.777 | 0.735 | 0.827 |
| **SGDClassifier** | `"loss":"perceptron","penalty":"l1"` | 0.772 | 0.732 | 0.819 |
| **SGDClassifier** | `"loss":"squared_hinge","penalty":"l1"` | 0.771 | 0.694 | 0.819 |
| **SGDClassifier** | `"loss":"modified_huber","penalty":"elasticnet"` | 0.792 | 0.722 | 0.831 |
| **SGDClassifier** | `"loss":"squared_hinge","penalty":"elasticnet"` | 0.783 | 0.715 | 0.828 |
| **SGDClassifier** | `"loss":"log_loss","penalty":"l1"` | 0.775 | 0.737 | 0.821 |
| **SGDClassifier** | `"loss":"hinge","penalty":"l1"` | 0.775 | 0.735 | 0.820 |
| **SGDClassifier** | `"loss":"modified_huber","penalty":"l1"` | 0.767 | 0.736 | 0.821 |
| **SGDClassifier** | `"loss":"perceptron","penalty":"elasticnet"` | 0.769 | 0.724 | 0.828 |
| **SGDClassifier** | `"loss":"log_loss","penalty":"elasticnet"` | 0.782 | 0.741 | 0.826 |

&#8203;


**Table 1-2：Machine learning test results and comparison for LineAstroSpectra**

| **Classifier** | **Parameters** | **LineAstroSpectra-v1** | **AstroSpectra-MNIST-v1** | **LineAstroSpectra-v2** | **AstroSpectra-MNIST-v2** |
|---|---|---|---|---|---|
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"random"` | 0.795 | 0.778 | 0.649 | 0.724 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"random"` | 0.779 | 0.774 | 0.557 | 0.745 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"random"` | 0.793 | 0.784 | 0.591 | 0.734 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"random"` | 0.803 | 0.780 | 0.646 | 0.728 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"random"` | 0.807 | 0.768 | 0.630 | 0.711 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"random"` | 0.814 | 0.764 | 0.658 | 0.713 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"best"` | 0.807 | 0.782 | 0.643 | 0.742 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"best"` | 0.795 | 0.795 | 0.657 | 0.742 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"best"` | 0.789 | 0.771 | 0.656 | 0.715 |
| **DecisionTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"best"` | 0.803 | 0.768 | 0.651 | 0.717 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"best"` | 0.810 | 0.758 | 0.671 | 0.727 |
| **DecisionTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"best"` | 0.809 | 0.750 | 0.666 | 0.729 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"random"` | 0.664 | 0.755 | 0.512 | 0.699 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"random"` | 0.661 | 0.787 | 0.507 | 0.680 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":10,"splitter":"best"` | 0.769 | 0.763 | 0.603 | 0.715 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"random"` | 0.762 | 0.755 | 0.606 | 0.693 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"random"` | 0.789 | 0.754 | 0.616 | 0.694 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"random"` | 0.778 | 0.756 | 0.604 | 0.687 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"random"` | 0.769 | 0.772 | 0.595 | 0.697 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":100,"splitter":"best"` | 0.795 | 0.750 | 0.619 | 0.695 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":10,"splitter":"best"` | 0.783 | 0.782 | 0.626 | 0.704 |
| **ExtraTreeClassifier** | `"criterion":"gini","max_depth":50,"splitter":"best"` | 0.794 | 0.753 | 0.628 | 0.694 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":50,"splitter":"best"` | 0.786 | 0.776 | 0.640 | 0.695 |
| **ExtraTreeClassifier** | `"criterion":"entropy","max_depth":100,"splitter":"best"` | 0.792 | 0.731 | 0.626 | 0.701 |
| **GaussianNB** | `"priors":[1/classnum,1/classnum,1/classnum]` | 0.359 | 0.642 | 0.303 | 0.597 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":10,"n_estimators":100` | 0.899 | 0.877 | 0.735 | 0.806 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":50,"n_estimators":10` | 0.829 | 0.780 | 0.678 | 0.742 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":50,"n_estimators":50` | 0.826 | 0.786 | 0.674 | 0.740 |
| **GradientBoostingClassifier** | `loss="log_loss","max_depth":50,"n_estimators":100` | 0.828 | 0.779 | 0.674 | 0.740 |
| **KNeighborsClassifier** | `"n_neighbors":1,"p":2,"weights":"uniform"` | 0.760 | 0.812 | 0.599 | 0.674 |
| **KNeighborsClassifier** | `"n_neighbors":9,"p":1,"weights":"uniform"` | 0.737 | 0.853 | 0.608 | 0.730 |
| **KNeighborsClassifier** | `"n_neighbors":5,"p":1,"weights":"distance"` | 0.741 | 0.852 | 0.613 | 0.723 |
| **LinearSVC** | `"C":1,"loss":"squared_hinge","multi_class":"ovr","penalty":"l2"` | 0.457 | 0.806 | 0.640 | 0.733 |
| **LinearSVC** | `"C":1,"loss":"hinge","multi_class":"ovr","penalty":"l2"` | 0.535 | 0.802 | 0.638 | 0.739 |
| **LinearSVC** | `"C":10,"loss":"hinge","multi_class":"ovr","penalty":"l2"` | 0.522 | 0.772 | 0.694 | 0.696 |
| **LinearSVC** | `"C":100,"loss":"squared_hinge","multi_class":"ovr","penalty":"l2"` | 0.511 | 0.805 | 0.728 | 0.709 |
| **LinearSVC** | `"C":10,"loss":"squared_hinge","multi_class":"ovr","penalty":"l2"` | 0.525 | 0.806 | 0.698 | 0.689 |
| **LinearSVC** | `"C":100,"loss":"hinge","multi_class":"crammer_singer","penalty":"l2"` | 0.664 | 0.712 | 0.713 | 0.718 |
| **LinearSVC** | `"C":100,"loss":"squared_hinge","multi_class":"crammer_singer","penalty":"l2"` | 0.665 | 0.713 | 0.668 | 0.718 |
| **LinearSVC** | `"C":100,"loss":"hinge","multi_class":"crammer_singer","penalty":"l1"` | 0.665 | 0.695 | 0.666 | 0.703 |
| **LinearSVC** | `"C":100,"loss":"squared_hinge","multi_class":"crammer_singer","penalty":"l1"` | 0.665 | 0.704 | 0.732 | 0.708 |
| **LogisticRegression** | `"C":100,"multi_class":"ovr","penalty":"l2"` | 0.524 | 0.808 | 0.657 | 0.741 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[10]` | 0.572 | 0.840 | 0.721 | 0.765 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[10,10]` | 0.618 | 0.829 | 0.720 | 0.773 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[10]` | 0.554 | 0.826 | 0.698 | 0.756 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[10,10]` | 0.554 | 0.825 | 0.718 | 0.768 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[100,10]` | 0.590 | 0.874 | 0.777 | 0.791 |
| **MLPClassifier** | `"activation":"relu","hidden_layer_sizes":[100]` | 0.553 | 0.872 | 0.698 | 0.782 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[100,10]` | 0.560 | 0.864 | 0.787 | 0.775 |
| **MLPClassifier** | `"activation":"tanh","hidden_layer_sizes":[100]` | 0.530 | 0.867 | 0.732 | 0.785 |
| **PassiveAggressiveClassifier** | `"C":1` | 0.515 | 0.776 | 0.692 | 0.713 |
| **PassiveAggressiveClassifier** | `"C":10` | 0.343 | 0.767 | 0.627 | 0.712 |
| **PassiveAggressiveClassifier** | `"C":100` | 0.431 | 0.794 | 0.646 | 0.708 |
| **Perceptron** | `"penalty":"l2"` | 0.512 | 0.762 | 0.575 | 0.706 |
| **Perceptron** | `"penalty":"l1"` | 0.506 | 0.792 | 0.579 | 0.720 |
| **Perceptron** | `"penalty":"elasticnet"` | 0.437 | 0.751 | 0.499 | 0.692 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":10,"n_estimators":10` | 0.834 | 0.836 | 0.629 | 0.751 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":100,"n_estimators":10` | 0.862 | 0.847 | 0.676 | 0.752 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":10,"n_estimators":10` | 0.845 | 0.836 | 0.642 | 0.748 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":50,"n_estimators":10` | 0.862 | 0.843 | 0.674 | 0.757 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":50,"n_estimators":10` | 0.864 | 0.834 | 0.681 | 0.755 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":100,"n_estimators":10` | 0.833 | 0.862 | 0.684 | 0.763 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":10,"n_estimators":50` | 0.847 | 0.835 | 0.639 | 0.760 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":10,"n_estimators":50` | 0.848 | 0.836 | 0.648 | 0.757 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":100,"n_estimators":50` | 0.875 | 0.872 | 0.711 | 0.780 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":50,"n_estimators":50` | 0.877 | 0.871 | 0.708 | 0.781 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":10,"n_estimators":100` | 0.846 | 0.854 | 0.641 | 0.758 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":100,"n_estimators":100` | 0.882 | 0.870 | 0.715 | 0.784 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":100,"n_estimators":50` | 0.881 | 0.873 | 0.704 | 0.780 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":50,"n_estimators":50` | 0.878 | 0.867 | 0.706 | 0.785 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":10,"n_estimators":100` | 0.861 | 0.846 | 0.646 | 0.759 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":100,"n_estimators":100` | 0.877 | 0.878 | 0.712 | 0.785 |
| **RandomForestClassifier** | `"criterion":"entropy","max_depth":50,"n_estimators":100` | 0.883 | 0.869 | 0.715 | 0.785 |
| **RandomForestClassifier** | `"criterion":"gini","max_depth":50,"n_estimators":100` | 0.881 | 0.873 | 0.719 | 0.782 |
| **SGDClassifier** | `"loss":"squared_hinge","penalty":"l2"` | 0.522 | 0.793 | 0.679 | 0.720 |
| **SGDClassifier** | `"loss":"hinge","penalty":"l2"` | 0.523 | 0.800 | 0.587 | 0.728 |
| **SGDClassifier** | `"loss":"modified_huber","penalty":"l2"` | 0.499 | 0.802 | 0.534 | 0.719 |
| **SGDClassifier** | `"loss":"perceptron","penalty":"l2"` | 0.540 | 0.780 | 0.552 | 0.711 |
| **SGDClassifier** | `"loss":"hinge","penalty":"elasticnet"` | 0.480 | 0.791 | 0.575 | 0.727 |
| **SGDClassifier** | `"loss":"log_loss","penalty":"l2"` | 0.436 | 0.777 | 0.509 | 0.735 |
| **SGDClassifier** | `"loss":"perceptron","penalty":"l1"` | 0.450 | 0.772 | 0.577 | 0.732 |
| **SGDClassifier** | `"loss":"squared_hinge","penalty":"l1"` | 0.409 | 0.771 | 0.568 | 0.694 |
| **SGDClassifier** | `"loss":"modified_huber","penalty":"elasticnet"` | 0.554 | 0.792 | 0.587 | 0.722 |
| **SGDClassifier** | `"loss":"squared_hinge","penalty":"elasticnet"` | 0.554 | 0.783 | 0.617 | 0.715 |
| **SGDClassifier** | `"loss":"log_loss","penalty":"l1"` | 0.479 | 0.775 | 0.542 | 0.737 |
| **SGDClassifier** | `"loss":"hinge","penalty":"l1"` | 0.485 | 0.775 | 0.598 | 0.735 |
| **SGDClassifier** | `"loss":"modified_huber","penalty":"l1"` | 0.363 | 0.767 | 0.645 | 0.736 |
| **SGDClassifier** | `"loss":"perceptron","penalty":"elasticnet"` | 0.450 | 0.769 | 0.612 | 0.724 |
| **SGDClassifier** | `"loss":"log_loss","penalty":"elasticnet"` | 0.464 | 0.782 | 0.519 | 0.741 |

&#8203;

**Deep Learning**
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

&#8203;

# Confusion matrix：


<!-- SimpleCNN1 -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img20.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img20.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of SimpleCNN1</strong></p>

<!-- SimpleCNN2 -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img21.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img21.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of SimpleCNN2</strong></p>

<!-- AlexNet -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img22.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img22.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of AlexNet</strong></p>

<!-- VGG16 -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img23.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img23.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of VGG16</strong></p>

<!-- LeNet -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img24.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img24.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of LeNet</strong></p>

<!-- GoogLeNet -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img25.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img25.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of GoogLeNet</strong></p>

<!-- ResNet18 -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img26.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img26.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of ResNet18</strong></p>

<!-- MobileNetV2 -->
<p align="center">
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img27.1.png" width="45%" />
  <img src="https://raw.githubusercontent.com/zzuwqk/AstroSpectra-MNIST_benchmark/main/Confusion%20matrix/img27.2.png" width="45%" />
</p>
<p align="center"><strong>Confusion matrix of MobileNetV2</strong></p>



**Deep Learning**


# Citation：

If you use this dataset, please cite:

<pre style="background-color: rgba(244, 244, 244, 1); padding: 12px; border-radius: 6px; font-size: 14px; line-height: 1.4; white-space: pre-wrap; word-wrap: break-word">@misc{astrospectra-mnist,
  title={AstroSpectra-MNIST: An Astronomical Spectral Dataset for Benchmarking Machine Learning Algorithms},
  author={Wu, Qiankun and Shi, Yungao and Wang, Ke and Guo, Ping},
  year={2025},
  url={https://www.kaggle.com/datasets/zzuygs/astrospectra-mnist-dataset}
}
</pre>
