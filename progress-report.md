# Progress report — Sprint 1 (giả lập)

## Phần 1 — Đầu file

**Lập ngày:** 2026-10-25 · **Bước 9**

**Bản HTML đọc được bằng trình duyệt:** [`261025-GH-buoc-9-progress-report.html`](reports/261025-GH-buoc-9-progress-report.html)
— tự chứa, không cần chạy server. **Số liệu điểm và giờ:** [`estimate.md`](estimate.md).

**Iteration trên Project:** `Sprint 1` · Project số 1 · `af2d180b` · bắt đầu 2026-10-26, dài 14 ngày
**Khoảng thời gian giả lập:** Thứ 2 **26/10/2026 → Thứ 6 06/11/2026** — 10 ngày làm việc. Sprint đóng Chủ nhật 08/11/2026.
**Phạm vi:** 45 dev task · **157 SWP** · 266,9 giờ (BE 21 ticket / 83 SWP · FE 24 ticket / 74 SWP)
**Đội:** 2 BE · 2 FE · 1 QA (`GĐ-L5-5`) — việc QA không nằm trên board, xem rủi ro R2

**Luật mô phỏng:** 7 giờ dev hiệu dụng mỗi người mỗi ngày (8 giờ trừ họp, review chéo, chuyển ngữ
cảnh) · một ticket một người · dev xong → `In Review` một ngày → `Done` · ticket chỉ vào hàng chờ
khi mọi ticket chặn nó đã `Done`. Thứ tự lấy từ `BAN-GIAO` mục 3: T0 migration nền chặn tất cả ·
T1 `driver-hours.ts` chạy song song T0 · T2 API route cần T0 · T3 màn SCR-28 cần T2 · `#286` mở
menu SCR-19 đi trước mọi thứ.

**Chỉ trường `Status` được ghi ở bước này.** `SWP`, `Giờ ước lượng`, `Sprint` giữ nguyên như bước 8.
Mỗi lượt đổi `Status` được đẩy lên Project theo đúng từng ngày, nên lịch sử board đọc lại được.

> **Chia vai sửa so với bước 8.** `estimate.md` bản đầu xếp `#285` và `#286` vào FE. Bản rã gốc
> (`task-breakdown.md`) ghi cả hai là *Development - Backend*, cha là `[PARENT][BE]`, và mã ticket
> trên board là `E12-ST-BE-02` / `E12-ST-BE-03`. Đã sửa về BE. Tổng sprint không đổi (45 ticket ·
> 157 SWP · 266,9 giờ); chỉ ranh giới hai vai đổi: BE 19→**21** ticket, FE 26→**24**.

---

## Phần 2 — Trạng thái cuối sprint

| Trạng thái | Số issue | Tổng SWP | Ghi chú |
|---|---:|---:|---|
| `Done` | 37 | 122 | 78% điểm đã cam kết |
| `In Review` | 3 | 14 | `#10` dải nhiệt xe ⟷ hàng · `#11` đơn chưa phân công · `#14` form A — dev xong N9, chưa kịp merge |
| `In Progress` | 2 | 12 | `#34` khối C bốn dòng ngưỡng (**còn 6,6 giờ**, chỉ bắt đầu được từ N10) · `#277` bộ đếm cảnh báo (còn 3,1 giờ) |
| `Blocked` | 1 | 3 | `#54` soát 18 chuỗi Nhật — đội không có người bản ngữ |
| `Todo` | 2 | 6 | `#15` khối đơn chưa phân công (chờ `#11`) · `#16` soát 22 chuỗi Nhật (chờ `#15`) |
| **Tổng** | **45** | **157** | |

Ba con số nói ba chuyện khác nhau, đừng trộn:

- **78%** — điểm đã `Done` (122/157). Đây là con số báo cáo.
- **86,6%** — điểm đã xong việc dev (`Done` + `In Review`, 136/157). Phần chênh là độ trễ review.
- **90,6%** — **giờ** dev đã tiêu (241,9 / 266,9 giờ). Chỉ **25,0 giờ** công chưa làm.

Board hụt 22% nhưng công chỉ hụt 9,4%. Chênh lệch nằm ở hạt ticket: `#34` một mình mang 8 SWP, và
ba ticket `In Review` mang thêm 14 SWP nữa — tất cả đều đã xong việc dev.

Mục tiêu sprint (E01 dựng tuyến + E02 luật giờ lái + E12 nền tảng chung) **chưa nghiệm thu được**:
`#34` là chỗ người điều phối đọc bốn dòng ngưỡng và bấm nút công bố. Thiếu nó thì SCR-28 dựng được
tuyến mà không hành động được trên tuyến đó — đúng cái ngõ cụt `PREMISE` §3 `V-1` nói LAB-4 không
chấp nhận.

