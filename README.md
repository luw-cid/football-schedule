# ⚽ Football Scheduler - Ứng Dụng Lập Lịch Bóng Đá

![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=csharp&logoColor=white)
![.NET Framework](https://img.shields.io/badge/.NET%20Framework-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white)
![Windows Forms](https://img.shields.io/badge/Windows%20Forms-0078D4?style=flat-square&logo=windows&logoColor=white)

## 📋 Giới Thiệu

**Football Scheduler** là ứng dụng quản lý và lập lịch bóng đá chuyên nghiệp dành cho các giải đấu bóng đá. Ứng dụng được xây dựng bằng C# với giao diện Windows Forms, cung cấp các tính năng toàn diện để quản lý các đội bóng, giải đấu, trận đấu, và lịch thi đấu.

### ✨ Tính Năng Chính

- 🏆 **Quản lý Giải Đấu** - Tạo và quản lý các giải bóng đá
- 👥 **Quản lý Đội Bóng** - Quản lý thông tin các đội tham gia giải đấu
- 📅 **Lập Lịch Thi Đấu** - Tự động tạo lịch trận đấu
- 🏟️ **Quản lý Sân Vận Động** - Quản lý các sân vận động phục vụ cho các trận đấu
- 👨‍⚖️ **Quản lý Trọng Tài** - Quản lý đội ngũ trọng tài
- 📊 **Xếp Hạng Giải Đấu** - Hiển thị bảng xếp hạng và thống kê
- 🔐 **Hệ Thống Xác Thực** - Đăng nhập với các vai trò khác nhau (Admin, Referee, Team)
- 🔒 **Bảo Mật** - Mã hóa mật khẩu, phân quyền người dùng

## 🏗️ Kiến Trúc Ứng Dụng

Ứng dụng được xây dựng theo **mô hình N-tier architecture** gồm 4 tầng:

```
┌─────────────────────────────────────────┐
│  GUI (Presentation Layer)               │
│  - Windows Forms                        │
│  - Giao diện người dùng                 │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  BUS (Business Logic Layer)             │
│  - Xử lý logic nghiệp vụ                │
│  - Validation, tính toán                │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  DAL (Data Access Layer)                │
│  - Truy cập dữ liệu từ DB               │
│  - CRUD operations                      │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  DTO (Data Transfer Objects)            │
│  - Đối tượng chuyển dữ liệu             │
│  - Định nghĩa cấu trúc dữ liệu         │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│  SQL Server Database                    │
│  - Lưu trữ dữ liệu                      │
└─────────────────────────────────────────┘
```

### 📁 Cấu Trúc Thư Mục

```
FootballScheduler/
├── GUI/                    # Tầng giao diện
│   ├── Forms/             # Các form chính
│   ├── Cruds/             # Các trang CRUD
│   ├── CustomUI/          # Tùy chỉnh giao diện
│   └── UserControls/      # User controls
├── BUS/                    # Tầng logic nghiệp vụ
│   ├── BUSs/              # Các lớp xử lý business
│   ├── Managers/          # Các manager
│   └── Helpers/           # Hàm trợ giúp
├── DAL/                    # Tầng truy cập dữ liệu
│   └── *.DAL.cs           # Các lớp DAL
├── DTO/                    # Tầng đối tượng dữ liệu
│   └── *.DTO.cs           # Các lớp DTO
└── FootballScheduler.sln   # Solution file
```

## 🚀 Các Đối Tượng Chính

### 1. **League (Giải Đấu)**
- Quản lý các giải bóng đá
- Theo dõi trạng thái: chưa lên lịch, đã lên lịch, đã kết thúc
- Giới hạn số đội tham gia

### 2. **Team (Đội Bóng)**
- Thông tin đội bóng
- Đội logo
- Các cầu thủ thuộc đội

### 3. **Match (Trận Đấu)**
- Lịch các trận đấu
- Thông tin đối phương
- Trọng tài phụ trách
- Địa điểm thi đấu

### 4. **Stadium (Sân Vận Động)**
- Thông tin sân vận động
- Địa chỉ, công suất

### 5. **Referee (Trọng Tài)**
- Quản lý đội ngũ trọng tài
- Gán trọng tài cho các trận đấu

### 6. **Account (Tài Khoản)**
- Xác thực người dùng
- Phân quyền: Admin, Referee, Team

## 💻 Yêu Cầu Hệ Thống

### Yêu Cầu Phát Triển
- **Visual Studio 2022** trở lên
- **.NET Framework 4.7.2** trở lên
- **SQL Server 2019** trở lên (hoặc SQL Server Express)

### Công Nghệ Sử Dụng
- **C#** - Ngôn ngữ lập trình
- **Windows Forms** - Framework giao diện
- **SQL Server** - Cơ sở dữ liệu
- **Dapper** - ORM lightweight
- **iTextSharp** - Tạo file PDF
- **Guna UI 2** - Thư viện giao diện đẹp
- **BouncyCastle** - Mã hóa/Giải mã
- **FontAwesome.Sharp** - Icon library

## 📦 Cài Đặt và Triển Khai

### 1. Chuẩn Bị Cơ Sở Dữ Liệu

```sql
-- Mở SQL Server Management Studio và chạy script:
-- FootballSchedulerDB.sql - Tạo cơ sở dữ liệu
-- SampleData.sql - Thêm dữ liệu mẫu
```

### 2. Cấu Hình Kết Nối Database

Chỉnh sửa file `app.config` trong các project (GUI, BUS, DAL):

```xml
<connectionStrings>
    <add name="FootballSchedulerDB" 
         connectionString="Server=YOUR_SERVER;Database=FootballScheduler;User Id=sa;Password=YOUR_PASSWORD;" 
         providerName="System.Data.SqlClient" />
</connectionStrings>
```

### 3. Mở Project

1. Mở `FootballScheduler.sln` trong Visual Studio
2. Restore NuGet packages
3. Build solution (Ctrl + Shift + B)
4. Chạy ứng dụng (F5)

### 4. Đăng Nhập

Sau khi cài dữ liệu mẫu, sử dụng thông tin đăng nhập:
- **Username**: admin
- **Password**: 123456 (mặc định)

## 🔑 Các Vai Trò Người Dùng

### 👨‍💼 Admin
- Toàn quyền quản lý hệ thống
- Quản lý tất cả người dùng
- Lập lịch thi đấu
- Quản lý giải đấu, đội, trọng tài, sân vận động

### 👨‍⚖️ Referee (Trọng Tài)
- Xem lịch trận đấu của mình
- Xem thông tin các trận đấu

### 👥 Team (Đội Bóng)
- Xem thông tin giải đấu
- Xem lịch thi đấu của đội
- Xem bảng xếp hạng

## 🗄️ Cơ Sở Dữ Liệu

### Các Bảng Chính

| Bảng | Mô Tả |
|------|-------|
| **League** | Thông tin giải đấu |
| **Team** | Thông tin đội bóng |
| **Match** | Thông tin trận đấu |
| **Stadium** | Thông tin sân vận động |
| **Referee** | Thông tin trọng tài |
| **Account** | Thông tin tài khoản người dùng |
| **LeagueTeam** | Mối quan hệ giữa giải và đội |
| **Standings** | Bảng xếp hạng |

## 🔧 Các Tính Năng Chính

### Quản Lý Giải Đấu
- ✅ Thêm giải đấu mới
- ✅ Chỉnh sửa thông tin giải
- ✅ Xóa giải đấu
- ✅ Xem danh sách giải

### Quản Lý Đội Bóng
- ✅ Thêm đội vào giải
- ✅ Xóa đội khỏi giải
- ✅ Quản lý thông tin đội

### Lập Lịch Thi Đấu
- ✅ Tự động tạo lịch đấu vòng tròn
- ✅ Gán sân vận động
- ✅ Gán trọng tài

### Quản Lý Trọng Tài
- ✅ Thêm trọng tài
- ✅ Chỉnh sửa thông tin
- ✅ Gán cho trận đấu

### Bảng Xếp Hạng
- ✅ Xem bảng xếp hạng theo trận đấu
- ✅ Tính toán điểm tự động
- ✅ Hiển thị thống kê

## 📝 Ví Dụ Sử Dụng

### Quy Trình Tạo Giải Đấu

1. **Đăng nhập** với tài khoản Admin
2. **Tạo Giải**: Chọn "Quản lý Giải" → "Thêm giải"
3. **Thêm Đội**: Chọn giải → "Thêm đội" → Chọn các đội tham gia
4. **Tạo Lịch**: Chọn "Lập Lịch" → Chọn giải → "Tạo lịch"
5. **Xem Kết Quả**: Xem bảng xếp hạng và lịch trận

## 🐛 Báo Cáo Lỗi và Đề Xuất

Nếu bạn tìm thấy lỗi hoặc có đề xuất cải tiến, vui lòng:
- Tạo **Issue** trên GitHub
- Mô tả chi tiết vấn đề
- Cung cấp các bước tái hiện lỗi

## 📄 License

Dự án này được phát hành dưới giấy phép **MIT License**. Xem file [LICENSE](LICENSE) để biết chi tiết.

## 👨‍💻 Tác Giả

Developed by the Football Scheduler Team

## 🙏 Cảm Ơn

- Cảm ơn các thư viện mã nguồn mở được sử dụng trong dự án
- Cảm ơn các đóng góp từ cộng đồng

---

**Truy cập thường xuyên để cập nhật phiên bản mới nhất!** 🚀