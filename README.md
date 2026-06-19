# JobPortal – Website Tuyển Dụng Việc Làm Trực Tuyến

Website tuyển dụng việc làm trực tuyến xây dựng bằng **ASP.NET Core 8 MVC**, **Entity Framework Core** và **SQL Server**.

## Tính năng

### Người dùng (User)
- Đăng ký / đăng nhập, quản lý hồ sơ cá nhân
- Tìm kiếm và lọc công việc theo ngành, địa điểm, loại hình, kinh nghiệm, mức lương
- Xem chi tiết công việc và thông tin công ty
- Nộp đơn ứng tuyển (upload CV PDF/Word)
- Lưu công việc yêu thích
- Xem trạng thái đơn ứng tuyển
- Thông báo (notification) khi đơn được cập nhật trạng thái

### Quản trị viên (Admin)
- Dashboard với thống kê và biểu đồ Chart.js
- Quản lý người dùng (xem, khóa/mở khóa)
- Quản lý tin tuyển dụng (CRUD, cập nhật trạng thái, nổi bật)
- Quản lý hồ sơ ứng tuyển (xem, cập nhật trạng thái, ghi chú)
- Quản lý danh mục ngành nghề (CRUD)
- Quản lý địa điểm (CRUD)
- Quản lý công ty (CRUD, upload logo)

## Công nghệ

| Thành phần | Phiên bản |
|---|---|
| ASP.NET Core MVC | 8.0 |
| Entity Framework Core | 8.0 |
| SQL Server LocalDB | Latest |
| ASP.NET Core Identity | 8.0 |
| Bootstrap | 5.x |
| Font Awesome | 6.5.0 |
| Chart.js | Latest CDN |

## Cài đặt và chạy

### Yêu cầu
- .NET 8 SDK
- SQL Server LocalDB (đi kèm Visual Studio) hoặc SQL Server Express

### Các bước

1. **Clone hoặc mở project**
   ```bash
   cd JobPortal
   ```

2. **Restore NuGet packages**
   ```bash
   dotnet restore
   ```

3. **Áp dụng migration (tạo database)**
   ```bash
   dotnet ef database update
   ```
   > Database `JobPortalDb` sẽ được tạo tự động trên LocalDB.
   > Dữ liệu mẫu (seed) sẽ được tạo khi chạy ứng dụng lần đầu.

4. **Chạy ứng dụng**
   ```bash
   dotnet run
   ```
   Hoặc nhấn **F5** trong Visual Studio / VS Code.

5. **Truy cập**: `https://localhost:5001` hoặc `http://localhost:5000`

## Tài khoản demo

| Vai trò | Email | Mật khẩu |
|---|---|---|
| Admin | admin@jobportal.com | Admin@123 |
| User | user@jobportal.com | User@123 |

## Cấu trúc project

```
JobPortal/
├── Areas/
│   └── Admin/                  # Khu vực quản trị
│       ├── Controllers/        # Dashboard, Users, Jobs, Applications, Companies, Categories, Locations
│       └── Views/
├── Controllers/                # Home, Account, Jobs, Applications, SavedJobs, Notifications
├── Data/
│   ├── ApplicationDbContext.cs
│   └── DbInitializer.cs        # Seed data
├── Models/                     # ApplicationUser, Job, JobApplication, Company, ...
├── Services/
│   └── FileUploadService.cs    # Upload CV, logo, avatar
├── ViewModels/                 # Account, Jobs, Admin ViewModels
├── Views/                      # Razor Views
│   ├── Shared/
│   │   ├── _Layout.cshtml      # Layout chính
│   │   └── _JobCard.cshtml     # Partial: card công việc
│   ├── Home/
│   ├── Jobs/
│   ├── Account/
│   ├── Applications/
│   ├── SavedJobs/
│   └── Notifications/
└── wwwroot/
    ├── css/
    │   ├── site.css            # CSS chính (blue/navy theme)
    │   └── admin.css           # CSS admin panel
    ├── js/
    └── uploads/                # CV, logo, avatar uploads
```

## Connection String

Trong `appsettings.json`:
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=JobPortalDb;Trusted_Connection=True;MultipleActiveResultSets=true"
}
```
