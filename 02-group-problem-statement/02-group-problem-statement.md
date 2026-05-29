## 1. Group convergence

Nhóm có 9 candidate problems từ 3 nhóm nguồn: vận hành dự án Locate Go, tư vấn/search sản phẩm, và workflow học tập.

| # | Nguồn | Candidate problem | Người gặp vấn đề | Điểm nghẽn | Cảm nhận nhanh |
|---:|---|---|---|---|---|
| 1 | Locate Go | Triage trạng thái đơn bị kẹt/lệch khi đồng bộ với hệ thống bên ngoài | Backend dev, ops/on-call, admin vận hành | Ghép database, action log, API log và error code để biết đơn kẹt ở bước nào | Workflow |
| 2 | Locate Go | Handover cho dev mới trong hệ thống vận hành phức tạp | Dev mới, người bàn giao, tech lead | Tìm đúng phần tài liệu và hiểu gotcha production | Workflow |
| 3 | Locate Go | Triage đơn không được phân phối tới tài xế | Backend dev, ops, support | Truy ngược queue, log, setting và DB flags | Workflow |
| 4 | Product recommendation | Khách mô tả nhu cầu mơ hồ nên khó recommend sản phẩm phù hợp | Khách hàng, shop/admin | Hiểu nhu cầu tự nhiên rồi map sang sản phẩm phù hợp | Workflow / Agent |
| 5 | Product FAQ | Trả lời câu hỏi lặp lại về sản phẩm | Shop/admin, khách hàng | Câu hỏi lặp lại như còn hàng, bao nhiêu mảnh, phù hợp độ tuổi nào | Rule / Workflow |
| 6 | Product search | Khó search sản phẩm bằng ngôn ngữ tự nhiên | Khách hàng | Keyword search không hiểu mô tả tự nhiên | Workflow |
| 7 | Learning workflow | Tổng hợp tài liệu LMS mỗi tối | Sinh viên trong lớp/lab | Đọc nhiều nguồn rời rạc rồi tổng hợp thành notes học được | Workflow |
| 8 | Learning workflow | Không theo kịp giảng trên lớp | Sinh viên | Bị hụt context trong giờ học, phải tự vá lại sau buổi học | Workflow |
| 9 | AI learning habit | Vibe code không hiểu bản chất | Sinh viên dùng AI để code | Code chạy nhưng không hiểu logic, khó debug/giải thích | Not Yet / Workflow |

## 2. Gom cluster

| Cluster | Candidates included | Pattern chung | Ghi chú |
|---|---|---|---|
| Triage / vận hành hệ thống | 1, 2, 3 | Truy ngược nhiều nguồn dữ liệu để hiểu incident hoặc trạng thái hệ thống | Pain thật, impact cao, nhóm hiểu domain từ dự án đã làm |
| Search / hỏi đáp / recommendation sản phẩm | 4, 5, 6 | Hiểu câu hỏi tự nhiên rồi tìm hoặc gợi ý thông tin phù hợp | Dễ hiểu, nhưng cần dữ liệu catalog và metric recommendation |
| Học tập / tổng hợp tài liệu | 7, 8, 9 | Sinh viên biến nhiều nguồn rời rạc thành hiểu biết và hành động học tập | Gần lớp học, dễ validate, nhưng impact vận hành và boundary rủi ro thấp hơn |

##3 Shortlist và score

