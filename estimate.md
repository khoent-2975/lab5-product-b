# Estimate — LAB-5 Product B

**Lập ngày:** 2026-10-24 · **Bước 8**

**Báo cáo HTML của skill chấm điểm:** [`reports/261024-GH-buoc-7-estimate-swp.html`](reports/261024-GH-buoc-7-estimate-swp.html)
— mở thẳng bằng trình duyệt, không cần chạy server.

> **Một chỗ trong báo cáo HTML đọc sẽ nhầm.** Nó ghi 18% khối lượng là *"Bug/Rework"*. Sản phẩm này
> chưa dựng xong dòng code nào, lấy đâu ra bug mà sửa. Skill xếp nhầm 45 ticket, vì thân ticket hay
> viết theo lối *"hôm nay hệ thống làm ngược lại"* nên nó tưởng là đi sửa lỗi. Điểm số không sai, chỉ
> cái nhãn sai. Đừng dùng con số *"Kế hoạch 548 / Bug-Rework 123"* ở đâu cả.

Board: https://github.com/users/khoent-2975/projects/1

| | |
|---|---|
| Tổng công | **671 SWP** · 1.140,7 giờ · **142,6 ngày công** |
| Dao động | 602 – 746 SWP |
| Đổi điểm ra giờ | **1 SWP = 1,7 giờ** |
| Sprint 1 | 45 ticket · 157 SWP · 266,9 giờ |

---

## 1. Skill chấm bao nhiêu, tôi chốt bao nhiêu

Chạy `tkm:estimate-swp --level high --label type:devtask --no-push-kpi` đọc thẳng từ GitHub Project.

Skill chấm 176 dev task. Còn 54 task cha, 26 story và 13 epic thì nó chỉ cộng điểm của con lên, không
chấm lại — nếu chấm lại thì một việc bị tính hai lần. 38 câu hỏi gửi khách không ước công, vì hỏi
khách thì chưa biết làm gì mà ước.

Cách chấm: mỗi ticket trả lời hai câu hỏi — việc này **rộng** tới đâu, và việc này **khó** tới đâu.
Rộng là Scope, khó là Complexity. Hai câu trả lời tra vào một bảng cố định, ra một con số là SWP. Cái
lợi của bảng cố định: cùng một mô tả việc thì luôn ra cùng một điểm, không phụ thuộc hôm đó ai chấm.

Skill tự chọn 5 ticket đại diện rồi hỏi tôi. Nó không chọn bừa — mỗi ticket đại diện cho một chỗ khác
nhau của thang điểm, để nếu thang bị lệch thì lộ ra.