---

## Phần 3 — Burndown

![Burndown Sprint 1 — đường thực tế nằm trên đường kế hoạch suốt sprint, kết thúc ở 35 SWP còn lại](reports/261025-GH-buoc-9-burndown-sprint-1.png)

Đường kế hoạch tính từ 157 SWP chia đều 10 ngày làm việc, tách riêng BE 83 và FE 74 vì hai vai
không đổi chỗ cho nhau được. Chỉ ticket `Done` mới trừ khỏi đường thực tế.

**Đường thực tế nằm trên đường kế hoạch suốt cả sprint**, và hai vai tách nhau rõ từ tuần thứ hai.
Bốn chỗ lệch, theo thứ tự đóng góp:

**Một — FE cạn việc nửa sau sprint. Đây là chỗ lệch lớn nhất.** Hết N5, FE đã làm xong toàn bộ 12
ticket vay của E03/E06/E07 và phần E12 của mình. Từ N6 trở đi ba ticket còn lại đều bị chặn:
`#14` chờ `#9` (API route), `#15` chờ `#11`, `#34` chờ `#32`. **N8 là đáy: FE nhàn rỗi 12,5 trên 14
giờ** — chỗ dải màu trên biểu đồ. Cả sprint FE nhàn rỗi **36,1 giờ trên 140**, tức **26% sức chứa
của vai này bốc hơi vì chờ**, không phải vì thiếu việc trên board.

**Hai — BE thì ngược lại, bão hoà tuyệt đối.** Cả 10 ngày BE chỉ nhàn rỗi **2,0 giờ**. Hai vai cộng
lại 38,1 trên 280 giờ hiệu dụng (13,6%), nhưng con số gộp đó giấu mất sự thật: gần như toàn bộ phần
nhàn rỗi dồn vào một vai. Đây chính là rủi ro R5 — board lệch 64% BE / 36% FE trong khi đội 50/50 —
hiện ra thành giờ đồng hồ cụ thể.

**Ba — hai mắt xích cuối chuỗi về quá muộn.** `#9` (API route) `Done` sáng N9, `#32` (hợp đồng
`check_result` theo `V-3`) `Done` sáng N10. `#34` phụ thuộc `#32`, cần 13,6 giờ, mà chỉ còn **một
ngày** — xong được 7, còn 6,6. Và `#15` không bao giờ đủ điều kiện vì `#11` chỉ kịp vào `In Review`,
kéo theo `#16` cũng không tới lượt. Đây là lỗi **rã ticket**, không phải lỗi xếp lịch: `#34` là
ticket FE to nhất board và nằm ở mắt cuối một chuỗi năm mắt.

**Bốn — độ trễ review một ngày, lệch có hệ thống.** N1 không trừ được điểm nào: `#286`, `#83`,
`#111`, `#112`, `#113`, `#121` đều xong việc trong ngày đầu nhưng nằm ở `In Review` tới sáng N2.
Đường thực tế vì vậy khởi hành muộn một ngày. Cuối sprint vẫn còn 14 SWP kẹt ở `In Review`. Đây
không phải trượt tiến độ, đây là cách đo.

Thêm một chỗ đáng ghi: **sức chứa 83% là con số đánh lừa.** 266,9 giờ trên sức chứa danh nghĩa 320
giờ (4 người × 8 giờ × 10 ngày) đúng là 83%. Nhưng trên sức chứa **hiệu dụng** 280 giờ thì là
**95%**. Sprint này không hề có đệm — xem R7.

**Điểm sáng:** `#286` xong ngay N1 và `Done` sáng N2, nên `/routes` trả 200 thay vì 404 từ ngày thứ
hai và `AC-28-01` của E01 có đường nghiệm thu. Nhánh nền T0 + T1 chạy song song đúng như thiết kế,
không mắt nào trong hai nhánh đó trễ.

---

## Phần 4 — Rủi ro trễ

Nguồn: `tkm:predict-risks --level high` (năm tiếng nói: Kiến trúc · Bảo mật · Hiệu năng · UX · Phản
biện) chạy trên kết quả mô phỏng, cộng bốn chỗ hụt đã biết từ `estimate.md` mục 2 và mục 5.
**Phán quyết chung: CAUTION.** Xếp theo mức nặng giảm dần.

