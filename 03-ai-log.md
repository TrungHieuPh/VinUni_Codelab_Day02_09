# AI Log — Nhật ký sử dụng AI (Lab 02)

**Đề tài:** Vinhomes — Hỗ trợ phân loại và điều phối phản ánh cư dân đa kênh  
**Phạm vi nhật ký:** Nghiên cứu Phase 1 (SCAN), Phase 2 (QUICK-ASSESS) và định hướng bước tiếp theo.  
**Công cụ đã dùng trong các tương tác được ghi lại:** ChatGPT.  
**Trạng thái:** Bản nháp dựa trên cuộc trao đổi thực tế, cần tôi tự đối chiếu, bổ sung trải nghiệm và ký nhận trước khi nộp. **Chưa ghi nhận việc chạy Gemini/Claude hoặc kiểm thử prototype.**

> **Nguyên tắc trung thực:** Tôi phân biệt (1) thông tin có nguồn công khai, (2) giả thuyết về quy trình nội bộ và (3) mục tiêu do nhóm đề xuất. Nội dung do ChatGPT hỗ trợ soạn không tự động trở thành kết quả nghiên cứu hoặc kinh nghiệm cá nhân của tôi.

## 1. Mục đích dùng AI và phần việc do tôi quyết định

Trong Lab 02, tôi dùng ChatGPT làm *thought partner* (trợ lý hỗ trợ suy nghĩ), chủ yếu để hiểu yêu cầu bài tập, tìm hướng nghiên cứu, so sánh cơ hội ứng dụng AI và chuẩn hóa bài làm thành Markdown. AI giúp tôi tiết kiệm công sức ở phần hệ thống hóa thông tin, nhưng tôi không nên giao cho nó quyền quyết định hoàn toàn bài toán nào có giá trị hay kết luận nào là sự thật.

Điều tôi đã chủ động thực hiện trong cuộc trao đổi là yêu cầu giải thích các Phase trước khi làm, lựa chọn hướng Vinhomes, cung cấp ý tưởng và mục tiêu nhóm đề xuất, yêu cầu thu thập nguồn, rồi nhiều lần chỉnh lại phạm vi tài liệu để đúng yêu cầu nộp bài. Tôi cũng yêu cầu thay danh sách năm bài toán cùng thuộc Vinhomes bằng **năm bài toán ở năm công ty khác nhau**, và giữ Vinhomes là một trong ba Quick Problem Cards của Phase 2.

**Tôi vẫn phải tự làm:** đọc ít nhất các nguồn chính, xác minh nhận định, xem lại các chỉ số, tự đánh giá các ưu/nhược điểm của phương án và chạy thử chương trình khi đến Phase 4.

## 2. Nhật ký tương tác với ChatGPT

| Lượt | Mục đích tôi yêu cầu | AI hỗ trợ được gì? | Điều tôi điều chỉnh / cần kiểm tra |
|---|---|---|---|
| **01 — Hiểu đề** | Giải thích Phase 0–3 cho người mới bắt đầu. | Làm rõ *pain point*, *bottleneck*, *workflow*, *metric*, *AI fit*, *human-in-the-loop* và *fallback*. | Đối chiếu từng phần với `01-worksheet.md`, vì giải thích dễ hiểu không thay thế đề gốc. |
| **02 — Tìm vấn đề** | Tìm hiểu website và phản ánh cư dân để làm Phase 1. | Gợi ý các bài toán Vinhomes và cách xem một phản ánh như **dấu hiệu cần khảo sát**, không phải kết luận đại diện cho mọi dự án. | Yêu cầu bổ sung nguồn, mô tả ngắn gọn và không biến giả thuyết thành sự thật. |
| **03 — Sửa phạm vi nộp bài** | Làm file Markdown theo yêu cầu giảng viên. | Soạn bảng SCAN và các Quick Cards. | Tôi làm rõ `01-problem-scan.md` phải gồm **cả Phase 1 và Phase 2**, không kèm các Phase khác. |
| **04 — Sửa danh sách doanh nghiệp** | Mỗi công ty Vin có một bài toán; Vinhomes giữ bài phân loại phản ánh. | Viết lại bảng cho Vinhomes, VinFast, Xanh SM, Vinmec và VinWonders/Vinpearl. | Tôi chốt phạm vi Vinhomes và yêu cầu Quick Card #1 phải bám đúng ý tưởng nhóm. |
| **05 — Định nghĩa AI và chỉ tiêu** | Làm rõ giải pháp phân loại phản ánh và mục tiêu đo lường. | Đề xuất LLM để gắn chủ đề, mức khẩn cấp, cờ ưu tiên và bộ phận gợi ý; nhân viên duyệt trước khi chuyển. | Tôi phải kiểm tra rằng các mốc **< 5 phút**, **≥ 90%** và **không bỏ sót ca khẩn trong bộ kiểm thử** là **mục tiêu**, chưa phải kết quả đã đạt. |