| Issue | Skill chấm | Tôi chốt | Vì sao chọn ticket này | Lý do tôi sửa |
|---|---|---|---|---|
| `#24` E02-BE-01 — thêm `unique(valid_from)` | S1 × C0 → **1** | S2 × C1 → **3** | Nhẹ nhất board. Xem đáy thang có bị đặt thấp quá không | Skill thấy bảng cùng họ đã có khuôn sẵn để chép nên coi là việc vặt. Nhưng chép khuôn thì vẫn phải viết migration, chạy nó, kiểm lại, và chuẩn bị đường lùi nếu hỏng. Mức 1 điểm nên để dành cho việc sửa một hằng số thôi |
| `#239` E10-18-BE-05 — giới hạn 1000 ký tự cho ghi chú | S2 × C1 → **3** | S3 × C1 → **4** | Nằm giữa bảng điểm, chỗ đông ticket nhất. Xem khúc giữa có lệch không | Skill tưởng chỉ thêm một chỗ kiểm. Thật ra phải làm cho **ba cột** ghi chú, và còn chưa ai quyết đặt giới hạn ở đâu — ràng buộc `check` của bảng, hay viết trong RPC. Ba cột cộng với một chỗ chưa quyết thì đủ nhích lên một bậc |
| `#297` E13-ST-BE-01 — bỏ đăng nhập demo, dùng OIDC của khách | S8 × C5 → **24** | S8 × C5 → **24** | Nặng nhất board. Xem đỉnh thang có bị thổi không | **Tôi giữ nguyên.** Hai AI chấm riêng bằng hai mô hình khác nhau đều ra đúng 24. Việc này đụng vào mọi đường 401 của cả 15 màn, thêm xác thực hai lớp, thêm xác thực thiết bị — rộng thật và rủi ro thật |
| `#301` E13-ST-BE-05 — chuyển 6 nguồn dữ liệu thật của khách | S8 × C3 → **16** | S8 × C3 → **16** | Lệch xa phần còn lại nhất. Xem có phải điểm bị thổi không | **Tôi giữ nguyên**, dù AI thứ hai hạ xuống 10. Nó lý luận là việc vẫn nằm trong một tầng cơ sở dữ liệu. Nhưng sáu nguồn là sáu bộ chuyển đổi riêng, mà chính ticket cũng thừa nhận chưa biết sáu nguồn đó định dạng ra sao, sạch bẩn thế nào. Chưa biết gì về dữ liệu đầu vào thì không có cơ sở để hạ điểm |
| `#153` E08-08-BE-01 — kiểm lại ②④⑤ trong `allocate_order` | S3 × C2 → **5** | S5 × C2 → **8** | Hai AI chấm lệch nhau. Xem bên nào đúng | Cả hai AI chỉ nhìn công viết lần đầu, và đúng là việc gọn trong một hàm. Chỗ cả hai bỏ sót: sau việc này, **cùng một luật sẽ nằm ở hai nơi — TypeScript và SQL**. Mỗi lần luật đổi là phải sửa cả hai và nhớ giữ chúng khớp nhau. Cái giá đó trả dài, không nằm ở lần viết đầu |

### Sửa một ticket thì những ticket giống hệt nó cũng đổi theo

Khi tôi sửa điểm một ticket, skill không áp con số mới cho cả board. Nó đi tìm những ticket **giống
hệt về bốn mặt** — cùng nghề, cùng loại việc, cùng kiểu rộng, cùng kiểu khó — rồi dịch điểm của chúng
đúng bằng số bậc tôi vừa dịch. Giống gần gần thì không tính.

| Nhóm ticket giống hệt | Tôi dịch | Sinh từ | Kéo theo |
|---|---|---|---:|
| API · tính năng · nhiều thành phần · có thuật toán | rộng thêm 1 bậc | `#153` | 1 ticket (`#62`) |
| API · tính năng · một thành phần · việc thường quy | rộng thêm 1 bậc | `#239` | 13 ticket |
| DB · migration · một thành phần · việc thường quy | rộng 1, khó 1 | `#24` | 1 ticket (`#25`) |

Kết quả: **646 → 671 SWP**, tăng 3,9%. 18 ticket đổi điểm — **3 cái tôi sửa** (`#24` `#239` `#153`; `#297` và `#301` tôi xem lại rồi giữ
nguyên) **cộng 15 cái ăn theo**. 158 ticket giữ nguyên. Không ticket nào bị đụng tới nếu nó không nằm đúng trong một trong ba nhóm trên.

<details>
<summary>18 ticket đổi điểm</summary>

`#24` 1→3 · `#25` 3→5 · `#28` 3→4 · `#30` 1→3 · `#31` 3→4 · `#32` 3→4 · `#62` 3→5 · `#105` 3→4 ·
`#108` 1→3 · `#132` 3→4 · `#144` 1→2 · `#153` 5→8 · `#178` 3→4 · `#227` 3→4 · `#228` 3→4 ·
`#239` 3→4 · `#268` 3→4 · `#277` 3→4
</details>

### Cho một AI khác chấm lại chỗ rủi ro

