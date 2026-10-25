# AI-report — LAB-5 Product B

**Lập ngày:** 2026-10-25 · Ba phần: **skill và prompt** · **cách review output của AI** · **điểm đặc biệt trong cách dùng AI**.

Bài này AI làm phần lớn khối lượng. Giá trị của tôi nằm ở chỗ **chặn những gì nó làm sai** — mục 2
liệt kê tám chỗ, trong đó ba chỗ nếu để lọt thì bảng ước công hoặc biểu đồ burndown sai.

---

## 1. Dùng skill nào, viết prompt thế nào

### 1.1 Skill cho từng việc

| Bước | Skill / công cụ | Ra cái gì |
|---|---|---|
| 0 Quét spec LAB-4 | Claude đọc thẳng `lab4-product-b/specs/` | `reports/261024-GH-buoc-0-quet-spec-lab4.md` — 272 dòng mục 6.3, 1.035 dòng AC, 8 mock |
| 4 Rã task | Claude, nhiều lượt theo từng epic | `task-breakdown.md` — 307 item, 6.824 dòng |
| 5 Tạo issue | `gh issue create` · `gh api` (sub-issue native) | 307 issue `#1`–`#307` + cây 4 cấp trên Project 1 |
| 7 Chấm điểm | **`tkm:estimate-swp --level high`** | `reports/261024-GH-buoc-7-estimate-swp.html` |
| 8 Quy giờ, cắt sprint | `gh project item-edit` (`--number-field`, `--iteration-id`) | `estimate.md` + `SWP`/`Giờ` trên 269 item, `Sprint` trên 47 item |
| 9 Chạy sprint giả lập | **`tkm:predict-risks --level high`** · **`tkm:preview-output --html`** · skill `dataviz` | `reports/261025-GH-buoc-9-progress-report.md` + `.html` + ảnh burndown |
| 10 Soát bài nộp | **`tkm:review-doc`** — ba tác nhân soát song song, mỗi nhóm tài liệu một tác nhân | 13 lỗi tìm ra và đã sửa · `README.md` · file này |

Mô phỏng Sprint 1 ở bước 9 **không phải AI bốc trạng thái**. Tôi bắt nó viết một bộ xếp lịch
(2 BE · 2 FE, 7 giờ hiệu dụng/người/ngày, đồ thị phụ thuộc T0→T3) rồi chạy. Chỗ trượt là **kết quả
của mô hình**, không phải lựa chọn kể chuyện — `#34` còn 6,6 giờ vì `#32` chỉ xong ngày thứ 10, chứ
không phải vì tôi muốn có một ticket trượt cho đẹp báo cáo.

### 1.2 Prompt và cờ

Hai câu lệnh có cờ đáng nói:

```
tkm:estimate-swp --level high --label type:devtask --no-push-kpi
tkm:predict-risks --level high
```

| Cờ | Vì sao để | Hệ quả thật |
|---|---|---|
| `--level high` (chấm điểm) | Bắt chạy thêm **một mô hình thứ hai** chấm lại 9 ticket rủi ro nhất, hai bên không thấy bài của nhau | Lòi ra 3 ticket lệch. Nặng nhất là `#153`: mô hình một chấm 5, mô hình hai chấm 3 — không phải lệch lớn, nhưng đủ để tôi mở ra xem và cuối cùng tự nâng lên 8 |
| `--label type:devtask` | Chỉ chấm **176 dev task**, bỏ 54 task cha / 26 story / 13 epic | Không tính hai lần. Cấp trên cộng điểm của con lên |
| `--no-push-kpi` | Không đẩy điểm sang KPI Insight của công ty | Đây là bài lab, số không phải số thật của dự án nào |
| `--level high` (rủi ro) | 5 tiếng nói, mỗi tiếng chốt riêng trước khi so | Ra hai chỗ **cãi nhau thật** (xem `progress-report.md` phần 4) |

Chỗ tôi phải nói rõ trong prompt chứ không để AI tự đoán:

