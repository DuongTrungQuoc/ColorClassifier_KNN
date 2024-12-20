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
1. **Trích xuất đặc trưng:** Lấy giá trị histogram màu RGB từ [training images](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/tree/main/color_classifier/src/training_dataset)
2. **Huấn luyện bộ phân loại KNN:** Sử dụng giá trị histogram màu R, G, B để huấn luyện bộ phân loại KNN.
3. **Phân loại bằng KNN đã huấn luyện:** Đọc từng khung hình từ webcam, trích xuất đặc trưng và phân loại màu chính của khung hình bằng KNN đã huấn luyện.
---

## Lý thuyết

Dự án này phân loại màu bằng thuật toán K-Nearest Neighbor. Bộ phân loại được huấn luyện bằng giá trị histogram màu R, G, B của hình ảnh. **Quy trình làm việc chung như sau:**

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/KNN.png" {width=35px height=350px}>
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

**1) Trích xuất đặc trưng** = Color Histogram

Color Histogram là một biểu diễn sự phân bố của các màu trong một hình ảnh. Đối với hình ảnh, một histogram màu biểu diễn số lượng điểm ảnh có các màu trong mỗi dải màu cố định, bao phủ không gian màu của hình ảnh, tập hợp tất cả các màu có thể có.

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/color_histogram.jpg">
</p>

**2) Phân loại** = Thuật toán K-Nearest Neighbors

## Chi tiết dự án:

Trong thư mục “[src](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/tree/main/color_classifier/src)” có 2 Python classes:

- **[color_classification_webcam.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_webcam.py):** thực hiện nhận dạng màu theo thời gian thực từ dòng webcam.

- **[color_classification_image.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_image.py):** thực hiện nhận dạng màu trên một hình ảnh.

Trong thư mục “[color_recognition_api](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/tree/main/color_classifier/src/color_recognition_api)” có 2 Python classes:

- **[feature_extraction.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/color_histogram_feature_extraction.py):** trích xuất đặc trưng

- **[knn_classifier.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_recognition_api/knn_classifier.py):** lớp phân loại KNN

**1) Giải thích về  “[feature_extraction.py](https://github.com/ahmetozlu/color_recognition/blob/master/src/color_recognition_api/color_histogram_feature_extraction.py)"**

Tôi có thể lấy được histogram màu RGB của các hình ảnh bằng lớp Python này. Ví dụ, histogram màu RGB của một trong những hình ảnh màu đỏ được đưa ra dưới đây.

<p align="center">
  <img src="https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/assets/red.jpg" {width=25px height=250px}>
</p>

Tôi quyết định sử dụng số lượng bin của histogram, cái có giá trị đỉnh là số lượng điểm ảnh cho R, G và B làm đặc trưng để tôi có thể lấy được các giá trị R, G và B chủ đạo nhằm tạo ra các vector đặc trưng cho việc huấn luyện. Ví dụ, các giá trị R, G và B chủ đạo của hình ảnh màu đỏ được đưa ra trên đây là [254, 0, 2].

Tôi lấy các giá trị R, G, B bằng cách sử dụng Color Histogram cho mỗi hình ảnh huấn luyện rồi gán nhãn cho chúng vì KNN là một thuật toán học giám sát và tôi triển khai các vector đặc trưng này vào tệp csv. Do đó, tôi tạo ra bộ dữ liệu vector đặc trưng huấn luyện của mình. Bộ dữ liệu này có thể được tìm thấy trong tệp có tên [training.data](https://github.com/ahmetozlu/color_recognition/blob/master/src/training.data) trong thư mục src.

**2) Giải thích về “[knn_classifier.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_recognition_api/knn_classifier.py)”**

Lớp này cung cấp các phương thức chính sau:

1. Lấy dữ liệu huấn luyện
2. Lấy đặc trưng hình ảnh
3. Tính toán khoảng cách Euclid
4. Lấy k láng giềng gần nhất
5. Dự đoán màu sắc
6. Trả về dự đoán đúng/sai

**“[color_classification_webcam.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_classification_webcam.py)”** là lớp chính trong Project, nó cung cấp:

1. Gọi [feature_extraction.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_recognition_api/color_histogram_feature_extraction.py) để tạo dữ liệu huấn luyện thông qua trích xuất đặc trưng
2. Gọi [knn_classifier.py](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/color_recognition_api/knn_classifier.py) để phân loại

Bạn có thể tìm thấy dữ liệu huấn luyện [ở đây](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/tree/main/color_classifier/src/training_dataset).

Bạn có thể tìm thấy các đặc trưng được lấy từ dữ liệu huấn luyện [ở đây](https://github.com/DuongTrungQuoc/ColorClassifier_KNN/blob/main/color_classifier/src/training.data).

