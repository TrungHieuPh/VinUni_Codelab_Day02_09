# 01-problem-scan.md — Lab 02: AI Product Scoping (Vinhomes)

## Phase 1 — SCAN (Cá nhân, 20 phút)

> **Nghiên cứu thứ cấp thực hiện ngày 09/11/2026.**  
> **Phạm vi:** Mảng quản lý vận hành khu đô thị và ứng dụng **Vinhomes Resident**.  
> **Phương pháp:** Đối chiếu quy trình công bố của Vinhomes với phản ánh công khai của người dùng ứng dụng; suy luận các bottleneck *có thể* xuất hiện; đề xuất bước xác minh.  
> **Giới hạn:** Chưa phỏng vấn cư dân/ban quản lý và chưa tiếp cận ticket, log, dữ liệu nội bộ. Không coi phản ánh cá nhân là bằng chứng một lỗi đang xảy ra trên diện rộng.

## 1.1. Bốn Lenses tìm bài toán AI

1. **Repetitive (Lặp lại):** Tác vụ có nội dung tương tự phải thực hiện nhiều lần.
2. **Time-consuming (Tốn thời gian):** Công việc cần đọc hiểu, kiểm tra, tra cứu hoặc chuyển qua nhiều người/bộ phận.
3. **AI-upgrade (Có thể cải thiện bằng AI):** Công việc cần hiểu ngôn ngữ tự nhiên hoặc dữ liệu đa dạng; cần so sánh với phương án dùng quy tắc thông thường.
4. **Stakeholder Pain (Khó khăn của bên liên quan):** Khách hàng, nhân viên hoặc bộ phận vận hành có thể gặp chậm trễ, thiếu thông tin hay khó sử dụng dịch vụ.

## 1.2. Danh sách 5 bài toán (mỗi doanh nghiệp 1 bài)

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|---|---|---|
| **1** | **Vinhomes** | **Repetitive / Time-consuming / Stakeholder Pain** | **Phân loại và điều phối phản ánh cư dân đa kênh:** Phản ánh qua hotline, email, thư, trực tiếp hoặc ứng dụng có nội dung khác nhau; bước xác định **chủ đề, mức độ khẩn cấp và cờ ưu tiên** rồi chuyển đúng bộ phận có thể gây chậm trễ hoặc chuyển nhầm. **[S1, S2, S3]** |
| **2** | **VinFast** | **Repetitive / Time-consuming** | **Sàng lọc yêu cầu bảo dưỡng, sửa chữa:** Khách hàng gửi mô tả lỗi xe, ảnh và yêu cầu đặt lịch; nhân viên dịch vụ cần xác định thông tin còn thiếu, loại nhu cầu và đúng nhóm chuyên trách, đặc biệt với dấu hiệu liên quan an toàn. **[S4]** |
| **3** | **Xanh SM (Green SM)** | **Stakeholder Pain / AI-upgrade** | **Xử lý phản ánh điểm đón không chính xác:** Khi ứng dụng không tìm được điểm đón hoặc vị trí định vị lệch, khách và tài xế phải xác minh lại địa điểm; phản ánh thiếu thông tin có thể gây khó cho việc truy vết, hỗ trợ và cải thiện dữ liệu địa điểm. **[S5]** |
| **4** | **Vinmec** | **Time-consuming / Stakeholder Pain** | **Tiếp nhận yêu cầu đặt và thay đổi lịch khám:** Người bệnh có thể mô tả nhu cầu tự do hoặc chưa rõ chuyên khoa, cơ sở và thời gian; đầu mối đặt lịch phải bổ sung thông tin, xác nhận lịch phù hợp và chuyển trường hợp cần đánh giá y tế cho nhân viên có chuyên môn. **[S6]** |
| **5** | **VinWonders / Vinpearl** | **Repetitive / AI-upgrade** | **Tra cứu chính sách vé và hỗ trợ thay đổi dịch vụ:** Khách hỏi về hiệu lực vé, điều kiện đổi/hủy, hóa đơn và dịch vụ đi kèm; nhân viên cần tra đúng quy định theo loại vé/sản phẩm để tránh tư vấn sai hoặc hứa xử lý ngoài chính sách. **[S7]** |

