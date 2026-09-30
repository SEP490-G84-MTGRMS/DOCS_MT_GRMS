# BẢN MẪU ĐẶC TẢ TÍNH NĂNG THEO CHUẨN "SPEC TRƯỚC, CODE SAU"
## (THAM KHẢO TỪ MỤC 8 - DO_AN_CSHARP_REACT_FRAMEWORK.MD)

> **Mã tính năng**: `FE-XX`  
> **Tên tính năng**: `[Tên tính năng tiếng Việt / tiếng Anh]`  
> **Người thực hiện (In-Charge)**: `[Tên thành viên]`  
> **Người duyệt (Reviewer)**: `[Tên thành viên]`  
> **Sprint dự kiến**: `[Sprint 1 / Sprint 2 / Sprint 3]`

---

## 1. PROPOSAL (ĐỀ XUẤT TÍNH NĂNG)

### 1.1 Vấn đề cần giải quyết (Problem Statement)
- *Mô tả ngắn gọn nỗi đau của người dùng (chủ tiệm, thu ngân hoặc khách mua hàng) khi chưa có tính năng này.*

### 1.2 Giải pháp đề xuất (Proposed Solution)
- *Tóm tắt cách giải quyết và giá trị nghiệp vụ mang lại.*

### 1.3 Phạm vi công việc (Scope)
- **Trong phạm vi (In Scope)**:
  - [x] Chức năng A...
  - [x] Chức năng B...
- **Ngoài phạm vi (Out of Scope)**:
  - [ ] Chức năng chưa làm trong Sprint này...

---

## 2. SPEC (KỊCH BẢN KIỂM CHỨNG BDD: GIVEN - WHEN - THEN)

### Scenario 1: [Tên kịch bản luồng chính thành công]
- **GIVEN**: [Tiền điều kiện dữ liệu ban đầu, ví dụ: Người dùng đã đăng nhập với vai trò Thu ngân, trong kho có sẵn lô hàng X].
- **WHEN**: [Hành động kích hoạt, ví dụ: Quét mã vạch sản phẩm Y tại quầy POS].
- **THEN**: [Kết quả mong đợi, ví dụ: Hệ thống tự động gán lô X có hạn dùng sớm nhất vào giỏ hàng và hiển thị đúng giá bán].

### Scenario 2: [Tên kịch bản ngoại lệ / chặn lỗi nghiệp vụ]
- **GIVEN**: [Ví dụ: Sản phẩm trong kho đã hết hàng tồn khả dụng].
- **WHEN**: [Ví dụ: Bấm nút xác nhận thanh toán].
- **THEN**: [Ví dụ: Hệ thống trả mã lỗi HTTP 422 kèm mã lỗi INSUFFICIENT_STOCK và thông báo lỗi rõ ràng trên UI].

---

## 3. DESIGN (THIẾT KẾ KỸ THUẬT)

### 3.1 Thiết kế Cơ sở Dữ liệu & Migrations
- **Bảng ảnh hưởng / Bảng mới**: `tên_bảng`
- **Các cột chính**:
  - `id`: UUID (Primary Key)
  - `tenant_id`: string (Indexed - Multi-tenant)
  - `...`: Kiểu dữ liệu
- **Tên Migration EF Core**: `Add[FeatureName]Table`

### 3.2 Thiết kế API RESTful
- **Endpoint**: `METHOD /api/v1/[resource]`
- **Header**: `Authorization: Bearer <token>`
- **Request Body DTO**:
  ```json
  {
    "field1": "value",
    "field2": 100
  }
  ```
- **Response Wrapper (`ApiResponse<T>`)**:
  ```json
  {
    "success": true,
    "message": "Xử lý thành công",
    "errorCode": null,
    "data": { }
  }
  ```

---

## 4. TASKS CHECKLIST (DANH MỤC ĐẦU VIỆC & CÁC FILE SỬA ĐỔI)

- [ ] **Backend - Database & Entities**:
  - [ ] Tạo Entity `[EntityName].cs` tại `backend/src/MTGRMS.Domain/Entities/...`
  - [ ] Tạo `[EntityName]Configuration.cs` tại `backend/src/MTGRMS.Infrastructure/Persistence/Configurations/`
  - [ ] Chạy `dotnet ef migrations add Add[Feature] -p ...`
- [ ] **Backend - Application Logic**:
  - [ ] Tạo DTOs trong `backend/src/MTGRMS.Application/[Feature]/Dtos/`
  - [ ] Tạo Validator trong `backend/src/MTGRMS.Application/[Feature]/Validators/`
  - [ ] Viết Service `[Feature]Service.cs` xử lý nghiệp vụ
  - [ ] Viết Unit Test `[Feature]ServiceTests.cs` đạt coverage $\ge 70\%$
- [ ] **Backend - API & Middleware**:
  - [ ] Tạo Controller `[Feature]Controller.cs` tại `backend/src/MTGRMS.WebApi/Controllers/`
  - [ ] Đăng ký DI trong `DependencyInjection.cs`
- [ ] **Frontend - Client UI**:
  - [ ] Khai báo kiểu TypeScript trong `frontend/src/features/[feature]/types.ts`
  - [ ] Viết API client trong `frontend/src/features/[feature]/api.ts`
  - [ ] Viết Custom Hook (TanStack Query) trong `frontend/src/features/[feature]/hooks.ts`
  - [ ] Xây dựng giao diện trang `[Feature]Page.tsx`
- [ ] **Verify & Definition of Done**:
  - [ ] `dotnet test` toàn bộ PASS
  - [ ] `npm run build` không báo lỗi kiểu TypeScript
  - [ ] Đối soát lại toàn bộ kịch bản Scenario trong mục 2
