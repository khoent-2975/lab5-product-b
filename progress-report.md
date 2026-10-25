# Progress report — Sprint 1 (giả lập)

## Phần 1 — Đầu file

**Lập ngày 25/10/2026.** Bản HTML đọc bằng trình duyệt:
[`261025-GH-buoc-9-progress-report.html`](reports/261025-GH-buoc-9-progress-report.html) — mở thẳng
được, không cần chạy server. Mọi con số về điểm và giờ lấy từ [`estimate.md`](estimate.md).

### Sprint nào, chạy trong bao lâu

- **Tên Iteration trên Project:** `Sprint 1`, bắt đầu 26/10/2026, kéo dài hai tuần.
- **Khoảng thời gian tôi mô phỏng:** từ thứ Hai **26/10** đến thứ Sáu **06/11/2026**, đúng **10
  ngày làm việc**. Sprint đóng sổ Chủ nhật 08/11.
- **Khối lượng nhận vào sprint:** 45 dev task, tổng **157 SWP**, quy ra 266,9 giờ. Chia hai vai:
  back-end 21 ticket (83 SWP), front-end 24 ticket (74 SWP).
- **Đội giả lập:** 2 back-end, 2 front-end, 1 QA. Riêng việc của QA không nằm trên board — lý do
  và hệ quả tôi ghi ở rủi ro R2.

### Tôi mô phỏng theo luật nào

Chạy giả lập không phải là bốc trạng thái cho đẹp. Tôi viết một bộ xếp lịch rồi để nó chạy, với
bốn luật sau:

- **Mỗi người làm được 7 giờ một ngày**, không phải 8. Một giờ còn lại trừ cho họp, review chéo và
  chuyển qua lại giữa các việc.
- **Một ticket chỉ một người làm**, không chia đôi.
- **Code xong chưa phải là xong.** Ticket đi qua một ngày chờ review rồi mới được tính là `Done`.
- **Ticket nào bị chặn thì phải chờ thật**, chỉ vào hàng khi mọi ticket chặn nó đã `Done`.

Thứ tự phụ thuộc tôi lấy từ `BAN-GIAO` mục 3: migration nền phải xong trước thì mọi thứ mới chạy
được; hàm tính giờ lái là hàm thuần nên làm song song được; API route cần migration; màn SCR-28
cần API. Riêng `#286` mở menu SCR-19 phải xong sớm nhất — chưa có nó thì vào `/routes` trả 404 và
cả epic E01 không nghiệm thu được.

### Hai điều cần nói rõ trước khi đọc số

- **Bước này tôi chỉ ghi một trường duy nhất lên board: `Status`.** Điểm SWP, giờ ước lượng và
  sprint giữ nguyên như đã chốt ở bước 8, không đụng tới. Mỗi lần đổi trạng thái tôi đẩy lên
  Project theo đúng ngày của nó, nên mở lịch sử board ra là đọc lại được diễn biến từng ngày.
- **Chia vai có sửa so với bước 8.** Bản `estimate.md` đầu tiên xếp `#285` và `#286` vào
  front-end. Soát lại thì bản rã gốc ghi cả hai là việc back-end, và mã ticket trên board cũng là
  `E12-ST-BE-02` và `E12-ST-BE-03`. Tôi đã trả chúng về back-end. Tổng sprint không đổi — vẫn 45
  ticket, 157 SWP — chỉ ranh giới giữa hai vai dịch đi: back-end từ 19 lên 21 ticket, front-end từ
  26 xuống 24.

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

### Ba cách đọc cùng một sprint, đừng trộn chúng với nhau

- **Làm xong 78%.** Tức 122 trên 157 điểm đã đóng hẳn. Đây là con số tôi mang đi báo cáo.
- **Lập trình xong 86,6%.** Cộng thêm ba ticket đã code xong nhưng còn nằm chờ review, thành 136
  trên 157 điểm. Khoảng chênh giữa hai con số này chính là độ trễ của khâu review.
- **Tiêu hết 90,6% số giờ.** Đội đã bỏ ra 241,9 trong 266,9 giờ dự kiến. Nói cách khác, **chỉ còn
  25 giờ công chưa làm**.

Ba con số lệch nhau khá xa, và lý do đáng chú ý: **bảng điểm hụt 22% trong khi công thực tế chỉ
hụt 9,4%.** Chuyện này xảy ra vì ticket quá to — riêng `#34` đã mang 8 điểm, ba ticket đang chờ
review mang thêm 14 điểm nữa, mà cả bốn đều đã code xong. Một ticket thiếu vài giờ cũng kéo trọn
số điểm của nó sang sprint sau.