Cờ `--level high` bắt skill chạy thêm một AI nữa, **dùng mô hình khác**, chấm lại 9 ticket rủi ro
nhất: ticket từ 13 điểm trở lên, ticket skill tự nhận là không chắc, ticket thiếu thông tin. Hai AI
không thấy bài của nhau. Điểm chính thức vẫn lấy của AI thứ nhất — AI thứ hai chỉ để chỉ ra chỗ nên
nhìn kỹ.

Kết quả: **2 ticket hai bên khớp hệt nhau, 4 ticket cùng điểm nhưng phân loại khác, 3 ticket lệch
nhẹ, không ticket nào lệch lớn.**

| Ticket | AI thứ nhất | AI thứ hai |
|---|---:|---:|
| `#301` chuyển 6 nguồn dữ liệu | 16 | 10 |
| `#298` ba định dạng logger | 6 | 5 |
| `#153` kiểm ②④⑤ | 8 (tôi đã sửa) | 3 |

Phải nói thẳng một điều: hai AI đồng ý **không** chứng minh điểm đúng. Chúng hoàn toàn có thể sai
giống nhau.

### Chỗ nào chấm chắc, chỗ nào không

109 ticket chấm chắc, 63 ticket tạm được, **4 ticket không chắc**. Bốn cái không chắc cộng lại 21
điểm: `#87`, `#88`, `#119` — cả ba đều rơi vào nhánh chưa ai quyết của E06 và E07 — cộng `#298`.
Không ticket nào to tới mức phải tách nhỏ.

Chạy với `--no-push-kpi` nên điểm nằm im trong báo cáo, không đẩy sang KPI Insight của công ty.

---

## 2. Đổi điểm ra giờ thế nào

**Chốt: 1 SWP = 1,7 giờ công của BE hoặc FE.**

### Vì sao không ước giờ thẳng cho từng ticket

Có hai đường. Một là ngồi ước giờ cho từng ticket. Hai là chấm điểm rồi nhân với một tỉ lệ.

Tôi chọn đường hai. Ước giờ thẳng cho 176 ticket thì mỗi ticket là một lần đoán riêng, chẳng ai kiểm
lại được, và hai ticket na ná nhau dễ ra hai con số khác hẳn. Chấm điểm bằng bảng cố định thì chỉ còn
**một** con số phải tranh luận: tỉ lệ đổi. Sai tỉ lệ thì sửa một chỗ, cả board đổi theo.

### Tỉ lệ 1,7 lấy ở đâu ra

Chuỗi việc của Sprint 1 — dựng nền, viết hàm tính giờ lái, làm API, làm màn SCR-28 — quy ra board
đúng bằng **E01 cộng E02**: 35 issue, 22 dev task, khớp chính xác. LAB-1 đã ước cho đúng phần đó:
**BE 9 ngày, FE 10 ngày**, tức 19 ngày công dev. Board chấm phần đó 92 điểm.

```
19 ngày × 8 giờ ÷ 92 điểm = 1,65 giờ cho 1 điểm   →   làm tròn 1,7
```

### Áp cho nhất quán

- **Mọi** ticket dev nhân cùng một tỉ lệ. Không ngoại lệ, không ai được chỉnh tay con số của riêng mình
- Ticket cha cộng giờ của con lên, không tự tính lại
- 38 câu hỏi khách để trống cả điểm lẫn giờ
- Giờ làm tròn một chữ số thập phân

### Ba tỉ lệ tôi đã cân, và vì sao loại hai cái

| Lấy từ đâu | giờ/điểm | Thành tổng | Vì sao loại |
|---|---:|---:|---|
| E01+E02, tính cả công QA | 2,2 | 184,5 ngày | Trộn công QA vào tỉ lệ, trong khi board không có một ticket QA nào. Nhân lên sẽ ra con số nói dối về công dev |
| **E01+E02, chỉ BE và FE** | **1,7** | **142,6 ngày** | **Đã chọn** |
| Cả phần so được với LAB-1 | 4,2 | 352,3 ngày | Cách này ngầm cho rằng LAB-5 làm hết những gì LAB-1 ước. Không đúng — LAB-5 chỉ làm 15 trong 44 màn |