| Candidate | Actor rõ | Workflow rõ | Pain có evidence | Impact đo được | Làm trong lab | So sánh R/W/A được | Nhóm hiểu domain | Tổng |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Triage trạng thái đơn bị kẹt khi báo cáo sang cơ quan quản lý| 5 | 5 | 4 | 5 | 4 | 5 | 5 | 33 |
| Triage đơn không được phân phối tới tài xế | 5 | 5 | 4 | 5 | 4 | 5 | 4 | 32 |
| Handover cho dev mới trong hệ thống vận hành phức tạp | 5 | 4 | 4 | 4 | 5 | 5 | 4 | 31 |
| Recommend LEGO theo nhu cầu mơ hồ | 5 | 4 | 4 | 4 | 5 | 5 | 4 | 31 |
| Trả lời FAQ sản phẩm | 5 | 5 | 5 | 4 | 5 | 4 | 4 | 32 |
| Semantic Product Search | 5 | 4 | 4 | 4 | 4 | 5 | 4 | 30 |
| Tổng hợp tài liệu LMS mỗi tối | 5 | 5 | 4 | 5 | 5 | 5 | 5 | 34 |
| Vibe code không hiểu bản chất | 5 | 3 | 4 | 3 | 5 | 3 | 5 | 28 |
| Không theo kịp giảng viên trên lớp | 5 | 4 | 4 | 4 | 5 | 4 | 5 | 21 |

Case nhóm chọn: **Triage trạng thái đơn bị kẹt/lệch khi đồng bộ với hệ thống bên ngoài**

Vì sao chọn:

- **Actor rõ:** backend dev, ops/on-call và admin vận hành đều có vai trò cụ thể trong incident.
- **Workflow rõ:** nhận mã đơn → kiểm database → kiểm action/log → đọc error code → quyết định retry/recovery/manual → phản hồi kết quả.
- **Bottleneck cụ thể:** dev phải ghép nhiều nguồn dữ liệu để hiểu trạng thái thật của một đơn trước khi dám thao tác.
- **Impact đo được:** có thể đo thời gian triage, số case có kết luận rõ, số lần retry/update sai và thời gian admin/support phải chờ.
- **Boundary rõ:** AI chỉ hỗ trợ đọc/tóm tắt/map checklist; thao tác live như retry/recovery/update DB vẫn do dev quyết định.
- **So sánh R/W/A tốt:** Rule đủ cho case đơn giản, Workflow hợp cho triage nhiều nguồn, Agent quá rủi ro vì có side effect production.

Vì sao chưa chọn các candidate còn lại:

- Dispatch tài xế cũng có workflow rõ, nhưng phụ thuộc nhiều vào queue/socket/dispatch setting nên scope kỹ thuật rộng hơn cho một bản Problem Statement đầu tiên.
- Handover dev mới phù hợp retrieval, nhưng metric "hiểu đúng" cần quiz hoặc onboarding task cụ thể mới đo chắc.
- Product recommendation/search cần catalog, lịch sử hỏi đáp và metric chất lượng recommendation.
- Product FAQ lặp lại rõ, nhưng dễ dừng ở rule/chatbot FAQ nếu không có bài toán phức tạp hơn.
- Các bài học tập gần bối cảnh lớp học, nhưng không có evidence production và rủi ro vận hành rõ bằng case trạng thái đơn.
- Vibe code là pain thật nhưng workflow và success metric còn mơ hồ nếu chưa thu hẹp vào một hành vi cụ thể.

