# PREMISE — Tiền đề của backlog LAB-5

**Dự án:** Product B — Yuki Cold (chuỗi kho lạnh thực phẩm) · **Lập ngày:** 2026-10-24
**Backlog rã từ:** bộ thiết kế LAB-4 nộp ngày 2026-10-21 — `lab4-product-b/specs/`

File này trả lời đúng một câu: **backlog LAB-5 khác bản thiết kế LAB-4 ở đâu, và vì sao.**

> **Bài lab không hỏi khách được.** Mọi chỗ RFP để ngỏ đều phải giả định thì mới break task và ước
> công tiếp được. Giả định ghi ở §2, mỗi dòng nói rõ nó lấp chỗ nào và ước công đổi ra sao nếu khách
> trả lời khác. Không giả định nào ghi đè một khối RFP đã nêu rõ.

> **Mã issue** trong file này là mã nội bộ **của vòng phác thảo đầu**, dạng `E01-1` · `E04-2`. Bản rã
> cuối cùng đổi sang dạng khác — `E04-BE-01` · `E02-FE-03` — nên **`task-breakdown.md` không tra được
> bằng mã cũ**; tra bằng epic và tên việc. Số `#` trên GitHub được điền sau khi
> issue được tạo — xem `task-breakdown.md` cho bảng ánh xạ đầy đủ.

---

## 1. Spec thêm / bỏ / sửa so với LAB-4

| Spec (mã/file) | Thêm/Bỏ/Sửa | Trước → sau | Vì sao | Issue bị ảnh hưởng |
|---|---|---|---|---|
| `04-screen-specs/scr-28-tao-tuyen-giao-hang.md` → `R-13`, `AC-28-50` · và `scr-29` §6.3 #6 | **Sửa** | **Trước:** điểm nghỉ `休憩` chèn được để tính nhưng **không lưu được**; `下書き保存` chỉ hiện `M_87` cảnh báo sẽ mất. **Sau:** `route_stops` có chỗ lưu **loại dòng** + **thời lượng nghỉ**; điểm nghỉ đi vào `snapshot.stops` | **Chỗ hở phát hiện khi break.** `AC-28-49` cho phép chèn 2 điểm nghỉ 30 phút → bốn ngưỡng thành `OK` → `AC-28-45` bật nút `公開へ進む`. Nhưng SCR-29 `R-14` **tính lại từ CSDL**, nơi điểm nghỉ không tồn tại → `AC-29-35` trả 422 `RULE_ROUTE_VIOLATION`. Người điều phối bị dẫn vào ngõ cụt, và **không dòng spec nào của LAB-4 xử lý luồng này** | `E04-1` `E04-2` `E04-3` · chặn `E03-1` |
| `04-screen-specs/scr-28-tao-tuyen-giao-hang.md` → `AC-28-33` | **Sửa** | **Trước:** nghiệm thu biên ngưỡng ④ (1.440 / 1.441 phút) bằng **ca dữ liệu qua CSDL**. **Sau:** nghiệm thu ở **unit test của hàm thuần** `lib/rules/driver-hours.ts`, không qua CSDL | **Mâu thuẫn phát hiện khi break.** Quyết định `Đ-3` chốt *"tuyến không vắt qua nửa đêm"*, và ② chặn ở 780 phút/ngày → **không ca dữ liệu hợp lệ nào** đưa ④ chạm 1.440 mà ② vẫn `OK`. Chính `R-10` đã tự nhận ④ là *"trần dự phòng, ② luôn chạm trước"*. Giữ nguyên AC thì dòng ④ là **mã chết** — đúng điều spec cảnh báo | `E02-4` |
| `04-screen-specs/scr-29-cong-bo-tuyen-giao-hang.md` → §2.2, §6.3 #2 | **Thêm** | **Trước:** `check_result.violations` là **mảng rỗng**; hình dạng của một phần tử vi phạm *"chưa có ví dụ nào ở đâu"*, LAB-4 ghi `[LAB-5] chốt`. **Sau:** chốt hình dạng phần tử — xem §3 `V-3` | Không chốt thì `E02` (phép tính) và `E03` (`publish_route` ghi `check_result`) **không ráp vào nhau được**, và hai bên tự định nghĩa hai hình dạng khác nhau | `E02-5` · `E03-3` |

**Không có dòng "Bỏ".** Phạm vi 15 màn của LAB-4 giữ nguyên; không màn nào, không quy tắc nào bị rút
khỏi backlog.

