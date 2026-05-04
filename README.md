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

## 🎨 Design Patterns Được Sử Dụng

Ứng dụng áp dụng nhiều design pattern hiện đại để đảm bảo code sạch, dễ bảo trì và mở rộng:

### 1. **N-Tier Architecture Pattern**
- Tách biệt rõ ràng giữa các lớp (GUI, BUS, DAL, DTO)
- Giảm sự phụ thuộc giữa các thành phần
- Dễ dàng kiểm thử (testing) từng lớp

**Ví dụ:**
```csharp
// GUI gọi BUS
LeagueBUS bus = new LeagueBUS();
List<LeagueDTO> leagues = bus.GetAllLeagues();

// BUS gọi DAL
public List<LeagueDTO> GetAllLeagues()
{
    LeagueDAL dal = new LeagueDAL();
    return dal.GetAllLeagues();
}
```

### 2. **Factory Pattern** 🏭
- **Vị trí**: `GUI/Cruds/CrudFactory.cs`
- Tạo các object CRUD phù hợp dựa trên kiểu dữ liệu
- Giảm sự phụ thuộc trực tiếp vào các class cụ thể

**Ví dụ:**
```csharp
public static class CrudFactory
{
    public static ICrud CreateCrud(string type, DataGridView dgv)
    {
        switch (type)
        {
            case "League":
                return new LeagueCrud(dgv);
            case "Team":
                return new TeamCrud(dgv);
            case "Referee":
                return new RefereeCrud(dgv);
            default:
                throw new ArgumentException("Invalid CRUD type");
        }
    }
}
```

### 3. **Strategy Pattern** 📋
- **Vị trí**: `GUI/Cruds/ICrud.cs` interface
- Định nghĩa giao diện chung cho các chiến lược CRUD
- Các class khác nhau implement ICrud với cách riêng

**Ví dụ:**
```csharp
public interface ICrud
{
    void LoadData();
    void Insert();
    void Update();
    void Delete();
    void Export();
    void Search(string searchText);
}

// Mỗi class (LeagueCrud, TeamCrud, RefereeCrud) implement ICrud
// với logic riêng cho từng entity
```

### 4. **Singleton Pattern** 🔒
- **Vị trí**: `BUS/Managers/DbConfigManager.cs`
- Quản lý kết nối database duy nhất
- Đảm bảo chỉ một instance của manager tồn tại

**Ví dụ:**
```csharp
public static class DbConfigManager
{
    private static string _connStr;
    
    static DbConfigManager()
    {
        // Load và test kết nối một lần duy nhất
        LoadAndTest();
    }
    
    public static string GetConnectionString() => _connStr;
}
```

### 5. **Data Access Object (DAO) Pattern** 🗄️
- **Vị trí**: `DAL/*.DAL.cs`
- Tách biệt logic truy cập dữ liệu khỏi business logic
- Centralized CRUD operations

**Ví dụ:**
```csharp
public class LeagueDAL
{
    public List<LeagueDTO> GetAllLeagues() { }
    public LeagueDTO GetLeagueById(string id) { }
    public bool InsertLeague(LeagueDTO league) { }
    public bool UpdateLeague(LeagueDTO league) { }
    public bool DeleteLeague(string id) { }
}
```

### 6. **Data Transfer Object (DTO) Pattern** 📦
- **Vị trí**: `DTO/*.DTO.cs`
- Chuyển dữ liệu giữa các lớp
- Giảm sự phụ thuộc vào các model của database

**Ví dụ:**
```csharp
public class LeagueDTO
{
    public string LeagueID { get; set; }
    public string LeagueName { get; set; }
    public string LogoURL { get; set; }
    public byte MaxTeams { get; set; }
    public DateTime StartDate { get; set; }
    public DateTime EndDate { get; set; }
    public byte Status { get; set; }
}
```

### 7. **Manager Pattern** 👔
- **Vị trí**: `BUS/Managers/`
- Tập trung các chức năng quản lý cụ thể
- Xử lý logic phức tạp và orchestration

**Ví dụ:**
```csharp
// DbConfigManager - quản lý cấu hình DB
// MatchManager - xử lý logic tạo và quản lý trận đấu
public class MatchManager
{
    public void CreateSchedule(LeagueDTO league) { }
    public void AssignStadium(MatchDTO match, string stadiumId) { }
    public void AssignReferee(MatchDTO match, string refereeId) { }
}
```

### 8. **Helper/Utility Pattern** 🛠️
- **Vị trí**: `BUS/Helpers/`, `GUI/Helpers/`
- Chứa các hàm tiện ích và hỗ trợ
- Tái sử dụng code chung

**Ví dụ:**
```csharp
public class IDGenerator
{
    public static string GenerateID(string prefix)
    {
        // Tạo ID duy nhất với prefix
        return prefix + DateTime.Now.Ticks.ToString();
    }
}
```

### 9. **Template Method Pattern** 📄
- **Vị trị**: Form base classes
- Định nghĩa cấu trúc chung cho các form
- Các form con override các phương thức cụ thể

### Lợi Ích Của Design Patterns Này

| Pattern | Lợi Ích |
|---------|---------|
| N-Tier | Tách biệt concern, dễ bảo trì |
| Factory | Linh hoạt tạo object, giảm coupling |
| Strategy | Dễ mở rộng, thay thế chiến lược |
| Singleton | Quản lý resource duy nhất |
| DAO | Tập trung truy cập dữ liệu |
| DTO | Rõ ràng cấu trúc dữ liệu |
| Manager | Xử lý logic phức tạp |
| Helper | Tái sử dụng code |

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

### 2. Mở Project

1. Mở `FootballScheduler.sln` trong Visual Studio
2. Restore NuGet packages
3. Build solution (Ctrl + Shift + B)
4. Chạy ứng dụng (F5)

### 3. Đăng Nhập

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

##  Cảm Ơn

- Cảm ơn các thư viện mã nguồn mở được sử dụng trong dự án
- Cảm ơn các đóng góp từ cộng đồng

---

**Truy cập thường xuyên để cập nhật phiên bản mới nhất!** 🚀