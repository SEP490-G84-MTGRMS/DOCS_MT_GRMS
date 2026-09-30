# QUY TẮC BẮT BUỘC: GHI WORKLOG MARKDOWN KHI COMMIT CODE

> **Mã quy tắc**: `RULE-01-WORKLOG`  
> **Phạm vi áp dụng**: Cả hai repository `MT_GRMS_BACKEND` và `MT_GRMS_FRONTEND`  
> **Người thực hiện**: Toàn bộ thành viên nhóm SEP490-G84 & Các AI Coding Agents

---

## 1. Mục Đích & Ý Nghĩa

Để loại bỏ hoàn toàn tình trạng:
* Không ai biết ai đang sửa file gì, dẫn đến xung đột khi merge (merge conflicts).
* PM không nắm được tiến độ cụ thể từng ngày.
* Người review PR không hiểu ngữ cảnh và mục đích của các thay đổi code.

$\rightarrow$ **MỌI COMMIT HOẶC PULL REQUEST ĐỀU PHẢI ĐÍNH KÈM 1 FILE MARKDOWN WORKLOG NỘI BỘ**.

---

## 2. Quy Định Đặt Tên & Vị Trí Lưu File Worklog

* **Vị trí bắt buộc**:
  * Tại Backend: `MT_GRMS_BACKEND/docs/worklogs/`
  * Tại Frontend: `MT_GRMS_FRONTEND/docs/worklogs/`
* **Quy ước đặt tên file (Naming Convention)**:
  ```text
  YYYY-MM-DD_FE-<ID>_<AUTHOR>_<NGAN_GON>.md
  ```
  *Ví dụ*:
  * Backend: `2026-10-01_FE-02_DUC_fefo-batch-engine.md`
  * Frontend: `2026-10-02_FE-01_TAM_product-table-component.md`
  * Bug fix: `2026-10-03_BUG-05_NHAT_fix-tenant-filter.md`

---

## 3. Cấu Trúc Nội Dung Bắt Buộc Của File Worklog

Mỗi file worklog phải tuân thủ đúng định dạng sau:

```markdown
# WORKLOG: [FE-xx / BUG-xx] - [Tiêu đề công việc]

- **Ngày thực hiện**: YYYY-MM-DD
- **Người thực hiện (Author)**: [Tên thành viên / AI Agent]
- **Nhánh Git (Branch)**: feat/FE-xx-... hoặc fix/...
- **Mã tính năng liên kết**: [FE-xx](../../DOCS_MT_GRMS/specs/FE-xx/spec.md)
- **Loại thay đổi**: [Feature / Bugfix / Refactor / Architecture]

---

### 1. Mục Đích Thay Đổi (Why)
[Mô tả 1-2 câu giải thích tại sao làm thay đổi này, giải quyết vấn đề gì]

### 2. Danh Sách Tệp Đã Sửa Đổi & Thêm Mới (What)
- `src/.../File1.cs`: [Mô tả sửa gì, thêm method nào]
- `src/.../File2.cs`: [Mô tả thêm class DTO nào]

### 3. Thay Đổi Kỹ Thuật Quan Trọng (Technical Highlights)
- **API Endpoints mới / sửa**:
  - `POST /api/v1/...`: [Mô tả contract]
- **Database / Entities**: [Có thêm cột hay bảng gì không]
- **Breaking Changes**: [Có làm ảnh hưởng đến Frontend hoặc service khác không?]

### 4. Kết Quả Kiểm Thử (Verification)
- [x] Đã chạy `dotnet build` / `npm run build`: Thành công (0 lỗi, 0 cảnh báo).
- [x] Đã chạy `dotnet test` / `npm run test`: Pass.
- [ ] Ảnh chụp màn hình test Swagger hoặc UI (nếu có).

---
### 5. Ghi Chú Dành Cho PM & Reviewer
- [Những điểm cần reviewer lưu ý khi merge]
- [Cần báo team Frontend/Backend đồng bộ endpoint nào]
```

---

## 4. Trách Nhiệm Của PM Khi Duyệt PR

1. Nếu một Pull Request **KHÔNG CÓ** file worklog trong `docs/worklogs/`, PM có quyền **TỪ CHỐI MERGE** ngay lập tức và yêu cầu bổ sung.
2. Sau khi merge PR, PM lấy thông tin tóm tắt từ file worklog này để cập nhật vào [`PM_TRACKING_DASHBOARD.md`](../PM_TRACKING_DASHBOARD.md) và [`INTEGRATION_CHANGELOG.md`](../INTEGRATION_CHANGELOG.md).