**Không phải nộp lại bộ spec.** Ba thay đổi trên đều nằm trong màn đã có, mô tả được bằng cột
*"Trước → sau"*; không thêm màn, không đổi khuôn biểu mẫu.

---

## 2. Giả định bổ sung

| Giả định | Chỗ spec/RFP để ngỏ | Ảnh hưởng tới issue / estimate |
|---|---|---|
| **GĐ-L5-1** — Điểm nghỉ lưu bằng **hai cột trên `route_stops`** (loại dòng + số phút nghỉ), **không** dựng bảng riêng | LAB-4 `scr-28` §6.3 #2 ghi nguyên văn: *"một cột phân loại dòng trên `route_stops` cộng một cột thời lượng, **hoặc** một bảng riêng — **LAB-5 chọn và đặt tên, spec không tự đặt**"* | `E04` = 3 đầu việc lúc phác thảo (migration · `publish_route` dựng `snapshot` · UI chèn nghỉ); rã ra thành **10 issue `#57`–`#66`, trong đó 5 dev task**. Khách muốn bảng riêng → thêm 1 bảng + phép trộn hai nguồn khi dựng `snapshot`, SP của `E04-1` và `E04-2` đều tăng |
| **GĐ-L5-2** — Nguồn giờ đã làm của những ngày trước: **tính từ tuyến và sự kiện tài xế trong hệ thống; số dư đầu kỳ nhập tay lúc go-live** | **Q13 khách chưa trả lời** (`client-qa-list.md`). Đây là giả định **của chính LAB-1**, dùng lại để ước công cho nhất quán | `E05` (2 ngưỡng bình quân nhiều ngày) ước được theo giả định này. LAB-1 ghi mức đổi **Vừa → Lớn**: đáp án khác thì phải bật FT-06-07 và thêm một màn nhập số dư |
| **GĐ-L5-3** — Giữ ràng buộc **một tài xế một tuyến mỗi ngày** | Chỉ mục `routes_driver_service_date_key` có comment viện dẫn `(Q13/Q16)`, nhưng **không câu nào trong hai câu đó hỏi về việc này** — tức ràng buộc **chưa có căn cứ nào từ khách**. Phát hiện khi đọc `R-15`; cần một câu hỏi mới gửi khách | Giữ nguyên = 0 công thêm. Khách cần nhiều tuyến/ngày → bỏ chỉ mục, đổi cách định danh tuyến, sửa `create_route` → mức **Lớn** |
| **GĐ-L5-4** — Kế thừa nguyên vẹn sáu giả định `GĐ-1`…`GĐ-6` của LAB-4 (bỏ `保留` · 30 phút ngoài dải · biên `3℃` · cận dưới `−30℃` · hai mức severity · 2 cấp ⟷ 3 cấp) | `lab4-product-b/specs/PREMISE.md` §2.1 — cả sáu đều *"giả định vendor, khách chưa xác nhận"* | Không đổi estimate so với LAB-4. Riêng `GĐ-6` (2 ⟷ 3 cấp severity) đã được LAB-1 ghi *"mỗi mức một luồng duyệt → thêm workflow"* → `E10` ước theo **2 cấp**, ghi sẵn mức đổi |
| **GĐ-L5-5** — Đội giả lập: **2 BE · 2 FE · 1 QA**, sprint **2 tuần**, 5 ngày làm việc/tuần | Bài lab không có đội thật. Lấy đúng số người LAB-1 đã chốt cho **tháng xây dựng đầu tiên (2026/12)** trong kế hoạch người theo tháng gửi khách — BE 2 người, FE 2 người, QA 1 người (`lab1-product-b/04-proposal/monthly_staffing_plan.py`, chốt 2026-10-08). Bản trước ghi 1 BE · 1 FE là bố trí ít hơn một nửa phần BE so với con số đã báo khách | Quyết năng lực sprint → đường kế hoạch của burndown trong `progress-report.md`. Không ảnh hưởng SP hay giờ của từng issue. ⚠ LAB-1 giảm người dần từ 2027/01 (FE còn 1, rồi 0,5); mô phỏng quá 2 sprint thì sức chứa phải giảm theo |

Năm giả định trên **chỉ lấp chỗ để ngỏ**. Không dòng nào đè lên một khối RFP đã nêu rõ: bốn ngưỡng
giờ lái (240 · 780 · 30 · 24h), ba dải nhiệt, bảy vai trò, mã cá thể bò 10 chữ số đều giữ nguyên
giá trị RFP.

---

## 3. Hướng đã chốt

