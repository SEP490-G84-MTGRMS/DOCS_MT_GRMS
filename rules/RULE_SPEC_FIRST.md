# QUY TRÌNH PHÁT TRIỂN SPEC-FIRST (SPEC-FIRST DEVELOPMENT PROTOCOL)

> **Mã quy tắc**: `RULE-03-SPEC-FIRST`  
> **Áp dụng cho**: Toàn bộ 26 Features của dự án MT-GRMS

---

## 1. Nguyên Tắc Cốt Lõi

> **"KHÔNG CÓ SPEC PHÊ DUYỆT $\rightarrow$ TUYỆT ĐỐI KHÔNG VIẾT CODE"**

Trước khi bắt tay vào code bất kỳ tính năng nào (dù là Backend hay Frontend), thành viên phụ trách (hoặc AI) bắt buộc phải kiểm tra xem thư mục `DOCS_MT_GRMS/specs/FE-xx/spec.md` đã có tài liệu đặc tả chưa.

---

## 2. Quy Trình 3 Pha

```text
PHA 1: LẬP SPEC (Tại DOCS_MT_GRMS)
- Sao chép SPEC_TEMPLATE.md vào thư mục specs/FE-xx/spec.md
- Viết Proposal (Vấn đề & Giải pháp)
- Viết kịch bản BDD Given - When - Then
- Định nghĩa Database Entity & RESTful API contracts
- Được Reviewer phê duyệt (Approved)
       │
       ▼
PHA 2: HIỆN THỰC HÓA (Tại BE & FE Repos)
- Backend: Tạo Entity, Configuration, DTOs, Service, Controller theo đúng Spec
- Frontend: Tạo Page, Component, Axios Service theo đúng API Contract trong Spec
- Tạo file Worklog trong docs/worklogs/
       │
       ▼
PHA 3: KIỂM CHỨNG & TÍCH HỢP (E2E Integration)
- Chạy unit tests BDD theo các kịch bản trong Spec
- PM duyệt PR và đánh dấu hoàn thành trên PM_TRACKING_DASHBOARD.md
```
