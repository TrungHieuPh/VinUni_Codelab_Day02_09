# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

**Họ tên:** Ngô Chí Vĩnh — **Branch:** `NgoChiVinh-2A202603724` — **Mảng tập trung:** 🏢 Vinhomes

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày.
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên.
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn.
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn.

> **Quy ước số liệu:** ✅ = số liệu có nguồn công khai (xem *Nguồn số liệu* cuối file) · 🧮 = ước tính giả định của tôi để scoping (Vinhomes không công bố số liệu vận hành nội bộ).
>
> **Bối cảnh:** ✅ Đến 31/12/2024 Vinhomes vận hành **30 khu đô thị / 7 tỉnh thành**, **>110.000 căn**, **~493.000 cư dân**; bàn giao **~19.400 căn** trong năm 2024 [1].

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Vinhomes | Lặp lại | **Phân loại & định tuyến phản ánh cư dân** từ 4 kênh (tổng đài, email, bản cứng, trực tiếp) đến đúng bộ phận. ✅ SLA chuyển tiếp 04 giờ (tổng đài) / 24 giờ (email) [2]. 🧮 0,5 yêu cầu/căn/tháng × 110.000 căn ≈ 55.000 yêu cầu/tháng × 6 phút ≈ **5.500 giờ công/tháng (~34 FTE)**. |
| 2 | Vinhomes | Lặp lại | **Đôn đốc tiến độ & gọi khảo sát sau xử lý**: ✅ nhắc bộ phận xử lý 05 ngày/lần, gọi khảo sát tối thiểu 03 lần/02 ngày nếu khách không nghe máy [2]. 🧮 30% yêu cầu là kỹ thuật (~16.500/tháng) × tối đa 3 cuộc × 2 phút ≈ **~1.650 giờ/tháng**. |
| 3 | Vinhomes | Tốn thời gian | **Tổng hợp defect list khi bàn giao căn hộ** từ biên bản giấy, ảnh chụp, tin nhắn rồi phân loại, giao nhà thầu. ✅ ~19.400 căn bàn giao 2024 [1]. 🧮 10 lỗi/căn × 3 phút ≈ **~9.700 giờ công/năm**. |
| 4 | Vinhomes | Pain từ người khác | **Soạn thông báo vận hành** (cắt điện/nước, bảo trì thang máy…) cho từng tòa, từng kênh (App, Zalo, bảng tin); cư dân phàn nàn khi thông báo muộn/thiếu. ✅ 30 khu đô thị [1]. 🧮 8 thông báo/khu/tháng × 3 kênh × 15 phút ≈ **~180 giờ/tháng**. |
| 5 | Vinhomes | AI có thể tốt hơn | **Phân mức ưu tiên & nhận diện khách dễ bị tổn thương**: nhân viên tự phân ✅ đơn giản (04 ngày) / phức tạp (06 ngày) / khẩn (xử lý ngay) và phải ✅ ưu tiên khách dễ bị tổn thương, chậm trễ gây thiệt hại phải bồi thường [2]. Trợ lý ảo hiện tại ✅ chưa hỗ trợ tác vụ này [3]. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

**Top 3 được chọn:** #1 (Định tuyến phản ánh cư dân) · #3 (Defect list bàn giao) · #5 (Phân mức ưu tiên & khách dễ bị tổn thương).

