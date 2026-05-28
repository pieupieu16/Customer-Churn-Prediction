# HỆ THỐNG DỰ ĐOÁN KHÁCH HÀNG RỜI ĐI (CHURN) - HƯỚNG DẪN HOÀN CHỈNH

##  Dữ liệu
- **`WA_Fn-UseC_-Telco-Customer-Churn.csv`** - Dữ liệu Telco Customer Churn (~7,000 khách hàng)

## Mục lục

###  Phần 1: Kiến thức cơ bản
- Hiểu bài toán Churn Prediction (Dự đoán khách hàng rời đi)
- Đây là **Classification Problem** (Bài toán phân loại)
- Khái niệm X (Input), y (Output)

### Phần 2: Làm quen dữ liệu
- Import thư viện cần thiết (pandas, numpy, matplotlib, seaborn)
- Đọc file CSV
- Khám phá kích thước dữ liệu
- Giải thích ý nghĩa các cột
- Phân biệt loại dữ liệu

###  Phần 3: Khám phá dữ liệu (EDA)
- Kiểm tra dữ liệu thiếu (Missing Values)
- Phân bố Churn: Pie chart & Bar chart
- So sánh Churn theo các đặc trưng (giới tính, hợp đồng, internet service, v.v.)
- Phân tích đặc trưng liên tục: tenure, MonthlyCharges, TotalCharges, Contract_Months

#### Insights chính từ EDA:
- **Hợp đồng tháng**: Tỷ lệ churn rất cao (42%)
- **Hợp đồng 2 năm**: Tỷ lệ churn rất thấp (3%)
- **Khách hàng mới (0-12 tháng)**: Có khuynh hướng rời đi cao nhất
- **Internet Fiber**: Tỷ lệ churn cao hơn DSL
- **Khách có bạn đời/người phụ thuộc**: Ít rời đi hơn

### Phần 4: Tiền xử lý dữ liệu (Data Preprocessing)
- **Fix lỗi dữ liệu**: Xử lý TotalCharges (11 giá trị trống)
- **Xóa dữ liệu cột không cần**: Bỏ customerID
- **Xóa dữ liệu trùng lặp**: Kiểm tra và xóa duplicate records
- **Xử lý outlier**: Không tìm thấy giá trị khả nghi
- **Mã hóa (Encoding)**:
  - Contract: Chuyển thành số tháng (1, 12, 24)
  - PaymentMethod: Mã hóa thành số
  - Binary Encoding: Yes/No → 1/0, Male/Female → 1/0
  - Group các dịch vụ: "No phone service" → "No"
  - One-Hot Encoding: Cho các cột danh mục còn lại

### Phần 5: Feature Engineering
- **Tenure_Cohort**: Phân nhóm khách hàng theo thời gian gắn bó
- **Total_Extra_Services**: Tổng số dịch vụ bổ sung
- **Is_Family**: Flag có gia đình hay không
- **Avg_Actual_Monthly_Charge**: Chi phí trung bình hàng tháng lịch sử
- **Charge_Fluctuation_Ratio**: Tỷ lệ biến động giá

### Phần 6: Xây dựng mô hình
- **Logistic Regression**: Thuật toán phân loại tuyến tính
  - Tách X, y
  - Chia train/test (80/20)
  - Chuẩn hóa (Scaling) dữ liệu số
  - Huấn luyện mô hình
  - Cách hoạt động & ứng dụng

- **Decision Tree**: Cây quyết định
  - Khởi tạo với max_depth=5
  - Huấn luyện trên dữ liệu chưa chuẩn hóa
  - Visualize cây quyết định
  
- **Random Forest**: Ensemble learning
  - n_estimators=76, max_depth=5
  - Xử lý cân bằng class_weight='balanced'
  - Huấn luyện trên dữ liệu chưa chuẩn hóa

### Phần 7: Đánh giá mô hình
Các metrics chính:
- **Accuracy**: Phần trăm dự đoán đúng tổng thể
- **Precision**: Trong những người dự đoán "rời đi", bao nhiêu thực sự rời?
- **Recall**: Trong tất cả những người thực sự rời, ta bắt được bao nhiêu?
- **F1-Score**: Cân bằng giữa Precision và Recall
- **Confusion Matrix**: Hiển thị TP, TN, FP, FN


