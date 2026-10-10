# [VẬN DỤNG CƠ BẢN] CHUẨN HÓA ACCEPTANCE CRITERIA THEO GIVEN-WHEN-THEN

> 👤 **Học viên:** Đỗ Hoàng Sơn | **Mã SV:** PTIT-HCM-066
> 🏫 **Môn học:** IT206-K25-Agile-va-Scrum

---

## Phần 1: Phân tích các Acceptance Criteria hiện tại

Dưới đây là kết quả rà soát 4 Acceptance Criteria do Tú (Developer) viết cho tính năng áp mã khuyến mãi của ứng dụng RikkeiGo, được đối chiếu trực tiếp với khung Given - When - Then và các quy tắc nghiệp vụ.

- AC1: Đã chuẩn cấu trúc, mỗi phần rõ ràng, chỉ có 1 hành động và kết quả cụ thể.
- AC2: Viết thiếu phần Then kết quả cụ thể, dùng cụm từ chung chung gây khó khăn cho việc viết test case.
- AC3: Trộn lẫn hành động của người dùng vào phần Given, sai trật tự logic cơ bản của Given - When - Then.
- AC4: Viết gộp 2 kịch bản độc lập vào chung 1 AC, vi phạm nguyên tắc mỗi AC chỉ chứa một kịch bản duy nhất.

| Acceptance Criteria | Đúng/Sai | Quy tắc bị vi phạm | Hậu quả khi kiểm thử |
| --- | --- | --- | --- |
| AC1. Given cước chuyến là 100.000đ và khách chưa áp mã nào, When khách áp mã 'GO20' (giảm 20%), Then cước hiển thị 80.000đ. | Đúng | Không vi phạm | Đúng chuẩn Given-When-Then. Kịch bản rõ ràng, kiểm thử viên có thể chuyển thẳng thành test case mà không cần đoán. |
| AC2. Given mã 'GO20' đã hết hạn, When khách áp mã 'GO20' và bấm 'Đặt xe', Then hệ thống xử lý phù hợp. | Sai | Thiếu kết quả cụ thể ở phần Then (dùng câu chung chung 'hệ thống xử lý phù hợp'), và phần When chứa 2 hành động liên tiếp ('áp mã' và 'bấm Đặt xe'). | Kiểm thử viên không biết hệ thống sẽ hiển thị thông báo lỗi gì, hay giữ nguyên giá cước, dẫn đến việc không thể viết test case chính xác. |
| AC3. Given khách bấm 'Áp dụng', When mã 'ABC123' không tồn tại, Then hệ thống hiển thị 'Mã khuyến mãi không hợp lệ'. | Sai | Đặt sai vị trí hành động của người dùng ('bấm Áp dụng') vào phần Given, trong khi Given phải là trạng thái ban đầu có sẵn. | Sai bản chất kỹ thuật của Given-When-Then. Given mô tả tiền điều kiện (ví dụ: giỏ hàng trống, mã đã lưu), còn hành động 'bấm' phải nằm ở When. |
| AC4. Given chuyến đã áp mã 'GO20', When khách áp thêm mã 'FREEKM', Then hệ thống hiển thị 'Mỗi chuyến chỉ áp được 01 mã' và cước giữ nguyên 80.000đ. | Sai | Gộp chung 2 kịch bản độc lập trong cùng một AC: (1) Kiểm tra thông báo lỗi, (2) Kiểm tra giá cước giữ nguyên. | Khi test case chạy fail ở phần thông báo, tester khó xác định lỗi thuộc về phần thông báo hay phần tính toán cước. |

## Phần 2: Sửa lỗi các Acceptance Criteria

Sau khi rà soát và thảo luận lại với Đức (Product Owner), mình đã viết lại các AC chưa đạt chuẩn để đảm bảo tính tường minh, phục vụ trực tiếp cho việc viết test case.

- Sửa AC2: Tách hành động bấm nút thành kịch bản rõ ràng và bổ sung thông báo lỗi cụ thể khi mã hết hạn.
- Sửa AC3: Đưa hành động 'bấm áp dụng' về đúng vị trí When và chuyển trạng thái mã không tồn tại về Given.
- Sửa AC4: Tách thành 2 AC riêng biệt tương ứng với 2 tiêu chí kiểm chứng (thông báo lỗi và giá cước không đổi).

| Mã AC | Nội dung AC đã viết lại theo chuẩn Given - When - Then |
| --- | --- |
| AC2 (Sửa lại) | Given mã khuyến mãi 'GO20' đã quá thời hạn sử dụng, When khách hàng nhập mã 'GO20' và bấm nút 'Áp dụng', Then hệ thống hiển thị thông báo 'Mã khuyến mãi đã hết hạn' và giá cước giữ nguyên ở mức gốc. |
| AC3 (Sửa lại) | Given khách hàng đang ở màn hình nhập mã và mã 'ABC123' chưa từng được hệ thống tạo ra, When khách hàng nhập mã 'ABC123' và bấm nút 'Áp dụng', Then hệ thống hiển thị thông báo 'Mã khuyến mãi không hợp lệ'. |
| AC4a (Tách ý 1) | Given chuyến đi đã áp dụng thành công mã khuyến mãi 'GO20', When khách hàng tiếp tục nhập và bấm áp dụng mã 'FREEKM', Then hệ thống hiển thị thông báo 'Mỗi chuyến chỉ áp được 01 mã'. |
| AC4b (Tách ý 2) | Given chuyến đi đã áp dụng thành công mã khuyến mãi 'GO20' và hệ thống đang hiển thị thông báo trùng mã khi khách cố áp thêm mã mới, When khách hàng kiểm tra lại tổng cước chuyến đi, Then cước chuyến đi vẫn được giữ nguyên ở mức 80.000đ. |

---

## 📁 Danh sách tệp tin nộp bài trong Repository
- 📝 `bt1.docx`: Báo cáo tài liệu phân tích nghiệp vụ hoàn chỉnh.
