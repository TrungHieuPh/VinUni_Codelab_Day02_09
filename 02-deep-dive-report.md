# 02 — Deep-Dive Report: Vinhomes — AI phân loại & điều hướng phản ánh cư dân

**Nhóm:** <!-- Tên nhóm / danh sách thành viên --> · **Mảng kinh doanh:** 🏢 Vinhomes — Quản lý vận hành khu đô thị & chăm sóc cư dân

> **Quy ước số liệu:** ✅ = số liệu có nguồn công khai (xem *Nguồn số liệu* cuối file) · 🧮 = ước tính giả định của nhóm để scoping (Vinhomes không công bố số liệu vận hành nội bộ) — cần đo lại trong giai đoạn chuẩn bị.

---

## 🗳️ Quyết định lựa chọn của nhóm

Nhóm chọn bài toán **"Phân loại & điều hướng phản ánh cư dân"** để Deep-Dive. Bài toán xuất hiện độc lập trong Phase 1 của nhiều thành viên (Card #1 trong `01-problem-scan.md`; dòng #3 "Chăm sóc cư dân" trong bảng SCAN của Khoa).

**Lý do chọn:**
* Quy trình và SLA được quy định **bằng văn bản chính thức** của Vinhomes ✅ [2] → Workflow Mapping và metric bám sát thực tế, không phải đoán.
* Quy mô lớn: ✅ 30 khu đô thị, >110.000 căn, ~493.000 cư dân [1].
* Đầu vào là **văn bản/lời nói tự do** → phù hợp năng lực của LLM, trong khi các bài khác (đặt sân, bãi xe, đối soát) phần lớn giải được bằng Rule.
* Có **ranh giới an toàn tự nhiên**: ca khẩn liên quan an toàn tính mạng và khách hàng dễ bị tổn thương ✅ [2].

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

## 3.1. Current-State Workflow Mapping

Quy trình xử lý một phản ánh của cư dân theo *Quy định xử lý khiếu nại/yêu cầu của khách hàng* ✅ [2] (sơ đồ đầy đủ: [`04-workflow-diagram.png`](04-workflow-diagram.png)):

```text
┌───────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│ Bước 1        │     │ Bước 2        │     │ Bước 3        │     │ Bước 4        │
│ Tiếp nhận     │     │ Ghi nhận &    │     │ Phân loại sự  │ 🔄  │ Chuyển tiếp   │
│ phản ánh      │ ──→ │ tạo ticket    │ ──→ │ vụ, mức độ &  │ ──→ │ đến BPXL      │
│ (4 kênh)      │     │ (nhập tay)    │     │ chọn bộ phận  │     │ + báo KH      │
│ Ai: CSKH/Lễ tân│    │ Ai: CSKH      │     │ Ai: CSKH      │     │ Ai: CSKH      │
│ ⏱ 3 phút      │     │ ⏱ 3 phút 🔴   │     │ ⏱ 3 phút 🔴   │     │ ⏱ 2 phút 🔴chờ│
│ In: cuộc gọi, │     │ In: nội dung  │     │ In: ticket    │     │ SLA ✅ ≤ 04h  │
│ email, giấy,  │     │ thô           │     │ Out: loại +   │     │ (tổng đài) /  │
│ trực tiếp     │     │ Out: ticket   │     │ bộ phận       │     │ ≤ 24h (email) │
└───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘
                                                                         │ 🔄
                                                                         ▼
┌───────────────┐     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│ Bước 8        │     │ Bước 7        │     │ Bước 6        │     │ Bước 5        │
│ Khảo sát sau  │     │ Phản hồi kết  │ 🔄  │ Đôn đốc BPXL  │     │ BPXL xử lý    │
│ hỗ trợ        │ ←── │ quả cho KH    │ ←── │ ✅ ≥ 05 ngày/ │ ←── │ ✅ 04 ngày    │
│ ✅ gọi ≥ 3    │     │ ✅ ≤ 01 ngày  │     │ lần           │     │ (đơn giản) /  │
│ lần / 02 ngày │     │ làm việc      │     │ Ai: CSKH      │     │ 06 ngày (phức │
│ Ai: CSKH      │     │ Ai: CSKH      │     │ ⏱ 2 phút/lần  │     │ tạp)          │
│ ⏱ 4 phút      │     │ ⏱ 3 phút      │     │               │     │ Sai bộ phận → │
│               │     │               │     │               │     │ 🔴 trả về B3  │
└───────────────┘     └───────────────┘     └───────────────┘     └───────────────┘

🔴 = Bottleneck   🔄 = Handoff (chuyển giao giữa bộ phận / người ↔ hệ thống)
⏱ Tổng thao tác thủ công của CSKH (🧮): 3 + 3 + 3 + 2 + 2 + 3 + 4 = 20 phút/lượt
   (chưa tính thời gian BPXL xử lý và thời gian ticket nằm chờ trong hàng đợi).
```

**Phân tích bottleneck:**
* 🔴 **Bước 2–3 (🧮 ~6 phút/lượt):** CSKH phải đọc/nghe nội dung tự do, nhập lại thông tin (tòa, căn, mô tả), hỏi thêm khi thiếu, rồi **tự phán đoán** loại sự vụ, mức độ (đơn giản / phức tạp / khẩn ✅ [2]) và bộ phận phụ trách.
* 🔴 **Thời gian chờ trước khi đến đúng người:** quy định cho phép tới ✅ **04 giờ làm việc** (tổng đài) và ✅ **24 giờ** (email) mới chuyển tiếp [2] — trong giờ cao điểm ticket nằm hàng đợi lâu.
* 🔴 **Vòng lặp chuyển sai:** nếu Bước 3 chọn sai bộ phận, BPXL trả về và ticket quay lại Bước 3 → mất thêm một vòng SLA.
* 🔄 **Handoff chính:** CSKH → BPXL (Bước 4), BPXL → CSKH (Bước 7). Mỗi lần chuyển giao là một điểm có thể thất lạc thông tin.

---

## 3.2. Problem Statement (6-field) & Metrics

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | **Nhân viên CSKH tổng đài** và **lễ tân/CSKH Ban Quản lý** tại các khu đô thị Vinhomes — đầu mối tiếp nhận (BPTN) theo quy định ✅ [2]. Người chịu ảnh hưởng: cư dân gửi phản ánh và các bộ phận xử lý (kỹ thuật, an ninh, vệ sinh, thủ tục, kế toán phí). |
| **2. Current Workflow** | Phản ánh đến từ ✅ 4 kênh (Tổng đài 1900 2323 89, email info@vinhomes.vn, bản cứng, trực tiếp tại BQL) [2]. CSKH ghi nhận vào hệ thống ticket, tự phân loại sự vụ và mức độ, chuyển cho bộ phận xử lý, đôn đốc ✅ tối thiểu 05 ngày/lần, phản hồi kết quả và gọi khảo sát ✅ tối thiểu 03 lần/02 ngày [2]. 8 bước, thao tác thủ công 🧮 ~20 phút/lượt. |
| **3. Bottleneck** | **Bước 2–3: đọc nội dung tự do → nhập lại → phân loại & chọn bộ phận** (🧮 ~6 phút/lượt). Đây là bước cần **hiểu ngôn ngữ tự nhiên** (cư dân mô tả "nước rỉ trần nhà tắm", "thang máy kêu lạ", "hàng xóm khoan đục giờ nghỉ trưa"…), dễ phân loại sai mức độ và chọn sai bộ phận → ticket bị trả về, trễ SLA. |
| **4. Business Impact** | ✅ >110.000 căn / ~493.000 cư dân tại 30 khu đô thị [1]. 🧮 Ước tính toàn hệ thống: 0,5 yêu cầu/căn/tháng ≈ 55.000 yêu cầu/tháng × 6 phút (Bước 2–3) ≈ **5.500 giờ công/tháng (~34 FTE)**. 🧮 Ở quy mô một phân khu (ước tính của thành viên nhóm): ~600 yêu cầu/tháng × 5 phút ≈ **50 giờ công/tháng**. Rủi ro phi tài chính: trễ SLA 04/06 ngày ✅; bỏ sót **khách hàng dễ bị tổn thương** → ✅ Vinhomes phải bồi thường thiệt hại theo quy định [2]. |
| **5. Success Metric** | **Efficiency:** thời gian từ tiếp nhận → chuyển đến đúng bộ phận giảm từ ✅ tối đa 04h/24h xuống 🧮 **median < 15 phút, P95 < 1 giờ làm việc**; thao tác CSKH Bước 2–3 từ 🧮 ~6 phút → **≤ 2 phút/lượt**.<br>**Quality:** 🧮 **≥ 90%** ticket định tuyến đúng bộ phận ngay lần đầu; giảm **≥ 50%** số ticket bị trả về do chuyển sai (so với baseline).<br>**Safety:** 🧮 **recall ≥ 98%** với ca khẩn (an toàn tính mạng); **100%** ca khẩn được chuyển cho người xử lý trong **≤ 5 phút**. |
| **6. Operational Boundary** | **AI ĐƯỢC PHÉP:** đọc nội dung phản ánh; trích xuất trường (tòa, căn, loại sự vụ, mức độ); gợi ý bộ phận xử lý kèm độ tin cậy; gắn **cờ gợi ý** khẩn / dễ bị tổn thương / trùng lặp; soạn **nháp** tin xác nhận cho cư dân (gắn `[DRAFT_ONLY]`).<br>**AI TUYỆT ĐỐI KHÔNG ĐƯỢC:** tự gửi phản hồi cho cư dân; tự đóng hoặc xóa ticket; **hạ mức** một ticket đã bị Rule gắn KHẨN; đưa ra cam kết bồi thường, miễn phí hay thời hạn sửa chữa; trả lời nội dung tranh chấp/pháp lý (phải chuyển Pháp chế ✅ [2]); lưu nhãn "dễ bị tổn thương" vào hồ sơ cư dân khi chưa có xác nhận.<br>**ĐIỂM BẮT BUỘC CÓ NGƯỜI DUYỆT (HITL):** CSKH xác nhận mọi quyết định định tuyến (giai đoạn pilot); CSKH duyệt mọi tin gửi cư dân; ca khẩn bỏ qua AI, chuyển thẳng người xử lý; phương án xử lý vẫn do CBLĐ phê duyệt theo Cẩm nang phân quyền ✅ [2]. |

---

## 3.3. Future-State Flow & AI Fit

### AI-Fit Matrix — so sánh 3 phương án

| Tiêu chí | Rule / State-Machine | LLM Feature | Agentic Loop |
|---|---|---|---|
| Hiểu mô tả tự do của cư dân ("nước rỉ trần", "thang máy kêu lạ") | ❌ Từ khóa dễ sót/nhầm khi cư dân diễn đạt khác | ✅ Hiểu ngữ cảnh, trích xuất được trường thông tin | ✅ |
| Bắt ca khẩn (cháy, rò điện, kẹt thang máy) — cần **chắc chắn, giải thích được** | ✅ Tất định, kiểm tra được | ⚠️ Xác suất, có thể bỏ sót | ⚠️ |
| Đếm SLA, nhắc đôn đốc 05 ngày/lần | ✅ Timer đơn giản | ❌ Thừa | ❌ Thừa |
| Soạn nháp tin xác nhận cho cư dân | ⚠️ Mẫu cứng, rập khuôn | ✅ | ✅ |
| Rủi ro & khả năng kiểm soát | Thấp | Trung bình (kiểm soát bằng HITL + validator) | **Cao** — tự hành động qua nhiều bước, khó kiểm toán |
| Phù hợp quy trình cần CBLĐ phê duyệt theo phân quyền ✅ [2] | ✅ | ✅ (chỉ gợi ý) | ❌ Mâu thuẫn với cơ chế phê duyệt |

**➡️ Lựa chọn: Hybrid — Rule + LLM Feature** (không dùng Agent).
* **Rule** cho phần cần tất định: cổng lọc ca khẩn theo từ khóa an toàn, đếm SLA, nhắc đôn đốc.
* **LLM Feature** cho phần cần hiểu ngôn ngữ: trích xuất, phân loại, gợi ý bộ phận, soạn nháp.
* **Không dùng Agentic Loop** vì quy trình đã cố định 8 bước, mọi phương án xử lý phải qua CBLĐ phê duyệt, và để AI tự hành động (gửi tin, đóng ticket) vi phạm Operational Boundary.

### Future-State Flow

```text
┌───────────────┐   ┌────────────────────┐        ┌──────────────────────┐
│ Bước 1        │   │ Bước 2             │  KHẨN  │ 🟢 CHUYỂN NGAY       │
│ Tiếp nhận     │──→│ RULE GATE          │──────→ │ Người xử lý + gọi    │
│ (email / app  │   │ Từ khóa an toàn:   │        │ điện cho cư dân      │
│ / tổng đài)   │   │ cháy, rò điện, kẹt │        │ (bỏ qua LLM)         │
└───────────────┘   │ thang máy, ngã…    │        │ ⏱ ≤ 5 phút           │
                    └────────────────────┘        └──────────────────────┘
                              │ không khẩn
                              ▼
┌────────────────────┐   ┌────────────────────┐   ┌────────────────────┐
│ Bước 3             │   │ Bước 4             │   │ Bước 5             │
│ 🔵 LLM trích xuất  │──→│ 🟢 CSKH DUYỆT      │──→│ Chuyển BPXL tự động│
│ & phân loại → JSON │   │ 1-click / sửa nhãn │   │ + 🔵 nháp xác nhận │
│ {tòa, căn, loại,   │   │ ⏱ ~1–2 phút        │   │ [DRAFT_ONLY] →     │
│  bộ phận, mức độ,  │   │                    │   │ 🟢 CSKH bấm gửi    │
│  confidence, cờ}   │   │                    │   │                    │
└────────────────────┘   └────────────────────┘   └────────────────────┘
          │                                                 │
          │ confidence < 0.8 / JSON lỗi / API lỗi           ▼
          ▼                                       ┌────────────────────┐
┌────────────────────┐                            │ Bước 6             │
│ ↩️ FALLBACK         │                            │ RULE: đếm SLA 04/06│
│ Đưa vào hàng chờ   │                            │ ngày, tự nhắc đôn  │
│ thủ công như hiện  │                            │ đốc 05 ngày/lần    │
│ tại (CSKH tự phân  │                            │ → phản hồi & khảo  │
│ loại); cư dân vẫn  │                            │ sát (như cũ)       │
│ nhận xác nhận mẫu  │                            └────────────────────┘
└────────────────────┘

🔵 = AI Step (LLM)   🟢 = Human Step (HITL)   ↩️ = Fallback
⏱ Thao tác CSKH Bước 2–3 dự kiến (🧮): ~6 phút → ~1–2 phút/lượt.
```

**Output có cấu trúc của LLM (Bước 3):**

```json
{
  "toa": "S2.05",
  "can_ho": "1203",
  "loai_su_vu": "ky_thuat_cap_thoat_nuoc",
  "bo_phan_de_xuat": "ky_thuat",
  "muc_do": "phuc_tap",
  "han_xu_ly_ngay_lam_viec": 6,
  "confidence": 0.86,
  "co_dau_hieu_de_ton_thuong": false,
  "nghi_trung_voi_ticket": null,
  "can_hoi_them": ["Thời điểm bắt đầu rò rỉ?"]
}
```

**Ranh giới được kiểm soát bằng code, không chỉ bằng prompt** (rút kinh nghiệm từ Phase 4): validator kiểm tra JSON đúng schema; mọi tin gửi cư dân phải mang `[DRAFT_ONLY]` cho tới khi CSKH duyệt; nếu Rule đã gắn KHẨN thì hệ thống bỏ qua mọi đề xuất hạ mức của LLM.

---

# 💻 Liên hệ với Phase 4 — Prompt Prototype

Mỗi thành viên đã xây dựng `starter-code/prompt_prototype.py` trên branch cá nhân (bài mẫu điều phối sạc pin Xanh SM). Kết quả rút ra áp dụng cho bài toán Vinhomes:
* Ranh giới `[DRAFT_ONLY]` và chống lệnh giả danh "admin/SYSTEM OVERRIDE" giữ vững ở cả 3 test tấn công.
* Model vẫn **tự suy diễn** ở chi tiết nhỏ (tự điền `battery_percent: 100` khi người dùng chỉ nói "sạc đầy rồi") → trong bài Vinhomes, các trường như `toa`, `can_ho` **chỉ được điền khi có trong nội dung**, và cần validator + HITL.

---

# 🏁 Phase 5 — EVALUATE (Nhóm)

### AI Readiness Checklist

| # | Câu hỏi | Đánh giá | Bằng chứng |
|---|---|---|---|
| 1 | Có sẵn dữ liệu mẫu/logs sạch để test? | ☐ **Chưa** | Lịch sử ticket có tồn tại trên các kênh ✅ [2], nhưng **chưa có nhãn chuẩn** "bộ phận đúng / mức độ đúng" để đo độ chính xác, và **chưa có baseline** đo thời gian chuyển tiếp, tỷ lệ chuyển sai. Toàn bộ số liệu giờ công hiện là 🧮 ước tính. |
| 2 | Rủi ro khi AI sai có nằm trong tầm kiểm soát? | ☑ **Có** | AI chỉ gợi ý, CSKH duyệt mọi định tuyến (HITL); ca khẩn đi qua Rule, không phụ thuộc LLM; Fallback về quy trình thủ công hiện tại; phương án xử lý vẫn do CBLĐ phê duyệt ✅ [2]. |
| 3 | Stakeholders sẵn sàng thay đổi quy trình cũ? | ☐ **Chưa xác nhận** | Cần BQL một phân khu đồng ý pilot và CSKH thay đổi thao tác (duyệt gợi ý thay vì tự nhập). Chưa có buổi làm việc với người vận hành thực tế. |

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

☐ **GO** (Bắt đầu xây dựng Prototype)
☑ **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline)** — chuẩn bị 3–4 tuần, sau đó chuyển sang **GO với scope hẹp**
☐ **NO-GO**

