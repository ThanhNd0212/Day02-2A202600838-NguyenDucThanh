# 01 — Individual Problem Scan
Nhân vật: Chính bản thân, Tôi khởi nghiệp và tạo một page bán hàng trên mạng xã hội.Mỗi tuần phải soạn ra 7 mô tả sản phẩm mới để đăng bài. Mỗi ngày phải trả lời từ 20-25 người, tư vấn sản phẩm, giải đáp thắc mắc về sản phẩm, chốt thông tin khách hàng từ tin nhắn để rồi nhập vào phần mềm giao hàng, danh sách khách hàng, đơn hàng đã mua. 
## Scan rộng


| # | Lăng kính | Problem quan sát được | Ai đang đau? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Lặp lại | Thu thập, viết mô tả sản phẩm LEGO mới theo format giống nhau | Admin page, content team | 10-20 phút/ sản phẩm |
| 2 | Lặp lại | Trả lời inbox các câu hỏi lặp lại như “còn hàng không”, “bao nhiêu mảnh”, “phù hợp độ tuổi nào” | Admin | Lặp lại với mỗi khách hàng mới |
| 3 | AI có thể làm tốt hơn | khách hàng muốn được tư vấn nhưng còn mơ hồ về nhu cầu của bản thân-> Khó recommend sản phẩm phù hợp | Khách hàng, Admin | Hỏi lại 2-3 lần/sp |
| 4 | Tốn thời gian | Đăng cùng 1 sản phẩm lên nhiều nền tảng khác nhau theo nhiều format khách nhau | Admin, content team | 10-15 phút/sản phẩm |
| 5 | Tốn thời gian | Cập nhật số sản phẩm còn hàng cho từng khách hàng mỗi lần hỏi | Admin | Lặp lại công việc cập nhật tình trạng kho, báo lại cho từng khách hàng |
| 6 | AI có thể tốt hơn | Khách không rõ sự ưu, nhược cùng mỗi hãng trong cùng dòng sản phẩm | Admin, khách hàng | Giải thích nhiều lần |
| 7 | Tốn thời gian  | Khách hàng ưu cầu cập nhật tình trạng đang giao của đơn hàng | Admin | Truy lại tình trạng đơn của từng khách hàng trên app giao, cập nhật lại cho khách  |

## Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 |Khách muốn được tư vấn nhưng mô tả nhu cầu còn mơ hồ → khó recommend sản phẩm phù hợp | Pain lớn, ảnh hưởng trực tiếp đến khả năng chốt đơn, AI semantic search + recommendation có thể giải quyết tốt | Recommendation có đủ chính xác và cá nhân hóa hay không |
| 2 |Trả lời các câu hỏi lặp lại như “còn hàng không”, “bao nhiêu mảnh”, “phù hợp độ tuổi nào”|	Công việc lặp lại mỗi ngày, tốn nhiều thời gian admin, dễ tự động hóa bằng RAG chatbot | Chất lượng dữ liệu sản phẩm phải luôn được cập nhật |
| 3 |Khó search sản phẩm khi khách mô tả bằng ngôn ngữ tự nhiên	| Keyword search truyền thống hoạt động kém với mô tả tự nhiên, semantic search tạo khác biệt rõ | Cần hybrid search để tránh recommend sai sản phẩm |

## Problem Card #1 — tóm tắt

**Problem 1 câu:**  
Khách hàng muốn được tư vấn LEGO phù hợp nhưng thường mô tả nhu cầu mơ hồ, khiến admin phải hỏi lại nhiều lần trước khi recommend được sản phẩm phù hợp.
**Actor:**  
Admin page bán LEGO chịu trách nhiệm tư vấn và recommend sản phẩm cho khách hàng.

**Thời điểm / bối cảnh:**  
Xảy ra hàng ngày trong inbox Instagram, Facebook, Shopee hoặc chat website khi khách tìm mua LEGO cho bản thân hoặc làm quà tặng.

**Current workflow:**

```text
1. Khách nhắn mô tả nhu cầu chung chung 
2. Admin hỏi thêm độ tuổi, sở thích, ngân sách 
3. Khách trả lời bổ sung 
4. Admin tìm sản phẩm phù hợp trong kho 
5. Admin gửi hình ảnh + thông tin sản phẩm 
6. Khách tiếp tục so sánh hoặc hỏi thêm 
7. Admin mới recommend được sản phẩm cuối cùng
```

**Bottleneck:**  
Bước 2–4 — admin phải hỏi lại nhiều lần để hiểu đúng nhu cầu khách và tự search thủ công sản phẩm phù hợp.

**Impact:**  
Mỗi cuộc tư vấn có thể mất 10–20 phút. Khi lượng inbox tăng, admin phản hồi chậm, khách dễ bỏ cuộc hoặc không chốt đơn.

**Success metric:**  
- Giảm thời gian tư vấn xuống dưới 5 phút/chat
- Giảm số lần hỏi lại khách
- Tăng tỷ lệ chốt đơn từ inbox

**Non-AI alternative:**  
Tag sản phẩm theo độ tuổi / chủ đề và dùng template tư vấn có thể hỗ trợ phần nào, nhưng vẫn khó xử lý các nhu cầu mô tả tự nhiên và mơ hồ.

**AI hypothesis:**  
AI sử dụng semantic search + recommendation để hiểu nhu cầu tự nhiên của khách và gợi ý sản phẩm phù hợp ngay từ những tin nhắn đầu tiên. Admin chỉ cần review trước khi gửi.

**Quick gut:**  
Workflow.

### Draft current workflow

```text
CURRENT STATE — 15 phút

[1 Khách mô tả nhu cầu: 1']
→ [2 Admin hỏi thêm thông tin: 4']
→ [3 Khách trả lời bổ sung: 3']
→ [4 Admin search sản phẩm thủ công: 4']
→ [5 Admin recommend sản phẩm: 2']
→ [6 Khách hỏi thêm: 1']
```

### Draft future workflow

```text
FUTURE STATE — 4 phút 
[1 gửi sẵn tệp câu hỏi cần thiết để khách hàng trả lời]
[2 Khách mô tả nhu cầu: 1'] 
→ [3 AI semantic search + recommendation: 10s] 
→ [4 AI draft câu trả lời + sản phẩm phù hợp: 20s] 
→ [5 Admin review + gửi: 2'] 
→ [6 Khách follow-up nếu cần: 30s] 
Fallback: recommendation chưa đúng → admin can thiệp thủ công.

```

## Problem Cards #2 và #3 — tóm tắt

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn làm #1 |
|---|---|---|---|---|---|
| Trả lời FAQ sản phẩm | Admin page bán LEGO | Trả lời lặp lại các câu hỏi như “còn hàng không”, “bao nhiêu mảnh”, “độ tuổi phù hợp” | Thời gian phản hồi trung bình từ 10 phút → dưới 2 phút | Workflow / RAG chatbot | Chủ yếu là retrieval + automation, AI depth chưa cao |
| Semantic Product Search | Khách hàng, admin | Search keyword truyền thống hoạt động kém với mô tả tự nhiên | Thời gian tìm đúng sản phẩm từ vài phút → dưới 30 giây | Semantic search | Thực chất là một phần con của recommendation workflow |
---
