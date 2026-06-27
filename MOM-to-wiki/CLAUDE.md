# MOM → Confluence Wiki — Project Guide

Skill này tự động hóa quy trình đọc file biên bản cuộc họp (MOM) `.docx`, phân tích nội dung, và đăng tải lên Confluence Wiki của NDSVN (Space MS).

---

## Khi nào dùng skill này

- Người dùng yêu cầu upload file MOM lên Wiki / Confluence sau khi họp xong (ví dụ: "đẩy file MOM lên wiki đi", "publish MOM hôm nay lên Confluence").
- File `.docx` trong thư mục `D:\BA_And_Stuff\MOM` đã sẵn sàng.

## Khi nào KHÔNG dùng

- Trang Wiki không phải Confluence NDSVN / ngoài Space MS.
- File MOM chưa hoàn chỉnh hoặc không phải định dạng `.docx`.

---

## Danh sách Account Team (để map @username)

| Tên hiển thị | Username Confluence |
|---|---|
| Hỗ Võ Hoàng Duy | duy.ho |
| Võ Quốc Huy | huy.vo |
| Định Quân | quan.dinh |
| Trần Tiến Phong | phong.tran |
| Đào Minh Hải | hai.dao |
| Phạm Xuân An | an.pham |
| Hoàng Tiến | tien.hoang |
| Trần Văn Đức | duc.tran |
| Nguyễn Vũ Anh Khoa | khoa.nguyen |
| Đổng Quốc Khánh | khanh.dong |

> Tên không có trong danh sách → giữ nguyên văn bản gốc.

---

## Các bước thực hiện

### Bước 1 — Parse file .docx
1. Quét `D:\BA_And_Stuff\MOM` để tìm file mới nhất (hoặc theo yêu cầu).
2. Chạy `scripts/parse_mom.py` để trích xuất: dự án, ngày họp, thành viên, action items, tasks, retro.
3. Đối chiếu tên thành viên với bảng trên → chuẩn hóa thành `@username`.

### Bước 2 — Định tuyến trang cha & tiêu đề

| Loại cuộc họp | Parent Page ID | Ví dụ tiêu đề |
|---|---|---|
| Daily Standup | `164660481` | `Daily Standup Meetings – 12/06/2026` |
| Sprint Review & Retro | `177373263` | `Sprint review and Retrospective – 15/06/2026` |
| Sprint Planning | `177373261` | `Sprint planning – 15/06/2026` |

**Format tiêu đề:** `[Tên trang cha] – [dd/mm/yyyy]`

### Bước 3 — Publish lên Confluence
1. Chuyển nội dung sang **HTML Storage Format (XHTML)**.
2. Map `@username` → thẻ mention Confluence:
   ```xml
   <ac:link><ri:user ri:username="username" /></ac:link>
   ```
3. Gọi `confluence_create_page` (MCP Server `ndsvn-confluence`) để tạo trang con.
4. Trả về link xác nhận:
   ```
   https://wiki.ndsvn.vn/pages/viewpage.action?pageId=PAGE_ID
   ```

---

## Cấu trúc thư mục

```
D:\BA_And_Stuff\MOM\
├── MOM-to-wiki/
│   └── CLAUDE.md          ← file này
└── [các file MOM .docx]
```
