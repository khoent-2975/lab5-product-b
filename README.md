# LAB-5 — Backlog và báo cáo tiến độ · Product B (Yuki Cold)

**Học viên:** Khoe Nguyen · **Mã học viên:** không có · **Đề:** Product B — chuỗi kho lạnh thực phẩm

## 1. Tổng quan

- Backlog này tôi rã ra từ bộ thiết kế **LAB-4** nộp ngày **21/10/2026** — 15 màn hình, kèm bản
  kiến trúc, mô hình dữ liệu, 4 bản thiết kế chi tiết và 5 quyết định kiến trúc.
- **Tiền đề có thay đổi so với LAB-4.** Trong lúc rã task tôi tìm ra ba chỗ spec phải sửa, phải
  thêm năm giả định, và phải chốt sáu hướng mà LAB-4 còn để ngỏ. Tất cả ghi trong
  [PREMISE.md](PREMISE.md).
- Rã ra **307 issue** (`#1`–`#307`), chia làm **13 epic**. Trong đó có 26 story, 54 task cha cho
  hai vai BE và FE, **176 dev task** thật sự sinh code, và 38 câu hỏi phải gửi khách.
- Ước công cả backlog: **671 SWP**, quy ra **1.140,7 giờ**, tức **142,6 ngày công**. Tôi chốt một
  điểm SWP đổi ra 1,7 giờ. Đây là **giờ của lập trình viên thôi**.
- Sprint giả lập đã chạy: **Sprint 1**, hai tuần từ 26/10 đến 06/11/2026 (10 ngày làm việc), nhận
  45 ticket tức 157 SWP. Hết sprint làm xong 37 ticket, được 122 SWP — **78%** số điểm đã nhận.

> **Con số 142,6 ngày công chưa phải là toàn bộ công của dự án.** Tôi ghi ba chỗ còn hụt ngay đây,
> để sau này không ai cầm nhầm con số đó đi báo giá.
>
> - **Chưa có công kiểm thử.** Backlog này tôi cố ý chỉ rã việc của lập trình viên, không rã việc
>   QA — vì QA phải đo bằng thang điểm riêng, trộn chung một thang thì con số tổng mất nghĩa. Nhìn
>   sang LAB-1 thì cứ 100 ngày công lập trình, QA tốn thêm khoảng 26 ngày nữa. Chiếu tỉ lệ đó vào
>   đây, còn **khoảng 37 ngày công QA** nằm ngoài con số 142,6.
> - **Chưa có công sửa lỗi.** Trên board không ticket nào mang việc sửa bug, đơn giản vì QA chưa
>   test thì bug chưa sinh ra. Nhưng việc làm ở Sprint 1 thế nào cũng có lỗi, và công sửa vẫn phải
>   trả ở những sprint sau. LAB-1 chừa sẵn cho khoản này **khoảng 12% công lập trình**.
> - **Phần nền tảng dùng chung nhiều khả năng tôi rã còn thiếu.** LAB-1 cho nhóm này 65 ngày công,
>   bản rã của tôi chỉ ra 6,8 ngày — **hụt 90%**. Chênh nhiều tới mức tôi nghi mình bỏ sót việc chứ
>   không phải LAB-1 ước thừa, nên chỗ này cần soi lại.
>
> Cả ba tôi phân tích kỹ trong [estimate.md](estimate.md), mục 2 và mục 5.

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

**Nếu anh/chị đọc lần đầu,** tôi gợi ý đi theo thứ tự: `README.md` → `PREMISE.md` →
`estimate.md` → `progress-report.md` → `AI-report.md`. Riêng `task-breakdown.md` dài 6.846 dòng,
chỉ nên mở khi cần tra nội dung gốc của một issue cụ thể, đừng đọc tuần tự.

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

### Vài điều về cách tôi dựng board

- **Phân cấp bằng nhãn, không bằng Issue Type.** GitHub chỉ cho dùng Issue Type ở repo của tổ
  chức, còn đây là repo cá nhân nên tính năng đó không bật được. Tôi thay bằng bốn nhãn:
  `type:epic`, `type:story`, `type:devtask`, `type:investigation`.
- **Quan hệ cha–con dùng sub-issue của chính GitHub,** không phải tự viết trong thân ticket. Nhờ
  vậy Project tự đếm được tiến độ của từng task cha.
- **Trên Project tôi dùng năm cột:** trạng thái, sprint, SWP, giờ ước lượng, và người phụ trách.
  Người phụ trách là người giả định — BE-1, BE-2, FE-1, FE-2 — và tôi chỉ điền cho 45 ticket của
  Sprint 1, vì đó là những ticket đã thật sự chạy qua mô phỏng.
- **38 câu hỏi gửi khách để trống cả SWP lẫn giờ, và đó là chủ ý.** Chưa biết khách trả lời thế
  nào thì chưa biết phải làm gì, mà chưa biết làm gì thì không ước công được.
