# ĐẶC TẢ TÍNH NĂNG KỸ THUẬT: FE-02 - QUẢN LÝ LÔ HÀNG & HẠN DÙNG THEO FEFO
## (SPEC-FIRST IMPLEMENTATION SPECIFICATION)

> **Mã tính năng**: `FE-02`  
> **Tên tính năng**: Quản lý Lô Hàng & Xuất Kho theo Hạn Sử Dụng (Batch & Expiry Date FEFO)  
> **Người thực hiện**: Đặng Đỗ Minh Đức (Backend Lead)  
> **Người phản biện**: Nguyễn Long Nhật (Tech Lead), Nguyễn Minh Tâm (BA)  
> **Vòng lặp phát triển**: Code Iteration 1 (Tuần 6 – Tuần 7)  
> **Tài liệu căn cứ**: [Report-4_Software_Design_Specification.md](../../../Document/report/Report-4_Software_Design_Specification.md) & [DO_AN_CSHARP_REACT_FRAMEWORK.md](../../DO_AN_CSHARP_REACT_FRAMEWORK.md)

---

## 1. PROPOSAL (ĐỀ XUẤT)

### 1.1 Vấn đề (Problem)
Cửa hàng tạp hóa truyền thống và siêu thị mini thường xuyên chịu tổn thất lớn do hàng hóa hết hạn sử dụng trên kệ mà nhân viên không biết. Khi bán hàng, thu ngân thường lấy sản phẩm ngẫu nhiên thay vì ưu tiên các lô cận date trước, dẫn đến việc hàng cũ bị dồn lại phía sau kệ và hư hỏng.

### 1.2 Giải pháp Đề xuất (Solution)
- Áp dụng nguyên tắc **FEFO (First-Expired, First-Out)**: Hệ thống tự động truy vấn và phân bổ các lô hàng có hạn sử dụng gần nhất (`ExpiryDate ASC`) khi bán lẻ tại quầy POS hoặc xuất chuyển kho.
- Cảnh báo trực quan 3 mức màu:
  - **ĐỎ (Critical)**: Còn $\le 7$ ngày $\rightarrow$ Báo động đỏ, kích hoạt thanh lý 50%.
  - **CAM (High)**: Còn 8 – 15 ngày $\rightarrow$ Nhãn cam, ưu tiên xuất lên kệ đầu.
  - **VÀNG (Warning)**: Còn 16 – 30 ngày $\rightarrow$ Nhãn vàng, đưa vào danh sách theo dõi.
- Cung cấp tính năng truy xuất nguồn gốc lô hàng (Batch Traceability) từ khâu Nhập kho (PO) $\rightarrow$ Tồn kho $\rightarrow$ Bán lẻ (Hóa đơn).

### 1.3 Phạm vi (Scope)
- **Trong phạm vi (In-Scope)**:
  - Quản lý thông tin lô: Số lô (BatchCode), ngày sản xuất (MFG), hạn dùng (EXP), số lượng ban đầu, số lượng khả dụng.
  - API `AllocateBatchesFefoAsync` phục vụ đơn hàng POS.
  - Background Job quét lô cận date định kỳ gửi cảnh báo.
  - Giao diện Dashboard cảnh báo lô hạn và Stepper timeline luân chuyển lô hàng.
- **Ngoài phạm vi (Out-of-Scope trong Iteration 1)**:
  - Tự động áp dụng mã giảm giá thanh lý tại POS (sẽ hoàn thiện tại Sprint 2 trong `FE-16`).

---

## 2. SPEC (KỊCH BẢN BDD KIỂM CHỨNG GIVEN - WHEN - THEN)

#### Scenario 1: Xuất kho tự động ưu tiên Lô có hạn sử dụng gần nhất (FEFO Happy Path)
- **GIVEN**: Chi nhánh Cầu Giấy có sản phẩm "Sữa chua Ba Vì" gồm 2 lô tồn kho:
  - Lô `LOT-A`: Hạn sử dụng `2026-10-30`, tồn khả dụng `10` hộp.
  - Lô `LOT-B`: Hạn sử dụng `2026-11-15`, tồn khả dụng `20` hộp.
- **WHEN**: Thu ngân quét bán `5` hộp "Sữa chua Ba Vì" tại quầy POS.
- **THEN**:
  - Hệ thống tự động gán Lô `LOT-A` vào giỏ hàng.
  - Số lượng yêu cầu `5` hộp được phân bổ hoàn toàn từ Lô `LOT-A`.
  - Tồn kho của Lô `LOT-A` sau giao dịch giảm còn `5` hộp, Lô `LOT-B` giữ nguyên `20` hộp.

#### Scenario 2: Phân bổ qua nhiều Lô khi Lô cận date nhất không đủ số lượng (Split Allocation)
- **GIVEN**: Chi nhánh có sản phẩm gồm 2 lô:
  - Lô `LOT-01`: Hạn `2026-10-25`, tồn khả dụng `3` gói.
  - Lô `LOT-02`: Hạn `2026-11-05`, tồn khả dụng `10` gói.
