# ỨNG DỤNG PCA ĐỂ CẢI THIỆN MÔ HỒI HỒI QUY TUYẾN TÍNH

## Mục tiêu của Project

Đề tài này tập trung vào việc áp dụng Phân tích Thành phần Chính (Principal Component Analysis - PCA) để giảm chiều dữ liệu, từ đó cải thiện mô hình Hồi quy Tuyến tính trong bài toán dự đoán giá nhà. Chúng ta sẽ xây dựng và so sánh hiệu suất của mô hình trước và sau khi áp dụng PCA để đánh giá tác động của kỹ thuật này một cách toàn diện, từ tiền xử lý dữ liệu đến phân tích kết quả.

## Dataset Sử dụng

* **Tên Dataset**: Ames Housing Dataset

## Cấu trúc Project

Project này bao gồm một Jupyter Notebook chính (`PCA_in_LinearRegression.ipynb`) chứa toàn bộ quy trình từ tải dữ liệu, tiền xử lý, áp dụng PCA, xây dựng mô hình hồi quy tuyến tính, và phân tích kết quả.

## Các Bước Thực Hiện Chính

1.  **Thu thập và Tải dữ liệu**: Tải bộ dữ liệu Ames Housing Dataset.
2.  **Khám phá Dữ liệu (EDA)**: Phân tích sơ bộ để hiểu cấu trúc, phân phối và mối quan hệ giữa các biến.
3.  **Tiền xử lý Dữ liệu**:
    * Xử lý giá trị thiếu (Missing Values).
    * Mã hóa biến phân loại (Categorical Encoding).
    * Xử lý ngoại lai (Outliers).
    * Chuẩn hóa dữ liệu (Feature Scaling).
4.  **Phân tích Thành phần Chính (PCA)**:
    * Áp dụng PCA để giảm số chiều của dữ liệu, chuyển các đặc trưng gốc thành các thành phần chính không tương quan.
    * Xác định số lượng thành phần chính tối ưu để giữ lại phần lớn phương sai của dữ liệu.
5.  **Xây dựng Mô hình Hồi quy Tuyến tính**:
    * Xây dựng mô hình trên dữ liệu gốc (trước PCA).
    * Xây dựng mô hình trên dữ liệu đã được giảm chiều bằng PCA.
6.  **Đánh giá và So sánh Mô hình**:
    * Sử dụng các chỉ số đánh giá như R-squared, RMSE, MAE để so sánh hiệu suất của hai mô hình.
    * Phân tích sự ảnh hưởng của PCA đến độ chính xác và khả năng diễn giải của mô hình.

## Kết quả và Nhận định

Dựa trên phân tích trong notebook:

* **Về Đa cộng tuyến**: Ban đầu, dữ liệu có mức độ đa cộng tuyến **không quá cao**. Sau khi áp dụng PCA, hiện tượng đa cộng tuyến giảm đáng kể, thể hiện qua các chỉ số VIF (Variance Inflation Factor) thấp. Điều này cho thấy PCA đã thành công trong việc loại bỏ sự tương quan giữa các đặc trưng.
* **Về Giảm chiều**: Để giữ được phần lớn thông tin (ví dụ: 95% phương sai), chúng ta chỉ cần đến 5 hoặc 6 thành phần chính, giảm từ 8 đặc trưng gốc. Tuy nhiên, việc giảm từ 8 xuống 6 chiều là một sự cắt giảm **không đáng kể** trong bối cảnh này.
* **Về Hiệu suất Mô hình**: Khi so sánh mô hình Hồi quy Tuyến tính trên 8 đặc trưng gốc với mô hình PCR (Principal Component Regression) trên 6 thành phần chính, kết quả thường cho thấy **mô hình gốc có độ chính xác nhỉnh hơn một chút** (chỉ số R² cao hơn hoặc RMSE thấp hơn).
* **Lý do**: Cái giá phải trả (mất đi thông tin của 2-3 chiều dữ liệu) lớn hơn lợi ích thu được (chỉ giảm được một chút đa cộng tuyến không quá nghiêm trọng). Trong trường hợp này, việc giữ lại tất cả 8 đặc trưng gốc, vốn đã khá "cô đọng" và dễ diễn giải, lại là lựa chọn tốt hơn. Đây là một minh chứng rõ ràng cho thấy PCA không phải lúc nào cũng là lựa chọn tối ưu, đặc biệt khi đa cộng tuyến không phải là vấn đề nghiêm trọng nhất hoặc khi việc giảm chiều không mang lại lợi ích đáng kể về mặt tính toán/diễn giải.

## Bảng Tóm tắt Khi nào PCA Hiệu quả/Không Hiệu quả

| Tình huống            | PCA Hiệu quả                                     | PCA Không Hiệu quả                                |
| :-------------------- | :----------------------------------------------- | :------------------------------------------------ |
| **Tương quan Dữ liệu** | Đa cộng tuyến cao (nhiều biến phụ thuộc nhau)    | Các đặc trưng ít tương quan hoặc không đáng kể   |
| **Cấu trúc Dữ liệu** | Dữ liệu có nhiều biến, có thể tổng hợp thành ít thành phần hơn mà vẫn giữ thông tin | Dữ liệu ít biến, hoặc mỗi biến đã độc lập và quan trọng |
| **Mục tiêu chính** | Giảm chiều dữ liệu, loại bỏ nhiễu, tăng hiệu suất tính toán | Giữ lại khả năng diễn giải của các đặc trưng gốc |
| **Khả năng diễn giải** | Các thành phần chính khó diễn giải trực tiếp    | Các đặc trưng gốc dễ hiểu và ý nghĩa             |

## Cách Chạy Project

1.  **Clone repository về máy tính của bạn:**
    ```bash
    git clone [https://github.com/ThanhDustin/project-pca_in_linear.git](https://github.com/ThanhDustin/project-pca_in_linear.git)
    ```
2.  **Di chuyển vào thư mục project:**
    ```bash
    cd project-pca_in_linear
    ```
3.  **Cài đặt các thư viện cần thiết:**
    Đảm bảo bạn đã cài đặt Anaconda hoặc Miniconda. Sau đó, bạn có thể cài đặt các thư viện cần thiết bằng pip:
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn jupyter
    ```
    (Nếu thiếu thư viện nào khác, Jupyter Notebook sẽ báo lỗi và bạn có thể cài đặt bổ sung.)
4.  **Mở Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
5.  Trong giao diện Jupyter, mở file `PCA_in_LinearRegression.ipynb` và chạy từng cell.

---

**Tác giả:** ThanhDustin
**Ngày tạo/Cập nhật lần cuối:** 04/07/2025
