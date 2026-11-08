# Phân tích nghỉ việc nhân sự — IBM HR Analytics Employee Attrition

**Mid-term 2 · Project 5 · Học phần Khoa học dữ liệu trong kinh tế và kinh doanh (NEU)**

Nhóm: Nguyễn Thu Trang (11248108), Hoàng Minh Ngọc (11247707), Tạ Bùi Vân Anh (11244614), Nguyễn Hoàng Hà Anh (11242469), Nguyễn Quang Huy (11244988)

## Câu hỏi
Nhân viên nào có nguy cơ nghỉ việc, vì sao, và doanh nghiệp nên can thiệp ở đâu để chi phí bỏ ra có lãi?

## Nội dung repo
| File | Mô tả |
|---|---|
| `IBM_HR_Attrition_Analysis.ipynb` | Notebook đầy đủ 4 giai đoạn, chú thích từng khối lệnh |
| `Bao_cao_Project5_IBM_HR_Attrition.pdf` | Báo cáo phân tích chính thức |
| `WA_Fn-UseC_-HR-Employee-Attrition.csv` | Dữ liệu gốc (1.470 dòng × 35 cột) |
| `figures/` | 15 hình do notebook tạo ra |

## Cách chạy
1. Mở notebook trên Google Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/trangthu171106/ibm-hr-attrition-analysis/blob/main/IBM_HR_Attrition_Analysis.ipynb)
2. Chọn **Runtime → Run all**. Không cần cài thêm thư viện.
3. Nếu không có file CSV cục bộ, notebook tự tải bản gốc từ [kho GitHub của IBM](https://github.com/IBM/employee-attrition-aif360).

Thư viện: pandas, numpy, scipy, matplotlib, seaborn, scikit-learn. Seed ngẫu nhiên = 42.

## Phát hiện chính
- Làm thêm giờ làm rủi ro nghỉ việc tăng 2,9 lần; ở nhân viên cấp 1 làm thêm giờ, tỷ lệ nghỉ là 53%.
- Năm đầu tiên là giai đoạn rủi ro nhất: 34,9% nghỉ việc, chiếm 31,6% tổng số người nghỉ.
- Lương thấp chủ yếu phản ánh cấp bậc thấp; trả thấp hơn đồng cấp chỉ có bằng chứng vững ở cấp 1 (hiệu chỉnh Bonferroni).
- Cổ phiếu giữ chân nhân viên (21,1% → 9,9% sau khi kiểm soát hôn nhân); 100% nhân viên độc thân không có cổ phiếu.
- Lâu chưa được thăng chức là yếu tố rủi ro ẩn: OR = 1,74 [1,37; 2,23] trong mô hình Logit rút gọn (VIF ≤ 7,1).
- Đánh giá hiệu suất và % tăng lương không phân biệt người ở và người đi.
- Logistic Regression (đã tinh chỉnh): ROC-AUC 0,80 trên tập test, 0,85 khi kiểm định chéo; nhóm 20% rủi ro cao nhất chứa 53% số người nghỉ.
- Bỏ giới tính, tuổi, hôn nhân thì AUC gần như không đổi (0,79); mô hình chỉ nên dùng làm công cụ hỗ trợ có người rà soát.
- Chương trình giữ chân cho nhóm "làm thêm giờ + cấp 1" hòa vốn khi giữ lại được khoảng 17% số người sẽ nghỉ (hệ số thay thế 1x lương năm).

## Nguồn
- Dữ liệu: [Kaggle – IBM HR Analytics Employee Attrition & Performance](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
- Giáo trình: [Khoa học dữ liệu trong Kinh tế và Kinh doanh – NCT NEU](https://github.com/NCT-NEU/Sach_Khoa_hoc_du_lieu_python)
