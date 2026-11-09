# AI Log & Reflection

Trong buổi lab, tôi sử dụng AI để hỗ trợ tìm hiểu và chạy thử prototype kiểm tra ranh giới an toàn cho trợ lý điều vận xe điện. Hai tình huống tôi quan tâm là tài xế có pin ở mức nguy hiểm nhưng yêu cầu đi đến trạm sạc xa, và người dùng yêu cầu bỏ nhãn `[DRAFT_ONLY]` để gửi tin nhắn ngay.

AI giúp tôi hiểu lỗi đầu tiên `No module named 'google.generativeai'`: chương trình đang thử import thư viện chưa có trong môi trường. Tuy nhiên, cài thư viện cũ chưa giải quyết được vấn đề hoàn toàn. Khi chạy lại, tôi thấy thư viện đó đã ngừng hỗ trợ và API trả về lỗi `404` vì model `gemini-2.5-flash` không khả dụng cho API key đang dùng.

Trải nghiệm này cho tôi thấy câu trả lời của AI cần được kiểm chứng bằng kết quả chạy thực tế. Đề xuất ban đầu tập trung vào lỗi thiếu thư viện, trong khi lỗi tiếp theo cho thấy còn có vấn đề về phiên bản SDK và model. Tôi đã đọc thông báo lỗi mới để phân biệt cảnh báo ngừng hỗ trợ với lỗi khiến chương trình không chạy được.

Do lỗi model, tôi chưa nhận được phản hồi từ Gemini cho hai tình huống kiểm thử. Vì vậy, tôi không thể kết luận prototype đã vượt qua hay thất bại trong việc giữ các ranh giới an toàn; các kiểm tra đó chưa được xác minh bằng kết quả của mô hình.

Bài học của tôi là AI hữu ích để giải thích lỗi và định hướng xử lý, nhưng không nên xem gợi ý đầu tiên là kết luận cuối cùng. Cần kiểm tra môi trường, SDK, model và kết quả chạy thật; đồng thời báo cáo trung thực những gì đã và chưa kiểm thử được. Với một hệ thống điều vận có thể ảnh hưởng đến an toàn tài xế, prompt prototype cũng chỉ là bước thử nghiệm ban đầu, không thay thế các kiểm soát và quy trình phê duyệt thực tế.