## 4. Quick validation
| Nguồn | Số người / số mẫu | Tín hiệu xác nhận | Tín hiệu phản bác | Nhóm sửa problem thế nào |
|---|---:|---|---|---|
| **Đánh giá lại Vấn đề (Pain)** | 1 kịch bản incident mẫu + 3 nguồn dữ liệu | Để tìm ra một lỗi kẹt đơn cần phải gom đồng thời ít nhất 3 nguồn dữ liệu: trạng thái order, action log và raw API/error code. Việc này gây tốn thời gian triage thủ công. | Nếu hệ thống đã gom sẵn 3 nguồn này lên một dashboard tập trung thì áp lực triage và bottleneck của quy trình sẽ giảm đi rất nhiều mà chưa cần đến AI. | **Đưa pain về đúng bản chất:** Không thần thánh hóa AI giải quyết mọi thứ. Đầu tiên cần xây dựng một non-AI baseline (Dashboard hoặc script tự động gom snapshot dữ liệu từ 3 nguồn) để làm sạch và tập trung hóa dữ liệu trước khi đẩy qua cho AI xử lý. |
| **Đánh giá Giải pháp AI (Workflow/Agent)** | 2 flow vận hành (Recovery & Status Sync) | AI có khả năng đọc hiểu log không cấu trúc, tự động phân loại loại lỗi (triage) và ánh xạ mã lỗi một cách linh hoạt thay cho bảng mapping tĩnh. | Các bước thực thi trên production như dry run, live update, retry/recovery có side effect rất lớn và chứa đựng rủi ro vận hành cao. Đây không phải là môi trường phù hợp để một Agent tự đưa ra quyết định thực thi (No full-auto). | **Đặt lại ranh giới (Boundary) cho AI:** Hạ cấp giải pháp từ Agent tự trị hoàn toàn xuống mức độ LLM Feature / Workflow (Copilot). AI sẽ chỉ chịu trách nhiệm gom dữ liệu, đọc log, tóm tắt tình trạng kẹt và đề xuất checklist hướng xử lý. Con người (Admin/Dev) luôn giữ quyền quyết định cuối cùng và trực tiếp nhấn nút chạy live thủ công. |
| **Đánh giá Hệ thống Đo lường (Metric)** | 3 metric đề xuất (Thời gian triage, số nguồn mở, độ chính xác) | Các chỉ số về thời gian phân loại ca lỗi và số lượng nguồn dữ liệu phải mở hoàn toàn có thể định lượng để đo đạc hiệu quả. | Con số thời gian xử lý baseline (ví dụ: giả định 30 phút) chưa có log cụ thể trong hệ thống hiện tại để chứng minh là hoàn toàn chính xác. | **Thay đổi cách tiếp cận metric:** Coi con số thời gian ban đầu chỉ là giả định giả thuyết. Nhóm sẽ triển khai một giai đoạn chạy thử (Pilot) trên từ 3 đến 5 sự cố (incident) thực tế để đo đạc lại chính xác các chỉ số baseline, từ đó mới làm căn cứ đánh giá hiệu quả thực tế của AI. |
| Audit tài liệu handover | 1 bộ tài liệu | Có nhiều phần riêng cho kiểm trạng thái đơn, retry system, error codes, known risks và recovery flow | Tài liệu đã có checklist nên một phần pain có thể giải bằng rule/process, không cần AI ngay | Thu hẹp problem vào triage nhiều nguồn, không phải "AI tự xử lý mọi lỗi đơn" |
| Replay một incident giả lập | 1 mã đơn mẫu / kịch bản mẫu | Để kết luận một đơn đang kẹt ở đâu cần gom ít nhất 3 nguồn: trạng thái order, action log và raw API/error code | Nếu đã có dashboard gom đủ 3 nguồn thì bottleneck giảm mạnh | Đưa dashboard/script gom snapshot làm non-AI baseline trước AI |
| Review workflow recovery/status sync | 2 flow vận hành | Có các bước rủi ro như dry run, live update, retry/recovery và cần người thật approve | Đây là thao tác production có side effect, không phù hợp để agent tự chạy | Boundary: AI chỉ tóm tắt/đề xuất checklist; dev quyết định và chạy live thủ công |
| Kiểm tra khả năng đo metric | 3 metric đề xuất | Có thể đo thời gian triage, số nguồn phải mở, số case kết luận đúng/sai | Chưa có log đủ để xác nhận baseline 30 phút là chính xác | Ghi baseline là giả định ban đầu; pilot cần đo 3-5 incident thật |

## 5. Research / hướng giải pháp thực tế
Nhóm không xem các option như những giải pháp ngang nhau. Research dùng để chốt một hướng V1 đủ thực tế: **read-only trước, rule rõ trước, AI chỉ hỗ trợ tóm tắt, mọi action production phải có người duyệt**.

