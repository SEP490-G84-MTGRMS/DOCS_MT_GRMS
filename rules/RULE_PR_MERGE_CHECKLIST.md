# QUY TRÌNH & CHECKLIST DUYỆT PULL REQUEST (PR MERGE PROTOCOL)

> **Mã quy tắc**: `RULE-02-PR-MERGE`  
> **Người thực hiện**: Project Manager (PM), Tech Lead & Reviewers

---

## 1. Nguyên Tắc Duyệt PR

* Không ai được commit trực tiếp vào nhánh `main` hoặc `develop`. Mọi thay đổi đều phải đi qua Pull Request (PR).
* PR chỉ được merge khi vượt qua 100% Checklist kỹ thuật và quy trình dưới đây.

---

## 2. Checklist Duyệt PR Dành Cho PM & Reviewer

| STT | Hạng mục kiểm tra | Tiêu chuẩn bắt buộc | Đạt / Không đạt |
|:---:|:---|:---|:---:|
| 1 | **Tài liệu Worklog** | Có file worklog mới trong `docs/worklogs/` theo đúng cú pháp tên và nội dung chuẩn. | [ ] |
| 2 | **Khớp với Spec** | Code hiện thực đúng với bản đặc tả trong `DOCS_MT_GRMS/specs/FE-xx`. | [ ] |
| 3 | **Biên dịch sạch** | Chạy `dotnet build` (BE) hoặc `npm run build` (FE) thành công: **0 Warning, 0 Error**. | [ ] |
| 4 | **Kiểm thử tự động** | Chạy `dotnet test` (BE) hoặc `npm run test` (FE): **100% Passed**. | [ ] |
| 5 | **Không vi phạm kiến trúc** | • BE: Controller không được trỏ vào Domain Entity; chỉ dùng DTO.<br>• FE: Gọi API qua `services/`, không hardcode URL trong component. | [ ] |
| 6 | **Xung đột mã nguồn** | Không có Git merge conflicts với nhánh đích (`develop`). | [ ] |

---

## 3. Các Bước Cần Làm Sau Khi Merge PR

Sau khi PM bấm nút **Merge Pull Request** trên GitHub:

1. **Cập nhật Bảng Tiến độ PM**:
   * Mở file [`PM_TRACKING_DASHBOARD.md`](../PM_TRACKING_DASHBOARD.md).
   * Chuyển trạng thái tính năng sang `In Review` hoặc `Merged / Completed`.
   * Gắn link dẫn đến file worklog vừa merge.
2. **Cập nhật Nhật ký Tích hợp Hệ thống**:
   * Mở file [`INTEGRATION_CHANGELOG.md`](../INTEGRATION_CHANGELOG.md).
   * Ghi nhận các Endpoint mới, breaking changes, hoặc trạng thái sẵn sàng tích hợp để team còn lại (BE/FE) biết và kết nối.
3. **Thông báo cho Team**:
   * Thông báo ngắn gọn trên kênh chat nhóm (Discord / Zalo) để các thành viên khác rebase nhánh của họ.