**Nhận xét:** AI làm tốt việc tạo cấu trúc và nêu nhiều phương án. Tuy nhiên, nếu tôi không mô tả rõ yêu cầu đầu ra, AI có thể tạo tài liệu quá dài, sai số Phase hoặc đề xuất phạm vi khác ý định của nhóm.

## 3. Lỗi và nguy cơ hallucination đã nhận diện

### 3.1. Nhầm thời hạn theo quy định với thời gian xử lý thực tế

Một điểm dễ dẫn đến kết luận sai là diễn giải mốc **4 giờ** cho điện thoại và **24 giờ** cho email như thể nhân viên mất từng ấy thời gian để đọc và phân loại một phản ánh. Đây là **thời hạn chuyển/tiếp nhận theo quy định công bố của đơn vị ban hành**, không phải số đo thời gian thao tác trung bình của toàn bộ ban quản lý Vinhomes.

**Cách khắc phục trong bài:** Viết rõ đây là mốc quy định thuộc phạm vi văn bản; muốn khẳng định AI giúp giảm thời gian từ bao nhiêu xuống bao nhiêu thì phải có **baseline** đo thực tế. Chỉ tiêu dưới 5 phút được dùng như **mục tiêu thử nghiệm cần xác nhận**, không so sánh trực tiếp với SLA 4/24 giờ.

### 3.2. Suy diễn từ tính năng/khiếu nại công khai sang quy trình nội bộ

Từ việc ứng dụng có kênh gửi phản ánh và có người dùng phàn nàn về xử lý yêu cầu, AI có thể suy ra rằng **mọi ticket đều đang được đọc thủ công, mọi kênh đều dồn vào một hệ thống và việc chuyển sai diễn ra thường xuyên**. Những khẳng định này chưa có chứng cứ từ dữ liệu vận hành của doanh nghiệp.

**Cách khắc phục:** Đổi cách viết từ khẳng định tuyệt đối sang **“bottleneck giả thuyết cần xác minh”**. Chỉ kết luận có quy trình/kênh phản ánh nếu nguồn thực sự hỗ trợ; chưa kết luận nguyên nhân hay tần suất lỗi.

### 3.3. Nguy cơ tự tạo số liệu đẹp nhưng không có phép đo

Các con số như “90% chính xác”, “< 5 phút”, “0 ca khẩn bị bỏ sót” dễ khiến báo cáo trông thuyết phục, nhưng **không chứng minh năng lực mô hình khi chưa chạy thử**. Ngay cả “0 ca khẩn bị bỏ sót trong bộ test” cũng không đồng nghĩa đảm bảo **không bao giờ** bỏ sót trong vận hành thật.

**Cách khắc phục:** Gắn nhãn *mục tiêu pilot*; cần bộ dữ liệu đã gán nhãn, chia nhóm ca bình thường/khẩn cấp, ghi rõ số mẫu, số dự đoán đúng/sai và thống kê riêng **recall đối với ca khẩn**. Không viết “AI đạt 90%” khi chưa kiểm thử.

