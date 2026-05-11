# 03 — Product ROI Dashboard (v2 sau red-team)

**Sản phẩm:** **OpenCalf** — mã nguồn mở (MIT trong *brief* thiết kế [O1]) để triển khai agent AI **voice & chat** với dữ liệu riêng trong vài phút; kênh MVP: **Web widget** (text + voice LiveKit [L1]), **Zalo Personal** (OpenClaw sidecar — mô tả kiến trúc trong [O1]).  
**Stack tham chiếu:** Theo [O1]: NestJS, PostgreSQL + Drizzle, Qdrant + LlamaIndex.TS, Redis + BullMQ, Next.js dashboard, widget Vite.  
**Người dùng chính:** Owner SME / marketing / CSKH; developer nội bộ hoặc agency self-host; khách cuối qua widget & Zalo.

---

# Part A — Adoption Context

## A.1 Thách thức & bối cảnh

| Trường | Trả lời |
|--------|---------|
| **Thách thức áp dụng AI** | SME VN cần chatbot **hiểu tài liệu nội bộ** + **bắt lead** trên **Zalo/Web**, không muốn **lock-in SaaS** và cần giảm **độ phức tạp triển khai** so với OSS tương tự (vd. Intervo có hướng dẫn self-host nhiều thành phần [I3]; con số “10+ API keys” trong brief [O1] là **ước lượng pain point**, không đếm tay trong bài này). |
| **Tình huống xuất phát** | Khách hỏi giá/dịch vụ trên web & Zalo; nhân sự không kịp trả lời 24/7; dữ liệu nằm trong PDF/DOCX. |
| **Dấu hiệu bị kẹt** | Cài chatbot xong **không ai mở dashboard**; không đo được **lead thật**; tiếng Việt voice/STT kém → bỏ dùng. |
| **Vì sao đáng giải** | **Zalo:** thị trường VN có **MAU ~78,3 triệu** (báo chí nửa đầu 2025; [Z1]) — kênh nhắn tin phổ biến; self-host + BYO API giảm lock-in; **retention loop** qua lead extraction (thiết kế [O1]). |

## A.2 Sản phẩm AI

| Trường | Trả lời |
|--------|---------|
| **Tên sản phẩm** | OpenCalf |
| **Người dùng chính** | Owner vận hành; nhân viên sales xem lead; dev vận hành stack Docker. |
| **Bối cảnh** | Spa/clinic/e-commerce SME: FAQ + thu SĐT/ngân sách/khu vực qua hội thoại. |
| **Mục tiêu KBH / vận hành** | Giảm thời gian trả lời lặp lại; tăng **lead có cấu trúc** export được; giữ **niềm tin** (trích dẫn nguồn). |
| **Không trong phạm vi MVP** | Zalo OA chính thức, Facebook/WA, workflow canvas, multi-tenant SaaS, billing Stripe trong core OSS. |

## A.3 Bốn workflow chính (đo được)

| # | Tên quy trình | Vai trò AI | Điểm người kiểm tra | Khi AI sai thì xử lý |
|---|---------------|------------|---------------------|----------------------|
| **1** | **Ingest KB → RAG trả lời** | Chunk/embed (Qdrant); trả lời có **source attribution**; từ chối khi không đủ bằng chứng. | Owner spot-check **citation** đúng trang/đoạn; QA sample hằng tuần. | Tắt “creative mode”; cập nhật prompt/guardrail; re-index tài liệu; ghi `qa_flag` trên message. |
| **2** | **Hội thoại widget / Zalo → Lead extract** | Sau session: LLM extract theo **JSON schema động** (BullMQ); lưu PostgreSQL. | Sales xác minh lead (gọi thử); owner xem field **null rate** cao bất thường. | Sửa schema mô tả; fallback **human-only** field; rollback prompt extract. |
| **3** | **Widget text (SSE)** | Streaming trả lời; session `localStorage`; public token scoped theo agent. | Owner đọc **conversation logs**; so khớp với policy giá/khuyến mãi. | Khóa token; rate limit; template trả lời an toàn; escalate sang người. |
| **4** | **Voice trong widget (LiveKit) + STT/TTS đa nhà cung cấp** | VAD/turn detection; pipeline STT→LLM+RAG→TTS; transcript hiển thị. | Owner nghe **mẫu ghi âm** + đọc transcript lỗi từ khách. | Đổi provider (FPT/Vbee cho VI); tăng **confidence threshold**; chuyển sang text-only khi đỏ. |

## A.4 ADKAR — rào cản chính

