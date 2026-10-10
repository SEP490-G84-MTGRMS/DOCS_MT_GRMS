# QUY TẮC BẮT BUỘC: QUẢN LÝ THAY ĐỔI & MERGE CODE QUA AI TEAM KIT (SEP KIT)

> **Mã quy tắc**: `RULE-01-SEP-MANAGEMENT` (Nâng cấp từ `RULE-01-WORKLOG`)  
> **Phạm vi áp dụng**: Cả hai repository `MT_GRMS_BACKEND` và `MT_GRMS_FRONTEND`  
> **Người thực hiện**: Toàn bộ thành viên nhóm SEP490-G84 & Các AI Coding Agents  
> **Hệ thống quản lý trung tâm**: [`ai-team-kit/team-ai-knowledge/openspec/`](../../../ai-team-kit/team-ai-knowledge/openspec/)

---

## 1. Mục Đích & Ý Nghĩa

Thay vì lưu các file markdown worklog thủ công rời rạc ở từng subproject, toàn bộ quy trình phát triển được chuyển giao cho **AI Team Kit (SEP Kit & OpenSpec)** quản lý tập trung:
* **Phân chia theo từng người**: Mỗi thành viên được gán làm `assignee` cho từng Change cụ thể (Đức, Tâm, Sơn, An, Nhật).
* **Phản biện đa chiều tự động**: Tự động kích hoạt Persona Review (`skeptic`, `codebase`, `guardian`, `advocate`) trước khi viết code.
* **Kiểm soát code hoàn thành**: Mọi task phải được chia nhỏ và tick hoàn thành trong `tasks.md`.
* **Nghiệm thu kiểm thử**: Bắt buộc có `test-report.md` với `verdict: PASS` (Build 0 lỗi, Test 100% Pass).
* **Hỗ trợ Admin / PM**: Cung cấp dashboard trực quan (`npm run sep -- list --all`) để PM duyệt và merge code an toàn, không xung đột.

---

## 2. Quy Trình 6 Bước Dành Cho Developer & AI Agent

Khi bắt đầu bất kỳ tính năng, refactor hoặc sửa bug nào:

```text
/sep-spec  ──►  /sep-brainstorm  ──►  /sep-verify-spec  ──►  /sep-apply  ──►  /sep-test  ──►  /sep-archive
(Bước 1)          (Bước 2)              (Bước 3)             (Bước 4)        (Bước 5)        (Bước 6)
```

1. **Bước 1 (`/sep-spec <mô tả>`)**:
   - Chọn schema (`feature` / `bug-fix` / `refactor`).
   - Tự động sinh `proposal.md` và gắn `assignee: @github_username`.
2. **Bước 2 (`/sep-brainstorm`)**:
   - Soạn thảo `exploration.md`, `design-brief.md`, và đặc tả delta `specs.md`.
3. **Bước 3 (`/sep-verify-spec`)**:
   - Đẩy lên Persona Review: Bắt buộc `review/skeptic.md` và `review/codebase.md`.
   - Lập danh sách công việc `tasks.md` dạng checklist có thể kiểm chứng.
4. **Bước 4 (`/sep-apply`)**:
   - Tiến hành code trên repository (`MT_GRMS_BACKEND` hoặc `MT_GRMS_FRONTEND`).
   - Tick toàn bộ các mục hoàn thành trong `tasks.md`.
5. **Bước 5 (`/sep-test`)**:
   - Chạy build và test thực tế (`dotnet test` / `npm run build`).
   - Tạo `test-report.md` với kết quả bắt buộc: `verdict: PASS`.
6. **Mở Pull Request**:
   - Đính kèm tên Change trong OpenSpec vào mô tả PR.

---

## 3. Trách Nhiệm Của PM & Admin Khi Duyệt & Merge PR

PM và Tech Lead **chỉ bấm Merge PR** sau khi xác nhận các tiêu chí sau:

1. **Kiểm tra tiến độ trên Team Kit**:
   ```bash
   cd ai-team-kit/team-ai-knowledge
   npm run sep -- list --all
   ```
2. **Xem chi tiết hồ sơ Change chuẩn bị merge**:
   ```bash
   npm run sep -- status <tên-change>
   ```
3. **Tiêu chí bắt buộc để Merge**:
   - [x] Change đã qua các bước Verify Spec và Persona Review.
   - [x] 100% mục trong `tasks.md` đã tick `[x]`.
   - [x] `test-report.md` đạt `verdict: PASS`.
   - [x] Không xung đột code Git với nhánh `main`.
4. **Sau khi Merge thành công**:
   - Chạy `/sep-archive <tên-change>` để chuyển trạng thái sang `archived` và tự động tích hợp delta specs vào spec gốc của hệ thống.