**Lưu ý:** Bảng trên mô tả *cơ hội cần khảo sát*, không khẳng định lỗi xảy ra phổ biến hoặc doanh nghiệp chưa có hệ thống tự động hóa.

## 1.3. Nhận xét nhanh sau SCAN

| Bài toán | Bằng chứng công khai | Điểm cần xác minh trước khi dùng AI |
|---|---|---|
| **P1 — Vinhomes** | Có quy trình tiếp nhận/chuyển xử lý, và ứng dụng cho phép gửi yêu cầu/phản ánh. | Thời gian phân loại thực tế, tỷ lệ phân loại sai, các bước đã tự động hóa. |
| **P2 — VinFast** | Có kênh đặt lịch, mô tả/ảnh xe, danh mục dịch vụ và bước xác nhận từ xưởng. | Các trường hợp nào chưa thể giải quyết bằng form/mã lỗi/quy tắc? |
| **P3 — Xanh SM** | FAQ chính thức có mục không tìm được điểm đón/đến và kênh hỗ trợ. | Nguyên nhân thực sự thuộc GPS, bản đồ, địa chỉ hay thao tác của người dùng? |
| **P4 — Vinmec** | Trang đặt lịch có trường chuyên khoa, thời gian, lý do khám và bước liên hệ xác nhận. | Có bao nhiêu yêu cầu thiếu dữ liệu; AI có thể hỗ trợ mà vẫn giữ an toàn y tế thế nào? |
| **P5 — VinWonders / Vinpearl** | Trang bán vé công bố chính sách sử dụng, đổi/hủy và hỗ trợ hóa đơn. | Tài liệu chính sách có cập nhật, truy xuất được không; liệu FAQ/rule đã đủ? |

**Chọn 3 bài toán để đánh giá ở Phase 2:** **P1 — Vinhomes; P2 — VinFast; P4 — Vinmec.** Cả ba có đầu vào ngôn ngữ tự nhiên, người dùng chịu ảnh hưởng trực tiếp, có thể xây thử nghiệm với yêu cầu giả lập và đặt ra ranh giới vận hành rõ ràng. **P1 — Vinhomes** là lựa chọn chính của nhóm.

## 1.4. Nguồn nghiên cứu Phase 1

- **[S1]** Vingroup, *Vingroup tăng 11 bậc trong bảng xếp hạng của Fortune…*, **17/06/2026**: công bố Vinhomes có **32 dự án đi vào vận hành, 650.000 cư dân**. <https://vingroup.net/tin-tuc-su-kien/bai-viet/6968/vingroup-tang-11-bac-trong-bang-xep-hang-cua-fortune-vao-top-30-doanh-nghiep-lon-nhat-dong-nam-a>
- **[S2]** Vinhomes Market, *Quy định xử lý khiếu nại/yêu cầu của khách hàng*, cập nhật **05/05/2025**: mô tả điện thoại, email, văn bản, trực tiếp; phân loại và chuyển bộ phận; thời hạn **04 giờ làm việc với điện thoại, 24 giờ làm việc với email hợp lệ**. **Văn bản áp dụng theo phạm vi của đơn vị ban hành được ghi trên trang, không mặc nhiên cho mọi BQL.** <https://market.vinhomes.vn/quy-dinh-xu-li-khieu-nai-yeu-cau-cua-khach-hang>
- **[S3]** Google Play, *Vinhomes Resident*: công bố tính năng gửi yêu cầu hỗ trợ và ý kiến tới Ban quản lý. <https://play.google.com/store/apps/details?id=com.vinhomes.resident&hl=vi>
- **[S4]** VinFast, *Đặt lịch dịch vụ bảo dưỡng*: biểu mẫu yêu cầu thông tin xe, loại dịch vụ, mô tả, ảnh, lịch/địa điểm và có bước xưởng dịch vụ xác nhận. <https://shop.vinfastauto.com/vn_vi/dat-lich-dich-vu-bao-duong.html> ; *Câu hỏi thường gặp về chính sách hậu mãi*: <https://vinfastauto.com/vn_vi/cau-hoi-thuong-gap/cau-hoi-xe-o-to/chinh-sach-hau-mai>
- **[S5]** Green SM, *Trung tâm giải đáp*: hướng dẫn chọn điểm đón, xử lý trường hợp **không tìm được điểm đón/đến**, và gửi yêu cầu qua Trung tâm hỗ trợ. <https://www.greensm.com/vn-vi/helps>
- **[S6]** Vinmec, *Đặt lịch khám*: người bệnh chọn cơ sở, chuyên khoa, giờ và điền lý do khám; lịch đề xuất cần được đầu mối liên hệ xác nhận. <https://www.vinmec.com/eng/booking/> ; biểu mẫu tiếng Việt: <https://online.vinmec.com/vn/dang-ky-kham>
- **[S7]** VinWonders, *Trang đặt vé chính thức*: điều kiện sử dụng vé, giới hạn đổi/hủy, quy định hóa đơn và kênh hỗ trợ. <https://booking.vinwonders.com/adminshop/>

