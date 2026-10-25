# Bàn giao — LAB-5 Product B (backlog + báo cáo tiến độ)

**Cập nhật:** 2026-10-25 · **Đã xong:** bước 0 → 9 · **Tiếp theo:** bước 10

> **Nguồn đúng cho mọi con số là `estimate.md` (bước 8) và `PREMISE.md`,** không phải
> file này. File này giữ hằng số, cấu trúc board và bối cảnh gốc.

Thread mới đọc file này trước, rồi đọc `estimate.md` (điểm, giờ, cắt sprint — bước 8),
`reports/261025-GH-buoc-9-progress-report.md` (Sprint 1 giả lập — bước 9), `task-breakdown.md` (bản rã 307
item — nguồn nội dung mọi issue), `PREMISE.md`, và
`reports/261024-GH-buoc-0-quet-spec-lab4.md` nếu cần ngữ cảnh gốc.

**Board đã dựng và chấm xong:** 307 issue `#1`–`#307`, đủ nhãn, đủ cây 4 cấp, đủ trên Project 1.
269 item đã có `SWP` và `Giờ ước lượng`; 38 investigation để trống có chủ ý. 45 ticket đã gán
`Sprint 1` và đã chạy giả lập 10 ngày. Việc còn lại là cắt Sprint 2 và nộp bài — không còn việc
tạo issue.

---

## 1. Hằng số — dùng nguyên văn, không tra lại

| Thứ | Giá trị |
|---|---|
| Repo (public) | `khoent-2975/lab5-product-b` · https://github.com/khoent-2975/lab5-product-b · nhánh `main` |
| Project | số **1** · `PVT_kwHOBf6CDs4Boeim` · https://github.com/users/khoent-2975/projects/1 |
| Nguồn spec | `/Users/nguyen.thi.khoe/Documents/ai-training/lab4-product-b/specs/` (chỉ đọc) |
| Estimate LAB-1 | `/Users/nguyen.thi.khoe/Documents/ai-training/lab1-product-b/03-estimate/product-b-vi-estimate-261006-1700.json` |

### Trường trên Project

| Trường | Kiểu | Field ID | Giá trị |
|---|---|---|---|
| Status | single-select | `PVTSSF_lAHOBf6CDs4Boeimzhm-fqE` | **đã dịch ở bước 9** — 45 item Sprint 1 mang trạng thái cuối sprint (39 Done · 2 In Review · 1 In Progress · 1 Blocked · 2 Todo), 262 item còn lại vẫn `Todo`. Todo `f75ad846` · In Progress `47fc9ee4` · In Review `eef67101` · Blocked `4cd94c4e` · Done `98236657` |
| Sprint | iteration | `PVTIF_lAHOBf6CDs4Boeimzhm-f2I` | **đã điền ở bước 8** — Sprint 1 `af2d180b` (2026-10-26, 14d) có 45 ticket; Sprint 2 `e59811eb` (2026-11-09, 14d) mới có `#39` `#60`, **phần còn lại chưa cắt** |
| SWP | number | `PVTF_lAHOBf6CDs4Boeimzhm-f2U` | **đã điền ở bước 8** — 269 item có điểm. **671 SWP là tổng của 176 dev task**; cộng cả 269 item ra 2.665 vì cấp cha cộng dồn điểm của con |
| Giờ ước lượng | number | `PVTF_lAHOBf6CDs4Boeimzhm-f3k` | **đã điền ở bước 8** — tổng **1.140,7 giờ** = 142,6 ngày công, quy ước **1 SWP = 1,7 giờ** (giờ dev thuần, không gồm QA) |
| ~~Vai phụ trách~~ | text | `PVTF_lAHOBf6CDs4Boeimzhm-f4I` | **BỎ** — không có trong đề, không bước nào đọc. ⚠ **Thực tế 202/307 item có giá trị** (dính theo lúc tạo issue), nhưng không bước 0–10 nào đọc cột này |
| ~~Tầng~~ | single-select | `PVTSSF_lAHOBf6CDs4Boeimzhm-f5E` | **BỎ** — chỉ để lọc, không bước nào đọc. ⚠ **Thực tế 152/307 item có giá trị**, dính theo lúc tạo issue. (Giá trị nếu sau cần: DB `53cad8a9` · RPC `c63257d1` · API `69aaf7f4` · UI `b1ed7222` · dùng chung `f0b33d08` · không code `e1c9fe6a`) |
| Parent issue · Sub-issues progress | native | — | có sẵn, dùng quan hệ cha/con native của GitHub |

