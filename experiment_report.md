# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600131
**Name:** Nguyen Anh Hao
**Date:** 2026-04-24

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Agent tim dung san pham phu hop va gia hop ly. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Agent bi danh lua boi du lieu ngoai lai (outlier) cuc doan. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai khi sử dụng Garbage Data vì dữ liệu đầu vào chứa nhiều vấn đề nghiêm trọng về chất lượng. Cụ thể, sự xuất hiện của "Nuclear Reactor" với mức giá cực đoan ($999999) đã khiến logic tìm kiếm giá cao nhất của Agent bị sai lệch hoàn toàn so với mục đích tìm kiếm sản phẩm điện tử thông thường. Ngoài ra, việc thiếu kiểm soát về kiểu dữ liệu (ví dụ: "ten dollars" thay vì số) có thể gây ra lỗi runtime nếu logic tính toán không đủ chặt chẽ. Các bản ghi trùng lặp ID hoặc có giá trị null cũng làm nhiễu hệ thống tri thức của Agent, khiến nó không thể đưa ra câu trả lời chính xác và đáng tin cậy. Khi dữ liệu "bẩn" được đưa vào pipeline mà không qua các bước validation như kiểm tra giá dương hay chuẩn hóa danh mục, Agent sẽ tiếp nhận thông tin sai lệch như là sự thật (ground truth), dẫn đến các phản hồi không chỉ sai về mặt logic mà còn có thể gây nguy hiểm hoặc vô lý trong thực tế.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Đồng ý. Mặc dù một Prompt tốt có thể giúp Agent lọc bớt nhiễu, nhưng nếu dữ liệu cơ sở đã bị "nhiễm độc" hoặc sai lệch hoàn toàn, Agent vẫn sẽ đưa ra kết quả sai dựa trên những thông tin sai đó (Garbage In, Garbage Out). Chất lượng dữ liệu là nền tảng cốt lõi để xây dựng một hệ thống AI tin cậy.