Ba con số chênh nhau **2,5 lần**. Không phải phép đo hỏng. Lý do là độ sâu rã task giữa các epic rất
lệch nhau — mục 5 nói rõ chỗ này.

> Tỉ lệ 1,7 dùng để **chia việc trong sprint**. Đừng dùng để **báo giá**. Nó rút ra từ một cặp epic,
> mà đúng cặp đó lại là chỗ LAB-5 rã kỹ nhất board.

### Đội bao nhiêu người

`GĐ-L5-5` ban đầu để **1 BE, 1 FE, 1 QA**. Con số đó sai so với bài đã nộp. LAB-1 có một kế hoạch
người theo tháng, chốt ngày 2026-10-08 và gửi khách; theo lịch trong đó, **tháng xây dựng đầu tiên là
12/2026** với **BE 2 người, FE 2 người, QA 1 người** — và BE giữ 2 người suốt ba tháng liền tới
02/2027.

Đã sửa `GĐ-L5-5` thành **2 BE · 2 FE · 1 QA** cho khớp. Sức chứa một sprint hai tuần thành **94 điểm
mỗi vai** thay vì 47.

Sửa xong thì Sprint 1 không còn phải cắt gì: cả E01 và E02 vào trọn vẹn, đúng như `BAN-GIAO` mục 2 #3
đã chốt từ đầu. Năm ticket tôi định hoãn — `#6`, `#10`, `#11`, `#15`, `#31` — quay lại hết.

Hai chỗ còn lệch, ghi để nhớ: LAB-1 **giảm người dần** từ 01/2027 (FE còn 1, rồi 0,5), nên mô phỏng
quá hai sprint thì sức chứa phải tụt theo. Và **lịch không khớp** — Sprint 1 của LAB-5 bắt đầu
26/10/2026, trong khi theo LAB-1 lúc đó còn đang thiết kế cơ bản, chưa ai viết code.

### Vì sao không rã việc QA

Backlog **không có ticket QA nào**, và đó là chủ ý. Bộ mẫu ticket của công ty có sẵn
`06-test-design` và `07-test-execution`, LAB-5 chỉ dùng 4 mẫu: epic, story, dev task, câu hỏi khách.

Lý do: **QA phải có thang điểm riêng.** Một điểm của việc viết test case không bằng một điểm của
việc viết code — hai loại việc đo bằng hai thước khác nhau. Nhét chung vào một thang rồi cộng lại thì
con số tổng mất nghĩa: không biết 671 điểm là bao nhiêu công dev, bao nhiêu công kiểm thử, và tỉ lệ
đổi ra giờ cũng không còn đúng cho bên nào. **Bài lab này chỉ rã và chấm việc dev.**

Hệ quả, ghi để người đọc không hiểu nhầm con số:

- **142,6 ngày công là công dev thuần.** Không gồm QA
- LAB-1 ước QA **235 ngày công** cho cả dự án, nặng thứ hai sau BE. Riêng phần LAB-5 chạm tới là
  **92 ngày QA trên 354 ngày công dev** của chính LAB-1 cho đúng phần đó ⇒ **tỉ lệ QA : dev = 26%**.
  Áp tỉ lệ ấy lên 142,6 ngày công dev của LAB-5 ⇒ **khoảng 37 ngày công QA**. ⚠ Đừng cộng thẳng 92
  vào 142,6 — 92 thuộc thang phạm vi rộng hơn của LAB-1, cộng vào là thành +64,5% chứ không phải 26%
- Đội vẫn có 1 QA theo `GĐ-L5-5`, nhưng việc của người đó không nằm trên board này
- Burndown ở bước 9 vì vậy chỉ vẽ được việc dev

---

## 3. Tổng theo epic