---

# Phase 2 — QUICK-ASSESS (Cá nhân, 30 phút)

## 2.1. Top 3 bài toán tiềm năng

1. **Vinhomes — AI phân loại phản ánh cư dân:** có quy trình công bố, phạm vi đầu vào rõ và phù hợp để kiểm thử khả năng hiểu tiếng Việt tự nhiên.
2. **VinFast — AI hỗ trợ sàng lọc yêu cầu dịch vụ:** có quy trình đặt lịch và phân nhóm dịch vụ công khai; có thể đo chất lượng phân loại từ mô tả tự do.
3. **Vinmec — AI hỗ trợ tiếp nhận yêu cầu đặt/đổi lịch khám:** có biểu mẫu và bước xác nhận từ nhân viên; có thể hỗ trợ việc thu thập thông tin hành chính nếu kiểm soát an toàn y tế.

> **Quy tắc đọc số liệu:** Chỉ số **32 dự án và khoảng 650.000 cư dân** được Vingroup công bố [S1]. Mốc **4 giờ/24 giờ** là *thời hạn chuyển thông tin theo quy định* tại [S2], **không phải thời gian phân loại thực tế**. Các metric về phút và tỷ lệ bên dưới là **mục tiêu của thử nghiệm do nhóm đề xuất**, chưa phải kết quả đo. Quy trình thủ công là mô hình cần xác minh bằng phỏng vấn hoặc dữ liệu nội bộ.

## 2.2. QUICK PROBLEM CARD #1 — VINHOMES: Phân loại phản ánh cư dân đa kênh

