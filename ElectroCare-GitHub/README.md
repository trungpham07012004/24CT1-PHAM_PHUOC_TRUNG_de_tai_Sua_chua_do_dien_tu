# ElectroCare

Ứng dụng web quản lý dịch vụ sửa chữa điện tử: khách hàng đặt lịch và tra cứu phiếu; kỹ thuật viên cập nhật quá trình sửa chữa; quản trị viên quản lý nhân sự, dịch vụ, linh kiện và phân công công việc.

## Chức năng chính

- Đăng ký, đăng nhập và phân quyền khách hàng, kỹ thuật viên, quản trị viên.
- Đặt lịch sửa chữa, đính kèm ảnh thiết bị và tra cứu phiếu bằng mã phiếu.
- Theo dõi trạng thái sửa chữa, báo giá, checklist kiểm tra và bàn giao.
- Quản lý dịch vụ, cửa hàng, linh kiện, nhân viên và thống kê.
- Tích hợp Gemini để hỗ trợ chẩn đoán; cần API key riêng để sử dụng.

## Công nghệ

- Giao diện: HTML, CSS, JavaScript.
- Máy chủ: Node.js, Express.
- Cơ sở dữ liệu: MySQL.

## Yêu cầu

- Windows
- Node.js 20 trở lên và npm
- MySQL (có thể dùng XAMPP)

## Cài đặt và chạy

1. Tạo database và các bảng bằng cách import `co-so-du-lieu/tao-co-so-du-lieu.sql` vào MySQL qua phpMyAdmin hoặc MySQL client.
2. Chạy `CAI_DAT_ELECTROCARE.bat`. Script cài thư viện và tự tạo `may-chu/.env` riêng trên máy lần đầu chạy, bao gồm khóa JWT và mã mời ngẫu nhiên. File `.env` không cần tải từ GitHub.
3. Nếu MySQL không dùng cấu hình XAMPP mặc định (`127.0.0.1`, cổng `3306`, tài khoản `root`, mật khẩu để trống), sửa các giá trị `DB_*` trong `may-chu/.env`. Mã mời đăng ký nhân viên/quản trị viên cũng được lưu trong file này. Không đưa file `.env` lên GitHub hoặc gửi công khai.
4. Bật MySQL trong XAMPP, sau đó chạy `CHAY_ELECTROCARE.bat`.
5. Mở giao diện tại <http://localhost:5173>. Kiểm tra API và kết nối database tại <http://localhost:3000/api/health>.

Có thể chạy từng thành phần riêng:

```powershell
npm --prefix may-chu install
npm --prefix may-chu start
```

Trong cửa sổ PowerShell khác:

```powershell
npm --prefix giao-dien run dev
```

## Cấu hình môi trường

Các tên biến được liệt kê trong `may-chu/.env.example`; script cài đặt tạo cấu hình cục bộ từ file mẫu. `GEMINI_API_KEY` không bắt buộc nếu không sử dụng tính năng AI. Nếu xóa `.env`, chạy lại script cài đặt để tạo file mới. Không đưa `may-chu/.env` lên GitHub.

Tài khoản demo được tạo bởi script database có mật khẩu `123456`, chỉ dùng để thử nghiệm cục bộ. Hãy đổi hoặc xóa các tài khoản demo trước khi dùng dữ liệu thật; không triển khai cấu hình demo lên môi trường công khai.

## Cấu trúc thư mục chính

```text
co-so-du-lieu/  Script tạo database
giao-dien/      Mã nguồn giao diện
may-chu/        API và cấu hình backend
```

Ảnh tải lên khi chạy ứng dụng được lưu cục bộ trong `may-chu/tep-tai-len/` và không thuộc mã nguồn.
