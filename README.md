# Chấm Hóa — phiên bản viết lại

PWA tĩnh, chạy trực tiếp trên GitHub Pages. Không cần Node.js, database hay máy chủ.

## Tính năng chính

- Giao diện trang chủ có ảnh giáo viên được cung cấp trong `teacher-photo.png`.
- Quản lý lớp và danh sách học sinh.
- SBD riêng cho từng học sinh; mặc định 6 chữ số, có thể đổi trong Cài đặt.
- Quản lý đề kiểm tra và nhiều mã đề.
- **Mã đề bắt buộc đúng 4 chữ số**, bao gồm cả mã có số 0 ở đầu như `0001`.
- Màn hình **Chấm hàng loạt** tối ưu cho điện thoại: hàng đợi, trạng thái chưa chấm/đã lưu, lưu và chuyển tiếp.
- Phiếu trả lời có 4 ô mốc, khu vực SBD, 4 cột mã đề và 18 câu phần I.
- **OMR qua camera:** mở camera trực tiếp hoặc chọn ảnh phiếu; hệ thống đọc ô mốc, hiệu chỉnh phối cảnh, nhận SBD, mã đề và đáp án A/B/C/D.
- Khi nhận dạng được đáp án, app tự tính điểm gợi ý theo đáp án phần I; giáo viên luôn có thể sửa điểm trước khi lưu.
- Phiếu có mã đề thiếu chữ số, tô nhiều ô hoặc SBD không rõ sẽ được đánh dấu cần xem lại.
- **Xuất Excel:** trong Thống kê, chọn `Xuất Excel`; file `.xls` mở được bằng Excel/Google Sheets.
- **Xuất PDF:** trong Thống kê, chọn `Xuất PDF`, sau đó chọn `Save as PDF` trong hộp thoại in của trình duyệt.
- In phiếu A4 theo đúng bố cục OMR.
- Sao lưu/khôi phục JSON.
- Offline-first qua service worker.

## Đưa lên GitHub Pages

1. Tạo repository mới trên GitHub.
2. Giải nén toàn bộ file trong thư mục này và đưa lên thư mục gốc của repository.
3. Vào **Settings → Pages**.
4. Chọn **Deploy from a branch**, branch `main`, folder `/ (root)` rồi bấm **Save**.
5. Mở link GitHub Pages bằng HTTPS. Camera chỉ hoạt động trên HTTPS hoặc localhost.

## Quy trình OMR

1. Tạo lớp và nhập học sinh kèm SBD.
2. Tạo đề, nhập đáp án phần I và thêm mã đề 4 chữ số.
3. Mở đề → `In phiếu A4`.
4. Cho học sinh tô kín SBD, mã đề và đáp án.
5. Mở `Chấm hàng loạt` → chọn học sinh → `Mở camera` hoặc `Chọn ảnh`.
6. Đảm bảo cả 4 ô mốc đen nằm trong ảnh. Kiểm tra SBD, mã đề, độ tin cậy và điểm gợi ý.
7. Nhập/sửa điểm nếu cần → `Lưu và quét tiếp`.

## Lưu ý dữ liệu

Dữ liệu được lưu trong trình duyệt của từng thiết bị. Hãy dùng **Cài đặt → Tải bản sao lưu** định kỳ trước khi xóa dữ liệu trình duyệt hoặc đổi máy.

OMR hiện chấm tự động phần I gồm 18 câu A/B/C/D. Phần II và III cần bổ sung layout/đáp án tương ứng nếu đề sử dụng đầy đủ cấu trúc THPT; điểm luôn có bước xác nhận thủ công trước khi lưu.

## Cấu trúc file

- `index.html`: giao diện và logic ứng dụng.
- `omr.js`: nhận dạng OMR, marker, phối cảnh, SBD, mã đề và đáp án.
- `teacher-photo.png`: ảnh giáo viên hiển thị trên Trang chủ và được cache offline.
- `manifest.webmanifest`: cấu hình cài PWA.
- `sw.js`: cache offline.
- `icon-*.png`: icon ứng dụng.
