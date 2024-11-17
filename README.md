# COLOR CLASSIFIER️🎨
Dự án này tập trung vào việc phân loại màu bằng thuật toán K-Nearest Neighbors (KNN) trong Học Máy, được huấn luyện bằng histogram màu RGB. 

## K-Nearest Neighbors (KNN) là gì ?👨‍👨‍👧‍👧

Để Quốc diễn giải cho mọi người hiểu nha @_@

**K-Nearest Neighbors** được dịch là số lượng k các hàng xóm gần nhất.

Trong bài toán Classification, label của một điểm dữ liệu mới được suy ra trực tiếp từ K điểm dữ liệu gần nhất trong training set. Label của một test data có thể được quyết định bằng major voting (bầu chọn theo số phiếu) giữa các điểm gần nhất, hoặc nó có thể được suy ra bằng cách đánh trọng số khác nhau cho mỗi trong các điểm gần nhất đó rồi suy ra label.

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/exam.jpg">
</p>

### Giải thích hình trên:

**Dữ liệu ban đầu (Initial Data):**
- Tập dữ liệu gồm 2 class: class A gồm các điểm dữ liệu được biểu diễn bằng hình tròn và class B gồm các điểm dữ liệu được biểu diễn bằng hình tam giác.
- Ta có một mẫu mới chưa được phân loại (?) và mục tiêu là xác định mẫu này thuộc lớp nào?(Label?)
  
**Tính toán khoảng cách (Calculate Distance):**
- Tính toán khoảng cách giữa điểm dữ liệu mới (?) và các điểm dữ liệu khác trong không gian.
- Phương pháp tính khoảng cách phổ biến là sử dụng khoảng cách Euclid (đo khoảng cách thẳng từ điểm này đến điểm kia theo đường chim bay)
<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/calc.jpg">
</p>

**Tìm các láng giềng và bỏ phiếu để chọn nhãn (Finding Neighbors & Voting for Labels):**
- Thuật toán KNN tìm ra "K" điểm gần nhất với điểm mới (ở đây K=3).
- Sau đó, thuật toán thực hiện bỏ phiếu để xác định lớp của điểm dữ liệu mới. Nếu đa số trong 3 điểm gần nhất là lớp A (vòng tròn), thì điểm dữ liệu mới sẽ được phân loại là lớp A. Ngược lại, nếu đa số là lớp B (tam giác), điểm dữ liệu mới sẽ được phân loại là lớp B.

---
## Demo Project

**Run [color_classification_webcam.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_webcam.py) để thực hiện nhận diện màu trong thời gian thực qua luồng webcam.**

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/demo.gif">
</p>

**Run [color_classification_image.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_image.py) để thực hiện nhận diện màu trên một ảnh.**

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/demo_img.jpg">
</p>

---
### Dự án này làm được những gì?
1. **Trích xuất đặc trưng:** Lấy giá trị histogram màu RGB từ [ảnh huấn luyện](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/tree/main/color_classifier/src/training_dataset)
2. **Huấn luyện bộ phân loại KNN:** Sử dụng giá trị histogram màu R, G, B để huấn luyện bộ phân loại KNN.
3. **Phân loại bằng KNN đã huấn luyện:** Đọc từng khung hình từ webcam, trích xuất đặc trưng và phân loại màu chính của khung hình bằng KNN đã huấn luyện.
---

## Lý thuyết

Dự án này phân loại màu bằng thuật toán K-Nearest Neighbor. Bộ phân loại được huấn luyện bằng giá trị histogram màu R, G, B của hình ảnh. **Quy trình làm việc chung như sau:**

<p align="center">
  <img src="https://user-images.githubusercontent.com/22610163/35335133-a9632c70-0125-11e8-9204-0b4bfd0702a7.png" {width=35px height=350px}>
</p>

### Giải thích sơ đồ trên:

**Dữ liệu huấn luyện (Training feature vectors with class labels):**
- Các vector đặc trưng được lấy từ dữ liệu huấn luyện, mỗi vector đặc trưng có nhãn lớp tương ứng (ví dụ: màu sắc). Dữ liệu huấn luyện này sẽ bao gồm các giá trị đặc trưng của histogram màu và nhãn lớp (ví dụ: màu đỏ, xanh lá cây, v.v.).

**Thuật toán huấn luyện (Training algorithm):**
- Thuật toán huấn luyện được áp dụng trên các dữ liệu huấn luyện (đặc trưng và nhãn lớp) để tạo ra các tham số phân loại. Quá trình này sẽ giúp hệ thống học cách phân biệt các lớp màu dựa trên đặc trưng histogram màu.

**Tham số phân loại (Classifier parameters):**
- Sau khi thuật toán huấn luyện hoàn tất, hệ thống sẽ tạo ra các tham số phân loại, giúp xác định cách phân loại các dữ liệu thử nghiệm trong các bước tiếp theo.

**Web cam frame:**
- Hình ảnh hoặc khung hình được thu thập từ webcam sẽ được sử dụng làm dữ liệu thử nghiệm. Đặc trưng của khung hình này (histogram màu) sẽ được tính toán và chuyển thành vector đặc trưng để phân loại.

**Thuật toán phân loại (Classification algorithm):**
- Thuật toán phân loại (ở đây là K-Nearest Neighbors) sẽ sử dụng các tham số phân loại và dữ liệu thử nghiệm để xác định nhãn lớp của màu sắc trong khung hình thử nghiệm.

**Nhãn lớp màu sắc (Class label - Color Name):**
- Sau khi phân loại, hệ thống sẽ trả về nhãn lớp tương ứng với màu sắc, ví dụ: "Red", "Blue", v.v.
  
## Đối với dự án này:

**1.) Trích xuất đặc trưng** = Color Histogram

Color Histogram là một biểu diễn sự phân bố của các màu trong một hình ảnh. Đối với hình ảnh, một histogram màu biểu diễn số lượng điểm ảnh có các màu trong mỗi dải màu cố định, bao phủ không gian màu của hình ảnh, tập hợp tất cả các màu có thể có.

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/color_histogram.jpg">
</p>

**2.) Phân loại** = Thuật toán K-Nearest Neighbors

Trong thư mục “[src](https://github.com/ahmetozlu/color_recognition/tree/master/src)” có 2 Python classes:

- **[color_classification_webcam.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_classification_webcam.py):** thực hiện nhận dạng màu theo thời gian thực từ dòng webcam.

- **[color_classification_image.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_classification_image.py):** thực hiện nhận dạng màu trên một hình ảnh.

Trong thư mục “[color_recognition_api](https://github.com/ahmetozlu/color_recognition/tree/master/src/color_recognition_api)” có 2 Python classes:

- **[feature_extraction.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/color_histogram_feature_extraction.py):** trích xuất đặc trưng

- **[knn_classifier.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/knn_classifier.py):** lớp phân loại KNN

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

