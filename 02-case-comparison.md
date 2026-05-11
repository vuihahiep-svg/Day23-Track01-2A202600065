# 02 — Case Comparison (nhóm → bản copy cá nhân)

**Học viên:** Hoàng Hiệp — **Mã số:** 2A202600065  

**Sản phẩm nhóm / cá nhân:** OpenCalf  
**Mục đích:** Rút bài học metric cho Product ROI Dashboard.

---

## Bảy so sánh hai case

| Trường | Case thành công / tín hiệu tốt | Case cảnh báo / thất bại |
|--------|--------------------------------|--------------------------|
| **Case** | **Klarna — AI customer support** ([K1] OpenAI; [K2] PR Newswire; diễn giải hậu kỳ [K3] CNA / Yahoo / Business Insider). | **AgentGPT** [A1] — OSS “star cao”, dễ neo vào **usage** hơn **outcome**; bài học pitfall gắn với brief OpenCalf [O1]. |
| **Workflow có AI** | Chat CS: phân loại, trả lời FAQ, chuyển case phức tạp, tóm tắt trước escalate. | User tạo agent “tự động làm việc”; không khóa vào workflow vận hành cụ thể có đo lường. |
| **Metric chính** | Public: **~2/3 chat** AI xử lý; **2,3M** conversations; thời gian xử lý **11 phút → <2 phút**; **−25%** repeat inquiries; narrative **700 FTE** ([K1], [K2]). | Public thường là **stars / signups** [A1] — không có **daily active workflow** hay **business outcome** rõ. |
| **Metric đó chứng minh được gì?** | **Productivity + coverage** rất mạnh; có story **cost / FTE equivalent** (700 FTE narrative). | Chứng minh **viral interest**, không chứng minh **value bền vững** hay **chất lượng**. |
| **Metric đó chưa chứng minh được gì?** | **Quality** dài hạn (sau IPO / tái cân bằng nhân sự — [K3]); cần theo dõi repeat/complaint theo tier case ngoài PR ban đầu. | Không chứng minh **doanh thu**, **lead quality**, **giảm ticket**, hay **người vận hành quay lại**. |
| **Thiếu metric nào?** | Tách theo **tier độ phức tạp**; repeat contact 7 ngày; complaint rate. | **Retention của người triển khai**; **% session hoàn thành mục tiêu**; **QA trên output**. |
| **Bài học cho dashboard OpenCalf** | Lấy Klarna làm **cảnh báo**: đừng dừng ở “nhiều conversation / nhanh”. Phải ghép **productivity + quality + trust**. | Lấy AgentGPT làm **cảnh báo**: tránh KPI kiểu **prompt count**. OpenCalf thiết kế **“leads mới hôm nay”** làm **daily check-in hook** — metric gắn **việc sales/owner phải mở dashboard**. |

---

## Câu chốt

```markdown
Case thành công (Klarna) dạy nhóm tôi rằng:
- Volume và tốc độ xử lý là **tín hiệu vận hành mạnh**, nhưng vẫn cần **phân tầng case** và theo dõi **chất lượng / trust** để tránh “coverage cao che rework”.

Case cảnh báo (AgentGPT / hype OSS) dạy nhóm tôi rằng:
- **Stars và novelty không thay thế retention**; nếu không có **outcome đo được** (lead, đặt lịch, ticket resolved), user sẽ bỏ quên sau vài ngày.

Vì vậy dashboard nhóm tôi (OpenCalf) phải:
- Neo vào **4 workflow MVP** có điểm đo cuối: RAG đúng nguồn, lead extract, widget session, Zalo bridge.
- Có **ít nhất một chỉ số retention kinh doanh** (leads/ngày + CSV export) song song với **chỉ số quality** (citation / human QA sample).
```

---

## Tự kiểm tra

- [x] Hai case đối lập rõ (tín hiệu tốt vs cảnh báo).  
- [x] Có bài học gắn trực tiếp OpenCalf.  

---

## Tham chiếu (đã kiểm chứng)

| Mã | Nguồn |
|----|--------|
| [K1] | OpenAI — Klarna: [https://openai.com/index/klarna/](https://openai.com/index/klarna/) |
| [K2] | PR Newswire (Klarna): [https://www.prnewswire.com/news-releases/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month-302072744.html](https://www.prnewswire.com/news-releases/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month-302072744.html) |
| [K3] | CNA; Yahoo Finance; Business Insider — tổng hợp trong [`REFERENCES.md`](REFERENCES.md) |
| [A1] | AgentGPT: [https://github.com/reworkd/AgentGPT](https://github.com/reworkd/AgentGPT) |
| [D1] | Đề lab: `Day23-Track01-AI-Adoption/Day23-Lab-Assignment.md` |
| [O1] | Brief OpenCalf — [`REFERENCES.md`](REFERENCES.md) |

*Danh mục đầy đủ:* [`REFERENCES.md`](REFERENCES.md).