Flow V1 đề xuất:

```text
Nhập order_number
→ gom diagnostic snapshot read-only
→ rule table phân loại case
→ RAG lấy đúng phần runbook/error-code/recovery docs liên quan
→ LLM tóm tắt + giải thích nếu log dài
→ dev/admin review
→ dry-run
→ human approve
→ retry/recovery khi thật sự cần
```

Workflow kỹ thuật V1:

```text
Admin/dev nhập order_number
→ Read-only diagnostic script query DB/action log/API log
→ Tạo 1 JSON snapshot chuẩn
→ Rule engine phân loại case rõ theo bảng lỗi
→ Nếu thiếu context hoặc log dài: retrieve docs liên quan từ runbook/error-code table
→ LLM đọc snapshot + docs được retrieve, trả về summary/checklist theo JSON schema
→ Dev/admin review raw evidence
→ Dry-run + preview affected records
→ Human approve
→ Live retry/recovery nếu cần
```

AI/model dùng trong V1:

- **Không cần fine-tune ở V1.** Upload docs không làm model "học" theo nghĩa đổi trọng số; docs nên được dùng như **knowledge base/RAG** để truy xuất đúng đoạn runbook, bảng error code và recovery flow.
- **LLM đề xuất cho pilot:** `GPT-4.1 mini` hoặc một LLM tương đương có khả năng đọc context dài và trả JSON ổn định. Nhiệm vụ của model là tóm tắt snapshot/log, giải thích vì sao case thuộc nhóm lỗi nào, và đề xuất checklist tiếp theo.
- **Nếu dùng docs upload/RAG:** dùng embedding/vector search để retrieve 3-5 đoạn liên quan nhất từ handover docs, error-code table, recovery guide; sau đó đưa các đoạn này cùng JSON snapshot vào LLM.
- **Nếu cần độ chính xác cao hơn:** rule table vẫn là nguồn phân loại chính cho các case rõ. LLM chỉ hỗ trợ phần log dài/context mơ hồ và phải được phép trả `Unknown / escalate to dev`.
- **Output bắt buộc dạng schema:** `case_type`, `evidence`, `confidence`, `recommended_next_check`, `must_not_do`, `needs_human_review`.

Tool / case tham khảo:

| Nguồn / tool / case | Link | Họ giải quyết phần nào? | Điểm mạnh | Khoảng trống / rủi ro | Bài học cho nhóm |
|---|---|---|---|---|---|
| OpenAI File Search / Vector Stores | https://platform.openai.com/docs/guides/tools-file-search | Upload runbook/error-code/recovery docs và retrieve đoạn liên quan khi xử lý một `order_number` | Có sẵn retrieval trên docs, hợp với handover dài | Không tự đảm bảo phân loại đúng nếu docs thiếu hoặc retrieve sai đoạn | Dùng RAG để lấy context, không gọi là model "học" docs |
| OpenAI GPT-4.1 mini | https://platform.openai.com/docs/models/gpt-4.1-mini | LLM đọc diagnostic snapshot + docs được retrieve, rồi tóm tắt và giải thích case | Nhanh, chi phí thấp hơn model lớn, hợp pilot đọc context và trả JSON | Có thể hallucinate hoặc hiểu sai error code nếu không ép evidence/schema | Chỉ dùng để summary/checklist, không dùng để quyết định live action |
| OpenAI Structured Outputs | https://platform.openai.com/docs/guides/structured-outputs | Ép output theo schema như `case_type`, `evidence`, `confidence`, `must_not_do` | Giúp dev dễ kiểm tra, log lại và so sánh với rule table | Schema đúng không có nghĩa nội dung luôn đúng | Output AI phải có evidence và confidence, không chỉ văn bản tự do |
| pgvector | https://github.com/pgvector/pgvector | Nếu muốn tự host RAG trong Postgres, lưu embedding cho handover docs/error-code table | Tận dụng Postgres, dễ giữ dữ liệu nội bộ hơn hosted vector store | Cần tự build ingestion, chunking, ranking và permission | Chỉ cần khi không muốn upload docs lên hosted tool |
| Appsmith internal dashboard | https://www.appsmith.com/ | Làm dashboard read-only nhập `order_number`, hiển thị snapshot, rule classification và AI summary | Nhanh để dựng admin/debug UI nội bộ | Nếu thêm nút live action quá sớm sẽ tăng rủi ro production | V1 dashboard chỉ read-only; retry/recovery tách flow approve riêng |

