# LAB-5 — Backlog và báo cáo tiến độ · Product B (Yuki Cold)

**Học viên:** Khoe Nguyen · **Mã học viên:** không có · **Đề:** Product B — chuỗi kho lạnh thực phẩm

## 1. Tổng quan

- Backlog rã từ bộ thiết kế **LAB-4** nộp ngày **2026-10-21** (15 màn · architecture · database · 4 detail design · 5 ADR).
- Tiền đề có thay đổi so với LAB-4 — xem [PREMISE.md](PREMISE.md): 3 spec sửa/thêm · 5 giả định bổ sung · 6 hướng đã chốt.
- **307 issue** `#1`–`#307` trên board: 13 epic · 26 story · 54 task cha BE/FE · **176 dev task** · 38 câu hỏi khách.
- **Ước công: 671 SWP · 1.140,7 giờ · 142,6 ngày công.** Quy ước **1 SWP = 1,7 giờ**, là **giờ dev thuần** — không gồm QA.
- Số epic: **13** · Sprint giả lập đã chạy: **Sprint 1** (26/10 → 06/11/2026, 10 ngày làm việc) — 45 ticket · 157 SWP · kết quả **37 Done / 122 SWP = 78%**.

> **Ba chỗ con số này chưa nói hết**, ghi ở đây để không ai trích nhầm: board **không có ticket QA**
> (LAB-1 cho phần tương ứng 92 ngày QA trên 354 ngày dev của chính nó ⇒ tỉ lệ **QA : dev = 26%**,
> áp lên 142,6 ra **~37 ngày công QA** chưa tính) · board **không có ticket
> sửa bug** (LAB-1 chừa 41 ngày, tức **~12% công dev**) · **E12 nền tảng chung hụt 90%** so với
> LAB-1, nghi rã thiếu. Chi tiết: [estimate.md](estimate.md) mục 2 và mục 5.

## 2. Link

- Repo: https://github.com/khoent-2975/lab5-product-b
- GitHub Project: https://github.com/users/khoent-2975/projects/1
- Báo cáo HTML của skill chấm SWP: [`reports/261024-GH-buoc-7-estimate-swp.html`](reports/261024-GH-buoc-7-estimate-swp.html)
- Báo cáo tiến độ Sprint 1 (HTML): [`reports/261025-GH-buoc-9-progress-report.html`](reports/261025-GH-buoc-9-progress-report.html)

Hai file HTML tự chứa, mở thẳng bằng trình duyệt, không cần chạy server.

**Đã mở thử bằng cửa sổ ẩn danh** (không đăng nhập GitHub), ngày 2026-10-25:

| Link | Kết quả |
|---|---|
| Repo | ✅ mở được — `visibility: public` |
| GitHub Project số 1 | ⚠️ **chưa mở được — đang `public: false`, trả 404.** Phải bật công khai trước khi nộp |
| Hai file HTML trong repo | ✅ tải và hiển thị được qua `raw.githubusercontent.com` |

## 3. Cấu trúc repo

| File / thư mục | Nội dung |
|---|---|
| `README.md` | File này — tổng quan, link, cấu trúc repo, ánh xạ spec → epic |
| `PREMISE.md` | Tiền đề: backlog LAB-5 khác bản thiết kế LAB-4 ở đâu và vì sao. 3 spec sửa · 5 giả định bổ sung · 6 hướng đã chốt |
| `task-breakdown.md` | Bản rã 307 item — nguồn nội dung của mọi issue trên board. Luật chia task, ánh xạ spec → issue, cụm ràng buộc giờ lái 2024, phần spec chưa thành issue (6.824 dòng) |
| `estimate.md` | Ước công: skill chấm bao nhiêu ⟷ tôi chốt bao nhiêu, cách quy SWP ra giờ, tổng theo epic, chia việc Sprint 1, đối chiếu estimate LAB-1 |
| `progress-report.md` | Báo cáo Sprint 1 giả lập: trạng thái cuối sprint, burndown, 10 rủi ro trễ có chủ và hạn |
| `AI-report.md` | Dùng AI thế nào: skill và prompt, cách review output, chỗ hiệu quả và chỗ chưa tốt |
| `BAN-GIAO.md` | Sổ làm việc nội bộ — hằng số của board, cấu trúc 307 issue, quyết định đã chốt, bảng 10 bước. Không nằm trong danh mục đề đòi, giữ lại để truy vết cách làm |
| `reports/` | Báo cáo sinh ra trong lúc làm — xem bảng dưới |
| `.gitignore` | Bỏ qua `.DS_Store` và file tạm |

Trong `reports/`:

| File | Nội dung |
|---|---|
| `261024-GH-buoc-7-estimate-swp.html` | **Báo cáo HTML của skill chấm SWP** (`tkm:estimate-swp --level high`) — đề đòi file này |
| `261025-GH-buoc-9-progress-report.html` | Bản HTML của `progress-report.md`, ảnh burndown nhúng sẵn, có nút đổi nền sáng/tối |
| `261025-GH-buoc-9-burndown-sprint-1.png` | Ảnh burndown Sprint 1 |
| `261024-GH-buoc-0-quet-spec-lab4.md` | Bản nháp quét 15 screen spec của LAB-4 — nguyên liệu dựng `PREMISE.md` và `task-breakdown.md` |

**Thứ tự đọc cho người mới:** `README.md` → `PREMISE.md` → `task-breakdown.md` → `estimate.md` →
`progress-report.md` → `AI-report.md`. `task-breakdown.md` dài, chỉ mở khi cần tra nội dung gốc của
một issue cụ thể.

