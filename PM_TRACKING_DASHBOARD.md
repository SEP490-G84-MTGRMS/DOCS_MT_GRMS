# PM TRACKING DASHBOARD (BẢNG QUẢN LÝ TIẾN ĐỘ TÍCH HỢP TOÀN DỰ ÁN)

> **Quản lý dự án**: Project Manager (PM)  
> **Dự án**: Multi-Tenant Grocery Retail Management System (MT-GRMS)  
> **Cập nhật lần cuối**: 2026-09-30  
> **Ghi chú**: PM cập nhật file này sau mỗi lần duyệt và merge PR từ Backend và Frontend.

---

## 1. Trạng Thái Tổng Thể (Overall Progress Summary)

| Phân loại | Tổng số | Chưa bắt đầu | Đang thực hiện | Đã Merge (Hoàn tất) | Tiến độ % |
|:---|:---:|:---:|:---:|:---:|:---:|
| **Backend (26 Features)** | 26 | 24 | 2 | 0 | 8% |
| **Frontend (26 Features)** | 26 | 25 | 1 | 0 | 4% |
| **Tích hợp BE-FE (E2E)** | 26 | 26 | 0 | 0 | 0% |

---

## 2. Bảng Theo Dõi Chi Tiết 26 Tính Năng (BE & FE Cross-Repo Tracker)

*Quy ước trạng thái*:  
⚪ `No Start` | 🟡 `In Progress` | 🔵 `In Review (PR Open)` | 🟢 `Merged (Done)` | 🔴 `Blocked`

| Mã Tính Năng | Tên Tính Năng | Phụ Trách BE | Trạng Thái BE | Worklog BE | Phụ Trách FE | Trạng Thái FE | Worklog FE | Tích hợp E2E | Ghi Chú PM |
|:---:|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---|
| **ARCH** | Kiến trúc Clean Architecture & Code-First Skeleton | Đức | 🟢 `Merged` | [Log](./../MT_GRMS_BACKEND/docs/worklogs/2026-09-30_INIT_ARCH_skeleton-setup.md) | Tâm | 🟡 `In Progress` | - | 🟡 Đang dựng | Đã dựng xong khung mẫu Catalog |
| **FE-01** | Product Catalog Management | Tâm | 🟡 `In Progress` | - | Tâm | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 1 |
| **FE-02** | Batch & Expiry Date (FEFO Engine) | Đức | 🟡 `In Progress` | - | Đức | ⚪ `No Start` | - | ⚪ Chưa test | [Spec có sẵn](./specs/FE-02-fefo-batch/spec.md) |
| **FE-03** | Selling Price & Price Book Management | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-04** | Inventory & Stocktaking (Kiểm kê kho) | Đức | ⚪ `No Start` | - | Đức | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-05** | Purchase & Goods Receipt (Nhập kho PO) | Đức | ⚪ `No Start` | - | Đức | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-06** | Internal Use & Wastage (Xuất nội bộ/Hủy) | Đức | ⚪ `No Start` | - | Đức | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-07** | Service Purchase Management (Mua dịch vụ) | An | ⚪ `No Start` | - | An | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-08** | Customer Management & CRM | An | ⚪ `No Start` | - | An | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-09** | Supplier Management (Quản lý NCC & Công nợ) | Đức | ⚪ `No Start` | - | Đức | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 2 |
| **FE-10** | Dashboard & Analytics Reports | An | ⚪ `No Start` | - | An | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-11** | Employee & Payroll Management | An | ⚪ `No Start` | - | An | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-12** | POS Checkout & Sales (Bán hàng quầy) | Nhật | ⚪ `No Start` | - | Nhật | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-13** | Return & Refund Management (Đổi trả hàng) | Nhật | ⚪ `No Start` | - | Nhật | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-14** | Promotion & Voucher Management | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-15** | Mini Web Store & Online Orders | Nhật | ⚪ `No Start` | - | Nhật | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-16** | Clearance Sales / Markdown (Thanh lý) | Đức | ⚪ `No Start` | - | Đức | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-17** | Cashbook & Financial Transactions (Sổ quỹ) | An | ⚪ `No Start` | - | An | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 3 |
| **FE-18** | Multi-Branch & Store Settings | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-19** | User Management & RBAC Permissions | Nhật | ⚪ `No Start` | - | Nhật | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-20** | SaaS Tenant Lifecycle & Subscription | Nhật | ⚪ `No Start` | - | Nhật | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-21** | AI Smart Cart & Demand Forecasting | Nhật | ⚪ `No Start` | - | Nhật | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-22** | Audit Log & System Security | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-23** | Barcode & Label Printing | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-24** | Notification & Alert Center | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-25** | Third-party Integrations (VietQR, GHN, CDN) | An | ⚪ `No Start` | - | An | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
| **FE-26** | System Backup & Configuration | Sơn | ⚪ `No Start` | - | Sơn | ⚪ `No Start` | - | ⚪ Chưa test | Sprint 4 |
