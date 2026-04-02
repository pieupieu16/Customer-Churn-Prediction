# HỆ THỐNG DỰ ĐOÁN KHÁCH HÀNG RỜI ĐI (CHURN) - HƯỚNG DẪN HOÀN CHỈNH

## Data
- **`WA_Fn-UseC_-Telco-Customer-Churn.csv`** - Dữ liệu Telco Customer Churn
## Mục lục:

###  Phần 1: Hiểu bài toán (Cell 1-3)
- Churn là gì?
- Đây là classification problem

### Phần 2: Làm quen dữ liệu (Cell 4-8)
- Import thư viện
- Đọc file CSV
- Xem 5 dòng đầu
- Giải thích ý nghĩa từng cột
- Phân biệt X (input) vs y (output)

### Phần 3: Khám phá dữ liệu - EDA (Cell 9-14)
- Kiểm tra dữ liệu thiếu
- Phân bố Churn (pie chart & bar chart)
- So sánh churn theo giới tính, loại hợp đồng, dịch vụ internet
- Insight rút ra từ biểu đồ

### Phần 4: Tiền xử lý dữ liệu (Cell 15-21)
- Fix lỗi dữ liệu (TotalCharges)
- Xóa cột không cần thiết
- Xóa dữ liệu trùng lặp
- Xử lý dữ liệu nhiễu
- Mã hóa (Encoding) dữ liệu chữ → số
- Tách X, y
- Tách train/test (80/20)
- Chuẩn hóa (Scaling) dữ liệu số

### Phần 5: Xây dựng mô hình (Cell 22-23)
- Giải thích Logistic Regression 
- Huấn luyện mô hình

### Phần 6: Đánh giá mô hình (Cell 24-26)
- 4 metric chính: Accuracy, Precision, Recall, F1-Score
- Giải thích bằng ví dụ đời thường
- Confusion Matrix và phân tích

### Phần 7: Cải thiện mô hình (Cell 27-30)
- Xây dựng Decision Tree
- Xây dựng Random Forest
- So sánh 3 mô hình
- Vẽ biểu đồ so sánh




## 📊 Kết quả dự kiến

Model               Recall  Precision  Accuracy  F1-Score
Logistic Regression 0.794118   0.493355  0.728500  0.608607
Decision Tree       0.807487   0.487884  0.723525  0.608258
Random Forest       0.764706   0.509804  0.742004  0.611765
