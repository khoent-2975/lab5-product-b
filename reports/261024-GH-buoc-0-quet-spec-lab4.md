# Bước 0 — Quét spec LAB-4 ở vai người break task

**Ngày:** 2026-10-24 · **Đề:** LAB-5 Product B (Yuki Cold — chuỗi kho lạnh)
**Nguồn:** `lab4-product-b/specs/` (bản nộp 2026-10-21) · **Đối chiếu estimate:** `lab1-product-b/03-estimate/`

Đây là bản nháp làm việc. Nó nuôi ba file nộp: `PREMISE.md` (§2 §3), `task-breakdown.md` (§2 §4),
`estimate.md` (§5).

---

## 1. Đã đọc gì — và bộ spec cho lại những gì

| Đọc | Số đo | Dùng để |
|---|---|---|
| `00-pham-vi-man-hinh-cot-loi.md` | 15 màn = 13 đã code + SCR-28 + SCR-29 | Khung epic |
| `04-screen-specs/` 15 file | **272 dòng** mục 6.3 *"khoảng cách khách ⟷ prototype, việc treo cho LAB-5"*, mỗi dòng có cột **Tầng** | Nguyên liệu issue |
| nt | **1.035 dòng** AC ở mục 6.4 | Định nghĩa xong của issue |
| `01-architecture.md` §9.1 §11 §12 | 8 mock → 8 điểm tích hợp ngoài; 7 mục *"cái KHÔNG có trong code"* | Epic tích hợp + nợ kỹ thuật |
| `02-database.md` | 39 bảng, 19 bảng append-only | Tầng `DB (migration)` |
| `07-detail-design/` 4 file | `receive_line` · `confirm_pick`+`confirm_load` · `advance_deviation` · `allocate_order` | Ba tầng mỗi lệnh ghi đi qua |
| `05-adr/` 5 bản | 5 hướng đã chốt + phương án đã bỏ | `PREMISE.md` §3 |
| LAB-1 `03-estimate/*.json` | 18 nhóm, mỗi task có sẵn `story_points` + `total_md` | `estimate.md` §5 |

**Điều may cho LAB-5:** LAB-4 viết mục 6.3 với cột `Tầng` nhận đúng sáu giá trị — `DB (migration)` ·
`RPC / luật` · `API route` · `UI` · `dùng chung` · `không code` — và tự nói *"gom cột này của mọi màn
trong cùng một phase là ra Implementation Steps"*. Bản rã task không phải dựng từ đầu, mà là **gom và
chọn** từ 272 dòng đã phân tầng sẵn.

**Điều khó:** 272 dòng không thể thành 272 issue. Phải có luật chọn, và đề đã chừa chỗ cho nó —
`task-breakdown.md` §2 đòi cột *"phần spec chưa thành issue và vì sao"*.

---

## 2. Nháp Spec → Epic (13 epic)

Đặt tên epic bám **nhóm chức năng của LAB-1** để bảng đối chiếu `estimate.md` §5 ghép được 1–1.

