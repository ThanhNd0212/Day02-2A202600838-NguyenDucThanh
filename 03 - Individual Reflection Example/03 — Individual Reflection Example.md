## Đóng góp của Tôi trong nhóm

| Hoạt động | Minh đã làm gì? | Kết quả |
|---|---|---|
| Scan cá nhân | Đưa ra 7 problems | Nhóm có nhiều candidate về reporting/workflow |
| Pitch | Pitch 3 top problems | Giúp cho các thành viên có thể đối chiếu và tìm ra problem tối ưu nhất |
| Challenge | Hỏi nhóm các tool dùng để triển khai và cùng nhóm tìm ra các tool phù hợp, tối ưu problem | Nhóm đã tìm ra tool phù hợp để phục vụ cho các giải pháp được đưa ra |
| Research | Gợi ý cho nhóm dùng phương pháp LLM để tổng hợp các lỗi cần sửa trong work flow đưa đến bộ phận operation | Nhóm thấy phươg pháp phù hợp và đã dùng kết hợp cùng RAG |
| Rule / Workflow / Agent | Lập luận chọn Workflow, không chọn Agent | Nhóm thống nhất decision |

## Bảng dùng AI trong reflection

| Phase | Tôi dùng AI để làm gì? | AI hữu ích ở đâu? | AI sai/hời hợt ở đâu? | Tôi sửa gì |
|---|---|---|---|---|
| Scan | Sử dụng AI mở rộng các lăng kính,người đau của 1 vấn đề trong các lĩnh vực khác  | Giúp quyết định xem các problem nào cần thiết, đối chiếu lăng kính đúng | Còn nhiều lăng kính không chính xác | chọn lọc các lăng kính đúng |
| Workflow | Nhờ AI chuyển mô tả thành Mermaid | Nhanh hơn khi vẽ flow | AI chưa hiểu rõ workflow đúng | kiểm tra và sửa lại workflow cuối cùng |
| Research | Tìm tool tương tự | Gợi ý OpenAI-40-mini,Elastic Stack (ELK - Elasticsearch, Logstash, Kibana) hoặc Grafana Loki | Gợi ý một số tool lan man, không phù hợp để áp dụng vào dự án | Chỉ giữ tool phù hợp|
| Problem validation | Nhờ AI giả lập validation | Gợi ý nhiều phương án giả lập | một vài phương án lan man, quá phức tạp đối chiếu với yêu cầu | Thảo luận cùng nhóm và lấy 1 phương án giả lập hữu ích nhất |

## Bài học của Tôi

- Problem cần có khả năng giải quyết vấn đề thực tế, workflow rõ ràng
- Workflow giúp hiểu rõ quy trình xử lý của vấn đề, từ đó tìm ra các bước cần và có thể cải thiện. 
- Không nhiết thiết phải áp dụng Agent vào bài toán, trong problem của nhóm, sử dụng mức độ AI đủ tốt có thể tiết kiệm được công sức và nâng cao tiến độ công việc
- Quick Validation đóng vai trò quan trọng trong giai đoạn bắt đầu dự án. Tham khảo ý kiến của người khác để có thể có cái nhìn tổng quan hơn về vấn đề, hiểu rõ những vấn đề cấp bách

Nếu làm lại:

```text
- Tôi kêu gọi các thành viên trong nhóm trao đổi tích cực và hiểu sâu hơn các workflow của họ. 
- Chuyển format sang Agent levek cải thiện khả năng tự động tìm lỗi sai và sửa lỗi sai trong problem group  
```