| Trường trong worksheet | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Đọc và phân loại phản ánh đa kênh theo **chủ đề, mức độ khẩn cấp và cờ ưu tiên** để chuyển đúng bộ phận có thể tạo điểm nghẽn tại khâu tiếp nhận. |
| **Công ty thành viên** | **Vinhomes** |
| **Ai đang đau (Actor)?** | Nhân viên CSKH/tổng đài, Ban quản lý, bộ phận chuyên trách; cư dân chịu ảnh hưởng nếu phản ánh chậm hoặc chuyển sai nơi. |
| **Workflow thủ công hiện tại (3–5 bước; cần xác minh)** | **1.** Cư dân gửi nội dung qua hotline/email/thư/trực tiếp/app → **2.** Đầu mối tiếp nhận ghi nhận → **3.** Nhân viên đọc và xác định chủ đề, mức khẩn, cờ ưu tiên → **4.** Chọn/chuyển bộ phận phụ trách → **5.** Theo dõi và cập nhật kết quả. |
| **Bước tốn thời gian/lỗi nhất?** | **Bước 3–4:** hiểu nội dung tự do, xác định độ khẩn và chọn đúng đầu mối. **Chưa có số phút/lượt thực tế**. Theo [S2], quy trình đặt thời hạn chuyển thông tin **04 giờ làm việc với điện thoại** và **24 giờ làm việc với email hợp lệ** trong phạm vi văn bản; **không thể coi đây là thời gian nhân viên ngồi phân loại**. |
| **AI hỗ trợ ở bước nào?** | Sau bước 2, LLM đề xuất `topic` (chủ đề), `urgency` (mức khẩn cấp), `priority_flag` (cờ ưu tiên) và `suggested_team` (bộ phận đề xuất). Nhân viên **kiểm tra, sửa và xác nhận** trước khi chuyển. |
| **Success Metric (có số; mục tiêu thử nghiệm)** | **< 5 phút** từ lúc ghi nhận ticket đến lúc **nhân viên duyệt kết quả phân loại**; **≥90%** phân loại đúng so với nhãn chuẩn trên tối thiểu **100 phản ánh giả lập/ẩn danh**; **0 trường hợp khẩn cấp bị bỏ sót trong bộ kiểm thử** (đo riêng recall ca khẩn, không suy ra bảo đảm tuyệt đối ngoài thực tế). |
| **Quick Architecture** | `[ ] No AI` · `[ ] Rule` · `[x] LLM Feature + Safety Rules + Human-in-the-loop` · `[ ] Agent tự trị` |
| **Operational Boundary** | AI **chỉ phân loại và gợi ý**, **không tự trả lời cư dân**, không tự đóng phiếu hoặc cam kết giải quyết. Phản ánh **liên quan an toàn, thiếu dữ kiện, hoặc AI không chắc chắn** phải được **chuyển thẳng cho người phụ trách**, không chờ AI đưa ra quyết định. |
| **Nguồn** | [S1] quy mô, [S2] quy trình và thời hạn, [S3] kênh phản ánh trên ứng dụng. |

**Bối cảnh đã xác minh:** Theo Vingroup [S1], Vinhomes vận hành **32 dự án**, phục vụ khoảng **650.000 cư dân**. Nhóm xét **5 hình thức phản ánh**: hotline, email, thư/bản cứng, gặp trực tiếp và app Vinhomes Resident. [S2] xác nhận 4 hình thức truyền thống; [S3] xác nhận tính năng phản ánh trên app. **Chưa có bằng chứng công khai rằng cả 5 kênh đều đổ vào một hệ thống ticket dùng chung hoặc tất cả yêu cầu đều được đọc thủ công.**

**Ví dụ giả lập:** “Trần nhà đang rò nước xuống ổ điện, cần người đến ngay” → `topic: kỹ thuật/điện-nước`; `urgency: khẩn cấp`; `priority_flag: true`; **chuyển nhân viên trực lập tức**.

**AI Fit:** Chọn **LLM + quy tắc cứng + người duyệt** vì phản ánh thường là văn bản tự do; so sánh với form/rule-based trên cùng bộ test để chứng minh lợi ích của AI.

## 2.3. QUICK PROBLEM CARD #2 — VINFAST: Sàng lọc yêu cầu bảo dưỡng/sửa chữa

