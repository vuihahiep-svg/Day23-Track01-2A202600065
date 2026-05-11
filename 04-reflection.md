# 04 — Reflection (cá nhân)

**Học viên:** Hoàng Hiệp — 2A202600065  
**Yêu cầu:** 150–200 từ — một metric hoặc một giả định tôi sẽ sửa sau buổi lab.

---

Trước khi làm dashboard, tôi thiên về đo **số cuộc hội thoại** và **số lần tải widget** để chứng minh OpenCalf “đang được dùng”. Sau khi đọc case Klarna ([K1], [K2]) và diễn biến hậu kỳ ([K3]), cùng pitfall AgentGPT ([A1]) trong khung lab ([D1]), tôi nhậ ra đây là **measurement trap**: các chỉ số đó tăng được khi traffic tăng hoặc khi bot crawl, nhưng **không nói gì về việc chủ spa có kiếm được khách hay không**.

Giả định tôi sửa là: “nhiều chat = thành công adoption”. Thay vào đó, tôi sẽ neo dashboard vào **lead đủ điều kiện mỗi tuần** (có SĐT chuẩn, field bắt buộc điền) kết hợp **tỷ lệ QA người duyệt đạt** trên mẫu hội thoại. Hai chỉ số này buộc sản phẩm trả lời câu hỏi **giá trị** và **niềm tin**, đồng thời hỗ trợ cơ chế **Reinforcement** (owner mở dashboard vì có việc gửi sales), tránh kịch bản “Day 1 hay, Day 7 quên”. Nếu lead tăng mà QA giảm, tôi coi đó là tín hiệu **pivot** prompt hoặc RAG chứ không phải scale marketing.

*(Độ dài ~190 từ.)*

---

**Tham chiếu:** [K1] [K2] [K3] [A1] [D1] — xem URL đầy đủ trong [`REFERENCES.md`](REFERENCES.md).
