# 系所資源預約與未來職業統計之學生平台-ScholaLink

使用 **ASP.NET Core 6.0 MVC** 開發綜合性學生資源管理平台。該系統旨在提供學生便捷的資源預約、職涯資訊分享以及助教(TA)諮詢預約服務，並整合了Line Notify通知功能。

## 核心功能

*   **教室預約系統 (Classroom Reservation)**：查看教室資訊、線上申請預約、管理預約紀錄。
*   **助教預約系統 (TA Appointment)**：預約助教諮詢時間、查看預約狀態與回饋。
*   **職涯與實習分享 (Career & Internship)**：分享實習心得、查看徵才資訊、職涯數據(Echarts)。
*   **個人資訊管理 (Member Center)**：登入管理、收藏職涯資訊、追蹤個人預約。
*   **Line Notify整合**：即時推送預約相關通知。

## 使用技術

*   **Framework**: .NET6.0(ASP.NET Core MVC)
*   **Database**: MySQL/MariaDB
*   **ORM**: Entity Framework Core
*   **Frontend**: 
    *   HTML5/CSS3
    *   JavaScript/jQuery
    *   Echarts
*   **Other Tools**:
    *   ClosedXML/OpenXml
    *   X.PagedList
    *   Line Notify API

## 環境準備

在開始之前，請確保您的環境中已安裝以下工具：
1.  [.NET 6.0 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
2.  [MySQL Server](https://dev.mysql.com/downloads/installer/) (或 MariaDB)
3.  IDE: Visual Studio 2022 或 VS Code

## 執行步驟

### 1. 資料庫設定
1.  開啟 `appsettings.json` 文件。
2.  修改 `ConnectionStrings` 中的 `MySqlConnection`，填入MySQL伺服器資訊Server,Port,Database,User,Password

```json
"ConnectionStrings": {
  "MySqlConnection": "Server=127.0.0.1;Port=3306;Database=student_web;User=您的帳號;Password=您的密碼;"
}
```

### 2.更新資料庫

專案包含多個 DbContext，請依照順序執行以下指令來建立資料庫表：

```bash
# 1.建立核心功能表 (實習/會員)
dotnet ef database update --context ApplicationDbContext

# 2.建立教室預約表
dotnet ef database update --context ClassroomDbContext

# 3.建立 TA 預約表
dotnet ef database update --context TADbContext
```

### 3.設定資料保護金鑰

專案預設將資料保護金鑰存放在 `C:/Student_web/DataProtectionKeys/`。請手動建立此資料夾，或在 `Program.cs`中修改路徑：

```csharp
// Program.cs
builder.Services.AddDataProtection()
    .PersistKeysToFileSystem(new DirectoryInfo("您的自定義路徑"));
```

### 4.啟動專案

在專案根目錄執行：

```bash
dotnet run
```

啟動後，開啟瀏覽器訪問 `https://localhost:7193` (或終端機顯示的其他通訊埠)。

## 專案結構說明
*   `Controllers/`: 處理業務邏輯與請求導向。
*   `Models/`: 定義資料實體與 ViewModel。
*   `Views/`: UI 頁面 (Razor Pages)。
*   `Data/`: DbContext 與資料庫遷移紀錄。
*   `wwwroot/`: 存放靜態資源 (CSS, JS, Images)。
*   `Services/`: 第三方服務整合 (如 Line Notify)。
---