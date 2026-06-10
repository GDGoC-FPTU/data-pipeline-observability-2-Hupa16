[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112896&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** aibuildduanvinunihupa16@gmail.com
**Name:** Phan Tan Hung
**Student ID:** AI20K-2A202600825

---

## Mo ta

Bài lab này xây dựng một ETL Pipeline hoàn chỉnh và tự động bằng Python và Pandas. Mục tiêu của dự án là trích xuất dữ liệu từ file `raw_data.json`, thực hiện kiểm tra chất lượng dữ liệu để lọc bỏ các bản ghi không hợp lệ (giá bán không dương hoặc thiếu nhóm sản phẩm), chuẩn hóa nhóm sản phẩm thành Title Case, tính toán giá chiết khấu 10% và ghi nhận timestamp xử lý. Cuối cùng, dữ liệu sạch được lưu vào file `processed_data.csv`. 

Dự án cũng tiến hành stress test để đo lường và phân tích tác động trực tiếp của chất lượng dữ liệu (Data Quality) đối với khả năng suy luận và độ chính xác của AI Agent.

---

## Cach chay (How to Run)

### Prerequisites
Đảm bảo bạn đã kích hoạt virtual environment và cài đặt các thư viện cần thiết:
```bash
python -m venv venv
.\venv\Scripts\activate
pip install pandas pytest
```

### Chay ETL Pipeline
Lệnh chạy pipeline để làm sạch và chuẩn hóa dữ liệu:
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
Để chạy mô phỏng thí nghiệm so sánh giữa Clean Data và Garbage Data:
```bash
# 1. Tạo file dữ liệu rác chứa các lỗi phổ biến (outliers, sai kiểu dữ liệu, trùng lặp, rỗng)
python generate_garbage.py

# 2. Chạy stress test mô phỏng phản hồi của AI Agent
python agent_simulation.py
```

### Chay Autograder Test
Để chạy bộ kiểm tra tự động xem điểm số bài làm:
```bash
python -m pytest tests/test_autograder.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── garbage_data.csv         # File dữ liệu rác phục vụ stress test
├── agent_simulation.py      # Mô phỏng AI Agent đọc dữ liệu
├── generate_garbage.py      # Script tạo dữ liệu rác
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- **Tổng số bản ghi ban đầu:** 5 bản ghi.
- **Số bản ghi hợp lệ sau khi validate:** 3 bản ghi (Laptop, Chair, Monitor).
- **Số bản ghi bị loại bỏ (Dropped):** 2 bản ghi (Mystery Box do giá <= 0; Phone do thiếu Category).
- **Kết quả Stress Test:** AI Agent đưa ra câu trả lời chính xác 10/10 trên dữ liệu sạch (`processed_data.csv`), nhưng đưa ra phản hồi sai lệch nghiêm trọng 1/10 (đề xuất mua Lò phản ứng hạt nhân) khi sử dụng dữ liệu rác (`garbage_data.csv`).