> **Tự kiểm chứng bắt buộc:** Tôi sẽ mở lại nguồn gốc, kiểm tra phạm vi áp dụng và ghi ít nhất một phát biểu đã chỉnh sửa bằng chính lời của mình ở Mục 6.

## 4. Tôi đã làm rõ prompt và ranh giới AI như thế nào?

Ban đầu yêu cầu của tôi khá rộng (“tìm hiểu các vấn đề đáng làm”). Sau đó tôi bổ sung điều kiện rõ ràng: **đúng định dạng worksheet**, **mỗi doanh nghiệp một bài toán**, **Phase 2 có Vinhomes**, **bảng SCAN ngắn gọn**, còn Quick Cards phải đầy đủ Actor/Workflow/Bottleneck/AI/Metric.

Với đề tài Vinhomes, phạm vi giải pháp được thu hẹp thành:

1. AI đọc nội dung phản ánh và **đề xuất** `topic`, `urgency`, `priority_flag` và bộ phận phụ trách.
2. Nhân viên CSKH **kiểm tra, sửa và xác nhận** trước khi điều phối.
3. AI **không tự gửi câu trả lời cho cư dân**, không tự đóng phiếu, không cam kết đền bù.
4. Trường hợp nguy hiểm hoặc thiếu chắc chắn phải **chuyển người phụ trách**, không để AI quyết định một mình.

Những giới hạn này là **thiết kế đã nêu trong bài**, chưa phải bằng chứng hệ thống đã thực thi thành công. Chỉ viết câu “AI không được làm X” trong prompt chưa đủ: khi lập trình cần thêm rule kiểm tra đầu ra, phân quyền và cơ chế fallback.

**Mẫu prompt tôi có thể tự sử dụng để kiểm tra bài (chưa khẳng định đã gửi nguyên văn):**

```text
Hãy đóng vai người phản biện báo cáo AI Product.
Kiểm tra từng nhận định tôi đưa ra và đánh dấu:
(A) Có nguồn xác minh; (B) Giả thuyết cần đo; (C) Mục tiêu thử nghiệm.
Đặc biệt kiểm tra: có nhầm SLA với thời gian thao tác không,
có suy diễn quy trình nội bộ từ đánh giá người dùng không,
và có bước nào chỉ cần rule-based mà không cần LLM không.
Chỉ chỉ ra vấn đề và gợi ý cách tự kiểm chứng; đừng viết lại hộ toàn bộ.
```

## 5. Những gì tôi chưa làm — không được ghi thành kết quả

- [ ] Chưa có biên bản phỏng vấn nhân viên CSKH/BQL hoặc dữ liệu ticket nội bộ để xác minh quy trình thủ công.
- [ ] Chưa đo **baseline** (thời gian phân loại, tỷ lệ chuyển sai bộ phận) tại Vinhomes.
- [ ] Chưa kiểm thử Gemini/Claude để đo độ chính xác 90% hay thời gian dưới 5 phút.
- [ ] Chưa chạy adversarial test của Phase 4 và lưu input/output thực tế.

**Khi thực hiện Phase 4, tôi sẽ tự bổ sung log kiểm thử thật:**

| Ngày | Prompt/tình huống tự viết | Kết quả thực tế (đã che thông tin nhạy cảm) | Đúng/sai? | Tôi sửa gì? |
|---|---|---|---|---|
| [Điền ngày] | [Tình huống khẩn cấp] | [Chưa chạy] | [—] | [—] |
| [Điền ngày] | [Yêu cầu bỏ qua phê duyệt] | [Chưa chạy] | [—] | [—] |
| [Điền ngày] | [Thiếu thông tin hoặc câu mơ hồ] | [Chưa chạy] | [—] | [—] |

*Lưu ý:* Phase 4 trong starter code của Lab 02 có bài kiểm thử Gemini theo tình huống Xanh SM. Nếu nhóm sử dụng đúng starter đó, cần ghi kết quả thực tế của bài Xanh SM, không mô tả nhầm là đã kiểm thử prototype Vinhomes.

## 6. Phần tôi phải tự bổ sung để nhật ký thực sự là của mình

