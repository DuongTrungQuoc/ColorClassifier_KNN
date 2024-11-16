# COLOR CLASSIFIER
Dự án này tập trung vào việc phân loại màu bằng thuật toán K-Nearest Neighbors (KNN) trong Học Máy, được huấn luyện bằng histogram màu R, G, B. 
Hệ thống có thể phân loại các màu: Trắng, Đen, Đỏ, Xanh lá, Xanh dương, Cam, Vàng và Tím.

## Demo

**Run [color_classification_webcam.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_webcam.py) để thực hiện nhận diện màu trong thời gian thực qua luồng webcam.**

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/demo.gif">
</p>

**Run [color_classification_image.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_image.py) để thực hiện nhận diện màu trên một ảnh.**

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/demo_img.jpg">
</p>

---
**Dự án này làm được những gì?**
1. **Trích xuất đặc trưng:** Lấy giá trị histogram màu R, G, B từ [ảnh huấn luyện](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/tree/main/color_classifier/src/training_dataset)
2. **THuấn luyện bộ phân loại KNN:** Sử dụng giá trị histogram màu R, G, B để huấn luyện bộ phân loại KNN.
3. **Phân loại bằng KNN đã huấn luyện:** Đọc từng khung hình từ webcam, trích xuất đặc trưng và phân loại màu chính của khung hình bằng KNN đã huấn luyện.
---

## Lý thuyết

Dự án này phân loại màu bằng thuật toán K-Nearest Neighbor. Bộ phân loại được huấn luyện bằng giá trị histogram màu R, G, B của hình ảnh. Quy trình làm việc chung như sau:

<p align="center">
  <img src="https://user-images.githubusercontent.com/22610163/35335133-a9632c70-0125-11e8-9204-0b4bfd0702a7.png" {width=35px height=350px}>
</p>

You should know 2 main pheomena to understand basic Object Detection/Recognition Systems of Computer Vision and Machine Learning.

**1.) Feature Extraction**

How to represent the interesting points we found to compare them with other interesting points (features) in the image.

**2.) Classification**

An algorithm that implements classification, especially in a concrete implementation, is known as a classifier. The term "classifier" sometimes also refers to the mathematical function, implemented by a classification algorithm, that maps input data to a category.

For this project;

**1.) Feature Extraction** = Color Histogram

Color Histogram is a representation of the distribution of colors in an image. For digital images, a color histogram represents the number of pixels that have colors in each of a fixed list of color ranges, that span the image's color space, the set of all possible colors.

<p align="center">
  <img src="https://user-images.githubusercontent.com/22610163/34918867-44f5feaa-f96b-11e7-9994-1747846266c9.png">
</p>

**2.) Classification** = K-Nearest Neighbors Algorithm

K nearest neighbors is a simple algorithm that stores all available cases and classifies new cases based on a similarity measure (e.g., distance functions). KNN has been used in statistical estimation and pattern recognition already in the beginning of 1970’s as a non-parametric technique.

<p align="center">
  <img src="https://user-images.githubusercontent.com/22610163/34918895-c7b94d24-f96b-11e7-87da-8619d9bd4246.png">
</p>

## Implementation

[OpenCV](https://pypi.python.org/pypi/opencv-python) was used for color histogram calculations and knn classifier. [NumPy](https://stackoverflow.com/questions/29499815/how-to-install-numpy-on-windows-using-pip-install) was used for matrix/n-dimensional array calculations. The program was developed on Python at Linux environment.

In the “[src](https://github.com/ahmetozlu/color_recognition/tree/master/src)” folder, there are 2 Python classes which are:

- **[color_classification_webcam.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_classification_webcam.py):** test class to perform real-time color recognition form webcam stream.

- **[color_classification_image.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_classification_image.py):** test class to perform color recognition on a single image.

In the “[color_recognition_api](https://github.com/ahmetozlu/color_recognition/tree/master/src/color_recognition_api)” folder, there are 2 Python classes which are:

- **[feature_extraction.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/color_histogram_feature_extraction.py):** feature extraction operation class

- **[knn_classifier.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/knn_classifier.py):** knn classification class

**1.) Explanation of “[feature_extraction.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/color_histogram_feature_extraction.py)"**

I can get the RGB color histogram of images by this Python class. For example, plot of RGB color histogram for one of the red images is given at the below.

<p align="center">
  <img src="https://user-images.githubusercontent.com/22610163/34919478-f198beb8-f975-11e7-8c1c-0a552f7cd673.jpg" {width=25px height=250px}>
</p>

I decided to use bin number of histogram which has the peak value of pixel count for R, G and B as feature so I can get the dominant R, G and B values to create feature vectors for training. For example, the dominant R, G and B values of the red image which is given at above is [254, 0, 2].

I get the dominant R, G, B values by using Color Histogram for each training image then I labelled them because KNN classifier is a supervised learner and I deploy these feature vectors in the csv file. Thus, I create my training feature vector dataset. It can be found in the file which name’s is [training.data](https://github.com/ahmetozlu/color_recognition/blob/master/src/training.data) under src folder.

**2.) Explanation of “[knn_classifier.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/knn_classifier.py)”**

This class provides these main calculations;

1. Fetching training data
2. Fetching test image features
3. Calculating euclidean distance
4. Getting k nearest neighbors
5. Prediction of color
6. Returning the prediction is true or false

**“[color_classification_webcam.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_classification_webcam.py)”** is the main class of my program, it provides;

1. Calling [feature_extraction.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/color_histogram_feature_extraction.py) to create training data by feature extraction
2. Calling [knn_classifier.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/knn_classifier.py) for classification

You can find training data in [here](https://github.com/ahmetozlu/color_classifier/tree/master/src/training_dataset).

You can find features are got from training data in [here](https://raw.githubusercontent.com/ahmetozlu/color_classifier/master/src/training.data).