| Rủi ro | Issue | Ảnh hưởng tới mốc nào | Hành động | Ai làm, khi nào |
|---|---|---|---|---|
| **R1 — Mục tiêu Sprint 1 không nghiệm thu được.** `#34` còn 6,6 giờ nhưng nó là chỗ bấm nút công bố. SCR-28 dựng được tuyến mà không hành động được | `#34` | `AC-28-37` (hiện khoảng vi phạm chính xác) · `AC-28-45` (bật nút `公開へ進む`) · demo cuối Sprint 1 | Tách `#34` làm hai: bốn dòng ngưỡng **chỉ đọc** đóng trước, phần gating nút công bố tách thành ticket riêng. 8 SWP ở mắt cuối chuỗi là hạt quá to cho một sprint | FE-1 · ngày đầu Sprint 2 (09/11) |
| **R2 — Board KHÔNG có việc QA, burndown chỉ vẽ được việc dev.** QA cần thang điểm riêng nên bài lab không rã cho QA. 142,6 ngày công là **công dev thuần** | cả board — 0 ticket QA trong 307 item | Mọi mốc nghiệm thu. LAB-1: **92 ngày QA trên 354 ngày dev** của chính nó cho cùng phạm vi ⇒ tỉ lệ **QA : dev = 26%**; áp lên 142,6 ra **~37 ngày công QA** nằm ngoài con số đó | Không trích 142,6 ngày ở bất kỳ đâu mà không kèm câu "chưa tính ~37 ngày QA (+26%)". **Đừng cộng thẳng 92 vào 142,6** — 92 thuộc thang phạm vi rộng hơn của LAB-1. Rã việc QA bằng thang đo riêng trước khi con số này đi ra ngoài | PM + QA lead · trước khi chốt báo giá |
| **R3 — Không ticket nào mang công sửa bug.** Việc làm ở Sprint 1 sẽ sinh bug khi QA test tới, công sửa vẫn phải trả nhưng hiện không ticket nào gánh | cả board — 0 nhãn `qa-bug`/`uat-bug`/`production-bug`, 0 tiêu đề `[BUG]`, 0 issue loại bug | Sức chứa từ Sprint 2 trở đi. LAB-1 chừa **41 ngày công BE+FE** cho nhóm kiểm thử hệ thống, tức **~12% công dev** | Chừa 12% sức chứa mỗi sprint từ Sprint 2: nhận ~83 SWP/vai thay vì 94. Hoặc sinh ticket mẫu `08-qa-bug` khi QA báo — số thật hơn nhưng không lên kế hoạch trước được. ⚠ 41 ngày của LAB-1 phần lớn là hỗ trợ UAT, kiểm tải và tinh chỉnh, nên 12% chỉ là số thay thế tạm | PM · khi cắt Sprint 2 |
| **R4 — E12 nền tảng chung nghi rã thiếu 90%.** LAB-1 cho 65 ngày công BE+FE, board chỉ 32 SWP tức 6,8 ngày | E12 `#273`–`#293` | Mọi epic sau đều đứng trên E12. **Nếu sprint nào trượt ở nhánh nền thì đây là nguyên nhân đáng ngờ nhất** | Sprint 1 đóng được 9 trong 11 ticket E12 (`#277` còn dở), không sự cố kỹ thuật nào — nhưng đó là bằng chứng **yếu**: nó chỉ nói về phần *đã* rã, không nói gì về 90% còn thiếu. Soi lại backlog E12 đối chiếu 65 ngày của LAB-1 | BA + tech lead · trong Sprint 2, trước khi cắt Sprint 3 |
| **R5 — Board lệch 64% BE / 36% FE trong khi đội 50/50.** BE cần 5 sprint, FE chỉ cần 3 | cả board | Mọi sprint. Sprint 1 đã đo được thành giờ: **BE nhàn rỗi 2,0 h, FE nhàn rỗi 36,1 h** trên cùng 140 giờ sức chứa | Chọn một: đổi tỉ lệ sang 3 BE / 1 FE từ Sprint 3 (va với kế hoạch người của LAB-1, phải báo khách), **hoặc** bổ sung E12 cho đủ — nền tảng chung là nơi sinh việc FE nhiều nhất. R4 và R5 là hai triệu chứng của một nguyên nhân | PM · quyết trước Sprint 3 |
| **R6 — Hợp đồng `check_result` giao tay giữa hai vai vào ngày cuối.** `#32` chốt hình dạng `V-3`, `#34` tiêu thụ nó. Hợp đồng chạy qua ranh giới BE ⟷ FE ở N10 | `#32` → `#34` | E03 SCR-29 ở Sprint 2 cũng đọc `check_result` — cùng một hợp đồng, cùng một chỗ vỡ | Tách hợp đồng khỏi phần cài đặt: chốt kiểu TypeScript dùng chung + một bộ fixture JSON ngay N1 Sprint 2, FE dựng trên fixture mà không chờ BE code xong | BE-1 + FE-1 · N1 Sprint 2 |
| **R7 — Sức chứa 83% đo sai mẫu số, và tỉ lệ 1,7 giờ/SWP là lập luận vòng tròn.** 266,9/320 giờ danh nghĩa = 83%, nhưng 266,9/280 giờ hiệu dụng = 95%. Thêm nữa, tỉ lệ 1,7 rút ra từ đúng E01+E02 — đúng cặp epic sprint này chạy | — | Cách cắt mọi sprint sau. Sprint 2 trở đi sẽ cắt quá tay nếu vẫn lấy 94 SWP/vai | Cắt sprint theo 7 giờ/người/ngày: trần thực tế ~82 SWP/vai, không phải 94. Khi sang epic ngoài E01/E02, đo lại tỉ lệ bằng số thật của sprint đó thay vì giữ 1,7 | PM · khi cắt Sprint 2 |
| **R8 — `#9` kiểm quyền ba lớp không có đường nghiệm thu độc lập.** Đây là ticket an-toàn-trọng-yếu duy nhất của sprint, và không QA nào soát nó (xem R2) | `#9` | An toàn truy cập của cả 15 màn | Bắt buộc review chéo BE-2 cộng một bộ test quyền tự động chạy trong CI trước khi đóng. Không đóng `#9` bằng lời khai của người viết nó | BE-2 · trong Sprint 2 |
| **R9 — Đội không có người bản ngữ tiếng Nhật.** 40 chuỗi Nhật mới của SCR-28 và SCR-29 không ai soát được | `#54` (Blocked) · `#16` (chưa tới lượt) | Nghiệm thu phần chữ của SCR-28 và SCR-29. Với khách Nhật đây là loại lỗi dễ thấy nhất và rẻ nhất để sửa | Đặt lịch một người bản ngữ ngoài đội, gộp 40 chuỗi vào một lượt soát. Không thu xếp được thì hạ xuống rủi ro chấp nhận và ghi vào biên bản sprint review | PM · trước 09/11 |
| **R10 — 12 ticket FE vay từ E03, E06, E07 không thuộc mục tiêu Sprint 1.** Kéo vào chỉ để FE khỏi ngồi không. Chúng trượt thì **không chặn ai** | `#50` `#51` `#52` `#54` `#83` `#84` `#111` `#112` `#113` `#121` `#122` `#123` — 33 SWP | **Không mốc nào.** Phải tách khỏi đường tới hạn khi đánh giá — trừ `#54`, nó nằm trong R9 vì lý do khác | Báo tải FE bằng **hai** con số: có việc vay 74/94 = 79%, không có việc vay **41/94 = 44%**. Con số thứ hai mới là tình trạng thật, và nó chính là R5 | PM · mỗi lần báo tiến độ |