| Epic | Số issue | Dev task | Tổng SWP | Tổng giờ | Ghi chú |
|---|---:|---:|---:|---:|---|
| E01 Dựng tuyến | 20 | 12 | 52 | 88,4 | Sprint 1 |
| E02 Luật giờ lái trong ngày | 15 | 10 | 40 | 68,0 | Sprint 1 |
| E03 Công bố có phiên bản | 21 | 15 | 55 | 93,5 | Phải chờ E04 xong — `PREMISE` §3 `V-1` |
| E04 Điểm nghỉ | 10 | 5 | 19 | 32,3 | Việc mới hoàn toàn, LAB-1 không ước cho nó dòng nào |
| E05 Ngưỡng nhiều ngày | 8 | 4 | 19 | 32,3 | Chờ khách trả lời Q13 |
| E06 Nhập kho | 27 | 13 | 45 | 76,5 | |
| E07 Tồn kho và trạng thái lô | 26 | 16 | 49 | 83,3 | |
| E08 Đơn hàng và phân bổ | 35 | 19 | 55 | 93,5 | |
| E09 Lấy hàng đến POD | 44 | 27 | 83 | 141,1 | Nhiều issue nhất |
| E10 Chuỗi nhiệt độ | 44 | 26 | 102 | 173,4 | **Nặng nhất board** |
| E11 Truy xuất | 22 | 10 | 32 | 54,4 | |
| E12 Nền tảng dùng chung | 21 | 11 | 32 | 54,4 | **Nghi rã thiếu** — xem mục 5. Một phần vào Sprint 1 |
| E13 Tích hợp ngoài M1–M8 | 14 | 8 | 88 | 149,6 | **Rã thô nhất** — 11 điểm một ticket, cả board trung bình 3,8 |
| **Tổng** | **307** | **176** | **671** | **1.140,7** | 38 issue còn lại là câu hỏi khách, không ước công |

---

## 4. Chia việc cho Sprint 1

### Hai nguyên tắc chia

**Một — việc nền làm trước.** Màn nào, API nào mà thứ khác phải đứng lên trên nó thì làm trước.

**Hai — chia cho khớp sức người đang có.** Lấy ticket xuống tới khi mỗi người đủ việc. Hết ticket cha
thì lấy vài ticket con của cái tiếp theo. Miễn là không ai ngồi không, không ai thiếu việc. Cuối
sprint đối chiếu xem có làm đủ đúng những gì đã giao không.

Đội 2 BE và 2 FE, mỗi người 10 ngày công trong sprint hai tuần. Sức chứa **94 điểm mỗi vai**, tức
160 giờ.

### Nguyên tắc một: xếp theo lớp nền

| Lớp nền | Việc | Ai làm |
|---|---|---|
| Nền dưới cùng | Mở menu để vào được màn, trang báo lỗi và trang 404 dùng chung | FE |
| Nền dữ liệu | Migration dựng bảng, thêm cột, thêm ràng buộc | BE |
| Nền luật | Hàm thuần tính giờ lái, không đụng cơ sở dữ liệu | BE |
| Trên nền | API route | BE |
| Trên API | Màn SCR-28 | FE |

Xếp theo lớp thì lòi ra một thứ cách chia cũ bỏ sót: **`#286` mở menu cho SCR-19.** Hôm nay vào
`/routes` trả 404, mà `AC-28-01` của chính E01 đòi lật cờ menu để trả 200. Không có `#286` thì màn
SCR-28 không mở ra được mà nghiệm thu. Nó phải nằm trong Sprint 1.

Ba epic nền vào trọn: **E01 dựng tuyến, E02 luật giờ lái, E12 nền tảng chung.** Cộng lại BE 83 điểm,
FE 41 điểm.

### Nguyên tắc hai: lấp cho FE đủ việc

BE 83 trên 94 là ổn. FE mới 41 trên 94, còn ngồi không hơn nửa sprint. Phải thêm việc cho FE.

