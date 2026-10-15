# User Stories — EduHub

Phạm vi: hệ thống quản lý câu lạc bộ và sự kiện sinh viên. Có đủ 3 vai trò: **Sinh viên (Student)**, **Ban chủ nhiệm CLB (Club Board)** và **Quản trị viên (Admin)**. Mỗi User Story có tối thiểu 2 tiêu chí nghiệm thu.

## 1. Vai trò: Sinh viên (Student)

### US-01 — Đánh giá sự kiện
**Là** sinh viên đã tham dự sự kiện, **tôi muốn** gửi đánh giá và nhận xét, **để** góp ý giúp CLB cải thiện hoạt động.

- **AC1:** Khi phiếu đăng ký của sinh viên đã được xác nhận và sinh viên đã check-in, hệ thống cho phép gửi đánh giá từ 1 đến 5 sao kèm nhận xét; đánh giá được lưu và điểm trung bình sự kiện được cập nhật.
- **AC2:** Nếu sinh viên chưa check-in, chưa đăng ký hoặc số sao nằm ngoài khoảng 1–5, hệ thống từ chối đánh giá và hiển thị thông báo phù hợp.

### US-02 — Hủy đăng ký sự kiện
**Là** sinh viên đã đăng ký sự kiện, **tôi muốn** hủy đăng ký trước giờ diễn ra, **để** nhường chỗ cho người khác khi không thể tham dự.

- **AC1:** Nếu sự kiện chưa bắt đầu và phiếu đang ở trạng thái `Pending` hoặc `Confirmed`, hệ thống chuyển phiếu sang `Cancelled` và cập nhật số chỗ còn lại.
- **AC2:** Nếu sự kiện đã hoặc đang diễn ra, hoặc phiếu đã bị hủy, hệ thống từ chối yêu cầu và thông báo lý do.

## 2. Vai trò: Ban chủ nhiệm CLB (Club Board)

### US-03 — Duyệt đơn đăng ký sự kiện
**Là** thành viên Ban CLB tổ chức sự kiện, **tôi muốn** duyệt các phiếu đăng ký, **để** xác nhận danh sách người tham dự.

- **AC1:** Khi phiếu ở trạng thái `Pending`, Ban CLB có thể xác nhận; trạng thái chuyển thành `Confirmed` và hệ thống hiển thị thông báo xác nhận.
- **AC2:** Nếu phiếu đã `Confirmed` hoặc `Cancelled`, hệ thống không cho duyệt lại và hiển thị thông báo lỗi.

### US-04 — Cập nhật thông tin câu lạc bộ
**Là** thành viên Ban CLB, **tôi muốn** cập nhật tên và mô tả CLB, **để** thông tin giới thiệu luôn chính xác.

- **AC1:** Khi tên CLB hợp lệ, hệ thống lưu tên và mô tả mới và hiển thị thông tin đã cập nhật.
- **AC2:** Nếu tên CLB bị bỏ trống hoặc chỉ chứa khoảng trắng, hệ thống không lưu thay đổi và thông báo lỗi.

## 3. Vai trò: Quản trị viên (Admin)

### US-05 — Duyệt đề xuất thành lập CLB
**Là** quản trị viên, **tôi muốn** xem xét và duyệt đề xuất thành lập CLB, **để** đảm bảo CLB mới tuân thủ quy định của nhà trường.

- **AC1:** Khi đề xuất đang chờ duyệt được chấp thuận, hệ thống tạo CLB mới từ thông tin hợp lệ và ghi nhận người duyệt.
- **AC2:** Nếu đề xuất đã được duyệt hoặc từ chối trước đó, hệ thống không xử lý lần nữa và thông báo đề xuất đã được xử lý.

---

## Phạm vi triển khai

Các User Story mô tả yêu cầu nghiệp vụ tổng thể. Phần Domain Model trong bài thực hành hiện triển khai 5 lớp cốt lõi `Member`, `Club`, `Event`, `Registration`, `CheckIn`; các chức năng đánh giá và duyệt đề xuất CLB được mô tả ở mức yêu cầu, chưa có entity riêng trong phạm vi 5 lớp của Ch01.