| Epic | Màn / nguồn | Dòng 6.3 | Nhóm LAB-1 | LAB-1: SP / MD |
|---|---|---|---|---|
| **E01 Dựng tuyến giao hàng** | SCR-28 | 19 | F06 (FT-06-01) | 26 / 14 |
| **E02 Luật giờ lái 2024 — kiểm trong ngày** | SCR-28 §6.2.1 | (trong 19) | F06 (FT-06-03) | 29 / 16 |
| **E03 Công bố tuyến có phiên bản** | SCR-29 | 18 | F06 (FT-06-05) | 13 / 8 |
| **E04 Điểm nghỉ `休憩`** | SCR-28 #2 · SCR-29 #6 | (trong trên) | F06 (FT-06-04) | 8 / 5 |
| **E05 Ngưỡng giờ lái cộng dồn nhiều ngày** | SCR-28 §6.2.2 | #4 #5 | F06 — *LAB-1 chưa tách* | — |
| **E06 Nhập kho & kiểm hàng** | SCR-12 | 15 | F02 | 91 / 49 |
| **E07 Tồn kho & trạng thái lô** | SCR-18 · SCR-19 | 29 | F03 | 90 / 51 |
| **E08 Đơn hàng & phân bổ** | SCR-20 · SCR-21 | 39 | F04 + F05 | 215 / 122 |
| **E09 Lấy hàng → xuất → POD** | SCR-23 · SCR-24 · SCR-26 | 60 | F05 | (trong trên) |
| **E10 Chuỗi nhiệt độ & sai lệch** | SCR-31 · SCR-32 · SCR-33 | 59 | F07 | 99 / 54 |
| **E11 Truy xuất nguồn gốc** | SCR-35 | 17 | F08 | 60 / 35 |
| **E12 Nền tảng dùng chung & phân quyền** | SCR-00 + xuyên màn | 16 + rải | C · D · F11 | 297 / 159 |
| **E13 Điểm tích hợp mở từ mock M1–M8** | `01-architecture.md` §9.1 | — | F10 | 47 / 27 |

Ba epic **E02 · E04 · E05** là chỗ ràng buộc đặc thù sống — xem §3.

**Chưa gán epic, cố ý:** việc chờ khách trả lời (Q12 · Q13 · Q16 · Q19 · Q34 · Q51 · Q52 · Q53 · Q56)
→ dựng thành **issue làm rõ** riêng, không trộn vào issue thi công, vì chúng không ước được công cho tới
khi có đáp án.

---

## 3. Cụm ràng buộc giờ lái 2024 — vì sao tách riêng, tách thành gì

Điều kiện kích hoạt của đề đã đạt: detail design **có** module lập lịch (SCR-28 tạo tuyến · SCR-29 công bố).

Bốn ngưỡng có cột trong `driver_rule_versions`, bản `DRV-RULE-2026-v1`:

| Ngưỡng | Cột | Giá trị | Toán tử | Sửa bằng cách nào |
|---|---|---|---|---|
| ① `連続運転` Lái liên tục | `max_continuous_drive_min` | 240 phút | `>` nghiêm | đổi thứ tự điểm giao, hoặc chèn nghỉ |
| ② `拘束時間` Thời gian ràng buộc | `max_binding_min_per_day` | 780 phút/ngày | `>` nghiêm | bớt điểm giao, hoặc đổi tài xế |
| ③ nghỉ reset chuỗi lái | `break_reset_min` | 30 phút | `>=` **không** nghiêm | kéo một điểm dừng lên ≥30 phút |
| ④ `ルート時間` Thời lượng tuyến | `max_route_hours` | 24 giờ | `>` nghiêm | chia hai ngày |

**Bốn ngưỡng = bốn issue, không gộp**, vì bốn cách sửa khác nhau và hai toán tử biên khác nhau
(`>` với `>=`). Spec LAB-4 nói thẳng: *"một câu gộp không nói được phải làm gì"* (`AC-28-34` cấm gộp
thành một câu `このルートは法定基準を満たしていません`).

Ngoài bốn ngưỡng, cụm này còn **sáu hạng mục tách rời**:

| # | Hạng mục | Vì sao là issue riêng |
|---|---|---|
| 1 | Khoảng thời gian vi phạm **chính xác** (`AC-28-37`: 12:20 → 15:35, 170 phút vượt) | RFP nghiệm thu đích danh `正確な違反時間範囲を表示`; là thuật toán riêng, không phải hệ quả của ① |
| 2 | Chọn bản luật theo `service_date`, **không** theo `now()` (`R-18`) | Lối tra khác hẳn; và bảng thiếu `unique(valid_from)` → kết quả không xác định |
| 3 | Ghim `driver_rule_version_id` lúc công bố (`R-20`) | Tầng khác (SCR-29), và phải từ chối nếu bản luật đổi giữa lúc kiểm và lúc ghi |
| 4 | Cấu trúc `check_result` jsonb (3 khoá `ok` · `violations` · `ruleVersion`) | Hình dạng một phần tử `violations` **chưa có ví dụ nào** — chờ chốt |
| 5 | Điểm nghỉ `休憩`: chèn được, **chưa có chỗ lưu** | `route_stops` không có cột loại dòng lẫn thời lượng → là migration + đổi `snapshot` |
| 6 | **8/11 ngưỡng FR-SCH-02 chưa phủ** | Hai nhóm chi phí khác hẳn nhau — xem dưới |

