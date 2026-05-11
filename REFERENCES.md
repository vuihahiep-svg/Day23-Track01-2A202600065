# Tham chiếu (References)

**Mục đích:** Liệt kê nguồn độc lập cho các **số liệu và case** dùng trong bài Day 23. Các chỉ số **baseline/target pilot** của OpenCalf trong dashboard là **giả định thiết kế** (xem mục [O1]).

**Ngày tra cứu / cập nhật liên kết:** 11/05/2026.

---

## Danh mục theo số

| ID | Nội dung được hỗ trợ | Nguồn |
|----|----------------------|--------|
| **K1** | Klarna AI assistant: **2,3M** cuộc hội thoại trong tháng đầu; **2/3** chat CS; tương đương **700** FTE; **CSAT** ngang human; **−25%** repeat inquiries; thời gian xử lý **<2 phút** so với **11 phút** trước đó; ước tính **+$40M** lợi nhuận 2024. | OpenAI — *Klarna customer story*: [https://openai.com/index/klarna/](https://openai.com/index/klarna/) |
| **K2** | Thông cáo báo chí Klarna lặp lại các KPI tháng đầu (2/3 chat, 2,3M conversations, v.v.). | PR Newswire: [https://www.prnewswire.com/news-releases/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month-302072744.html](https://www.prnewswire.com/news-releases/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month-302072744.html) |
| **K3** | **Hậu kỳ / điều chỉnh chiến lược:** Klarna IPO 2025, CEO nói đã “over indexed” vào cắt giảm chi phí nhờ AI, chuyển trọng tâm tăng trưởng; báo chí đồng thời đưa tin về lo ngại chất lượng và gán lại nhân sự hỗ trợ khách hàng. | Reuters (headline gốc thường dùng trong khóa học): `https://www.reuters.com/business/swedens-klarna-shifts-ai-focus-cost-cuts-growth-2025-09-10/` — *Truy cập tự động có thể trả 403; dùng bản phân phối lại:* CNA [https://www.channelnewsasia.com/business/swedens-klarna-shifts-ai-focus-cost-cuts-growth-5342726](https://www.channelnewsasia.com/business/swedens-klarna-shifts-ai-focus-cost-cuts-growth-5342726); Yahoo Finance [https://uk.finance.yahoo.com/news/europes-ai-poster-child-klarna-154000756.html](https://uk.finance.yahoo.com/news/europes-ai-poster-child-klarna-154000756.html); Business Insider (chất lượng AI / tái phân công): [https://www.businessinsider.com/klarna-reassigns-workers-to-customer-support-after-ai-quality-concerns-2025-9](https://www.businessinsider.com/klarna-reassigns-workers-to-customer-support-after-ai-quality-concerns-2025-9) |
| **I1** | Repo **Intervo/Intervo**: mã nguồn mở nền tảng voice + chat; **số sao GitHub biến động theo thời gian** (không dùng làm KPI vận hành). | GitHub: [https://github.com/Intervo/Intervo](https://github.com/Intervo/Intervo) |
| **I2** | Giấy phép / edition mã nguồn mở Intervo (MIT theo tài liệu dự án & trang docs). | Intervo Open Source docs: [https://docs.intervo.ai/open-source/introduction](https://docs.intervo.ai/open-source/introduction) |
| **I3** | Hướng dẫn cài đặt self-host Intervo (để chứng minh *độ phức tạp triển khai* có tài liệu chính thức, không dùng số “10+ key” như một định lượng đã kiểm chứng). | Intervo — *Setup & Installation*: [https://docs.intervo.ai/open-source/setup](https://docs.intervo.ai/open-source/setup) |
| **Z1** | **Quy mô Zalo tại Việt Nam:** báo chí dẫn số **MAU** ~**78,3 triệu** (nửa đầu 2025) và các mốc lân cận — dùng làm **bằng chứng thị trường kênh**, không đồng nhất với “user duy nhất”. | Vietnam.vn (78,3M MAU): [https://www.vietnam.vn/en/zalo-lap-ky-luc-78-3-trieu-nguoi-dung-thuong-xuyen-hang-thang](https://www.vietnam.vn/en/zalo-lap-ky-luc-78-3-trieu-nguoi-dung-thuong-xuyen-hang-thang); VietnamNet: [https://vietnamnet.vn/en/zalo-s-number-of-users-hits-78-3-million-putting-telcos-at-pipeline-trap-2436470.html](https://vietnamnet.vn/en/zalo-s-number-of-users-hits-78-3-million-putting-telcos-at-pipeline-trap-2436470.html) |
| **A1** | **AgentGPT:** ví dụ OSS có **sao GitHub rất cao** nhưng dễ rơi vào “hype / không neo workflow đo được” trong phân tích lab; repo có thể ở trạng thái archived (kiểm tra trên GitHub). | GitHub: [https://github.com/reworkd/AgentGPT](https://github.com/reworkd/AgentGPT) |
| **AD1** | Mô hình **ADKAR** (Awareness, Desire, Knowledge, Ability, Reinforcement) dùng để chẩn đoán rào cản adoption. | Prosci — *The ADKAR Model*: [https://www.prosci.com/methodology/adkar](https://www.prosci.com/methodology/adkar) |
| **L1** | **LiveKit** (WebRTC / agents) — tham chiếu kiến trúc voice trong brief sản phẩm; license MIT theo repo chính thức. | GitHub `livekit/livekit`: [https://github.com/livekit/livekit](https://github.com/livekit/livekit) |
| **D1** | Đề bài lab, rubric và ví dụ **Klarna** trong khung “Product ROI Dashboard”. | `Day23-Track01-AI-Adoption/Day23-Lab-Assignment.md` (trong repo học tập). |
| **O1** | **OpenCalf:** mô tả sản phẩm MVP, stack (NestJS, Qdrant, BullMQ, Zalo bridge, v.v.), **baseline/target pilot** trong bảng dashboard — là **bản thiết kế / product brief** kèm bài học pitfall do học viên/hướng dẫn cung cấp; **không** có URL bên thứ ba xác minh sản phẩm thương mại tại thời điểm nộp bài. | Bài báo cáo OpenCalf (phiên bản 1.1, 14/04/2026) — nội dung gốc trong yêu cầu học tập; cập nhật khi có repo hoặc báo cáo độc lập. |

---

## Ghi chú phương pháp

1. **GitHub stars:** là chỉ số **snapshot**; số chính xác tại thời điểm đọc có thể khác văn bản bài làm. Trong ma trận evidence, stars được xếp loại **proxy engagement**, không phải ROI.
2. **So sánh case:** Klarna (K1–K3) là **doanh nghiệp + báo cáo đối tác**; AgentGPT (A1) là **OSS consumer** — so sánh nhằm **bài học metric**, không khẳng định hai sản phẩm cùng phân khúc.
3. **Reuters:** URL gốc có thể chặn bot; nên ưu tiên đọc **CNA/Yahoo** cùng nội dung hoặc mở Reuters trên trình duyệt người dùng.

---

## Ánh xạ file bài làm ↔ mã tham chiếu

| File | Mã tham chiếu chính |
|------|---------------------|
| `01-case-evidence-matrix.md` | I1, I2, O1 |
| `02-case-comparison.md` | K1, K2, K3, A1, D1 |
| `03-product-roi-dashboard.md` | K1, K3, Z1, AD1, L1, I3, O1 |
| `04-reflection.md` | K1, K3, A1, D1 |