- **Cấu trúc file nộp.** Bước 9 tôi không để nó tự đặt 4 phần của `progress-report.md`, tôi đưa
  đúng khung: đầu file · bảng trạng thái · burndown · bảng rủi ro có cột *ai làm, khi nào*. Lần
  trước để nó tự đặt thì nó đẻ ra mục thứ năm.
- **Ràng buộc chỉ được ghi `Status`.** Bước 9 dễ nhất là tiện tay sửa luôn `SWP` cho khớp. Tôi cấm
  trước, và kiểm lại sau khi chạy: 262 item ngoài Sprint 1 vẫn nguyên `Todo`, ba trường kia không đổi.
- **Năm thứ bắt buộc phải vào phần rủi ro.** Liệt kê thẳng trong prompt, vì đó là những chỗ *board
  không có dữ liệu* nên AI đọc board sẽ không bao giờ tự thấy.

### 1.3 Cách dùng Agent ghi SWP và giờ lên Project

Đây là chỗ tôi **không** để AI gõ tay từng lệnh. Ghi 269 con số bằng 269 lệnh rời thì vừa chậm vừa
không kiểm lại được. Cách đã dùng, ba bước:

1. **AI sinh dữ liệu, không ghi thẳng.** Skill chấm xong thì xuất ra bảng `issue → SWP`. Tôi đọc
   bảng đó, sửa 3 ticket, rồi mới cho ghi. Giờ ước lượng **không chấm riêng** mà tính bằng
   `SWP × 1,7` ngay lúc sinh lệnh — một công thức, không có chỗ cho AI tự ý làm tròn khác nhau giữa
   các ticket.
2. **Gom thành một truy vấn GraphQL, không gọi `gh` 269 lần.** Mỗi item là một alias
   `updateProjectV2ItemFieldValue` trỏ đúng `fieldId` của `SWP` và `Giờ ước lượng`. Bước 9 làm y hệt
   cho `Status`: 109 lượt đổi gom thành **10 truy vấn, mỗi ngày mô phỏng một truy vấn**, nên lịch sử
   board đọc lại được theo ngày chứ không phải một cục.
3. **Đọc lại board sau mỗi lượt ghi và so với nguồn.** `gh project item-list --format json` rồi đối
   chiếu từng item. Bước 9 so 45 item với kết quả mô phỏng: **0 lệch**. Bước ghi `Người phụ trách`
   còn bắt được một lỗi thật — gom 45 alias vào một truy vấn thì GitHub **chỉ thực thi 23 và không
   báo lỗi gì**. Không đọc lại thì mất 22 ticket mà không ai biết. Sửa bằng cách chia lô 10.

Bài học của bước này: **một truy vấn trả về thành công không có nghĩa là nó đã làm hết việc.** Phải
đếm lại ở phía nhận.

## 2. Review output của AI

### 2.1 Con người kiểm ở những bước nào

| Kiểm gì | Bằng cách nào | Kết quả |
|---|---|---|
| Điểm của skill | Skill tự chọn **5 ticket đại diện** trải khắp thang điểm (nhẹ nhất `#24`, giữa bảng `#239`, nặng nhất `#297`, lệch xa nhất `#301`, hai AI bất đồng `#153`) | Sửa 3, giữ nguyên 2. Kéo theo 13 ticket cùng kiểu → **646 → 671 SWP** |
| Điểm chỗ rủi ro | Mô hình thứ hai chấm lại 9 ticket, mù bài của nhau | 2 khớp hệt · 4 cùng điểm khác phân loại · 3 lệch nhẹ · **0 lệch lớn** |
| Tổng công | Đối chiếu **estimate LAB-1** từng nhóm chức năng | Chênh từ **−90% tới +19%** — chính chỗ chênh bất thường là chỗ phát hiện ra vấn đề |
| Tỉ lệ quy giờ | Cân **ba** cách tính, viết rõ vì sao loại hai | Chọn 1,7 giờ/SWP; ba con số chênh nhau 2,5 lần nên ghi kèm giới hạn dùng |
| Số trên board | Đọc lại Project bằng `gh project item-list` sau mỗi lượt ghi | Bước 9: 45 item khớp mô phỏng **không lệch cái nào** |
| Link trong tài liệu | Quét toàn bộ link tương đối trong repo | 0 link gãy |
| Bảng màu biểu đồ | `dataviz` có script kiểm mù màu, chạy cả nền sáng lẫn nền tối | Qua hết 5 phép kiểm ở cả hai nền |