**Phủ 3 trong 11 ngưỡng.** Tám ngưỡng còn thiếu chia hai nhóm, và đây là ranh giới ước công quan trọng nhất
của cả bài:

- **Thiếu cột thôi** (960h/năm · 3.300h/năm · 284h/tháng · trần 15h ngày ngoại lệ · nghỉ giữa ca 11h / 9h):
  thêm cột vào `driver_rule_versions`. Nhưng bảng **append-only** → mọi bản cũ phải nhận giá trị mặc định
  có chủ ý. Ước được.
- **Thiếu cả nguồn dữ liệu** (lái bình quân 9h/ngày qua 2 ngày · 44h/tuần qua 2 tuần): cần **giờ đã làm của
  những ngày trước**, hệ chưa có bảng nào ghi. Đây là ⚠ **Q13 chưa có đáp án**; LAB-1 đã ghi mức đổi
  **Vừa→Lớn**. Không ước được tới khi khách trả lời → vào E05, tách khỏi E02.

---

## 4. Chỗ hở và mâu thuẫn phát hiện khi break

### 4.1 Mâu thuẫn mới — chưa dòng nào của LAB-4 xử lý

| # | Chỗ | Mâu thuẫn | Bằng chứng | Xử lý đề xuất |
|---|---|---|---|---|
| **M-1** | SCR-28 ⟷ SCR-29, luồng điểm nghỉ | Chèn 2 điểm nghỉ 30 phút → SCR-28 cho **bốn ngưỡng OK** → nút `公開へ進む` **bật** → sang SCR-29 → SCR-29 **tính lại từ CSDL**, mà điểm nghỉ **không được lưu** → lại vi phạm → `公開する` **tắt**. Người dùng bị dẫn vào ngõ cụt | `AC-28-49` (2 điểm nghỉ → ① ③ thành OK) · `R-13` + `AC-28-50` (nghỉ không lưu, mở lại là mất) · `AC-28-45` (D-2 bật khi bốn OK, **không ghi gì vào CSDL**) · SCR-29 `R-14` (màn **kiểm lại**) · `AC-29-35` (vi phạm → 422 `RULE_ROUTE_VIOLATION`) | **Tạo issue làm rõ.** Ba đường: (a) chỗ lưu điểm nghỉ lên trước, E04 thành chặn của E03; (b) D-2 chỉ bật theo kết quả tính **không có điểm nghỉ**, nghỉ chỉ để xem thử; (c) giữ nguyên, thêm câu cảnh báo ở D-2. Không chọn thay khách được vì (a) đổi phạm vi, (b) làm hỏng mục đích của nút `休憩を挿入` |
| **M-2** | SCR-28 `AC-28-33` ⟷ quyết định `Đ-3` | AC đòi kiểm biên ④ ở **1.440 / 1.441 phút**, nhưng `Đ-3` chốt *"tuyến không vắt qua nửa đêm"* và ② chặn ở 780 phút/ngày. Không dựng được ca dữ liệu hợp lệ nào để ④ chạm 1.440 mà ② vẫn OK | `R-10` tự nhận *"④ là trần dự phòng, ② luôn chạm trước"* · `Đ-3` (6.3 #14) | **Giả định ghi vào PREMISE:** `AC-28-33` nghiệm thu ở tầng **unit test của hàm thuần** `driver-hours.ts`, không qua CSDL. Nếu không, dòng ④ là mã chết — đúng điều chính spec cảnh báo |
| **M-3** | SCR-28 #11 ⟷ SCR-29 #10 | Cùng một lỗ chống gửi trùng (`client_request_id` thiếu ở `routes` và ở `route_versions`), hai màn ghi thành hai dòng riêng | SCR-28 6.3 #11 · SCR-29 6.3 #10 | **Gộp một issue migration**, không tách đôi theo màn. Ghi vào `task-breakdown.md` §1 như một ca của luật chia task |

### 4.2 Chỗ hở LAB-4 đã ghi sẵn — LAB-5 chỉ việc gán tầng và ước công

| Nguồn | Nội dung | Ảnh hưởng break task |
|---|---|---|
| `01-architecture.md` §12 | 7 mục *"cái KHÔNG có trong code"*: phân trang · trang `/lots` · làm mới số đếm · `movements` không ghi khi `confirm_pick` · đổi trạng thái lô không chạm phân bổ · `available` là ngõ cụt · severity 2 cấp ⟷ Q19 giả định 3 cấp | 7 issue nền, 2 trong số đó (**US-05 AC3** phân bổ, **Q19** severity) là **P0 chưa phủ**, không phải nợ nhỏ |
| `00-pham-vi…` §8 | US-05 AC3 **không đạt** · US-11 AC3 mock đã khai · US-11 AC4 **POD không sửa được bằng đường nào** · US-14 AC2 đạt một nửa | 4 issue, mỗi cái gắn thẳng một AC của khách |
| SCR-28 6.3 #6 | **US-12 AC3** — đơn chưa phân công và **lý do từ chối**: không có chỗ sinh, không có chỗ lưu | P0 chưa phủ, nằm trong E01 |
| `PREMISE.md` LAB-4 §1.1 | **FR-REC-03** (số nhận/từ chối/chờ + mã lý do + luồng duyệt) đã bị cắt từ LAB-2 | LAB-1 **vẫn tính công** cho `FT-02-03` → bảng `estimate.md` §5 phải trừ dòng này, nếu không chênh lệch đọc sai |

---

## 5. Giả định và câu hỏi treo (nuôi `PREMISE.md` §2)

LAB-4 đã chốt sáu giả định `GĐ-1`…`GĐ-6` (bỏ `保留` · 30 phút ngoài dải · biên 3℃ · cận dưới −30℃ ·
hai mức severity · 2 cấp ⟷ 3 cấp). **Tất cả đều là giả định vendor, khách chưa xác nhận.**

Riêng module lập lịch có thêm **bảy** điểm chờ khách, chúng **không chặn cả tầng** — phần kiểm trong một
ngày đủ căn cứ làm trước:

| Q | Hỏi gì | Giả định vendor | Mức đổi nếu đáp án khác |
|---|---|---|---|
| Q12 | Người điều phối dựng tuyến hay hệ tự sinh | người dựng, hệ kiểm | khác → **màn khác**, bật FT-06-02 |
| Q13 | Giờ đã làm của những ngày trước lấy từ đâu | tính từ tuyến + sự kiện tài xế, số dư đầu kỳ nhập tay | **Vừa → Lớn** |
| Q16 | "24 giờ" nghĩa là gì | tổng thời gian ước tính một tuyến | — |
| Q34 | Có áp ca đặc biệt (phà, đường dài, ca chia đôi) | không áp | Vừa |
| Q56 | Tuyến có 6 trạng thái hay 2 | 2 (`draft` · `published`) | Nhỏ — chỉ đổi state machine |
| — | Quy ước mã tuyến `route_code` | `R<YYMMDD>-<4 số>` | — |
| — | `routes_driver_service_date_key` ép một tài xế một tuyến/ngày | **chưa có căn cứ nào từ khách** — comment viện dẫn Q13/Q16 mà hai câu đó hỏi việc khác | Lớn nếu khách cần nhiều tuyến/ngày |

Dòng cuối là một **câu hỏi mới phải gửi khách**, không có trong `client-qa-list.md` — phát hiện khi đọc
`R-15`.

---

## 6. Hướng LAB-4 đã chốt (nuôi `PREMISE.md` §3)

| Trụ | Đã chốt | ADR |
|---|---|---|
| Ghi nghiệp vụ | chỉ qua RPC `security definer`; `authenticated` chỉ `grant select` | adr-01 |
| Tầng chứng cứ | append-only ở Postgres, 19 bảng, sửa = thêm dòng | adr-02 |
| Phân quyền | RLS chỉ hai nhóm, chi tiết đẩy lên tầng ứng dụng | adr-03 |
| Trạng thái lô | bỏ `保留`, enum 4 giá trị — **là `GĐ-1`, khách chưa xác nhận** | adr-04 |
| Ranh giới lỗi | `raise` ⟷ `return blocked` định bằng *"có để lại bằng chứng không"* | adr-05 |

Ba quyết định riêng của module lập lịch, chốt ở bước 6 của LAB-4: `Đ-1` tính chặng quay về DEPOT ·
`Đ-2` `サービスタイム` vào ② ④ không vào ① · `Đ-3` tuyến không vắt qua nửa đêm.

---

## 7. Đã chốt (2026-10-24)

| # | Chỗ | Chốt | Hệ quả |
|---|---|---|---|
| 1 | Độ sâu backlog | **~120 issue** — 13 epic · 73 issue theo nhóm (màn × tầng) · 35 nhóm lớn tách thêm sub-issue | Mọi dòng trong 229 dòng ước được truy về một issue. Không dòng nào bị bỏ vì "chưa rõ" |
| 2 | **M-1** điểm nghỉ ⟷ công bố | **Chỗ lưu điểm nghỉ lên trước**, E04 thành chặn của E03 | Sửa thiết kế LAB-4 (`R-13`), ghi vào `PREMISE.md` §1 + §3 như **giả định vendor** — bài lab không hỏi khách được |
| 3 | Sprint 1 | **T0 + T1 + T2 + T3** — migration nền · `driver-hours.ts` · API route · UI SCR-28 | Cuối sprint: dựng tuyến, thấy bốn ngưỡng, lưu nháp được; **chưa công bố được**. Nhánh công bố sang sprint 2 |
| 4 | Quy SWP → giờ | Chốt ở bước 7, sau khi có điểm | — |

### 7.1 Vì sao 229 dòng không thành 229 issue

Một dòng 6.3 mang tầng ghép (`DB + RPC + UI`), nên 272 dòng rải thành **417 lượt gán tầng**, gom lại
thành **73 nhóm (màn × tầng)**; 35 nhóm lớn hơn 4 dòng, tách tiếp thành sub-issue → **~120 issue**.

Chỗ **thật sự** không thành issue thi công chỉ có hai nhóm:

| Nhóm | Dòng | Vì sao |
|---|---|---|
| 2 ngưỡng bình quân nhiều ngày (9h/ngày qua 2 ngày · 44h/tuần qua 2 tuần) | 2 | Thiếu **nguồn dữ liệu**, không phải thiếu cột — chờ Q13. Vẫn ước công theo giả định của LAB-1, kèm mức đổi Vừa→Lớn |
| Dòng `không code` kết luận *"giữ nguyên, nhưng ghi thành quyết định có văn bản"* | 43 | Không sinh dòng code → vào `PREMISE.md` hoặc một issue ghi vết chung |

### 7.2 Thứ tự chạy thật của module lập lịch

```
T0 migration nền ────┐        create_route · set_route_stops
   (chặn tất cả)     │        sequence route_code · client_request_id · unique(valid_from)
                     ├──► T2 API route ──► T3 UI SCR-28
T1 driver-hours.ts ──┘        (hàm thuần, unit test, song song được với T0)

T4 chỗ lưu điểm nghỉ ──► T5 publish_route ──► T6 UI SCR-29     ← M-1 đẩy T4 lên trước
T7 ngưỡng cộng dồn nhiều ngày — chờ Q13, không chặn ai
```
