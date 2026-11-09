# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của **Vinhomes**. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: Phân loại phản ánh cư dân theo chủ đề).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Tra cứu thông tin trước khi phản hồi yêu cầu của cư dân).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Hỗ trợ cư dân tìm câu trả lời phù hợp từ tài liệu hướng dẫn đã duyệt).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến cư dân hoặc nhân viên vận hành phàn nàn. (Ví dụ: Cư dân phải liên hệ nhiều lần để hỏi tiến độ xử lý yêu cầu).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup), đang tìm kiếm pain point vận hành tại Vinhomes có thể cải thiện bằng AI. Hãy gợi ý 5 quy trình nghiệp vụ cụ thể, nêu rõ người thực hiện, điểm nghẽn và cách đo tác động. Nếu không có dữ liệu thực tế, hãy ghi rõ con số là giả định, không trình bày như số liệu đã được xác minh."*

### 📝 List bài toán của tôi:
| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| 1 | Vinhomes | Lặp lại | Nhân viên đọc và phân loại phản ánh của cư dân theo chủ đề |
| 2 | Vinhomes | Tốn thời gian | Soạn phản hồi ban đầu cho các đánh giá hoặc phản ánh phổ biến |
| 3 | Xanh SM | Stakeholder Pain | Tài xế báo điểm đón không chính xác, cần chuyển phản ánh đến đúng bộ phận |
| 4 | VinFast | Lặp lại | Nhân viên tổng hợp câu hỏi thường gặp về lịch bảo dưỡng |
| 5 | Vinmec | Tốn thời gian | Nhân viên hành chính phân loại yêu cầu đặt lịch khám |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): ____________________________________      |
|      Phân loại phản ánh và soạn nháp trả lời                │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? nhân viên CSKH                         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận phản ánh ──> 2. Đọc ──> 3. Phân loại ──> 4. Tìm   |
|    thông tin  ──> 5.  Soạn phản hồi ──> 6. Quản lý duyệt    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ____________________       |
|     Đọc và phân loại (⏱ ___ phút/lượt)                     |
│ AI có thể nhảy vào hỗ trợ ở bước nào? ____                  |
|     Tạo nhãn và bản nháp; nhân viên kiểm tra trước khi gửi  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? _____________________ │
│  "Giảm thời gian xử lý trung bình từ 10 min ──> under 5 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent |
|    LLM Feature + người duyệt                                │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                           │
│                                                                 │
│ Bài toán (1 câu): ___________________________________           |
|    Phân loại phản ánh về điểm đoán để chuyển đúng bộ phận       │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes      │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________      │
│                                                                 │
│ Ai đang đau (Actor)?_______________                             │
│    Nhân viên hỗ trợ vận hành                                    |  
|                                                                 │
│ Workflow thủ công hiện tại (3-5 bước):                          │
│   1. Nhận phản ánh ──> 2. Đọc ──> 3. Xác minh thông tin chuyến  |
|──> 4. Phân loại nguyên nhân  ──> 5. Chuyển bộ phận phụ trách    │
│                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? __________(⏱ ___ phút/lượt)   |
|  Đọc và xác định nhóm nguyên nhân; thời gian cần đo thực tế     │
│                                                                 |
| AI có thể nhảy vào hỗ trợ ở bước nào? ________________          |
|  Đề xuất loại vấn đề và bộ phận xử lý dựa trên nội dung phản ánh│
│                                                                 │
│ Đo thành công bằng gì (Metric có số)? ______________________    │
│  Giảm thời gian phân loại trung bình 30% mà không tăng tỉ lệ sai│
│                                                                 │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent     │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                           │
│                                                                 │
│ Bài toán (1 câu): ___________________________________           |
|    Phân loại câu hỏi bảo dưỡng                                  │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes      │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________      │
│                                                                 │
│ Ai đang đau (Actor)?_______________                             │
│    Nhân viên chăm sóc khách hàng và khách hàng cần thông tin    |
| bảo dưỡng                                                       |  
|                                                                 │
│ Workflow thủ công hiện tại (3-5 bước):                          │
│   1. Nhận câu hỏi ──> 2. Xác định dòng xe/ nội dung ──> 3. Tìm  |
| tài liệu hướng dẫn đã duyệt ──> 4. Soạn câu trả lời ──> 5. Nhân |
| viên kiểm tra và gửi                                            │
│                                                                 │
│ Bước nào tốn thời gian/lỗi nhất? __________(⏱ ___ phút/lượt)   |
|  Tìm đúng tài liệu và soạn câu trả lời phù hợp                  │
│                                                                 |
| AI có thể nhảy vào hỗ trợ ở bước nào? ________________          |
|  Phân loại câu hỏi và tạo bản nháp dựa trên tài liệu đã duyệt   │
│                                                                 │
│ Đo thành công bằng gì (Metric có số)? ______________________    │
│  Giảm thời gian soạn trả lời 30%, đồng thời nhân viên xác nhận  |
| câu trả lời có căn cứ                                           │
│                                                                 │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent     │
└─────────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---