Nguyên tắc tôi giữ: **không nhận một con số nào mà không có đường truy ngược.** Mỗi con số trong
`estimate.md` và `progress-report.md` đều chỉ được về một ticket, một dòng spec, hoặc một dòng của
estimate LAB-1.

### 2.2 Tám chỗ AI làm sai mà tôi bắt được

Xếp theo mức nguy giảm dần, không theo thứ tự phát hiện.

| # | Sai gì | Phát hiện ra sao | Nếu để lọt |
|---|---|---|---|
| 1 | Báo cáo HTML bước 7 ghi **18% khối lượng là "Bug/Rework"** | Sản phẩm chưa có dòng code nào, lấy đâu ra bug mà sửa | Con số *"Kế hoạch 548 / Bug-Rework 123"* đi vào báo cáo. Nguyên nhân: 45 ticket viết theo lối *"hôm nay hệ thống làm ngược lại"* nên skill tưởng là đi sửa lỗi. **Điểm không sai, chỉ cái nhãn sai** — đã ghi cảnh báo ngay đầu `estimate.md` |
| 2 | Đội giả lập đặt **1 BE · 1 FE · 1 QA** | Đối chiếu kế hoạch người theo tháng LAB-1 đã gửi khách (chốt 2026-10-08): tháng xây dựng đầu tiên 12/2026 là **2 BE · 2 FE · 1 QA** | Sức chứa sprint sai một nửa phần BE. Sprint 1 sẽ bị cắt nhỏ vô cớ, và 5 ticket đã suýt bị hoãn oan |
| 3 | `#24` thêm `unique(valid_from)` chấm **1 điểm** | Skill thấy bảng cùng họ đã có khuôn sẵn để chép nên coi là việc vặt | Chép khuôn vẫn phải viết migration, chạy, kiểm lại, chuẩn bị đường lùi. Mức 1 điểm để dành cho việc sửa một hằng số. → 3 điểm |
| 4 | `#153` kiểm ②④⑤ trong `allocate_order` chấm **5 điểm** (mô hình hai còn hạ xuống 3) | Cả hai chỉ nhìn công viết lần đầu | Bỏ sót: sau việc này **cùng một luật nằm ở hai nơi — TypeScript và SQL**. Mỗi lần luật đổi phải sửa cả hai. Cái giá đó trả dài. → 8 điểm |
| 5 | `BAN-GIAO.md` nói bước 7, 8 là **việc chưa làm** trong khi đã xong | Tôi đọc lại trước khi giao việc bước 9 | Thread sau đọc file bàn giao sẽ chạy lại bước đã xong, hoặc tệ hơn là dùng số cũ. Đã cập nhật và thêm câu *"nguồn đúng là `estimate.md`, không phải file này"* ngay đầu file |
| 8 | **Bỏ trường `Vai phụ trách` với lý do "không có trong đề".** Ghi trong `BAN-GIAO` mục 2 #9 | Đọc lại đề ở bước 10. Đề đòi rõ: *"Project có epic/issue/sub-issue, trạng thái, Iteration, **người phụ trách giả định**, trường point…"* | Nộp thiếu một thứ đề liệt kê thẳng. Quyết định đó dựa trên **trí nhớ về đề**, không phải đọc lại đề — và cả tôi lẫn AI đều không đặt câu hỏi. Đã tạo trường `Người phụ trách`, điền BE-1/BE-2/FE-1/FE-2 cho 45 ticket Sprint 1 lấy từ chính bộ xếp lịch bước 9 |
| 7 | **`#285` và `#286` xếp nhầm sang FE.** Bản rã gốc ghi *Development - Backend*, cha `[PARENT][BE]`, mã ticket trên board là `E12-ST-BE-02`/`-03` | Không phải tôi đọc ra. Bước 10 tôi cho **ba `doc-reviewer` chạy song song** đối chiếu từng con số trong tài liệu với board và với bản rã; một trong ba bắt được | Chia vai sai thì **burndown sai**, mà burndown là sản phẩm chính của bước 9. Sửa xong: BE 19→21 ticket (79→83 SWP), FE 26→24 (78→74). Phải chạy lại mô phỏng, vẽ lại biểu đồ, đẩy lại Status. Kết quả đổi thật: Done 83%→**78%**, và **FE nhàn rỗi 18,7→36,1 giờ** — chỗ lệch BE/FE hiện ra rõ hơn hẳn |
| 6 | Sức chứa Sprint 1 báo **83%**, và tỉ lệ 1,7 giờ/SWP dùng để khẳng định sprint vừa sức | Tiếng nói *Phản biện* của `tkm:predict-risks` chỉ ra: 83% là đo trên giờ **danh nghĩa** (320 h); trên giờ **hiệu dụng** (280 h) đã là **95%**. Và tỉ lệ 1,7 rút ra từ đúng cặp E01+E02 — đúng cặp sprint này chạy | Lập luận vòng tròn: sprint "vừa khít" không chứng minh gì cho 11 epic còn lại. Sprint 2 sẽ bị cắt quá tay. Đã hạ trần xuống **~82 SWP/vai** |