⚠ **Issue Type không dùng được** — repo cá nhân, `repository.issueTypes` trả `null` (kiểm 2026-10-24);
Issue Type là tính năng cấp tổ chức. Đánh dấu cấp bằng **nhãn** `type:epic` / `type:story` /
`type:devtask` / `type:investigation` (đã tạo), nối cha–con bằng **quan hệ sub-issue native** (đã
nối). Xem `task-breakdown.md` §1.7.

⚠ **Assignees không dùng** — repo chỉ có một cộng tác viên (`khoent-2975`), gán vào không thêm
thông tin gì.

---

## 2. Quyết định đã chốt — không mở lại

| # | Chốt |
|---|---|
| 1 | ~~Backlog ~120 issue~~ → **rã thật ra 307 item**: 13 epic · 26 story · 54 parent BE/FE · 176 dev task · 38 investigation. Mọi dòng trong 229 dòng ước được đều truy về một dev task. Xem `task-breakdown.md` §1.1 |
| 2 | **M-1**: chỗ lưu điểm nghỉ `休憩` làm **trước**, E04 chặn E03. Ghi là giả định vendor (bài lab không hỏi khách được) — `PREMISE.md` §1 + §3 `V-1` `V-2` `V-6` |
| 3 | ~~Sprint 1 = T0 + T1 + T2 + T3~~ → **thay ở bước 8.** Sprint 1 chốt **45 dev task · 157 SWP · 266,9 giờ**: trọn E01 + E02 + phần E12 nền tảng chung, cộng **12 ticket FE vay** từ E03/E06/E07 để FE khỏi ngồi không. Thêm `#286` mở menu SCR-19 — không có nó thì `/routes` trả 404 và `AC-28-01` không nghiệm thu được. Nhánh công bố (T4→T6) vẫn sang Sprint 2. Chi tiết: `estimate.md` mục 4 |
| 4 | ~~Đội 1 BE · 1 FE · 1 QA~~ → **sửa ở bước 8.** Đội giả lập **2 BE · 2 FE · 1 QA**, sprint 2 tuần (`GĐ-L5-5`), cho khớp kế hoạch người theo tháng của LAB-1 (tháng xây dựng đầu tiên 2026/12). Sức chứa **94 SWP mỗi vai** thay vì 47 |
| 5 | ~~Quy SWP → giờ chưa chốt~~ → **chốt ở bước 8: 1 SWP = 1,7 giờ**, rút từ E01+E02 đối chiếu LAB-1 (19 ngày công × 8 giờ ÷ 92 SWP = 1,65 → làm tròn). Dùng để **chia việc trong sprint**, KHÔNG dùng để báo giá — xem `estimate.md` mục 2 |
| 6 | Còn thiếu: **mã học viên** trong `README.md` |
| 7 | `E03-BE-08` chỗ lưu "tài xế đã xem bản nào" = **bảng mới `route_version_acks`** (một dòng mỗi tài xế × bản tuyến, có mốc xem). Không thêm cột vào `pods` |
| 8 | `E03-BE-10` **thêm** khoá `checkedRules` vào `check_result`, ghi rõ là **mở rộng hợp đồng ngoài `PREMISE` §3 `V-3`**, chốt cùng `E02-BE-09` |
| 9 | **Bỏ `Vai phụ trách` và `Tầng`** — đề không đòi, không bước nào đọc. Ý định là để trống, nhưng **thực tế 202 và 152 item dính giá trị lúc tạo issue**; không bước nào đọc nên để nguyên. `Assignees` cũng không dùng |
| 10 | **Sprint điền ở bước 8**, không điền sớm: phải có giờ thật mới cắt được ranh giới sprint. ✅ đã làm |
| 11 | **Bốn chỗ hụt đã biết, ghi để không ai quên** (bước 8 + 9): board không có ticket QA — LAB-1 cho phần tương ứng 92 ngày công, tức **+26%** ngoài 142,6 ngày · board không có ticket sửa bug — LAB-1 chừa 41 ngày, tức **~12% công dev** · **E12 hụt 90%** so với LAB-1, nghi rã thiếu · board lệch **64% BE / 36% FE** trong khi đội 50/50. Chi tiết: `progress-report.md` phần 4 |

