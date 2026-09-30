# INTEGRATION CHANGELOG (NHẬT KÝ TÍCH HỢP HỆ THỐNG TOÀN DIỆN)

> **Dự án**: Multi-Tenant Grocery Retail Management System (MT-GRMS)  
> **Người cập nhật**: Project Manager (PM)  
> **Mục đích**: Ghi nhận các mốc tích hợp giữa Backend ASP.NET Core và Frontend React SPA, danh sách API contracts đã kích hoạt và các thay đổi quan trọng (breaking changes).

---

## [v0.1.0-alpha] - 2026-09-30 (Initial Architecture & Code-First Skeleton)

### 📌 Backend Changes
- Thiết lập kiến trúc Clean Architecture 4 tầng (.NET 8): `Domain`, `Application`, `Infrastructure`, `Api`.
- Áp dụng nguyên tắc đóng gói: Controller không được trỏ vào Domain Entity, chỉ giao tiếp 100% bằng DTO.
- Thiết lập mẫu chuẩn Code-First với Fluent API Configuration cho `products` table (`ProductConfiguration.cs`).
- Khắc phục lỗi `Global Query Filter` đa người thuê (Multi-Tenancy) trong `AppDbContext.cs`.
- Cung cấp module mẫu chuẩn `Catalog`: `ICatalogService`, `CatalogService`, `ProductsController`.
- **Worklog liên kết**: [`MT_GRMS_BACKEND/docs/worklogs/2026-09-30_INIT_ARCH_skeleton-setup.md`](../MT_GRMS_BACKEND/docs/worklogs/2026-09-30_INIT_ARCH_skeleton-setup.md)

### 📌 Frontend Contract Ready
- Endpoints sẵn sàng cho Frontend kết nối:
  - `GET /api/v1/health` $\rightarrow$ Trả trạng thái Healthy
  - `GET /api/v1/products` $\rightarrow$ Lấy danh sách sản phẩm (DTO `ProductResponse`)
  - `GET /api/v1/products/{id}` $\rightarrow$ Chi tiết sản phẩm
  - `POST /api/v1/products` $\rightarrow$ Thêm mới sản phẩm (Body: `ProductCreateRequest`)
- Định dạng dữ liệu phản hồi chuẩn: `ApiResponse<T>` (`{ success: bool, data: T, message: string, errorCode: string }`).