Chỗ 1 và chỗ 2 là hai chỗ nguy nhất: cả hai đều **đọc rất trôi chảy** và không có gì trong chính
đầu ra báo cho biết là sai. Chỉ lòi ra khi đem đối chiếu với một nguồn bên ngoài — ở đây là hiểu
biết về trạng thái dự án, và kế hoạch người của LAB-1.

Chỗ 7 đáng nói riêng, vì nó cho thấy **đọc lại bài của chính mình thì không đủ**. Tôi đã soát chéo
tay 12 con số qua 6 file và thấy sạch. Vòng `tkm:review-doc` với ba tác nhân soát độc lập — mỗi
tác nhân một nhóm tài liệu, bắt buộc trích dẫn cả hai phía và tự chạy lệnh đếm thay vì đếm mắt —
tìm ra **13 lỗi**, trong đó chỗ 7 làm sai cả sản phẩm chính. Tỉ lệ đó nói rằng vòng soát độc lập
không phải thủ tục cho đủ bước.


## 3. Điểm đặc biệt trong cách dùng AI

### 3.1 Chỗ tôi tin là hiệu quả

- **Rã 307 item từ 272 dòng spec.** Việc cơ học, lượng lớn, và nó không bỏ sót: soát lại 0 tiêu đề
  lệch, 0 cha gắn sai, 0 dòng nội dung rơi. Làm tay thì vài ngày và chắc chắn sót.
- **Chấm điểm nhất quán.** Cái lợi thật của thang Scope × Complexity không phải là chấm đúng, mà là
  **cùng một mô tả việc luôn ra cùng một điểm**. Người chấm tay thì ticket thứ 150 không còn cùng
  thước với ticket thứ nhất.
- **Hai tiếng nói cãi nhau có ích.** `tkm:predict-risks` ra hai chỗ bất đồng thật, không phải bất
  đồng dựng lên cho đủ bảng: Hiệu năng ⟷ Phản biện về 12 ticket FE vay (giảm thiểu hay che giấu),
  và UX ⟷ Kiến trúc về `#34` (kéo sớm hay chẻ nhỏ). Chỗ thứ hai đẻ ra hành động R1.
- **Đối chiếu LAB-1 theo từng nhóm.** Chính việc so từng nhóm thay vì so tổng mới lòi ra **E12 hụt
  90%** — so tổng thì nó chìm trong con số −60% chung và không ai hỏi gì.