### Hai chỗ năm tiếng nói cãi nhau

**Hiệu năng ⟷ Phản biện, về 12 ticket vay.** Hiệu năng nói việc vay là đúng: không có nó thì FE
nhàn rỗi thêm 56 giờ nữa. Phản biện nói việc vay che mất vấn đề — bỏ nó ra thì FE chỉ 44% tải và ai
cũng thấy ngay đội lệch. *Xử:* giữ việc vay (giảm thiểu) nhưng báo cáo cả hai con số (đo lường).
Giảm thiểu và đo lường là hai việc khác nhau, đừng để cái trước xoá dấu cái sau.

**UX ⟷ Kiến trúc, về `#34`.** UX đòi kéo `#34` lên sớm vì nó là thứ đem đi demo. Kiến trúc nói
không kéo được: `#34` phụ thuộc `#32`, mà `#32` phụ thuộc cả bốn ticket ngưỡng. *Xử:* Kiến trúc
đúng về **thứ tự**, UX đúng về **phạm vi** — không dời được thì phải chẻ nhỏ. Đó là R1.

### Còn ngỏ

- **Sprint 2 chưa cắt** — hiện mới có `#39` và `#60`. Cắt theo trần 82 SWP/vai (R7) và chừa 12% cho
  sửa bug (R3) thì mỗi vai nhận khoảng 72 SWP việc mới.
- **Mô phỏng quá 2 sprint phải giảm sức chứa** — LAB-1 giảm FE dần từ 01/2027 (còn 1 người, rồi
  0,5). `PREMISE` `GĐ-L5-5`.
- **Lịch lệch hai tháng** — Sprint 1 của LAB-5 bắt đầu 26/10/2026, còn theo kế hoạch LAB-1 thì lúc
  đó dự án đang thiết kế cơ bản, tháng xây dựng đầu tiên là 12/2026.