| Vấn đề | Các phương án ở LAB-4 | Phương án chốt | Vì sao |
|---|---|---|---|
| **V-1** Tuyến đạt ngưỡng **nhờ điểm nghỉ** thì SCR-28 bật nút công bố, SCR-29 lại chặn | LAB-4 **không nêu phương án nào** — chỗ hở này do bước 0 của LAB-5 phát hiện. Ba đường rút ra khi break: (a) chỗ lưu điểm nghỉ lên trước · (b) nút `公開へ進む` chỉ bật theo kết quả **không tính** điểm nghỉ · (c) giữ nguyên, thêm câu cảnh báo ở nút | **(a)** — chỗ lưu điểm nghỉ làm trước, `E04` thành chặn của `E03` | (b) làm hỏng mục đích của nút `休憩を挿入`: **US-29 AC2** đòi *vị trí và thời lượng nghỉ hiện trên lịch trình tài xế*, muốn vậy thì phải lưu được. (c) để người dùng đi hết một luồng rồi mới biết là ngõ cụt — thứ duy nhất spec LAB-4 tuyên bố không chấp nhận (`R-13`: *"mất dữ liệu im lặng"*) |
| **V-2** Chỗ lưu điểm nghỉ đặt ở đâu | cột trên `route_stops` · bảng riêng (`scr-28` §6.3 #2) | **Cột trên `route_stops`** | `snapshot.stops` là **một mảng theo `seq`**; dòng nghỉ phải nằm đúng thứ tự giữa các điểm giao. Bảng riêng buộc `publish_route` trộn hai nguồn rồi sắp lại — thêm một chỗ sai mà không đổi lại được gì |
| **V-3** Hình dạng một phần tử `check_result.violations` | LAB-4 đề xuất *"bám bốn ngưỡng của SCR-28"*, để `[LAB-5] chốt` | `{ "threshold": "continuous_drive" \| "binding" \| "break_reset" \| "route_hours", "measured": <phút>, "limit": <phút>, "from": "HH:MM", "to": "HH:MM", "overMinutes": <phút> }` — ba khoá `from`/`to`/`overMinutes` chỉ có ở `continuous_drive` | Bốn mã ngưỡng khớp đúng bốn cột của `driver_rule_versions`. Ba khoá cuối là thứ `AC-28-37` bắt buộc hiện (*khoảng vi phạm chính xác 12:20 → 15:35, 170 phút vượt*) — để ngoài thì bản đã công bố không tự giải thích được. **Ba khoá cấp trên `ok` · `violations` · `ruleVersion` giữ nguyên**, không đụng tới bản seed `R-SEED-01` |
| **V-4** `driver_rule_versions` thiếu `unique (valid_from)` → hai bản cùng ngày thì tra ra kết quả **không xác định** | thêm `unique (valid_from)` · thêm tiebreaker `created_at desc` vào câu tra (`scr-28` §6.3 #10) | **Thêm `unique (valid_from)`** | Bảng cùng họ `temperature_threshold_versions` **đã có** `unique (temp_zone, valid_from)` — làm khác đi là để hai bảng cùng họ lệch nhau. Tiebreaker chỉ giấu triệu chứng: dữ liệu vẫn cho phép hai bản cùng hiệu lực một ngày |
| **V-5** `routes.start_time` nullable → tuyến lưu được mà bốn ngưỡng không tính ra số nào | đổi cột thành `not null` · giữ nullable và bắt màn hiện `C-12` thay vì bốn dòng `OK` giả (`scr-28` §6.3 #9) | **Giữ nullable** — như LAB-4 đã chọn cho vòng đầu | Một tuyến đang dựng dở có quyền chưa có giờ xuất phát. Đổi `not null` còn kéo theo xử lý dòng seed cũ, mà không mua thêm gì cho người dùng |
| **V-6** `snapshot` phải mang được dòng nghỉ mà **không phá** bản `R-SEED-01` đã nằm trong CSDL | LAB-4 cảnh báo *"hình dạng `snapshot` đã bị `R-SEED-01` cố định, thêm khoá phải có chủ ý"* (`scr-29` §2.2) | Giữ **đúng 6 khoá cấp trên**; thêm hai khoá vào **phần tử** của `stops`: `stopType` (mặc định `"delivery"`) và `breakMinutes` (`null` cho điểm giao) | Phần tử cũ của `R-SEED-01` đọc lên vẫn hợp lệ, khoá thiếu hiểu theo mặc định. Thêm ở cấp trên thì bản seed thiếu khoá và mọi chỗ đọc phải có nhánh phòng thủ |