| Trường trong worksheet | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Những mô tả triệu chứng xe và yêu cầu dịch vụ tự do có thể cần được chuẩn hóa trước khi chuyển đúng nhóm bảo dưỡng hoặc sửa chữa. |
| **Công ty thành viên** | **VinFast** |
| **Ai đang đau (Actor)?** | Chủ xe, nhân viên tiếp nhận dịch vụ và cố vấn kỹ thuật tại xưởng. |
| **Workflow thủ công hiện tại (3–5 bước; cần xác minh)** | **1.** Khách gửi yêu cầu qua kênh hỗ trợ/đặt lịch → **2.** Tiếp nhận thông tin xe và mô tả → **3.** Hỏi bổ sung triệu chứng, ảnh/mã lỗi nếu cần → **4.** Phân nhóm yêu cầu, xác định đầu mối phù hợp → **5.** Xưởng xác nhận lịch/đề xuất bước tiếp theo. |
| **Bước tốn thời gian/lỗi nhất?** | **Bước 3–4:** mô tả không thống nhất hoặc thiếu thông tin; nguy cơ bỏ sót dấu hiệu cần kiểm tra an toàn. **Chưa đo phút/lượt thực tế**. |
| **AI hỗ trợ ở bước nào?** | LLM đọc ghi chú/mô tả để đề xuất `service_category`, `missing_information`, `safety_escalation`; gợi ý đúng đầu mối. Tra cứu quy trình/tài liệu đã phê duyệt; nhân viên xác nhận. |
| **Success Metric (có số; mục tiêu thử nghiệm)** | **≥90%** phân nhóm đúng trên ít nhất **100 yêu cầu kiểm thử**; thời gian phân nhóm và nhân viên duyệt **< 3 phút/yêu cầu**; **100% tình huống nguy hiểm được gắn cờ trong tập kiểm thử**. |
| **Quick Architecture** | `[ ] No AI` · `[ ] Rule` · `[x] LLM Feature + Knowledge Base + Rules + Human Review` · `[ ] Agent tự trị` |
| **Operational Boundary** | AI không chẩn đoán hư hỏng chính thức, không khẳng định xe an toàn để tiếp tục di chuyển, không tự cam kết lịch/chi phí khi chưa có xác nhận xưởng. |
| **Nguồn** | [S4] biểu mẫu dịch vụ, quy trình xác nhận lịch, tài liệu hậu mãi chính thức. |

**Ví dụ giả lập:** “Xe báo lỗi hệ thống phanh, tôi muốn đặt lịch kiểm tra.” → đề xuất nhóm **kiểm tra kỹ thuật/an toàn**, **chuyển nhân viên có chuyên môn**, không tư vấn tiếp tục chạy xe.

**AI Fit:** LLM có ích cho **ghi chú mở**; những yêu cầu đã được khách chọn rõ từ menu, mã lỗi và quy tắc đặt lịch vẫn có thể dùng **rule-based** rẻ và ổn định hơn.

## 2.4. QUICK PROBLEM CARD #3 — VINMEC: Tiếp nhận yêu cầu đặt/đổi lịch khám

| Trường trong worksheet | Nội dung |
|---|---|
| **Bài toán (1 câu)** | Yêu cầu đặt/đổi lịch khám diễn đạt tự do có thể thiếu chuyên khoa, cơ sở hoặc thời gian, khiến việc xác nhận lịch và chuyển đúng đầu mối mất thêm lượt trao đổi. |
| **Công ty thành viên** | **Vinmec** |
| **Ai đang đau (Actor)?** | Người bệnh, nhân viên tổng đài/đặt lịch và bộ phận hành chính khám bệnh. |
| **Workflow thủ công hiện tại (3–5 bước; cần xác minh)** | **1.** Người bệnh gửi yêu cầu → **2.** Bộ phận tiếp nhận kiểm tra thông tin → **3.** Hỏi bổ sung chuyên khoa/cơ sở/thời gian nếu thiếu → **4.** Đối chiếu lịch và chuyển đúng đầu mối → **5.** Nhân viên xác nhận lịch chính thức. |
| **Bước tốn thời gian/lỗi nhất?** | **Bước 2–4:** diễn giải yêu cầu mơ hồ, bổ sung các trường chưa có và phân biệt yêu cầu hành chính với tình huống cần đánh giá y tế. **Chưa có số đo thời gian thực tế**. |
| **AI hỗ trợ ở bước nào?** | LLM chỉ trích xuất **ý định hành chính, cơ sở/chuyên khoa/thời gian mong muốn và trường còn thiếu**, tạo bản nháp cho tổng đài; nhân viên có thẩm quyền tra lịch và xác nhận. Dấu hiệu cần cấp cứu được ưu tiên chuyển nhân viên y tế. |
| **Success Metric (có số; mục tiêu thử nghiệm)** | **≥90%** xác định đúng ý định đặt/đổi/hỏi lịch trong ít nhất **100 yêu cầu giả lập**; **≥95%** phát hiện đúng trường bắt buộc còn thiếu; **100% ca có dấu hiệu cảnh báo khẩn trong bộ test** được đánh dấu chuyển nhân viên ngay. |
| **Quick Architecture** | `[ ] No AI` · `[ ] Rule` · `[x] LLM Feature + Form/Rules + Human Review` · `[ ] Agent tự trị` |
| **Operational Boundary** | AI không chẩn đoán, kê đơn, quyết định người bệnh an toàn để chờ lịch thường hoặc tự xác nhận đã đặt/đổi lịch. Không đưa thông tin sức khỏe cá nhân thật vào dịch vụ thử nghiệm khi chưa có phép và biện pháp bảo vệ dữ liệu. |
| **Nguồn** | [S6] form đặt lịch và thông báo nhân viên liên hệ xác nhận lịch. |

