# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600825
**Name:** Phan Tan Hung
**Date:** 10/6/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.0. | 10 | Agent hoạt động hoàn hảo, tìm đúng sản phẩm điện tử có giá tốt nhất và dữ liệu được chuẩn hóa sạch sẽ. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Agent đưa ra đề xuất phi thực tế (mua lò phản ứng hạt nhân) và thuật toán bị sai lệch do kiểu dữ liệu cột bị lỗi. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi sử dụng Garbage Data, AI Agent đã đưa ra câu trả lời sai lệch nghiêm trọng do hệ thống dữ liệu đầu vào bị suy giảm chất lượng nghiêm trọng bởi các yếu tố sau:
1. **Wrong Data Types (Sai kiểu dữ liệu):** Bản ghi "Broken Chair" có giá trị cột price là chuỗi `"ten dollars"` thay vì số. Điều này buộc Pandas phải coi toàn bộ cột `price` là kiểu chuỗi (object). Khi Agent gọi hàm tìm kiếm giá trị lớn nhất `idxmax()`, Pandas thực hiện so sánh chuỗi theo thứ tự bảng chữ cái thay vì so sánh số thực tế, làm sai lệch việc tìm kiếm sản phẩm tối ưu.
2. **Outliers (Ngoại lai cực hạn):** Bản ghi "Nuclear Reactor" có giá trị price quá lớn ($999999), là một ngoại lai không thực tế đối với các sản phẩm thương mại thông thường, khiến Agent bị đánh lừa và đề xuất sản phẩm này.
3. **Duplicate IDs (Trùng lặp ID):** Bản ghi "Laptop" và "Banana" cùng chia sẻ ID là 1, gây mất tính toàn vẹn dữ liệu (data integrity).
4. **Null values (Giá trị rỗng):** Bản ghi "Ghost Item" bị rỗng các trường cốt lõi như ID và Category, có thể gây ra lỗi runtime nếu logic Agent cố truy cập các thuộc tính này.

Tóm lại, dữ liệu rác làm mờ đi các tri thức chính xác và khiến thuật toán suy luận của Agent đưa ra các quyết định sai lầm.

---

## 3. Ket luan

**Quality Data > Quality Prompt?**

Hoàn toàn đồng ý. Chất lượng dữ liệu (Data Quality) quan trọng hơn nhiều so với việc tối ưu hóa câu lệnh (Prompt Engineering). Bản chất của mô hình AI là hoạt động theo nguyên lý "Garbage In, Garbage Out" (Dữ liệu rác vào, kết quả rác ra). Nếu cơ sở dữ liệu tri thức của Agent bị sai lệch, thiếu sót hoặc chứa thông tin độc hại, dù prompt có được viết chi tiết hay tối ưu đến đâu thì Agent vẫn sẽ đưa ra những câu trả lời sai lầm, thậm chí nguy hiểm. Dữ liệu chất lượng cao là điều kiện tiên quyết cho sự tin cậy của các hệ thống AI.