---

## 3. Thứ tự chạy thật của module lập lịch

```
T0 migration nền ────┐   create_route · set_route_stops · sequence route_code
   (chặn tất cả)     │   client_request_id (routes + route_versions) · unique(valid_from)
                     ├──► T2 API route ──► T3 UI SCR-28
T1 driver-hours.ts ──┘   hàm thuần, unit test, song song được với T0

T4 chỗ lưu điểm nghỉ ──► T5 publish_route ──► T6 UI SCR-29      ← M-1 đẩy T4 lên trước
T7 ngưỡng cộng dồn nhiều ngày — chờ Q13, không chặn ai
```

---

## 4. Nguyên liệu đã đo — không đo lại

| Số | Nghĩa |
|---|---|
| **272** | dòng mục 6.3 *"khoảng cách khách ⟷ prototype"* của 15 screen spec |
| **229** | trong đó có tầng code → ước công được |
| **43** | chỉ cần một quyết định, không sinh code |
| **39** | chờ khách trả lời — đều có số Q và giả định vendor sẵn |
| **3** | mâu thuẫn thật: M-1 (điểm nghỉ ⟷ công bố) · M-2 (`AC-28-33` ⟷ `Đ-3`) · M-3 (`client_request_id` ghi hai nơi) |
| **417** | lượt gán tầng (một dòng mang nhiều tầng) → **73 nhóm (màn × tầng)**, 35 nhóm > 4 dòng |
| **1.035** | dòng AC ở mục 6.4 — dùng làm định nghĩa xong của issue |

**13 epic** (bám nhóm chức năng LAB-1 để đối chiếu estimate được): E01 dựng tuyến · E02 luật giờ lái
trong ngày · E03 công bố có phiên bản · E04 điểm nghỉ · E05 ngưỡng nhiều ngày · E06 nhập kho ·
E07 tồn kho & trạng thái lô · E08 đơn hàng & phân bổ · E09 lấy hàng→POD · E10 chuỗi nhiệt độ ·
E11 truy xuất · E12 nền tảng dùng chung · E13 tích hợp ngoài từ mock M1–M8.

**LAB-1 để đối chiếu** (`options[0].categories`, mỗi task có sẵn `story_points` + `total_md`):
F06 Lộ trình và giờ ràng buộc = 105 SP / 59 MD, trong đó phần thuộc phạm vi LAB-5 là
FT-06-01 (26/14) · FT-06-03 (29/16) · FT-06-04 (8/5) · FT-06-05 (13/8).
⚠ LAB-1 **vẫn tính công** cho `FT-02-03` (FR-REC-03) mà LAB-2 đã cắt → bảng đối chiếu phải trừ ra.

---

## 4b. Board đang có gì — cấu trúc 307 issue đã dựng

**File:** `task-breakdown.md` · **307 item** · cấu trúc **4 cấp**:

```
[EPIC]                     13   nhãn type:epic          không có cha
└── [STORY]                26   nhãn type:story         24 US thật + 2 story kỹ thuật (E12-ST, E13-ST)
    ├── [PARENT][BE]       27 ┐ nhãn type:devtask       Task Category = Feature, không tự có code
    │   └── dev task       …  │                          Task Type = Development - Backend
    └── [PARENT][FE]       27 ┘                          Task Type = Development - Frontend
        └── dev task       …
[INVESTIGATION]            38   nhãn type:investigation  treo dưới epic, KHÔNG ước công
                          ───
  dev task (cả BE lẫn FE)  176
```