### Nhưng mục tiêu sprint vẫn chưa nghiệm thu được

Sprint này đặt mục tiêu làm xong ba phần: dựng tuyến giao hàng, luật giờ lái, và nền tảng dùng
chung. Vướng ở `#34` — đó là khối màn hình nơi người điều phối nhìn bốn dòng kết quả kiểm giờ lái
rồi bấm nút công bố tuyến.

Thiếu nó thì SCR-28 cho phép dựng tuyến nhưng không cho làm gì với tuyến vừa dựng. Đúng cái bẫy mà
bản thiết kế LAB-4 tuyên bố không chấp nhận: dẫn người dùng đi hết một luồng rồi mới báo là ngõ
cụt (xem `PREMISE` mục 3, dòng `V-1`).

---

## Phần 3 — Burndown

![Burndown Sprint 1 — đường thực tế nằm trên đường kế hoạch suốt sprint, kết thúc ở 35 SWP còn lại](reports/261025-GH-buoc-9-burndown-sprint-1.png)

Đường kế hoạch vẽ đơn giản: 157 điểm chia đều cho 10 ngày làm việc. Tôi tách riêng đường back-end
(83 điểm) và front-end (74 điểm), vì hai vai này không gánh việc hộ nhau được. Chỉ ticket đã đóng
hẳn mới được trừ khỏi đường thực tế.

**Đường thực tế nằm trên đường kế hoạch suốt cả sprint**, và sang tuần thứ hai thì hai vai tách
hẳn nhau. Bốn lý do, xếp theo mức đóng góp:

### Một — front-end hết việc từ giữa sprint. Đây là chỗ lệch lớn nhất

Hết ngày thứ 5, front-end đã làm xong toàn bộ 12 ticket vay từ các epic khác, và xong luôn phần
nền tảng của mình. Từ ngày thứ 6 trở đi, ba ticket còn lại đều phải chờ back-end: màn form A chờ
API route, khối đơn chưa phân công chờ hàm lấy danh sách đơn, khối bốn dòng ngưỡng chờ hợp đồng
dữ liệu.

**Ngày thứ 8 là đáy — front-end ngồi không 12,5 trên 14 giờ**, đúng chỗ dải màu trên biểu đồ. Tính
cả sprint, front-end nhàn rỗi **36,1 giờ trên tổng 140 giờ**. Tức là **hơn một phần tư sức người
của vai này bốc hơi chỉ vì chờ**, chứ không phải vì hết việc trên board.

### Hai — back-end thì ngược lại, chạy hết công suất

Suốt 10 ngày back-end chỉ rảnh đúng **2 giờ**. Nếu cộng gộp hai vai thì tổng nhàn rỗi là 38,1 trên
280 giờ, nghe có vẻ chỉ 13,6% — nhưng con số gộp ấy che mất điều quan trọng: gần như toàn bộ phần
nhàn rỗi dồn vào một bên.

Đây chính là rủi ro R5 hiện nguyên hình. Khối lượng việc trên board nghiêng 64% về back-end, trong
khi đội chia đôi 50/50. Trước đây đó mới là một nhận định; sau sprint này nó là con số giờ đo được.

### Ba — hai mắt xích cuối chuỗi về quá muộn

API route đóng sáng ngày thứ 9. Hợp đồng dữ liệu `check_result` đóng sáng ngày thứ 10. Mà khối bốn
dòng ngưỡng phụ thuộc vào hợp đồng đó, lại cần tới 13,6 giờ — chỉ còn một ngày thì làm được 7 giờ,
thiếu 6,6.

Cùng lúc đó, khối đơn chưa phân công không bao giờ đủ điều kiện để bắt đầu, vì ticket chặn nó chỉ
kịp vào trạng thái chờ review. Kéo theo ticket soát chuỗi tiếng Nhật cũng không tới lượt.

Chỗ này tôi cho là **lỗi khi rã ticket, không phải lỗi xếp lịch.** Khối bốn dòng ngưỡng là ticket
front-end to nhất board mà lại nằm ở mắt cuối một chuỗi năm mắt. Dời nó sớm hơn là không thể.

### Bốn — một ngày chờ review, lặp lại suốt sprint

Ngày đầu tiên burndown không trừ được điểm nào, dù sáu ticket đã code xong trong ngày hôm đó —
tất cả đều nằm chờ review tới sáng hôm sau. Đường thực tế vì vậy khởi hành muộn một ngày và giữ
nguyên khoảng cách đó tới cuối. Hết sprint vẫn còn 14 điểm kẹt ở chỗ chờ review.

