# ElectroCare

<p align="center">
  <strong>Hệ thống quản lý dịch vụ sửa chữa thiết bị điện tử</strong><br>
  Hỗ trợ khách hàng đặt lịch và theo dõi sửa chữa; hỗ trợ kỹ thuật viên xử lý phiếu; hỗ trợ quản trị viên quản lý hoạt động cửa hàng.
</p>

<p align="center">
  <img alt="Giao diện" src="https://img.shields.io/badge/Giao%20di%E1%BB%87n-HTML%20%7C%20CSS%20%7C%20JavaScript-E34F26">
  <img alt="Backend" src="https://img.shields.io/badge/Backend-Node.js%20%7C%20Express-339933">
  <img alt="Database" src="https://img.shields.io/badge/Database-MySQL-4479A1">
</p>

---

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Chức năng](#chức-năng)
- [Công nghệ sử dụng](#công-nghệ-sử-dụng)
- [Yêu cầu hệ thống](#yêu-cầu-hệ-thống)
- [Cài đặt và khởi chạy](#cài-đặt-và-khởi-chạy)
- [Cấu hình](#cấu-hình)
- [Cấu trúc dự án](#cấu-trúc-dự-án)
- [Xử lý sự cố](#xử-lý-sự-cố)
- [Lưu ý bảo mật](#lưu-ý-bảo-mật)

## Giới thiệu

ElectroCare là ứng dụng web hỗ trợ quy trình tiếp nhận và quản lý dịch vụ sửa chữa điện tử. Hệ thống phân quyền theo vai trò, kết nối giao diện web với API Node.js và cơ sở dữ liệu MySQL.

## Chức năng

- **Khách hàng:** đăng ký, đăng nhập, đặt lịch sửa chữa, gửi ảnh thiết bị và tra cứu phiếu bằng mã phiếu.
- **Kỹ thuật viên:** theo dõi phiếu được giao, cập nhật tiến độ, báo giá và checklist kiểm tra.
- **Quản trị viên:** quản lý nhân viên, cửa hàng, dịch vụ, linh kiện và phân công công việc.
- **Theo dõi sửa chữa:** cập nhật trạng thái và thông tin bàn giao.
- **Hỗ trợ AI:** tích hợp Gemini để hỗ trợ chẩn đoán; cần cấu hình API key riêng.
- **Kiểm tra dịch vụ:** API cung cấp endpoint kiểm tra trạng thái máy chủ và kết nối cơ sở dữ liệu.

## Công nghệ sử dụng

| Thành phần | Công nghệ |
| --- | --- |
| Giao diện | HTML, CSS, JavaScript |
| Máy chủ và API | Node.js, Express |
| Cơ sở dữ liệu | MySQL |
| Hỗ trợ AI | Google Gemini API (tùy chọn) |

## Yêu cầu hệ thống

- Windows
- Node.js 20 trở lên và npm
- MySQL; có thể sử dụng MySQL đi kèm XAMPP

## Cài đặt và khởi chạy

### Cách nhanh trên Windows

1. Cài Node.js 20 trở lên và XAMPP.
2. Khởi động MySQL trong XAMPP.
3. Tạo database `electrocare_v2` nếu chưa có, sau đó import [`co-so-du-lieu/tao-co-so-du-lieu.sql`](co-so-du-lieu/tao-co-so-du-lieu.sql) bằng phpMyAdmin hoặc MySQL client.
   - Nếu database đã có dữ liệu, hãy sao lưu trước khi import.
4. Chạy `CAI_DAT_ELECTROCARE.bat` để cài thư viện và tạo `may-chu/.env` cục bộ lần đầu.
5. Nếu MySQL không sử dụng cấu hình XAMPP mặc định, cập nhật các biến `DB_*` trong `may-chu/.env`.
6. (Tùy chọn) Điền Gemini API key vào `GEMINI_API_KEY` trong `may-chu/.env` nếu cần tính năng AI.
7. Chạy `CHAY_ELECTROCARE.bat` và giữ các cửa sổ máy chủ đang chạy.
8. Mở giao diện tại <http://localhost:5173>. Kiểm tra API và kết nối database tại <http://localhost:3000/api/health>.

### Chạy từng thành phần

Mở PowerShell tại thư mục dự án:

```powershell
npm --prefix may-chu install
npm --prefix may-chu start
```

Mở một cửa sổ PowerShell khác để chạy giao diện:

```powershell
npm --prefix giao-dien run dev
```

## Cấu hình

Các thiết lập máy chủ được lưu trong `may-chu/.env`. Mẫu cấu hình nằm tại `may-chu/.env.example`; script cài đặt sẽ tạo file `.env` cục bộ nếu file chưa tồn tại.

| Biến | Mục đích |
| --- | --- |
| `DB_HOST`, `DB_PORT` | Địa chỉ và cổng MySQL |
| `DB_USER`, `DB_PASSWORD`, `DB_NAME` | Tài khoản và database MySQL |
| `GEMINI_API_KEY` | API key Gemini; không bắt buộc nếu không dùng AI |
| `JWT_SECRET` | Khóa ký token đăng nhập |
| `STAFF_INVITE_CODE`, `ADMIN_INVITE_CODE` | Mã mời đăng ký nhân viên và quản trị viên |

Nếu xóa `may-chu/.env`, chạy lại `CAI_DAT_ELECTROCARE.bat` để tạo cấu hình mới. Không đưa file này lên GitHub.

## Cấu trúc dự án

```text
ElectroCare-GitHub/
├── co-so-du-lieu/       # Script khởi tạo cơ sở dữ liệu
├── giao-dien/           # Giao diện web
├── may-chu/              # API, máy chủ và cấu hình backend
├── CAI_DAT_ELECTROCARE.bat
├── CHAY_ELECTROCARE.bat
└── README.md
```

Ảnh tải lên khi ứng dụng chạy được lưu cục bộ trong `may-chu/tep-tai-len/`, không phải mã nguồn.

## Xử lý sự cố

- **`/api/health` báo `database: false`:** kiểm tra MySQL đã chạy chưa và xác nhận `DB_HOST`, `DB_PORT`, `DB_USER`, `DB_PASSWORD`, `DB_NAME` trong `may-chu/.env`.
- **Cổng 3000 hoặc 5173 đã được sử dụng:** đóng phiên ElectroCare cũ hoặc ứng dụng đang chiếm cổng rồi khởi động lại.
- **Gemini không phản hồi:** kiểm tra `GEMINI_API_KEY`, cấu hình model và hạn mức API của Google AI Studio.
- **Không khởi động được script cài đặt:** xác nhận Node.js/npm đã cài đặt và kiểm tra thông báo lỗi trong cửa sổ lệnh.

## Lưu ý bảo mật

- Tài khoản demo được tạo từ script database có mật khẩu `123456`; chỉ dùng để thử nghiệm cục bộ. Hãy đổi hoặc xóa trước khi dùng dữ liệu thật.
- Không triển khai các tài khoản hoặc cấu hình demo lên môi trường công khai.
- Không chia sẻ `may-chu/.env`, API key Gemini, mật khẩu database, khóa JWT hoặc mã mời.
- Kiểm tra và xác minh thông tin cửa hàng mẫu trước khi sử dụng với khách hàng thật.