### Template ticket — của công ty, đã kiểm có thật

Lấy nguyên từ bộ mẫu issue nội bộ của công ty (`.github/ISSUE_TEMPLATE/`), tên repo không ghi ở đây vì repo này công khai:

| Cấp | Template | Nhãn | Tiền tố tiêu đề |
|---|---|---|---|
| Epic | `01-epic.yml` | `type:epic` | `[EPIC] ` |
| Story | `02-story.yml` | `type:story` | `[STORY] ` |
| Parent BE/FE | `05-dev-task.yml` | `type:devtask` | `[PARENT][BE] ` / `[PARENT][FE] ` |
| Dev task | `05-dev-task.yml` | `type:devtask` | `[DEV TASK] ` |
| Câu hỏi khách | `12-investigation.yml` | `type:investigation` | `[INVESTIGATION] ` |

- Tiêu đề **tiếng Anh, động từ đứng đầu**, không chữ Nhật, gọi thẳng tên cột/hàm thật
- Thân ticket **tiếng Việt**; AC viết dạng `**AC-xx-yy** — Given … · When … · Then …`
- AC nào spec không có mã thì đánh dấu `[tự viết]`

### Dải số issue của từng epic

| Epic | Issue | Item |
|---|---|---:|
| E01 Dựng tuyến | `#1`–`#20` | 20 |
| E02 Luật giờ lái trong ngày | `#21`–`#35` | 15 |
| E03 Công bố có phiên bản | `#36`–`#56` | 21 |
| E04 Điểm nghỉ | `#57`–`#66` | 10 |
| E05 Ngưỡng nhiều ngày | `#67`–`#74` | 8 |
| E06 Nhập kho | `#75`–`#101` | 27 |
| E07 Tồn kho & trạng thái lô | `#102`–`#127` | 26 |
| E08 Đơn hàng & phân bổ | `#128`–`#162` | 35 |
| E09 Lấy hàng → POD | `#163`–`#206` | 44 |
| E10 Chuỗi nhiệt độ | `#207`–`#250` | 44 |
| E11 Truy xuất | `#251`–`#272` | 22 |
| E12 Nền tảng dùng chung | `#273`–`#293` | 21 |
| E13 Tích hợp ngoài M1–M8 | `#294`–`#307` | 14 |

**Ngoại lệ cấu trúc:** E05 không có story — hai parent `#68` `#72` treo thẳng dưới epic `#67`.

**Hai chỗ bản rã để ngỏ, đã chốt khi tạo issue:** `#46` (`E03-BE-08`) và `#48` (`E03-BE-10`) —
xem mục 2 #7 #8. Quyết định ghi thẳng trong thân ticket dưới nhãn *"Quyết định LAB-5 (chốt
2026-10-24)"*.

**32 parent không có mục `Specification` trong bản rã** → thân ticket dựng từ meta của chúng cộng
câu luật §1.7 *"task cha không tự có code, đóng khi con đóng hết"*.

**6 dev task của E02** (`#24` `#25` `#26` `#31` `#32` `#34`) không có dòng `**Parent:**` trong thân
vì bản rã không viết — quan hệ cha–con trên GitHub vẫn đúng.

---

## 5. Bước còn lại