**Justification:**
> Bài toán **có giá trị thật**: quy trình và SLA được Vinhomes quy định bằng văn bản ✅, quy mô lớn (✅ >110.000 căn), đầu vào là ngôn ngữ tự nhiên phù hợp với LLM, và rủi ro đã được khoanh vùng bằng Rule cho ca khẩn + HITL + Fallback. Tuy nhiên nhóm **chưa thể chứng minh** AI đạt các metric đặt ra vì: (1) chưa có tập ticket lịch sử đã gán nhãn để đo độ chính xác định tuyến; (2) chưa có baseline thật — các con số 5.500 giờ công/tháng hay 6 phút/lượt đều là ước tính; (3) chưa biết một bộ **Rule từ khóa đơn giản** đã định tuyến đúng được bao nhiêu phần trăm — nếu Rule đã đạt gần 90% thì LLM không đáng chi phí tích hợp.
>
> **Điều kiện để chuyển sang GO (pilot 1 phân khu, kênh email + app):**
> 1. Gán nhãn ~500 ticket lịch sử của một phân khu (bộ phận đúng, mức độ đúng, có phải ca khẩn).
> 2. Đo baseline 1 tháng: thời gian tiếp nhận → chuyển đúng bộ phận, tỷ lệ ticket bị trả về.
> 3. Chạy offline so sánh **Rule-only vs Rule + LLM** trên tập 500 ticket: LLM chỉ được triển khai nếu đạt **≥ 90%** định tuyến đúng, **recall ≥ 98%** ca khẩn và **vượt Rule-only rõ rệt**.
> 4. BQL phân khu pilot và đội CSKH đồng ý quy trình duyệt mới; chi phí API (theo báo giá thực tế) thấp hơn giờ công tiết kiệm được.

---

## 📚 Nguồn số liệu

1. Cafeland (16/04/2025), trích Báo cáo thường niên 2024 của Vinhomes — *"Gần nửa triệu người đã chọn sống tại các dự án của tỷ phú Phạm Nhật Vượng"*: https://cafeland.vn/tin-tuc/gan-nua-trieu-nguoi-da-chon-song-tai-cac-du-an-cua-ty-phu-pham-nhat-vuong-137107.html
2. Công ty CP Vinhomes — *Quy định xử lý khiếu nại/yêu cầu của khách hàng* (cập nhật 05/05/2025): https://market-files.vinhomes.vn/public-mngt/d/279c2b19-3e4d-406a-950b-be78102f50fa