Cái này không phải trượt tiến độ, mà là **cách đo**: tôi chỉ trừ điểm khi ticket đóng hẳn.

### Còn một chỗ nữa: con số "dùng 83% sức chứa" là ảo

266,9 giờ trên sức chứa danh nghĩa 320 giờ (4 người × 8 giờ × 10 ngày) thì đúng là 83%, nghe như
còn dư chỗ. Nhưng nếu tính trên sức chứa **thật sự dùng được** — 280 giờ, sau khi trừ họp và
review — thì đã là **95%**. Sprint này không hề có đệm ngay từ lúc lên kế hoạch. Tôi ghi chi tiết
ở rủi ro R7.

### Chỗ làm được

Ticket mở menu SCR-19 xong ngay ngày đầu và đóng sáng ngày thứ hai. Nhờ vậy đường dẫn `/routes`
trả về trang thật thay vì lỗi 404 ngay từ ngày thứ hai của sprint, và tiêu chí nghiệm thu đầu tiên
của epic dựng tuyến có đường đi. Hai nhánh nền — migration và hàm tính giờ lái — chạy song song
đúng như thiết kế, không mắt nào trễ.

---

## Phần 4 — Rủi ro trễ

Bảng dưới đây dựng từ hai nguồn. Một là kết quả mô phỏng vừa chạy. Hai là năm góc nhìn chuyên môn
khác nhau — kiến trúc, bảo mật, hiệu năng, trải nghiệm người dùng, và một góc chuyên đi phản biện —
mỗi góc tự đánh giá riêng trước khi so với nhau. Cộng thêm bốn chỗ hụt tôi đã biết từ trước, ghi
trong `estimate.md` mục 2 và mục 5.

**Kết luận chung: cần thận trọng, nhưng chưa tới mức phải dừng.** Mười rủi ro xếp theo mức nặng
giảm dần.

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

**Về chuyện vay 12 ticket cho front-end làm.** Góc hiệu năng bảo vay là đúng: không có chúng thì
front-end còn ngồi không thêm 56 giờ nữa. Góc phản biện bảo chính việc vay đã che mất vấn đề — bỏ
chúng ra thì front-end chỉ còn 44% tải, và ai nhìn cũng thấy ngay đội đang lệch.

*Tôi xử thế này:* vẫn vay, vì đó là cách giảm thiệt hại ngay bây giờ. Nhưng mỗi lần báo tiến độ
phải đưa cả hai con số. Chữa cháy và đo đạc là hai việc khác nhau, đừng để cái trước xoá dấu vết
của cái sau.

**Về chuyện có nên kéo khối bốn dòng ngưỡng lên làm sớm.** Góc trải nghiệm người dùng đòi kéo lên,
vì đó là thứ mang đi demo cuối sprint. Góc kiến trúc nói không kéo được: nó phụ thuộc hợp đồng dữ
liệu, mà hợp đồng lại phụ thuộc cả bốn ticket tính ngưỡng.

*Tôi xử thế này:* góc kiến trúc đúng về **thứ tự** — không thể đảo. Góc trải nghiệm đúng về **phạm
vi** — ticket đó quá to. Không dời được thì phải chẻ nhỏ ra, và đó chính là hành động R1.

### Còn ngỏ

- **Sprint 2 tôi chưa cắt.** Hiện mới có hai ticket được gán sẵn. Khi cắt thì phải áp hai bài học
  của sprint này: trần thật chỉ khoảng 82 điểm mỗi vai chứ không phải 94, và còn phải chừa 12%
  sức chứa cho việc sửa lỗi. Tính ra mỗi vai nhận được khoảng 72 điểm việc mới.
- **Nếu mô phỏng tiếp quá hai sprint thì phải giảm người.** Theo kế hoạch nhân sự của LAB-1, từ
  tháng 01/2027 front-end rút còn 1 người, rồi nửa người. Giữ nguyên 2 người là sai với kế hoạch
  đã gửi khách.
- **Lịch của tôi lệch hai tháng so với kế hoạch thật.** Sprint 1 ở đây bắt đầu 26/10/2026, nhưng
  theo LAB-1 thì lúc đó dự án vẫn đang thiết kế cơ bản — tháng bắt đầu viết code là 12/2026. Đây
  là giả lập cho bài lab, không phải lịch chạy thật.
