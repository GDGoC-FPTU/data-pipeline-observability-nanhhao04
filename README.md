[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23704406&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** 2A202600131
**Name:** Nguyen Anh Hao

---

## Mô tả (Description)

Dự án này tập trung vào việc xây dựng một pipeline ETL (Extract, Transform, Load) tự động để xử lý dữ liệu thương mại điện tử từ JSON sang CSV. Mục tiêu chính là áp dụng các kỹ thuật quan sát dữ liệu (Data Observability) để đảm bảo chất lượng dữ liệu đầu vào cho AI Agent, đồng thời thực hiện Stress Test để thấy rõ tác động của dữ liệu "bẩn" đối với độ chính xác của mô hình.

---

## Cách chạy (How to Run)

### Prerequisites
Cài đặt các thư viện cần thiết:
```bash
pip install pandas pytest
```

### Chạy ETL Pipeline
Script này sẽ đọc `raw_data.json`, lọc các bản ghi lỗi, thực hiện tính toán chiết khấu và chuẩn hóa danh mục:
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)
1. Tạo dữ liệu rác (Garbage Data):
   ```bash
   python generate_garbage.py
   ```
2. Chạy mô phỏng so sánh kết quả giữa dữ liệu Sạch và dữ liệu Rác:
   ```bash
   python agent_simulation.py
   ```

### Kiểm tra tự động (Autograder)
Chạy bộ test để xác nhận kết quả bài làm:
```bash
pytest tests/test_autograder.py
```

---

## Cấu trúc thư mục

```
├── solution.py              # Script chính thực hiện ETL Pipeline
├── processed_data.csv       # Dữ liệu đã được làm sạch và biến đổi
├── experiment_report.md     # Báo cáo chi tiết kết quả Stress Test
├── agent_simulation.py      # Script mô phỏng phản hồi của AI Agent
├── generate_garbage.py      # Script tạo dữ liệu rác để thử nghiệm
└── README.md                # Hướng dẫn và thông tin dự án
```

---

## Kết quả (Results)

- **ETL Performance**: Xử lý thành công 3/5 bản ghi từ dữ liệu thô (loại bỏ 2 bản ghi không hợp lệ).
- **Data Quality**: Đảm bảo 100% bản ghi trong `processed_data.csv` có giá dương, danh mục được chuẩn hóa Title Case và có timestamp.
- **Stress Test**: Agent hoạt động chính xác 10/10 với dữ liệu sạch, nhưng giảm xuống 2/10 khi gặp dữ liệu rác do bị ảnh hưởng bởi giá trị ngoại lai (outliers).