| Stage | Nhận định |
|-------|-----------|
| Awareness | Trung bình: owner biết “cần AI” nhưng chưa biết **OpenCalf khác gì ChatGPT tab**. |
| Desire | Cao nếu có **Zalo + tiếng Việt**; thấp nếu setup lâu. |
| Knowledge | Trung bình: cần hiểu **agent token**, upload KB, schema lead. |
| Ability | **Cao** — Docker + API keys (rào cản thực tế với SME không IT). |
| **Reinforcement** | **Rào cản chính:** nếu không có **lý do quay lại dashboard** (lead mới), adoption **suy giảm** như kịch bản “star cao, không outcome” của AgentGPT [A1]. |

**Barrier chính (chọn 1):** **Reinforcement** — thiếu “daily hook” thì owner ngừng mở tool dù chatbot vẫn chạy (khớp định nghĩa giai đoạn *Reinforcement* trong ADKAR [AD1]).

```markdown
Reinforcement: OpenCalf phải khiến owner **thấy lead mới mỗi sáng** + export CSV cho sales; nếu không, sản phẩm rơi vào vòng “Day 1 cool, Day 7 quên”.
```

## A.5 Ba tactic tăng adoption

| Tactic | Barrier | Workflow | Người phụ trách | Khi hoàn thành |
|--------|---------|----------|-----------------|----------------|
| **1. “Leads hôm nay”** trên home dashboard + digest email tuỳ chọn | Reinforcement | 2, 3, 4 | Product Owner / Growth | Sprint MVP tuần 1 (ngày 4–5 roadmap). |
| **2. QA sample 20 cuộc/tuần** + checklist citation | Knowledge + Quality | 1, 3 | QA Lead / Owner | Tuần đầu sau go-live; lặp hằng tuần. |
| **3. “0-key trial”** (Ollama/Groq) trong `docker compose` + `.env` tối giản | Ability | 1 | DevRel / Backend Lead | Trước public beta; README 5 bước. |

---

# Part B — ROI Dashboard (8 cột)

> Cột: **Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix (v2)**

## B.1 Chỉ số toàn sản phẩm

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|-------|--------|----------:|--------:|-------------|-------|----------------|-----|
| **Activation** | **TTV (time-to-value)** — phút từ `docker up` đến **câu trả lời RAG đúng** từ PDF mẫu | 45 phút (giả định SME lần đầu) | **≤10 phút** (mục tiêu đề) | Install logs + `first_success_at` trong DB | DevRel Lead | Baseline tự khai báo → gamed | Đo bằng **scripted smoke test** + telemetry opt-in |
| **Retention / Value** | **Qualified leads / tuần / agent** (schema đủ field bắt buộc) | 2 lead/tuần (pilot) | **≥8** sau 6 tuần playbook | `leads` table + validation rule | Sales Owner | Lead **rác** làm inflate | Thêm **precision**: % lead có SĐT hợp lệ + contacted |
| **Trust / Quality** | **% trả lời có citation** khi retrieval hit KB | 40% | **≥85%** | RAG trace logs + message metadata | QA Lead | Citation **giả** (đúng chunk nhưng sai ý) | V2: thêm **human QA pass rate** trên mẫu |

## B.2 Workflow 1 — Ingest KB → RAG Q&A

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|-------|--------|----------:|--------:|-------------|-------|----------------|-----|
| Activation | **% ingest job thành công** (PDF/DOCX/ảnh) | 85% | ≥98% | BullMQ job status + object storage | Backend Lead | Fail im lặng | Alert Slack + retry policy hiển thị UI |
| Engagement | **KB queries / active agent / tuần** | 20 | ≥60 | `messages` role=user | Product Owner | Chỉ là usage | Ghép với **citation rate** |
| Productivity | **Median tokens retrieved → first token** | 2.5s | ≤1.2s | APM + RAG span | Backend Lead | Nhanh nhưng sai | V2: giữ + **rerank hit@k** |
| Quality | **Human QA pass rate** (sample 20/tuần) | 75% | ≥90% | QA sheet + `message_id` | QA Lead | Sample nhỏ | Tăng sample theo traffic tier |
| Trust | **“Không đủ bằng chứng” rate** khi không có chunk | 10% | 5–15% có chủ đích | Policy flags | QA Lead | Quá ít → overclaim | Tune prompt + min score |
| Value | **Giảm % câu hỏi lặp** so tuần baseline | 0% | −30% | dedupe hash câu hỏi | Ops Lead | Giảm do traffic giảm | Chuẩn hoá theo **sessions** |

