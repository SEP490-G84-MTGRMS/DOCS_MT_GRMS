# QUY CHẾ QUẢN TRỊ 3 REPO DỰ ÁN MT-GRMS (AGENT INSTRUCTIONS)

Tất cả các AI Agents và Developer khi làm việc trên dự án MT-GRMS bắt buộc phải tuân thủ quy chế 3 repo:

## 1. Cấu Trúc 3 Repo:
- `DOCS_MT_GRMS`: Chứa tài liệu tổng quan, rules, specs (FE-01 đến FE-26), và bảng quản trị PM (`PM_TRACKING_DASHBOARD.md`).
- `MT_GRMS_BACKEND`: Mã nguồn ASP.NET Core 8 Clean Architecture & Code-First.
- `MT_GRMS_FRONTEND`: Mã nguồn React 19 / Vite / TypeScript.

## 2. Quy Tắc Bắt Buộc Khi Sửa Code hoặc Commit:
- **Tạo Worklog**: Mỗi khi thực hiện một task hoặc commit ở Backend hoặc Frontend, BẮT BUỘC phải tạo 1 file markdown ghi chép trong thư mục `docs/worklogs/` của repo đó theo mẫu `WORKLOG_TEMPLATE.md`.
- **Đặt tên file**: `YYYY-MM-DD_FE-<ID>_<AUTHOR>_<MOTA_NGAN>.md`.
- **Cập nhật PM Dashboard**: Sau khi hoàn tất hoặc merge, cập nhật trạng thái tính năng tương ứng trong `DOCS_MT_GRMS/PM_TRACKING_DASHBOARD.md`.
- **Kiến trúc Backend**: Controller tuyệt đối không trỏ vào Domain Entity; chỉ giao tiếp qua DTO. Entity chỉ DbContext và Service được truy cập.
