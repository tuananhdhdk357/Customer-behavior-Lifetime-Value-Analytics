# 📊 DỰ ÁN PHÂN TÍCH HÀNH VI VÀ GIÁ TRỊ TRỌN ĐỜI KHÁCH HÀNG (CLV)

## 🎯 Tổng quan Dự án

Dự án này là một mô phỏng quy trình Phân tích Dữ liệu **End-to-End** theo tiêu chuẩn doanh nghiệp, tập trung vào lĩnh vực **Fintech E-commerce**. Mục tiêu chính là chuyển đổi dữ liệu giao dịch thô thành **thông tin chiến lược** thông qua việc xây dựng mô hình **Phân khúc Khách hàng RFM** và dự báo Giá Trị Trọn Đời Khách Hàng (CLV) tiềm năng.

Kết quả được trình bày dưới dạng Dashboard tương tác, cung cấp kiến nghị cụ thể cho các chiến dịch Marketing và duy trì khách hàng (Retention).

## 🚀 Vấn đề Kinh doanh & Mục tiêu Phân tích

### Vấn đề
Làm thế nào để xác định khách hàng có giá trị cao, khách hàng có nguy cơ rời bỏ, và tối ưu hóa ngân sách Marketing cho từng nhóm để tối đa hóa lợi nhuận.

### Mục tiêu
1.  **Tính toán chỉ số RFM:** Xác định Recency (Thời gian gần nhất), Frequency (Tần suất), và Monetary (Giá trị tiền tệ) cho từng khách hàng.
2.  **Phân khúc Khách hàng (Segmentation):** Sử dụng thuật toán Học máy (K-Means Clustering) để nhóm khách hàng thành các phân khúc có ý nghĩa chiến lược (ví dụ: Khách hàng Trung thành, Khách hàng Ngủ quên).
3.  **Đưa ra Kiến nghị Chiến lược:** Đề xuất các hành động cụ thể cho đội ngũ kinh doanh dựa trên hồ sơ hành vi của từng phân khúc.

## 🛠️ Công nghệ & Công cụ

| Lĩnh vực | Công cụ/Thư viện | Mục đích |
| :--- | :--- | :--- | |
| **Làm sạch/Tính năng** | Python (Pandas, NumPy) | Xử lý dữ liệu thô, tính toán các chỉ số RFM. |
| **Mô hình hóa** | Python (Scikit-learn, KMeans) | Áp dụng Clustering để phân khúc khách hàng. |
| **Trực quan hóa** | Power BI / Tableau | Xây dựng Dashboard tương tác và báo cáo kết quả. |
| **Thống kê** | Matplotlib, Seaborn | Phân tích Khám phá Dữ liệu (EDA). |

## 📦 Dataset

Dữ liệu được sử dụng là **Online Retail Data** (Dữ liệu Bán lẻ Trực tuyến), chứa thông tin giao dịch của một cửa hàng bán lẻ trực tuyến.

### Các trường dữ liệu chính:
* `InvoiceNo`: Mã đơn hàng.
* `StockCode`: Mã sản phẩm.
* `CustomerID`: Mã khách hàng (Yếu tố chính để phân tích).
* `InvoiceDate`: Ngày giao dịch.
* `Quantity`, `UnitPrice`: Số lượng và đơn giá (Dùng để tính `TotalRevenue`).

## 🗺️ Quy trình Phân tích Dữ liệu End-to-End

Dự án được thực hiện theo 4 giai đoạn chính, mô phỏng đúng quy trình làm việc của một Data Analyst.

### Giai đoạn 1: Thu thập & Chuẩn bị Dữ liệu (Data Cleaning)
* Tính toán cột **TotalRevenue** = `Quantity` * `UnitPrice`.
* **Xử lý dữ liệu thiếu:** Loại bỏ các hàng thiếu `CustomerID`.
* **Xử lý ngoại lai:** Loại bỏ các giao dịch có `Quantity` hoặc `UnitPrice` $\le 0$ (hàng trả lại, giao dịch lỗi).
* Chuyển đổi `InvoiceDate` sang định dạng datetime.

### Giai đoạn 2: Phân tích Khám phá & Kỹ thuật Tính năng (Feature Engineering - RFM)
* Xác định **Ngày Tham chiếu (Reference Date)**.
* **Tính toán 3 chỉ số RFM** cho mỗi khách hàng:
    * **Recency:** Số ngày kể từ lần mua cuối cùng.
    * **Frequency:** Tổng số giao dịch duy nhất.
    * **Monetary:** Tổng doanh thu đã chi tiêu.

### Giai đoạn 3: Mô hình hóa & Phân khúc Khách hàng (K-Means Clustering)
* **Chuẩn hóa dữ liệu:** Sử dụng biến đổi **Logarit** và **StandardScaler** để giảm thiểu độ lệch và đưa các biến RFM về cùng phạm vi.
* **Tìm K tối ưu:** Áp dụng **Elbow Method** để xác định số lượng cụm $K$ tối ưu (đã chọn $K=4$). 
* **Chạy K-Means:** Phân nhóm khách hàng và gán nhãn cụm (Cluster Labels).
* **Diễn giải:** Phân tích giá trị trung bình RFM của từng cụm để đặt tên chiến lược (Ví dụ: Khách hàng Trung thành, Khách hàng Ngủ quên).

### Giai đoạn 4: Trực quan hóa & Báo cáo Kinh doanh
* **Dashboard:** Xây dựng Dashboard tương tác trong Power BI (hoặc Tableau). 
* **Key Visuals:**
    * Biểu đồ Vòng hiển thị tỷ lệ khách hàng theo Phân khúc.
    * Biểu đồ Cột so sánh giá trị **Trung bình R, F, M** giữa các cụm.
    * Biểu đồ Tán xạ hiển thị sự phân tán của các cụm theo trục Recency và Monetary.

## 💡 Kết quả & Đề xuất Chiến lược (Key Takeaways)

Dự án đã xác định được 4 phân khúc khách hàng chính, với **[X]%** doanh thu được đóng góp bởi phân khúc **'Khách hàng Trung thành'**.

| Phân khúc (Ví dụ) | Hồ sơ RFM | Đề xuất Hành động |
| :--- | :--- | :--- |
| **Khách hàng Trung thành** | Rất thấp, F cao, M cao | **Duy trì & Tăng trưởng:** Mời tham gia chương trình VIP, giảm giá đặc biệt cho sản phẩm mới. |
| **Khách hàng Ngủ quên** | Rất cao, F thấp, M thấp | **Tái kích hoạt:** Gửi phiếu giảm giá giá trị cao (Win-back Offer) để khuyến khích giao dịch đầu tiên sau thời gian dài. |
| **Khách hàng Tiềm năng Mới** | R thấp, F thấp, M thấp | **Thúc đẩy Giao dịch Lặp lại:** Email Onboarding, Cross-sell các sản phẩm bổ sung. |

---


