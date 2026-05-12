# VinTelligence Datathon 2026 - The GridBreaker 

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![Team](https://img.shields.io/badge/Team-Waffle-brown?logo=buymeacoffee&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)

> Repository chứa toàn bộ source code và notebook của nhóm **Waffle** tham dự **VinTelligence Datathon 2026 - The GridBreaker**.

---

## Mục lục

- [Cấu trúc Repository](#-cấu-trúc-repository)
- [Cách chạy](#-cách-chạy)
- [Thành viên nhóm](#-thành-viên-nhóm)

---

## Cấu trúc Repository

```
📦 VinTelligence-Datathon2026
 ├── data/                               # Tất cả dữ liệu gốc từ Ban Tổ Chức
 ├── src/
 │    ├── MCQs.ipynb                     # Part 1 — Trả lời câu hỏi trắc nghiệm
 │    ├── EDA.ipynb                      # Part 2 — Khám phá và trực quan hóa dữ liệu (Cung cấp thông tin cho báo cáo)
 │    ├── Forecast EDA insights.ipynb    # Part 3 — Insight từ EDA phục vụ cho modeling
 │    └── Forecast.ipynb                 # Part 3 — Xây dựng & huấn luyện mô hình dự đoán revenue
 └── README.md
```


## Cách chạy

**1. Clone repository:**
```bash
git clone https://github.com/VinTelligence-Datathon2026.git
cd VinTelligence-Datathon2026
```

**2. Cài đặt dependencies:**
```bash
pip install -r requirements.txt
```

**3. Đặt dữ liệu vào đúng thư mục:**
```
data/
```

**4. Chạy các notebook**
Mở các file `.ipynb` trong thư mục `src/` bằng Jupyter Notebook, JupyterLab hoặc VS Code.
Sau đó, trên thanh công cụ:
- Chọn **Kernel > Restart Kernel and Run All Cells...**  
  *(hoặc nút **Restart & Run All**)*

## Thành viên nhóm

| Họ tên | Vai trò |
|--------|---------|
| Đinh Bảo Bảo | Trưởng nhóm |
| Nguyễn Thị Khánh Linh | Thành viên |
| Nguyễn Ngọc Minh | Thành viên |
| Ra Lan Đỗ Tú Trinh | Thành viên |

---

## 🛠️ My Technical Contributions (Ra Lan Đỗ Tú Trinh)

[cite_start]Trong dự án này, mình chịu trách nhiệm chính về thiết kế kiến trúc mô hình và xây dựng pipeline dự báo doanh thu (Phần 3 của báo cáo)[cite: 86]. Các đóng góp cụ thể bao gồm:

### 1. Robust Forecasting Pipeline Design
* [cite_start]Thiết kế quy trình huấn luyện theo nguyên tắc **Zero-Leakage**, sử dụng lag $> 549$ ngày để ngăn chặn việc rò rỉ thông tin tương lai[cite: 88].
* [cite_start]Triển khai phương pháp **Walk-forward Validation** (điểm cắt 2022-01-01) để đánh giá mô hình một cách khách quan theo dòng thời gian[cite: 89].
* [cite_start]Áp dụng **Recency Weighting** để ưu tiên dữ liệu gần đây mà vẫn bảo toàn giá trị từ dữ liệu lịch sử xa[cite: 90].

### 2. Advanced Feature Engineering
[cite_start]Xây dựng hệ thống đặc trưng đa tầng giúp mô hình học được các quy luật phức tạp[cite: 91]:
* [cite_start]**Cyclic Encoding:** Mã hóa các yếu tố thời gian (tháng, tuần, ngày)[cite: 91].
* [cite_start]**Event-driven Features:** Thiết kế các biến tiệm cận Tết (tet_proximity) và các ngày lễ E-commerce (11/11, 12/12)[cite: 92].
* [cite_start]**Interaction Features:** Tạo các biến tương tác như `promo_x_sessions` để bắt kịp các điểm bùng nổ doanh thu khi có sự kết hợp giữa khuyến mãi và lưu lượng truy cập lớn[cite: 96, 112].

### 3. Hybrid Ensemble Strategy
[cite_start]Thiết kế hệ thống Ensemble kết hợp 4 thành phần để tối ưu hóa sai số[cite: 98, 100]:
* [cite_start]**LightGBM (L1 & Tweedie):** Anchor chính để xử lý outlier và phân phối dữ liệu lệch phải[cite: 100].
* [cite_start]**XGBoost (MAE):** Tăng tính đa dạng (diversity) cho ensemble[cite: 100].
* [cite_start]**Prophet + LGB Residual:** Bắt các yếu tố mùa vụ có cấu trúc và bù đắp sai số bằng gradient boosting[cite: 100].
* [cite_start]**Optimization:** Sử dụng thuật toán **Nelder-Mead** để tìm trọng số tối ưu giúp tối thiểu hóa MAE trên tập validation[cite: 102].

### 4. Model Explainability & Post-processing
* [cite_start]**XAI (SHAP):** Sử dụng **SHAP Summary Plot** để minh bạch hóa tác động của 30 đặc trưng quan trọng nhất (như `Revenue_lag_730_med` và `tet_proximity`), chuyển đổi từ "hộp đen AI" sang insights kinh doanh[cite: 108, 109, 119].
* [cite_start]**Business Constraints:** Cài đặt các ràng buộc hậu xử lý thực tế như hệ số hiệu chỉnh tăng trưởng 1.14x và điều kiện tài chính $COGS \le 0.99 \times Revenue$[cite: 106, 107].

[cite_start]**Kết quả:** Giải pháp đạt độ chính xác cao với $R^2 \approx 0.79$, đảm bảo tính ổn định và khả năng ứng dụng thực tế[cite: 114, 115].

---

<p align="center">
  Made with ❤️ by <strong>Waffle</strong> · 2026
</p>
