# PHÂN LOẠI TIN NHẮN RÁC (SPAM MESSAGE CLASSIFICATION) SỬ DỤNG HỌC MÁY

> **BÀI TẬP LỚN HỌC PHẦN: NHẬP MÔN HỌC MÁY (MCL)**  
> **Khoa Công nghệ Thông tin – Trường Đại học Đại Nam**  
> **Giảng viên hướng dẫn:** ThS. Lê Thị Thùy Trang  
> **Nhóm thực hiện:** NHÓM 5  

---

## 📌 1. Giới thiệu đề tài

Dự án nghiên cứu và xây dựng hệ thống phân loại tin nhắn SMS tự động thành hai nhóm:
* **Ham (0):** Tin nhắn bình thường.
* **Spam (1):** Tin nhắn rác, quảng cáo làm phiền hoặc lừa đảo viễn thông.

Toàn bộ quy trình tuân thủ nghiêm ngặt 6 bài giảng nền tảng của học phần Máy học: tiền xử lý văn bản, trích xuất đặc trưng Túi từ (Bag-of-Words) và TF-IDF, kỹ thuật đặc trưng cấu trúc SMS, huấn luyện và đối sánh 8 mô hình học máy (**Multinomial Naive Bayes**, **Bernoulli Naive Bayes**, **K-Nearest Neighbors**, **Decision Tree**), tối ưu hóa siêu tham số bằng **GridSearchCV 5-Fold**, phân tích ma trận nhầm lẫn và đề xuất cơ chế **Phân tầng rủi ro 3 mức**.

---

## 📊 2. Tập dữ liệu thực nghiệm

* **Nguồn:** [SMS Spam Collection - UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/228/sms+spam+collection).
* **Quy mô sạch:** 5.169 tin nhắn SMS độc nhất (sau khi lọc bỏ 403 bản ghi trùng lặp).
* **Phân phối nhãn:** 4.516 tin Ham (87,37%) và 653 tin Spam (12,63%).
* **Phân chia dữ liệu:** Stratified 80/20 (Huấn luyện: 4.135 mẫu | Kiểm thử: 1.034 mẫu).

---

## 🏆 3. Kết quả thực nghiệm chính trên tập kiểm thử

| Thuật toán | Luồng tiền xử lý | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Bernoulli Naive Bayes** | Luồng A (Baseline BoW) | **98.65%** | **98.39%** | **93.13%** | **0.9444** | **0.9950** |
| **Bernoulli Naive Bayes** | Luồng B (TF-IDF N-gram) | 98.26% | 100.00% | 86.26% | 0.9262 | 0.9956 |
| **Multinomial Naive Bayes** | Luồng B (TF-IDF N-gram) | 98.45% | 95.83% | 87.79% | 0.9163 | 0.9905 |
| **Multinomial Naive Bayes** | Luồng A (Baseline BoW) | 97.97% | 92.97% | 90.84% | 0.9119 | 0.9890 |
| **KNN (K=3, Cosine)** | Luồng B (TF-IDF N-gram) | 96.42% | 98.96% | 72.52% | 0.8462 | 0.9542 |
| **Decision Tree (CART)** | Luồng A (Baseline BoW) | 96.03% | 86.40% | 82.44% | 0.8408 | 0.8350 |

---

## 🚀 4. Cấu trúc thư mục kho mã nguồn

```text
├── PhanLoaiTinNhanRac_MayHoc.ipynb   # File Notebook chính chứa toàn bộ mã nguồn thực thi
├── README.md                          # Tài liệu giới thiệu và hướng dẫn chạy dự án
├── .gitignore                         # Tệp cấu hình loại trừ file rác khi đẩy Git
├── data/                              # Dữ liệu thực nghiệm
│   ├── spam.csv                       # Dữ liệu gốc
│   └── spam_cleaned.csv               # Dữ liệu sau khi làm sạch
├── figures/                           # Các biểu đồ trực quan hóa kết quả (300 DPI)
└── Template_BCTT_DATN-main/           # Toàn bộ mã nguồn LaTeX báo cáo bài tập lớn
    ├── main.tex                       # File biên dịch chính
    ├── settings.tex                   # Cấu hình định dạng
    ├── cover.tex                      # Bìa 1 & Bìa 2
    ├── frontmatter/                   # Lời nói đầu, danh mục bảng, hình, từ viết tắt
    ├── chapters/                      # Nội dung Chương 1 đến Chương 5
    └── backmatter/                    # Kết luận, tài liệu tham khảo
```

---

## 💻 5. Hướng dẫn chạy thử nghiệm

1. **Cài đặt các thư viện cần thiết:**
   ```bash
   pip install scikit-learn pandas numpy matplotlib seaborn
   ```
2. **Khởi chạy Notebook:**
   Mở tệp `PhanLoaiTinNhanRac_MayHoc.ipynb` trong VS Code hoặc Jupyter Lab và chọn **Run All Cells**.

