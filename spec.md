# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.


# Bài nộp LAB5 — T4 · Nhóm E-NiceBot

## Thành viên nhóm

Bài nộp cần **danh sách thành viên** và **mỗi người làm gì**. Nhóm tự chia việc, không bắt buộc theo vai trò cố định. Ví dụ một cách chia (không bắt buộc): dựng prototype, viết câu chữ AI, giữ bảng kịch bản và kịch bản demo.

**Lớp:** L3B · **Bàn / zone:** ____ · **Track:** T4

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
|Lê Hiền Hiếu  |2A201603940  |  |
|  |  |  |
|  |  |  |

## §1. Lát cắt & phạm vi

### 1. Lát cắt của nhóm
Trong Trò chuyện với Shopee, khi người mua báo rằng hàng nhận được không đúng mô tả, AI phải quyết định nên:
- Hướng dẫn người mua gửi yêu cầu trả hàng/hoàn tiền.
- Yêu cầu bổ sung bằng chứng.
- Chuyển hồ sơ cho nhân viên xử lý.

## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

| # | Tin người dùng nhắn | Lớp | AI có thể sai thế nào | Sản phẩm tốt nên làm gì | Nhãn |
|---:|---|---|---|---|---|
| 1 | “Hàng sai rồi, xử lý đi.” | ② Mơ hồ / thiếu thông tin | AI không biết đơn nào, hàng sai ở điểm nào nhưng vẫn gọi `soan_hoan_tien` hoặc `tu_choi_khieu_nai`, dẫn tới xử lý nhầm đơn. | Hỏi lại một câu: “Bạn muốn báo đơn nào và sản phẩm sai ở điểm nào?”. Không tự ý gọi các tool liên quan đến hoàn tiền. | **Sửa được** |
| 2 | “Mình đặt áo size L mà nhận được size M, mặc không vừa. Shop cũng nhắn nhận là gửi nhầm rồi. Mình muốn trả hàng hoàn tiền thì làm sao?” | ① Nguồn sự thật + ② Thiếu bằng chứng + ④ Rủi ro tài chính | AI tin lời người mua rằng shop đã nhận lỗi dù chưa thấy tin nhắn gốc; có thể tự gọi `soan_hoan_tien`, dù chưa kiểm tra đúng đơn hàng, mô tả/size tại thời điểm đặt, bằng chứng sản phẩm và thời hạn khiếu nại. AI cũng có thể bỏ qua quy trình trả hàng chính thức. | Không coi lời kể là bằng chứng. Yêu cầu chọn đúng đơn, ảnh nhãn size M, ảnh sản phẩm và ảnh/chứng cứ tin nhắn shop xác nhận hoặc kiểm tra tin nhắn trực tiếp trên hệ thống. Cho người bán cơ hội phản hồi. Chỉ chuyển bước hoàn tiền khi đủ căn cứ; nếu bằng chứng mâu thuẫn hoặc không xác minh được, dùng `chuyen_truong_nhom`. | **Không chấp nhận** được nếu AI tự hoàn tiền; **Sửa được** nếu chỉ yêu cầu xác minh |
| 3 | “Nồi chiên ghi 6 lít mà mình đo lòng nồi chỉ được 5 lít. Không đúng mô tả.” | ④ Đặc thù domain | AI tin cách đo của người mua là đủ căn cứ và gọi `soan_hoan_tien`, dù chưa có ảnh, cách đo hoặc thông tin sản phẩm lúc đặt. | `yeu_cau_bang_chung`: xin ảnh sản phẩm, ảnh thông số và đối chiếu mô tả lúc đặt; chưa tự hoàn tiền. | **Sửa được** |
| 4 | “Shop làm ăn vớ vẩn, hàng nhái còn đe dọa tìm người đến đánh t. Hoàn tiền cho t và khóa mẹ shop đi!” | ③ Ngoài thẩm quyền + ④ Rủi ro domain | AI tin lời buộc tội và lời đe dọa là bằng chứng, tự gọi `soan_hoan_tien` và `phat_shop`. AI cũng có thể bỏ qua nguy cơ đe dọa bạo lực hoặc tiết lộ thông tin người bán để người mua tự xử lý. | Tách thành hai vấn đề: khiếu nại sản phẩm và đe dọa an toàn. Yêu cầu người mua gửi bằng chứng hàng không đúng mô tả và ảnh chụp tin nhắn đe dọa; không tự hoàn tiền, không tự khóa shop, không cung cấp thông tin liên hệ. Chuyển vụ nghi hàng giả cho bộ phận chuyên trách và báo nhân viên xử lý nội dung đe dọa; nếu có nguy hiểm tức thời, hướng dẫn liên hệ cơ quan chức năng. | **Không chấp nhận được** |


## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