###  Phần 8: Cải thiện & Tuning mô hình
- **Cross-Validation (K-Fold)**: Dùng StratifiedKFold với k=10
- **Hyperparameter Tuning**: Tìm tham số tối ưu cho Random Forest
- **So sánh mô hình**: Đánh giá 3 thuật toán khác nhau



#### 💡 Cross-Validation Results (Random Forest, k=10):
- **Accuracy**: ~0.78-0.80 (rất ổn định, σ ≈ 0.0106)
- **Precision**: 0.63-0.70 (khá tốt)
- **Recall**: 0.41-0.54 (khía cạnh cần cải thiện)
- Mô hình **không bị overfitting**, có khả năng tổng quát hóa tốt

## 🎓 Kiến thức Machine Learning

### 1. **Classification Problem** (Bài toán phân loại)
- Dự đoán kết quả rời rạc (Yes/No, 0/1)
- Khác với Regression (dự đoán giá trị liên tục như giá nhà, nhiệt độ)

### 2. **Encoding (Mã hóa dữ liệu)**
- **Binary Encoding**: Yes/No → 1/0 (2 giá trị)
- **One-Hot Encoding**: Chuyển danh mục thành cột số nhị phân

### 3. **Feature Engineering**
- Tạo đặc trưng mới từ dữ liệu hiện có
- Ví dụ: từ tenure (tháng) tạo Tenure_Cohort (nhóm khách hàng)

### 4. **Train/Test Split (80/20)**
- 80%: Dùng để huấn luyện (training set)
- 20%: Dùng để kiểm tra (test set)
- Đảm bảo tỷ lệ churn không thay đổi (stratify=y)

### 5. **Scaling (Chuẩn hóa)**
- Đặc biệt quan trọng cho: Logistic Regression
- Không bắt buộc cho: Tree-based models (Decision Tree, Random Forest)

### 6. **Cross-Validation (K-Fold)**
- Chia dữ liệu thành k phần (ở đây k=10)
- Huấn luyện k lần với mỗi phần khác nhau làm test set
- **Lợi ích**: Đánh giá mô hình ổn định hơn, phát hiện overfitting

### 7. **Class Weight Balancing**
- `class_weight='balanced'` giúp mô hình chú ý hơn đến class thiểu số (Churn=Yes)
- Xử lý imbalanced data

### 8. **Confusion Matrix**
```
                  Dự đoán KHÔNG rời   Dự đoán RỜI
Thực tế KHÔNG rời       TN              FP
Thực tế RỜI             FN              TP

TN (True Negative):  Dự đoán ở lại, thực sự ở lại ✓
FP (False Positive): Dự đoán rời, nhưng thực sự ở lại ✗
FN (False Negative): Dự đoán ở lại, nhưng thực sự rời ✗
TP (True Positive):  Dự đoán rời, thực sự rời ✓
```

### 9. **Precision vs Recall - Đánh đổi**
- **High Precision**: Khi dự đoán rời, chắc chắn đúng (ít sai lầm)
  - Chi phí: Bỏ sót nhiều khách hàng thực sự rời (Recall thấp)
- **High Recall**: Bắt được hầu hết khách hàng sắp rời
  - Chi phí: Chọn sai nhiều người (Precision thấp)

## 📌 Khuyến nghị thực hành

### Prioritization (Ưu tiên):
1. **Recall cao hơn Precision** trong ngữ cảnh này vì:
   - Chi phí tặng quà giảm giá < Chi phí mất khách hàng
   - Bỏ sót chỉ tốn thêm chi phí quà tặng, nhưng không tốn khách

2. **Tuning ngưỡng (threshold)**:
   - Logistic Regression: Điều chỉnh ngưỡng để tăng Recall nếu cần
   - Mặc định = 0.5, có thể giảm xuống 0.22 để bắt được nhiều khách hàng hơn

3. **Ensemble Methods** (Kết hợp nhiều mô hình):
   - Random Forest vượt trội hơn các thuật toán riêng lẻ
   - Bwatagi phương sai cao, ổn định trong cross-validation

## 🔗 Mối liên hệ giữa các phần

```
Dữ liệu thô → EDA → Preprocessing → Feature Engineering → 
              ↓
          Modeling (LR, DT, RF) → Evaluation → Tuning → 
              ↓
          Final Model for Production
```

## 📚 Tài liệu tham khảo
- Scikit-learn documentation
- Pandas documentation
- Matplotlib & Seaborn for visualization