> **Các ô dưới đây là phần tự làm, không nhờ AI viết thay.** Tôi hoàn thiện bằng chính trải nghiệm khi đọc nguồn và thực hành rồi mới nộp.

**(1) Nguồn tôi đã tự mở và kiểm tra:**  
- URL: [Tôi điền]  
- Nguồn thực sự xác nhận điều gì? [Tự viết 2–3 câu]  
- Điều gì tôi đã từng nghĩ đúng nhưng nguồn KHÔNG xác nhận? [Tự viết 1–2 câu]

**(2) Một phương án tôi tự phản biện với AI:**  
- Tôi thử giải quyết bằng rule-based như thế nào? [Tự viết]  
- Tại sao tôi vẫn chọn/không chọn LLM? [Tự viết]

**(3) Một điều tôi hiểu khác đi sau khi học:**  
[Tự viết 4–6 câu, ví dụ sự khác nhau giữa metric mục tiêu và kết quả thử nghiệm; không chép lại định nghĩa của AI.]

**(4) Nếu đã làm Phase 4:**  
- Lệnh chạy: [Tôi điền]  
- Một output khiến tôi bất ngờ hoặc phát hiện lỗi: [Tôi điền]  
- Tôi đã sửa prompt/code/test như thế nào: [Tôi điền]

## 7. Reflection — Bài học rút ra

Qua quá trình sử dụng ChatGPT, tôi nhận ra AI hữu ích nhất ở khâu **gợi mở hướng làm và tổ chức thông tin**. Nếu chấp nhận ngay câu trả lời đầu tiên, tôi có thể nộp nhầm phạm vi Phase, chọn một giải pháp AI không cần thiết hoặc đưa các mốc thời gian/metric vào báo cáo sai bản chất. Vì vậy, tôi đã yêu cầu sửa tài liệu nhiều lần để khớp yêu cầu thật của nhóm và của worksheet.

Tôi cũng hiểu hơn sự khác nhau giữa **AI hỗ trợ quyết định** và **AI tự ra quyết định**. Với phản ánh cư dân, mô hình có thể giúp đọc ngôn ngữ tự nhiên nhanh hơn, nhưng người phụ trách phải giữ quyền duyệt, đặc biệt khi liên quan an toàn. Việc một phương án nghe hợp lý chưa đủ để kết luận nên triển khai: cần dữ liệu được phép dùng, chỉ số nền, kết quả thử nghiệm và so sánh với giải pháp không dùng AI.

**Kết luận cá nhân (tôi cần đọc và sửa lại theo trải nghiệm thật):** Tôi muốn dùng AI để đặt câu hỏi tốt hơn, nhận phản biện và phát hiện chỗ thiếu trong suy nghĩ của mình, thay vì chỉ yêu cầu AI viết sẵn đáp án. Những quyết định, bằng chứng và kết quả thực nghiệm cuối cùng phải do tôi kiểm tra và chịu trách nhiệm.

## 8. Nguồn và tài liệu để đối chiếu

- `01-worksheet.md` — yêu cầu Phase 1, Phase 2 và Phase 6 của Lab 02.
- `01-problem-scan.md` — bảng SCAN và ba Quick Problem Cards của nhóm.
- [Vinhomes Market — Quy định xử lý khiếu nại/yêu cầu](https://market.vinhomes.vn/quy-dinh-xu-li-khieu-nai-yeu-cau-cua-khach-hang) — cần đọc đúng phạm vi áp dụng và định nghĩa các mốc thời gian.
- [Vinhomes Resident — Google Play](https://play.google.com/store/apps/details?id=com.vinhomes.resident&hl=vi) — kênh và phản ánh của người dùng; không đại diện cho toàn bộ hệ thống.

**Ghi chú về AI:** ChatGPT hỗ trợ soạn bản nháp nhật ký này từ lịch sử trao đổi. Trước khi nộp, tôi sẽ kiểm tra lại các nội dung ở ngôi thứ nhất, thay phần trong dấu `[ ]` bằng trải nghiệm thật và không nhận là đã thực hiện các bước chưa làm.