Chỗ lấy: **142 điểm việc FE chạy được ngay mà không chờ BE**, nằm rải ở 8 epic. Sở dĩ có nhiều việc
như vậy là vì LAB-2 đã dựng prototype — phần lớn ticket FE là đi sửa màn đã có, không phải dựng màn
mới, nên không phụ thuộc API nào chưa viết.

Lấy theo thứ tự epic, gần chuỗi tuyến đường trước:

| Lấy từ | Ticket | Điểm |
|---|---:|---:|
| E03 công bố tuyến | `#50` `#51` `#52` `#54` | 12 |
| E06 nhập kho | `#83` `#84` | 4 |
| E07 tồn kho | `#111` `#112` `#113` `#121` `#122` `#123` | 17 |
| | | **33** |

FE lên 74 điểm. Vẫn thấp hơn BE 9 điểm — bước 9 đo ra chỗ chênh đó thành 36,1 giờ FE nhàn rỗi.

### Sprint 1 chốt — 45 ticket, 157 điểm, 266,9 giờ

| Vai | Ticket | Điểm | Giờ | Sức chứa |
|---|---:|---:|---:|---:|
| BE | 21 | 83 | 141,1 | **88%** |
| FE | 24 | 74 | 125,8 | **79%** |
| **Tổng** | **45** | **157** | **266,9** | **83%** |

> ⚠ **Sửa sau khi soát bước 9.** Bản đầu xếp `#285` và `#286` vào FE (BE 19/79, FE 26/78). Bản rã
> gốc ghi cả hai là *Development - Backend*, cha `[PARENT][BE]`, mã ticket trên board là
> `E12-ST-BE-02` / `E12-ST-BE-03`. Đã trả về BE. Tổng sprint không đổi.

**BE — 21 ticket · 83 điểm**

| Nhóm | Ticket |
|---|---|
| E01 dựng tuyến | `#5` `#6` `#7` `#8` `#9` `#10` `#11` |
| E02 luật giờ lái | `#24` `#25` `#26` `#27` `#28` `#29` `#30` `#31` `#32` |
| E12 nền tảng chung | `#276` `#277` `#284` `#285` `#286` |

**FE — 24 ticket · 74 điểm**

| Nhóm | Ticket |
|---|---|
| E12 nền tảng chung | `#279` `#280` `#281` `#288` `#289` `#290` |
| E01 màn SCR-28 | `#12` `#13` `#14` `#15` `#16` |
| E02 khối C trên SCR-28 | `#34` |
| E03 màn SCR-29 | `#50` `#51` `#52` `#54` |
| E06 màn nhập kho | `#83` `#84` |
| E07 màn tồn kho | `#111` `#112` `#113` `#121` `#122` `#123` |

Sprint 2 hiện còn 2 ticket `#39` và `#60` gán từ trước. **Phần còn lại chưa chia.**

### Phần sửa bug tính ở đâu

**Board không có một ticket sửa bug nào.** Tôi đã kiểm cả ba cách: không ticket nào mang nhãn
`qa-bug`, `uat-bug` hay `production-bug`; không tiêu đề nào có `[BUG]`; không ticket nào thuộc loại
bug. 176 dev task đều là việc dựng mới.

Nghĩa là: QA chưa test nên bug chưa sinh ra, nhưng công sửa bug của những việc làm ở Sprint 1 **vẫn
sẽ phải trả** — chỉ là trả ở các sprint sau, khi QA test tới. Hiện công đó **không nằm trong 142,6
ngày** ở mục 2, vì không có ticket nào mang nó.

LAB-1 có chừa chỗ cho phần này: nhóm *"Kiểm thử hệ thống và yêu cầu phi chức năng"* được **41 ngày
công BE và FE** — đó chính là công sửa những gì kiểm thử tìm ra. LAB-5 chưa rã nhóm đó thành ticket.

Hai cách xử lý, chọn một ở sprint sau:

- **Chừa sẵn chỗ:** mỗi sprint từ số 2 trở đi để dành một phần sức chứa cho sửa bug của sprint trước,
  không nhận hết việc mới. Lấy tỉ lệ từ LAB-1 là 41 trên 354 ngày, tức khoảng 12% công dev