### Card #1 — Vinhomes: AI phân loại & định tuyến phản ánh cư dân

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Phản ánh cư dân đến từ 4 kênh dưới dạng   │
│   văn bản/lời nói tự do; nhân viên phải đọc, ghi lại và tự  │
│   quyết định chuyển cho bộ phận nào (kỹ thuật, an ninh, vệ  │
│   sinh, thủ tục, phí dịch vụ…).                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? CSKH tổng đài & lễ tân Ban Quản lý     │
│   (quá tải giờ cao điểm); cư dân (chờ lâu, bị chuyển qua    │
│   lại nhiều bộ phận).                                       │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Nhận phản ánh (tổng đài/email/bản cứng/trực tiếp)      │
│   ──> 2. Đọc/nghe, ghi lại nội dung vào hệ thống ticket     │
│   ──> 3. Xác định loại sự vụ + bộ phận phụ trách            │
│   ──> 4. Chuyển tiếp & báo khách "đã tiếp nhận"             │
│   ──> 5. Đôn đốc bộ phận xử lý tối thiểu 05 ngày/lần        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ ~6 phút/lượt; │
│   SLA cho phép tới 04h/24h mới chuyển)                      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4: LLM đọc nội │
│   dung tự do → trích xuất tòa, căn, loại sự vụ → gợi ý bộ   │
│   phận + soạn nháp tin xác nhận; nhân viên bấm duyệt.       │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Thời gian tiếp nhận → chuyển đúng bộ phận: từ tối đa    │
│     04h (tổng đài)/24h (email) ──> dưới 15 phút.            │
│   - ≥ 90% ticket định tuyến đúng ngay lần đầu (đo trên 500  │
│     ticket lịch sử đã gán nhãn).                            │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> **Số liệu Card #1:** ✅ 4 kênh tiếp nhận, SLA 04h/24h, đôn đốc 05 ngày/lần [2] · 🧮 ~6 phút/lượt, mục tiêu 15 phút, 90%, tập 500 ticket.

### Card #3 — Vinhomes: AI tổng hợp defect list khi bàn giao căn hộ

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Lỗi phát hiện khi bàn giao căn hộ được    │
│   ghi tay trên biên bản + ảnh chụp rời rạc; nhân viên phải  │
│   nhập lại, phân loại hạng mục và giao cho đúng nhà thầu    │
│   sửa.                                                      │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên bàn giao & kỹ sư giám sát    │
│   (nhập liệu thủ công); cư dân mới nhận nhà (chờ sửa lỗi    │
│   mới vào ở được).                                          │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Cư dân + nhân viên kiểm tra căn, ghi lỗi tay & chụp    │
│      ảnh                                                    │
│   ──> 2. Nhân viên nhập lại từng lỗi vào Excel/hệ thống     │
│   ──> 3. Phân loại hạng mục (sơn, điện, nước, cửa…) + gán   │
│          thầu                                               │
│   ──> 4. Gửi nhà thầu, theo dõi tiến độ sửa                 │
│   ──> 5. Hẹn cư dân nghiệm thu lại                          │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ ~30 phút/căn  │
│   = 10 lỗi × 3 phút)                                        │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: LLM đa      │
│   phương thức đọc ảnh biên bản + ảnh lỗi → xuất defect list │
│   có cấu trúc (vị trí, hạng mục, mức độ) + gợi ý nhà thầu;  │
│   kỹ sư duyệt.                                              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Thời gian nhập & phân loại: ~30 phút/căn ──> dưới 5     │
│     phút/căn.                                               │
│   - ≥ 95% lỗi được gán đúng hạng mục (kỹ sư kiểm tra mẫu).  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> **Số liệu Card #3:** ✅ ~19.400 căn bàn giao năm 2024 [1] · 🧮 10 lỗi/căn, 3 phút/lỗi, mục tiêu 5 phút/căn, 95%.

