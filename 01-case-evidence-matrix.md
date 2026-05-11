# 01 — Case Evidence Matrix (cá nhân)

**Học viên:** Hoàng Hiệp — 2A202600065  
**Case được phân tích:** **Intervo** (nền tảng voice + text agent mã nguồn MIT, tương đồng phân khúc với **OpenCalf** trong báo cáo thiết kế [O1]).  
**Nguồn xác minh:** repo GitHub & docs chính thức [I1], [I2]; so sánh chiến lược với OpenCalf lấy từ brief [O1].

---

## A. Case Evidence Matrix

| Trường | Trả lời |
|--------|---------|
| **Case** | Intervo — OSS multimodal (voice qua Twilio + text), workflow canvas, RAG (ChromaDB), multi-provider STT/TTS/LLM, Docker self-host, embeddable widget. |
| **AI được dùng trong workflow nào?** | (1) Thiết kế luồng hội thoại trên canvas; (2) Trả lời khách voice/text với RAG; (3) Goal-oriented agents (thu thập thông tin theo mục tiêu). |
| **Người dùng chính là ai?** | Developer / team kỹ thuật triển khai cho doanh nghiệp; end-user là khách hàng cuối qua widget hoặc cuộc gọi. |
| **Họ đo metric gì?** | Công khai chủ yếu là **GitHub stars** (số sao **thay đổi theo ngày**, ví dụ ~360+ tại 05/2026 — xem [I1]), và roadmap tính năng (vd. analytics). Không có báo cáo KPI vận hành chuẩn enterprise (resolution time, lead quality, v.v.) trong repo công khai. |
| **Metric đó thuộc layer nào?** | Chủ yếu **Activation / Engagement proxy** (stars = quan tâm cộng đồng), **không** phải Productivity/Quality/Value đã được công bố. |
| **Metric đó chứng minh được gì?** | Có **interest** ban đầu từ developer; có **khả năng kỹ thuật** (multimodal, RAG, Docker). |
| **Metric đó chưa chứng minh được gì?** | **Không chứng minh** adoption thực tế trong SME, ROI, chất lượng trả lời tiếng Việt, retention người vận hành, hay giảm chi phí support. Stars không phản ánh “AI đang chạy trong workflow thật”. |
| **Thiếu metric nào?** | **Lead → deal** hoặc **repeat inquiry** sau AI; **time-to-first-value** sau `docker compose up`; **% conversation có human review**; **WER/CSAT theo ngôn ngữ**; **cost per resolved session** (Twilio + LLM). |
| **Rủi ro lớn nhất** | **Measurement trap:** đo “đã cài” / “đã star” thay vì đo **giá trị vận hành**; **setup friction** (10+ API keys) làm giảm activation thật. |
| **Bài học cho dashboard nhóm (OpenCalf)** | Dashboard OpenCalf **không** lấy stars làm KPI chính. Ưu tiên: **leads mới/ngày**, **RAG citation rate**, **median time-to-reply**, **Zalo/widget session completion**, và **QA sample pass** — gắn với “5 phút thấy giá trị” trong thiết kế MVP. |

---

## Tự kiểm tra

- [x] Không chỉ kể chuyện — có phân tích layer metric.  
- [x] Có metric cụ thể (stars, roadmap, setup).  
- [x] Nêu rõ chứng minh được / chưa chứng minh được.  
- [x] Có ≥1 bài học áp dụng cho dashboard OpenCalf.  

---

## Tham chiếu (đã kiểm chứng)

| Mã | Nguồn |
|----|--------|
| [I1] | Intervo trên GitHub — [https://github.com/Intervo/Intervo](https://github.com/Intervo/Intervo) |
| [I2] | Intervo Open Source — docs giới thiệu / license: [https://docs.intervo.ai/open-source/introduction](https://docs.intervo.ai/open-source/introduction) |
| [O1] | OpenCalf — *product brief* học viên (không có nguồn bên thứ ba độc lập); xem tổng hợp mã nguồn tham chiếu: [`REFERENCES.md`](REFERENCES.md) |

*Danh mục đầy đủ:* [`REFERENCES.md`](REFERENCES.md).