## 4. Spec → epic

15 screen spec của LAB-4 rã thành 13 epic. Epic bám **nhóm chức năng của estimate LAB-1** để đối
chiếu công được, nên một epic có thể gom nhiều màn, và một màn có thể rải sang nhiều epic.

| Spec (file LAB-4 / dòng PREMISE) | Epic trên Project | Ghi chú |
|---|---|---|
| `scr-28-tao-tuyen-giao-hang.md` | [`#1`](https://github.com/khoent-2975/lab5-product-b/issues/1) — E01 Build delivery route creation on SCR-28 | 52 SWP · issue `#1`–`#20` |
| `scr-28` §6.2.1 — bốn ngưỡng giờ lái | [`#21`](https://github.com/khoent-2975/lab5-product-b/issues/21) — E02 Enforce 2024 driver-hour limits within a single service day | **Ràng buộc đặc thù của đề: giới hạn giờ lái xe tải từ 2024.** 40 SWP · `#21`–`#35` · rã riêng 4 dev task cho 4 ngưỡng, xem `task-breakdown.md` §3 |
| `scr-29-cong-bo-tuyen-giao-hang.md` | [`#36`](https://github.com/khoent-2975/lab5-product-b/issues/36) — E03 Publish routes as immutable versions with pinned rule version | 55 SWP · `#36`–`#56` · bị E04 chặn, xem `PREMISE` §3 `V-1` |
| `PREMISE.md` §1 dòng 1 + §3 `V-1` `V-2` — chỗ lưu điểm nghỉ `休憩` | [`#57`](https://github.com/khoent-2975/lab5-product-b/issues/57) — E04 Store and honour rest stops in route planning and publishing | **Việc mới hoàn toàn**, sinh từ chỗ hở phát hiện khi break; LAB-1 không ước cho nó dòng nào. 19 SWP · `#57`–`#66` |
| `scr-28` §6.2.2 ngưỡng #8 #9 | [`#67`](https://github.com/khoent-2975/lab5-product-b/issues/67) — E05 Enforce multi-day cumulative driver-hour thresholds | Ràng buộc giờ lái, phần cộng dồn nhiều ngày. Chờ khách trả lời Q13 (`GĐ-L5-2`). 19 SWP · `#67`–`#74` |
| `scr-12-nhap-kiem-hang.md` | [`#75`](https://github.com/khoent-2975/lab5-product-b/issues/75) — E06 Harden goods receiving and lot creation on SCR-12 | 45 SWP · `#75`–`#101` |
| `scr-18-tra-cuu-ton-kho.md` · `scr-19-trang-thai-lot.md` | [`#102`](https://github.com/khoent-2975/lab5-product-b/issues/102) — E07 Make inventory search trustworthy and lot status changes traceable | 49 SWP · `#102`–`#127` |
| `scr-20-don-hang.md` · `scr-21-phan-bo-ton.md` | [`#128`](https://github.com/khoent-2975/lab5-product-b/issues/128) — E08 Make order intake and stock allocation consistent and auditable | 55 SWP · `#128`–`#162` |
| `scr-23-lay-hang-boc-xep.md` · `scr-24-kiem-truoc-xuat.md` · `scr-26-pod.md` | [`#163`](https://github.com/khoent-2975/lab5-product-b/issues/163) — E09 Close the evidence gaps along the pick → dispatch → POD chain | Nhiều issue nhất: 44. 83 SWP · `#163`–`#206` |
| `scr-31-nhap-csv-nhiet-do.md` · `scr-32-canh-bao-nhiet-do.md` · `scr-33-quan-ly-sai-lech.md` | [`#207`](https://github.com/khoent-2975/lab5-product-b/issues/207) — E10 Make the temperature chain judge, alert and resolve with a complete audit trail | **Nặng nhất board: 102 SWP** · `#207`–`#250` · ba dải nhiệt, hai mức cảnh báo theo `GĐ-L5-4` |
| `scr-35-truy-xuat-nguon-goc.md` | [`#251`](https://github.com/khoent-2975/lab5-product-b/issues/251) — E11 Make the traceability chain complete, fast and safe to read | 32 SWP · `#251`–`#272` |
| `scr-00-home-trang-chu.md` + phần dùng chung của cả 15 màn | [`#273`](https://github.com/khoent-2975/lab5-product-b/issues/273) — E12 Build the shared app shell, error boundaries and role surface | **Nghi rã thiếu — hụt 90% so với LAB-1**, xem `estimate.md` mục 5. 32 SWP · `#273`–`#293` |
| `01-architecture.md` §9.1 — 8 mock của prototype LAB-2, không thuộc màn nào | [`#294`](https://github.com/khoent-2975/lab5-product-b/issues/294) — E13 Replace the eight prototype mocks with real integration points | Rã thô nhất: 8 dev task mang 88 SWP, trung bình 11 điểm/ticket so với 3,8 của cả board. `#294`–`#307` |

**Cách đánh dấu trên board:** `Issue Type` không dùng được (repo cá nhân, `repository.issueTypes`
trả `null`), nên cấp được đánh bằng **nhãn** `type:epic` / `type:story` / `type:devtask` /
`type:investigation`, và quan hệ cha–con nối bằng **sub-issue native** của GitHub.

**Trường trên Project:** `Status` · `Sprint` (iteration) · `SWP` (number) · `Giờ ước lượng`
(number) · `Người phụ trách` (text — người giả định, điền cho 45 ticket Sprint 1). 38 issue
`type:investigation` để trống `SWP` và `Giờ` có chủ ý — hỏi khách thì chưa biết làm gì mà ước.