## B.3 Workflow 2 — Lead extraction → Dashboard

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|-------|--------|----------:|--------:|-------------|-------|----------------|-----|
| Activation | **% conversation tạo được lead row** | 50% | ≥70% | `conversations`→`leads` | Product Owner | Extract **mọi lúc** → spam | Chỉ chạy khi **session end** + min turns |
| Engagement | **Owner login có xem tab Leads** | 2 lần/tuần | 5 lần/tuần | Audit `page_views` | Growth | Login không = value | V2: track **CSV export** |
| Productivity | **Thời gian sales từ lead → first call** | 24h | ≤4h | CRM timestamp / manual log | Sales Lead | CRM không kết nối | Export CSV chuẩn + webhook sau MVP |
| Quality | **Lead precision** (% SĐT đúng chuẩn VN) | 60% | ≥85% | Sales validation + bitmask field | Sales Lead | LLM bịa SĐT | Regex+libphonenumber; human confirm |
| Trust | **Opt-out / “không thu thập”** respect rate | 100% | 100% | consent flag | Legal/Owner | Privacy | Log policy; xoá lead on request |
| Value | **Lead → opportunity rate** | 8% | ≥15% | CRM stage | Sales Lead | Biến ngoài AI | A/B playbook sales |

## B.4 Workflow 3 — Widget text (SSE)

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|-------|--------|----------:|--------:|-------------|-------|----------------|-----|
| Activation | **% embed có ≥1 user message** trong 7 ngày | 35% | ≥60% | Widget analytics SDK | Growth | Gamed bởi bot | V2: bot score + IP rate limit |
| Engagement | **Median session length (turns)** | 4 | ≥6 | `messages` per `session_id` | Product Owner | Turns cao do loop lỗi | Phát hiện **repeat same intent** |
| Productivity | **Median first response latency** | 3s | ≤1.5s | API latency logs | Backend Lead | Chỉ đo happy path | V2: p95 + error budget |
| Quality | **Repeat question trong 24h** (same session) | 12% | ≤6% | session analytics | QA Lead | Khách hỏi lại do người | Tách **AI vs human** follow-up |
| Trust | **Escalation / “gặp người” click rate** | — | ≤15% sessions | widget events | CS Lead | Thấp quá → AI che giấu lỗi | Copy rõ “AI có thể sai” |
| Value | **% session có lead qualified** | 15% | ≥25% | joins `leads` | Sales Owner | — | — |

## B.5 Workflow 4 — Voice (LiveKit) + đa STT/TTS

| Layer | Metric | Baseline | Target | Data source | Owner | Red-team risk | Fix |
|-------|--------|----------:|--------:|-------------|-------|----------------|-----|
| Activation | **% voice session hoàn thành** (không drop <10s) | 55% | ≥75% | LiveKit session events | Voice Lead | Drop do mic permission | UX hướng dẫn + fallback text |
| Engagement | **Voice share of sessions** | 8% | 20% | channel=`voice` | Product Owner | Ép dùng voice | Mặc định text; voice optional |
| Productivity | **E2E latency p50** (end utterance→first TTS audio) | 2.0s | ≤1.0s (mục tiêu sản phẩm) | pipeline traces | Voice Lead | Đo không chuẩn | V2: **server-side segment** marker |
| Quality | **WER proxy** — % transcript có sửa tay owner | 18% | ≤10% | QA tool | QA Lead | SME không sửa | Incentivize 10 audit/tuần |
| Trust | **Handoff to text khi confidence thấp** | — | ≥95% compliance | policy logs | Risk Owner | Khách không biết | UI “đang chuyển text…” |
| Value | **Voice sessions tạo lead** | 5% | ≥12% | joins | Sales Owner | Lead kém do ASR | FPT/Vbee theo locale |

---

# Part C — Dashboard Mock (6 ô)

```text
┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 1: PRODUCT HEALTH             │ │ TILE 2: RAG + KB WORKFLOW          │
│ Metric: Qualified leads / week     │ │ Metric: Citation rate when KB hit  │
│ Current: 3   Target: 8            │ │ Current: 72%  Target: 85%         │
│ Status: AMBER                      │ │ Status: AMBER                      │
│ Action if red: Run playbook + fix │ │ Action if red: Freeze deploy;     │
│   schema; sales validate 10 leads  │ │   increase min retrieval score    │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 3: WIDGET TEXT                │ │ TILE 4: TRUST / QUALITY          │
│ Metric: p95 first token latency    │ │ Metric: Human QA weekly pass %   │
│ Current: 2.1s Target: 1.5s        │ │ Current: 78%  Target: 90%         │
│ Status: RED                        │ │ Status: AMBER                    │
│ Action if red: Scale worker; cut │ │ Action if red: Add QA headcount  │
│   context; cache embed warm        │ │   sample; review worst sessions  │
└────────────────────────────────────┘ └────────────────────────────────────┘

┌────────────────────────────────────┐ ┌────────────────────────────────────┐
│ TILE 5: VALUE (SALES)              │ │ TILE 6: DECISION                   │
│ Metric: Lead → opp rate            │ │ Continue with guardrails         │
│ Current: 9%   Target: 15%        │ │ Strongest metric: qualified leads  │
│ Status: GREEN                    │ │ Before scale: QA voice VI; Zalo   │
│ Action if red: Tighten ICP; fix  │ │   test account policy; cost cap   │
│   pricing copy in KB             │ │ Owner: Product + Risk — 14 days   │
└────────────────────────────────────┘ └────────────────────────────────────┘
```