- **WHEN**: Khách mua `5` gói sản phẩm.
- **THEN**:
  - Hệ thống phân bổ `3` gói từ Lô `LOT-01` (hết sạch tồn lô này).
  - Phân bổ tiếp `2` gói từ Lô `LOT-02`.
  - Hóa đơn sinh 2 dòng chi tiết thể hiện rõ nguồn gốc từng lô.

#### Scenario 3: Từ chối xuất kho khi lô hàng đã hết hạn sử dụng (Expired Protection)
- **GIVEN**: Lô `LOT-OLD` có `ExpiryDate` nhỏ hơn thời điểm hiện tại (`DateTime.UtcNow`).
- **WHEN**: Hệ thống chạy thuật toán phân bổ FEFO cho đơn hàng mới.
- **THEN**:
  - Hệ thống bỏ qua Lô `LOT-OLD`, không cho phép gán vào đơn hàng.
  - Nếu toàn bộ các lô đều quá hạn, ném ngoại lệ `BusinessException(ErrorCodes.BatchExpired, "Sản phẩm đã hết hạn sử dụng, không thể xuất bán")`.
  - Trả về mã lỗi HTTP 422.

---

## 3. DESIGN (THIẾT KẾ KỸ THUẬT)

### 3.1 Thực thể Cơ sở Dữ liệu (`Batches` & `StockOnHand`)
```csharp
// MTGRMS.Domain/Entities/Inventory/Batch.cs
public class Batch : BaseTenantEntity
{
    public Guid ProductId { get; set; }
    public Guid BranchId { get; set; }
    public string BatchCode { get; set; } = null!;
    public DateTime ManufactureDate { get; set; }
    public DateTime ExpiryDate { get; set; }
    public decimal InitialQuantity { get; set; }
    public decimal LandedCostPerUnit { get; set; }

    public Product Product { get; set; } = null!;
    public StockOnHand StockOnHand { get; set; } = null!;
}

// MTGRMS.Domain/Entities/Inventory/StockOnHand.cs
public class StockOnHand : BaseTenantEntity
{
    public Guid BranchId { get; set; }
    public Guid ProductId { get; set; }
    public Guid BatchId { get; set; }
    public decimal Quantity { get; set; }
    public decimal ReservedQuantity { get; set; }
    public decimal AvailableQuantity => Quantity - ReservedQuantity;

    public Batch Batch { get; set; } = null!;
}
```

### 3.2 Endpoint RESTful API
- `GET /api/v1/batches/product/{productId}?branchId={branchId}` $\rightarrow$ Lấy danh sách lô theo sản phẩm (có sắp xếp theo hạn dùng).
- `POST /api/v1/batches/fefo/allocate` $\rightarrow$ Thuật toán phân bổ lô FEFO cho giỏ hàng.
- `GET /api/v1/batches/alerts/near-expiry?days=30` $\rightarrow$ Danh sách lô sắp hết hạn cần thanh lý.

---

## 4. TASKS CHECKLIST (CHECKLIST CÔNG VIỆC CỤ THỂ)

- [ ] **Database & Persistence**:
  - [ ] `MTGRMS.Domain/Entities/Inventory/Batch.cs` (Kế thừa `BaseTenantEntity`)
  - [ ] `MTGRMS.Infrastructure/Persistence/Configurations/BatchConfiguration.cs` (Đánh B-Tree Index trên `ExpiryDate` và `TenantId`)
  - [ ] Chạy migration `dotnet ef migrations add AddBatchAndStockOnHandTables`
- [ ] **Application Logic**:
  - [ ] `MTGRMS.Application/Batches/IFefoEngine.cs`
  - [ ] `MTGRMS.Application/Batches/FefoEngine.cs` (Cài đặt thuật toán phân bổ và đánh giá mức rủi ro Đỏ/Cam/Vàng)
  - [ ] `MTGRMS.Application/Batches/Dtos/BatchResponseDto.cs`
  - [ ] `MTGRMS.UnitTests/Batches/FefoEngineTests.cs` (Kiểm thử 3 Scenarios trên)
- [ ] **API Controller**:
  - [ ] `MTGRMS.WebApi/Controllers/BatchesController.cs` (Controller mỏng, trả `ApiResponse<T>`)
- [ ] **Frontend React**:
  - [ ] `frontend/src/features/batches/api.ts`
  - [ ] `frontend/src/features/batches/hooks.ts` (Dùng TanStack Query `useQuery`)
  - [ ] `frontend/src/features/batches/components/NearExpiryBadge.tsx` (Màu Đỏ/Cam/Vàng)
  - [ ] `frontend/src/features/batches/pages/NearExpiryDashboardPage.tsx`
- [ ] **Hoàn tất & Kiểm tra**:
  - [ ] `dotnet test` vượt qua 100%
  - [ ] Kiểm thử luồng xuất kho tự động gán đúng lô có date gần nhất