| # | Việc | Ra cái gì | Skill / công cụ |
|---|---|---|---|
| ~~4~~ | ✅ **XONG** — `task-breakdown.md`, 6.824 dòng, 13 epic, **307 item** | `task-breakdown.md` | — |
| ~~5~~ | ✅ **XONG** — 307 issue `#1`–`#307` trên repo + Project 1, 4 nhãn `type:*`, cây 4 cấp nối bằng sub-issue native. Đã soát: 0 tiêu đề lệch, 0 cha gắn sai, 0 dòng nội dung rơi | issue trên board | `gh issue create` · `gh api` sub-issues |
| ~~6~~ | ✅ **XONG — không còn việc.** `Status` cả 307 đã là `Todo` do workflow Project tự gán. `Sprint` dời sang bước 8. `Vai phụ trách` · `Tầng` · `Assignees` đã bỏ (mục 2 #9) | — | — |
| ~~7~~ | ✅ **XONG** — chấm 176 dev task, review 5 ticket đại diện, hiệu chỉnh kéo theo 13 ticket, đối chứng 9 ticket rủi ro bằng mô hình thứ hai | `reports/261024-GH-buoc-7-estimate-swp.html` | `tkm:estimate-swp --level high` |
| ~~8~~ | ✅ **XONG** — **671 SWP · 1.140,7 giờ · 142,6 ngày công**, quy ước 1 SWP = 1,7 giờ. Đã ghi `SWP` + `Giờ ước lượng` lên 269 item và gán Sprint 1 cho 45 ticket. Đối chiếu LAB-1: −60% trên phần giao nhau | `estimate.md` (5 phần) | `gh project item-edit --number-field` · `--iteration-id` |
| ~~9~~ | ✅ **XONG** — chạy Sprint 1 giả lập 10 ngày, đẩy **110 lượt đổi `Status`** lên Project theo từng ngày. Kết quả: **37 Done / 122 SWP = 78%**, `#34` còn 6,6 giờ. 10 rủi ro trễ có chủ và hạn | `reports/261025-GH-buoc-9-progress-report.md` (4 phần) + `…-burndown-sprint-1.png` + `…-progress-report.html` | `tkm:predict-risks` · `tkm:preview-output --html` |
| 10 | `AI-report.md` + `README.md` đầy đủ · soát theo đề · mở thử bằng cửa sổ ẩn danh | bài nộp hoàn chỉnh | `tkm:review-doc --checklist` |

**Hai phụ thuộc giữ nguyên thứ tự:** item phải trên board thì `tkm:estimate-swp` mới đọc được (5→7) ·
phải có số giờ mới cắt được sprint và vẽ được đường kế hoạch burndown (8→9). Cả hai đã thoả.

**Còn ngỏ trước bước 10:** Sprint 2 mới có `#39` `#60`, phần còn lại chưa cắt.

**Vì sao để trống SWP tới bước 8:** `tkm:estimate-swp` mặc định **bỏ qua issue đã có ước lượng**.
Ghi số trước khi chấm thì nửa board bị loại khỏi lượt chấm, phải chạy lại bằng `--reestimate-existing`.

**Vì sao bỏ `Vai phụ trách` và `Tầng`:** kiểm 2026-10-24 — không file đề bài nào trên máy đòi hai cột
này (chúng chỉ xuất hiện trong chính file bàn giao này), và không bước 7–10 nào đọc tới. `Tầng` vốn
chép từ cột cùng tên của 272 dòng mục 6.3 spec LAB-4, công dụng duy nhất là lọc board
(`task-breakdown.md` §1.7). Cần dùng lại thì giá trị rút sẵn được từ dòng `**Tầng:**` trong thân
từng ticket.

**~~Số liệu Sprint 1 để dùng ở bước 8~~ — khối này đã bị bước 8 thay, giữ lại chỉ để truy nguồn.**
Bản cũ tính cho chuỗi T0–T3 (E01 + E02) với đội 1 BE · 1 FE · 1 QA: BE 9 MD · FE 10 MD · QA 6 MD
= 25 MD, kết luận FE 100% / BE 90%, không còn đệm. **Số đang dùng:** đội 2 BE · 2 FE · 1 QA, sức
chứa 94 SWP mỗi vai, Sprint 1 nhận 45 ticket · 157 SWP · 266,9 giờ (BE 88% · FE 79% sức chứa danh
nghĩa — nhưng **95% sức chứa hiệu dụng**, xem `progress-report.md` phần 3). Chỗ mỏng nhất bản cũ
nêu vẫn đúng và vẫn chưa xử: LAB-1 cho 4 MD BE cho "kiểm giới hạn trong ngày" mà LAB-5 rã thành
9 dev task BE.