- **Sinh ticket khi có bug thật:** dùng mẫu `08-qa-bug` của công ty, tạo ticket lúc QA báo. Số thật
  hơn nhưng không lên kế hoạch trước được

### Vì sao một epic bị xé ra nhiều sprint

~~Chỉ 2 trong 13 epic tự nó buộc phải chia hai sprint — E10 và E13, vì riêng phần BE của chúng vượt
sức chứa một sprint.~~ **Sai, và sai từ thời đội còn 1 BE.** Với sức chứa 94 SWP mỗi vai thì
**không epic nào tự nó buộc phải chia hai sprint**: BE của E10 là 63 SWP, BE của E13 là 67 SWP, cả
hai đều dưới 94. Câu cũ đúng khi sức chứa còn 47.

Việc bị xé là hệ quả của **hình dạng việc không khớp hình dạng đội**, chứ không phải epic to. Cả
board là 64% việc BE, 36% việc FE. Đội 2 BE và 2 FE là 50/50. Hai con số sức chứa không đổi chỗ cho
nhau được — FE rảnh không gánh hộ BE.

Với đội hiện tại, cả board cần tối thiểu **5 sprint cho BE** nhưng chỉ **3 sprint cho FE**. Nên sprint
nào cũng phải vay việc FE từ epic khác để FE khỏi ngồi không — đúng như Sprint 1 vừa vay 12 ticket
của E03, E06, E07.

Chỗ này nối với một phát hiện ở mục 5: **E12 nền tảng chung hụt 90% so với LAB-1**. Nền tảng chung là
nơi sinh ra nhiều việc FE nhất. Rã thiếu chỗ đó thì FE không có việc. Bổ sung cho đủ E12 thì FE tự
khắc đầy, và con số hụt 90% cũng tự co lại. Hai triệu chứng, một nguyên nhân.

## 5. So với estimate LAB-1

LAB-1 ước cho **72 feature, 44 màn**. LAB-5 rã backlog cho **15 màn** mà LAB-4 đã thiết kế. Hai phạm
vi khác nhau nên chỉ so được phần giao nhau, và chỉ so **BE với FE**, vì board không có việc QA.

| Phần | LAB-1 | LAB-5 | Chênh | Vì sao |
|---|---:|---:|---:|---|
| Lộ trình và giờ ràng buộc — E01…E05 | 33 ngày | 39,3 ngày | **+19%** | LAB-4 soi kỹ 15 màn này, tìm ra 272 chỗ bản mẫu còn hở. Riêng **E04 là việc mới hoàn toàn**: chỗ lưu điểm nghỉ do `PREMISE` §3 `V-1` và `V-2` chốt, LAB-1 không ước cho nó dòng nào. E02 cũng phình thêm vì `V-3` chốt hình dạng `check_result` và `V-4` thêm `unique(valid_from)` |
| Nhập hàng và kiểm hàng — E06 | 36 ngày | 9,6 ngày | −73% | LAB-5 chỉ làm một phần màn của nhóm này |
| Tồn kho, lô, ba dải nhiệt — E07 | 39 ngày | 10,4 ngày | −73% | Như trên |
| Hạn dùng và giao hàng — E08 | 29 ngày | 11,7 ngày | −60% | Như trên |
| Xuất hàng, POD, khiếu nại — E09 | 63 ngày | 17,6 ngày | −72% | Như trên |
| Nhiệt độ, sai lệch, HACCP — E10 | 41 ngày | 21,7 ngày | −47% | Hụt ít hơn các nhóm khác vì LAB-4 có soi nhóm này. `GĐ-L5-4` giữ hai mức cảnh báo thay vì ba nên chưa phát sinh thêm luồng duyệt |
| Truy xuất và thu hồi — E11 | 28 ngày | 6,8 ngày | −76% | Như trên |
| Nền tảng chung — E12 | 65 ngày | 6,8 ngày | **−90%** | **Bất thường, nghi rã thiếu** — xem bên dưới |
| Tích hợp bên ngoài — E13 | 20 ngày | 18,7 ngày | **−7%** | Gần bằng nhau. Thay 8 mock bằng tích hợp thật là việc LAB-1 gộp rất thô, LAB-5 rã ra mới thấy hết |
| **Tổng** | **354 ngày** | **142,6 ngày** | **−60%** | |