---

# Part D — Decision Memo

```markdown
# Memo Quyết Định Cuối — OpenCalf

1. Nhóm khuyến nghị: **continue (có guardrail)** — tiếp tục MVP OSS với trọng tâm lead+RAG+widget; **pivot** phần voice nếu p95 latency và WER VN không đạt sau 6 tuần đo.

2. Chỉ số mạnh nhất để bảo vệ quyết định là:
   **Qualified leads / tuần / agent** (hiện pilot 3, mục tiêu 8+) vì đây là **retention hook** và bằng chứng gần tiền nhất với SME (sales có việc để làm), tránh bẫy “nhiều chat nhưng vô nghĩa” — bài học từ public metrics Klarna [K1] và diễn biến hậu kỳ [K3].

3. Chỉ số / giả định đã sửa sau phản biện:
   **V1:** Dùng **conversation count** + **widget loads** làm engagement chính — dễ tạo cảm giác tăng trưởng nhưng **CFO/User** phản biện không chứng minh value.
   **V2:** Đổi sang **sessions có ≥1 user message**, **qualified lead rate**, **CSV export/week**, và **human QA pass** — vì V2 neo vào **kết quả công việc** và **chất lượng**, không neo vào hoạt động.

4. Trước khi scale, nhóm phải:
   1. **Chạy QA 50 hội thoại song song** (text+Zalo) với rubric citation — QA Lead — hết 14 ngày sau pilot đầu.
   2. **Policy Zalo Personal** (account test, rate limit, nội dung nhạy cảm) + runbook khoá kênh — Risk Owner — 7 ngày.
   3. **Cost guardrail** API (LLM/STT/TTS) theo workspace + alert 80% budget — Finance BP + Backend — trước mở rộng 50 agent.
```

---

# Red-team (tóm tắt) & v1 → v2

## Nhóm bị phản biện — rủi ro chính

| Vai | Rủi ro | Metric / giả định | Sửa v2 |
|-----|--------|-------------------|--------|
| **CFO** | “Conversation” không bảo chứng tiền | conv count | **Qualified lead** + export CRM |
| **User** | Owner bị spam lead rỗng | auto extract mọi lúc | Extract **khi session kết thúc** + min turns |
| **Risk** | Zalo personal → compliance / khoá acc | bridge uptime | Disclaimer + account test + kill switch |
| **Workflow Owner** | Latency chỉ đo p50 | first token | Thêm **p95** + error budget dashboard |

## Ít nhất 2 thay đổi cụ thể v1 → v2

| # | V1 | V2 | Vì sao tốt hơn |
|---|----|----|----------------|
| 1 | Engagement = **widget loads + conv count** | Engagement = **meaningful sessions** + **CSV exports** | Giảm vanity metric; gần hành vi sales thật |
| 2 | Quality = **citation rate một mình** | Quality = **citation + weekly human QA pass** | Giảm rủi ro citation đúng chunk nhưng sai nghiệp vụ |

---

## Checklist rubric (tự chấm)

- [x] 1 product cụ thể + 4 workflow.  
- [x] ADKAR barrier chính + 3 tactic khớp barrier.  
- [x] Metric product + per workflow; có Quality/Trust/Value.  
- [x] Baseline, target, data source, owner.  
- [x] Red-team risk + Fix; ≥2 thay đổi v1→v2.  
- [x] Decision: continue + điều kiện pivot voice.  

---
*Bài làm cá nhân — Hoàng Hiệp — dựa trên brief OpenCalf [O1], đề lab [D1], và tham chiếu độc lập trong [`REFERENCES.md`](REFERENCES.md).*

---

## Tham chiếu (mã tắt)

| Mã | Ý nghĩa |
|----|---------|
| [O1] | Brief / báo cáo thiết kế OpenCalf (học viên) — không có URL sản phẩm độc lập |
| [K1] [K2] [K3] | Case Klarna — OpenAI + PR + báo hậu kỳ |
| [Z1] | MAU Zalo — báo chí VN |
| [AD1] | ADKAR — Prosci |
| [L1] | LiveKit — GitHub |
| [A1] | AgentGPT — GitHub |
| [I3] | Intervo — tài liệu setup (độ phức tạp OSS so sánh) |

*Liệt kê URL đầy đủ:* [`REFERENCES.md`](REFERENCES.md).
