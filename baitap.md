# BÁO CÁO PHÂN TÍCH VÀ XỬ LÝ SỰ CỐ CACHE & PHIÊN ĐĂNG NHẬP

## Phần 1: Phân tích nguyên nhân

* **Tại sao CSS không cập nhật (Vấn đề giao diện):**
  * Trình duyệt đang lưu trữ tệp CSS cũ trong **Browser Cache** để tối ưu hóa tốc độ tải trang. Khi nhấn `F5` (Normal Reload), trình duyệt vẫn ưu tiên tải lại file từ bộ nhớ đệm cục bộ thay vì gửi yêu cầu mới nhận file CSS đã sửa đổi từ máy chủ.
* **Tại sao phiên đăng nhập bị mất (Vấn đề Cookies):**
  * Mã nguồn không thiết lập các thuộc tính thời gian sống như `Max-Age` hay `Expires` cho cookie định danh, khiến chúng trở thành **Session Cookies**. Khi đóng trình duyệt, toàn bộ **Session Cookies** này sẽ tự động bị xóa sạch, dẫn đến việc người dùng bị văng khỏi hệ thống và phải đăng nhập lại từ đầu. Ngược lại, **Persistent Cookies** có định nghĩa thời gian sống rõ ràng sẽ được lưu trữ lâu dài trên ổ cứng ngay cả khi tắt trình duyệt.

---

## Phần 2: Giải pháp khắc phục

* **1. Xử lý tức thì lỗi giao diện cũ:**
  * Thực hiện **Hard Reload** bằng cách sử dụng phím tắt `Ctrl + F5` (trên Windows) hoặc `Cmd + Shift + R` (trên Mac). Hành động này buộc trình duyệt bỏ qua bộ nhớ đệm và tải lại toàn bộ tài nguyên (bao gồm file CSS mới nhất) trực tiếp từ máy chủ.
* **2. Duy trì trạng thái đăng nhập lâu dài:**
  * Cấu hình lại mã nguồn phía backend/frontend khi khởi tạo cookie định danh, bổ sung thuộc tính `Max-Age` (hoặc `Expires`) với khoảng thời gian phù hợp (ví dụ: `Max-Age=86400` cho 1 ngày hoặc lâu hơn) để chuyển đổi từ **Session Cookie** sang **Persistent Cookie**, giúp lưu giữ phiên làm việc qua các lần đóng/mở trình duyệt.