Tool stack V1 được chọn:

```text
Read-only diagnostic script + rule table
+ OpenAI File Search hoặc pgvector cho docs retrieval
+ GPT-4.1 mini cho summary/checklist dạng structured output
+ dashboard read-only để dev/admin review
+ dry-run script riêng cho action có side effect
```

| Thành phần V1 | Vai trò | Vì sao thực tế | Boundary |
|---|---|---|---|
| Diagnostic snapshot | Gom order status, `isDelivered`, `isCanceled`, reference code, report/sync status, missing actions, latest API error, retry count, latest log timestamp | Giảm việc mở DB, action log và API log thủ công; PM/admin có một màn hình chung để hiểu case | Chỉ read-only, không update DB |
| Rule table | Phân loại case: completed/no action, missing report action, retryable external error, need admin verification, manual recovery, unknown/escalate | Dễ audit, dễ thống nhất cách xử lý giữa dev cũ và dev mới | Rule chỉ gợi ý nhóm lỗi, không tự quyết định live action |
| RAG + AI summary | Retrieve đúng đoạn docs liên quan, rồi tóm tắt snapshot/log dài và gợi ý checklist kiểm tra tiếp theo | Hữu ích khi log dài hoặc người xử lý chưa quen domain; không cần "dạy" model bằng fine-tune ngay | AI không tự query DB, không gọi API ngoài, không retry/recovery |
| Safe action flow | Dry-run, preview danh sách record bị ảnh hưởng, human approve rồi mới chạy live action nếu cần | Giảm rủi ro thao tác nhầm production | Dev/admin chịu trách nhiệm quyết định cuối |

Before / After ngắn:

| Before | After |
|---|---|
| Dev phải mở DB, action log và API log thủ công | Nhập `order_number` là có snapshot |
| Mỗi người debug theo cách riêng | Có rule table và checklist xử lý thống nhất |
| Khó biết lỗi có retry được hay cần manual recovery | Case được phân loại trước khi quyết định |
| Dễ thao tác nhầm trên production | Action nguy hiểm luôn có dry-run và human approve |

Research takeaway:

```text
V1 không nên là AI Agent tự xử lý production. Giải pháp thực tế hơn là:
nhập order_number → gom diagnostic snapshot read-only → rule table phân loại case
→ RAG lấy đúng docs liên quan → LLM tóm tắt nếu log dài → dev/admin review → dry-run → human approve
→ mới retry/recovery khi cần.
```

---

## 6. Workflow before/after

Nội dung workflow:

