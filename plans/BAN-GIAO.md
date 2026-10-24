# Bàn giao — LAB-5 Product B (backlog + báo cáo tiến độ)

**Cập nhật:** 2026-10-24 · **Đã xong:** bước 0 → 3 · **Tiếp theo:** bước 4

Thread mới đọc file này trước, rồi đọc `plans/reports/261024-GH-buoc-0-quet-spec-lab4.md` và `PREMISE.md`.

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
| Status | single-select | `PVTSSF_lAHOBf6CDs4Boeimzhm-fqE` | Todo `f75ad846` · In Progress `47fc9ee4` · In Review `eef67101` · Blocked `4cd94c4e` · Done `98236657` |
| Sprint | iteration | `PVTIF_lAHOBf6CDs4Boeimzhm-f2I` | Sprint 1 `af2d180b` (2026-10-26, 14d) · Sprint 2 `e59811eb` (2026-11-09, 14d) |
| SWP | number | `PVTF_lAHOBf6CDs4Boeimzhm-f2U` | điền **sau** khi chấm, chỉ điền điểm đã review |
| Giờ ước lượng | number | `PVTF_lAHOBf6CDs4Boeimzhm-f3k` | điền ở bước 8 |
| Vai phụ trách | text | `PVTF_lAHOBf6CDs4Boeimzhm-f4I` | người phụ trách giả định (配送計画者, 品質管理…) |
| Tầng | single-select | `PVTSSF_lAHOBf6CDs4Boeimzhm-f5E` | DB (migration) `53cad8a9` · RPC / luật `c63257d1` · API route `69aaf7f4` · UI `b1ed7222` · dùng chung `f0b33d08` · không code `e1c9fe6a` |
| Parent issue · Sub-issues progress | native | — | có sẵn, dùng quan hệ cha/con native của GitHub |

---

## 2. Quyết định đã chốt — không mở lại

| # | Chốt |
|---|---|
| 1 | **Backlog ~120 issue**: 13 epic · 73 issue theo nhóm (màn × tầng) · 35 nhóm lớn tách thêm sub-issue. Mọi dòng trong 229 dòng ước được phải truy về một issue |
| 2 | **M-1**: chỗ lưu điểm nghỉ `休憩` làm **trước**, E04 chặn E03. Ghi là giả định vendor (bài lab không hỏi khách được) — `PREMISE.md` §1 + §3 `V-1` `V-2` `V-6` |
| 3 | **Sprint 1** = T0 migration nền + T1 `driver-hours.ts` + T2 API route + T3 UI SCR-28. Nhánh công bố (T4→T6) sang Sprint 2 |
| 4 | Đội giả lập 1 BE · 1 FE · 1 QA, sprint 2 tuần (`GĐ-L5-5`) |
| 5 | Quy SWP → giờ: **chưa chốt**, quyết ở bước 7 sau khi có điểm |
| 6 | Còn thiếu: **mã học viên** trong `README.md` |

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

## 5. Bước còn lại

| # | Việc | Ra cái gì | Skill / công cụ |
|---|---|---|---|
| 4 | Break epic → issue → sub-issue trên giấy. Chốt độ hạt + định nghĩa xong. Cụm giờ lái 2024 tách đủ bốn ngưỡng + sáu hạng mục (khoảng vi phạm · chọn bản luật theo `service_date` · ghim `driver_rule_version_id` · `check_result` · điểm nghỉ · 8/11 ngưỡng chưa phủ) | `task-breakdown.md` (4 phần) | `tkm:estimate` |
| 5 | Tạo ~120 issue thật kèm `--project "LAB-5 Product B — Backlog"`, gắn Issue Type, nối cha/con | issue trên board | `tkm:git-issues` (`create`, `type`, `set-parent`) |
| 6 | Điền Sprint · Status ban đầu · Vai phụ trách · Tầng. **Chưa điền SWP và Giờ** | board đủ trường | `gh project item-edit` |
| 7 | Chấm điểm trên URL Project, review mẫu đại diện, hiệu chỉnh, xuất HTML rồi copy vào repo | báo cáo HTML | `tkm:estimate-swp --level high` |
| 8 | So điểm skill ⟷ điểm mình chốt + lý do · chốt quy ước SWP→giờ · ghi **SWP đã review** và **giờ** lên Project · đối chiếu LAB-1 | `estimate.md` (5 phần) | `gh project item-edit --number-field` |
| 9 | Chạy Sprint 1 giả lập: dịch trạng thái theo ngày, dựng burndown, rủi ro trễ | `progress-report.md` (4 phần) + ảnh burndown | `tkm:predict-risks` · `tkm:preview-output --html` |
| 10 | `AI-report.md` + `README.md` đầy đủ · soát theo đề · mở thử bằng cửa sổ ẩn danh | bài nộp hoàn chỉnh | `tkm:review-doc --checklist` |

**Ba phụ thuộc giữ nguyên thứ tự:** issue phải có trước mới gắn cha/con và điền trường (4→5→6) ·
item phải trên board thì `tkm:estimate-swp` mới đọc được (5→7) · phải có số giờ mới vẽ được đường
kế hoạch burndown (8→9).

**Vì sao để trống SWP tới bước 8:** `tkm:estimate-swp` mặc định **bỏ qua issue đã có ước lượng**.
Ghi số trước khi chấm thì nửa board bị loại khỏi lượt chấm, phải chạy lại bằng `--reestimate-existing`.