**Ví dụ giả lập:** “Tôi muốn đổi lịch khám nội tổng quát từ sáng thứ Tư sang chiều thứ Sáu.” → `intent: đổi lịch`, đề xuất thông tin cần kiểm tra; lịch chính thức **phải được nhân viên/hệ thống đặt lịch xác nhận**.

**AI Fit:** Chỉ áp dụng AI cho **hiểu ngôn ngữ tự nhiên và kiểm tra đủ thông tin**, không làm thay quyết định chuyên môn y khoa hoặc hệ thống quản lý lịch khám.

## 2.5. So sánh 3 Quick Problem Cards và kết luận

| Tiêu chí | Vinhomes | VinFast | Vinmec |
|---|---|---|---|
| Có nguồn mô tả quy trình/kênh chính thức | **Có — quy trình tiếp nhận cụ thể** | Có — biểu mẫu/xưởng xác nhận | Có — form và xác nhận lịch |
| Đầu vào ngôn ngữ tự nhiên phù hợp thử LLM | **Rõ ràng** | Có, ở phần mô tả lỗi mở | Có, ở phần yêu cầu tự do |
| Làm demo bằng dữ liệu giả lập, không cần tích hợp hệ thống thật | **Khả thi** | Khả thi, cần rule an toàn xe | Khả thi, nhưng lưu ý an toàn y tế |
| Cần con người phê duyệt | **Có** | Có | Có |
| Ưu tiên triển khai prototype trong Lab 02 | **#1 — Chọn** | #2 — Dự phòng | #3 — Dự phòng |

**Kết luận Phase 2:** Chọn **Vinhomes — AI phân loại phản ánh cư dân đa kênh**. Phạm vi prototype: **nhận phản ánh → đề xuất 3 nhãn (`topic`, `urgency`, `priority_flag`) và bộ phận → nhân viên xác nhận**; không tự trả lời cư dân; ca khẩn/không chắc chắn phải chuyển người xử lý. **Mục tiêu pilot:** thời gian đến khi nhãn được duyệt **dưới 5 phút**, **độ chính xác ≥90%**, **không bỏ sót tình huống khẩn trong tập test**. Đây là **mục tiêu cần kiểm chứng**, không phải hiệu quả đã đạt.

**Việc nhóm cần kiểm chứng trước khi áp dụng thực tế:** thời gian thao tác *baseline*; hệ thống đã tự động hóa tới đâu; bảng nhãn chuẩn và phân công bộ phận; bộ dữ liệu ticket được phép sử dụng và đã ẩn danh; đo riêng hiệu suất phân loại và nhận diện ca khẩn. **Không so sánh trực tiếp SLA 4 giờ/24 giờ với thời gian thao tác phân loại như thể chúng là cùng một chỉ số.**