### 3.2 Chỗ chưa tốt, phải cải thiện khi làm thật

- **AI không tự biết thứ gì vắng mặt.** Nó đọc board rất kỹ, nhưng board không có ticket QA và
  không có ticket sửa bug thì nó không thấy thiếu. Cả hai chỗ đó là tôi phải nêu, và chúng cộng lại
  **+38%** lên trên 142,6 ngày công. Đây là giới hạn thật, không phải lỗi prompt.
- **Nó mặc định tin đầu vào của chính nó.** Nhãn "Bug/Rework" sai ở chỗ 1 nằm ngay trong báo cáo nó
  tự sinh, và nó không tự nghi. Phải có người hỏi *"sản phẩm này đã có code chưa?"*.
- **Nó trôi khỏi khung nếu không bị chặn.** Để tự do thì nó thêm mục, thêm cột, thêm phần — bản
  nháp `progress-report.md` đẻ ra phần thứ năm dù đã chốt bốn.
- **Hai AI đồng ý không chứng minh điểm đúng.** 2 trong 9 ticket đối chứng khớp hệt nhau. Điều đó
  dễ đọc thành "chắc rồi", nhưng hai mô hình hoàn toàn có thể sai giống nhau. Tôi ghi câu này thẳng
  vào `estimate.md` để người đọc sau không dùng sự đồng thuận làm bằng chứng.

**Về giới hạn thời gian, công sức và token** — ba thứ đề hỏi riêng:

- **Token là chỗ đắt nhất, và đắt ở khâu soát chứ không phải khâu làm.** Rã 307 item tốn ít hơn
  nhiều so với vòng `tkm:review-doc` cuối: ba tác nhân soát ngốn ~372k token cho một việc không sinh
  ra dòng nội dung nào. Nhưng nó tìm ra 13 lỗi, trong đó một lỗi làm sai cả burndown. **Tôi vẫn sẽ
  trả khoản đó**, chỉ là lần sau cho chạy sớm hơn chứ không để tới bước 10 — sửa chia vai ở bước 8
  thì khỏi phải chạy lại mô phỏng, vẽ lại biểu đồ và đẩy lại 109 lượt `Status`.
- **Công sức của tôi dồn sai chỗ.** Tôi đọc kỹ nội dung AI viết (văn có trôi không, lập luận có
  chặt không) mà kiểm hời hợt những con số nó chép qua lại giữa các file. Đúng ra phải ngược lại:
  văn thì AI viết khá, còn con số đi qua ba file là chỗ nó trượt. Lần sau tôi viết script đối chiếu
  số trước, đọc văn sau.
- **Chưa có ý tưởng cho một chỗ:** làm sao biết AI **bỏ sót** cái gì. Nó không có ticket QA và không
  có ticket sửa bug thì nó không thấy thiếu, vì board không có chỗ nào ghi "ở đây đáng lẽ phải có".
  Cả hai lần đều là tôi nhớ ra, không phải quy trình bắt được. Một checklist "đối chiếu với estimate
  LAB-1 theo từng nhóm" có giúp — nó chính là chỗ lòi ra E12 hụt 90% — nhưng chỉ dùng được khi có
  sẵn một bản ước khác để so. Dự án thật thường không có.

### 3.3 Lần sau làm khác chỗ nào

1. **Khai mẫu số trước khi báo phần trăm.** Con số 83% suýt đi vào báo cáo mà không ai hỏi "83% của
   cái gì". Từ nay mọi tỉ lệ sức chứa viết kèm giờ hiệu dụng.
2. **Hỏi "thiếu gì" thành một bước riêng**, không trông vào việc AI tự thấy. Ở bài này nếu không có
   bước đó thì mất cả QA lẫn công sửa bug.
3. **Cập nhật file bàn giao ngay trong bước, không để dồn.** Chỗ 5 là lỗi quy trình của tôi, không
   phải của AI.
