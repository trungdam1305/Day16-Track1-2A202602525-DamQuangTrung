# Memo Teardown — Cursor (Anysphere)

**Họ tên:** Đàm Quang Trung — MSV 2A202602525

**Vì sao chọn sản phẩm này:** Cursor là sản phẩm AI-native mà AI chiếm gần như toàn bộ trải nghiệm; changelog và blog công khai đầy đủ nên dựng được timeline có link gốc; JTBD rõ ràng ("viết và sửa code nhanh hơn").

## §1. Timeline các cập nhật lớn

| Thời điểm | Cập nhật | Context lúc đó | Nguyên lý |
|---|---|---|---|
| 24/11/2024 | v0.43: Composer trong sidebar + bản đầu của agent tự chọn context và dùng terminal ([changelog](https://cursor.com/changelog/0-43-x)) | Copilot vẫn chủ yếu là autocomplete/chat; model (Claude 3.5 Sonnet) đủ mạnh để làm tác vụ nhiều bước | **Quy tắc x10**: chuyển từ "gợi ý từng dòng" sang "giao cả tác vụ" thì nhanh hơn một bậc độ lớn, không phải +20% |
| 19/02/2025 | v0.46: Agent thành chế độ mặc định, gộp Chat/Composer/Agent ([changelog](https://cursor.com/changelog/0-46-x)) | Cuộc đua agent coding bắt đầu nóng; forum có phản ứng trái chiều về việc ép mặc định | **Định nghĩa "tốt" thay đổi**: "tốt" không còn là gợi ý đúng mà là tác vụ hoàn thành end-to-end; đặt cược workflow lên agent |
| 04/06/2025 | Cursor 1.0: Bugbot (review PR), Background Agent cho mọi user, Memories, MCP một-click ([changelog](https://cursor.com/changelog/1-0)) | Cùng tháng ARR vượt 500 triệu USD, vòng Series C 900 triệu USD ([TechCrunch](https://techcrunch.com/2025/06/05/cursors-anysphere-nabs-9-9b-valuation-soars-past-500m-arr/)); OpenAI mua Windsurf | **Moat từ workflow** (Memories, review PR, MCP gắn vào chu trình dev thật) + **vòng lặp học** (memory giữ ngữ cảnh theo dự án) |
| 16/06 – 04/07/2025 | Đổi pricing từ 500 fast request sang pool credit theo giá API; sau phản ứng dữ dội phải xin lỗi và hoàn tiền ([blog xin lỗi](https://cursor.com/blog/june-2025-pricing)) | Model mới tiêu nhiều token hơn mỗi request, chi phí inference vượt mô hình flat | **Unit economics của AI**: giá cố định không sống nổi khi chi phí biên theo token; chuyển sang usage-based, giữ Auto/Tab làm "mức sàn" không giới hạn |
| 29/10/2025 | Cursor 2.0: model Composer riêng + giao diện multi-agent chạy song song bằng git worktree ([blog](https://cursor.com/blog/2-0)) | Phụ thuộc API của Anthropic/OpenAI, cũng là đối thủ trực tiếp (Claude Code, Codex) | **Wrapper → moat**: tự có model để giảm phụ thuộc và biên lợi nhuận; dữ liệu agent từ user làm vòng lặp học cho model riêng |
| 19/03/2026 | Composer 2: continued pretraining + RL, định giá thấp ([blog](https://cursor.com/blog/composer-2)) | Các lab tự làm công cụ coding; Cursor cần chi phí/token thấp hơn để giữ biên | **Vòng lặp học (data flywheel)**: hành vi dùng thật → huấn luyện model → trải nghiệm tốt hơn → thêm user |
| 02/09 và 10/09/2026 | Self-hosted Machines ([changelog](https://cursor.com/changelog/self-hosted-machines)) và Cursor Projects với coordinator agent ([changelog](https://cursor.com/changelog/projects)) | Khách doanh nghiệp đòi chạy trong hạ tầng riêng; agent chạy dài hơn | **Vertical AI / moat doanh nghiệp**: bảo mật, hạ tầng tự quản, quản lý dự án dài hạn là thứ model thô không có |

**Vì sao chọn những mốc này:** Mình chỉ giữ các quyết định đổi hình dạng sản phẩm (đơn vị công việc, giá, model, khách hàng). Đã loại: Tab model update và Yolo mode (0.44, cải tiến trong cùng khung autocomplete/agent), Jupyter support và dashboard (tính năng nhỏ), các vòng gọi vốn riêng lẻ (là kết quả chứ không phải quyết định sản phẩm — chỉ dùng làm context). Lưu ý: nguồn công khai về thương vụ mua lại Anysphere năm 2026 chỉ có ở Wikipedia và báo thứ cấp, mình chưa tự kiểm chứng ở nguồn gốc nên không đưa vào bảng.

## §2. Tệp user & JTBD

| | Early adopters (2023–đầu 2024) | Tệp hiện tại (2025–2026) |
|---|---|---|
| Đặc điểm | Lập trình viên cá nhân/indie hacker, đã dùng VS Code và Copilot, theo dõi AI Twitter, tự trả $20/tháng | Dev trong team nhỏ-vừa, ví dụ đội 12 người ở Innovatrix Infotech làm Shopify/Next.js/React Native với thư viện component dùng chung ([DEV](https://dev.to/emperorakashi20/why-we-switched-our-dev-team-to-cursor-and-what-we-miss-about-copilot-1459)); công ty mua theo seat/enterprise |
| JTBD chính | "Viết và sửa đoạn code này nhanh hơn mà không rời editor" | "Giao một tính năng/bug cho agent, rồi review kết quả và đưa vào PR đúng chuẩn của team" |
| Trước đó họ làm bằng cách nào | VS Code + Copilot, copy-paste sang ChatGPT | Tự code từng bước, hoặc dùng Copilot/Claude Code/Codex song song |

> **Nguồn cho §2:** [TechCrunch](https://techcrunch.com/2025/06/05/cursors-anysphere-nabs-9-9b-valuation-soars-past-500m-arr/) (Pro $20, Business $40), case study [DEV Community](https://dev.to/emperorakashi20/why-we-switched-our-dev-team-to-cursor-and-what-we-miss-about-copilot-1459) và [Trustpilot](https://ca.trustpilot.com/review/cursor.com). Hồ sơ early adopters là suy luận từ giá, lịch sử sản phẩm và việc Cursor là fork VS Code, không có nguồn trực tiếp nào mô tả nhóm này.

**Dịch chuyển tệp:** Mốc Cursor 1.0 (Bugbot, Background Agent, Memories) và Cursor 2.0 (multi-agent) làm đơn vị công việc đổi từ "dòng code" sang "PR/tác vụ", đây là ngôn ngữ của team chứ không phải cá nhân; mốc self-hosted/Projects (2026) xác nhận hướng doanh nghiệp.

**Switching cost (4 forces):**
- **Đẩy khỏi sản phẩm cũ (Copilot/VS Code thuần):** autocomplete không đủ khi cần sửa nhiều file; đội dev báo Cursor hiểu vấn đề ở cấp codebase thay vì từng file riêng lẻ.
- **Hút về Cursor:** agent + Composer, multi-agent, review PR; GitHub Copilot vẫn nhanh hơn ở inline completion nên nhiều dev dùng cả hai.
- **Thói quen cũ:** muốn giữ giao diện VS Code; Cursor là fork nên lực này nhẹ, nhưng với dev dùng JetBrains thì rất mạnh: 2 người trong đội 12 người ở trên không chuyển được.
- **Lo lắng chuyển đổi:** giá $20 so với $10 của Copilot, mất tích hợp GitHub (PR summary, Autofix), phải index 2–5 phút. Trên [Trustpilot](https://ca.trustpilot.com/review/cursor.com) (1,5/5, 337 review) các review 1–2 sao chủ yếu về hóa đơn bất ngờ, phụ phí dù đã tắt, hỗ trợ chỉ do AI từ chối hoàn tiền, và agent bỏ qua rules. Đây là JTBD "biết trước mình sẽ trả bao nhiêu" chưa được đáp ứng. Lưu ý Trustpilot thiên lệch về người đang bức xúc.

Lực giữ mạnh nhất hiện nay là **thói quen + context dự án** (rules, memories, index codebase nằm trong Cursor). Nếu lực này biến mất (đối thủ như Claude Code đạt tính năng tương đương và import được rules), user rời đi rất nhanh vì lòng trung thành chủ yếu dựa trên chất lượng agent chứ chưa phải dữ liệu bị khóa.

## §3. Ba dự đoán hướng đi (6–12 tháng tới)

**Dự đoán 1** *(loại: đe dọa Big Tech)*
- **Dự đoán:** Cursor sẽ tiếp tục đẩy mô hình Composer thành lựa chọn mặc định và bán rẻ hơn model của lab khác, để giảm phụ thuộc vào Anthropic/OpenAI.
- **Lập luận:** Mốc 2.0 và Composer 2 (§1) cho thấy quyết định đi từ wrapper sang model riêng; sự cố pricing 06/2025 cho thấy chi phí token là điểm đau lớn nhất; tệp đối thủ chính (Claude Code, Codex) cũng là nhà cung cấp model của họ.

**Dự đoán 2** *(loại: mở rộng segment)*
- **Dự đoán:** Cursor sẽ ra gói doanh nghiệp mạnh hơn (SSO/audit, self-host, chính sách riêng cho team) và nhắm cả người không phải dev (PM, designer) qua giao diện web/mobile và Projects.
- **Lập luận:** Self-hosted Machines và Projects (§1, mốc 2026) đã đi theo hướng này; tệp hiện tại dịch từ cá nhân sang team (§2) nên bước tiếp theo là ăn sâu workflow doanh nghiệp.

**Dự đoán 3** *(loại: mô hình kiếm tiền)*
- **Dự đoán:** Giá sẽ chuyển dần sang tính theo agent/tác vụ hoặc credit doanh nghiệp (pooled credits), thay cho seat cố định, kèm giới hạn minh bạch hơn.
- **Lập luận:** Mốc pricing 06–07/2025 cho thấy chi phí biên theo token buộc phải chuyển sang usage-based; khi agent chạy dài và song song (2.0, Projects), seat không còn phản ánh chi phí. **Giả định có thể gãy:** nếu Composer rẻ đi đủ nhiều, Cursor có thể quay lại gói flat "không giới hạn" để cạnh tranh.

Tự tin nhất: Dự đoán 3 (đã có tiền lệ trực tiếp trong timeline); giả định dễ gãy nhất: Dự đoán 1, vì phụ thuộc việc Composer đủ gần chất lượng frontier.

## §4. AI Log

| Việc | AI làm hay bạn làm? | Bạn kiểm chứng/phán đoán lại thế nào? |
|---|---|---|
| Tìm và tổng hợp mốc ứng viên, soạn bảng timeline | AI (Claude Code, dùng công cụ tìm web và đọc trang) | AI tự mở lại tất cả link trong bảng (0.43, 0.46, 1.0, 2.0, Composer 2, bài giá, Self-hosted, Projects, TechCrunch) và đối chiếu ngày/nội dung. Số "225 request" chỉ có ở bài báo thứ cấp nên không đưa vào. Công cụ đọc trang trả về tóm tắt, không phải bản gốc từng chữ. |
| Loại nguồn thứ cấp không rõ gốc (ARR, vụ mua lại 2026) | AI | Chỉ giữ số liệu có trên TechCrunch hoặc trang chính thức; vụ mua lại chỉ ghi chú, không đưa vào bảng |
| Chọn 7 cột mốc và gắn tên nguyên lý | AI đề xuất, người nộp chưa chỉnh | Nhãn nguyên lý là phán đoán của AI, không phải kết luận của nguồn |
| Viết §2 tệp user và 4 forces | AI, dựa trên tóm tắt review (G2, Trustpilot, DEV) | AI đọc case study DEV và Trustpilot; G2 chặn truy cập (403) nên không dùng. Tệp early adopters là suy luận, đã ghi rõ trong §2 |
| Viết 3 dự đoán | AI | Lập luận dẫn từ §1–§2; giả định dễ gãy đã ghi ngay trong dự đoán |