```text
CURRENT STATE — 7 bước, 30 phút

┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│ Bước 1              │     │ Bước 2              │     │ Bước 3              │
│ Admin/support báo   │ ──→ │ Dev nhận mã đơn     │ ──→ │ Kiểm trạng thái DB  │
│ đơn lỗi             │     │ Ai: Dev/Ops         │     │ Ai: Dev/Ops         │
│ ◷ 2'                │     │ ◷ 2'                │     │ ◷ 5'                │
│ In: mã đơn          │     │ In: mã đơn          │     │ In: order fields    │
│ Out: ticket/alert   │     │ Out: case mở        │     │ Out: trạng thái DB  │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
                                                                  │
                                                                  ▼
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│ Bước 6              │     │ Bước 5              │     │ Bước 4              │
│ Tra rule + quyết    │ ←── │ Đọc raw API log     │ ←── │ Kiểm action log     │
│ định hướng xử lý    │     │ + error code        │     │ / bước đồng bộ      │
│ Ai: Dev/Ops         │     │ Ai: Dev/Ops         │     │ Ai: Dev/Ops         │
│ ◷ 5' 🔴             │     │ ◷ 8' 🔴             │     │ ◷ 5'                │
│ In: log + rule      │     │ In: raw log         │     │ In: action records  │
│ Out: next action    │     │ Out: nhóm lỗi       │     │ Out: bước thiếu     │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
          │
          ▼
┌─────────────────────┐
│ Bước 7              │
│ Phản hồi kết quả    │
│ cho admin/support   │
│ Ai: Dev/Ops         │
│ ◷ 3'                │
│ In: next action     │
│ Out: update status  │
└─────────────────────┘

🔴 = Bottleneck      ◷ Tổng: 30 phút


FUTURE STATE — 5 bước, 8-10 phút

┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│ Bước 1              │     │ Bước 2              │     │ Bước 3              │
│ Nhập mã đơn         │ ──→ │ Rule/script gom     │ ──→ │ AI tóm tắt tình     │
│ Ai: Admin/Dev       │     │ DB + action + log   │     │ trạng + checklist   │
│ ◷ 1'                │     │ 🔵 Rule/script      │     │ 🔵 Workflow step    │
│ In: mã đơn          │     │ ◷ 2'                │     │ ◷ 1'                │
│ Out: case           │     │ Out: snapshot       │     │ Out: triage draft   │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
                                                                  │
                                                                  ▼
                         ┌─────────────────────┐     ┌─────────────────────┐
                         │ Bước 4              │     │ Bước 5              │
                         │ Dev review raw data │ ──→ │ Dev quyết định      │
                         │ + checklist         │     │ retry/recovery      │
                         │ 🟢 Human boundary   │     │ / manual            │
                         │ ◷ 4'                │     │ 🟢 Human action     │
                         │ In: snapshot/draft  │     │ ◷ 1-2'              │
                         │ Out: kết luận       │     │ Out: action plan    │
                         └─────────────────────┘     └─────────────────────┘

🔵 = AI / rule xử lý      🟢 = Human boundary      ◷ Tổng: 8-10 phút
Fallback: AI tóm tắt sai hoặc thiếu dữ liệu → dev đọc raw logs và dùng checklist thủ công.
Bottleneck mới: Dev review raw data + checklist. Đây là bottleneck chấp nhận được vì là điểm kiểm soát trước thao tác production.
```

Before/after impact:

| Metric | Trước | Sau kỳ vọng | Ghi chú |
|---|---:|---:|---|
| Thời gian triage | Khoảng 30 phút/incident | Dưới 10 phút/incident | Target chính |
| Số nguồn phải mở thủ công | 3-5 nguồn | 1 snapshot tổng hợp | DB/action/API log được gom trước |
| Bước thủ công | 7/7 | 2/5 chính | Dev vẫn review và quyết định |
| Bottleneck chính | Đọc log + tra rule thủ công | Review checklist/data | Human boundary chấp nhận được |
| Risk mới | Không có AI hallucination | AI có thể tóm tắt sai log/error code | Bắt buộc kiểm raw data trước live action |

---

## 7. Problem Statement v0