### Card #5 — Vinhomes: AI phân mức ưu tiên & nhận diện khách dễ bị tổn thương

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #5                                       │
│                                                             │
│ Bài toán (1 câu): Nhân viên tự đánh giá mỗi yêu cầu là đơn  │
│   giản/phức tạp/khẩn và tự nhận ra khách thuộc nhóm dễ bị   │
│   tổn thương — đánh giá sai dẫn đến trễ hạn hoặc bỏ sót ca  │
│   nguy hiểm.                                                │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? CSKH/lễ tân Ban Quản lý (phải phán     │
│   đoán nhanh); cư dân cao tuổi, khuyết tật, phụ nữ mang     │
│   thai… (cần được ưu tiên).                                 │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhận yêu cầu từ cư dân                                 │
│   ──> 2. Tự phân mức: đơn giản (04 ngày) / phức tạp (06     │
│          ngày) / khẩn – an toàn tính mạng (xử lý ngay)      │
│   ──> 3. Tự nhận biết khách dễ bị tổn thương (thường chỉ    │
│          khi khách tự nói)                                  │
│   ──> 4. Đặt hạn xử lý & chuyển bộ phận                     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ ~2 phút/lượt) │
│   — ít tốn thời gian nhưng rủi ro cao: phân mức sai → trễ   │
│   SLA; bỏ sót khách dễ bị tổn thương → phải bồi thường      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: Rule bắt từ │
│   khóa an toàn (cháy, rò điện, kẹt thang máy, ngã…) → luôn  │
│   gắn KHẨN, chuyển người ngay; LLM phân mức đơn giản/phức   │
│   tạp + gắn cờ dấu hiệu khách dễ bị tổn thương để nhân viên │
│   xác nhận.                                                 │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Recall ≥ 98% với yêu cầu khẩn (gần như không bỏ sót).   │
│   - Giảm 50% số ticket trễ hạn 04/06 ngày so với baseline   │
│     (đo baseline 1 tháng trước).                            │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

> **Số liệu Card #5:** ✅ 3 mức thời hạn 04 ngày / 06 ngày / xử lý ngay, danh sách khách dễ bị tổn thương & nghĩa vụ bồi thường [2] · 🧮 ~2 phút/lượt, recall 98%, giảm 50%.
>
> ⚠️ **Ranh giới:** AI **không bao giờ được hạ mức** một yêu cầu đã bị Rule gắn KHẨN; "khách dễ bị tổn thương" là dữ liệu cá nhân nhạy cảm → AI chỉ **gắn cờ gợi ý**, nhân viên xác nhận.

> [!TIP]
> **Đề xuất mang vào buổi họp nhóm:** **Card #3 — Vinhomes: AI tổng hợp defect list khi bàn giao căn hộ.** Lý do: pain cụ thể mà mọi cư dân nhận nhà mới đều gặp, quy mô có nguồn (✅ ~19.400 căn bàn giao năm 2024 [1]), bottleneck rõ (nhập lại thủ công từ biên bản giấy + ảnh), metric đo được (🧮 ~30 → dưới 5 phút/căn, ≥ 95% đúng hạng mục) và ranh giới tự nhiên: AI chỉ soạn defect list nháp, **không được tự đóng/xóa/gộp lỗi**, lỗi liên quan an toàn (điện, ban công, kính) luôn được đánh dấu nghiêm trọng để kỹ sư xử lý; ảnh mờ/chữ khó đọc → Fallback cho nhân viên nhập tay.

---

## 📚 Nguồn số liệu

1. Cafeland (16/04/2025), trích Báo cáo thường niên 2024 của Vinhomes — *"Gần nửa triệu người đã chọn sống tại các dự án của tỷ phú Phạm Nhật Vượng"*: https://cafeland.vn/tin-tuc/gan-nua-trieu-nguoi-da-chon-song-tai-cac-du-an-cua-ty-phu-pham-nhat-vuong-137107.html
2. Công ty CP Vinhomes — *Quy định xử lý khiếu nại/yêu cầu của khách hàng* (cập nhật 05/05/2025): https://market-files.vinhomes.vn/public-mngt/d/279c2b19-3e4d-406a-950b-be78102f50fa
3. Báo SGGP (27/07/2022) — *"Ra mắt trợ lý ảo trên ứng dụng Vinhomes Resident và Vinhomes Online"*: https://www.sggp.org.vn/ra-mat-tro-ly-ao-tren-ung-dung-vinhomes-resident-va-vinhomes-online-post645421.html