LAB-1 còn **255 ngày công BE và FE** mà LAB-5 không đụng tới: dữ liệu gốc 52, báo cáo và xuất bằng
chứng 43, bảo mật và phân quyền 37, kiểm thử hệ thống 41, chuyển đổi dữ liệu 50, đào tạo và hỗ trợ
sau go-live 32.

> ⚠ LAB-1 vẫn tính công cho `FT-02-03` (`FR-REC-03`) mà LAB-2 đã cắt bỏ. Cột LAB-1 ở dòng E06 chưa
> trừ phần đó nên hơi cao hơn thực tế.

### Ba điều rút ra

**Một — chênh lệch giữa các epic trải từ −90% tới +19%, hơn hai lần.** Không một tỉ lệ đổi giờ nào
đúng được cho cả board. Đây là lý do tỉ lệ 1,7 chỉ dùng để chia việc trong sprint, không dùng để báo
giá.

**Hai — phần hụt phần lớn là thật và hợp lý.** LAB-5 chỉ làm 15 trong 44 màn. E06 hụt 73% nhiều khả
năng chỉ có nghĩa là LAB-5 chạm một phần nhóm đó, chứ không phải ước thiếu.

**Ba — hai chỗ bất thường, phải xử lý chứ đừng lấy hệ số san cho phẳng:**

- **E01 đến E05 vượt 19%, và E13 chỉ hụt 7%**, trong khi các nhóm khác hụt từ 47 tới 76%. Đúng hai
  chỗ LAB-4 soi kỹ nhất. LAB-5 nhìn ra việc mà LAB-1 không thấy. Đây là tín hiệu tốt, nó chứng minh
  công rã spec có giá trị.
- **E12 nền tảng chung hụt 90%.** LAB-1 cho 65 ngày, nhiều nhất trong nhóm nền tảng; board chỉ có 32
  điểm trên 11 dev task. Chỗ này không đổ cho phạm vi màn được, vì nền tảng chung thì màn nào cũng
  dùng. **Nghi rã thiếu, cần soi lại backlog.**

Thêm một chỗ nên để mắt: **E13 chỉ có 8 dev task mà 88 điểm** — trung bình 11 điểm một ticket, trong
khi cả board trung bình 3,8. Rã thô nhất backlog. Đổi ra giờ sẽ cho những con số khó tin ở mức từng
ticket.

---

## Bước tiếp theo

Bước 9 ✅ **xong** — Sprint 1 giả lập đã chạy 10 ngày, 110 lượt đổi `Status` đã đẩy lên Project.
Kết quả: **37/45 ticket Done · 122/157 SWP · 78%**, `#34` còn 6,6 giờ. Bảng rủi ro 10 dòng có chủ
và hạn. Xem [`progress-report.md`](progress-report.md)
(bản HTML: [`reports/261025-GH-buoc-9-progress-report.html`](reports/261025-GH-buoc-9-progress-report.html)).

Hai con số bước 9 rút ra phải áp khi cắt Sprint 2: trần thực tế **~82 SWP mỗi vai** chứ không phải
94 (sức chứa 83% ở mục 4 là đo trên giờ danh nghĩa; trên giờ hiệu dụng đã là 95%), và chừa **12%**
cho công sửa bug của Sprint 1 ⇒ mỗi vai nhận khoảng **72 SWP việc mới**.

Bước 10 — `AI-report.md` + `README.md` đầy đủ, soát theo đề, mở thử bằng cửa sổ ẩn danh.