| Field | Nội dung |
|---|---|
| **Actor** | Backend dev hoặc ops/on-call xử lý incident khi trạng thái đơn trong hệ thống nội bộ bị kẹt/lệch với hệ thống bên ngoài. |
| **Workflow** | Admin/support báo mã đơn lỗi, dev kiểm database, kiểm action log, đọc raw API log/error code, tra rule xử lý rồi quyết định retry, recovery hoặc xử lý thủ công. |
| **Bottleneck** | Bước đọc log và tra rule mất khoảng 13 phút trong tổng 30 phút vì dev phải ghép nhiều nguồn dữ liệu rời rạc để hiểu trạng thái thật của đơn. |
| **Impact** | Admin/support phải chờ phản hồi; đơn bị lệch trạng thái lâu hơn; dev mới phụ thuộc người cũ; xử lý sai có thể retry nhầm, update DB sai hoặc bỏ sót đơn cần recovery. |
| **Success Metric** | Giảm thời gian triage từ khoảng 30 phút xuống dưới 10 phút; 90% incident có kết luận rõ về bước thiếu, nhóm lỗi và next action; không tăng retry/update sai. |
| **Boundary** | AI không gọi API bên ngoài, không chạy live command, không update database, không tự đánh dấu đơn thành công. Dev/ops phải kiểm raw data trước mọi thao tác có side effect. |

Điểm còn mơ hồ của v0:

- Cần nói rõ AI can thiệp sau khi script/rule đã gom dữ liệu, không tự truy cập production.
- Cần tách rõ retry/recovery/manual là quyết định của dev, không phải output tự động.
- Baseline 30 phút nên được thay bằng số liệu incident thật nếu nhóm có log.

---

## 8. AI-fit matrix

Bài toán nằm ở ô:

```text
Độ mơ hồ trung bình/cao + độ phức tạp cao → Workflow có AI hỗ trợ, chưa cần Agent.
```

Vì sao:

- Độ phức tạp cao: cần nối nhiều nguồn như database, action log, raw API log, error code và setting.
- Độ mơ hồ trung bình/cao: cùng một error code có thể cần xử lý khác nhau tùy context đơn.
- AI không cần tự quyết định bước tiếp theo; checklist có thể định nghĩa trước.
- Sai sót có thể gây hậu quả production, nên phải có human review.

---

## 9. Rule / Workflow / Agent

| Mức | Phương án cho bài toán nhóm | Khi nào đủ | Rủi ro | Chọn? |
|---|---|---|---|---|
| **No AI / process fix** | Checklist debug thủ công: field nào cần kiểm, log nào cần mở, error code nào cần tra | Đủ nếu incident ít và dev quen domain | Vẫn mất thời gian, dev mới dễ bỏ sót bước | Không chọn làm toàn bộ, nhưng là baseline |
| **Rule** | Script/dashboard gom trạng thái đơn, action thiếu, error code mới nhất và cảnh báo case rõ | Đủ cho case đơn giản như thiếu action rõ ràng hoặc error code đã map | Không giải thích tốt raw log dài hoặc context phức tạp | Dùng cho bước gom data |
| **Workflow** | Rule/script gom snapshot → AI tóm tắt tình trạng và map checklist → dev review raw data → dev quyết định action | Hợp vì workflow tuyến tính, AI chỉ hỗ trợ đọc/tóm tắt/giải thích | AI tóm tắt sai, bỏ sót context, dev quá tin output | Chọn |
| **Agent** | Agent tự query production, tự gọi retry/recovery, tự update database theo kết luận | Chỉ cần nếu hệ thống có guardrail, sandbox, approval flow và audit rất chặt | Quá rủi ro: side effect production, data/security, khó rollback | Không chọn |

Mức chọn:

```text
Workflow.
```

Vì sao chọn:

- Rule/checklist giải được phần gom dữ liệu và case rõ.
- AI có ích ở bước đọc/tóm tắt log và giải thích error code theo ngữ cảnh.
- Dev vẫn là người review raw data và quyết định thao tác cuối.
- Chưa cần agent vì không nên để AI tự hành động trên production.

---

## 10. Problem Statement v1

| Field | Nội dung |
|---|---|
| **Actor** | Backend dev hoặc ops/on-call xử lý incident khi trạng thái đơn trong hệ thống nội bộ bị kẹt/lệch với hệ thống bên ngoài. |
| **Workflow** | Admin/support báo mã đơn lỗi → dev kiểm trạng thái đơn trong database → kiểm action log/bước đồng bộ → đọc raw API log và error code → tra rule xử lý → quyết định retry, recovery hoặc xử lý thủ công → phản hồi kết quả. |
| **Bottleneck** | Bước đọc raw API log và tra rule xử lý mất khoảng 13 phút trong tổng 30 phút vì dev phải tự ghép nhiều nguồn dữ liệu để biết đơn đang kẹt ở bước nào. |
| **Impact** | Admin/support phản hồi chậm; đơn bị lệch trạng thái lâu hơn; dev mới phụ thuộc người cũ; xử lý sai có thể retry nhầm, update database sai hoặc bỏ sót đơn cần recovery. |
| **Success Metric** | Giảm thời gian triage từ khoảng 30 phút xuống dưới 10 phút; ít nhất 90% incident có kết luận rõ về bước thiếu, nhóm lỗi và next action; không tăng số lần retry nhầm hoặc update database sai. |
| **Boundary** | AI không tự gọi API bên ngoài, không chạy live command, không update database, không tự đánh dấu đơn thành công. Dev/ops phải kiểm raw data trước mọi thao tác có side effect. |
| **AI intervention point** | Sau khi rule/script gom snapshot gồm database fields, action log và API log; trước khi dev quyết định retry/recovery/manual. |
| **Mức chọn** | Workflow: rule/script gom dữ liệu, AI tóm tắt tình trạng và map checklist, dev review raw data rồi quyết định action. |
| **Rủi ro & người thật kiểm tra** | Risk: AI tóm tắt sai log, hiểu sai error code, bỏ sót context. Người thật kiểm tra: dev/ops đối chiếu raw data và checklist trước mọi thao tác live. |

---

## 11. Final decision

| Câu hỏi | Yes / Not Yet / No | Ghi chú |
|---|---|---|
| Actor và workflow đã rõ chưa? | Yes | Backend dev/ops xử lý incident trạng thái đơn. |
| Baseline và success metric đã đo được chưa? | Not Yet | Có ước lượng 30 phút → dưới 10 phút; nên đo thêm 3-5 incident thật. |
| Có data/input đủ dùng chưa? | Yes | Có database fields, action log, raw API log, error code table, handover checklist. |
| Nếu AI sai, hậu quả có chấp nhận được không? | Yes, nếu có review | AI chỉ tóm tắt; dev kiểm raw data trước live action. |
| Có người review/owner vận hành không? | Yes | Dev/ops/on-call là owner. |
| Có cách non-AI đơn giản hơn không? | Yes | Checklist + dashboard/script gom trạng thái là baseline. |

Decision:

```text
Go với scope nhỏ.
```

Pilot nhỏ nhất:

- Chọn 3-5 incident trạng thái đơn đã xử lý trước đó.
- Viết script hoặc template gom snapshot: order fields, action log, API log/error code.
- Cho AI tóm tắt tình trạng và đề xuất nhóm nguyên nhân/next action.
- Dev so sánh output AI với kết luận thật của incident.
- Đo thời gian triage, số lỗi tóm tắt, số case cần đọc lại raw log.

Exit / rollback:

- Nếu AI phân loại sai nhóm lỗi quá 20% trong pilot, chỉ dùng dashboard/rule checklist.
- Nếu AI output thiếu raw evidence hoặc không chỉ ra nguồn, không dùng để hỗ trợ quyết định.
- Nếu thao tác có side effect như retry/recovery/update DB, bắt buộc dev chạy thủ công sau khi kiểm checklist.

Decision rationale:

- Problem rõ, workflow rõ, metric rõ.
- Có evidence từ dự án thật và tài liệu handover.
- Có non-AI baseline trước.
- AI nằm ở một bước cụ thể: tóm tắt và map checklist.
- Human review và rollback rõ, không trao quyền production cho AI.