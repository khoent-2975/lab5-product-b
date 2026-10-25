# Bản rã task — LAB-5 Product B

**Ngày:** 2026-10-24 · **Nguồn:** `lab4-product-b/specs/` · **Trạng thái:** §1 xong · §2 mới điền E02 (mẫu duyệt) · §3 §4 chưa làm

---

## 1. Luật chia task

Bản rã này không dựng từ đầu. Mục 6.3 của 15 screen spec đã cho **272 dòng** chênh lệch, mỗi dòng
có sẵn cột `Tầng`; **229 dòng** trong đó có tầng code. Việc của LAB-5 là **gom và chọn**, nên phải
có luật chọn viết ra trước.

### 1.1 Độ hạt — một issue là gì

Một dev task = **một (màn × tầng × một việc nghiệm thu được một mình)**.

⚠ **Số thật khác con số ước ban đầu.** `BAN-GIAO.md` §2 #1 chốt `~120 item` dựa trên phép gom
417 lượt gán tầng thành 73 nhóm. Rã xong thật thì ra **312 item**:

| Cấp | Dự kiến | Thật | Chênh |
|---|---|---|---|
| Epic | 13 | **13** | 0 |
| Story | — | **26** | +26 (cấp mới, theo template công ty) |
| `[PARENT][BE]` / `[PARENT][FE]` | — | **54** | +54 (cấp mới) |
| Dev task | 108 (73 + 35) | **176** | +68 |
| Investigation | (nằm trong 73) | **38** | tách riêng |
| **Tổng** | **~120** | **307** | **+187** |

**Ba nguyên nhân, không cái nào là phình việc:**
1. **+80 từ hai cấp mới.** Story và hai parent BE/FE là cấu trúc, không phải việc. Bỏ hai cấp này
   thì còn **214**
2. **+68 dev task** vì luật *"một task một việc"* cắt mịn hơn phép gom `màn × tầng`. Ví dụ bốn
   ngưỡng giờ lái là **một** nhóm `SCR-28 × RPC` nhưng phải thành **bốn** task
3. **38 investigation** trước đây nằm lẫn trong 73; nay tách ra vì chúng **không ước công**

**Đã chốt 2026-10-24:** giữ 307, sửa con số trong `BAN-GIAO.md`.

### 1.1.1 Câu hỏi khách trùng gốc — hỏi một lần

Một câu hỏi khách chỉ có **một** investigation, dù nó chạm nhiều epic. Hai ca đã gộp:

| Câu hỏi | Ở epic | Các epic khác trỏ về |
|---|---|---|
| **Q19** — mấy mức severity, ai duyệt mức nào, tệp bắt buộc nào | `E10-INV-01` | E06 (`E06-03-BE-03`) · E09 |
| **Quyền theo kho và theo người** | `E12-INV-01` | E07 (SCR-18) · E09 (SCR-24, SCR-26) |

### 1.2 Khi nào tách

| Tách khi | Ca thật |
|---|---|
| Hai cách sửa khác nhau | ① sửa bằng đổi thứ tự điểm giao · ② sửa bằng bớt điểm giao hoặc đổi tài xế |
| Hai toán tử biên khác nhau | ① ② ④ dùng `>` nghiêm · ③ dùng `>=` không nghiêm |
| Hai tầng khác nhau | chỗ lưu điểm nghỉ = `DB (migration)`, phép reset chuỗi lái = `RPC / luật` |
| Hai bộ AC khác nhau ở mục 6.4 | `AC-28-37` (khoảng vi phạm) không nằm trong bộ AC của ① |
| Một nhánh chờ khách, một nhánh không | 6 ngưỡng thiếu cột (ước được) ⟷ 2 ngưỡng thiếu nguồn dữ liệu (chờ Q13) |

Căn cứ cấm gộp nằm trong chính spec: `AC-28-34` cấm rút bốn ngưỡng thành một câu
`このルートは法定基準を満たしていません`.

### 1.3 Khi nào gộp

Cùng **một lỗ hổng** lộ ra ở hai màn thì vẫn là **một** issue, không tách theo màn.

Ca thật — **M-3**: `client_request_id` thiếu ở cả `routes` (SCR-28 #11) và `route_versions`
(SCR-29 #10). Hai dòng spec, một migration, một issue.

### 1.4 Định nghĩa xong

Định nghĩa xong của một issue là **danh sách mã AC ở mục 6.4**, chép mã chứ không diễn đạt lại —
1.035 dòng AC đã viết sẵn dạng *cho … khi … thì …* với số đo thật từ seed. Viết lại bằng lời là
tự tạo thêm một bản dịch để sai.

Issue nào không có mã AC nào đỡ thì phải tự viết tiêu chí, và **phải ghi rõ là tự viết**.

### 1.5 Dòng không sinh code

43 dòng `không code` không thành issue thi công. Chúng đi một trong hai đường:
- cần khách trả lời → **issue làm rõ**, không ước công, không chặn tầng nào;
- chỉ cần ghi thành văn bản → gộp vào `PREMISE.md` hoặc một issue ghi vết chung.

### 1.6 Luật truy ngược

Mọi dòng trong 229 dòng ước được phải truy về **đúng một** issue. §4 giữ cột *"phần spec chưa
thành issue và vì sao"* — để trống cột đó nghĩa là bản rã chưa xong.

### 1.7 Format ticket — theo template công ty

Dùng nguyên bộ mẫu issue nội bộ của công ty (`.github/ISSUE_TEMPLATE/`). Ba cấp khớp sẵn:

| Cấp LAB-5 | Template | Nhãn | Tiền tố tiêu đề |
|---|---|---|---|
| Epic | `01-epic.yml` | `type:epic` | `[EPIC] ` |
| Story (có mã US) | `02-story.yml` | `type:story` | `[STORY] ` |
| Dev task cha (gom theo đội) | `05-dev-task.yml` | `type:devtask` | `[PARENT][BE] ` / `[PARENT][FE] ` |
| Dev task | `05-dev-task.yml` | `type:devtask` | `[DEV TASK] ` |
| Câu hỏi chờ khách | `12-investigation.yml` | `type:investigation` | `[INVESTIGATION] ` |

- Dưới mỗi story luôn có **đúng hai** dev task cha: `[PARENT][BE]` và `[PARENT][FE]`, đặt
  `Task Category = Feature`. Mọi dev task con treo vào cha đúng đội của nó, `Task Category = Task`
- Task cha không tự có code — đóng khi con đóng hết
- Mã task mang luôn đội: `E02-BE-01`, `E02-FE-01` — nhìn danh sách phẳng vẫn biết của ai
- `Task Type`: tầng `DB (migration)` và `RPC / luật` → `Development - Backend`; tầng `UI` →
  `Development - Frontend`
- Trường `Tầng` trên board giữ nguyên 6 giá trị, dùng để lọc; **không** nhét tag tầng vào tiêu đề
  nữa — template đã có `Task Type`

### 1.8 Cách viết Acceptance Criteria

Mỗi AC một dòng bullet, dạng **Given / When / Then**, mở đầu bằng mã AC để truy ngược:

```
- **AC-28-27** — Given chuỗi lái liên tục 241 phút · When khối C render · Then dòng ① badge `超過`,
  hiện `241分 / 上限 240分`
```

- Một ý một bullet, không viết đoạn văn dài
- Số đo lấy nguyên từ mục 6.4 của spec, không làm tròn, không diễn đạt lại
- AC tự viết (mục 6.4 không có mã) thì đánh dấu `[tự viết]` ngay đầu dòng

### 1.9 Phân cấp trên GitHub — Issue Type không dùng được

Repo `khoent-2975/lab5-product-b` là repo **cá nhân**, mà Issue Type là tính năng **cấp tổ chức** —
kiểm 2026-10-24: `repository.issueTypes` trả `null`. Đánh dấu cấp bằng **nhãn** (`type:epic`,
`type:story`, `type:devtask`, `type:investigation`), nối cha–con bằng **quan hệ sub-issue native**
(trường `Parent issue` / `Sub-issues progress` đã có sẵn trên board).

---

## 2. Spec → issue — Epic → Story → Dev task

> **Đã xong: cả 13 epic.**

### E01 · Dựng tuyến giao hàng

| | |
|---|---|
| **Màn** | SCR-28 |
| **Dòng 6.3 hút vào** | #1 (DB + API + UI) · #6 · #8 · #9 · #11 · #16 · #17 · #18 |
| **Nhóm LAB-1 đối chiếu** | F06 · `FT-06-01` — 26 SP / 14 MD |
| **Số item** | 1 epic + 1 story + 2 parent + 12 dev task + 4 investigation = **20** |

```
[EPIC] E01 Build delivery route creation on SCR-28
└── [STORY] US-12 Dispatcher builds a delivery route from orders, vehicle and time window
    ├── [PARENT][BE] E01-BE Create route/stop RPCs, code generation and hard-reject guards
    │   ├── E01-BE-01 Create create_route RPC with route_code sequence
    │   ├── E01-BE-02 Add client_request_id to routes and route_versions for duplicate guard
    │   ├── E01-BE-03 Create set_route_stops RPC with contiguous seq renumbering
    │   ├── E01-BE-04 Pre-check three unique constraints and return precise conflict codes
    │   ├── E01-BE-05 Expose route read/write API routes with three-layer permission parity
    │   ├── E01-BE-06 Check vehicle temp_zone against cargo temperature range
    │   └── E01-BE-07 Build unassigned-order list and rejection reason catalogue
    └── [PARENT][FE] E01-FE Build SCR-28 route builder screen
        ├── E01-FE-01 Build screen shell, role gating and the four mandatory load states
        ├── E01-FE-02 Build stop table B with depot/return rows and travel/service columns
        ├── E01-FE-03 Build header form A and draft save with busy state
        ├── E01-FE-04 Render unassigned orders block with rejection reasons
        └── E01-FE-05 Review 22 new Japanese strings with a native speaker
[INVESTIGATION] E01-INV-01 Confirm Q12 — dispatcher builds the route vs system generates it
[INVESTIGATION] E01-INV-02 Confirm route_code convention R<YYMMDD>-<4 digits>
[INVESTIGATION] E01-INV-03 Confirm the one-driver-one-route-per-day constraint
[INVESTIGATION] E01-INV-04 Confirm Q56 — route status enum has 2 values or 6
```

---

#### `[EPIC]` E01 — Build delivery route creation on SCR-28

**Overview & Goal**
- As a `配送計画者` (*"Điều phối giao hàng"*)
- I want dựng một tuyến giao hàng cho một ngày: chọn xe, tài xế, giờ xuất phát, xếp thứ tự điểm giao
- So that có một tuyến nháp hợp lệ để đưa sang bước kiểm luật và công bố

**Scope & Features**
- Hai hàm `create_route` và `set_route_stops` — **chưa tồn tại trong migration nào**
- Sinh `route_code` từ một sequence
- Chống gửi trùng bằng `client_request_id`
- Ba ràng buộc unique kiểm trước để trả đúng mã lỗi
- Màn SCR-28: 4 section, 17 trạng thái, bảng tra điều kiện hiện/ẩn
- Kiểm dải nhiệt xe ⟷ hàng, và khối đơn chưa phân công kèm lý do từ chối

**Ngoài phạm vi**
- Bốn ngưỡng giờ lái → **E02** · Điểm nghỉ → **E04** · Công bố → **E03**
- `US-30` ghi sự cố có bằng chứng — SCR-30, **ngoài phạm vi 15 màn**

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-28-01** đảo chiều — Given LAB-5 đã dựng trang và lật `MENU:46` thành `enabled: true` ·
  When vai `配送計画者` mở `/routes` · Then trả **200** thay vì 404
- **AC-28-11** — Given khối rỗng · When bấm `A-10` · Then có **đúng một** dòng `routes` mới
  `status='draft'`, `current_version=0`, `route_code` theo khuôn `R<YYMMDD>-<4 chữ số>`

**References & Dependencies**
- Spec: `scr-28-tao-tuyen-giao-hang.md` §6.3 #1 #6 #8 #9 #11 #16 #17 #18 · §6.4.1 §6.4.2 §6.4.3 §6.4.8
- Estimate LAB-1: F06 / `FT-06-01` — 26 SP / 14 MD
- Chặn: **E02** (khối C cần tuyến có thật) · **E03**

---

#### `[STORY]` US-12 — Dispatcher builds a delivery route from orders, vehicle and time window

**Overview**
- **Who:** `配送計画者`
- **What:** tạo tuyến cho một ngày, gán xe và tài xế, xếp thứ tự điểm giao, lưu nháp
- **Why:** không có tuyến thì không có gì để kiểm luật và không có gì để phát cho tài xế

**Acceptance Criteria**
- **AC-28-02** — Given trang đã dựng · When vai `配送計画者` mở `/routes` · Then trả 200, hiện
  tiêu đề `配送ルート作成`, mã `SCR-28`, ô `配送日` (`A-1`) đặt sẵn hôm nay theo JST
- **AC-28-10** — Given một ngày chưa có tuyến nào · When chọn ngày đó ở `A-1` · Then hiện khối rỗng
  kèm nút `配送ルート作成` (`A-10`), **không** có bảng `B`, **không** có khối `C`
- **AC-28-11** — Given khối rỗng · When bấm `A-10` · Then có đúng một dòng `routes` mới
  (`draft`, `current_version=0`, `service_date` = ngày đã chọn, `route_code` đúng khuôn), màn
  chuyển sang hiện A + B + C + D
- **AC-28-17** — Given tuyến nháp mới · When chọn `VH-02` ở `A-2`, `DRV-02` ở `A-3`, `08:00` ở
  `A-4` rồi lưu · Then `routes.vehicle_id` `.driver_id` `.start_time` mang đúng ba giá trị đó
- **AC-28-18** — Given tuyến nháp chưa có điểm giao · When bấm `B-9` chọn `CUS-006` · Then có một
  dòng `route_stops` `seq=1`, `delivery_point_id` = id của `CUS-006`, `order_id = NULL`
  — **không có đơn là hợp lệ** (`R-16`)
- **AC-28-19** — Given tuyến có ba điểm giao `seq` 1·2·3 · When xoá dòng `seq=2` bằng `B-10` ·
  Then hai dòng còn lại mang `seq` **1 và 2** — đánh số lại liên tục, không thủng số
- **AC-28-20** — Given tuyến có ba điểm giao · When đổi chỗ dòng 1 và 2 bằng `B-11` · Then ghi
  thành công trong **một** giao dịch, `unique(route_id, seq)` **không** bị vi phạm giữa chừng
- **AC-28-21** — Given tuyến hiện trên màn · When nhìn bảng `B` · Then dòng đầu là `B-2` `出発`
  với `DEPOT` / `サービスタイム 0分` và ô `順` để trống; dòng cuối là `B-12` `帰着` về `DEPOT`
  — hai dòng này **không** phải dòng `route_stops`
- **AC-28-22** — Given `CUS-006` ở `seq=1` · When nhìn ô `移動時間` · Then giá trị là **150 phút**
- **AC-28-23** — Given `CUS-007` ở `seq=2` sau `CUS-006` · When nhìn ô `移動時間` · Then **120 phút**;
  và `サービスタイム` của hai dòng là **20 phút** và **25 phút**
- **AC-28-25** — Given đã sửa bảng `B` · When bấm `D-1 下書き保存` · Then chữ trên nút **bị thay**
  thành `M_06 処理中…` (không phải thêm chữ), nút nhận `aria-busy`; xong thì hiện `D-4`,
  badge vẫn `下書き`, màn **không** rời đi

**References & Dependencies**
- Spec: SCR-28 §6.4.1 · §6.4.2 · §6.4.3 · §6.4.8
- Dữ liệu kiểm: seed `R-SEED-02`, `DEPOT` + `CUS-001…007`, ma trận 56 chặng

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E01-BE — Create route/stop RPCs, code generation and hard-reject guards

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 7 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật` + `API route`

**Specification**
- Gom toàn bộ phần máy chủ của `US-12`. Hôm nay **không có gì**: `create_route` và
  `set_route_stops` không tồn tại trong migration nào; `app/api/` có 14 thư mục, không có `routes`
- Nhánh lập tuyến bị cắt ở **phase 04c** — có tuyên bố, không phải thiếu âm thầm
- Thứ tự: `E01-BE-01` → `E01-BE-03` → `E01-BE-04` → `E01-BE-05`; `E01-BE-02` song song được

**Impact Range**
- `supabase/migrations/` · `routes` · `route_stops` · `app/api/routes/`

---

##### `[DEV TASK]` E01-BE-01 — Create create_route RPC with route_code sequence

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Sprint 1** (T0)

**Specification**
- Dựng hàm `create_route` dạng `security definer`, theo adr-01 (ghi nghiệp vụ chỉ qua RPC)
- Sinh `route_code` theo khuôn `R<YYMMDD JST>-<4 chữ số>` từ một sequence, theo đúng lối `lot_code`
  và mã Sai lệch của LAB-2
- Hôm nay `routes.route_code` là `text not null unique` nhưng **không ai sinh nó** — hai mã trong DB
  là `R-SEED-01`/`R-SEED-02` do seed đặt tay
- **AC-28-11** — Given khối rỗng · When bấm `A-10` · Then đúng một dòng `routes` mới với
  `status='draft'`, `current_version=0`, `service_date` = ngày đã chọn, `route_code` đúng khuôn
- ⚠ Khuôn mã là **giả định vendor** — xem `E01-INV-02`

**Impact Range**
- `routes` · sequence mới · `app/api/routes/`

---

##### `[DEV TASK]` E01-BE-02 — Add client_request_id to routes and route_versions for duplicate guard

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Sprint 1** (T0)

**Specification**
- `routes` **không có** `client_request_id`, trong khi `receiving_lines` có và dùng nó để chống
  gửi trùng. `route_versions` thiếu y hệt
- Bấm `配送ルート作成` hai lần sát nhau có thể sinh **hai tuyến nháp**; `route_code` unique không
  chặn được vì mỗi lần gọi sinh một mã khác
- **Gộp một task cho cả hai bảng** — cùng một lỗ hổng lộ ở hai màn (`SCR-28 #11` ⟷ `SCR-29 #10`),
  không tách theo màn. Đây là mâu thuẫn **M-3** và là ca mẫu của luật gộp ở §1.3
- Thêm cột + ràng buộc unique theo đúng khuôn `receiving_lines.client_request_id`
- `[tự viết]` Given hai lần gọi cùng `client_request_id` · When gọi sát nhau · Then chỉ một dòng
  `routes` được tạo, lần hai trả về chính dòng đó

**Impact Range**
- `routes` · `route_versions` · `create_route` · `publish_route` (E03)

---

##### `[DEV TASK]` E01-BE-03 — Create set_route_stops RPC with contiguous seq renumbering

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Sprint 1** (T0)

**Specification**
- Dựng `set_route_stops` — thêm, xoá, đổi chỗ điểm giao trong **một** giao dịch
- **AC-28-18** — Given tuyến chưa có điểm giao · When thêm `CUS-006` · Then một dòng `route_stops`
  `seq=1`, `order_id = NULL` — điểm giao không gắn đơn là **hợp lệ** (`R-16`)
- **AC-28-19** — Given ba điểm `seq` 1·2·3 · When xoá `seq=2` · Then còn lại mang `seq` 1 và 2
  (`R-17`)
- **AC-28-20** — Given ba điểm giao · When đổi chỗ dòng 1 và 2 · Then ghi trong một giao dịch,
  `unique(route_id, seq)` không vỡ giữa chừng
- **AC-28-57** — Given `create_route` thành công nhưng `set_route_stops` hỏng · When kiểm DB ·
  Then dòng `routes` **vẫn còn**, không có `route_stops` nào — ca "ghi một phần" **hợp lệ**, màn hiện `S4`

**Impact Range**
- `route_stops` · `create_route`

---

##### `[DEV TASK]` E01-BE-04 — Pre-check three unique constraints and return precise conflict codes

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Kiểm **trước** ba ràng buộc unique rồi mới ghi, để trả mã lỗi chỉ đúng ô — không để Postgres tự nổ
- **AC-28-51** — Given `DRV-02` đã có tuyến `R-SEED-02` ngày `2026-10-20` · When gán `DRV-02` cho
  tuyến khác cùng ngày · Then **409** `CONFLICT_DRIVER_ROUTE_EXISTS`, ô `A-3` bị tô, **không** dòng
  `routes` nào được ghi
- **AC-28-52** — Given RPC **không** kiểm trước mà để Postgres nổ · When gọi · Then ra
  **409 `conflict_duplicate` không có `detail`** và màn không chỉ được ô nào — **đây là hành vi
  phải tránh**, bẫy 1 của 3.3
- **AC-28-53** — Given một `order_id` đã nằm ở chặng của tuyến khác · When gán vào tuyến đang dựng ·
  Then **409** `CONFLICT_ORDER_ALREADY_ROUTED` — `route_stops.order_id` unique **toàn bảng**
- **AC-28-54** — Given hai dòng cùng `seq` trong một tuyến · When ghi · Then **409**, không dòng nào được ghi
- **AC-28-55** — Given `delivery_point_id` không có trong master · When ghi · Then **422**
  `VALIDATION_UNKNOWN_MASTER`, dòng tương ứng bị tô
- **AC-28-56** — Given bất kỳ ca 422/409/403 nào ở trên · When kiểm DB · Then **không** dòng mới ở
  `routes` và `route_stops` — `raise` thoát hàm nên transaction cuộn

**Impact Range**
- `create_route` · `set_route_stops` · `mapRpcError`

---

##### `[DEV TASK]` E01-BE-05 — Expose route read/write API routes with three-layer permission parity

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- 2 endpoint ghi + 1 endpoint đọc danh mục. Ba tầng quyền (trang · API · RPC) phải khớp nhau
- **AC-28-05** — Given tài khoản **không** phải `配送計画者` · When gọi thẳng endpoint ghi với thân
  hợp lệ · Then **403** `{"error":"forbidden"}` **và** `routes` không tăng dòng
- **AC-28-06** — Given gọi thẳng RPC `create_route` bằng JWT của vai khác · When gọi · Then RPC
  `raise FORBIDDEN`, API trả **403**
- **AC-28-07** — Given bất kỳ vai nào trong bảy vai đã đăng nhập · When truy vấn
  `driver_rule_versions` hoặc `travel_times` qua PostgREST · Then nhận **đủ dòng** — hiện trạng
- **AC-28-08** — Given vai `ドライバー` · When truy vấn `routes` · Then chỉ nhận dòng
  `status='published'`; **và** năm vai còn lại nhận **cả** `R-SEED-02` (`draft`) — hiện trạng,
  ghi vết ở 6.3 #12, **khách quyết có siết hay không**

**Impact Range**
- `app/api/routes/` · RLS policies · `create_route` · `set_route_stops`

---

##### `[DEV TASK]` E01-BE-06 — Check vehicle temp_zone against cargo temperature range

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- **US-12 AC1** đòi tuyến dựng từ **dải nhiệt của xe**. Hôm nay `vehicles.temp_zone` nạp về nhưng
  **không vế nào đọc** (`R-26`)
- Thiếu đường nối từ `route_stops.order_id` sang SKU để so dải nhiệt → **phải dựng đường đọc mới**
- `[tự viết]` Given tuyến gán `VH-03 常温` và một đơn chứa hàng `冷凍` · When kiểm · Then báo lệch
  dải nhiệt, nêu đích danh đơn và dải nhiệt đòi hỏi
- ⚠ Chờ **Q14** (`R-26`) — chưa có đáp án; làm theo giả định vendor: so dải nhiệt ở mức **cảnh báo**,
  không chặn cứng

**Impact Range**
- `vehicles.temp_zone` · `route_stops` → `orders` → SKU · khối cảnh báo trên SCR-28

---

##### `[DEV TASK]` E01-BE-07 — Build unassigned-order list and rejection reason catalogue

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- **US-12 AC3** là **tiêu chí nghiệm thu P0 chưa được phủ** — không phải việc nhỏ
- Hôm nay: không có khối nào hiện đơn chưa phân công, `orders` **không có cột "lý do không xếp được
  tuyến"**, và không có chỗ nào sinh lý do từ chối
- Hai vế: (a) truy vấn đơn chưa phân công của ngày · (b) danh mục lý do từ chối + chỗ lưu
- `[tự viết]` Given một ngày có 3 đơn chưa vào tuyến nào · When mở SCR-28 · Then cả 3 đơn trả về
  kèm mã lý do từ chối, không đơn nào biến mất im lặng

**Impact Range**
- `orders` (cột mới hoặc bảng lý do) · endpoint đọc của SCR-28

---

#### `[PARENT][FE]` E01-FE — Build SCR-28 route builder screen

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 5 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Dựng cả màn SCR-28: 4 section, bảng tra điều kiện hiện/ẩn 2.0, 17 trạng thái của mục 5.1
- Phụ thuộc `[PARENT][BE]` cho đường ghi; khối `C` thì thuộc **E02**

**Impact Range**
- `app/(app)/routes/` (mới) · `MENU:46`

---

##### `[DEV TASK]` E01-FE-01 — Build screen shell, role gating and the four mandatory load states

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Sprint 1** (T3)

**Specification**
- Dựng `app/(app)/routes/`, lật `MENU:46` thành `enabled: true`
- **AC-28-02** — Given vai `配送計画者` · When mở `/routes` · Then 200, hiện `配送ルート作成`, mã
  `SCR-28`, ô `配送日` đặt sẵn hôm nay theo JST
- **AC-28-03** — Given một trong sáu vai còn lại · When mở `/routes` · Then **403**, hiện
  `M_01` / `M_02` / `M_03`, **không** ô nhập nào được render
- **AC-28-04** — Given phiên chưa đăng nhập · When mở `/routes` · Then chuyển hướng tới `/login`
- **AC-28-09** — Given dữ liệu chưa về · When trang vừa render · Then vùng nội dung hiện **đúng
  một dòng** `M_22 読み込み中…`, tiêu đề vẫn đầy đủ
- **AC-28-16** — Given tuyến `R-SEED-01` (`published`) · When mở ở màn này · Then badge `A-14`
  hiện `公開済み` và **năm item** `B-9` `B-10` `B-11` `C-10` `D-1` **không** được render — chỉ đọc

**Impact Range**
- `app/(app)/routes/page.tsx` · `MENU:46`

---

##### `[DEV TASK]` E01-FE-02 — Build stop table B with depot/return rows and travel/service columns

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Sprint 1** (T3)

**Specification**
- **AC-28-21** — Given tuyến hiện trên màn · When nhìn bảng `B` · Then dòng đầu `B-2 出発` với
  `DEPOT` / `サービスタイム 0分`, ô `順` để trống; dòng cuối `B-12 帰着` về `DEPOT` — hai dòng này
  **không** phải dòng `route_stops`
- **AC-28-22** — Given `CUS-006` ở `seq=1` · When nhìn `移動時間` · Then **150 phút**
- **AC-28-23** — Given `CUS-007` ở `seq=2` · When nhìn `移動時間` · Then **120 phút**;
  `サービスタイム` hai dòng là **20** và **25 phút**
- **AC-28-12** — Given `R-SEED-02` sau khi xoá hết `route_stops` · When mở màn · Then bảng `B` hiện
  `配送先は登録されていません`, khối `C` **vẫn hiện đủ bốn dòng**
- **AC-28-10** — Given ngày chưa có tuyến · When chọn ngày · Then khối rỗng kèm `A-10`, không bảng `B`

**Impact Range**
- Bảng `B` của SCR-28 — item `B-2`, `B-9`…`B-12`

---

##### `[DEV TASK]` E01-FE-03 — Build header form A and draft save with busy state

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Sprint 1** (T3)

**Specification**
- **AC-28-17** — Given tuyến nháp mới · When chọn `VH-02`/`DRV-02`/`08:00` rồi lưu · Then ba cột
  `routes` mang đúng ba giá trị
- **AC-28-25** — Given đã sửa bảng `B` · When bấm `D-1 下書き保存` · Then chữ trên nút **bị thay**
  thành `M_06 処理中…`, nút nhận `aria-busy`; xong hiện `D-4`, badge vẫn `下書き`, màn **không** rời đi
- **AC-28-14** — Given `start_time` là NULL · When mở màn · Then khối `C` hiện `C-12`, `D-1`
  **vẫn bật**, `D-2` tắt — giữ cột nullable theo `PREMISE V-5`

**Impact Range**
- Section `A` của SCR-28 — item `A-1`…`A-4`, `A-10`, `A-14` · nút `D-1`, `D-4`

---

##### `[DEV TASK]` E01-FE-04 — Render unassigned orders block with rejection reasons

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** E01-BE-07

**Specification**
- Khối "đơn chưa phân công" + lý do từ chối, luôn hiện trên màn (**US-12 AC3**, P0 chưa phủ)
- `[tự viết]` Given ngày có đơn chưa vào tuyến · When mở SCR-28 · Then khối hiện đủ đơn kèm lý do,
  không đơn nào bị ẩn

**Impact Range**
- Section mới trên SCR-28

---

##### `[DEV TASK]` E01-FE-05 — Review 22 new Japanese strings with a native speaker

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `dùng chung` + `UI`

**Specification**
- Màn có **32 chuỗi có nguồn** (19 `[CODE]`, 11 `[RFP]`, 2 `[JA-NEW]` đã đăng ký); **22 chuỗi soạn
  mới** cần duyệt: 12 nhãn riêng của màn + 10 câu thông báo
- 10 câu thông báo **đã cấp mã** `M_79`–`M_88` ở `_common/thong-bao-ja.md` — ba khuôn B2
  (`M_79`, `M_80`, `M_86`) và bảy câu riêng màn
- `[tự viết]` Given 22 chuỗi soạn mới · When người bản ngữ Nhật duyệt xong · Then mỗi chuỗi có một
  trạng thái duyệt ghi lại, không chuỗi nào vào code khi chưa duyệt
- **Tầng `dùng chung` treo dưới FE** vì chuỗi được tiêu thụ ở tầng giao diện

**Impact Range**
- `_common/thong-bao-ja.md` · mọi nhãn của SCR-28

---

#### `[INVESTIGATION]` E01-INV-01 — Confirm Q12: dispatcher builds the route vs system generates it

**Overview**
- Hỏi khách: người điều phối tự dựng tuyến, hay hệ thống tự sinh và tối ưu
- **Giả định vendor:** người điều phối dựng, hệ thống kiểm — căn cứ là nội dung đào tạo dispatcher
  `ルート構築、拘束時間警告の読み取り`
- **Mức đổi nếu đáp án khác:** khách chọn tự sinh → **màn khác hẳn**, bật `FT-06-02`
- Đây là câu **nặng nhất** của E01: đáp án khác thì phần lớn `[PARENT][FE]` phải làm lại

**References**
- `R-02` · `QA:24`

---

#### `[INVESTIGATION]` E01-INV-02 — Confirm route_code convention R<YYMMDD>-<4 digits>

**Overview**
- Hỏi khách: có quy ước đánh mã tuyến riêng không
- **Giả định vendor:** `R<YYMMDD JST>-<4 chữ số>` từ một sequence, theo lối `lot_code` của LAB-2
- **Mức đổi:** Thấp — chỉ đổi hàm sinh mã trong `create_route`

**References**
- SCR-28 §6.3 #18 · `A-5`

---

#### `[INVESTIGATION]` E01-INV-03 — Confirm the one-driver-one-route-per-day constraint

**Overview**
- Chỉ mục `routes_driver_service_date_key` ép **một tài xế một tuyến mỗi ngày**, comment viện dẫn
  `(Q13/Q16)` — nhưng **không câu nào trong hai câu đó hỏi về việc này**
- Nghĩa là ràng buộc này **chưa có căn cứ nào từ khách**. Đây là **câu hỏi mới phải gửi khách**,
  không có trong `client-qa-list.md` — phát hiện khi đọc `R-15`
- **Giả định vendor:** giữ nguyên (`PREMISE GĐ-L5-3`)
- **Mức đổi:** Thấp nếu khách xác nhận · **Lớn** nếu khách cần nhiều tuyến/ngày — phải bỏ chỉ mục
  và đổi cả cách định danh tuyến

**References**
- `MIG-R:18-21` · `R-15` · `PREMISE.md` §2 `GĐ-L5-3`

---

#### `[INVESTIGATION]` E01-INV-04 — Confirm Q56: route status enum has 2 values or 6

**Overview**
- Khách mô tả tuyến đi qua **sáu** trạng thái `created → checked → published → in-progress →
  completed/cancelled`; enum `route_status` hôm nay đúng **hai** giá trị
- **Giả định vendor:** giữ hai giá trị `draft` · `published`
- **Mức đổi:** Nhỏ — chỉ đổi state machine. Nhưng `in-progress`/`completed` còn cần **sự kiện tài
  xế ghi khi chạy tuyến**, thứ hôm nay không có → khi đó mức đổi thành **Vừa**
- **Tầng:** `DB (migration)` nếu phải thêm giá trị enum

**References**
- SCR-28 §6.3 #8 · `MIG-E:56-59` · `QA:81` · `RFPJA:801`

---

---

### E02 · Luật giờ lái 2024 — kiểm trong một ngày

#### Cây E02

```
[EPIC] E02 Enforce 2024 driver-hour limits within a single service day
└── [STORY] US-13 Dispatcher sees four driver-hour threshold results while building a route
    ├── [PARENT][BE] E02-BE Build driver-hour rule engine and rule-version storage
    │   ├── E02-BE-01 Add unique(valid_from) to driver_rule_versions
    │   ├── E02-BE-02 Add six missing threshold columns to driver_rule_versions
    │   ├── E02-BE-03 Build driver-hours.ts skeleton, time axis and empty-data cases
    │   ├── E02-BE-04 Enforce max_continuous_drive_min and report exact violation range
    │   ├── E02-BE-05 Enforce max_binding_min_per_day incl. return leg and service time
    │   ├── E02-BE-06 Reset driving streak at break_reset_min with non-strict >=
    │   ├── E02-BE-07 Enforce max_route_hours cap in pure-function unit tests
    │   ├── E02-BE-08 Select rule version by service_date instead of now()
    │   └── E02-BE-09 Implement check_result jsonb contract per PREMISE V-3
    └── [PARENT][FE] E02-FE Build block C compliance panel on SCR-28
        └── E02-FE-01 Render block C with four threshold rows and publish-button gating
[INVESTIGATION] E02-INV-01 Confirm Q34 special shift rules with the customer
```

**Tổng E02: 1 epic + 1 story + 2 parent + 10 dev task + 1 investigation = 15 item.**

Gộp hai task (khoảng vi phạm → `E02-BE-04`; hệ quả lên nút → `E02-FE-01`) bù đúng phần cấp Story thêm
vào, nên tổng backlog vẫn **~120 item** như `BAN-GIAO.md` §2 #1 đã chốt. Không mất việc nào — hai
việc gộp vẫn đứng thành khối bullet riêng, có đủ mã AC.

⚠ Thêm cấp **Story** làm tổng backlog vượt con số `~120` đã chốt ở `BAN-GIAO.md` §2 #1:
13 epic + ~15 story + 73 + ~35 ≈ **~136 item**. Cần xác nhận trước khi chạy 12 epic còn lại.

---

#### `[EPIC]` Enforce 2024 driver-hour limits within a single service day

**Overview & Goal**
- As a `配送計画者` (*"Điều phối giao hàng"*)
- I want hệ thống kiểm bốn ngưỡng giờ lái ngay lúc tôi dựng tuyến
- So that tuyến phát cho tài xế không vi phạm luật giờ lái Nhật 2024

**Scope & Features**
- Bốn ngưỡng của bản luật `DRV-RULE-2026-v1`, đọc từ DB, không viết cứng
- Hàm thuần `lib/rules/driver-hours.ts` — tính lại tại chỗ, không gọi máy chủ
- Chọn bản luật theo `service_date`, không theo `now()`
- Khoảng thời gian vi phạm chính xác (`C-13`)
- Chỗ lưu cho sáu ngưỡng còn thiếu — chỉ thêm cột, chưa cài phép kiểm
- Khối `C` trên SCR-28: bốn dòng riêng, mỗi dòng một badge

**Ngoài phạm vi** (ghi rõ để không ai tưởng bỏ sót)
- Ghim `driver_rule_version_id` lúc công bố → **E03**
- Chỗ lưu điểm nghỉ `休憩` → **E04**
- Hai ngưỡng bình quân nhiều ngày → **E05**, chờ Q13

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-28-36** — Given `R-SEED-02` đúng như seed · When mở màn · Then khối C ra đúng bộ bốn kết
  quả: ① `超過` 410/240 · ② `OK` 455/780 · ③ `超過` · ④ `OK` 7h35/24h
- **AC-28-63** đảo chiều — Given grep `driver_rule` trên `lib/ app/ components/` · When module
  lập lịch đã sống · Then có hit ở mã ứng dụng, không chỉ ở `database-generated.ts`

**References & Dependencies**
- Spec: `04-screen-specs/scr-28-tao-tuyen-giao-hang.md` §6.2.1 · §6.3 #1 #3 #4 #10 #13 #19 ·
  §6.4.4 §6.4.5 §6.4.9
- Estimate LAB-1 đối chiếu: F06 / `FT-06-03` — 29 SP / 16 MD
- Phụ thuộc: T0 migration nền

---

#### `[STORY]` US-13 — Dispatcher sees four driver-hour threshold results while building a route

**Overview**
- **Who:** `配送計画者`
- **What:** thấy bốn dòng kết quả ngưỡng giờ lái, cập nhật ngay mỗi lần đổi tuyến
- **Why:** biết tuyến vi phạm ở ngưỡng nào để sửa trước khi công bố

**Acceptance Criteria**
- **AC-28-34** — Given tuyến bất kỳ · When khối C render · Then hiện **đủ bốn dòng riêng**, mỗi
  dòng một badge và một số đo kèm `上限`; **cấm** gộp thành một câu
- **AC-28-35** — Given khối C · When render · Then có dòng `A-15 ルール版 DRV-RULE-2026-v1`, bốn trần
  bằng đúng giá trị cột `240 · 780 · 30 · 24`
- **AC-28-26** — Given chuỗi lái liên tục đúng 240 phút · When render · Then ① badge `OK`,
  hiện `240分 / 上限 240分`
- **AC-28-27** — Given chuỗi lái 241 phút · When render · Then ① badge `超過`, hiện `241分 / 上限 240分`
- **AC-28-28** — Given `拘束時間` đúng 780 phút · When render · Then ② badge `OK`; Given 781 phút ·
  Then ② badge `超過`
- **AC-28-30** — Given một điểm dừng đúng 30 phút · When tính ① · Then chuỗi lái reset về 0;
  Given điểm dừng 29 phút · Then chuỗi lái giữ nguyên
- **AC-28-33** — Given tổng thời gian tuyến đúng 1.440 phút · When render · Then ④ badge `OK`;
  Given 1.441 phút · Then ④ badge `超過`
- **AC-28-37** — Given `R-SEED-02` · When đọc `C-13` của dòng ① · Then khoảng vi phạm là
  `12:20 → 15:35`, số phút vượt trần là `170分`
- **AC-28-24** — Given thao tác bất kỳ ở `A-2`…`A-4` hoặc `B-9`…`B-11` · When thao tác xong ·
  Then bốn dòng tính lại và hiện ngay, **không** phát sinh lượt gọi máy chủ
- **AC-28-41** — Given `R-SEED-02` mở hai lần, dữ liệu không đổi · When so hai kết quả ·
  Then giống hệt nhau
- **AC-28-58** — Given hai bản luật đều có `valid_from <= service_date` · When render ·
  Then dùng bản `valid_from` lớn nhất, `A-15` hiện đúng `version_label` của bản đó
- **AC-28-59** — Given bản luật có `valid_from` **sau** `service_date` · When render ·
  Then bản đó không được dùng

**References & Dependencies**
- Spec: SCR-28 §6.4.4 · §6.4.5 · §6.4.9
- Dữ liệu kiểm: `03-wireframes/README.md` §4 — seed `R-SEED-02`, `DRV-RULE-2026-v1`, ma trận 56 chặng

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E02-BE — Build driver-hour rule engine and rule-version storage

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 9 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- Gom toàn bộ phần máy chủ của `US-13`: chỗ lưu bản luật, hàm thuần tính bốn ngưỡng, hợp đồng
  `check_result`
- Không tự có code — đóng khi 9 task con đóng hết
- Thứ tự chạy: `E02-BE-01` → `E02-BE-08` · `E02-BE-03` → `E02-BE-04`…`07` · `E02-BE-09` sau cùng

**Impact Range**
- `driver_rule_versions` · `lib/rules/driver-hours.ts` · `route_versions.check_result`

---

##### `[DEV TASK]` E02-BE-01 — Add unique(valid_from) to driver_rule_versions

- **Task Type:** Development - Backend · **Task Category:** Task
- **Tầng:** `DB (migration)` · **Sprint 1** (trong T0) · **Chặn:** E02-BE-08

**Specification**
- Thêm ràng buộc `unique (valid_from)` vào `driver_rule_versions`
- Làm theo khuôn bảng cùng họ `temperature_threshold_versions` — đã có `unique (temp_zone, valid_from)`
- Vì sao: hai bản cùng `valid_from` thì `order by valid_from desc limit 1` cho kết quả **không xác
  định** — mở cùng một tuyến hai lần có thể ra hai kết quả kiểm khác nhau
- **AC-28-60** đảo chiều — Given hai dòng `driver_rule_versions` cùng `valid_from` · When ghi dòng
  thứ hai · Then DB từ chối ngay ở tầng ràng buộc
- Hôm nay seed chỉ một dòng nên lỗi chưa lộ — không chờ nó lộ mới sửa

**Impact Range**
- Bảng `driver_rule_versions`
- Câu tra bản luật trong `driver-hours.ts` (E02-BE-08)

---

##### `[DEV TASK]` E02-BE-02 — Add six missing threshold columns to driver_rule_versions

- **Task Type:** Development - Backend · **Task Category:** Task
- **Tầng:** `DB (migration)` · **Sprint 2**

**Specification**
- Thêm sáu cột ngưỡng: 960h/năm · 3.300h/năm · 284h/tháng · trần 15h cho ngày ngoại lệ ·
  nghỉ giữa ca 11h · 9h
- **Bẫy:** bảng là **append-only** — không sửa dòng cũ; mọi bản luật đã có phải nhận giá trị mặc
  định **có chủ ý**, và phải viết ra chọn giá trị nào, vì sao
- **Chỉ thêm chỗ lưu, không cài phép kiểm** — phép kiểm cộng dồn nằm ở E05
- `[tự viết]` Given sáu cột đã thêm · When đọc `DRV-RULE-2026-v1` · Then bốn trần cũ không đổi,
  `AC-28-35` vẫn đúng
- `[tự viết]` Given bản luật cũ · When migration chạy xong · Then mỗi cột mới có giá trị mặc định
  đã ghi lý do trong file migration

**Impact Range**
- Bảng `driver_rule_versions` · seed `SEED2:22-25`
- `lib/types/database-generated.ts`

---

##### `[DEV TASK]` E02-BE-03 — Build driver-hours.ts skeleton, time axis and empty-data cases

- **Task Type:** Development - Backend · **Task Category:** Task
- **Tầng:** `RPC / luật` · **Sprint 1** (T1 — chạy song song được với T0)

**Specification**
- Dựng `lib/rules/driver-hours.ts` theo lối `lib/rules/delivery-window.ts` đã có
- Phạm vi task này: chữ ký hàm, dựng trục thời gian từ `travel_times` + `service_minutes` +
  `start_time`, và các ca rỗng / thiếu dữ liệu. **Bốn ngưỡng nằm ở `E02-BE-04`…`E02-BE-07`**
- **AC-28-41** — Given cùng dữ liệu · When chạy hai lần · Then ra một kết quả (hàm xác định)
- **AC-28-24** — Given một thao tác trên màn · When tính lại · Then **không** gọi máy chủ
- **AC-28-12** — Given tuyến 0 điểm giao · When render · Then vẫn đủ bốn dòng, 0 phút lái
- **AC-28-13** — Given thiếu một chặng `travel_times` · When render · Then **không** hiện số cho
  ①②④, hiện `C-11` nêu đích danh chặng thiếu, và chặng đó **không** bị tính là 0 phút
- **AC-28-14** — Given `start_time` là NULL · When render · Then hiện `C-12`, không hiện bốn dòng
- **AC-28-15** — Given không có bản luật nào `valid_from <= service_date` · When render ·
  Then hiện `C-12`, **không** có bốn dòng `OK` giả

**Impact Range**
- `lib/rules/driver-hours.ts` (mới) · unit test đi kèm
- Màn SCR-28 khối `C` (E02-FE-01)

---

##### `[DEV TASK]` E02-BE-04 — Enforce max_continuous_drive_min and report exact violation range

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`

**Specification**
- Ngưỡng ① `連続運転` (*"Lái liên tục"*), trần 240 phút, so sánh **`>` nghiêm**
- `サービスタイム` **không** vào ① (quyết định `Đ-2`)
- **AC-28-26** — Given chuỗi lái đúng 240 phút · When render · Then ① `OK`, hiện `240分 / 上限 240分`
- **AC-28-27** — Given 241 phút · When render · Then ① `超過`, hiện `241分 / 上限 240分`
- **AC-28-38** — Given tắt quyết định `Đ-1` (không tính chặng về) · When tính ① · Then ra 270 phút
- Cách người dùng sửa: đổi thứ tự điểm giao, hoặc chèn điểm nghỉ → lý do ① không gộp với ②

**Khoảng thời gian vi phạm** (`C-13`) — `FR-SCH-02` nghiệm thu đích danh
`正確な違反時間範囲を表示` (*"hiển thị chính xác khoảng thời gian vi phạm"*), không chỉ đòi báo có
vi phạm:
- **AC-28-37** — Given `R-SEED-02` · When đọc `C-13` của dòng ① · Then khoảng là `12:20 → 15:35`,
  số phút vượt trần là `170分`

**Impact Range**
- `lib/rules/driver-hours.ts` · item `C-13` của khối C

---

##### `[DEV TASK]` E02-BE-05 — Enforce max_binding_min_per_day including return leg and service time

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`

**Specification**
- Ngưỡng ② `拘束時間` (*"Thời gian ràng buộc"*), trần 780 phút/ngày, so sánh **`>` nghiêm**
- Hai quyết định đã chốt phải cài đúng: `Đ-1` tính cả chặng quay về DEPOT · `Đ-2` `サービスタイム`
  vào ② và ④, **không** vào ①
- **AC-28-28** — Given 780 phút · Then ② `OK`; Given 781 phút · Then ② `超過`
- **AC-28-29** — Given tuyến `DEPOT → CUS-006 → CUS-005 → CUS-006 → CUS-005 → DEPOT` · When render ·
  Then ② ra con số **khác** ① — hai ngưỡng không dùng chung một biến
- **AC-28-36** — Given `R-SEED-02` · When render · Then ② = 455 phút, badge `OK`
- **AC-28-38** — Given tắt `Đ-1` · When tính ② · Then ra 315 phút
- **Đã biết là ước lượng thấp:** giờ chuẩn bị trước `出発時刻` và giờ hoàn tất sau khi về kho không
  có chỗ lưu, nên hôm nay đo từ `start_time` (6.3 #3). Ghi `PREMISE.md`, không mở task riêng vòng này

**Impact Range**
- `lib/rules/driver-hours.ts`

---

##### `[DEV TASK]` E02-BE-06 — Reset driving streak at break_reset_min with non-strict >= comparison

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`

**Specification**
- Ngưỡng ③, trần 30 phút, so sánh **`>=` KHÔNG nghiêm** — đây là lý do ③ đứng riêng khỏi ①②④
- **AC-28-30** — Given điểm dừng đúng 30 phút · When tính ① · Then chuỗi lái reset về 0;
  Given 29 phút · Then chuỗi lái giữ nguyên
- **AC-28-31** — Given không có điểm dừng nào ≥30 phút và ① đang `超過` · When render ·
  Then ③ `超過` kèm `C-14` nêu **đích danh** điểm dừng ngắn nhất và thời lượng của nó
- **AC-28-32** — Given có ít nhất một điểm dừng ≥30 phút · When render · Then ③ `OK`
- **AC-28-39** — Given `R-SEED-02` · When đọc `C-14` · Then câu nêu `CUS-007` và `25分`, không phải
  câu chung chung về "chưa đủ nghỉ"

**Impact Range**
- `lib/rules/driver-hours.ts`

---

##### `[DEV TASK]` E02-BE-07 — Enforce max_route_hours cap in pure-function unit tests

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`

**Specification**
- Ngưỡng ④ `ルート時間` (*"Thời lượng tuyến"*), trần 24 giờ, so sánh **`>` nghiêm**
- **AC-28-33** — Given tổng 1.440 phút · Then ④ `OK`; Given 1.441 phút · Then ④ `超過`.
  **Nghiệm thu ở unit test của hàm thuần, không qua CSDL**
- **AC-28-36** — Given `R-SEED-02` · When render · Then ④ = 7 giờ 35 phút, badge `OK`
- **Vì sao chạy ở unit test — mâu thuẫn M-2:** `Đ-3` chốt tuyến không vắt qua nửa đêm, ② chặn ở
  780 phút/ngày → **không dựng được ca dữ liệu hợp lệ nào** để ④ chạm 1.440 mà ② vẫn `OK`.
  Giả định đã ghi `PREMISE.md`. Không làm vậy thì nhánh ④ là mã chết

**Impact Range**
- `lib/rules/driver-hours.ts` · unit test

---

##### `[DEV TASK]` E02-BE-08 — Select rule version by service_date instead of now()

- **Task Type:** Development - Backend · **Task Category:** Task
- **Tầng:** `RPC / luật` · **Phụ thuộc:** E02-BE-01

**Specification**
- Tra bản luật theo `routes.service_date`, **không** theo `now()` (`R-18`)
- Bốn trần đọc từ cột của bản đã chọn — **không** số nào viết cứng trong mã
- **AC-28-58** — Given hai bản đều `valid_from <= service_date` · When render · Then dùng bản
  `valid_from` lớn nhất, `A-15` hiện đúng `version_label` của bản đó
- **AC-28-59** — Given bản có `valid_from` **sau** `service_date` · When render · Then không dùng
  bản đó — mốc tra là **ngày chạy tuyến**
- **AC-28-35** — Given khối C render · Then bốn trần bằng đúng giá trị cột
- Thiếu E02-BE-01 thì kết quả không xác định → E02-BE-01 phải xong trước

**Impact Range**
- `lib/rules/driver-hours.ts` · bảng `driver_rule_versions`

---

##### `[DEV TASK]` E02-BE-09 — Implement check_result jsonb contract per PREMISE V-3

- **Task Type:** Development - Backend · **Task Category:** Task
- **Tầng:** `RPC / luật` · **Nơi tiêu thụ:** E03 `publish_route`

**Specification**
- Hợp đồng đã chốt ở `PREMISE.md` §3 **`V-3`** — task này **cài đặt**, không mở lại thiết kế
- Ba khoá cấp trên giữ nguyên: `ok` · `violations` · `ruleVersion`
- Một phần tử `violations`:

```json
{ "threshold": "continuous_drive" | "binding" | "break_reset" | "route_hours",
  "measured": 410, "limit": 240,
  "from": "12:20", "to": "15:35", "overMinutes": 170 }
```

- Ba khoá `from` · `to` · `overMinutes` **chỉ có ở** `continuous_drive`
- Bốn mã `threshold` khớp đúng bốn cột của `driver_rule_versions`
- `[tự viết]` Given `R-SEED-02` · When chạy `driver-hours.ts` · Then ra `check_result` có đúng hai
  phần tử `violations`: `continuous_drive` (410/240, `12:20→15:35`, 170) và `break_reset`
- `[tự viết]` Given hợp đồng này · When E03 `publish_route` ghi vào `route_versions.check_result` ·
  Then không phải đổi kiểu, và bản seed `R-SEED-01` đọc lên vẫn hợp lệ

**Điểm hở còn lại** — hình dạng `V-3` **không có khoá nào trỏ tới điểm dừng ngắn nhất**, trong khi
`AC-28-31` / `AC-28-39` đòi `C-14` nêu đích danh (`CUS-007`, `25分`). Hôm nay `C-14` dựng tại chỗ
lúc render nên không sao; bản đã công bố thì **không tự giải thích được** vi phạm ③. Hai đường:
thêm một khoá `stopRef` cho riêng `break_reset`, hoặc chấp nhận và ghi thành quyết định. **Chưa
chốt** — nêu ở đây để bước 8 không bỏ sót.

**Impact Range**
- `lib/rules/driver-hours.ts` · `route_versions.check_result` · E03 `publish_route`

---

#### `[PARENT][FE]` E02-FE — Build block C compliance panel on SCR-28

- **Task Type:** Development - Frontend · **Task Category:** **Feature**
- **Tầng:** `UI`

**Specification**
- Gom phần giao diện của `US-13`: khối `C` bốn dòng ngưỡng và hành vi hai nút `D-1` `D-2`
- Phụ thuộc `[PARENT][BE]` — cần hợp đồng vào/ra của `driver-hours.ts` trước

**Impact Range**
- `app/(app)/routes/` — khối `C`, item `C-9`…`C-14`, `A-15`, nút `D-1`, `D-2`

---

##### `[DEV TASK]` E02-FE-01 — Render block C with four threshold rows and publish-button gating

- **Task Type:** Development - Frontend · **Task Category:** Task
- **Tầng:** `UI` · **Sprint 1** (T3) · **Phụ thuộc:** E02-BE-03 · E02-BE-08

**Specification**
- Dựng khối `C` trên SCR-28 — bốn dòng ngưỡng, mỗi dòng một badge và một số đo
- **AC-28-34** — Given tuyến bất kỳ · When render · Then đủ **bốn dòng riêng** kèm `上限`;
  **cấm** gộp thành `このルートは法定基準を満たしていません`
- **AC-28-35** — Given khối C · When render · Then có `A-15 ルール版 …`, bốn trần đọc từ DB
- **AC-28-36** — Given `R-SEED-02` · When render · Then ra đủ bốn kết quả đúng số
- **AC-28-12** — Given tuyến không còn điểm giao nào · When render · Then khối C **vẫn hiện đủ bốn
  dòng**, cả bốn `OK` với 0 phút — không ẩn khối
- **AC-28-13** — Given thiếu chặng `travel_times` · When render · Then hiện `C-11` nêu đích danh
  chặng thiếu, `D-2` tắt
- **AC-28-14 / AC-28-15** — Given thiếu `start_time` hoặc thiếu bản luật · When render ·
  Then hiện `C-12` thay cho bốn dòng
- **AC-28-24** — Given một thao tác ở `A-2`…`B-11` · When xong · Then bốn dòng tính lại và hiện
  ngay, không cần bấm nút

**Hệ quả của vi phạm lên hai nút** — vi phạm giờ lái **không** chặn lưu nháp, chỉ chặn đi tiếp
sang công bố:
- **AC-28-42** — Given `R-SEED-02` đang vi phạm ① và ③ · When bấm `D-1 下書き保存` · Then lưu thành
  công (2xx), tuyến vẫn `draft`, `current_version = 0`
- **AC-28-43** — Given cùng tuyến · When nhìn `D-2 公開へ進む` · Then nút **tắt**, cuối khối `C`
  hiện `C-9` nói rõ lưu nháp được nhưng công bố thì không
- **AC-28-44** — Given cùng tuyến · When đọc phản hồi của `D-1` · Then **không** có mã lỗi nào
  trong thân phản hồi — vi phạm là **trạng thái màn hình**, không phải mã lỗi
- **AC-28-45** — Given tuyến đạt cả bốn ngưỡng · When bấm `D-2` · Then chuyển sang SCR-29 mà
  **không** ghi gì vào CSDL
- ⚠ **M-1:** `AC-28-45` chỉ hết ngõ cụt khi **E04 (chỗ lưu điểm nghỉ) xong trước** — đó là lý do
  E04 chặn E03

**Impact Range**
- Màn SCR-28 (`app/(app)/routes/`) · khối `C`, item `C-9`…`C-14`, `A-15` · nút `D-1`, `D-2` ·
  endpoint lưu nháp

---

#### `[INVESTIGATION]` E02-INV-01 — Confirm Q34 special shift rules with the customer

**Overview**
- Hỏi khách: có áp dụng các ca đặc biệt của Thông cáo tiêu chuẩn cải thiện không — phà, đường dài,
  ca chia đôi (`QA:48`)
- **Giả định vendor đang dùng:** **không áp dụng**
- **Mức đổi nếu đáp án khác:** Vừa
- **Không ước công, không chặn dev task nào.** Đóng khi khách trả lời

**References**
- `client-qa-list.md` Q34 · SCR-28 §6.3 #13 · quyết định `Đ-2`

---

##### Sáu hạng mục của cụm giờ lái — ba cái không nằm ở E02

| # | Hạng mục | Ở đâu | Vì sao không ở E02 |
|---|---|---|---|
| 1 | Khoảng vi phạm chính xác | **E02-BE-08** | — |
| 2 | Chọn bản luật theo `service_date` | **E02-BE-08** | — |
| 3 | Ghim `driver_rule_version_id` lúc công bố | **E03** | Tầng khác (SCR-29), và phải từ chối nếu bản luật đổi giữa lúc kiểm và lúc ghi — `AC-28-61` `AC-28-62` `R-20` |
| 4 | Cấu trúc `check_result` | **E02-BE-09** | — |
| 5 | Chỗ lưu điểm nghỉ `休憩` | **E04** | Là `DB (migration)` + đổi `snapshot`, không phải phép tính. **M-1 đẩy E04 lên trước E03** |
| 6 | 8/11 ngưỡng chưa phủ | **E02-BE-02** (6 cái thiếu cột) + **E05** (2 cái thiếu nguồn dữ liệu) | Hai nhóm chi phí khác hẳn: thêm cột thì ước được; thiếu giờ đã làm của ngày trước thì **chờ Q13**, mức đổi Vừa→Lớn |

---

### E03 · Công bố tuyến có phiên bản

| | |
|---|---|
| **Màn** | SCR-29 |
| **Dòng 6.3 hút vào** | #1 · #2 · #3 · #4 · #5 · #7 · #8 · #9 · #10 · #11 · #12 · #13 · #16 · #17 · #18 |
| **Nhóm LAB-1 đối chiếu** | F06 · `FT-06-05` — 13 SP / 8 MD |
| **Số item** | 1 epic + 1 story + 2 parent + 15 dev task + 2 investigation = **21** |

⚠ **Lệch đáng kể với LAB-1.** `FT-06-05` chỉ 13 SP / 8 MD, trong khi LAB-4 gọi `publish_route`
là *"hạng mục nặng nhất của màn"* — năm việc một giao dịch, ghim bản luật, dựng `snapshot`,
khoá dòng. Ghi lại để `estimate.md` §5 giải thích chênh lệch, **không** cắt task cho khớp số cũ.

```
[EPIC] E03 Publish routes as immutable versions with pinned rule version
└── [STORY] US-14 Dispatcher publishes a route version that drivers receive and auditors can trace
    ├── [PARENT][BE] E03-BE Build publish_route and its version/audit guarantees
    │   ├── E03-BE-01 Create publish_route RPC performing five writes in one transaction
    │   ├── E03-BE-02 Build snapshot with left join so stops without orders survive
    │   ├── E03-BE-03 Pin the rule version used by the check and reject if it changed
    │   ├── E03-BE-04 Block publishing of violating and empty routes with precise codes
    │   ├── E03-BE-05 Lock the routes row to serialise concurrent publishes
    │   ├── E03-BE-06 Require change_reason from version 2 onward
    │   ├── E03-BE-07 Record blocked publish attempts in the events table
    │   ├── E03-BE-08 Add storage for which version each driver has seen
    │   ├── E03-BE-09 Expose publish API carrying the checked rule version id
    │   └── E03-BE-10 Add checkedRules key so check_result states what it verified
    └── [PARENT][FE] E03-FE Build SCR-29 publish screen and the driver-facing indicator
        ├── E03-FE-01 Build screen shell reachable only from SCR-28 with four load states
        ├── E03-FE-02 Build diff block C-4 against the previous snapshot
        ├── E03-FE-03 Build publish history block D
        ├── E03-FE-04 Build violation panel B with disabled publish and replan exit
        └── E03-FE-05 Review 18 new Japanese strings with a native speaker
[INVESTIGATION] E03-INV-01 Confirm how drivers should be told a new version exists
[INVESTIGATION] E03-INV-02 Confirm cross-route audit lookup is out of scope until SCR-41
```

---

#### `[EPIC]` E03 — Publish routes as immutable versions with pinned rule version

**Overview & Goal**
- As a `配送計画者` (*"Điều phối giao hàng"*)
- I want công bố tuyến thành một bản bất biến có ghim phiên bản luật
- So that tài xế luôn nhận bản mới nhất, và `監査者` (*"kiểm toán viên"*) tra lại được bản cũ

**Scope & Features**
- `publish_route` — **không tồn tại trong migration nào**; `grep -rn "publish_route" supabase/` ra 0 hit
- Năm việc trong **một** giao dịch, có khoá dòng `routes`
- Ghim `driver_rule_version_id` **đúng bản đã dùng để kiểm**, từ chối nếu bản luật đổi giữa chừng
- `snapshot` dựng bằng **`left join`** để điểm dừng không đơn không bị mất im lặng
- Màn SCR-29: 4 section, khối so khác biệt, lịch sử công bố
- Chỗ lưu *"tài xế đã xem bản nào"* + chỉ báo trên SCR-26

**Ngoài phạm vi**
- Phép tính bốn ngưỡng → **E02** (hai màn gọi **cùng một** hàm, không viết lại)
- Chèn điểm nghỉ → **E04** · Tra cứu xuyên tuyến xuyên ngày → **SCR-41**, wave 3
- Thông báo đẩy → **chưa có màn nào**; quyết định 8.4 chọn chỉ báo trên màn

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-29-02** đảo chiều — Given grep `publish_route` trên `supabase/` · When module đã sống ·
  Then có kết quả, không còn 0 hit
- **AC-29-39** — Given `publish_route` chạy · When bất kỳ việc nào trong năm việc hỏng ·
  Then **không việc nào** để lại dấu vết

**References & Dependencies**
- Spec: `scr-29-cong-bo-tuyen-giao-hang.md` §6.3 toàn bộ · §6.4.1…§6.4.9
- Estimate LAB-1: F06 / `FT-06-05` — 13 SP / 8 MD
- **Bị chặn bởi E04** (M-1, `PREMISE` §3 `V-1`) · Phụ thuộc **E02** (hàm `driver-hours.ts`)

---

#### `[STORY]` US-14 — Dispatcher publishes a route version that drivers receive and auditors can trace

**Overview**
- **Who:** `配送計画者`, và `ドライバー` ở đầu ra
- **What:** công bố tuyến thành bản có số thứ tự, ghim bản luật, bản cũ giữ nguyên
- **Why:** tuyến đã phát là chứng cứ pháp lý — phải tra lại được "lúc đó đã kiểm theo luật nào"

**Acceptance Criteria**
- **AC-29-16** — Given tuyến `draft` đạt cả bốn ngưỡng · When mở màn · Then `C-7 公開する` **bật**,
  `B-8` hiện `DRV-RULE-2026-v1`, `C-3` liệt đủ điểm giao theo `seq` tăng dần
- **AC-29-18** — Given `publish_route` chạy xong 2xx · When đọc CSDL · Then **đúng một** dòng
  `route_versions` mới `version_no=1`, `change_reason` NULL, `published_by` = id người bấm
- **AC-29-19** — Given cùng lần công bố · When đọc `routes` · Then `status='published'` **và**
  `current_version=1` — hai cột đổi trong **cùng** giao dịch với dòng `route_versions`
- **AC-29-20** — Given cùng lần công bố · When đọc `snapshot` · Then **đúng sáu khoá** `routeCode` ·
  `serviceDate` · `startTime` · `vehicleCode` · `driverCode` · `stops`; mỗi phần tử `stops` có
  `seq` · `orderId` · `customerRef` · `deliveryPointCode`
- **AC-29-22** — Given cùng lần công bố · When đọc `check_result` · Then ba khoá `ok` ·
  `violations` · `ruleVersion`, với `ok=true`, `violations=[]`, `ruleVersion='DRV-RULE-2026-v1'`
- **AC-29-23** — Given công bố xong · When màn render lại · Then `C-9` hiện
  `第1版として公開しました。ドライバーには最新版が表示されます。`, `A-3` đổi sang `公開済み`,
  khối `D` có **một** dòng, màn **không** điều hướng đi đâu
- **AC-29-25** — Given `R-SEED-01` (`published`, `current_version=1`) · When mở màn · Then `A-8`
  hiện `第1版（公開 2026/10/09 17:00）`, `C-2` ghi `第2版 として公開します`, `C-5 変更理由` hiện
  kèm `M_04 必須`
- **AC-29-28** — Given `C-5` có chữ · When công bố · Then dòng `route_versions` mới `version_no=2`
  với `change_reason` đúng chuỗi đã nhập, **và** dòng `version_no=1` **không bị sửa một cột nào**
- **AC-29-52** — Given tuyến vừa công bố cho `DRV-01` · When tài khoản `ドライバー` mở SCR-26 ·
  Then băng hiện tuyến đó với `第{n}版（公開 …）` của bản mới nhất
- **AC-29-53** — Given tuyến đã công bố bản 2 · When tài xế mở lại SCR-26 · Then băng hiện **bản 2**
- **AC-29-57** — Given một bản đã công bố · When tìm thao tác thu hồi hay huỷ bản · Then **không có
  thao tác nào** — enum chỉ `draft` | `published`
- **AC-29-58** — Given muốn huỷ nội dung đã phát · When làm · Then đường duy nhất là **công bố bản
  mới kèm lý do**, bản cũ vẫn nằm nguyên trong khối `D`

**References & Dependencies**
- Spec: SCR-29 §6.4.3 · §6.4.4 · §6.4.7 · §6.4.8 · §6.4.9
- Dữ liệu kiểm: `R-SEED-01` (bản 1, `SEED5:42-54`) · `R-SEED-02` (`draft`)

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E03-BE — Build publish_route and its version/audit guarantees

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 10 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật` + `API route`

**Specification**
- Gom toàn bộ phần máy chủ của `US-14`. Hôm nay **không có gì** — nhánh lập tuyến cắt ở phase 04c
- **Dùng lại** `lib/rules/driver-hours.ts` của E02, **không** viết lại phép tính
- Thứ tự: `E03-BE-01` → `02` `03` `04` `05` `06` → `09`; `07` `08` `10` làm sau, không chặn ai

**Impact Range**
- `route_versions` · `routes` · `events` · `app/api/routes/publish/`

---

##### `[DEV TASK]` E03-BE-01 — Create publish_route RPC performing five writes in one transaction

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Sprint 2** (T5)

**Specification**
- Dựng `publish_route` làm **năm việc trong một giao dịch**: tính `version_no`, dựng `snapshot`,
  dựng `check_result`, chèn `route_versions`, UPDATE `routes`
- **AC-29-18** — Given chạy xong 2xx · When đọc CSDL · Then đúng một dòng `route_versions` mới
- **AC-29-19** — Given cùng lần đó · When đọc `routes` · Then `status='published'`,
  `current_version=1`, đổi trong **cùng** giao dịch
- **AC-29-39** — Given bất kỳ việc nào trong năm việc hỏng · When chạy · Then **không việc nào**
  để lại dấu vết
- **AC-29-40** — Given cố ý đổi `routes.status='published'` khi `current_version` vẫn `0` ·
  When chạy · Then CSDL **từ chối** bằng `check (status <> 'published' or current_version >= 1)`
- **AC-29-41** — Given cố ý tạo dòng `route_versions` mà **không** UPDATE `routes` · When chạy ·
  Then CSDL **chấp nhận**, và tài xế **không** thấy gì — đây là thứ tự sai CSDL **không** chặn,
  và là lý do năm việc phải nằm trong một hàm
- **AC-29-44** — Given UPDATE hoặc DELETE lên dòng `route_versions` đã có · When chạy · Then
  `forbid_mutation()` `raise 'APPEND_ONLY'`, API trả **500 `internal_error`** — ⚠ hiện trạng đã
  biết là **chưa đúng về status** (`01-architecture.md` §3.1 ‡ ghi là suy luận chưa chạy thử)

**Impact Range**
- `route_versions` · `routes` · trigger `forbid_mutation()`

---

##### `[DEV TASK]` E03-BE-02 — Build snapshot with left join so stops without orders survive

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Câu dựng `snapshot.stops` của seed dùng `join public.orders` → điểm dừng **không có đơn** bị loại
  khỏi mảng. `R-SEED-02` có **hai** điểm dừng `order_id = null`, comment `MIG-R:23` ghi đích danh
  là **hợp lệ**
- Chép thẳng câu của seed là **mất im lặng** mọi điểm dừng không đơn — và đó đúng là hình dạng của
  một tuyến mới lập
- **AC-29-20** — Given lần công bố · When đọc `snapshot` · Then đúng sáu khoá cấp trên, mỗi phần tử
  `stops` có bốn khoá
- **AC-29-21** — Given tuyến có điểm dừng `order_id = null` · When công bố · Then điểm dừng đó
  **vẫn nằm trong** `snapshot.stops` với `orderId = null` và `customerRef = null`

**Impact Range**
- `publish_route` · `route_versions.snapshot`

---

##### `[DEV TASK]` E03-BE-03 — Pin the rule version used by the check and reject if it changed

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `API route` · **Phụ thuộc:** `E02-BE-08`

**Specification**
- **US-14 AC3** (P0): *"tuyến gắn phiên bản quy tắc tài xế tại thời điểm công bố; đổi quy tắc sau
  đó không áp ngược"*
- Cách rẻ nhất khi dựng `publish_route` là đọc `driver_rule_versions` một lần nữa lúc ghi và ghim
  bản mới nhất — kết quả là **bản được ghim khác bản đã dùng để kiểm**. Không được làm vậy
- `publish_route` **nhận id bản luật mà khối `B` đã dùng** làm tham số, đọc lại bản hiệu lực
  **trong cùng giao dịch**, và `raise` khi hai id khác nhau — không tự chọn bản thay người dùng
- **AC-29-46** — Given tuyến đạt bốn ngưỡng được công bố · When đọc `driver_rule_version_id` ·
  Then bằng **đúng id bản luật khối `B` đã dùng**, không phải "bản mới nhất lúc ghi"
- **AC-29-47** — Given hai bản `valid_from` khác nhau đều `<= service_date` · When công bố ·
  Then ghim bản `valid_from` **lớn nhất**, `B-8` đã hiện đúng `version_label` trước khi bấm
- **AC-29-48** — Given bản luật đổi **giữa** lúc khối `B` kiểm và lúc ghi · When công bố ·
  Then **409** `CONFLICT_DRIVER_RULE_VERSION_CHANGED` kèm câu
  `ドライバー規則版が公開前に変更されました。法定確認をやり直してください。`
- **AC-29-49** — Given bản luật mới thêm **sau** khi tuyến đã công bố · When đọc lại bản cũ ·
  Then `driver_rule_version_id` **không đổi** — `過去バージョンは監査可能` chính là điều này
- **AC-29-50** — Given hai dòng `driver_rule_versions` cùng `valid_from` · When tra · Then kết quả
  **không xác định**. Hậu quả ở đây **nặng hơn SCR-28** vì giá trị bị ghim **vĩnh viễn** →
  `E02-BE-01` phải xong trước

**Impact Range**
- `publish_route` · `route_versions.driver_rule_version_id` · `app/api/routes/publish/`

---

##### `[DEV TASK]` E03-BE-04 — Block publishing of violating and empty routes with precise codes

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `UI`

**Specification**
- Nơi cưỡng chế thật là `publish_route`, không phải nút bị tắt trên màn (`AC-28-46`)
- **AC-29-35** — Given tuyến vi phạm · When gọi thẳng endpoint (đi vòng qua nút tắt) · Then **422**
  `RULE_ROUTE_VIOLATION`, `route_versions` **không tăng dòng**, `routes.status` vẫn `draft`
- **AC-29-36** — Given mã `RULE_ROUTE_VIOLATION` · When đi qua `mapRpcError` · Then **422** vì tiền
  tố `RULE_`; Given đặt tên `ROUTE_PUBLISH_BLOCKED` thay vào · Then **500 `internal_error`** vì
  không khớp tiền tố nào — kịch bản kiểm cho luật đặt tên của 3.2
- **AC-29-37** — Given toàn bộ phạm vi màn · When tìm đường công bố tuyến vi phạm với bất kỳ vai
  nào · Then **không tồn tại** đường nào — không cờ ghi đè, không tham số bỏ qua, không vai đặc biệt
- Tuyến **rỗng**: `R-13` chốt **chặn**, mã `RULE_ROUTE_EMPTY` — `jsonb_agg` trên tập rỗng trả `null`,
  và `snapshot.stops = null` làm băng SCR-26 hiện `配送先は登録されていません` cho một tuyến
  *"đã công bố"*
- **AC-29-11** — Given tuyến `draft` sau khi xoá hết `route_stops` · When mở màn · Then `C-3` hiện
  `配送先は登録されていません`, `C-7` **tắt**, khối `B` vẫn hiện đủ bốn dòng với 0 phút lái

**Impact Range**
- `publish_route` · `mapRpcError` · `C-7` của SCR-29

---

##### `[DEV TASK]` E03-BE-05 — Lock the routes row to serialise concurrent publishes

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `dùng chung`

**Specification**
- `unique (route_id, version_no)` **đã chặn** ca hai người cùng bấm công bố, nhưng chặn bằng một
  `conflict_duplicate` trần: không `detail`, không nói người kia vừa làm gì
- Hai việc: (a) `select … for update` trên dòng `routes` để hai phiên không cùng tính ra một
  `version_no`; (b) câu riêng `M_101`, kèm nạp lại khối `D`
- **AC-29-42** — Given hai phiên cùng bấm `公開する` trên cùng tuyến · When cả hai chạy · Then
  **đúng một** phiên thành công, phiên kia nhận **409** với câu
  `この版はすでに公開されています。最新の公開履歴を確認してください。`, `route_versions` có
  **đúng một** dòng mới
- **AC-29-43** — Given `publish_route` **không** khoá dòng `routes` · When hai phiên cùng đọc
  `current_version` · Then cả hai tính ra cùng `version_no` và một phiên vỡ ở ràng buộc unique
  thay vì được báo sớm — **đây là hành vi phải tránh**
- **AC-29-45** — Given xung đột đồng thời của Postgres (`40001` / `40P01`) · When `mapRpcError`
  xử lý · Then **409 `conflict_concurrent_update`**, màn hiện
  `処理が混み合っています。もう一度公開してください`

**Impact Range**
- `publish_route` · `mapRpcError` · `_common/thong-bao-ja.md` (`M_101`)

---

##### `[DEV TASK]` E03-BE-06 — Require change_reason from version 2 onward

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Ràng buộc `check (version_no = 1 or change_reason is not null)` đã có ở `MIG-R:46` — **không được
  để nó tự nổ**
- **AC-29-27** — Given `C-5` để trống mà gọi thẳng endpoint · When gọi · Then **422**
  `VALIDATION_CHANGE_REASON_REQUIRED` với `detail.fields = ["changeReason"]`, **không** phải 500
  (bẫy 2 của 3.2)
- **AC-29-28** — Given `C-5` có chữ · When công bố · Then `version_no=2` với `change_reason` đúng
  chuỗi, dòng `version_no=1` **không bị sửa cột nào**

**Impact Range**
- `publish_route` · `route_versions.change_reason`

---

##### `[DEV TASK]` E03-BE-07 — Record blocked publish attempts in the events table

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Hệ **không lưu vết một lần công bố bị chặn** (`R-20`). SCR-23 có `loading_checks(result='blocked')`
  cho đúng loại bằng chứng này; tuyến thì không có bảng nào
- Với một ràng buộc **pháp luật lao động**, *"ai đã thử công bố một tuyến vi phạm, lúc nào"* là thứ
  `監査者` sẽ hỏi
- Rẻ nhất: ghi một dòng `events` với `action` dạng `route.publish_blocked`, `payload` mang
  `check_result` — `events` đã có sẵn, append-only, `log_event()` đã chạy
- **AC-29-38** đảo chiều — Given một lần công bố bị chặn vì vi phạm · When tìm vết trong CSDL ·
  Then có **đúng một** dòng `events` `route.publish_blocked` (hôm nay: không vết nào)
- ⚠ **Spec khuyến nghị làm, không tự quyết** — nó thêm một hành vi khách chưa yêu cầu

**Impact Range**
- `events` · `publish_route`

---

##### `[DEV TASK]` E03-BE-08 — Add storage for which version each driver has seen

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)`

**Specification**
- **US-14 AC2** (P0): tài xế **nhận** bản mới nhất. Hôm nay tài xế **đọc được** bản mới nhất ở băng
  SCR-26 nhưng **không được báo** — không thông báo đẩy, không dấu "có bản mới"
- ⚠ **Đây là ca nguy hiểm nhất của cả màn:** tài xế đã nhận tuyến rồi mới có bản 2 thì họ chạy theo
  bản cũ mà không biết
- Cần chỗ lưu *"tài xế đã xem bản nào"* → **chưa có cột**. Đề xuất một cột trên `pods` hoặc một bảng
  mới; **LAB-5 chọn và đặt tên**
- **AC-29-55** đảo chiều — Given tài xế đang xem bản 1 và bản 2 vừa công bố · When tài xế mở lại
  màn POD · Then thấy chỉ báo "có bản mới" (hôm nay: **không được báo gì**, vẫn chạy theo bản 1)
- Quyết định wireframe 8.4 giữ nguyên: **chỉ báo trên màn, KHÔNG làm thông báo đẩy**

**Impact Range**
- Bảng mới hoặc cột trên `pods` · băng SCR-26

---

##### `[DEV TASK]` E03-BE-09 — Expose publish API carrying the checked rule version id

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- 1 endpoint ghi (`POST`) + 1 endpoint đọc. `app/api/` có 14 thư mục, **không có `routes`**
- `publish_route` nhận `grant execute` cho `authenticated`; `route_versions` **không** nhận
  `grant insert`
- Đường ghi mang theo **id bản luật đã dùng để kiểm** (xem `E03-BE-03`)
- **AC-29-07** — Given tài khoản không phải `配送計画者` · When gọi thẳng endpoint công bố với thân
  hợp lệ · Then **403** `{"error":"forbidden"}`, `route_versions` không tăng dòng
- **AC-29-08** — Given gọi thẳng RPC bằng JWT của vai khác · When gọi · Then RPC `raise FORBIDDEN`,
  API trả **403** — ba tầng quyền khớp nhau
- **AC-29-15** — Given một `routeId` không tồn tại · When mở màn hoặc gọi endpoint · Then **404**
  `NOT_FOUND_ROUTE`

**Impact Range**
- `app/api/routes/publish/` · grant của `publish_route`

---

##### `[DEV TASK]` E03-BE-10 — Add checkedRules key so check_result states what it verified

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E02-BE-09` · `E02-BE-02`

**Specification**
- `check_result.ok = true` hôm nay chỉ nói *"ba ngưỡng trong một ngày đều đạt"*
- Khi `E02-BE-02` thêm sáu cột ngưỡng, một bản công bố **cũ** và một bản **mới** sẽ có cùng
  `ok = true` mà **nghĩa khác hẳn nhau**
- Thêm khoá `checkedRules: []` vào `check_result`, liệt mã các ngưỡng đã thực sự kiểm
- **AC-29-51** — Given `check_result.ok = true` của một bản đã công bố · When hỏi nó chứng thực
  những ngưỡng nào · Then trả lời được chính xác (hôm nay: **ba trong mười một**, cộng ④ từ IF-MAP-01)
- ⚠ Khoá này **không** có trong `PREMISE` §3 `V-3` — `V-3` chỉ chốt hình dạng phần tử `violations`.
  Thêm `checkedRules` là **mở rộng hợp đồng**, phải quyết cùng `E02-BE-09` trước khi có bản công bố
  vi phạm nào nằm trong CSDL

**Impact Range**
- `route_versions.check_result` · `publish_route` · `driver-hours.ts`

---

#### `[PARENT][FE]` E03-FE — Build SCR-29 publish screen and the driver-facing indicator

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 5 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Dựng cả màn SCR-29: 4 section, bảng tra 2.0, 17 trạng thái của mục 5.1
- ⚠ Màn **không bao giờ hiện trên menu**: `enabled: false` **và** `navHidden: true`. Lật
  `enabled: true` thì mục vẫn **không** hiện vì `menuForRole` lọc cả `navHidden`. Lối vào duy nhất
  là nút `公開へ進む` của `SCR-28 D-2` — **phải có `E02-FE-01` thì màn này mới tới được**

**Impact Range**
- `app/(app)/routes/` · `MENU:47` · băng `最新の公開済み配送ルート` của SCR-26

---

##### `[DEV TASK]` E03-FE-01 — Build screen shell reachable only from SCR-28 with four load states

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Sprint 2** (T6)

**Specification**
- **AC-29-03** — Given đã lật `MENU:47` · When vai `配送計画者` mở màn từ nút `公開へ進む` của SCR-28
  với một tuyến `draft` · Then 200, hiện `A-1 配送ルート公開`, `A-2 配送ルート R-SEED-02`,
  `A-3` badge `下書き`
- **AC-29-04** — Given một trong sáu vai còn lại · When mở `/routes` · Then **403**, hiện
  `M_01`/`M_02`/`M_03`, không ô nhập nào được render
- **AC-29-05** — Given `MENU:47` giữ `navHidden: true` · When vai `配送計画者` mở trang chủ ·
  Then mục `配送ルート公開` **không** nằm trong thanh điều hướng
- **AC-29-06** — Given phiên chưa đăng nhập · When mở · Then chuyển hướng `/login`
- **AC-29-09** — Given dữ liệu chưa về · When render · Then **đúng một dòng** `M_22 読み込み中…`
- **AC-29-10** — Given `R-SEED-02` (`current_version=0`) · When mở màn · Then khối `D` hiện
  `このルートはまだ公開されていません。`, `C-2` ghi `第1版 として公開します`, `C-4` và `C-5`
  **không được render**
- **AC-29-12** — Given thiếu cặp `travel_times` · When mở màn · Then khối `B` không hiện số nào cho
  ①②④, hiện `M_83` nêu đích danh chặng thiếu, `C-7` tắt
- **AC-29-13** / **AC-29-14** — Given `start_time` NULL, hoặc không có bản luật hợp lệ · When mở màn ·
  Then khối `B` hiện `M_84`, `C-7` tắt — không bốn dòng `OK` giả
- **AC-29-17** — Given màn sẵn sàng · When bấm `C-7` · Then chữ **đổi** thành `M_06 処理中…`,
  nút vô hiệu hoá và nhận `aria-busy`

**Impact Range**
- `app/(app)/routes/publish/` · `MENU:47`

---

##### `[DEV TASK]` E03-FE-02 — Build diff block C-4 against the previous snapshot

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Đọc `route_versions.snapshot` của bản `version_no = current_version`, so với nội dung hiện tại
  theo `seq` và `deliveryPointCode`, hiện ba loại thay đổi: đổi điểm · thêm điểm · bớt điểm
- **Thuần trình duyệt, không cần cột mới** — `snapshot` của bản cũ lưu đủ để so
- **AC-29-29** — Given bản 1 có `CUS-001`, `CUS-002`, tuyến hiện tại đổi điểm hai sang `CUS-003` và
  thêm `CUS-005` · When mở màn · Then `C-4 第1版との差分` hiện **đúng hai** thay đổi:
  `CUS-002 → CUS-003` và `(追加) CUS-005`
- **AC-29-30** — Given `C-4` render · When xem thứ tự · Then nó nằm **trên** ô `C-5 変更理由` —
  người dùng thấy mình đổi gì trước khi viết lý do
- **AC-29-26** — Given `C-5` để trống · When bấm `C-7` · Then hiện `変更理由を入力してください`
  dưới ô, **không** phát sinh một lượt gọi API nào

**Impact Range**
- Khối `C-4`, `C-5` của SCR-29

---

##### `[DEV TASK]` E03-FE-03 — Build publish history block D

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- **AC-29-24** — Given công bố xong · When đọc khối `D` · Then dòng đó hiện đủ **năm cột**:
  `版` = `第1版` · `公開日時` theo JST · `ルール版` = `DRV-RULE-2026-v1` · `変更理由` = `―` ·
  `判定` = `OK`
- **AC-29-31** — Given đã công bố bản 2 · When đọc khối `D` · Then có **hai** dòng, sắp `版` giảm
  dần, dòng `第1版` có `変更理由` = `―`, dòng `第2版` có chữ người dùng nhập
- ⚠ Khối `D` chỉ phủ **một tuyến**. `過去バージョンは監査可能` ở nghĩa đầy đủ là tra xuyên tuyến,
  xuyên ngày — thuộc **SCR-41**, xem `E03-INV-02`

**Impact Range**
- Khối `D` của SCR-29

---

##### `[DEV TASK]` E03-FE-04 — Build violation panel B with disabled publish and replan exit

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E02-BE-03`

**Specification**
- Màn này **kiểm lại** từ CSDL (`R-14`) — gọi **cùng một** hàm `driver-hours.ts`, không viết lại
- **AC-29-32** — Given `R-SEED-02` (① 410/240 `超過` · ② 455/780 `OK` · ③ điểm dừng dài nhất 25
  phút `超過` · ④ 455 phút = 7h35 `OK`) · When mở màn · Then khối `B` hiện **đủ bốn dòng**,
  hai `超過` và hai `OK`
- **AC-29-33** — Given trạng thái trên · When xem nút · Then `C-7 公開する` **TẮT**,
  `B-9 ルート違反は公開禁止` hiện, **và** `B-11 再計画` hiện ra như lối thoát
- **AC-29-34** — Given ③ `超過` vì `CUS-007` chỉ 25 phút · When khối `B` render · Then `B-10` hiện
  thể của `M_79`: `サービスタイム 25分（CUS-007）は30分に満たないため、連続運転の計算はリセットされません`
  — nêu **đích danh** điểm dừng, không chỉ báo `超過`
- ⚠ **M-1:** trước khi **E04** xong, một tuyến đạt ngưỡng **nhờ điểm nghỉ** ở SCR-28 sẽ vi phạm lại
  tại đây. `PREMISE` §3 `V-1` chốt E04 lên trước

**Impact Range**
- Khối `B` của SCR-29 — item `B-8`…`B-11`, `C-7`

---

##### `[DEV TASK]` E03-FE-05 — Review 18 new Japanese strings with a native speaker

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `dùng chung` + `UI`

**Specification**
- Màn có **26 chuỗi có nguồn** (14 `[CODE]`, 9 `[RFP]`, 3 đã đăng ký); **18 chuỗi soạn mới** cần
  duyệt: 9 nhãn riêng của màn + 9 câu thông báo
- 9 câu thông báo **đã có mã**: năm mã riêng màn (`M_97`–`M_101`) và bốn **thể của khuôn dùng chung**
  (`M_61` · `M_64` · `M_80` · `M_86`)
- `[tự viết]` Given 18 chuỗi soạn mới · When người bản ngữ duyệt xong · Then mỗi chuỗi có trạng thái
  duyệt ghi lại, không chuỗi nào vào code khi chưa duyệt

**Impact Range**
- `_common/thong-bao-ja.md` bản `0.9.0` · mọi nhãn của SCR-29

---

#### `[INVESTIGATION]` E03-INV-01 — Confirm how drivers should be told a new version exists

**Overview**
- Hỏi khách: khi có bản mới, tài xế được báo bằng cách nào
- **Giả định vendor:** chỉ báo trên màn SCR-26, **không** làm thông báo đẩy (quyết định wireframe 8.4)
- **Mức đổi:** khách đòi thông báo đẩy → **Lớn**, phải dựng cả hạ tầng thông báo (mock **M7** cho
  thấy mảng này chưa làm gì cả)
- ⚠ Liên quan trực tiếp tới **ca nguy hiểm nhất** của màn — xem `E03-BE-08`

**References**
- SCR-29 §6.3 #4 · `AC-29-55` · `US-14 AC2`

---

#### `[INVESTIGATION]` E03-INV-02 — Confirm cross-route audit lookup is out of scope until SCR-41

**Overview**
- `FR-SCH-04` đòi `過去バージョンは監査可能` (*"phiên bản cũ có thể kiểm toán được"*)
- Dữ liệu **đã đủ**: mọi bản nằm trong `route_versions` append-only, 6 vai không phải tài xế đọc
  được qua PostgREST. Nhưng **không có màn nào** cho `監査者` — SCR-41 và SCR-39 đều `enabled: false`
- Khối `D` của SCR-29 chỉ phủ **một tuyến**; nghĩa đầy đủ là tra xuyên tuyến, xuyên ngày
- **Giả định vendor:** nghĩa đầy đủ thuộc **SCR-41, wave 3** — ngoài phạm vi LAB-5
- Ghi ở đây để **không coi khối `D` là đã đóng được yêu cầu**

**References**
- SCR-29 §6.3 #12 · `MENU:49, 51`

---

### E04 · Điểm nghỉ `休憩`

| | |
|---|---|
| **Màn** | SCR-28 #2 · SCR-29 #6 |
| **Nhóm LAB-1 đối chiếu** | F06 · `FT-06-04` — 8 SP / 5 MD |
| **Số item** | 1 epic + 1 story + 2 parent + 5 dev task + 1 investigation = **10** |

⚠ **M-1 đẩy epic này lên trước E03.** Chốt ở `PREMISE.md` §3 `V-1`: nếu không có chỗ lưu điểm
nghỉ, người dùng chèn nghỉ ở SCR-28 → bốn ngưỡng thành `OK` → nút công bố bật → sang SCR-29 →
màn đó tính lại từ CSDL, mà nghỉ **không được lưu** → vi phạm lại → nút công bố tắt. **Ngõ cụt.**

```
[EPIC] E04 Store and honour rest stops in route planning and publishing
└── [STORY] US-29 Dispatcher inserts rest stops that persist and reach the driver itinerary
    ├── [PARENT][BE] E04-BE Add rest-stop storage and carry it into the published snapshot
    │   ├── E04-BE-01 Add stop_type and break_minutes columns to route_stops
    │   ├── E04-BE-02 Extend snapshot stop items with stopType and breakMinutes
    │   └── E04-BE-03 Feed stored rest stops into the break-reset calculation
    └── [PARENT][FE] E04-FE Build rest-stop insertion on SCR-28
        ├── E04-FE-01 Add insert-break button on threshold row and break rows in table B
        └── E04-FE-02 Remove the unsaved-break warning once storage lands
[INVESTIGATION] E04-INV-01 Confirm rest-stop storage shape with the customer
```

---

#### `[EPIC]` E04 — Store and honour rest stops in route planning and publishing

**Overview & Goal**
- As a `配送計画者` (*"Điều phối giao hàng"*)
- I want chèn điểm nghỉ vào tuyến và **lưu được** chúng
- So that tuyến đạt ngưỡng nhờ nghỉ vẫn công bố được, và tài xế thấy nghỉ ở đâu, bao lâu

**Scope & Features**
- Chỗ lưu: hai cột trên `route_stops` (`PREMISE` §3 `V-2`)
- Dòng nghỉ vào được `snapshot.stops` mà **không phá** bản `R-SEED-01` (`PREMISE` §3 `V-6`)
- Dòng nghỉ tham gia phép tính ③ reset chuỗi lái

**Ngoài phạm vi**
- Phép tính ③ → **E02** (`E02-BE-06`); epic này chỉ cấp **nguồn dữ liệu** cho nó
- Giờ đến / giờ rời từng điểm — cùng nhóm nhưng spec chọn phương án (a) cho vòng đầu: hiện trên
  màn, chưa vào `snapshot`

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-28-50** đảo chiều — Given tuyến đã chèn điểm nghỉ · When bấm `D-1 下書き保存` rồi mở lại ·
  Then điểm nghỉ **vẫn còn** và bốn ngưỡng giữ nguyên kết quả (hôm nay: nghỉ biến mất, màn phải
  cảnh báo rõ)
- `[tự viết]` Given bản `R-SEED-01` đã nằm trong CSDL · When đọc `snapshot` sau khi thêm hai khoá ·
  Then vẫn hợp lệ, khoá thiếu hiểu theo mặc định

**References & Dependencies**
- Spec: SCR-28 §6.3 #2 · §6.4.7 · SCR-29 §6.3 #6 · `R-13` · `US-29 AC2` (`US:367`) · `DR-ROUTE-01`
- `PREMISE.md` §1 · §3 `V-1` `V-2` `V-6` · §2 `GĐ-L5-1`
- Estimate LAB-1: F06 / `FT-06-04` — 8 SP / 5 MD
- **Chặn E03** (M-1)

---

#### `[STORY]` US-29 — Dispatcher inserts rest stops that persist and reach the driver itinerary

**Overview**
- **Who:** `配送計画者`, và `ドライバー` ở đầu ra
- **What:** chèn điểm nghỉ đủ dài trước khi lái liên tục quá 4 giờ, và nghỉ đó được lưu
- **Why:** `FR-SCH-03` đòi *vị trí và thời lượng nghỉ hiện trên lịch trình tài xế và trong tính
  toán tuân thủ*; từ điển dữ liệu của khách liệt `break` là thành phần của Phiên bản tuyến

**Acceptance Criteria**
- **AC-28-47** — Given dòng ① đang `超過` · When khối `C` render · Then nút `C-10 休憩を挿入` hiện
  ra **ở đúng dòng ①**; Given dòng ① đang `OK` · Then nút **không** hiện
- **AC-28-48** — Given `R-SEED-02` · When chèn **một** điểm nghỉ 30 phút giữa `CUS-006` và
  `CUS-007` · Then chuỗi lái reset tại đó nhưng dòng ① **vẫn `超過`**: đoạn sau điểm nghỉ là
  `120 + 140 = 260分 > 240分`. **Một điểm nghỉ không đủ cho ca này** — tiêu chí phải fail nếu ai đó
  cài reset chạm tới cả chặng quay về
- **AC-28-49** — Given `R-SEED-02` đã chèn **hai** điểm nghỉ 30 phút (sau `CUS-006` và sau
  `CUS-007`) · When khối `C` render · Then ① chuyển sang **`OK`** và ③ chuyển sang **`OK`**;
  ② tăng thêm **60 phút** thành **515 phút** và vẫn **`OK`**
- **AC-28-50** đảo chiều — Given tuyến đã chèn điểm nghỉ · When lưu nháp rồi mở lại · Then điểm
  nghỉ **vẫn còn** (hôm nay: biến mất, và màn phải cảnh báo rõ là không lưu)

**References & Dependencies**
- Spec: SCR-28 §6.4.7 · `R-13` · `RFPJA:789` `:797`
- `PREMISE.md` §3 `V-2` `V-6`

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E04-BE — Add rest-stop storage and carry it into the published snapshot

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- `route_stops` chỉ có `seq`, `order_id`, `delivery_point_id` — bảng được dựng cho "điểm giao",
  không cho "điểm dừng nói chung"
- Yêu cầu tối thiểu lấy từ **US-29 AC2**: lưu được **vị trí trong chuỗi** và **thời lượng**, và cả
  hai phải vào được `snapshot` của `route_versions`
- Thứ tự: `E04-BE-01` → `E04-BE-02` → `E04-BE-03`

**Impact Range**
- `route_stops` · `route_versions.snapshot` · `driver-hours.ts`

---

##### `[DEV TASK]` E04-BE-01 — Add stop_type and break_minutes columns to route_stops

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` · **Sprint 2** (T4)

**Specification**
- Hai cột trên `route_stops`: `stop_type` (mặc định `'delivery'`) và `break_minutes` (`null` cho
  điểm giao) — **không** dựng bảng riêng
- Căn cứ chọn cột thay vì bảng riêng (`PREMISE` §3 `V-2`): `snapshot.stops` là **một mảng theo
  `seq`**; dòng nghỉ phải nằm đúng thứ tự giữa các điểm giao. Bảng riêng buộc `publish_route` trộn
  hai nguồn rồi sắp lại — thêm một chỗ sai mà không đổi lại được gì
- Dòng nghỉ có `delivery_point_id` và `order_id` đều `null` → phải nới ràng buộc hiện có cho hợp lệ
- `[tự viết]` Given một dòng nghỉ 30 phút chèn giữa `seq` 2 và 3 · When ghi · Then
  `unique(route_id, seq)` vẫn giữ, các dòng sau được đánh số lại liên tục

**Impact Range**
- `route_stops` · `set_route_stops` (`E01-BE-03`)

---

##### `[DEV TASK]` E04-BE-02 — Extend snapshot stop items with stopType and breakMinutes

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E03-BE-02`

**Specification**
- **Hình dạng `snapshot` đã bị `R-SEED-01` cố định** (`SEED5:42-52`) — thêm khoá phải có chủ ý và
  phải tương thích ngược với bản seed
- `PREMISE` §3 `V-6` chốt: giữ **đúng 6 khoá cấp trên**; thêm hai khoá vào **phần tử** của `stops`:
  `stopType` (mặc định `"delivery"`) và `breakMinutes` (`null` cho điểm giao)
- Vì sao không thêm ở cấp trên: bản seed sẽ thiếu khoá và **mọi chỗ đọc phải có nhánh phòng thủ**
- **AC-29-20** vẫn đúng — Given lần công bố · When đọc `snapshot` · Then vẫn **đúng sáu khoá cấp
  trên**
- `[tự viết]` Given bản `R-SEED-01` đã có trong CSDL · When đọc lại sau migration · Then phần tử cũ
  vẫn hợp lệ, `stopType` hiểu là `"delivery"`, `breakMinutes` hiểu là `null`

**Impact Range**
- `publish_route` · `route_versions.snapshot` · băng SCR-26

---

##### `[DEV TASK]` E04-BE-03 — Feed stored rest stops into the break-reset calculation

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E02-BE-06` · `E04-BE-01`

**Specification**
- Trước khi có cột, `R-13` cho dòng nghỉ **sống trong phiên** và tham gia phép tính ③. Sau khi có
  cột, nguồn dữ liệu đổi từ phiên sang CSDL — **phép tính ③ không đổi**, chỉ đổi chỗ đọc
- **AC-28-48** — Given `R-SEED-02` · When chèn **một** điểm nghỉ 30 phút giữa `CUS-006` và
  `CUS-007` · Then ① **vẫn `超過`** (`120 + 140 = 260分 > 240分`) — reset **không** được chạm tới
  chặng quay về
- **AC-28-49** — Given chèn **hai** điểm nghỉ 30 phút · When render · Then ① `OK`, ③ `OK`,
  ② tăng **60 phút** thành **515 phút** và vẫn `OK`
- Hệ quả M-1 được gỡ: SCR-29 tính lại từ CSDL sẽ ra **cùng** kết quả với SCR-28

**Impact Range**
- `lib/rules/driver-hours.ts` · `route_stops`

---

#### `[PARENT][FE]` E04-FE — Build rest-stop insertion on SCR-28

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `UI`

**Specification**
- Nút chèn nghỉ và dòng nghỉ trong bảng `B`; gỡ câu cảnh báo "không lưu" sau khi có chỗ lưu

**Impact Range**
- Khối `C` item `C-10` · bảng `B` của SCR-28 · nút `D-1`

---

##### `[DEV TASK]` E04-FE-01 — Add insert-break button on threshold row and break rows in table B

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E04-BE-01`

**Specification**
- **AC-28-47** — Given dòng ① đang `超過` · When khối `C` render · Then nút `C-10 休憩を挿入` hiện
  **ở đúng dòng ①**; Given ① đang `OK` · Then nút **không** hiện
- `[tự viết]` Given bấm `C-10` · When chọn vị trí và thời lượng · Then bảng `B` hiện một dòng nghỉ
  phân biệt rõ với điểm giao, có số phút, và bốn ngưỡng tính lại ngay (`AC-28-24`)

**Impact Range**
- `C-10` · bảng `B` của SCR-28

---

##### `[DEV TASK]` E04-FE-02 — Remove the unsaved-break warning once storage lands

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E04-BE-01`

**Specification**
- Trước khi có cột: `D-1 下書き保存` phải **cảnh báo rõ là điểm nghỉ không được lưu** (`R-13` cấm
  *"mất dữ liệu im lặng"*)
- Sau khi có cột: gỡ câu cảnh báo, vì nó trở thành sai
- **AC-28-50** đảo chiều — Given tuyến đã chèn nghỉ · When lưu nháp rồi mở lại · Then nghỉ **vẫn
  còn**, bốn ngưỡng giữ nguyên kết quả, **không** còn câu cảnh báo nào
- ⚠ Task này là chỗ **duy nhất** đóng vòng M-1 ở tầng giao diện — đừng đóng epic khi còn câu cảnh báo

**Impact Range**
- Nút `D-1` của SCR-28 · `_common/thong-bao-ja.md`

---

#### `[INVESTIGATION]` E04-INV-01 — Confirm rest-stop storage shape with the customer

**Overview**
- LAB-4 để ngỏ: *"một cột phân loại dòng trên `route_stops` cộng một cột thời lượng, **hoặc** một
  bảng riêng — **LAB-5 chọn và đặt tên, spec không tự đặt**"*
- **Giả định vendor (`GĐ-L5-1`):** hai cột trên `route_stops`
- **Mức đổi:** khách muốn bảng riêng → thêm một bảng + phép trộn hai nguồn khi dựng `snapshot`;
  SP của `E04-BE-01` và `E04-BE-02` **đều tăng**
- Không chặn thi công — làm theo giả định, đóng khi khách trả lời

**References**
- SCR-28 §6.3 #2 · `PREMISE.md` §2 `GĐ-L5-1` · §3 `V-2`

---

### E05 · Ngưỡng giờ lái cộng dồn nhiều ngày

| | |
|---|---|
| **Màn** | SCR-28 §6.2.2 · 6.3 #5 |
| **Nhóm LAB-1 đối chiếu** | F06 — **LAB-1 chưa tách**, không có mã `FT` riêng |
| **Số item** | 1 epic + 0 story + 2 parent + 4 dev task + 1 investigation = **8** |

⚠ **Epic này không có story.** Nó là **nhánh cộng dồn** của `US-13`, mà `US-13` đã thuộc E02 — một
US không nằm ở hai epic. Dev task treo thẳng dưới hai parent. Xem câu hỏi ở cuối §2.

⚠ **Không ước được công chắc chắn** cho tới khi có đáp án Q13. Vẫn ước theo giả định của LAB-1 để
`estimate.md` có số, kèm mức đổi **Vừa → Lớn** ghi rõ.

```
[EPIC] E05 Enforce multi-day cumulative driver-hour thresholds
├── [PARENT][BE] E05-BE Build the worked-hours source and the two average thresholds
│   ├── E05-BE-01 Build a worked-hours source for a driver's previous days
│   ├── E05-BE-02 Enforce the 9h/day average over 2 consecutive days
│   └── E05-BE-03 Enforce the 44h/week average over 2 consecutive weeks
└── [PARENT][FE] E05-FE Build opening-balance entry for go-live
    └── E05-FE-01 Build manual opening-balance entry screen for driver worked hours
[INVESTIGATION] E05-INV-01 Confirm Q13 — where previous days' worked hours come from
```

---

#### `[EPIC]` E05 — Enforce multi-day cumulative driver-hour thresholds

**Overview & Goal**
- As a `配送計画者` (*"Điều phối giao hàng"*)
- I want hệ cảnh báo cả hai ngưỡng **bình quân nhiều ngày** của luật 2024
- So that tuyến hợp lệ trong một ngày không âm thầm làm tài xế vượt trần của hai ngày hay hai tuần

**Scope & Features**
- Hai ngưỡng: lái bình quân **9h/ngày qua 2 ngày** · **44h/tuần qua 2 tuần**
- Nguồn **giờ đã làm của những ngày trước** — hôm nay **không bảng nào ghi**
- Màn nhập số dư đầu kỳ lúc go-live

**Ngoài phạm vi**
- Sáu ngưỡng chỉ thiếu cột → **E02** (`E02-BE-02`). Ranh giới này là **chỗ phân chia chi phí quan
  trọng nhất của cả bài**: thiếu cột thì ước được, thiếu nguồn dữ liệu thì không

**Acceptance Criteria**
- Toàn bộ dev task con đã đóng
- `[tự viết]` Given một tài xế đã lái 10h ngày hôm trước · When dựng tuyến 9h cho hôm nay ·
  Then hệ cảnh báo vượt bình quân 9h/ngày qua 2 ngày, nêu rõ hai ngày nào

**References & Dependencies**
- Spec: SCR-28 §6.2.2 ngưỡng #8 #9 · §6.3 #5
- `PREMISE.md` §2 `GĐ-L5-2` · **Q13 chưa có đáp án**
- LAB-1: mức đổi **Vừa → Lớn**, phải bật `FT-06-07` và một màn nhập số dư
- **Không chặn epic nào** — phần kiểm trong một ngày (E02) đủ căn cứ làm trước

---

#### `[PARENT][BE]` E05-BE — Build the worked-hours source and the two average thresholds

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- ⚠ **Chặn bởi Q13.** Hai ngưỡng này thiếu **nguồn dữ liệu**, không phải thiếu cột — khác hẳn
  `E02-BE-02`
- Làm theo `GĐ-L5-2`: tính từ tuyến và sự kiện tài xế trong hệ thống; số dư đầu kỳ nhập tay lúc
  go-live

**Impact Range**
- Bảng mới cho giờ đã làm · `driver_rule_versions` · `driver-hours.ts`

---

##### `[DEV TASK]` E05-BE-01 — Build a worked-hours source for a driver's previous days

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- Hôm nay **không có bảng nào ghi giờ làm thực tế của tài xế**. Phạm vi v6 dừng ở "một tuyến một ngày"
- Theo `GĐ-L5-2`: cộng dồn từ `routes` đã công bố + sự kiện tài xế, cộng số dư đầu kỳ nhập tay
- `[tự viết]` Given tài xế `DRV-02` có hai tuyến đã công bố trong 7 ngày qua · When tra giờ đã làm ·
  Then ra tổng đúng theo `拘束時間` của từng tuyến, không đếm trùng
- ⚠ Ước công theo giả định; đáp án Q13 khác → **Lớn**

**Impact Range**
- Bảng mới · `routes` · `route_versions.snapshot`

---

##### `[DEV TASK]` E05-BE-02 — Enforce the 9h/day average over 2 consecutive days

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E05-BE-01`

**Specification**
- Thêm cột ngưỡng vào `driver_rule_versions` (bảng **append-only** — xem bẫy ở `E02-BE-02`)
- `[tự viết]` Given tài xế lái 10h hôm trước và tuyến hôm nay 9h · When kiểm · Then bình quân 9,5h
  > 9h → báo vượt, nêu đích danh hai ngày
- `[tự viết]` Given bình quân đúng 9h · When kiểm · Then `OK` — biên phải chốt `>` hay `>=` trước
  khi code (spec **chưa nói**, khác với bốn ngưỡng trong ngày đã nói rõ)

**Impact Range**
- `driver_rule_versions` · `driver-hours.ts`

---

##### `[DEV TASK]` E05-BE-03 — Enforce the 44h/week average over 2 consecutive weeks

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E05-BE-01`

**Specification**
- Như trên, mốc là **tuần**. Phải chốt tuần bắt đầu thứ mấy theo JST — spec **chưa nói**
- `[tự viết]` Given hai tuần liền có tổng 90h · When kiểm · Then bình quân 45h > 44h → báo vượt,
  nêu đích danh hai tuần

**Impact Range**
- `driver_rule_versions` · `driver-hours.ts`

---

#### `[PARENT][FE]` E05-FE — Build opening-balance entry for go-live

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Specification**
- Màn nhập số dư đầu kỳ — LAB-1 ghi đây là phần phải bật thêm khi đáp án Q13 khác giả định

**Impact Range**
- Màn mới, chưa có mã SCR

---

##### `[DEV TASK]` E05-FE-01 — Build manual opening-balance entry screen for driver worked hours

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E05-BE-01`

**Specification**
- Nhập tay giờ đã làm của từng tài xế tại thời điểm go-live, để hai ngưỡng bình quân có số để cộng
- `[tự viết]` Given go-live ngày `D` · When nhập số dư cho `DRV-01` · Then phép kiểm của ngày `D+1`
  cộng đúng số dư đó
- ⚠ Màn này **chỉ tồn tại** nếu giả định `GĐ-L5-2` đúng. Đáp án Q13 khác → màn khác hoặc không cần

**Impact Range**
- Màn mới · bảng giờ đã làm

---

#### `[INVESTIGATION]` E05-INV-01 — Confirm Q13: where previous days' worked hours come from

**Overview**
- Hỏi khách: giới hạn theo tháng / năm / 2 ngày / 2 tuần lấy giờ đã làm từ đâu
- **Giả định vendor (`GĐ-L5-2`):** tính từ tuyến và sự kiện tài xế trong hệ thống; số dư đầu kỳ
  nhập tay lúc go-live. Đây là giả định **của chính LAB-1**, dùng lại để ước công cho nhất quán
- **Mức đổi:** **Vừa → Lớn** — phải bật `FT-06-07` và một màn nhập số dư
- ⚠ Đây là câu **duy nhất** chặn ước công trong cả module lập lịch. Bảy điểm chờ khách còn lại đều
  ước được theo giả định

**References**
- SCR-28 §6.3 #5 · `QA:27` · `PREMISE.md` §2 `GĐ-L5-2`

---

### E06 · Nhập kho & kiểm hàng

| | |
|---|---|
| **Màn** | SCR-12 |
| **Dòng 6.3 hút vào** | #1…#15 (15 dòng) |
| **Nhóm LAB-1 đối chiếu** | F02 — 91 SP / 49 MD |
| **Số item** | 1 epic + 3 story + 6 parent + 11 dev task + 4 investigation = **25** |

⚠ **Màn này đã code.** Khác SCR-28/29, 6.3 ở đây là **bịt chỗ hở**, không phải dựng mới.

⚠ **`US-02` không có story riêng** — tạo lô bất biến **đã chạy đủ** (`AC-12-15`, `AC-12-19`);
6.3 không có dòng nào đòi sửa nó. Chỉ `E06-01-BE-04` (unique cho `photo_path`) chạm tới nó.

⚠ **`FT-02-03` ⟷ `US-23`:** LAB-1 **vẫn tính công** cho `FT-02-03` (FR-REC-03) mà LAB-2 đã cắt
khỏi v6. LAB-5 đưa việc đó trở lại qua `US-23`. Bảng đối chiếu ở `estimate.md` §5 phải nói rõ
điều này, nếu không chênh lệch sẽ đọc sai thành "LAB-5 phình việc".

```
[EPIC] E06 Harden goods receiving and lot creation on SCR-12
├── [STORY] US-01 Receiving clerk records one inspected line at a time
│   ├── [PARENT][BE] E06-01-BE Close the validation gaps between zod, RPC and the columns
│   │   ├── E06-01-BE-01 Enforce the three upper bounds that only zod checks today
│   │   ├── E06-01-BE-02 Reject beef cattle ids on non-beef trace lanes
│   │   ├── E06-01-BE-03 Make supplier lot number and production date nullable if Q51 says so
│   │   └── E06-01-BE-04 Add unique index on receiving_lines.photo_path
│   └── [PARENT][FE] E06-01-FE Make the receiving form survive a 50-line shift
│       ├── E06-01-FE-01 Build the per-session list of recorded lines
│       └── E06-01-FE-02 Split the 5xx message from the 422 input-error message
├── [STORY] US-03 Failed checks move goods into quarantine with a deviation
│   ├── [PARENT][BE] E06-03-BE Settle the quarantine rules the RFP contradicts itself on
│   │   ├── E06-03-BE-01 Implement the Q52 answer for out-of-range temperature
│   │   ├── E06-03-BE-02 Give packaging NG its own lot status once 保留 exists
│   │   └── E06-03-BE-03 Assign severity to deviations opened from receiving
│   └── [PARENT][FE] E06-03-FE Adjust the quarantine result panel to the settled rules
│       └── E06-03-FE-01 Re-render quarantine reasons and severity per the settled rules
└── [STORY] US-23 Receiving clerk records accepted/rejected/pending quantities with reason codes
    ├── [PARENT][BE] E06-23-BE Add the three quantity columns, reason codes and the approval flow
    │   ├── E06-23-BE-01 Add accepted/rejected/pending quantity columns to receiving_lines
    │   └── E06-23-BE-02 Add reason code master and the variance approval flow
    └── [PARENT][FE] E06-23-FE Build the quantity split and reason code input
        └── E06-23-FE-01 Build the quantity split block with reason code selection
[INVESTIGATION] E06-INV-01 Confirm Q52 — block on temperature deviation or receive into quarantine
[INVESTIGATION] E06-INV-02 Confirm Q51 — are supplier lot number and production date mandatory
[INVESTIGATION] E06-INV-03 Confirm Q53 — does lot_status need the 保留 value
[INVESTIGATION] E06-INV-04 Confirm Q2 — which reason code catalogue to use
```

---

#### `[EPIC]` E06 — Harden goods receiving and lot creation on SCR-12

**Overview & Goal**
- As an `入荷担当者` (*"Nhân viên nhập hàng"*)
- I want ghi từng dòng hàng nhập, hệ tự tạo lô bất biến và tự đẩy hàng lỗi vào cách ly
- So that mọi lô trong kho đều có bằng chứng nhập và không lô lỗi nào lọt vào hàng bán được

**Scope & Features**
- Bịt ba chỗ zod chặt hơn RPC — gọi thẳng API là lọt cả ba
- Chốt bốn câu khách còn treo quanh luật cách ly (Q51 · Q52 · Q53 · câu hỏi mở 9)
- Trả lại `US-23` (FR-REC-03) đã bị cắt khỏi v6: ba cột số lượng + mã lý do + luồng duyệt chênh
- Danh sách dòng đã nhập trong phiên — người nhập làm 20–50 dòng một chuyến xe

**Ngoài phạm vi**
- Đổi trạng thái lô sau khi nhập → **E07** (SCR-19)
- Hồ sơ sai lệch → **E10** (SCR-33); SCR-12 chỉ là **nơi sinh ra** Sai lệch
- Dọn ảnh mồ côi · quyền đọc ảnh theo tiền tố · dữ liệu thừa ở `lookups` — ba dòng `không code`,
  xem `E12-INV`

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-12-41** vẫn đúng sau mọi thay đổi — Given bất kỳ ca 422/409/403 nào · When kiểm DB ·
  Then **không** dòng mới ở `receiving_lines`, `lots`, `lot_state`, `inventory_balances`,
  `lot_status_history`, `deviations`, `events`
- **AC-12-19** vẫn đúng — Given một lô đã tạo · When thử `UPDATE`/`DELETE` · Then trigger
  append-only chặn

**References & Dependencies**
- Spec: `scr-12-nhap-kiem-hang.md` §6.3 #1…#15 · §6.4.1…§6.4.9
- Estimate LAB-1: F02 — 91 SP / 49 MD, **gồm cả `FT-02-03`**

---

#### `[STORY]` US-01 — Receiving clerk records one inspected line at a time

**Overview**
- **Who:** `入荷担当者`
- **What:** nhập 12 field của một dòng hàng, đính ảnh, bấm ghi nhận; làm liên tục 20–50 dòng
- **Why:** FR-REC-02 (P0) — mỗi dòng là một bằng chứng kiểm hàng

**Acceptance Criteria**
- **AC-12-13** — Given SKU `trace_lane='none'`, nhiệt trong dải, vị trí cùng `temp_zone`,
  `梱包状態 = OK` · When bấm `入荷を登録` với 12 field hợp lệ và ảnh đã đính · Then API trả 2xx
- **AC-12-17** — Given gửi thành công · When form render lại · Then mọi ô về rỗng, ảnh bị bỏ,
  `clientRequestId` là GUID **mới**
- **AC-12-20** — Given form thiếu nhiều trường bắt buộc · When bấm gửi · Then **không** phát sinh
  request nào, **và** mọi ô thiếu hiện câu riêng của nó **cùng lúc**
- **AC-12-21** — Given `数量 = 0` · When gửi · Then ô `数量` hiện `数量は1以上で入力してください`
- **AC-12-21b** — Given `仕入先ロット番号` dài hơn 100 ký tự · When gửi · Then ô đó hiện câu riêng
- **AC-12-22** — Given `製造日` sau `有効期限` · When gửi · Then câu hiện **dưới ô `製造日`**
- **AC-12-23** — Given SKU `expiry_type='use_by'` · When chọn SKU · Then ô `期限タイプ` hiện gợi ý
  `SKUマスター: 消費期限` — gợi ý, **không khoá**
- **AC-12-50** — Given chưa gửi dòng nào trong lần mở trang này · When nhìn khối `登録済み一覧` ·
  Then hiện `M_07 データがありません`
- **AC-12-51** — Given đã gửi thành công ba dòng · When nhìn khối đó · Then có **ba** hàng, mỗi
  hàng đủ `ロット番号` · `状態` · `登録時刻`
- **AC-12-52** — Given đã gửi vài dòng · When rời trang rồi quay lại · Then khối **trống trở lại**
  — danh sách chỉ sống trong một lần mở trang, **không** gọi thêm API nào để dựng
- **AC-12-53** — Given lỗi máy chủ (HTTP ≥ 500) · When màn hiện thông báo · Then câu là
  `システムエラーが発生しました。時間をおいて再度お試しください`, **không** phải câu lỗi nhập liệu

**References & Dependencies**
- Spec: SCR-12 §6.4.3 · §6.4.4 · §6.4.8 · §6.3 #2 #6 #9 #10 #13

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E06-01-BE — Close the validation gaps between zod, RPC and the columns

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `RPC / luật` + `DB (migration)`

**Specification**
- Ba luật chỉ sống ở zod, RPC không kiểm lại → gọi thẳng API hoặc thẳng RPC là **lọt cả ba**
- Cộng hai chỗ hở khác: kiểm làn truy xuất, và thiếu unique cho `photo_path`

**Impact Range**
- `receive_line` · `receiving_lines` · `lots`

---

##### `[DEV TASK]` E06-01-BE-01 — Enforce the three upper bounds that only zod checks today

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- zod chặt hơn RPC ở **ba chỗ**: `quantity ≤ 1.000.000` · `実測温度 −60…60` ·
  `仕入先ロット番号 ≤ 100`. RPC chỉ kiểm `quantity <= 0`; `measured_temp_c` chỉ bị chặn bởi kiểu
  `numeric(5,2)`; độ dài lô **không kiểm**
- Thêm check ở RPC hoặc check constraint ở cột
- `qty > 2^31` cho Postgres `22003` → **500, không ghi bằng chứng** — phải chặn trước khi tới đó
- `[tự viết]` Given gọi thẳng RPC với `quantity = 2_000_000` · When gọi · Then **422** có mã riêng,
  không phải 500
- `[tự viết]` Given `measured_temp_c = 999` gửi thẳng API · When gọi · Then 422, không phải lỗi kiểu

**Impact Range**
- `receive_line` · check constraint trên `receiving_lines`

---

##### `[DEV TASK]` E06-01-BE-02 — Reject beef cattle ids on non-beef trace lanes

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `牛個体識別番号` trên SKU **không phải** làn beef: UI không gửi, nhưng **RPC nhận, kiểm định dạng
  và LƯU** nếu có
- Client khác (hoặc gọi thẳng API) **gắn được mã bò vào lô gạo**
- Thêm kiểm `trace_lane` ở RPC, **hoặc** tuyên bố là cố ý cho phép (phải ghi thành văn bản)
- `[tự viết]` Given SKU `trace_lane='rice'` và thân có `牛個体識別番号` hợp lệ · When gọi thẳng RPC ·
  Then 422, **và** không lô nào được tạo
- **AC-12-35** vẫn đúng — Given mã bò sai định dạng trên SKU làn beef · When gửi · Then **422**
  `VALIDATION_BEEF_ID_FORMAT`, **không** lô nào được tạo — khác hẳn ca để trống (`AC-12-27`)

**Impact Range**
- `receive_line` · `lots.cattle_id`

---

##### `[DEV TASK]` E06-01-BE-03 — Make supplier lot number and production date nullable if Q51 says so

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `DB (migration)` · **Phụ thuộc:** `E06-INV-02`

**Specification**
- Hôm nay bắt buộc cả hai ở **ba tầng**: zod, RPC, và `not null` ở cột
- Danh sách P0 của FR-REC-02 **không có** hai field này; từ điển dữ liệu Lot lại bắt buộc cả hai
- ⚠ **Chờ Q51.** Nếu khách trả lời "không chặn": bỏ khỏi zod + RPC, **và đổi cột thành nullable**
  → là **migration**, không phải sửa form. Q51 ghi mức **Nhỏ** nhưng **chạm cột DB**
- `[tự viết]` Given Q51 trả lời "không chặn" · When gửi dòng thiếu hai field · Then 2xx, lô tạo
  được, hai cột mang `null`

**Impact Range**
- `lots` (2 cột) · `receive_line` · schema zod

---

##### `[DEV TASK]` E06-01-BE-04 — Add unique index on receiving_lines.photo_path

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)`

**Specification**
- `VALIDATION_PHOTO_ALREADY_USED` kiểm bằng `exists(...)`, mà `receiving_lines.photo_path`
  **không có unique constraint/index nào** trong migration — chỉ có FK tới `photo_uploads.path`
- Hai request song song cùng một ảnh **có thể cùng qua** → hai dòng nhập dùng chung một bằng chứng
- ⚠ **Chưa chạy thật để xác nhận** — là suy từ mã
- **AC-12-39** vẫn đúng — Given `photoPath` đã gắn với dòng trước · When gửi lại · Then **422**
  `VALIDATION_PHOTO_ALREADY_USED`
- `[tự viết]` Given hai request song song cùng một `photoPath` · When cả hai chạy · Then **đúng một**
  thành công

**Impact Range**
- `receiving_lines.photo_path` · `receive_line`

---

#### `[PARENT][FE]` E06-01-FE — Make the receiving form survive a 50-line shift

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Hai chỗ người nhập đang chịu thiệt: không tự kiểm được đã nhập dòng nào, và bị dẫn đi sửa dữ
  liệu vốn không sai khi gặp lỗi hệ thống

**Impact Range**
- Form SCR-12 · `FORM:88`

---

##### `[DEV TASK]` E06-01-FE-01 — Build the per-session list of recorded lines

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Code chỉ giữ panel của **dòng cuối cùng**; nhập dòng tiếp là panel cũ bị thay. Người nhập làm
  liên tục 20–50 dòng một chuyến xe **không có cách nào tự kiểm** "tôi đã nhập dòng đó chưa"
- **Spec đã định nghĩa xong giao diện và nhãn** (S20): bảng 3 cột `登録済み一覧` —
  `ロット番号` · `状態` · `登録時刻`. LAB-5 **chỉ việc dựng, không phải quyết lại**
- Dữ liệu đã có sẵn ở trình duyệt → **không tốn thêm lượt gọi API**
- **AC-12-50** — Given chưa gửi dòng nào · Then hiện `M_07 データがありません`
- **AC-12-51** — Given đã gửi ba dòng · Then ba hàng đủ ba cột
- **AC-12-52** — Given rời trang rồi quay lại · Then khối **trống trở lại**

**Impact Range**
- Khối `登録済み一覧` của SCR-12

---

##### `[DEV TASK]` E06-01-FE-02 — Split the 5xx message from the 422 input-error message

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Màn không phân biệt **500 lỗi hệ thống** với **422 lỗi nhập liệu**: cả hai hiện cùng câu
  `登録できませんでした。入力内容を確認してください`, khiến người dùng **đi sửa dữ liệu vốn không sai**
- 9/14 mã dùng chung một câu, trong đó có `internal_error`
- **Spec đã định nghĩa câu riêng cho nhóm 5xx** (S16, mục 4.2.3) → thêm một nhánh trong `FORM:88`
  theo `response.status >= 500`
- **AC-12-53** — Given HTTP ≥ 500 · When màn hiện thông báo · Then câu là
  `システムエラーが発生しました。時間をおいて再度お試しください`
- 8 câu `[JA-NEW]` ở `_common/thong-bao-ja.md` cần người bản ngữ duyệt

**Impact Range**
- `FORM:88` · `_common/thong-bao-ja.md`

---

#### `[STORY]` US-03 — Failed checks move goods into quarantine with a deviation

**Overview**
- **Who:** `入荷担当者` ghi, `品質管理` (*"Quản lý chất lượng"*) xử lý tiếp
- **What:** hàng lỗi vào trạng thái Cách ly và tự mở một hồ sơ Sai lệch
- **Why:** FR-REC-05 (P0) — hàng không đạt không được lẫn vào hàng bán được

**Acceptance Criteria**
- **AC-12-24** — Given SKU dải `冷蔵` (ngưỡng `0…5℃`) và nhiệt đo `5.01` · When gửi · Then **201**,
  badge `隔離`, `隔離理由` có câu `実測温度がSKUの温度帯の基準外`
- **AC-12-25** — Given đúng dữ liệu đó nhưng nhiệt đo `5.00` · When gửi · Then **201** badge
  `利用可能` — biên nằm **trong** dải
- **AC-12-26** — Given SKU `temp_zone='chilled'` và vị trí `temp_zone='ambient'` · When gửi ·
  Then `隔離理由` có `保管場所の温度帯がSKUと不一致`
- **AC-12-27** — Given SKU `trace_lane='beef'` và ô mã bò để trống · When gửi · Then **201**,
  `隔離理由` có `牛個体識別番号が未入力`, **và lô vẫn vào kho**
- **AC-12-28** — Given SKU `trace_lane='rice'` và ô `米産地` để trống · Then `隔離理由` có
  `米産地が未入力`
- **AC-12-29** — Given `梱包状態 = NG（破損・汚損あり）` · Then `隔離理由` có `梱包状態NG`
- **AC-12-30** — Given hai điều kiện Cách ly cùng đúng · When gửi · Then `隔離理由` liệt **cả hai**
  câu, mỗi câu một mục danh sách
- **AC-12-31** — Given một lô bị Cách ly · When kiểm DB · Then `lot_state.status='quarantined'`,
  `receiving_lines.result='quarantined'`, `lot_status_history.reason` bắt đầu bằng `入荷時隔離: `,
  **và** đúng một dòng `deviations` `source='receiving'`
- **AC-12-32** — Given Sai lệch vừa mở · When đọc `deviations.summary_ja` · Then chuỗi chứa đủ
  **bốn vế**: người ghi · thời điểm JST · vị trí · giá trị đo
- **AC-12-33** — Given Sai lệch mở từ màn này · When đọc `severity` · Then **NULL** — hiện trạng
- **AC-12-34** — Given panel Cách ly và `deviationCode` NULL · Then dòng `逸脱番号` hiện `-`

**References & Dependencies**
- Spec: SCR-12 §6.4.5 · §6.3 #1 #3 #5 #8 #11

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E06-03-BE — Settle the quarantine rules the RFP contradicts itself on

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `RPC / luật` + `DB (migration)`

**Specification**
- Ba dòng 6.3 (#1 #3 #5, cộng #11 trùng) đều quay về **một gốc**: FR-REC-03 bị cắt khỏi v6 và
  Q53 bỏ `保留` → không còn chỗ nào thể hiện NG. **Xử một lần, ba mục cùng đóng**
- Cả ba **chặn bởi câu trả lời của khách** — xem `E06-INV-01` `E06-INV-03` `E06-INV-05`

**Impact Range**
- `receive_line` · `lot_status` enum · `lot_status_transitions` · `deviations.severity`

---

##### `[DEV TASK]` E06-03-BE-01 — Implement the Q52 answer for out-of-range temperature

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E06-INV-01`

**Specification**
- **Hai điều trái nhau trong chính RFP:** BR-TEMP-02 nói lệch dải nhiệt *"luôn chặn xác nhận, không
  có ngoại lệ"*; FR-REC-05 nói kiểm nhiệt thất bại thì *"chuyển hàng vào cách ly"*
- Code hôm nay làm theo FR-REC-05: **nhận vào Cách ly + mở Sai lệch**
- **Giả định để ước công:** *"Nhận vào cách ly (bao trùm cả hai)"*, mức **Vừa**
- Khách chọn "chặn" → **bỏ phần tạo lô cách ly lúc nhập**, `AC-12-24` đảo chiều thành 422
- ⚠ Còn một **câu hỏi phụ chưa ai trả lời**: nếu chọn "chặn" thì FR-REC-05 *"chuyển hàng vào cách
  ly"* áp vào lúc nào?

**Impact Range**
- `receive_line` · `lot_state` · `deviations`

---

##### `[DEV TASK]` E06-03-BE-02 — Give packaging NG its own lot status once 保留 exists

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E06-INV-03`

**Specification**
- Hàng `梱包状態 NG` hôm nay vào thẳng `quarantined`, **chung một trạng thái với hàng lệch nhiệt**
- FR-REC-05 **chỉ liệt** Kiểm nhiệt độ và Truy xuất thất bại làm điều kiện cách ly, **không** có
  Tình trạng đóng gói
- Gốc vướng mắc: FR-REC-03 bị cắt + Q53 bỏ `保留` → không còn chỗ nào thể hiện NG
- Hai phương án đã soạn sẵn cho khách: **(a)** giữ như nay · **(b)** chỉ ghi cờ NG, lô vẫn dùng được
- Khách xác nhận cần `保留` → thêm giá trị enum + **2 dòng** `lot_status_transitions` + màn chuyển
  trạng thái (màn đó thuộc **E07**)
- **AC-12-29** đổi theo phương án được chọn

**Impact Range**
- `lot_status` enum · `lot_status_transitions` · `receive_line` · SCR-19 (E07)

---

##### `[DEV TASK]` E06-03-BE-03 — Assign severity to deviations opened from receiving

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E10-INV-01` (Q19 — một câu dùng chung)

**Specification**
- `deviations.severity` để **NULL** cho mọi Sai lệch nguồn `receiving`; cột dùng lại enum
  `alarm_severity` nên chỉ có **2 mức**, trong khi giả định ước công là **3 mức**
- SCR-12 là **nơi sinh ra** Sai lệch không mức — ảnh hưởng nặng hơn ở **SCR-33** (E10)
- **AC-12-33** đảo chiều — Given Sai lệch mở từ màn này · When đọc `severity` · Then có giá trị,
  không còn NULL
- ⚠ Q19 cảnh báo: *"Mỗi mức có luồng duyệt khác nhau → thêm workflow"*. **Vào bảng rủi ro của bài nộp**

**Impact Range**
- `deviations.severity` · enum `alarm_severity` · `receive_line` · SCR-33 (E10)

---

#### `[PARENT][FE]` E06-03-FE — Adjust the quarantine result panel to the settled rules

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Specification**
- Panel kết quả hôm nay đã chạy đúng (`AC-12-24`…`AC-12-34`). Việc của epic này là **sửa theo
  đáp án khách**, nên task con là **có điều kiện** — chỉ chạy sau khi ba investigation đóng

**Impact Range**
- Panel kết quả của SCR-12

---

##### `[DEV TASK]` E06-03-FE-01 — Re-render quarantine reasons and severity per the settled rules

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E06-03-BE-01` · `E06-03-BE-02` · `E06-03-BE-03`

**Specification**
- Sửa panel theo đáp án Q52 / câu hỏi mở 9 / Q19:
  - Q52 = "chặn" → ca `AC-12-24` không còn panel Cách ly, thành lỗi 422 tô ô nhiệt độ
  - `保留` được thêm → badge thứ ba, khác `隔離`
  - Severity có giá trị → hiện mức trên panel, `AC-12-34` thêm một dòng
- **AC-12-30** giữ nguyên — Given hai điều kiện Cách ly cùng đúng · Then liệt **cả hai** câu
- `[tự viết]` Given đáp án khách đã chốt · When panel render · Then mỗi lý do cách ly khớp đúng một
  câu đã đăng ký, không câu nào mồ côi

**Impact Range**
- Panel kết quả · `_common/thong-bao-ja.md`

---

#### `[STORY]` US-23 — Receiving clerk records accepted/rejected/pending quantities with reason codes

**Overview**
- **Who:** `入荷担当者`, và người đủ quyền duyệt phần chênh
- **What:** mỗi dòng ghi **số lượng nhận / từ chối / chờ xử lý kèm mã lý do**; tổng các dòng khớp
  số báo, không khớp thì cần duyệt
- **Why:** FR-REC-03 (P1) — **đã bị cắt khỏi v6**, LAB-5 đưa trở lại

**Acceptance Criteria**
- `[tự viết]` Given một dòng nhập 100 thùng, nhận 90 từ chối 10 kèm mã lý do · When ghi ·
  Then ba cột số lượng mang đúng ba giá trị, tổng bằng 100
- `[tự viết]` Given tổng các dòng **không khớp** số báo · When ghi · Then dòng vào trạng thái chờ
  duyệt, và chỉ người đủ quyền mới duyệt được phần chênh
- `[tự viết]` Given mã lý do chọn từ danh mục · When ghi · Then mã lưu vào cột riêng, không phải
  chuỗi tự do
- **AC-12-15** đổi — Given một lần gửi thành công · When kiểm `receiving_lines` · Then ngoài
  `result` còn có ba cột số lượng và cột mã lý do

**References & Dependencies**
- Spec: SCR-12 §6.3 #4 · FR-REC-03 (tr.16) · **Q2 chưa trả lời** (danh mục mã lý do)
- ⚠ LAB-1 đã tính công cho `FT-02-03` — xem ghi chú đầu epic

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E06-23-BE — Add the three quantity columns, reason codes and the approval flow

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- `receiving_lines` hôm nay chỉ có **một** cột `quantity` và một cột `result` hai giá trị. Không có
  cột mã lý do, không có luồng duyệt chênh lệch
- **Là thêm bảng và thêm cột, không phải sửa màn**

**Impact Range**
- `receiving_lines` · bảng mã lý do mới · `receive_line`

---

##### `[DEV TASK]` E06-23-BE-01 — Add accepted/rejected/pending quantity columns to receiving_lines

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)`

**Specification**
- Ba cột số lượng thay cho một cột `quantity`. `receiving_lines` là bảng **append-only** → dòng cũ
  phải nhận giá trị mặc định có chủ ý (cùng bẫy với `E02-BE-02`)
- `[tự viết]` Given dòng nhập cũ chỉ có `quantity` · When migration chạy · Then `accepted` = giá
  trị cũ, `rejected` = 0, `pending` = 0, và lý do chọn mặc định này ghi trong file migration

**Impact Range**
- `receiving_lines` · `inventory_balances`

---

##### `[DEV TASK]` E06-23-BE-02 — Add reason code master and the variance approval flow

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E06-INV-04`

**Specification**
- Bảng danh mục mã lý do + cột mã lý do trên `receiving_lines`
- Luồng duyệt phần chênh: tổng các dòng không khớp số báo → cần người đủ quyền duyệt
- ⚠ **Q2 chưa trả lời**: *"danh mục mã lý do nào"*. Giả định vendor: **cấu hình được**
- `[tự viết]` Given tổng dòng lệch số báo · When ghi · Then trạng thái chờ duyệt; vai không đủ
  quyền gọi duyệt → 403

**Impact Range**
- Bảng mã lý do mới · `receiving_lines` · `receive_line` · RLS

---

#### `[PARENT][FE]` E06-23-FE — Build the quantity split and reason code input

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Specification**
- Khối nhập ba số lượng + chọn mã lý do trên form SCR-12

**Impact Range**
- Form SCR-12

---

##### `[DEV TASK]` E06-23-FE-01 — Build the quantity split block with reason code selection

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E06-23-BE-01` · `E06-23-BE-02`

**Specification**
- Ba ô số lượng thay ô `数量` hiện tại, cộng ô chọn mã lý do hiện khi `rejected > 0` hoặc
  `pending > 0`
- `[tự viết]` Given nhập `rejected = 10` mà chưa chọn mã lý do · When bấm gửi · Then **không** phát
  sinh request, ô mã lý do hiện câu bắt buộc (cùng lối `AC-12-20`)
- **AC-12-21** mở rộng — Given tổng ba ô = 0 · When gửi · Then câu `数量は1以上で入力してください`

**Impact Range**
- Form SCR-12 · `_common/thong-bao-ja.md`

---

#### `[INVESTIGATION]` E06-INV-01 — Confirm Q52: block on temperature deviation or receive into quarantine

**Overview**
- **Hai điều trái nhau trong chính RFP:** BR-TEMP-02 (tr.21) *"luôn chặn xác nhận, không có ngoại
  lệ"* ⟷ FR-REC-05 (tr.15-16) *"chuyển hàng vào cách ly"*
- **Giả định vendor:** *"Nhận vào cách ly (bao trùm cả hai)"* · **Mức đổi:** Vừa
- Khách chọn "chặn" → **bỏ phần tạo lô cách ly lúc nhập**
- ⚠ Kèm một **câu hỏi phụ chưa ai trả lời:** nếu chọn "chặn" thì FR-REC-05 *"chuyển hàng vào cách
  ly"* áp vào lúc nào?

**References**
- SCR-12 §6.3 #1 · `RF:122, 143-173`

---

#### `[INVESTIGATION]` E06-INV-02 — Confirm Q51: are supplier lot number and production date mandatory

**Overview**
- Danh sách P0 của FR-REC-02 **không có** hai field này; từ điển dữ liệu Lot (tr.50) **bắt buộc cả hai**
- **Giả định vendor:** có chặn như trường P0
- **Mức đổi:** Q51 ghi **Nhỏ**, nhưng thực tế **chạm cột DB** — phải đổi `not null` thành nullable,
  là migration chứ không phải sửa form

**References**
- SCR-12 §6.3 #2 · `client-qa-list.md:78` · `BR-EXP-01`

---

#### `[INVESTIGATION]` E06-INV-03 — Confirm Q53: does lot_status need the 保留 value

**Overview**
- **RFP tự mâu thuẫn:** Hình 11 (tr.19) vẽ `隔離 → 保留 → 解除/廃棄`; FR-INV-05 (tr.22) chỉ có
  **4 trạng thái**
- **Giả định vendor:** `保留` là **bước nghiệp vụ trong lúc lô đang cách ly**, không phải trạng
  thái riêng — cách hiểu này **chưa được khách xác nhận**
- **Mức đổi:** có `保留` → thêm giá trị enum + 2 dòng `lot_status_transitions` + màn chuyển trạng
  thái. Kéo theo: Tình trạng đóng gói NG có chỗ đứng riêng

**References**
- SCR-12 §6.3 #5 #3 #11 · `ENUM:19` · `PREMISE` `GĐ-1`

---

#### `[INVESTIGATION]` E06-INV-04 — Confirm Q2: which reason code catalogue to use

**Overview**
- FR-REC-03 đòi mã lý do cho số lượng từ chối / chờ xử lý, nhưng **không nói danh mục nào**
- **Giả định vendor:** cấu hình được (bảng danh mục, không hard-code)
- Không chặn `E06-23-BE-01`; chỉ chặn `E06-23-BE-02`

**References**
- SCR-12 §6.3 #4 · FR-REC-03 (tr.16)

---

---

### E07 · Tồn kho & trạng thái lô

| | |
|---|---|
| **Màn** | SCR-18 (14 dòng 6.3) · SCR-19 (15 dòng 6.3) |
| **Nhóm LAB-1 đối chiếu** | F03 — 90 SP / 51 MD |
| **Số item** | 1 epic + 2 story + 4 parent + 14 dev task + 3 investigation = **24** |

```
[EPIC] E07 Make inventory search trustworthy and lot status changes traceable
├── [STORY] US-26 Quality manager searches inventory and gets a complete, honest result set
│   ├── [PARENT][BE] E07-26-BE Add server-side paging, supplier filter and query validation
│   │   ├── E07-26-BE-01 Add server-side paging with a real total count
│   │   ├── E07-26-BE-02 Move the location filter from TypeScript into the query
│   │   ├── E07-26-BE-03 Add supplier code as a ninth search criterion
│   │   └── E07-26-BE-04 Reject an expiry range whose start is after its end
│   └── [PARENT][FE] E07-26-FE Make the search screen tell the truth when things go wrong
│       ├── E07-26-FE-01 Build the paging control block below the table
│       ├── E07-26-FE-02 Map the fields payload back onto the filter inputs
│       ├── E07-26-FE-03 Split loading state from data so a failed first load exits the spinner
│       └── E07-26-FE-04 Disambiguate the temperature zone filter label
├── [STORY] US-05 Quality manager changes a lot status with a reason and an audit trail
│   ├── [PARENT][BE] E07-05-BE Version the transition matrix and close the validation gaps
│   │   ├── E07-05-BE-01 Drop 'available' from the zod target set
│   │   ├── E07-05-BE-02 Enforce the 500-character reason limit below zod
│   │   ├── E07-05-BE-03 Add version_label and valid_from to lot_status_transitions
│   │   └── E07-05-BE-04 Decide and implement allocation release on quarantine or scrap
│   └── [PARENT][FE] E07-05-FE Give the lot screen a way back and real error boundaries
│       ├── E07-05-FE-01 Add the return link to inventory search
│       ├── E07-05-FE-02 Build error.tsx and not-found.tsx with the registered Japanese copy
│       ├── E07-05-FE-03 Split the 5xx message from the input-error message
│       └── E07-05-FE-04 Hide the allocation link from roles that cannot open it
[INVESTIGATION] E07-INV-02 Confirm whether quarantine or scrap must release allocations automatically
[INVESTIGATION] E07-INV-03 Confirm which role may release allocations on behalf of quality control
[INVESTIGATION] E07-INV-04 Record the decision not to build the /lots list page
```

---

#### `[EPIC]` E07 — Make inventory search trustworthy and lot status changes traceable

**Overview & Goal**
- As a `品質管理` (*"Quản lý chất lượng"*)
- I want tra cứu tồn kho ra **đủ** kết quả, và đổi trạng thái lô có lý do và dấu vết
- So that không lô nào biến mất khỏi tầm nhìn, và mọi lần đổi trạng thái đều dựng lại được

**Scope & Features**
- Phân trang phía máy chủ 100 dòng/trang — hôm nay `max_rows = 1000` **cắt im lặng**
- Thêm tiêu chí lọc Nhà cung cấp (US-26 AC1 đòi 8 tiêu chí, màn thiếu cái này)
- Chặn khoảng ngày đảo ngược, trả lỗi về đúng ô
- Đánh phiên bản cho `lot_status_transitions` — bảng luật **duy nhất không có phiên bản**
- Lối quay lại và hai biên lỗi cho SCR-19

**Ngoài phạm vi**
- Gỡ phân bổ → **E08** (SCR-21 có nút thật); E07 chỉ quyết **có tự gỡ hay không**
- Trạng thái `保留` → **E06** (`E06-INV-03`), vì gốc nằm ở luồng nhập
- Trang danh sách `/lots` — **đã quyết không dựng**, xem `E07-INV-04`

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-18-56** đảo chiều — Given hơn 1000 lô khớp bộ lọc · When màn render · Then **không** còn
  cắt im lặng ở 1000 dòng
- **AC-19-32** vẫn đúng — Given lô đã có lịch sử · When thử `UPDATE`/`DELETE` trên
  `lot_status_history` · Then trigger append-only chặn

**References & Dependencies**
- Spec: `scr-18-tra-cuu-ton-kho.md` §6.3 #1…#14 · §6.4.1…§6.4.10 ·
  `scr-19-trang-thai-lot.md` §6.3 #1…#15 · §6.4.1…§6.4.8
- Estimate LAB-1: F03 — 90 SP / 51 MD

---

#### `[STORY]` US-26 — Quality manager searches inventory and gets a complete, honest result set

**Overview**
- **Who:** sáu vai không phải tài xế
- **What:** lọc lô theo 8 tiêu chí, xem 9 cột, bấm mã lô sang lý lịch lô
- **Why:** FR-INV-06 (P1) — *"Kết quả nhất quán và tôn trọng quyền theo kho"*

**Acceptance Criteria**
- **AC-18-14** — Given cả 8 ô để trống · When bấm `検索` · Then request là `GET /api/inventory`
  **không tham số nào** — ô rỗng **không** được gửi thành `?skuCode=`
- **AC-18-15** — Given ô `ロット番号` gõ `L2610` · When tìm · Then kết quả gồm **mọi** lô có
  `lot_code` chứa chuỗi đó (khớp một phần)
- **AC-18-19** — Given hai ô ngày `2026-10-01` và `2026-10-31` · When tìm · Then chỉ lô có
  `expiry_date` trong khoảng đó — biên hai đầu **tính vào**
- **AC-18-23** — Given `有効期限（開始） = 2026-10-31` và `（終了） = 2026-10-01` · When tìm ·
  Then API trả **422**, lỗi gắn vào ô `expiryFrom` với câu `M_102`
- **AC-18-31** — Given kết quả bất kỳ · When bảng render · Then đúng **9 cột**, đúng thứ tự
- **AC-18-32** — Given một lô nằm ở **hai** vị trí (120 ở `C-01`, 30 ở `C-02`) · When render ·
  Then lô đó là **một hàng duy nhất**, cột 5 liệt cả hai vị trí
- **AC-18-36** — Given lô đã hết tồn ở mọi vị trí · When render · Then lô **vẫn là một hàng**,
  cột 5 hiện `在庫なし`, cột 6/7/8 hiện `0`
- **AC-18-37** — Given lô có một vị trí `qty_on_hand = 0` và một vị trí `= 40` · When render ·
  Then cột 5 chỉ liệt vị trí còn 40, cột 6 ghi **40**
- **AC-18-44** — Given kết quả nhiều hàng · When render · Then thứ tự là `expiry_date` tăng dần
  rồi `lot_code` tăng dần — lô sắp hết hạn ở trên cùng (FEFO)
- **AC-18-53** — Given một hàng bất kỳ · When bấm mã lô ở cột 1 · Then sang `/lots/{lotId}` —
  và đó là **thao tác rời màn duy nhất**
- **AC-18-57** — Given 2.418 lô khớp bộ lọc **sau khi có phân trang** · When render · Then đúng
  **100** hàng, khối điều khiển dưới bảng có `前のページ` · `次のページ`
- **AC-18-58** — Given đang ở trang 3 với bộ lọc `状態 = 隔離` · When bấm `次のページ` · Then bộ
  lọc **giữ nguyên**, chỉ số trang đổi
- **AC-18-59** — Given phân trang đã có và bộ lọc `保管場所 = C-01` · When đọc số tổng · Then số
  đó là tổng **thật** của lô còn hàng ở `C-01`
- **AC-18-60** — Given phân trang đã có · When đếm truy vấn phía máy chủ cho một trang · Then
  đúng **2** — một lấy dòng, một đếm tổng
- **AC-18-61** đảo chiều — Given khối lọc · When đếm tiêu chí · Then có ô `仕入先` (hôm nay thiếu)
- **AC-18-47** — Given bảng đang hiện 24 hàng · When một lượt tìm trả **422** · Then dòng đỏ hiện
  ra **và** lỗi gắn đúng từng ô
- **AC-18-48** — Given bảng đang hiện kết quả · When một lượt tìm trả **500** · Then câu là
  `システムエラーが発生しました。時間をおいて再度お試しください`
- **AC-18-50** — Given lượt gọi ở **lần tải đầu** thất bại · When màn render xong · Then chỉ dòng
  lỗi hiện trên bảng rỗng — **không** còn `読み込み中…`

**References & Dependencies**
- Spec: SCR-18 §6.4.3 · §6.4.5 · §6.4.7 · §6.4.9 · §6.4.10

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E07-26-BE — Add server-side paging, supplier filter and query validation

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `API route` + `RPC / luật`

**Specification**
- Bốn việc máy chủ của `US-26`. Thứ tự bắt buộc: `E07-26-BE-01` → `E07-26-BE-02` (dời bộ lọc vị
  trí **là phần khó nhất** của phân trang, không phải phần thêm nút)

**Impact Range**
- `app/api/inventory/` · `inventoryQuerySchema` · `COLUMNS` · `lookups`

---

##### `[DEV TASK]` E07-26-BE-01 — Add server-side paging with a real total count

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- Hôm nay **không có phân trang**, không `limit`/`range`/truy vấn đếm. `max_rows = 1000`
  **cắt im lặng**: dòng đếm hiện `1000件` như thể là toàn bộ
- Cắt ngầm là **lỗi**, không phải giới hạn thiết kế (`R-15`) — nó làm `品質管理` **mất lô mà
  không biết**. Bước 5 mở rộng phạm vi này một cách **có chủ đích** cho LAB-5
- **Spec đã định nghĩa xong giao diện và nhãn** (S18): phía máy chủ, **100 dòng/trang**, kèm tổng
  số thật
- **AC-18-57** · **AC-18-59** · **AC-18-60** (đúng **2** truy vấn mỗi trang)

**Impact Range**
- `app/api/inventory/` · `inventoryQuerySchema` · `CFG:18`

---

##### `[DEV TASK]` E07-26-BE-02 — Move the location filter from TypeScript into the query

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` · **Phụ thuộc:** `E07-26-BE-01`

**Specification**
- `保管場所` đang lọc **phía TypeScript sau truy vấn** (`R-12`). Hôm nay vô hại; **sau khi có phân
  trang thì sai** — lọc một trang 100 dòng rồi báo "trang 1/25" là **báo sai số**
- Không lọc trong embed được: lọc embed sẽ cắt mảng `locations` và làm `在庫数` thôi khớp `引当済`
- Cách làm: truy vấn con lấy `lot_id` từ `inventory_balances` rồi `.in('id', …)`, **giữ nguyên
  embed `locations` đầy đủ**
- ⚠ **Đây là phần khó nhất của phân trang**
- **AC-18-18** vẫn đúng — Given chọn `C-01` · When tìm · Then chỉ lô còn hàng ở `C-01`
- **AC-18-32** vẫn đúng — Given lô ở hai vị trí · Then cột 5 vẫn liệt **cả hai**

**Impact Range**
- `INVQ:101-102` · `inventory_balances` · embed `locations`

---

##### `[DEV TASK]` E07-26-BE-03 — Add supplier code as a ninth search criterion

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- **US-26 AC1** đòi tìm theo 8 tiêu chí, trong đó có **nhà cung cấp**. Màn có 8 ô nhưng tách hạn
  thành bắt đầu/kết thúc và **bỏ nhà cung cấp**
- Dữ liệu **đã có sẵn**: `lots.supplier_id` + `lots.supplier_lot_no`. Không ai ghi vết chỗ này
- Thêm `supplierCode` vào `inventoryQuerySchema`, `suppliers!inner(code, name)` vào `COLUMNS`,
  `suppliers` vào `kinds` của lookups
- Nhãn JA **đã có sẵn** ở SCR-12 (`仕入先`) — không cần soạn chuỗi mới
- **AC-18-61** đảo chiều

**Impact Range**
- `inventoryQuerySchema` · `COLUMNS` · `lookups` · lưới lọc SCR-18

---

##### `[DEV TASK]` E07-26-BE-04 — Reject an expiry range whose start is after its end

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- `有効期限（開始） > （終了）` **hợp lệ với zod**, trả danh sách rỗng. Người dùng thấy
  `該当する在庫はありません` và **không biết lỗi nằm ở hai ô ngày**
- **Spec quyết: chặn, không chỉ cảnh báo.** Thêm `.refine` vào `inventoryQuerySchema` với
  `path: ['expiryFrom']`, câu **`M_102`**. Cùng nếp với `.refine` thứ tự ngày của SCR-12
- **AC-18-23** — Given hai ngày đảo ngược · When tìm · Then **422**, lỗi gắn vào ô `expiryFrom`
- Phụ thuộc `E07-26-FE-02` để lỗi hiện đúng ô

**Impact Range**
- `INVQ:32-43` · `_common/thong-bao-ja.md` (`M_102`)

---

#### `[PARENT][FE]` E07-26-FE — Make the search screen tell the truth when things go wrong

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Bốn chỗ màn đang nói sai hoặc nói thiếu khi có lỗi

**Impact Range**
- `BROWSER:47` · `BROWSER:83` · `FILTER` · khối điều khiển dưới bảng

---

##### `[DEV TASK]` E07-26-FE-01 — Build the paging control block below the table

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E07-26-BE-01`

**Specification**
- Khối điều khiển dưới bảng — nhãn đã định nghĩa ở S18
- **AC-18-57** — Given 2.418 lô · Then 100 hàng + `前のページ` · `次のページ`
- **AC-18-58** — Given đang trang 3 với bộ lọc · When sang trang · Then bộ lọc **giữ nguyên**
- **AC-18-30** vẫn đúng — Given đổi giá trị một ô mà **không** bấm `検索` · Then **không** gọi API

**Impact Range**
- Khối điều khiển của SCR-18

---

##### `[DEV TASK]` E07-26-FE-02 — Map the fields payload back onto the filter inputs

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- API trả `fields` với câu JA riêng cho **từng tham số**, UI **bỏ hết**, chỉ hiện một câu chung
  `絞り込み条件を確認してください`
- `BROWSER:47` chỉ đọc `result.status === 422`; **không có bản đồ `fields` → ô nào**
- Hai component `TF` và `SF` **đã sẵn sàng nhận** prop `errors` và render `FieldErrorList` — chỉ
  cần truyền xuống
- **AC-18-20** — Given ô `ロット番号` gõ hơn 100 ký tự · Then **422** với
  `fields.lotCode = ['検索条件が長すぎます']`, gắn đúng ô
- **AC-18-22** — Given `?expiryType=xxx` · Then 422 với `fields.expiryType` gắn đúng ô
- **AC-18-47** — Given bảng đang hiện 24 hàng · When 422 · Then bảng **giữ nguyên** và lỗi gắn ô

**Impact Range**
- `BROWSER:47` · `FILTER` · `TF` · `SF`

---

##### `[DEV TASK]` E07-26-FE-03 — Split loading state from data so a failed first load exits the spinner

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **Lỗi ở lần tải đầu để màn kẹt ở `読み込み中…` vĩnh viễn** (S9b): `rows` vẫn `null` nên nhánh
  "đang tải" vẫn render, trong khi **không còn gì đang tải** và không có nút thử lại
- `BROWSER:83` chia nhánh theo `rows === null`, trong khi "chưa tải xong" và "tải hỏng" là **hai
  việc khác nhau** → thêm một trạng thái `loaded`
- Cộng: màn không phân biệt **500** với **403 / mạng hỏng** — cả ba hiện cùng câu. Thêm nhánh
  `result.status >= 500` dùng `M_53`. **Cùng một sửa đổi với SCR-12 #13, SCR-20, SCR-23, SCR-35**
- **AC-18-50** · **AC-18-48** · **AC-18-49** (mạng hỏng giữ câu `在庫を読み込めませんでした`)

**Impact Range**
- `BROWSER:47` · `BROWSER:83` · `_common/thong-bao-ja.md` (`M_53`)

---

##### `[DEV TASK]` E07-26-FE-04 — Disambiguate the temperature zone filter label

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Ô lọc `温度帯` lọc theo `skus.temp_zone`, còn cột `保管場所（在庫）` hiện `locations.temp_zone`
  — **hai thứ có thể khác nhau** (`R-10`). Lọc `冷蔵` vẫn có thể ra hàng mà cột 5 ghi `常温`
- Đổi nhãn cho rõ, ví dụ `温度帯（SKU）`, hoặc thêm hint
- ⚠ **Nhãn ô lọc là nhãn riêng của màn**, không vào đăng ký chung. Chữ chính xác là việc của
  **người bản ngữ cùng khách** — spec **không** tự chốt chữ, chỉ chốt là phải làm rõ
- **AC-18-17** vẫn đúng — Given chọn `冷蔵` · Then bộ lọc áp lên `skus.temp_zone`

**Impact Range**
- Nhãn ô lọc `温度帯` của SCR-18

---

#### `[STORY]` US-05 — Quality manager changes a lot status with a reason and an audit trail

**Overview**
- **Who:** `品質管理`
- **What:** xem lý lịch một lô và đổi trạng thái theo ma trận, kèm lý do bắt buộc
- **Why:** FR-INV-05 (P0) — mỗi lần đổi là một quyết định chất lượng phải dựng lại được

**Acceptance Criteria**
- **AC-19-16** — Given bảng `lot_status_transitions` · When đếm · Then **đúng 4 dòng**:
  `available→quarantined`, `released→quarantined`, `quarantined→released`, `quarantined→scrapped`
- **AC-19-17** — Given lô `利用可能` · Then **đúng một** nút `隔離`
- **AC-19-19** — Given lô `隔離` · Then **đúng hai** nút theo thứ tự `リリース` rồi `廃棄`
- **AC-19-20** — Given lô `廃棄` · Then **không nút nào**
- **AC-19-21** — Given lô `廃棄` · When gọi thẳng API với `toStatus: 'available'` · Then **422**
  `RULE_LOT_TRANSITION`
- **AC-19-22** — Given `toStatus` **bằng đúng** trạng thái hiện tại · Then **422**
  `RULE_LOT_TRANSITION` — ma trận không có dòng tự chuyển
- **AC-19-26** / **AC-19-27** — Given lô `隔離` và lý do hợp lệ · When bấm `変更` cho đích
  `リリース` · Then `lot_state.status='released'`, `status_changed_at` cập nhật, **đúng một** dòng
  mới ở `lot_status_history`
- **AC-19-31** — Given lý do có khoảng trắng hai đầu · When gửi · Then giá trị lưu đã cắt trắng
- **AC-19-33** — Given lô vừa đổi · When đọc bảng lịch sử · Then hàng đầu đời có `変更前` là `-`
- **AC-19-35** / **AC-19-36** — Given ô `理由` trống hoặc chỉ khoảng trắng · When bấm `変更` ·
  Then **không** request nào, hiện `理由を入力してください`
- **AC-19-43** — Given bất kỳ ca 403/404/409/422 nào · When kiểm DB · Then `lot_state` giữ nguyên,
  không dòng mới ở `lot_status_history` lẫn `events`
- **AC-19-44** — Given một ca lỗi · When nhìn màn · Then khối xác nhận **vẫn mở** và chữ đã gõ
  trong ô `理由` **vẫn còn**
- **AC-19-57** / **AC-19-58** — Given đích là `廃棄` và còn đơn `引当済` · Then có thêm ô
  `ロット番号（確認）`; gõ sai thì **không** request nào
- **AC-19-61** — Given màn đang mở · When nhìn đầu trang · Then có liên kết `在庫照会へ戻る`
  trỏ `/inventory`

**References & Dependencies**
- Spec: SCR-19 §6.4.3 · §6.4.4 · §6.4.5 · §6.4.7 · §6.4.8

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E07-05-BE — Version the transition matrix and close the validation gaps

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- Bốn việc máy chủ của `US-05`. `E07-05-BE-04` chặn bởi `E07-INV-02`

**Impact Range**
- `lot_status_transitions` · `set_lot_status` · `apply_lot_status` · `allocations`

---

##### `[DEV TASK]` E07-05-BE-01 — Drop 'available' from the zod target set

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `LOT_STATUS_CHANGE_TARGETS` của zod có **4** giá trị kể cả `'available'`, trong khi ma trận
  **không có dòng nào** `to_status='available'`. Gọi API với giá trị đó qua được zod, qua được
  route, rồi **luôn luôn** vỡ ở `apply_lot_status`
- Comment của chính schema nói danh sách hiển thị đến từ `lot_status_transitions`, nhưng **hằng số
  zod thì không đọc bảng**
- **Wireframe 7.1 đã quyết: bỏ `'available'`.** LAB-5 sửa `Z:9` còn ba giá trị
- **AC-19-40** — Given `toStatus` không thuộc enum · Then **422** với câu
  `変更後の状態を選択してください`
- Nếu nghiệp vụ thật sự cần gỡ `隔離` về `利用可能` thì đó là **thêm dòng vào ma trận**, không
  phải nới zod

**Impact Range**
- `Z:9` · `lot_status_transitions`

---

##### `[DEV TASK]` E07-05-BE-02 — Enforce the 500-character reason limit below zod

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` hoặc `RPC / luật`

**Specification**
- Trần **500 ký tự** của `理由` **chỉ có ở zod**. `set_lot_status` chỉ `btrim` + kiểm rỗng; cột
  `lot_status_history.reason text` **không có ràng buộc độ dài**
- Cùng họ với **năm chỗ zod chặt hơn RPC** trong kiến trúc
- Thêm `check (char_length(reason) <= 500)` ở cột, hoặc một phép kiểm trong `set_lot_status`
- **AC-19-37** — Given lý do 501 ký tự qua API · Then **422** `validation_failed`
- **AC-19-38** đảo chiều — Given cùng lý do 501 ký tự gửi **thẳng tới RPC** qua PostgREST ·
  Then bị từ chối (hôm nay: **được chấp nhận và lưu đủ 501 ký tự**)

**Impact Range**
- `lot_status_history.reason` · `set_lot_status`

---

##### `[DEV TASK]` E07-05-BE-03 — Add version_label and valid_from to lot_status_transitions

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)`

**Specification**
- `lot_status_transitions` là bảng luật **duy nhất không có `version_label` và `valid_from`**,
  **không** append-only, và **không** có trigger `audit_row_change`. Ba bảng luật kia đều có
  phiên bản theo ngày hiệu lực
- Sửa ma trận hôm nay làm **đổi ý nghĩa của lịch sử hôm qua**, và không để lại dấu vết nào:
  `events.rule_version` của `lot.status_changed` là NULL
- Dựng lại một phép đổi cũ **không biết nó đã chạy trên ma trận nào**
- **AC-19-29** đảo chiều — Given dòng `events` của `lot.status_changed` · When đọc `rule_version` ·
  Then có `version_label` của ma trận đã dùng (hôm nay: **NULL**)
- **AC-19-16** vẫn đúng — bốn dòng ma trận không đổi, chỉ thêm cột phiên bản

**Impact Range**
- `lot_status_transitions` · `apply_lot_status` · `events.rule_version`

---

##### `[DEV TASK]` E07-05-BE-04 — Decide and implement allocation release on quarantine or scrap

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E07-INV-02`

**Specification**
- **US-05 AC3 (P0):** *"Đổi trạng thái thì kết quả phân bổ cập nhật theo thời gian thực"*
- **Không có trong code.** `apply_lot_status` không chạm `allocations` hay `orders`. Màn chỉ
  **cảnh báo** và **không khoá nút**
- LAB-2 chốt không tự gỡ phân bổ, thay bằng thao tác tay — nhưng **chưa ai hỏi khách** chọn nhánh
  nào: (a) RPC tự gỡ phân bổ khi lô sang `隔離`/`廃棄`, kéo theo đơn tụt trạng thái · (b) giữ thủ công
- **AC-19-59** phụ thuộc đáp án — Given lô bị đổi sang `廃棄` khi còn đơn `引当済` · When kiểm DB ·
  Then hôm nay `allocations` và `orders` **không đổi một dòng nào**
- **AC-19-53** vẫn đúng — khối cảnh báo hiện cho cả sáu vai non-driver
- **AC-19-54** vẫn đúng — lô đã `引当解除` thì khối cảnh báo **không** hiện

**Impact Range**
- `apply_lot_status` · `allocations` · `orders` · SCR-21 (E08)

---

#### `[PARENT][FE]` E07-05-FE — Give the lot screen a way back and real error boundaries

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Màn `navHidden` không có menu, không breadcrumb, **không lối quay lại** — xử xong một lô,
  `品質管理` phải bấm nút back của trình duyệt

**Impact Range**
- SCR-19 · `app/error.tsx` · `app/not-found.tsx` · `ACT:57-63`

---

##### `[DEV TASK]` E07-05-FE-01 — Add the return link to inventory search

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- **Spec đã định nghĩa xong giao diện và nhãn**: liên kết `在庫照会へ戻る` ở đầu trang trỏ
  `/inventory`, **giữ bộ lọc nếu có** (S25)
- **AC-19-61** — Given màn đang mở · Then có liên kết đó, và không mục nào trong thanh menu dẫn tới
  màn này

**Impact Range**
- Đầu trang SCR-19

---

##### `[DEV TASK]` E07-05-FE-02 — Build error.tsx and not-found.tsx with the registered Japanese copy

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Trong `app/` chỉ có `forbidden.tsx`; **không có `error.tsx`, không có `not-found.tsx`** → cả
  trang 500 lẫn trang 404 hiện **chữ tiếng Anh mặc định của Next.js**
- `LOT_STATE_MISSING` là mã tầng TypeScript, **không thuộc 42 mã DB**, không khớp tiền tố nào →
  API trả 500; trên trang thì `throw new Error`
- **AC-19-09** / **AC-19-10** — Given `lotId` không phải GUID, hoặc GUID không khớp lô nào ·
  Then **404** với câu `指定されたロットは見つかりません。在庫照会から選び直してください`
- **AC-19-11** — Given lô có `lots` nhưng **không** có `lot_state` · Then **500** với câu
  `システムエラーが発生しました…` — đây là **dữ liệu hỏng**, không phải lỗ hổng quyền
- ⚠ Hai biên lỗi này dùng chung cho **toàn ứng dụng**, không riêng SCR-19

**Impact Range**
- `app/error.tsx` · `app/not-found.tsx` · mục 4.2.4

---

##### `[DEV TASK]` E07-05-FE-03 — Split the 5xx message from the input-error message

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Màn không phân biệt **500** với **422**: `internal_error`, `invalid_json` và
  `VALIDATION_LOT_STATUS_SOURCE` đều hiện `状態を変更できませんでした`
- Thêm nhánh `status >= 500` trong `ACT:57-63` dùng `M_53` — **cùng câu với trang 500 ở
  `E07-05-FE-02`**, nên hai chỗ nói giống nhau
- Cộng: `.strict()` từ chối khoá lạ bằng câu **tiếng Anh** `Unrecognized key: "<tên>"` rơi vào
  khoá `_form` → dùng `M_52` đã có trong đăng ký chung
- **AC-19-39** — Given field lạ · Then **422** với câu `送信内容に不明な項目が含まれています`
- **AC-19-45** — Given mã lỗi không có `detail.fields` · Then câu nằm ở khối `_form`
- **AC-19-47** — Given mạng rớt · Then câu `通信できませんでした。接続を確認して…`

**Impact Range**
- `ACT:57-63` · `Z:23` · `JSONR:26` · `_common/thong-bao-ja.md` (`M_52`, `M_53`)

---

##### `[DEV TASK]` E07-05-FE-04 — Hide the allocation link from roles that cannot open it

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E07-INV-03`

**Specification**
- Khối cảnh báo bảo người đọc sang SCR-21 gỡ phân bổ và đặt liên kết `引当画面へ` → `/allocation`.
  **`/allocation` chỉ mở cho `dispatcher`**
- Khối cảnh báo nằm **trên** nhánh vai nên **cả 6 vai đều thấy liên kết**. Vai `品質管理` — chính
  người đang đứng trước nút `廃棄` — bấm vào sẽ nhận **403**
- Hai cách: ẩn liên kết cho vai không mở được, **hoặc** mở quyền đọc SCR-21 cho `品質管理`.
  **Mở quyền là việc khách quyết** → khuyến nghị ẩn liên kết trước
- **AC-19-60** đảo chiều — Given vai `品質管理` · When nhìn khối cảnh báo · Then **không** thấy
  liên kết dẫn tới 403

**Impact Range**
- `ACT:76` · `ACT:110-112` · `LABELS:29`

---

#### `[INVESTIGATION]` E07-INV-02 — Confirm whether quarantine or scrap must release allocations automatically

**Overview**
- **US-05 AC3 (P0)** đòi *"kết quả phân bổ cập nhật theo thời gian thực"*
- Hai nhánh, **chưa ai hỏi khách chọn nhánh nào**:
  - **(a)** RPC tự gỡ phân bổ khi lô sang `隔離`/`廃棄` — kéo theo đơn tụt trạng thái
  - **(b)** giữ thao tác tay như LAB-2 đã chốt, màn chỉ cảnh báo
- **Giả định vendor:** (b), theo quyết định LAB-2
- **Mức đổi:** (a) → `apply_lot_status` chạm `allocations` và `orders`, thêm cả state machine của đơn
- ⚠ Đây là **P0 chưa phủ**, không phải nợ nhỏ

**References**
- SCR-19 §6.3 #4 #9 · `FIX:26-69` · `screen-list-final-vi.md` §3.3

---

#### `[INVESTIGATION]` E07-INV-03 — Confirm which role may release allocations on behalf of quality control

**Overview**
- Tài liệu hiện trạng ghi SCR-19 *"có nút Gỡ phân bổ thủ công"* — **trên SCR-19 không có nút nào
  như vậy**. Nút thật nằm ở SCR-21, nơi có quyền `dispatcher`, **không ở nơi có người cần dùng**
- Dựng nút `引当解除` ngay trên SCR-19 là **đổi phân quyền** — `release_allocation` thuộc `dispatcher`
- **Hỏi khách:** vai nào được gỡ phân bổ khi `品質管理` cần cách ly một lô
- Liên quan trực tiếp `E07-05-FE-04` và `E07-INV-02`

**References**
- SCR-19 §6.3 #8 #9 · `screen-list-final-vi.md` dòng 32

---

#### `[INVESTIGATION]` E07-INV-04 — Record the decision not to build the /lots list page

**Overview**
- Menu khai SCR-19 `href: '/lots'` nhưng `app/(app)/lots/` chỉ có `[lotId]/page.tsx`, **không có
  trang danh sách**. Vì `navHidden: true` nên **không vai nào bấm trúng link hỏng**
- **Đã quyết ở wireframe 7.2 / 2.2: KHÔNG dựng `/lots`** — trang đó trùng gần hết với SCR-18, và
  sinh ra **hai nơi phải sửa** mỗi khi bộ lọc đổi
- **Việc duy nhất:** sửa `href` của entry SCR-19 thành `/inventory` hoặc bỏ hẳn
- Ghi thành quyết định có văn bản, **không** để ngầm
- **AC-18-55** ghi lại hiện trạng này

**References**
- SCR-18 §6.3 #12 · `MENU:31`

---

### E08 · Đơn hàng & phân bổ tồn

| | |
|---|---|
| **Màn** | SCR-20 (16 dòng 6.3) · SCR-21 (23 dòng 6.3) |
| **Nhóm LAB-1 đối chiếu** | F04 + F05 — 215 SP / 122 MD |
| **Số item** | 1 epic + 3 story + 6 parent + 16 dev task + 6 investigation = **32** |

⚠ **Epic nặng nhất của bài.** 39 dòng 6.3 và 163 mã AC. SCR-21 là màn có **nhiều luật cài trùng
nhất**: bước ① cài hai bản, "lần phân bổ hiệu lực" cài **ba** bản.

```
[EPIC] E08 Make order intake and stock allocation consistent and auditable
├── [STORY] US-06 Dispatcher registers an order line that survives duplicate and master checks
│   ├── [PARENT][BE] E08-06-BE Close the order validation gaps and add paging
│   │   ├── E08-06-BE-01 Enforce the three limits that only zod checks today
│   │   ├── E08-06-BE-02 Add server-side paging to the order list
│   │   └── E08-06-BE-03 Return the existing order id on a 23505 duplicate
│   └── [PARENT][FE] E08-06-FE Make order feedback say what actually happened
│       ├── E08-06-FE-01 Stop treating every 409 as a duplicate reference
│       ├── E08-06-FE-02 Split the 5xx message and fix the stuck first-load spinner
│       ├── E08-06-FE-03 Distinguish loading, empty master and unselected in the two selects
│       ├── E08-06-FE-04 Show the contract delivery window rule on the order form
│       └── E08-06-FE-05 Build the paging control block below the order list
├── [STORY] US-07 Dispatcher allocates stock atomically in FEFO order with full evidence
│   ├── [PARENT][BE] E08-07-BE Deduplicate the allocation rules that exist in two or three places
│   │   ├── E08-07-BE-01 Unify the two implementations of exclusion step ①
│   │   ├── E08-07-BE-02 Collapse the three implementations of effective allocation run
│   │   └── E08-07-BE-03 Record rule_versions on release runs or document why they are empty
│   └── [PARENT][FE] E08-07-FE Stop the allocation screen from reporting things it did not do
│       ├── E08-07-FE-01 Split the two 422 groups so rolled-back runs stop claiming success
│       ├── E08-07-FE-02 Soft-block repeated judgement recording
│       ├── E08-07-FE-03 Add a delivery-date filter to the allocation list
│       ├── E08-07-FE-04 Read fields.reason in the release-allocation dialog
│       └── E08-07-FE-05 Fix the two comments that claim six evaluation steps
└── [STORY] US-08 Allocation refuses expiry inversion and honours the contract delivery window
    ├── [PARENT][BE] E08-08-BE Make the five-step chain enforce what the preview promised
    │   ├── E08-08-BE-01 Re-check steps ②④⑤ inside allocate_order
    │   └── E08-08-BE-02 Settle the multi-lot delivery history assumption
    └── [PARENT][FE] E08-08-FE Raise best-before expiry from a small badge to a real warning
        └── E08-08-FE-01 Raise the expired best-before lot to a visible warning level
[INVESTIGATION] E08-INV-01 Confirm Q9 — which evidence set each delivery term requires
[INVESTIGATION] E08-INV-02 Confirm Q31 — how an order changed after 16:00 is handled
[INVESTIGATION] E08-INV-03 Confirm which role registers orders — dispatcher or sales
[INVESTIGATION] E08-INV-04 Confirm Q65 and Q30 — partial allocation and multi-lot order lines
[INVESTIGATION] E08-INV-05 Confirm Q47 — who handles business-review rows and how
[INVESTIGATION] E08-INV-06 Confirm Q54 — delivery history rows without an expiry date
```

---

#### `[EPIC]` E08 — Make order intake and stock allocation consistent and auditable

**Overview & Goal**
- As a `配送計画者` (*"Điều phối giao hàng"*)
- I want tạo đơn và phân bổ tồn theo một chuỗi luật năm bước có bằng chứng
- So that mọi lần phân bổ dựng lại được, và không đơn nào đi tiếp với dữ liệu sai

**Scope & Features**
- Gom các luật đang cài hai–ba bản về một chỗ
- Phân trang phía máy chủ cho cả hai danh sách (`max_rows = 1000` **cắt im lặng**)
- Sửa chỗ màn **nói sai sự thật**: 422 của nhóm ① hiện câu "đã ghi nhận" trong khi transaction
  đã cuộn
- Chặn mềm việc bấm `判定結果を記録` vô hạn lần

**Ngoài phạm vi**
- Tự gỡ phân bổ khi lô bị cách ly → **E07** (`E07-INV-02`); E08 chỉ giữ cờ `要再引当` và nút thủ công
- Bộ bằng chứng POD theo `配送条件` → **E09**; SCR-20 chỉ **chọn** điều kiện
- Nhập đơn từ tệp / ERP — **ngoài phạm vi v6**, xem `E08-INV-02`

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-21-98** vẫn đúng — Given bất kỳ dòng nào của `allocation_runs`, `allocations`,
  `delivery_history`, `events` · When thử `UPDATE`/`DELETE` · Then bị chặn
- **AC-21-96** — Given cùng một đơn · When so kết quả của ba bản cài "lần phân bổ hiệu lực" ·
  Then ba bản cho **cùng** kết quả (sau `E08-07-BE-02` chỉ còn hai bản)

**References & Dependencies**
- Spec: `scr-20-don-hang.md` §6.3 #1…#16 · §6.4.1…§6.4.9 ·
  `scr-21-phan-bo-ton.md` §6.3 #1…#23 · §6.4.1…§6.4.13
- Estimate LAB-1: F04 + F05 — 215 SP / 122 MD

---

#### `[STORY]` US-06 — Dispatcher registers an order line that survives duplicate and master checks

**Overview**
- **Who:** `配送計画者` (⚠ US-06 ghi vai là `営業担当者` — xem `E08-INV-03`)
- **What:** nhập một dòng đơn với sáu thông tin, hệ chặn trùng tham chiếu và mã không có trong master
- **Why:** FR-OUT-01 (P0) — khách muốn đơn *"không còn rải trong email và Excel"*

**Acceptance Criteria**
- **AC-20-22** — Given form trống hết · When bấm `受注を登録` · Then **không** phát sinh request
- **AC-20-23** — Given `数量 = 0` · Then ô `数量` hiện `数量は1以上で入力してください`
- **AC-20-24** / **AC-20-25** — Given `顧客参照番号` dài hơn 100 ký tự, hoặc chỉ gồm khoảng trắng ·
  Then ô đó hiện câu riêng
- **AC-20-27** / **AC-20-28** — Given mã không có trong master · Then **422**
  `VALIDATION_UNKNOWN_MASTER`; cả hai mã sai thì **một** phản hồi duy nhất tô cả hai ô
- **AC-20-31** — Given bất kỳ ca 422/409/403 nào · When kiểm DB · Then **không** dòng mới ở `orders`
- **AC-20-33** — Given đã có đơn của `CUS-001` với `PO-2026-1042` · When gửi lại cùng cặp ·
  Then **409** `CONFLICT_DUPLICATE_ORDER_REF`
- **AC-20-34** / **AC-20-35** — Given 409 có `detail.orderId` · Then hiện câu + link; bấm link thì
  hàng đơn cũ **cuộn tới giữa màn và tô vàng**
- **AC-20-36** — Given cùng chuỗi tham chiếu nhưng **khách khác** · Then **200** — trùng tính theo
  cặp khách + tham chiếu
- **AC-20-37** — Given hai request gửi **cùng lúc** cùng cặp · Then ràng buộc unique chốt
- **AC-20-39** / **AC-20-40** — Given cặp có hợp đồng `default_delivery_term = doorstep` · Then ô
  `配送条件` đặt theo hợp đồng; cặp không hợp đồng thì về `車上渡し`
- **AC-20-41** — Given người dùng **đã tự chỉnh** ô `配送条件` · When đổi sang SKU khác có hợp
  đồng · Then **không** ghi đè lựa chọn của người dùng
- **AC-20-47** — Given danh sách có dữ liệu · Then hàng tiêu đề đúng **8 cột, đúng thứ tự**
- **AC-20-53** — Given nhiều đơn · Then thứ tự là `納品希望日` tăng dần rồi tiếp theo
- **AC-20-56** — Given 120 đơn · When nạp một lần · Then **1 truy vấn `orders` + 3 truy vấn `events`**
- **AC-20-57** — Given vượt **50** đơn sau khi có phân trang · Then chỉ 50 hàng hiện
- **AC-20-63** — Given một đơn đã tạo · When thử `UPDATE` thẳng trên `orders` · Then **KHÔNG** bị
  trigger nào chặn — `orders` **không** append-only (là lý do `E08-INV-02` quan trọng)

**References & Dependencies**
- Spec: SCR-20 §6.4.4…§6.4.9

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E08-06-BE — Close the order validation gaps and add paging

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `RPC / luật` + `API route` + `DB (migration)`

**Impact Range**
- `create_order` · `orders` · `app/api/orders/`

---

##### `[DEV TASK]` E08-06-BE-01 — Enforce the three limits that only zod checks today

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `DB (migration)`

**Specification**
- **Ba giới hạn chỉ có ở zod**: `顧客コード`/`SKUコード` ≤ 50 · `顧客参照番号` ≤ 100 ·
  `数量` ≤ 1.000.000 và phải nguyên. RPC chỉ kiểm `quantity <= 0`
- Cột `customer_ref` là `text` **không giới hạn độ dài**; `quantity` chỉ có `check > 0`
- Gọi thẳng API hoặc thẳng RPC thì **lọt cả ba**. `quantity > 2^31` cho Postgres `22003` → 500
- Cùng một lỗ hổng với `E06-01-BE-01` (SCR-12) và `E07-05-BE-02` (SCR-19) — **ba màn, một họ lỗi**
- **AC-20-29** — Given gọi thẳng RPC với `p_quantity = 0` · Then **422** `VALIDATION_QUANTITY_*`
- **AC-20-30** — Given `p_customer_ref` rỗng · Then **422** `VALIDATION_MISSING_FIELDS`

**Impact Range**
- `create_order` · `orders.customer_ref` · `orders.quantity`

---

##### `[DEV TASK]` E08-06-BE-02 — Add server-side paging to the order list

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- Danh sách **không có phân trang, không có giới hạn hàng**; `max_rows = 1000` cắt **im lặng** —
  người dùng không biết mình đang nhìn thiếu
- **Spec đã định nghĩa xong giao diện và nhãn** (S21): **50 dòng/trang**, ba nhãn riêng của màn
  `前のページ` · `次のページ` · `{tổng}件中 {từ}〜{đến}件`
- ⚠ Khác SCR-18 (**100 dòng/trang**) — hai màn hai con số, **không** gom thành một hằng chung
- **AC-20-57** — Given vượt 50 đơn · Then chỉ 50 hàng hiện, khối điều khiển hiện ra
- **AC-20-56** vẫn đúng — số truy vấn không phình theo số đơn

**Impact Range**
- `app/api/orders/` · `OLQ`

---

##### `[DEV TASK]` E08-06-BE-03 — Return the existing order id on a 23505 duplicate

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `CONFLICT_DUPLICATE_ORDER_REF` (RPC, **có** `detail.orderId`) và `conflict_duplicate` (Postgres
  23505, **không** có detail) cùng mô tả **một sự kiện nghiệp vụ**
- Phép kiểm trước trong RPC tồn tại **chỉ để** trao id đơn cũ cho màn; ràng buộc unique mới là
  chốt thật. **Đây là thiết kế đúng, không phải lỗi** — ghi lại thành quyết định có văn bản
- Muốn link luôn hiện: bắt `23505` trong RPC rồi tra lại đơn cũ và raise mã có detail
- **AC-20-37** — Given hai request cùng lúc · Then ca thua nhận 409 **có** `detail.orderId`

**Impact Range**
- `create_order` · `SQL:162-164`

---

#### `[PARENT][FE]` E08-06-FE — Make order feedback say what actually happened

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 5 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `FORM:130-145` · `LIST:48-53` · `SF:35-40` · `SHIP:55-61`

---

##### `[DEV TASK]` E08-06-FE-01 — Stop treating every 409 as a duplicate reference

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **Form coi MỌI status 409 là trùng tham chiếu** — nhánh `result.status === 409` chặn trước mọi
  phân loại, nên `conflict_concurrent_update` (`40001`/`40P01`) cũng hiện
  `同じ顧客参照番号の受注が既にあります` — **nói sai việc**
- **Spec đã định nghĩa câu riêng:** `M_64` `処理が混み合っています。もう一度登録してください`
- **AC-20-38** — Given 409 `conflict_concurrent_update` · Then câu là thể của `M_64`
- **AC-20-34** vẫn đúng cho ca trùng thật

**Impact Range**
- `FORM:130-137` · `_common/thong-bao-ja.md` (`M_64`)

---

##### `[DEV TASK]` E08-06-FE-02 — Split the 5xx message and fix the stuck first-load spinner

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Màn không phân biệt **500** với **422** — cả hai hiện
  `受注を登録できませんでした。入力内容を確認してください`, đẩy người dùng đi sửa dữ liệu vốn
  không sai. `failureMessage` **không có nhánh cho 5xx**
- Lần nạp danh sách **đầu tiên** mà hỏng thì màn hiện **đồng thời** `読み込み中…` và dòng đỏ —
  `orders` vừa là dữ liệu vừa là cờ "đã nạp xong"
- **Cùng một sửa đổi với `E06-01-FE-02`, `E07-26-FE-03`** và sẽ còn ở SCR-23, SCR-35
- **AC-20-32** — Given HTTP ≥ 500 · Then câu là `M_53`
- **AC-20-11** / **AC-20-12** — Given lỗi khác 422 / lỗi 422 · Then hai câu khác nhau

**Impact Range**
- `FORM:143` · `SHIP:55-61` · `LIST:48-53`

---

##### `[DEV TASK]` E08-06-FE-03 — Distinguish loading, empty master and unselected in the two selects

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Hai ô chọn `顧客コード` / `SKUコード` hiện **y hệt nhau** trong **ba tình huống khác hẳn**:
  đang tải · danh mục trống · người dùng chưa chọn — cả ba chỉ có `M_05 選択してください`
- `SelectField` **không có nhánh rỗng và không có trạng thái tải**
- **Spec đã định nghĩa câu cho ca danh mục trống:** khuôn `M_54`
- **AC-20-13** — Given danh mục khách trả mảng rỗng · Then dưới ô hiện câu riêng

**Impact Range**
- `SF:35-40` · `_common/thong-bao-ja.md` (`M_54`)

---

##### `[DEV TASK]` E08-06-FE-04 — Show the contract delivery window rule on the order form

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Đơn đăng ký xong ở SCR-20 **không được báo gì** về quy tắc cửa sổ giao; **tới SCR-21 mới biết**
  bị `業務判断` hoặc mất lô ứng viên ở bước ④
- `delivery_window_rule` **đã được tải về màn** nhưng **không component nào đọc**
- **Spec đã định nghĩa xong dòng tham khảo** (S22): `M_65`
  `契約の納品期限ルール：{ルール}（引当時に判定します）`
- **AC-20-45** — Given cặp có hợp đồng `AGR-005` (`ONE_THIRD`) · Then dòng tham khảo hiện quy tắc
- **AC-20-46** — Given một `納品希望日` chắc chắn trượt quy tắc · Then màn vẫn **nhận đơn** —
  dòng này là **tham khảo**, không phải chặn
- Việc này biến `delivery_window_rule` từ dữ liệu thừa thành **dữ liệu có người dùng** (6.3 #15)

**Impact Range**
- Form SCR-20 · `LOOKUPS:41` · `_common/thong-bao-ja.md` (`M_65`)

---

##### `[DEV TASK]` E08-06-FE-05 — Build the paging control block below the order list

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E08-06-BE-02`

**Specification**
- Khối điều khiển dưới bảng, ba nhãn riêng của màn đã định nghĩa ở S21
- **AC-20-57** — Given vượt 50 đơn · Then 50 hàng + khối điều khiển
- **AC-20-50** / **AC-20-51** vẫn đúng — bộ lọc trạng thái và ngày giữ nguyên khi sang trang

**Impact Range**
- Khối điều khiển của SCR-20

---

#### `[STORY]` US-07 — Dispatcher allocates stock atomically in FEFO order with full evidence

**Overview**
- **Who:** `配送計画者`
- **What:** chạy chuỗi loại trừ năm bước, phân bổ trọn gói theo FEFO, mọi lần để lại bằng chứng
- **Why:** FR-OUT-02 (P0) — `原子的アロケーション` (*"phân bổ nguyên tử: tất cả hoặc không gì cả"*)

**Acceptance Criteria**
- **AC-21-25** / **AC-21-26** — Given đơn mẫu · Then bảng phán định chỉ gồm lô của đúng SKU
- **AC-21-27** / **AC-21-28** / **AC-21-29** — Given lô quá hạn sử dụng · lô sai dải nhiệt · lô
  `隔離` · Then mỗi lô bị loại ở đúng bước, kèm câu căn cứ riêng
- **AC-21-30** — Given lô `リリース` còn tồn và đúng vùng nhiệt · Then **qua** bước ①
- **AC-21-31** — Given lô `廃棄` · Then **không xuất hiện** trong bảng
- **AC-21-51** / **AC-21-52** — Given hai lô đủ điều kiện · Then lô có hạn **sớm hơn** được lấy
  trước (FEFO)
- **AC-21-53** — Given lô có tồn 50 và `qty_allocated` 20 · Then `引当可能数` là 30
- **AC-21-54** — Given tổng `引当可能数` **nhỏ hơn** số lượng đơn · Then kết cục là thiếu tồn
- **AC-21-58** / **AC-21-59** — Given bấm `引当を実行` · Then **một** dòng `allocation_runs`
  (`result='allocated'`), các dòng `allocations`, và `lot_state.qty_allocated` tăng đúng
- **AC-21-60** — Given lần phân bổ đó · When đọc `evidence` · Then chứa đủ `deliveryDate`,
  `contractCode`, `deliveryWindowRule`, …
- **AC-21-61** — Given lần đó · When đọc `events` · Then có `allocation.allocated` mang
  `rule_version = 'BR-DELWIN-01/v1'`
- **AC-21-77**…**AC-21-81** — gỡ phân bổ: hộp xác nhận, lý do bắt buộc, `qty_allocated` giảm đúng,
  **không dòng `allocations` nào bị xoá hay sửa**
- **AC-21-87**…**AC-21-90** — cờ `要再引当` khi lô trong lần phân bổ hiệu lực bị cách ly
- **AC-21-94** / **AC-21-95** — chuỗi run `allocated → rejected` vẫn hiệu lực; `allocated →
  released` thì **không có** lần nào hiệu lực

**References & Dependencies**
- Spec: SCR-21 §6.4.4 · §6.4.7 · §6.4.8 · §6.4.11 · §6.4.12 · §6.4.13

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E08-07-BE — Deduplicate the allocation rules that exist in two or three places

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `RPC / luật`

**Specification**
- SCR-21 là màn có **nhiều luật cài trùng nhất**. Sửa một bản mà quên bản kia là **lệch im lặng**

**Impact Range**
- `allocate_order` · `release_allocation` · `effective_allocation_run` · `EXCL` · `A3`

---

##### `[DEV TASK]` E08-07-BE-01 — Unify the two implementations of exclusion step ①

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- **Bước ① cài hai bản độc lập**: TypeScript `useByReached` và SQL. Tập ứng viên cũng vậy:
  `isAllocationCandidate` ⟷ bản SQL
- Comment gọi bản SQL là *"SQL twin"* — **đã biết, chưa gom**
- Hai cách: thêm một kiểm tra tự động so hai bản trên cùng bộ dữ liệu, **hoặc** gom bản SQL thành
  một hàm dùng chung cho cả ba chỗ (`allocate_order`, `log_use_by_blocked_lots`)
- **AC-21-93** — Given đơn có n lô bị loại ở bước ① · When bấm **bất kỳ** nút phán định nào ·
  Then cả hai nhánh ghi cùng kết quả loại trừ
- `[tự viết]` Given cùng bộ dữ liệu · When chạy cả hai bản · Then kết quả giống hệt nhau

**Impact Range**
- `EXCL:69` · `EXCL:113-115` · `A3:74-78` · `A3:176` · `log_use_by_blocked_lots`

---

##### `[DEV TASK]` E08-07-BE-02 — Collapse the three implementations of effective allocation run

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- **"Lần phân bổ hiệu lực" cài ba bản**: TS `effectiveRun`, SQL viết thẳng trong
  `release_allocation`, SQL hàm `effective_allocation_run`. Hiện **khớp nhau**
- Gom hai bản SQL về một: `release_allocation` **gọi** `effective_allocation_run` thay vì lặp lại
  câu lệnh. Bản TS **phải ở lại** (nó chạy trên dữ liệu đã nạp sẵn)
- Rẻ, và bỏ được **một trong ba** chỗ phải sửa
- **AC-21-96** — Given cùng một đơn · When so kết quả ba bản · Then khớp nhau (sau task này: hai bản)
- **AC-21-94** / **AC-21-95** vẫn đúng sau khi gom

**Impact Range**
- `A3:280-287` · `B3:27-39` · `EFF:12-18`

---

##### `[DEV TASK]` E08-07-BE-03 — Record rule_versions on release runs or document why they are empty

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `release_allocation` **không ghi `rule_versions`**, trong khi `allocate_order` và
  `record_rejected_allocation` đều ghi. Run `引当解除` vì vậy mang `'{}'`
- **Đúng về logic** (không có phiên bản luật nào áp vào việc giải phân bổ) nhưng làm **bốn loại
  run không cùng hình dạng**
- Chọn một: ghi cùng bộ `ALLOCATION_RULE_VERSIONS` cho đủ bộ, **hoặc** ghi một câu vào tài liệu
  nói run `released` **cố ý** để trống. **Không** để người đọc tự đoán
- **AC-21-91** / **AC-21-92** — Given run `allocated`/`rejected`/`business_review` · Then
  `rule_versions` đầy đủ; Given run `released` · Then `{}` — hiện trạng cần một quyết định

**Impact Range**
- `A3:297-298` · `allocation_runs.rule_versions`

---

#### `[PARENT][FE]` E08-07-FE — Stop the allocation screen from reporting things it did not do

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 5 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `ACT:30` · `REL:27` · `RPREV:6` · `DETAIL:15` · danh sách SCR-21

---

##### `[DEV TASK]` E08-07-FE-01 — Split the two 422 groups so rolled-back runs stop claiming success

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- ⚠ **Thông báo nói SAI sự thật.** 422 của **nhóm ①** (`RULE_LOT_NOT_ALLOCATABLE`, `RULE_PLAN_*`)
  hiện cùng câu `引当不可として記録しました` như 422 của nhóm ②, **trong khi transaction đã cuộn
  và không dòng nào được ghi**
- `ACT:30` chỉ phân nhánh theo `result.status === 422`, không phân biệt hai nhóm
- **Quyết định wireframe 8.2, spec đã định nghĩa xong** (S22): tách nhánh theo sự có mặt của
  `detail.summary` — **có `summary` thì đúng là đã ghi**
- **AC-21-74** — Given plan hỏng giữa chừng · When nhìn màn · Then câu **không** được là
  `引当不可として記録しました`
- **AC-21-67** — Given hai ca 422 có ghi · Then `orders.status` vẫn `validated`, **không** dòng
  `allocations` nào, `qty_allocated` không đổi
- **AC-21-72** / **AC-21-73** — Given lô trong plan bị cách ly giữa preview và lúc bấm · Then phần
  giữ chỗ của **lô thứ nhất cũng cuộn**

**Impact Range**
- `ACT:30` · `_common/thong-bao-ja.md`

---

##### `[DEV TASK]` E08-07-FE-02 — Soft-block repeated judgement recording

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Nút `判定結果を記録` bấm được **vô hạn lần**, mỗi lần một dòng bằng chứng. **Mười dòng
  `引当不可` giống hệt nhau không phải bằng chứng — nó là nhiễu**, và người kiểm toán phải mất
  công phân biệt "thử lại" với "tình huống đã đổi"
- Wireframe 8.1 đã quyết **chặn mềm**; code chưa dựng. **Spec đã định nghĩa xong giao diện và
  nhãn** (S29): sau lần ghi đầu, nút chuyển sang `記録済み（HH:MM）`
- ⚠ **Không** thêm mã chống gửi trùng kiểu `client_request_id` — bản chất của bảng bằng chứng là
  ghi mọi lần bấm; cái cần chặn là **thao tác lặp vô ích**, không phải ghi trùng
- **AC-21-68** — Given vừa ghi run `引当不可` · When bấm lại · Then hôm nay sinh dòng thứ hai
- **AC-21-69** — Given sau khi dựng quyết định 8.1 · When bấm lần thứ hai · Then nút đã ở trạng
  thái `記録済み…`

**Impact Range**
- Khối ❸ của SCR-21 · `allocation_runs`

---

##### `[DEV TASK]` E08-07-FE-03 — Add a delivery-date filter to the allocation list

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Danh sách **không có bộ lọc nào**. Tham số `date` **đã tồn tại ở API** nhưng màn không gửi
- Wireframe 8.4 đã quyết: **không phân trang**, thêm **lọc theo `納品希望日`** — khác SCR-20 và
  SCR-18, hai màn kia đều phân trang
- Rỗng thì không gửi tham số (giữ nguyên hành vi hôm nay). Không khớp dòng nào thì hiện `M_78` thể
  `条件に一致する受注はありません` — **khác** câu khi danh sách vốn rỗng
- **AC-21-12** — Given không đơn nào ở ba trạng thái · Then câu "không có đơn", **không** phải câu
  "không khớp điều kiện lọc"

**Impact Range**
- Danh sách SCR-21 · `OLQ:35, 79` · `_common/thong-bao-ja.md` (`M_78`)

---

##### `[DEV TASK]` E08-07-FE-04 — Read fields.reason in the release-allocation dialog

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Route trả `fields.reason = ["引当解除の理由を入力してください"]`, nhưng hộp Gỡ phân bổ **không
  đọc `fields`** — chỉ phân nhánh theo 409, mọi mã khác về câu chung `引当解除できませんでした`
- **Chỗ duy nhất của màn có `detail.fields` mà không dùng**; để nguyên thì tầng dưới làm đúng việc
  mà tầng trên vứt đi
- **AC-21-78** — Given ô `理由` trống hoặc chỉ khoảng trắng · When bấm · Then câu gắn **đúng ô**
- **AC-21-85** — Given lý do dài hơn 500 ký tự qua API · Then **422** `validation_failed`

**Impact Range**
- `REL:27` · `RREL:10`

---

##### `[DEV TASK]` E08-07-FE-05 — Fix the two comments that claim six evaluation steps

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- **Hai comment nói "6 bước"** — `RPREV:6` và `DETAIL:15` — trong khi code có **năm**:
  `EXCLUSION_STEPS` 5 phần tử, mô tả trang ghi ①〜⑤, `EVID:4` ghi *"five checks"*
- **Không có bước thứ sáu ở đâu cả.** Một dòng mỗi chỗ, nhưng để nguyên thì người đọc code sau
  **sẽ đi tìm một bước không tồn tại**
- **AC-21-99** — Given mã nguồn của màn · When đọc hai comment · Then chúng nói **"5 bước"**

**Impact Range**
- `RPREV:6` · `DETAIL:15`

---

#### `[STORY]` US-08 — Allocation refuses expiry inversion and honours the contract delivery window

**Overview**
- **Who:** `配送計画者`, và khách ở đầu ra
- **What:** bước ④ áp quy tắc cửa sổ giao theo hợp đồng, bước ⑤ cấm giao hàng có hạn sớm hơn lần
  giao đã nhận gần nhất
- **Why:** FR-OUT-02 / BR-EXP-02 (P0) — đảo hạn là lỗi khách phát hiện được ngay khi nhận hàng

**Acceptance Criteria**
- **AC-21-33** — Given hợp đồng `ONE_HALF`, lô sản xuất `2026-09-01` hạn `2026-09-20`, giao
  `2026-09-15` · When phán định · Then kết quả đúng theo công thức một nửa
- **AC-21-34** / **AC-21-35** — Given hợp đồng `ONE_THIRD` · Then giao `2026-10-20` đạt, giao
  `2026-10-21` bị `除外 ④ 配送ウィンドウ` — **biên một ngày**
- **AC-21-36** / **AC-21-37** — Given `LABEL_DATE_ONLY` · Then hạn **bằng đúng** ngày giao thì đạt;
  hạn **sau** một ngày thì khác
- **AC-21-38** / **AC-21-39** / **AC-21-40** — Given hợp đồng không có quy tắc, hoặc không có dòng
  hợp đồng nào · Then kết cục là `業務判断`, **không lô nào bị loại ở bước ④**
- **AC-21-41** / **AC-21-42** — Given khách đã nhận hạn `2026-09-20` · When phán định lô hạn sớm
  hơn · Then bị loại ở bước ⑤; khách **không có** lịch sử thì **ĐẠT**
- **AC-21-43** — Given `CUS-003 × CHI-002` · When đọc mốc bước ⑤ · Then mốc là lần giao đã nhận
  gần nhất, **không** phải lần giao gần nhất bất kỳ
- **AC-21-44** — Given lô có hạn **bằng đúng** hạn của lần giao đã nhận gần nhất · Then **ĐẠT**
- **AC-21-45** — Given hai dòng `delivery_history` cùng `delivered_at` với hạn khác nhau · Then
  mốc là hạn **lớn nhất** — xem `E08-INV-06`
- **AC-21-47** — Given lô `賞味期限` đã quá hạn so với ngày giao · Then lô **qua** bước — hạn dùng
  tốt nhất chỉ để **cảnh báo**
- **AC-21-48** / **AC-21-49** / **AC-21-50** — badge cảnh báo **không** làm lô bị loại

**References & Dependencies**
- Spec: SCR-21 §6.4.5 · §6.4.6 · §6.4.7 · BR-EXP-02 (tr.25)

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E08-08-BE — Make the five-step chain enforce what the preview promised

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `RPC / luật`

**Impact Range**
- `allocate_order` · `delivery_history` · `lib/rules/`

---

##### `[DEV TASK]` E08-08-BE-01 — Re-check steps ②④⑤ inside allocate_order

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `allocate_order` **chỉ kiểm lại** trạng thái đơn, trạng thái lô, bước ①, tồn khả dụng và tổng
  plan. Nó **không kiểm** bước ②, ④, ⑤ và **không kiểm thứ tự FEFO** — nó **tin plan do route tính**
- Hai bộ luật, hai ngôn ngữ: ②④⑤ ở TypeScript, ① ở SQL. Chỉ an toàn vì EXECUTE của hàm **chỉ cấp
  cho `service_role`**
- Hai đường: **(a)** kiểm lại ②④⑤ trong SQL · **(b)** giữ nguyên **và viết thành quyết định có văn
  bản**, kèm một dòng trong tài liệu vận hành: *ai cầm khoá `service_role` thì bỏ qua được ba bước*
- Liên quan `AC-21-18` (bề mặt tin cậy): `p_actor_id` do route truyền, **không** từ JWT
- `[tự viết]` Given plan bị sửa tay để chứa một lô trượt bước ⑤ · When gọi thẳng RPC bằng
  `service_role` · Then (a) bị từ chối, hoặc (b) đi qua và hành vi đó đã được ghi thành văn bản

**Impact Range**
- `allocate_order` · `A3:169-178` · tài liệu bảo mật

---

##### `[DEV TASK]` E08-08-BE-02 — Settle the multi-lot delivery history assumption

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E08-INV-06`

**Specification**
- Q54 hỏi *"dòng lịch sử giao gần nhất không có ngày hết hạn thì xử lý thế nào"*, giả định ghi
  *"bỏ qua, so với dòng có hạn trước đó"*
- **Ca đó không dựng được**: `delivery_history.expiry_date` là `not null`, nên **không có dòng nào
  thiếu hạn để mà bỏ qua**
- Đổi lại, code mang **một giả định khác, rộng hơn**: nhiều lô trong cùng một lần giao → lấy
  **hạn lớn nhất**. `CONV:93` tự nhận đây là giả định chưa xác nhận
- **AC-21-45** nghiệm thu đúng giả định đang cài
- Việc của LAB-5: hỏi khách **giả định đang cài**, không phải giả định đã ghi trong Q54

**Impact Range**
- `REV:27-31` · `delivery_history`

---

#### `[PARENT][FE]` E08-08-FE — Raise best-before expiry from a small badge to a real warning

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Impact Range**
- Bảng phán định của SCR-21

---

##### `[DEV TASK]` E08-08-FE-01 — Raise the expired best-before lot to a visible warning level

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Luật **đúng**: lô `賞味期限切れ` **vẫn vào plan được** nếu bước ④ cho qua. Nhưng trên màn nó chỉ
  là **một badge vàng nhỏ** trong ô `期限`, **cùng cỡ với `賞味期限接近`**
- Chỗ hở là **mức hiển thị**, không phải mức luật — người dùng phân bổ hàng quá hạn dùng tốt nhất
  mà không nhận ra mình vừa làm gì
- Quyết định wireframe 8.3, spec đã định nghĩa xong mức hiển thị mới
- **AC-21-47** vẫn đúng — lô **qua** bước, không bị loại
- **AC-21-50** vẫn đúng — badge cảnh báo **không** làm lô bị loại

**Impact Range**
- Ô `期限` của bảng phán định SCR-21

---

#### `[INVESTIGATION]` E08-INV-01 — Confirm Q9: which evidence set each delivery term requires

**Overview**
- Hỏi khách: mỗi điều kiện `車上渡し` / `軒先渡し` cần **bộ bằng chứng nào** (chữ ký, ảnh, vị trí,
  bằng chứng dỡ hàng); trách nhiệm dỡ hàng và trách nhiệm nhiệt độ thuộc về ai; **điểm chuyển giao
  trách nhiệm** nằm ở đâu
- RFP Hình 15 tr.28 ghi 「theo điều kiện hợp đồng」 ở **cả ba cột** — tức là không nói gì
- `配送条件` chọn ở SCR-20 **khoá cứng** bộ bằng chứng ở SCR-26
- **Mức đổi:** Lớn — chạm cả SCR-20 và **E09** (SCR-26)

**References**
- SCR-20 §6.3 #1 · `AC-20-43` · `AC-20-44`

---

#### `[INVESTIGATION]` E08-INV-02 — Confirm Q31: how an order changed after 16:00 is handled

**Overview**
- **Không có đường sửa, không có đường huỷ đơn** ở SCR-20 (wireframe 7.3 quyết giữ nguyên)
- ⚠ `orders` **không phải bảng append-only** — một nút sửa đặt vào sẽ **ghi đè im lặng**, trong
  khi `events` chỉ ghi được chuyển trạng thái, **không** ghi được "ai sửa gì" (`AC-20-63`)
- **Giả định vendor:** *"Huỷ phân bổ + phân bổ lại, giữ nhật ký"*
- Làm thật cần: luồng sửa **có vết** (ai sửa, sửa trường nào, lúc nào)
- ⚠ Tình huống của Q31 hôm nay **không có đường thực hiện nào** trong prototype

**References**
- SCR-20 §6.3 #2 · SCR-21 §6.3 #22 · `client-qa-list.md:46`

---

#### `[INVESTIGATION]` E08-INV-03 — Confirm which role registers orders — dispatcher or sales

**Overview**
- **US-06 ghi vai đăng ký là `営業担当者`** (nhân viên kinh doanh); triển khai là `配送計画者`.
  Comment code nói thẳng: *"phase scope v6; US-06 says Nhân viên kinh doanh"*
- US-06 tự ghi chú *"bảng vai trò tr.7 không ghi ai nhập đơn"* — vai Nhân viên kinh doanh là
  **suy đoán của LAB-1**, không phải khách nêu
- **Mức đổi:** khách chốt Nhân viên kinh doanh → phải thêm **vai thứ tám** vào hệ, chạm RLS, menu,
  và cả bảy màn đang kiểm vai

**References**
- SCR-20 §6.3 #7 · `SQL:100` · `conventions:88`

---

#### `[INVESTIGATION]` E08-INV-04 — Confirm Q65 and Q30: partial allocation and multi-lot order lines

**Overview**
- **Q65** *"thiếu tồn thì phân bổ một phần hay từ chối cả dòng"* — **giả định: từ chối cả dòng**
- **Q30** *"một dòng đơn có được lấy từ nhiều lô không"* — **giả định: có, tách nhiều lô**
- RFP chỉ có chữ `原子的アロケーション` (tr.30), **không nói khi thiếu hàng**
- **Mức đổi Q65:** cho phân bổ một phần → **thêm trạng thái đơn** và đổi cả chuỗi sau đó

**References**
- SCR-21 §6.3 #20 · `CONV:59-60` · `R-24` `R-25`

---

#### `[INVESTIGATION]` E08-INV-05 — Confirm Q47: who handles business-review rows and how

**Overview**
- Hỏi khách: *"dòng business-review do ai xử lý, bằng cách nào — màn hình trong hệ thống hay xuất
  danh sách để nghiệp vụ ký"*
- **Giả định vendor:** *"xuất danh sách để nghiệp vụ ký"*
- Hôm nay màn **ghi một run `業務判断` rồi dừng**: không hàng chờ xử lý, không danh sách xuất ra,
  không màn nào gom các đơn đang ở trạng thái đó. Đơn vẫn `検証済` và **nằm lại trong danh sách y
  như trước khi bấm**
- **Mức đổi:** khách muốn màn xử lý trong hệ → **một màn mới**, ngoài 15 màn

**References**
- SCR-21 §6.3 #21 · `client-qa-list.md:52` · `AC-21-64` · `AC-21-65`

---

#### `[INVESTIGATION]` E08-INV-06 — Confirm Q54: delivery history rows without an expiry date

**Overview**
- Q54 hỏi về dòng lịch sử giao **không có hạn** — nhưng ca đó **không dựng được**,
  `delivery_history.expiry_date` là `not null`
- Câu **thật sự cần hỏi** là giả định code đang mang: nhiều lô trong cùng một lần giao → lấy
  **hạn lớn nhất**. `CONV:93` tự nhận đây là giả định chưa xác nhận
- ⚠ Đây là ca **câu hỏi đã gửi khách sai trọng tâm** — phải gửi lại câu đúng

**References**
- SCR-21 §6.3 #6 · `REV:27-31` · `CONV:93` · `client-qa-list.md:80`

---

### E09 · Lấy hàng → xuất hàng → POD

| | |
|---|---|
| **Màn** | SCR-23 (16 dòng) · SCR-24 (21 dòng) · SCR-26 (23 dòng) — **60 dòng 6.3** |
| **Nhóm LAB-1 đối chiếu** | F05 (nằm trong 215 SP / 122 MD của F04+F05) |
| **Số item** | 1 epic + 4 story + 8 parent + 21 dev task + 4 investigation = **38** |

⚠ **Nhiều dòng 6.3 nhất trong 15 màn.** Ba màn nối thành một chuỗi: lấy hàng → xuất hàng → giao
hàng. Một lỗi ở đầu chuỗi đi hết tới cuối mà không ai chặn lại.

```
[EPIC] E09 Close the evidence gaps along the pick → dispatch → POD chain
├── [STORY] US-09 Center worker picks and loads with an evidence row for every attempt
│   ├── [PARENT][BE] E09-09-BE Make pick and load enforce what the UI already hides
│   │   ├── E09-09-BE-01 Reject closed storage locations inside confirm_pick
│   │   ├── E09-09-BE-02 Add the quantity ceiling that only zod enforces
│   │   ├── E09-09-BE-03 Narrow the exception handler that swallows every P0001
│   │   └── E09-09-BE-04 Write a movements row when confirm_pick removes stock
│   └── [PARENT][FE] E09-09-FE Show the operator the limits and the history before they submit
│       ├── E09-09-FE-01 Mirror the four server-side limits in the browser
│       ├── E09-09-FE-02 Surface the loading_checks history on the order card
│       ├── E09-09-FE-03 Mark the six mandatory fields as required
│       └── E09-09-FE-04 Unify the three messages for the empty-pick-line case
├── [STORY] US-10 Pre-dispatch checks record readings atomically and block with the right reason
│   ├── [PARENT][BE] E09-10-BE Make the pre-dispatch gate atomic and its evidence complete
│   │   ├── E09-10-BE-01 Accept both driver readings in one atomic request
│   │   ├── E09-10-BE-02 Add a staleness bound to pre-dispatch readings
│   │   └── E09-10-BE-03 Document or align the two expiry reference dates
│   └── [PARENT][FE] E09-10-FE Make the dispatch screen stop contradicting itself
│       ├── E09-10-FE-01 Replace the three wrong fallback messages with the right ones
│       ├── E09-10-FE-02 Distinguish a reused deviation from a newly opened one
│       ├── E09-10-FE-03 Hide the best-before notice while the order is blocked
│       ├── E09-10-FE-04 Show the full reading history instead of only the latest
│       └── E09-10-FE-05 Warn on silent decimal rounding of temperature input
├── [STORY] US-11 Driver completes proof of delivery with the evidence the contract requires
│   ├── [PARENT][BE] E09-11-BE Close the POD validation gaps and give POD a correction path
│   │   ├── E09-11-BE-01 Enforce the photo count and four length limits inside complete_pod
│   │   ├── E09-11-BE-02 Check the photo payload before the evidence gate
│   │   ├── E09-11-BE-03 Add a POD supersedes chain so a wrong POD can be corrected
│   │   └── E09-11-BE-04 Record delivery history even when the allocation was released
│   └── [PARENT][FE] E09-11-FE Make POD feedback precise and the evidence reviewable
│       ├── E09-11-FE-01 Map the deliveredAt boundary errors onto the time field
│       ├── E09-11-FE-02 Show uploaded POD photos back to the driver after submit
│       ├── E09-11-FE-03 Route photo uploads through apiFetch
│       ├── E09-11-FE-04 Warn that the rejection exception code has downstream effects
│       └── E09-11-FE-05 Make the allocated-lot table scrollable on a phone
└── [STORY] US-27 Center worker groups picking tasks by zone, route and load order
    ├── [PARENT][BE] E09-27-BE Build the picking task grouping the RFP asks for
    │   └── E09-27-BE-01 Build picking task grouping by zone, route and load order
    └── [PARENT][FE] E09-27-FE Present picking tasks in the grouped order
        └── E09-27-FE-01 Render the picking queue grouped by zone, route and load order
[INVESTIGATION] E09-INV-01 Confirm what happens when a picked lot is quarantined before departure
[INVESTIGATION] E09-INV-02 Confirm Q66 — who records pre-dispatch checks and who confirms loading
[INVESTIGATION] E09-INV-03 Confirm Q64 — is a printed dispatch slip required
[INVESTIGATION] E09-INV-05 Confirm whether POD location must be real coordinates
```

---

#### `[EPIC]` E09 — Close the evidence gaps along the pick → dispatch → POD chain

**Overview & Goal**
- As a `センター作業者` (*"Nhân viên trung tâm"*) và `ドライバー` (*"Tài xế"*)
- I want mỗi bước của chuỗi xuất hàng để lại bằng chứng đầy đủ và báo đúng lý do khi bị chặn
- So that khi khách khiếu nại, hệ dựng lại được **ai làm gì, lúc nào, vì sao bị chặn**

**Scope & Features**
- Bịt các chỗ **UI che mà máy chủ không chặn** (vị trí đã dừng dùng, trần số lượng, trần ảnh)
- Gửi **nguyên tử** hai số đo của tài xế — hôm nay gửi tuần tự, một ô hỏng thì ô kia **vẫn đã ghi**
- Sửa các câu thông báo **nói sai việc**: trạng thái không đổi mà báo "trạng thái đã thay đổi"
- Đường sửa POD sai — hôm nay **không có đường nào cả**
- Ghi `movements` khi hàng rời vị trí — mắt xích truy vết đang mất

**Ngoài phạm vi**
- Bộ bằng chứng theo `配送条件` cần khách chốt → `E09-INV-...` và **E08-INV-01** (cùng Q9)
- Hàng đợi POD ngoại tuyến 8 giờ (**US-11 AC3**) — **M5 là mock**, thuộc **E13**
- Mức severity của Sai lệch → **E10** · SCR-15 Dịch chuyển tồn (**US-04**) — **ngoài 15 màn**

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-23-64** · **AC-24-25** · **AC-26-26** vẫn đúng — Given dòng `loading_checks` /
  `pre_dispatch_readings` / `pods` · When thử `UPDATE`/`DELETE` · Then bị trigger append-only chặn
- **AC-23-69** đảo chiều — Given một lượt lấy hàng thành công · When đếm dòng `movements` ·
  Then có dòng (hôm nay: **0 dòng**)

**References & Dependencies**
- Spec: `scr-23-lay-hang-boc-xep.md` · `scr-24-kiem-truoc-xuat.md` · `scr-26-pod.md`, §6.3 và §6.4
- Phụ thuộc **E08** (lần phân bổ hiệu lực) · ảnh hưởng **E11** (SCR-35 đọc `pods`)

---

#### `[STORY]` US-09 — Center worker picks and loads with an evidence row for every attempt

**Overview**
- **Who:** `センター作業者`
- **What:** nhập dòng lấy hàng theo lô và vị trí, rồi xác nhận chất lên xe
- **Why:** FR-OUT-04 (P0) — mỗi lần xác nhận, kể cả bị chặn, phải để lại một dòng bằng chứng

**Acceptance Criteria**
- **AC-23-23**…**AC-23-26** — Given đơn `引当済` với hai dòng phân bổ · When nhập đúng rồi gửi ·
  Then tồn giảm đúng, **đúng một** dòng `loading_checks`, `orders.status` chuyển sang `picked`
- **AC-23-35**…**AC-23-43** — sáu lý do chặn, mỗi lý do một câu riêng gắn đúng dòng
- **AC-23-44** — Given hai dòng cùng sai theo **hai kiểu khác nhau** · When gửi **một** lần ·
  Then cả hai dòng hiện lý do của riêng nó
- **AC-23-45** — Given lượt gửi bị chặn vì bất kỳ lý do nào · When kiểm DB · Then có **đúng một**
  dòng `loading_checks` ghi lại lần chặn đó
- **AC-23-47** — Given đơn đã bị chặn ba lần · Then có **ba** dòng — mỗi lần một dòng
- **AC-23-46** — Given lượt gửi bị chặn · Then `orders.status` **không đổi**, tồn **không đổi**
- **AC-23-49**…**AC-23-52** — chất hàng thành công: `vehicle_id` và `seal_no` được ghi, đơn **biến
  khỏi** `/loading`
- **AC-23-53** — Given SKU `冷蔵` và xe `冷凍` · When bấm `積込確認` · Then bị chặn vì
  `temp_zone_mismatch`
- **AC-23-55** — Given `confirm_load` trong mọi ca · Then **không** mã nào ngoài
  `temp_zone_mismatch` xuất hiện trong `block_reasons`
- **AC-23-63** — Given bất kỳ ca 403/404/409/422 nhóm ① nào · Then **không** dòng mới nào
- **AC-23-73** đảo chiều — Given sáu ô nhập · Then mỗi nhãn kèm chữ `必須` (hôm nay: không ô nào có)

**References & Dependencies**
- Spec: SCR-23 §6.4.4…§6.4.10

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E09-09-BE — Make pick and load enforce what the UI already hides

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `RPC / luật` + `DB (migration)`

**Impact Range**
- `confirm_pick` · `confirm_load` · `movements` · `loading_checks`

---

##### `[DEV TASK]` E09-09-BE-01 — Reject closed storage locations inside confirm_pick

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- UI lọc bỏ vị trí `is_closed` khỏi dropdown, nhưng `confirm_pick` **không kiểm** — gọi thẳng API
  với một vị trí đã dừng dùng **vẫn qua** nếu còn tồn (`R-12`)
- **Ẩn ở giao diện là che, không phải chặn.** Một vị trí bị dừng dùng có lý do vận hành của nó
- Wireframe 7.3 đã chốt: **giữ dropdown đã lọc, thêm phép chặn ở RPC**
- **AC-23-68** đảo chiều — Given vị trí `is_closed = true` còn tồn · When gọi thẳng API · Then
  bị chặn (hôm nay: qua được)
- **AC-23-15** vẫn đúng — dropdown không liệt vị trí đã đóng

**Impact Range**
- `confirm_pick` · `locations.is_closed`

---

##### `[DEV TASK]` E09-09-BE-02 — Add the quantity ceiling that only zod enforces

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Gọi thẳng RPC với `qty > 2^31` cho Postgres `22003`; mã này **không nằm trong ba mã Postgres
  thuần** của bảng ánh xạ → **500 `internal_error`**, và **không có dòng `loading_checks` nào**
- Tức là một lần thử bị hỏng **không để lại bằng chứng** — trái với cả thiết kế của màn
- zod chặn ở trần 1.000.000 nhưng RPC **không có trần nào**; cột `qty` là `integer`
- Thêm trần `qty` vào `confirm_pick`, **trước vòng lặp**
- **AC-23-67** đảo chiều — Given `qty > 2^31` · When gọi thẳng RPC · Then 422 có mã riêng và **có**
  dòng bằng chứng (hôm nay: 500, không dòng nào)
- Cùng họ lỗi với `E06-01-BE-01` · `E07-05-BE-02` · `E08-06-BE-01` — **bốn màn, một họ**

**Impact Range**
- `confirm_pick` · `loading_checks`

---

##### `[DEV TASK]` E09-09-BE-03 — Narrow the exception handler that swallows every P0001

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `exception when raise_exception` bắt **mọi** `P0001` phát sinh trong vùng trừ tồn, không chỉ
  `PICK_STOCK_UNAVAILABLE`. Một trigger thêm vào sau này mà raise `P0001` cũng sẽ ra
  `保管場所の在庫不足` — **nói sai nguyên nhân**
- Khối bắt theo **loại lỗi**, không theo **mã** → đặt `errcode` riêng và bắt theo mã đó
- **AC-23-65** / **AC-23-66** — Given lượt lấy hàng qua hết sáu phép kiểm nhưng tồn bị người khác
  lấy mất · Then ra lý do `insufficient_stock`, và chuỗi `PICK_STOCK_UNAVAILABLE` **không** xuất
  hiện trong phản hồi HTTP
- `[tự viết]` Given một `P0001` khác phát sinh trong vùng đó · When chạy · Then **không** bị gán
  nhầm thành thiếu tồn

**Impact Range**
- `M3B:198` · `confirm_pick`

---

##### `[DEV TASK]` E09-09-BE-04 — Write a movements row when confirm_pick removes stock

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `confirm_pick` trừ `inventory_balances` và `lot_state` nhưng **không ghi dòng `movements` nào`** —
  bảng **tồn tại, append-only, chưa có RPC nào ghi**
- **Hàng rời vị trí mà không có dòng dịch chuyển** → mất một mắt xích truy vết
- Gốc: SCR-15 Dịch chuyển tồn bị cắt ở phase 04a, và `confirm_pick` **không được giao việc** ghi
  `movements`
- **AC-23-69** đảo chiều — Given lượt lấy hàng thành công · When đếm dòng `movements` của lô ·
  Then có dòng (hôm nay: **0**)
- Nằm trong 7 mục *"cái KHÔNG có trong code"* của `01-architecture.md` §12

**Impact Range**
- `movements` · `confirm_pick` · SCR-35 (E11)

---

#### `[PARENT][FE]` E09-09-FE — Show the operator the limits and the history before they submit

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `PF` · `LF` · thẻ đơn SCR-23

---

##### `[DEV TASK]` E09-09-FE-01 — Mirror the four server-side limits in the browser

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Bốn trần `50 dòng` · `ロット番号 ≤ 50` · `数量 ≤ 1.000.000` · `シール番号 ≤ 100` **chỉ sống ở
  máy chủ** (`R-19`)
- Người thao tác thêm dòng thứ 51, gửi đi, nhận về `入力内容を確認してください` — **mất cả lượt
  nhập mà không biết sai ở đâu**
- **AC-23-70** đảo chiều — Given gửi 51 dòng · When bấm nút · Then bị chặn ngay ở trình duyệt
  (hôm nay: request vẫn gửi đi)

**Impact Range**
- `PF` · `LF` · schema zod phía trình duyệt

---

##### `[DEV TASK]` E09-09-FE-02 — Surface the loading_checks history on the order card

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Mọi lần bị chặn đều được ghi vào `loading_checks` nhưng **không màn nào đọc bảng đó** — grep
  trong `app/` và `components/` ra **0 hit**. **Người làm ca sau không biết ca trước đã vướng gì**
- Wireframe 7.4 đã quyết dựng lịch sử trên thẻ đơn
- **AC-23-74** — Given đơn chưa từng bị chặn · Then **không** dòng lịch sử nào trên thẻ
- **AC-23-75** — Given đơn đã bị chặn hai lần, lần gần nhất vì `qty_mismatch` · Then hiện một dòng
  tóm tắt
- **AC-23-76** — Given bấm `詳細を表示` · Then hiện bảng `確認履歴`
- **AC-23-77** — Given vai `センター作業者` · When đường đọc `loading_checks` được gọi · Then đọc được

**Impact Range**
- Thẻ đơn SCR-23 · `loading_checks` · endpoint đọc mới

---

##### `[DEV TASK]` E09-09-FE-03 — Mark the six mandatory fields as required

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Sáu ô của màn đều bắt buộc nhưng **không ô nào có nhãn `必須`** — hai form không truyền
  `required` cho `TextField`/`SelectField`, trong khi SCR-12 thì có
- `TF:21` và `SF:25` **chỉ vẽ nhãn khi nhận `required`** — đây là thiếu sót của **chỗ gọi**, không
  phải của component
- **AC-23-73** — Given sáu ô nhập · Then mỗi nhãn kèm chữ `必須` màu đỏ
- Đây là việc **trợ năng**, không chỉ thẩm mỹ

**Impact Range**
- `PF:124-126` · `LF:72-79`

---

##### `[DEV TASK]` E09-09-FE-04 — Unify the three messages for the empty-pick-line case

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **Ba lớp kiểm nói ba kiểu về cùng một việc**, và lớp trong cùng **không tới được người dùng**:
  client `ピッキング行を1行以上入力してください` ⟷ zod `ピッキング明細を1行以上入力してください`
  ⟷ RPC (không tới nơi)
- Cộng: màn không phân biệt **500** với **422** — `failureMessage` chỉ có nhánh cho 0/403/404/409.
  Hàm này **dùng chung cho SCR-23 và SCR-24**, nên sửa một lần được cả hai
- **AC-23-31** — Given mọi dòng đã bị xoá hết · When bấm `ピッキング確認` · Then một câu duy nhất
- **AC-23-71** — Given HTTP ≥ 500 · Then `M_53`
- **AC-23-48** — Given mã reason không có trong bảng nhãn · Then màn vẫn hiện được, không vỡ
- Cộng: `CONFLICT_NO_EFFECTIVE_ALLOCATION` đang dùng chung câu 409 *"trạng thái đơn đã thay đổi"*
  trong khi **trạng thái vẫn đúng** — thứ thiếu là lần phân bổ hiệu lực (`AC-23-72`)

**Impact Range**
- `PF:78` · `SL:55-61` · `_common/thong-bao-ja.md`

---

#### `[STORY]` US-10 — Pre-dispatch checks record readings atomically and block with the right reason

**Overview**
- **Who:** `センター作業者` ghi nhiệt hàng, `ドライバー` ghi seal và nhiệt xe
- **What:** ghi ba số đo rồi xác nhận xuất hàng; giá trị ngoài chính sách thì mở Sai lệch và chặn
- **Why:** FR-OUT-05 (P0) — đây là **cổng cuối** trước khi hàng rời kho

**Acceptance Criteria**
- **AC-24-21**…**AC-24-24** — ghi số đo: **đúng một** dòng mới mỗi lần; ghi lần hai cùng loại thì
  có **hai** dòng, không ghi đè
- **AC-24-29** — Given nhiệt độ `-60` hoặc `60` · Then **200** — biên **nằm trong** dải
- **AC-24-32**…**AC-24-35** — phân vai theo loại số đo, cưỡng chế ở **ba tầng**, ba bản đồ vai
  **phải khớp nhau**
- **AC-24-37** / **AC-24-38** — xuất hàng thành công: `orders.status = dispatched`, có sự kiện
  `order.dispatched`
- **AC-24-43**…**AC-24-49** — bốn lý do chặn, biên `5.00` đạt / `5.01` chặn, seal so **không phân
  biệt hoa thường sau khi cắt trắng**, hai lý do cùng đúng thì **cả hai** nhãn hiện
- **AC-24-50** — Given đơn bị chặn · Then `orders.status` **vẫn là** `loaded`
- **AC-24-51**…**AC-24-58** — Sai lệch: mở mới lần đầu, **tái dùng** lần sau, và ca chặn **chỉ vì**
  `use_by_expired` thì **không** mở Sai lệch nào
- **AC-24-65** — Given bất kỳ ca 403/404/409/422 nào · Then không dòng mới nào
- **AC-24-72** / **AC-24-73** — Given tài xế điền cả hai ô · When gửi · Then **một** yêu cầu nguyên
  tử; một ô sai thì **không** dòng nào được ghi

**References & Dependencies**
- Spec: SCR-24 §6.4.4…§6.4.11

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E09-10-BE — Make the pre-dispatch gate atomic and its evidence complete

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `RPC / luật` + `API route`

**Impact Range**
- `record_pre_dispatch_reading` · `confirm_dispatch` · `pre_dispatch_readings`

---

##### `[DEV TASK]` E09-10-BE-01 — Accept both driver readings in one atomic request

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` + `RPC / luật`

**Specification**
- Hai ô của tài xế gửi **tuần tự, không nguyên tử**. **Một ô hỏng thì ô kia vẫn đã ghi**, và bảng
  append-only nên gửi lại **sinh dòng thừa**
- **Spec đã định nghĩa xong hợp đồng** (mục 5.2.3): một yêu cầu mang mảng `[{kind, value}, …]`
- **AC-24-26** đảo chiều — Given tài xế điền cả hai ô rồi bấm `記録` · Then **một** request
  (hôm nay: **hai**)
- **AC-24-72** — Given gửi gộp · Then cả hai số đo ghi trong một giao dịch
- **AC-24-73** — Given lần gửi gộp bị từ chối vì một ô sai · Then **không** dòng
  `pre_dispatch_readings` nào

**Impact Range**
- `app/api/orders/{id}/pre-dispatch-readings/` · `record_pre_dispatch_reading` · `FORM:56-61`

---

##### `[DEV TASK]` E09-10-BE-02 — Add a staleness bound to pre-dispatch readings

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- ⚠ **Điểm mù:** không kiểm số đo được ghi **sau thời điểm xếp xe**, không kiểm **tuổi** số đo
  (`R-34`). Một `出発時車両温度` ghi **từ hôm trước** vẫn tính là hợp lệ
- Nghiệp vụ muốn *"số đo ngay trước khi xe chạy"* thì phải có mốc so — mốc rẻ nhất đã có sẵn là
  thời điểm `confirm_load`
- `[tự viết]` Given số đo ghi trước thời điểm `confirm_load` của đơn · When bấm `出荷確認` ·
  Then số đo đó **không** được tính là hợp lệ
- ⚠ Đây là chỗ **spec nêu nhưng chưa chốt ngưỡng tuổi** — phải chốt trước khi code

**Impact Range**
- `confirm_dispatch` · `pre_dispatch_readings` · `loading_checks`

---

##### `[DEV TASK]` E09-10-BE-03 — Document or align the two expiry reference dates

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- SCR-24 xét `消費期限` theo **hôm nay (JST)**; SCR-21 xét cùng loại hạn theo **`orders.requested_date`**
- **Có thể là cố ý** — phân bổ nhìn tới ngày giao, xuất hàng nhìn ngày đang đứng — nhưng **không
  có dòng nào trong code nói vậy**
- Chọn một: viết thành quyết định có văn bản, **hoặc** thống nhất hai mốc
- **AC-24-48** — Given lô `消費期限` có hạn **đúng bằng hôm nay (JST)** · When bấm · Then kết quả
  theo mốc đã chốt
- **AC-24-19** — Given lô hạn `<=` hôm nay · Then cột `判定` hiện đúng phán định

**Impact Range**
- `M2:29` · `confirm_dispatch` · tài liệu quyết định

---

#### `[PARENT][FE]` E09-10-FE — Make the dispatch screen stop contradicting itself

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 5 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `BTN:90` · `BTN:93` · `LABELS:59` · `OSD:79-85`

---

##### `[DEV TASK]` E09-10-FE-01 — Replace the three wrong fallback messages with the right ones

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **Ba mã nghiệp vụ rơi vào câu dự phòng sai ngữ nghĩa:**
  - `CONFLICT_NO_VEHICLE` và `CONFLICT_NO_EFFECTIVE_ALLOCATION` hiện *"trạng thái đơn đã thay đổi"*
    — **trạng thái không đổi**
  - `RULE_NO_TEMPERATURE_THRESHOLD` hiện câu của một việc khác
- Cộng `conflict_concurrent_update` cũng rơi vào câu 409 chung — **nói sai việc**, và còn kéo theo
  **một lần nạp lại danh sách vô ích**
- **AC-24-69** đảo chiều — Given đơn chưa gán xe · When bấm `出荷確認` · Then câu nói **đúng** là
  thiếu xe (hôm nay: *"trạng thái đã thay đổi"*)
- **AC-24-70** — Given HTTP ≥ 500 · Then `M_53`
- **AC-24-62** / **AC-24-63** / **AC-24-64** — ba mã 409 có câu riêng

**Impact Range**
- `LABELS:59` · `_common/thong-bao-ja.md`

---

##### `[DEV TASK]` E09-10-FE-02 — Distinguish a reused deviation from a newly opened one

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Sai lệch **tái dùng** nhưng màn vẫn hiện `逸脱 {code} を記録しました` **y hệt lần mở mới**.
  Payload **không có cờ phân biệt**
- Spec đã định nghĩa xong câu cho hai ca
- **AC-24-54** — Given đã có Sai lệch `pre_dispatch` chưa đóng · When bấm lại · Then **tái dùng**,
  không mở mã mới
- **AC-24-74** — Given lần chặn thứ hai dùng lại Sai lệch đang mở · Then màn nói rõ là **dùng lại**
- **AC-24-57** — Given Sai lệch trước đã `closed` · Then mở **mã mới**

**Impact Range**
- `BTN:90` · `M2:174-204` (thêm cờ vào payload)

---

##### `[DEV TASK]` E09-10-FE-03 — Hide the best-before notice while the order is blocked

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- `警告: 賞味期限切れ（出荷は止まりません）` hiện **cả khi** đơn đang bị chặn vì lý do khác —
  câu *"việc xuất hàng không bị dừng"* đặt **ngay dưới danh sách lý do không xuất được**.
  **Hai câu phủ định nhau cùng một chỗ**
- **AC-24-75** — Given đơn **vừa bị chặn vừa** có lô `賞味期限` quá hạn · Then câu đó **không** hiện
- **AC-24-76** — Given đơn xuất **thành công** mà có lô quá hạn dùng tốt nhất · Then câu đó **hiện**

**Impact Range**
- `BTN:93` · `BLOCK:21`

---

##### `[DEV TASK]` E09-10-FE-04 — Show the full reading history instead of only the latest

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Bảng `記録済みの測定値` chỉ hiện **bản mới nhất** mỗi loại. **Một nhiệt độ ghi lại ba lần trong
  mười phút nhìn y hệt một lần ghi duy nhất** — mất thông tin kiểm toán
- `OQ:68` chọn **mọi** dòng số đo của đơn, nhưng `OSD:79-85` rút còn một dòng mỗi loại **trước khi
  trả ra** → dữ liệu đã có, chỉ bị giấu
- **AC-24-77** — Given `実測貨物温度` đã ghi ba lần · Then có nút mở lịch sử
- **AC-24-78** — Given loại số đo chỉ ghi **một** lần · Then **không** nút mở lịch sử
- **AC-24-79** — Given khối lịch sử được mở · Then **không** request mới nào — dữ liệu đã có sẵn
- Cộng: hai định nghĩa "mới nhất" lệch nhau — DB sắp theo micro-giây, UI theo mili-giây. Hai số đo
  cách nhau **dưới 1 ms** có thể làm màn hiện một giá trị trong khi RPC phán quyết theo giá trị khác

**Impact Range**
- `OSD:79-85` · `M2:80` · bảng `記録済みの測定値`

---

##### `[DEV TASK]` E09-10-FE-05 — Warn on silent decimal rounding of temperature input

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- `3.456℃` gõ vào thì zod nhận, RPC nhận, DB lưu `3.46` (`R-08`). **Không tầng nào báo**
- **Không phải lỗi** — nhiệt kế hiện trường không đọc tới ba chữ số thập phân. Thêm **một dòng
  gợi ý** dưới ô là đủ
- **AC-24-30** — Given `3.456` · When kiểm DB · Then `value_num` là `3.46`, **và** màn đã báo trước

**Impact Range**
- `FORM:79` · ô nhiệt độ của SCR-24

---

#### `[STORY]` US-11 — Driver completes proof of delivery with the evidence the contract requires

**Overview**
- **Who:** `ドライバー`
- **What:** ghi thời điểm, người nhận, chữ ký hoặc ảnh, mã ngoại lệ — theo bộ bằng chứng của
  `配送条件`
- **Why:** FR-OUT-06 (P0) — POD là bằng chứng pháp lý của việc giao hàng

**Acceptance Criteria**
- **AC-26-22**…**AC-26-25** — POD thành công: **đúng một** dòng `pods`, `orders.status = delivered`,
  `events` có **đúng hai** dòng mới, `delivery_history` có đúng số dòng bằng số lô
- **AC-26-26** — Given dòng `pods`/`pod_photos`/`delivery_history` · When thử sửa/xoá · Then bị chặn
- **AC-26-27** — Given đơn đã POD · When gọi lại · Then **409**
- **AC-26-29**…**AC-26-35** — bộ bằng chứng theo `配送条件`: `軒先渡し` cần ảnh hoặc ghi chú chỗ
  đặt hàng; `車上渡し` cần tick `署名確認`; thiếu thì **422** `RULE_POD_EVIDENCE` và **không** dòng
  nào được ghi
- **AC-26-36**…**AC-26-38** — mã ngoại lệ: chỉ `受取拒否` làm `accepted = false`
- **AC-26-16** / **AC-26-17** — Given thân gửi thêm khoá `phone` · Then **422**; bảng `pods`
  **không có cột nào mang nghĩa số điện thoại**
- **AC-26-45** — Given đúng 5 ảnh · Then **200**; 6 đường dẫn gửi thẳng thì bị chặn
- **AC-26-46** — Given đường dẫn ảnh do **tài xế khác** tải lên · Then bị từ chối
- **AC-26-54** — Given hai yêu cầu POD **đồng thời** · Then một **200**, một **409**
- **AC-26-58**…**AC-26-62** — băng tuyến chỉ hiện tuyến `published`, tài khoản không nối `drivers`
  thì **không render gì**

**References & Dependencies**
- Spec: SCR-26 §6.4.3…§6.4.9
- ⚠ Bộ bằng chứng chờ **Q9** — cùng câu hỏi với `E08-INV-01`

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E09-11-BE — Close the POD validation gaps and give POD a correction path

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `RPC / luật` + `DB (migration)`

**Impact Range**
- `complete_pod` · `pods` · `pod_photos` · `delivery_history`

---

##### `[DEV TASK]` E09-11-BE-01 — Enforce the photo count and four length limits inside complete_pod

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Trần **5 ảnh** chỉ có ở zod. RPC **không giới hạn số phần tử** của `p_photo_paths` — chỉ kiểm
  `cardinality = 0`
- Ba trần độ dài chỉ có ở zod: `受取人氏名` ≤ 100, hai ghi chú ≤ 500, `端末ラベル` ≤ 100. RPC chỉ
  `btrim` và kiểm rỗng — grep `char_length` trong thân hàm ra **0 hit**
- `complete_pod` được `grant execute` cho `authenticated` → **gọi thẳng qua PostgREST là bỏ qua zod**
- **AC-26-68** đảo chiều — Given 6 đường dẫn ảnh gửi **thẳng vào RPC** · Then bị từ chối
- **AC-26-69** đảo chiều — Given `受取人氏名` dài 500 ký tự gửi thẳng vào RPC · Then **422**
- **AC-26-19** vẫn đúng — 100 ký tự đạt, 101 thì 422

**Impact Range**
- `complete_pod` (`POD2:176-195`, `POD2:204`)

---

##### `[DEV TASK]` E09-11-BE-02 — Check the photo payload before the evidence gate

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `RULE_POD_EVIDENCE` kiểm **trước** `VALIDATION_POD_PHOTO`. Phép đếm `photo_required` đếm **cả
  đường dẫn chưa xác thực**, nên một đơn `軒先渡し` gửi **một đường dẫn rác** *qua được cổng bằng
  chứng* rồi mới bị 422 ở bước sau
- Người dùng nhận một lỗi khác với lỗi thật — **thứ tự kiểm giấu mất lỗi gốc**
- **AC-26-29** / **AC-26-30** vẫn đúng cho ca thiếu bằng chứng thật
- `[tự viết]` Given đơn `軒先渡し` gửi một đường dẫn ảnh không tồn tại · When gọi · Then lỗi trả về
  là `VALIDATION_POD_PHOTO`, không phải `RULE_POD_EVIDENCE`

**Impact Range**
- `POD2:204` · `POD2:211` · `POD2:224`

---

##### `[DEV TASK]` E09-11-BE-03 — Add a POD supersedes chain so a wrong POD can be corrected

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- **US-11 AC4:** không sửa thẳng bằng chứng POD; **sửa = phiên bản mới liên kết bản cũ**
- Đạt vế thứ nhất (bảng append-only), **không có** vế thứ hai: `pods` không có cột phiên bản và
  `order_id` là **unique** → **POD sai thì không có đường sửa nào cả**
- Comment `TBL:104` tuyên bố cắt đúng vế này
- ⚠ Đây là **P0 chưa phủ**, không phải nợ nhỏ — và là một trong bốn mục `00-pham-vi… §8` ghi là
  *"US-11 AC4 POD không sửa được bằng đường nào"*
- `[tự viết]` Given POD ghi sai người nhận · When ghi bản sửa · Then có dòng `pods` mới trỏ về bản
  cũ, bản cũ **không bị sửa**, và SCR-35 đọc ra bản mới nhất
- Phải bỏ `unique(order_id)` và thay bằng unique theo (đơn, phiên bản)

**Impact Range**
- `pods` (cột phiên bản + supersedes) · `complete_pod` · SCR-35 (E11)

---

##### `[DEV TASK]` E09-11-BE-04 — Record delivery history even when the allocation was released

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Đơn bị `引当解除` sau khi đã `出発済` thì `effective_allocation_run` trả `null` → **0 dòng
  `delivery_history`**, nhưng **POD vẫn hoàn tất** (`R-14`)
- **Hàng đã giao mà không để lại vết nào** cho bước ⑤ của SCR-21 → lần giao đó biến mất khỏi phép
  cấm đảo hạn
- Comment `POD2:254-255` nói rõ lựa chọn: hàng đã giao thật, không được từ chối POD. **Đúng** —
  nhưng hệ quả mất vết thì chưa ai xử
- **AC-26-41** — Given đơn `出発済` mà lần phân bổ đã bị gỡ · When POD hoàn tất · Then hôm nay
  không dòng `delivery_history` nào
- `[tự viết]` Given cùng ca đó · When POD hoàn tất · Then vẫn có vết đủ để bước ⑤ của SCR-21 dùng

**Impact Range**
- `complete_pod` · `delivery_history` · SCR-21 bước ⑤ (E08)

---

#### `[PARENT][FE]` E09-11-FE — Make POD feedback precise and the evidence reviewable

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 5 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `FORM:114-131` · `PUF:38-77` · `LIST:70`

---

##### `[DEV TASK]` E09-11-FE-01 — Map the deliveredAt boundary errors onto the time field

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- `配送時刻` ngoài khoảng W3 trả `VALIDATION_POD_PAYLOAD` với `fields:['deliveredAt']`, và màn hiện
  **câu chung** — **không có manh mối nào** về biên nào bị vi phạm
- Cộng: nhóm 5xx rơi vào câu dự phòng *"vui lòng kiểm tra nội dung đã nhập"* — bảo người dùng đi
  sửa dữ liệu trong khi **lỗi nằm ở máy chủ**
- Cộng: `conflict_concurrent_update` rơi vào câu 409 chung; 404 hiện *"Đã làm mới danh sách"* nhưng
  **danh sách KHÔNG được nạp lại**
- **AC-26-51** / **AC-26-52** — hai biên: tương lai hơn 1 ngày, sớm hơn tạo đơn hơn 1 giờ
- **AC-26-63** — Given ngoài khoảng · Then hiện **câu riêng của đúng biên đó**
- **AC-26-64** — Given 422 của hai biên · When đọc `detail` · Then có khoá phân biệt được biên nào
- **AC-26-67** — Given 5xx · Then `M_53` · **AC-26-57** — Given `40001`/`40P01` · Then câu bận
- **AC-26-71** — Given 404 · Then câu khớp với hành vi thật của màn

**Impact Range**
- `FORM:114-131` · `LABELS:55-61` · `_common/thong-bao-ja.md`

---

##### `[DEV TASK]` E09-11-FE-02 — Show uploaded POD photos back to the driver after submit

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Ảnh **chỉ xem trước cục bộ** trước khi gửi; gửi xong là **không xem lại được** từ màn này.
  Grep `signed-url` và `SignedPhoto` trong `components/pod/` ra **0 hit**
- **Hạ tầng đã có sẵn** (`GET /api/photos/signed-url`) — chỉ thiếu chỗ gọi
- **AC-26-66** — Given đơn `軒先渡し` vừa POD xong có 2 ảnh · When nhìn màn sau khi gửi · Then hai
  ảnh đó **hiện lại**
- **AC-26-70** — Given phản hồi `complete_pod` · When đọc kiểu `PodSubmitResult` · Then kiểu khai
  đủ **6 khoá** kể cả `photoCount` (hôm nay thiếu một khoá) — đây là thứ duy nhất cho tài xế biết
  mấy tấm đã vào

**Impact Range**
- `components/pod/` · `Z:80-86`

---

##### `[DEV TASK]` E09-11-FE-03 — Route photo uploads through apiFetch

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Đường ảnh dùng `fetch` thẳng, **không qua `apiFetch`**. Hai hệ quả đo được:
  - **401 trên đường ảnh không chuyển sang `/login`** — màn chỉ hiện `M_10` và **tài xế bấm lại
    mãi không được**
  - `body.fields` của hai mã `validation_failed` **không bao giờ hiện ra** vì chỗ gọi chỉ đọc
    `body.message`
- **AC-26-72** — Given 401 trên đường tải ảnh · When phiên hết hạn · Then chuyển sang `/login`
- **AC-26-73** — Given mọi lần gửi POD hỏng sau khi đã đính ảnh · Then dòng `photo_uploads` **vẫn
  còn** — ảnh là bằng chứng, giữ nguyên hành vi này

**Impact Range**
- `PUF:38` · `PUF:41`

---

##### `[DEV TASK]` E09-11-FE-04 — Warn that the rejection exception code has downstream effects

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Ô `例外コード` trông như **ba lựa chọn ngang nhau**, nhưng **chỉ `受取拒否` làm `accepted = false`**,
  và hệ quả nằm ở **màn khác**: dòng đó bị loại khỏi phép tìm "lần giao đã nhận gần nhất" của
  `SCR-21 R-18`
- **AC-26-65** — Given tài xế chọn `受取拒否` · When ô đổi giá trị · Then ngay dưới ô hiện câu cảnh
  báo hệ quả
- **AC-26-39** — Given dòng `delivery_history` có `accepted = false` · When SCR-21 tìm lần giao đã
  nhận · Then dòng đó **bị bỏ qua**

**Impact Range**
- Ô `例外コード` của SCR-26 · `_common/thong-bao-ja.md`

---

##### `[DEV TASK]` E09-11-FE-05 — Make the allocated-lot table scrollable on a phone

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Bảng `引当ロット` dùng `min-w-full` **không có khung cuộn ngang**; năm cột **tràn mép trên màn
  điện thoại**. Toàn màn chỉ có **một** điểm ngắt responsive
- ⚠ Màn này là màn **tài xế dùng trên điện thoại ngoài hiện trường** — không phải lỗi thẩm mỹ
- **AC-26-75** — Given màn hình rộng dưới 400 px · When bảng render · Then cuộn ngang được trong
  khung của nó
- **AC-26-13** vẫn đúng — **đúng 5 cột, đúng thứ tự**

**Impact Range**
- `LIST:70` · `FORM:138`

---

#### `[STORY]` US-27 — Center worker groups picking tasks by zone, route and load order

**Overview**
- **Who:** `センター作業者`
- **What:** tác vụ lấy hàng **gom theo khu vực, tuyến và thứ tự xếp xe**; đổi tác vụ vẫn giữ phân
  bổ ban đầu và nhật ký
- **Why:** FR-OUT-03 (P1) — đi lại trong kho là phần lớn thời gian của một ca

**Acceptance Criteria**
- `[tự viết]` Given mười đơn cùng ngày ở ba khu vực kho · When mở `/loading` · Then danh sách gom
  theo khu vực, trong mỗi khu vực sắp theo tuyến rồi thứ tự xếp xe
- `[tự viết]` Given đổi một tác vụ sang người khác · When đổi · Then phân bổ ban đầu **giữ nguyên**
  và có một dòng nhật ký ghi việc đổi
- **AC-23-16** vẫn đúng — thẻ đơn giữ nguyên nội dung

**References & Dependencies**
- Spec: SCR-23 §6.3 #10 · `screen-list-final-vi` (SCR-22 **đã gộp vào SCR-23**)
- ⚠ **Không có trong code.** Danh sách chỉ sắp theo `納品日` rồi `受注番号` — **không có khái niệm
  khu vực, tuyến hay thứ tự xếp xe, không có bảng tác vụ lấy hàng**
- Phụ thuộc **E01**/**E03** cho khái niệm tuyến

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E09-27-BE — Build the picking task grouping the RFP asks for

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `DB (migration)` + `API route`

**Impact Range**
- Bảng tác vụ lấy hàng (mới) · `app/api/orders/`

---

##### `[DEV TASK]` E09-27-BE-01 — Build picking task grouping by zone, route and load order

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `API route` · **Phụ thuộc:** `E03-BE-01`

**Specification**
- Cần: khái niệm **khu vực kho** (`locations` chưa nhóm), liên kết đơn ⟷ tuyến (chỉ có sau E03),
  và một **bảng tác vụ lấy hàng** với nhật ký đổi người
- `[tự viết]` Given đơn đã nằm trên một tuyến đã công bố · When dựng tác vụ lấy hàng · Then thứ tự
  xếp xe lấy từ `route_stops.seq` **đảo ngược** (hàng xuống sau xếp vào trước)
- ⚠ Mức P1, và **phụ thuộc cả module lập lịch** — xếp sau cùng trong E09

**Impact Range**
- Bảng mới · `locations` (cột khu vực) · `OLQ:75`

---

#### `[PARENT][FE]` E09-27-FE — Present picking tasks in the grouped order

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Impact Range**
- Danh sách SCR-23

---

##### `[DEV TASK]` E09-27-FE-01 — Render the picking queue grouped by zone, route and load order

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E09-27-BE-01`

**Specification**
- Danh sách gom nhóm thay cho danh sách phẳng hiện nay
- `[tự viết]` Given tác vụ đã gom nhóm · When mở `/loading` · Then mỗi nhóm có tiêu đề khu vực và
  số tác vụ, và thứ tự trong nhóm khớp thứ tự xếp xe
- **AC-23-12** vẫn đúng — không đơn nào thì hiện đúng một câu

**Impact Range**
- Danh sách SCR-23

---

#### `[INVESTIGATION]` E09-INV-01 — Confirm what happens when a picked lot is quarantined before departure

**Overview**
- Lô bị Cách ly **sau khi đã lấy hàng, trước khi xe chạy** **không được kiểm lại**: `confirm_load`
  không đọc `lot_state`, và `confirm_pick` đã chạy xong
- Đã được xếp vào *"cần quyết định nghiệp vụ"* ở `conventions-and-assumptions.md:108`
- **Hỏi khách:** hàng đã lấy ra khỏi vị trí rồi mà lô bị cách ly thì chặn xe, hay cho đi và xử sau
- **Giả định vendor:** cho đi, xử sau (hành vi hiện tại)
- **Mức đổi:** chặn → `confirm_load` và `confirm_dispatch` phải đọc lại `lot_state`
- **AC-23-21** / **AC-23-37** ghi lại hành vi hôm nay

**References**
- SCR-23 §6.3 #14 · `conventions-and-assumptions.md:108`

---

#### `[INVESTIGATION]` E09-INV-02 — Confirm Q66: who records pre-dispatch checks and who confirms loading

**Overview**
- Hỏi khách: ai ghi kiểm tra trước xuất và ai xác nhận xếp xe — trưởng kho, tài xế, hay chia nhau
- **Giả định vendor:** **chia nhau trên cùng màn SCR-24**, cưỡng chế ở **ba tầng**
- Vai Trưởng kho của RFP ánh xạ sang `センター作業者` vì bảng vai không có vai đó
- **Mức đổi:** khách chia khác → đổi `READING_KIND_ROLE` ở **ba nơi** cùng lúc (`AC-24-35`)

**References**
- SCR-24 §6.3 #1 · `client-qa-list.md:60` · `AC-24-32`…`AC-24-35`

---

#### `[INVESTIGATION]` E09-INV-03 — Confirm Q64: is a printed dispatch slip required

**Overview**
- Hỏi khách: có cần in Phiếu xuất kho không
- **Giả định vendor:** **không in**; thay bằng màn hình SCR-24 và SCR-25. Comment `API16:9` ghi
  thẳng *"No Phiếu xuất kho printing (Q64)"*
- **Mức đổi:** khách trả lời "cần in" → thêm **hai mẫu in PDF** (FORM-DSP-01 và mẫu kèm)

**References**
- SCR-24 §6.3 #15 · `client-qa-list.md:58`

---

#### `[INVESTIGATION]` E09-INV-05 — Confirm whether POD location must be real coordinates

**Overview**
- **US-11 AC1** đòi ghi **thời điểm, vị trí**, người nhận, chữ ký/ảnh, mã ngoại lệ
- Hôm nay *"vị trí"* **chỉ là ô chữ tự do** `位置メモ` ≤ 500 ký tự — **không toạ độ, không dấu thời
  gian GPS**; và cột `pods.location_note` **không ai đọc**
- Cộng: màn ghi **11 cột** vào `pods` nhưng SCR-35 chỉ lấy **7**. **Năm cột không ai đọc**:
  `signature_mock_checked`, `place_note`, `location_note`, `uploaded_by`, `device_label`
- **Hỏi khách:** vị trí phải là toạ độ GPS hay ghi chú chữ là đủ
- **Mức đổi:** cần GPS → thêm quyền định vị trên thiết bị, cột toạ độ, và xử lý ca từ chối quyền

**References**
- SCR-26 §6.3 #14 #15 · `Z:48` · `TRACE:60`

---

### E10 · Chuỗi nhiệt độ & sai lệch

| | |
|---|---|
| **Màn** | SCR-31 (22 dòng) · SCR-32 (16 dòng) · SCR-33 (21 dòng) — **59 dòng 6.3** |
| **Nhóm LAB-1 đối chiếu** | F07 — 99 SP / 54 MD |
| **Số item** | 1 epic + 4 story + 8 parent + 20 dev task + 5 investigation = **38** |

⚠ **Q19 (số mức nghiêm trọng) là câu hỏi đắt nhất của epic này** — nó chạm cả ba màn, cộng SCR-12
và SCR-24. Giả định ước công là **3 mức**, code đang có **2**. `GĐ-6` của LAB-4 ghi đúng chỗ lệch này.

```
[EPIC] E10 Make the temperature chain judge, alert and resolve with a complete audit trail
├── [STORY] US-15 Quality manager imports a logger CSV and sees exactly what was accepted
│   ├── [PARENT][BE] E10-15-BE Make import boundaries explicit and chainable across files
│   │   ├── E10-15-BE-01 Move the 15-minute review deadline out of hardcoded SQL
│   │   ├── E10-15-BE-02 Let an excursion chain span two import files
│   │   ├── E10-15-BE-03 Group excursion chains by device, not only by location
│   │   └── E10-15-BE-04 Align the two 5000-row counters and the file-name length rules
│   └── [PARENT][FE] E10-15-FE Stop the import panel from hiding what it skipped
│       ├── E10-15-FE-01 Raise quarantined lots from a footnote to a real consequence block
│       ├── E10-15-FE-02 Separate unmapped-device rows from accepted rows in the counts
│       ├── E10-15-FE-03 Build a read-only view of a past import
│       └── E10-15-FE-04 Unify the three empty-file messages and add the date filter
├── [STORY] US-16 Each reading is judged against the threshold version in force on its day
│   ├── [PARENT][BE] E10-16-BE Record the peak that actually matters and pin the rule version
│   │   ├── E10-16-BE-01 Store the minimum as well as the maximum of an excursion
│   │   └── E10-16-BE-02 Write rule_version on the three temperature events
│   └── [PARENT][FE] E10-16-FE Show both ends of the excursion on the alarm card
│       └── E10-16-FE-01 Show both the highest and the lowest reading on the alarm card
├── [STORY] US-17 Quality manager reviews every alarm within fifteen minutes
│   ├── [PARENT][BE] E10-17-BE Make the review deadline and the late rate measurable
│   │   ├── E10-17-BE-01 Expose reviewed alarms so the queue is not the only view
│   │   └── E10-17-BE-02 Build the late-review rate report US-17 AC3 asks for
│   └── [PARENT][FE] E10-17-FE Keep the alarm queue fresh and its messages precise
│       ├── E10-17-FE-01 Refresh the alarm queue every 60 seconds with a manual reload
│       ├── E10-17-FE-02 Add a reviewed tab so confirmed alarms stay reachable
│       └── E10-17-FE-03 Split the four situations that share one failure message
└── [STORY] US-18 Quality manager drives a deviation through five steps with evidence
    ├── [PARENT][BE] E10-18-BE Give the deviation record a history, attachments and separation of duty
    │   ├── E10-18-BE-01 Make the deviation step history append-only and readable
    │   ├── E10-18-BE-02 Add attachment storage and the mandatory-evidence close gate
    │   ├── E10-18-BE-03 Enforce separation between the initiator and the approver
    │   ├── E10-18-BE-04 Move the step matrix into a table instead of two hardcoded copies
    │   ├── E10-18-BE-05 Enforce the 1000-character note limit below zod
    │   └── E10-18-BE-06 Move the Japanese history strings out of SQL
    └── [PARENT][FE] E10-18-FE Make the deviation queue behave like a queue
        ├── E10-18-FE-01 Default the step filter to not-closed and add paging
        ├── E10-18-FE-02 Render the three error messages that are currently dropped
        ├── E10-18-FE-03 Split the shared 409 and list-load messages
        └── E10-18-FE-04 Rewrite the severity note so it stops stating an assumption as fact
[INVESTIGATION] E10-INV-01 Confirm Q19 — how many deviation severity levels and who approves each
[INVESTIGATION] E10-INV-02 Confirm Q36 — how long out of range before it becomes an alarm
[INVESTIGATION] E10-INV-03 Confirm Q17 — is the 15-minute deadline measured from reading or import
[INVESTIGATION] E10-INV-04 Confirm Q46 — does an alarm quarantine lots automatically
[INVESTIGATION] E10-INV-05 Confirm the frozen-zone lower bound and the severity comparison operator
```

---

#### `[EPIC]` E10 — Make the temperature chain judge, alert and resolve with a complete audit trail

**Overview & Goal**
- As a `品質管理` (*"Quản lý chất lượng"*)
- I want nạp dữ liệu máy ghi nhiệt, thấy cảnh báo đúng mức, xác nhận trong hạn và đóng hồ sơ sai
  lệch có bằng chứng
- So that khi cơ quan quản lý hỏi *"lô này có bị phá vỡ chuỗi lạnh không"*, hệ trả lời được

**Scope & Features**
- Chuỗi vượt nhiệt **nối được giữa hai tệp** — hôm nay 50 phút cắt làm hai tệp 25 phút thì
  **không cảnh báo nào sinh ra**
- Gom chuỗi **theo thiết bị**, không chỉ theo vị trí
- Hạn 15 phút ra khỏi SQL viết cứng, vào bảng có phiên bản
- Hồ sơ sai lệch: **lịch sử bước**, **tệp đính kèm**, **tách người khởi tạo với người duyệt**
- Báo cáo tỷ lệ xem trễ — mục tiêu nghiệp vụ là kéo từ **11,0% xuống dưới 1,0%**

**Ngoài phạm vi**
- Sai lệch mở từ **SCR-12** và **SCR-24** → E06/E09 là nơi **sinh ra**; E10 là nơi **xử lý**
- Kết nối máy ghi nhiệt trực tiếp — ngoài phạm vi, chỉ nạp CSV

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-31-19** · **AC-33-62** vẫn đúng — Given dòng `logger_imports`/`temperature_readings`/`events`
  · When thử sửa/xoá · Then bị chặn
- **AC-32-47** · **AC-33-61** đảo chiều — Given dòng `temperature.alarm_reviewed` và
  `deviation.step_advanced` · When đọc `rule_version` · Then **không** còn NULL

**References & Dependencies**
- Spec: `scr-31-nhap-csv-nhiet-do.md` · `scr-32-canh-bao-nhiet-do.md` · `scr-33-quan-ly-sai-lech.md`
- Estimate LAB-1: F07 — 99 SP / 54 MD

---

#### `[STORY]` US-15 — Quality manager imports a logger CSV and sees exactly what was accepted

**Overview**
- **Who:** `品質管理`
- **What:** nạp tệp CSV của máy ghi nhiệt, thấy rõ dòng nào nhận, dòng nào loại và vì sao
- **Why:** FR-TEMP-01 (P0) — đây là **nguồn duy nhất** của dữ liệu chuỗi lạnh

**Acceptance Criteria**
- **AC-31-15**…**AC-31-18** — tệp sạch: **đúng một** dòng `logger_imports`, một sự kiện
- **AC-31-29**…**AC-31-39** — mười lý do loại một dòng, **tệp vẫn nạp**; một dòng hỏng cả bốn ô
  thì bốn câu lý do nối liền
- **AC-31-41**…**AC-31-44** — chống nạp trùng bằng **SHA-256**: cùng nội dung khác tên tệp vẫn là
  trùng; khác byte (BOM) thì **không** trùng
- **AC-31-45** — Given hai yêu cầu nạp cùng tệp **đồng thời** · Then chỉ một thành công
- **AC-31-48**…**AC-31-51** — ba dải nhiệt, biên `5.00` trong dải / `5.01` ngoài dải
- **AC-31-52** — Given hai phiên bản ngưỡng đều `<= ngày đo` · Then dùng bản `valid_from` lớn nhất
- **AC-31-57** / **AC-31-58** — chuỗi **đúng 30 phút** thành cảnh báo; **25 phút** thì không
- **AC-31-76**…**AC-31-79** — thiết bị chưa map vị trí: dòng vẫn đếm vào `rowsAccepted` nhưng
  **không tham gia** phán định
- **AC-31-93**…**AC-31-97** — lịch sử nạp 20 dòng, bảy cột

**References & Dependencies**
- Spec: SCR-31 §6.4.3 · §6.4.6…§6.4.10 · §6.4.13 · §6.4.14

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E10-15-BE — Make import boundaries explicit and chainable across files

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Impact Range**
- `import_logger_csv` · `temperature_alarms` · `logger_imports`

---

##### `[DEV TASK]` E10-15-BE-01 — Move the 15-minute review deadline out of hardcoded SQL

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E10-INV-03`

**Specification**
- `v_due_at := v_now + interval '15 minutes'` — **số 15 viết cứng trong SQL**, khác hẳn **mọi ngưỡng
  khác** đều có `version_label` + `valid_from`
- Đưa vào một bảng ngưỡng có phiên bản, theo đúng lối `temperature_threshold_versions`
- **AC-31-75** — Given mọi cảnh báo sinh trong **cùng một lần nạp** · When đọc `due_at` · Then
  cùng một mốc
- **AC-32-26** — Given tệp nạp lúc 09:00 sinh ba cảnh báo · Then cả ba cùng hạn
- ⚠ Chờ **Q17**: hạn tính từ **lúc đo** hay **lúc nạp**. Giả định vendor: **từ lúc nạp**

**Impact Range**
- `M04b:246` · bảng ngưỡng mới · `temperature_alarms.due_at`

---

##### `[DEV TASK]` E10-15-BE-02 — Let an excursion chain span two import files

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- `where r.import_id = v_import_id` — **chỉ gom trên dòng đo của chính lần nạp này**
- ⚠ **Hệ quả thật:** một đợt vượt nhiệt **50 phút bị cắt làm hai tệp 25 phút** thì **không cảnh
  báo nào sinh ra** — cả hai đoạn đều dưới ngưỡng 30 phút
- Comment `M04b:250-251` nói rõ là chủ ý (`temperature_alarms.import_id` là nguồn gốc), nhưng chủ ý
  đó **tạo ra một điểm mù thật**
- **AC-31-64** đảo chiều — Given chuỗi vượt ngưỡng bị cắt làm hai tệp mỗi tệp 25 phút · When nạp
  lần lượt · Then có cảnh báo (hôm nay: **không**)
- Phải giữ được `import_id` là nguồn gốc trong khi vẫn nối chuỗi — thiết kế này cần quyết trước

**Impact Range**
- `M04b:267` · `temperature_alarms.import_id`

---

##### `[DEV TASK]` E10-15-BE-03 — Group excursion chains by device, not only by location

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Chuỗi gom theo `partition by f.location_id` — **theo vị trí, không theo thiết bị**. Hai máy ghi
  nhiệt cùng một kho **trộn chung một dòng thời gian**: một lần đo **trong dải** của máy này
  **cắt chuỗi** của máy kia
- Comment nói rõ là chủ ý (*"một cảnh báo cho một kho"*), nhưng hệ quả là **cảnh báo bị bỏ sót**
- **AC-31-63** — Given hai máy ghi cùng gắn với **một** vị trí · When nạp tệp có dòng đo xen kẽ ·
  Then chuỗi không bị cắt sai
- Hệ quả riêng ở SCR-32: thẻ hiện **mã vị trí**, không hiện mã thiết bị → sau task này phải thêm

**Impact Range**
- `M04b:271` · `M04b:248-251` · thẻ cảnh báo SCR-32

---

##### `[DEV TASK]` E10-15-BE-04 — Align the two 5000-row counters and the file-name length rules

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `API route`

**Specification**
- **Hai nơi đếm 5000 khác nhau**: parser đếm **mọi dòng dữ liệu** (gồm dòng trống và dòng sẽ bị
  loại); RPC chỉ đếm **dòng được nhận**. Hai hằng `5000` và `200` **lặp literal trong SQL**
- **Ba tầng đếm tên tệp khác đơn vị**: trình duyệt và route dùng `.trim().length` (UTF-16), RPC
  dùng `btrim` + `char_length` (ký tự) — **và hai câu thông báo khác nhau**
- ⚠ `LOGGER_FILE_TOO_LARGE` trả **HTTP 413** mà `mapRpcError` không có 413 — việc **đăng ký mã**
  đó không thuộc task này, nó nằm ở `E12-ST-BE-01` (bảng mã lỗi gom chung)
- **AC-31-26** — Given tệp 5001 dòng (đếm cả dòng trống) · Then bị chặn
- **AC-31-81** — Given RPC nhận `p_rows` 5001 phần tử · Then 422
- **AC-31-21** — Given tên tệp dài hơn 200 ký tự · Then một câu duy nhất, một cách đếm duy nhất

**Impact Range**
- `PARSE:156` · `M04b:152` · `M04b:109` · `API:59-60` · `FORM:67`

---

#### `[PARENT][FE]` E10-15-FE — Stop the import panel from hiding what it skipped

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `PANEL:86-96` · `FORM:41` · khối lịch sử nạp

---

##### `[DEV TASK]` E10-15-FE-01 — Raise quarantined lots from a footnote to a real consequence block

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Lô bị cách ly hiện trong **một dòng chữ nhỏ** cuối panel, **cùng cỡ chữ với thông tin phụ**.
  **Không màn nào nói** cho người dùng rằng lô đó **đã rời khỏi phân bổ ở SCR-21**
- Dữ liệu **đã có sẵn** trong phản hồi, chỉ thiếu chỗ hiện
- **AC-31-89** — Given lần nạp có `quarantinedLots.length > 0` · Then khối `隔離したロット` hiện ra
- **AC-31-90** — Given khối đó · When bấm một mã lô · Then mở `/lots/{lotId}` (SCR-19) đúng lô

**Impact Range**
- `PANEL:86-90`

---

##### `[DEV TASK]` E10-15-FE-02 — Separate unmapped-device rows from accepted rows in the counts

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Dòng đo của thiết bị **chưa map vị trí** tính vào `rowsAccepted` và hiện ở thẻ `取込` **như mọi
  dòng khác**; việc chúng **không được phán định** chỉ lộ ra ở **một dòng chữ xám**
- → người dùng tưởng tệp đã được kiểm hết
- **AC-31-91** — Given `unmappedDevices.length > 0` · Then khối riêng hiện ra
- **AC-31-77** — Given cùng tệp đó · When đọc `rowsAccepted` · Then dòng chưa map **vẫn được đếm**
  — nhưng màn phải nói rõ chúng không được phán định

**Impact Range**
- `PANEL:96-…` · thẻ `取込`

---

##### `[DEV TASK]` E10-15-FE-03 — Build a read-only view of a past import

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `API route`

**Specification**
- Cách **duy nhất** để xem lại kết quả một lần nạp cũ là **nạp lại chính tệp đó** — một thao tác
  **trông như ghi dữ liệu**, và trả về **bản rút gọn** không có lô đã cách ly, không có mã Sai lệch
- Dữ liệu **đã lưu đủ**: `rejected_rows` nằm trong `logger_imports`
- **AC-31-92** — Given lần nạp trùng · Then panel nói rõ đây là bản rút gọn
- `[tự viết]` Given một lần nạp cũ trong lịch sử · When bấm vào dòng đó · Then mở lại panel đầy đủ
  **mà không** ghi gì vào DB
- Cân nhắc hiện thêm `device_raw_ts` và `device_tz` — hai cột **ghi đúng theo US-15 AC3 nhưng
  không endpoint nào trả về**

**Impact Range**
- `logger_imports.rejected_rows` · endpoint đọc mới · khối lịch sử

---

##### `[DEV TASK]` E10-15-FE-04 — Unify the three empty-file messages and add the date filter

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- *"Tệp không có gì"* có **ba câu** ở ba chỗ khác nhau: tệp 0 byte (route) · 0 dòng (parser) ·
  chỉ có tiêu đề (parser) — ba câu cho **cùng một việc** dưới mắt người dùng
- Cộng: **sáu tình huống rơi về cùng một câu** `CSVを取り込めませんでした`, gồm cả `internal_error`
  và `conflict_concurrent_update`
- Cộng: `取込履歴` cố định **20 dòng mới nhất**, không lọc. **Spec đã định nghĩa xong**: không
  phân trang, thêm **lọc theo khoảng ngày nạp**
- **AC-31-23** / **AC-31-24** — hai ca tệp rỗng, câu nhất quán
- **AC-31-87** — Given HTTP ≥ 500 · Then `M_53`
- **AC-31-97** — Given bảng lịch sử có lọc theo khoảng ngày · When chọn khoảng không khớp ·
  Then câu riêng

**Impact Range**
- `API:56` · `PARSE:144` · `PARSE:155` · `FORM:41` · khối `取込履歴`

---

#### `[STORY]` US-16 — Each reading is judged against the threshold version in force on its day

**Overview**
- **Who:** `品質管理`, và `監査者` về sau
- **What:** mỗi dòng đo so với ngưỡng **có hiệu lực vào ngày đo**, mỗi đợt vượt lưu **peak**
- **Why:** FR-TEMP-02 (P0) + BR-TEMP-01 — bản ghi cũ phải **đọc lại đúng bản luật có hiệu lực lúc nó được phán**

**Acceptance Criteria**
- **AC-31-52** — Given hai phiên bản ngưỡng đều `<= ngày đo` · Then dùng bản `valid_from` lớn nhất
- **AC-31-53** / **AC-31-54** — Given tệp đo ngày trước mọi `valid_from` · Then `detail.uncovered`
  nêu rõ dải nào chưa được phủ
- **AC-31-60** / **AC-31-61** — Given chuỗi tại `C-01` (`max_c = 5`, `severe_delta_c = 3`) với
  đỉnh `8.00℃` · Then `軽微`; với `8.01℃` · Then `重大` — biên dùng so sánh **nghiêm**
- **AC-31-62** — Given chuỗi tại kho đông vi phạm **cận dưới** · Then phân mức đúng
- **AC-32-16** — Given cảnh báo ở `F-02` với `max_c của alarm = -12.40` · Then thẻ hiện đúng
- **AC-32-52** — Given cảnh báo bất kỳ · Then có **hai** ô `最高値` và giá trị thấp nhất
- **AC-32-44** — Given cảnh báo kho Mát có chuỗi đo **toàn phần dưới** `0℃` · Then `max_c` **không
  phải** con số tệ nhất — hiện trạng chưa đúng
- **AC-31-46** — Given tệp đã nạp từ tuần trước và bảng ngưỡng **đã thêm phiên bản mới** · Then
  phán định cũ **không đổi**
- **AC-32-47** đảo chiều — Given dòng `temperature.alarm_reviewed` · Then `rule_version` có giá trị

**References & Dependencies**
- Spec: SCR-31 §6.4.8 · §6.4.9 · SCR-32 §6.4.3 · §6.4.7 · BR-TEMP-01 (tr.21)

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E10-16-BE — Record the peak that actually matters and pin the rule version

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Impact Range**
- `temperature_alarms` · `events.rule_version`

---

##### `[DEV TASK]` E10-16-BE-01 — Store the minimum as well as the maximum of an excursion

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- **US-16 AC2** đòi mỗi đợt vượt ngưỡng lưu **peak**. Cột `max_c` **luôn là giá trị cao nhất**,
  nên **đợt vi phạm cận dưới hiện một con số không phải con số tệ nhất**
- Giá trị thấp nhất **không có cột** trong `temperature_alarms`; nó chỉ sống trong
  `events.payload.minC` và trong `summary_ja` của Sai lệch — **không truy vấn được**
- **AC-32-44** đảo chiều — Given cảnh báo kho Mát với chuỗi toàn phần dưới `0℃` · Then con số hiện
  ra là **con số tệ nhất**
- **AC-31-62** vẫn đúng cho ca cận dưới

**Impact Range**
- `temperature_alarms` (cột mới) · `import_logger_csv` · thẻ SCR-32

---

##### `[DEV TASK]` E10-16-BE-02 — Write rule_version on the three temperature events

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- **BR-TEMP-01** đòi bản ghi cũ **neo vào bản luật có hiệu lực lúc phán, không trôi theo bản mới**
- Ba sự kiện ghi `rule_version = NULL` dù dữ liệu nguồn **có sẵn** đường tới `threshold_version_id`:
  `temperature.alarm_raised` (SCR-31) · `temperature.alarm_reviewed` (SCR-32) ·
  `deviation.step_advanced` (SCR-33)
- Nguyên nhân chung: **tham số thứ tư của `log_event` bị bỏ trống** ở cả ba chỗ
- **AC-32-47** / **AC-33-61** đảo chiều — Given ba dòng sự kiện đó · Then `rule_version` có giá trị
- Cùng họ với `E07-05-BE-03` (`lot.status_changed` cũng NULL) → **bốn sự kiện, một nguyên nhân**

**Impact Range**
- `RPCS:490-491` · `M04b:660` · `import_logger_csv` · `log_event`

---

#### `[PARENT][FE]` E10-16-FE — Show both ends of the excursion on the alarm card

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Impact Range**
- Thẻ cảnh báo SCR-32

---

##### `[DEV TASK]` E10-16-FE-01 — Show both the highest and the lowest reading on the alarm card

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E10-16-BE-01`

**Specification**
- **AC-32-52** — Given cảnh báo bất kỳ · Then có **hai** ô: giá trị cao nhất và giá trị thấp nhất
- **AC-32-14** vẫn đúng — thẻ hiện đủ **bảy** ô theo đúng thứ tự (nay thành tám)
- **AC-32-16** — Given cảnh báo ở `F-02` · Then hiện đúng cả hai đầu
- Cộng: thẻ hiện **mã vị trí**, không hiện mã thiết bị — sau `E10-15-BE-03` phải thêm mã thiết bị

**Impact Range**
- Thẻ cảnh báo SCR-32

---

#### `[STORY]` US-17 — Quality manager reviews every alarm within fifteen minutes

**Overview**
- **Who:** `品質管理`
- **What:** hàng đợi cảnh báo chưa xác nhận, đồng hồ đếm ngược, bấm xác nhận
- **Why:** FR-TEMP-03 (P0) — mục tiêu nghiệp vụ là kéo tỷ lệ xem trễ từ **11,0% xuống dưới 1,0%**

**Acceptance Criteria**
- **AC-32-19** — Given ba cảnh báo khác mức và khác hạn · Then thứ tự hàng đợi đúng
- **AC-32-21**…**AC-32-25** — đồng hồ đếm ngược: còn 6 phút, còn ≤5 phút đổi dạng, đã quá hạn
- **AC-32-24** — Given đồng hồ máy người dùng **nhanh hơn máy chủ 10 phút** · Then màn vẫn đúng
- **AC-32-28** / **AC-32-29** — Given cảnh báo chưa ai xác nhận và **còn trong hạn** · When bấm
  `確認` · Then `first_reviewed_at` bằng **giờ máy chủ**
- **AC-32-30** — Given cảnh báo **đã quá hạn** · When bấm lần đầu · Then đánh dấu `遅延`
- **AC-32-31** / **AC-32-32** — Given **người khác** đã xác nhận trước · Then giữ nguyên mốc đầu
- **AC-32-34** / **AC-32-35** — Given lần `確認` ghi được · Then **đúng một** dòng `events`;
  nhánh `alreadyReviewed` thì **không** dòng nào
- **AC-32-38** — Given hai phiên bấm gần như đồng thời · Then chỉ một ghi được
- **AC-32-53** — Given màn có hai tab `未確認` và `確認済み` · Then cảnh báo đã xác nhận **vẫn
  xem lại được**
- **AC-32-54** — Given màn ở tab `未確認` · When chờ 60 giây · Then tự gọi lại `GET /api/alarms`

**References & Dependencies**
- Spec: SCR-32 §6.4.4…§6.4.6 · §6.4.8

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E10-17-BE — Make the review deadline and the late rate measurable

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `API route`

**Impact Range**
- `app/api/alarms/` · `temperature_alarms`

---

##### `[DEV TASK]` E10-17-BE-01 — Expose reviewed alarms so the queue is not the only view

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- **Không có chỗ nào xem lại cảnh báo đã xác nhận.** Thẻ rời hàng đợi và **biến mất**;
  `first_reviewed_at`, `first_reviewed_by`, `reviewed_late` **không màn nào đọc**
- Mô tả trang **tự hứa** `「遅延」として残ります` (*"vẫn được giữ lại dưới dạng «Trễ»"*) — lời hứa
  này hôm nay **không đúng**
- `QRY:83` lọc cứng `first_reviewed_at is null`
- **AC-32-46** đảo chiều — Given cảnh báo vừa được xác nhận · When tìm nó trên toàn ứng dụng ·
  Then tìm thấy (hôm nay: **không đâu cả**)

**Impact Range**
- `QRY:83` · `app/api/alarms/`

---

##### `[DEV TASK]` E10-17-BE-02 — Build the late-review rate report US-17 AC3 asks for

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- **US-17 AC3** đòi xem trễ được đánh dấu rõ **và đưa vào báo cáo quản lý**
- Vế **đánh dấu** có (`reviewed_late`). Vế **báo cáo quản lý** **không có trong code** — không màn
  nào, không endpoint nào tổng hợp tỷ lệ xem trễ
- ⚠ **Đây là chỗ đo mục tiêu nghiệp vụ của cả US-17** (11,0% → dưới 1,0%). Không có nó thì không
  ai biết hệ có đạt mục tiêu không
- `[tự viết]` Given một khoảng thời gian · When gọi endpoint báo cáo · Then trả tổng số cảnh báo,
  số xem trễ và tỷ lệ

**Impact Range**
- Endpoint mới · `temperature_alarms.reviewed_late`

---

#### `[PARENT][FE]` E10-17-FE — Keep the alarm queue fresh and its messages precise

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `QUEUE:87-90` · `QUEUE:97`

---

##### `[DEV TASK]` E10-17-FE-01 — Refresh the alarm queue every 60 seconds with a manual reload

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Màn **tải một lần**; cảnh báo mới **không hiện** cho tới khi người dùng tự tải lại. Với một hàng
  đợi có hạn **15 phút**, điều này làm hỏng chính mục tiêu của màn
- **Wireframe 6.4 đã quyết: 60 giây một lần**, kèm nút tải lại thủ công
- **AC-32-54** — Given màn ở tab `未確認` · When chờ 60 giây · Then tự gọi lại
- **AC-32-56** — Given nút tải lại thủ công · When bấm · Then gọi một lần
- **AC-32-48** đảo chiều — Given tệp CSV nạp **sau khi** màn đã mở · When chờ 5 phút · Then cảnh
  báo mới hiện ra
- **AC-32-27** — Given màn đang mở với n thẻ · When tải lại · Then đồng hồ không nhảy sai

**Impact Range**
- `QUEUE:87-90`

---

##### `[DEV TASK]` E10-17-FE-02 — Add a reviewed tab so confirmed alarms stay reachable

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E10-17-BE-01`

**Specification**
- **AC-32-53** — Given màn có hai tab `未確認` và `確認済み` · Then cảnh báo đã xác nhận xem lại
  được, kèm mốc và cờ `遅延`
- Cộng: thẻ cần ô liên kết sang Sai lệch đang mở — cảnh báo **thứ hai trở đi** tại cùng vị trí
  **không gắn khoá ngoại** vào Sai lệch đang mở; liên kết chỉ còn trong payload sự kiện
- **AC-32-55** — Given cảnh báo thuộc một Sai lệch đang mở · Then thẻ có ô dẫn tới hồ sơ đó
- **AC-32-50** / **AC-32-51** — Given cảnh báo gắn ≥1 lô, kể cả mức `軽微` · Then khối
  `隔離したロット` hiện ra — **lô vẫn bị cách ly dù cảnh báo chỉ nhẹ**, và màn phải nói rõ

**Impact Range**
- Thẻ cảnh báo SCR-32 · `deviations.alarm_id` · `QRY:13, 59`

---

##### `[DEV TASK]` E10-17-FE-03 — Split the four situations that share one failure message

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **Bốn tình huống khác hẳn nhau** — 403 mất quyền, 409 hai phiên chạm nhau, 5xx lỗi hệ thống,
  mất mạng — **dùng chung một câu** `確認を記録できませんでした`. Nhánh phân biệt duy nhất là 404
- **Spec đã định nghĩa ba câu riêng** (`M_96`, `M_95`, thể của `M_73` và `M_64`)
- **AC-32-39** — Given 409 `conflict_concurrent_update` · Then câu riêng
- **AC-32-40** — Given HTTP ≥ 500 · Then câu riêng
- **AC-32-49** — Given lần tải lại sau `確認` thành công bị lỗi · Then màn nói đúng việc
- **AC-32-43** — Given 401 · Then cả trang chuyển `/login`

**Impact Range**
- `QUEUE:97` · `_common/thong-bao-ja.md`

---

#### `[STORY]` US-18 — Quality manager drives a deviation through five steps with evidence

**Overview**
- **Who:** `品質管理` thao tác, `監査者` đọc lại
- **What:** hồ sơ sai lệch đi năm bước `起票 → 受領確認 → 調査 → 是正措置 → 決定 → クローズ`
- **Why:** FR-TEMP-04 (P0) — hồ sơ phải liên kết cảnh báo, điều tra, bằng chứng, trạng thái tồn
  kho, hành động khắc phục, quyết định

**Acceptance Criteria**
- **AC-33-27**…**AC-33-35** — năm bước đúng thứ tự, mỗi bước **chỉ một** nút đi tiếp
- **AC-33-30** / **AC-33-31** / **AC-33-32** — ghi chú bắt buộc, chỉ khoảng trắng thì chặn, hơn
  1000 ký tự thì chặn
- **AC-33-36**…**AC-33-45** — bước `決定` là **bước duy nhất đổi trạng thái lô**; lô không đổi được
  thì **cả bước bị chặn** và `deviations.step` **không đổi**
- **AC-33-46** — Given hồ sơ ở `起票` · When gọi thẳng API nhảy ba bước · Then bị chặn
- **AC-33-49** — Given hồ sơ đã `クローズ` · When gọi với bất kỳ `toStep` nào · Then bị chặn
- **AC-33-50** — Given bất kỳ ca 422/409/403 nào · Then `deviations` không đổi
- **AC-33-58** / **AC-33-59** — chuyển bước thành công thì **đúng một** dòng `events`; bị từ chối
  thì **không** dòng nào
- **AC-33-62** — Given hồ sơ đã đi vài bước · When thử sửa/xoá `events` · Then bị chặn
- **AC-33-64** / **AC-33-65** — Given hồ sơ đã qua bước `調査` lúc 10:30 · Then **ai làm, lúc nào**
  hiện ra; kể cả bước **không ghi cột nội dung nào**
- **AC-33-67** — Given mở `/deviations` lần đầu · Then ô `手順` ở `未クローズ`
- **AC-33-68** — Given 240 hồ sơ khớp bộ lọc · Then phân trang, **không** cắt im lặng ở 200

**References & Dependencies**
- Spec: SCR-33 §6.4.4…§6.4.9

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E10-18-BE — Give the deviation record a history, attachments and separation of duty

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 6 dev task con)
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- `deviations` là bảng **không append-only**, **bị ghi đè tại chỗ** — ba thiếu sót nặng nhất của
  epic nằm ở đây

**Impact Range**
- `deviations` · `advance_deviation` · bảng lịch sử bước (mới) · bảng tệp đính kèm (mới)

---

##### `[DEV TASK]` E10-18-BE-01 — Make the deviation step history append-only and readable

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- **US-18 AC2** đòi hồ sơ liên kết cảnh báo, điều tra, bằng chứng, trạng thái tồn kho, hành động
  khắc phục, quyết định
- ⚠ **Không chỗ nào xem được ai làm bước nào, lúc nào.** `deviations` **không append-only**, bị
  **ghi đè tại chỗ**; thẻ `完了` chỉ hiện **nội dung**
- Dựng một bảng lịch sử bước append-only, theo đúng lối `lot_status_history`
- **AC-33-64** — Given hồ sơ đã qua bước `調査` lúc 10:30 bởi một tài khoản · Then **ai và lúc nào**
  hiện ra
- **AC-33-65** — Given thẻ `受領確認` ở `完了` — bước **không ghi cột nội dung nào** · Then vẫn
  thấy ai làm, lúc nào
- **AC-33-63** — Given hồ sơ đi từ `起票` tới `クローズ` · When đọc `summary_ja` ở mỗi bước ·
  Then dựng lại được toàn bộ

**Impact Range**
- Bảng lịch sử bước (mới) · `deviations` · `advance_deviation` · `AO:25-31`

---

##### `[DEV TASK]` E10-18-BE-02 — Add attachment storage and the mandatory-evidence close gate

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E10-INV-01`

**Specification**
- **US-18 AC2 và AC4** đòi hồ sơ liên kết **bằng chứng**; *"thiếu căn cứ hoặc tệp bắt buộc thì
  **không đóng được**"*
- **Không có gì**: `deviations` đủ 15 cột, **không cột nào cho tệp**; **không có bảng nối** sang
  ảnh hay tệp
- ⚠ Danh sách tệp bắt buộc **phụ thuộc Q19** (mỗi mức một bộ tệp khác nhau)
- `[tự viết]` Given hồ sơ `重大` thiếu tệp bắt buộc · When bấm `クローズする` · Then bị chặn, nêu
  đích danh tệp còn thiếu
- `[tự viết]` Given hồ sơ đủ tệp · When đóng · Then đóng được, tệp **không xoá được** sau đó

**Impact Range**
- Bảng tệp đính kèm (mới) · `advance_deviation` · Storage

---

##### `[DEV TASK]` E10-18-BE-03 — Enforce separation between the initiator and the approver

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` · **Phụ thuộc:** `E10-INV-01`

**Specification**
- **NFR-SEC-02** đòi RBAC **và tách người khởi tạo với người phê duyệt**
- ⚠ **Không được cưỡng chế.** `advance_deviation` đọc `auth.uid()` **đúng một lần để ghi vết,
  không so nó với ai**. **Cùng một tài khoản đi trọn năm bước**
- Bản mẫu chỉ có **một** tài khoản `品質管理`, nên lỗ hổng này **chưa lộ ra khi chạy thử**
- `[tự viết]` Given tài khoản A đã ghi bước `調査` · When chính A bấm bước duyệt · Then bị chặn
- ⚠ Ai duyệt mức nào **phụ thuộc Q19** — không chốt được trước khi có đáp án

**Impact Range**
- `advance_deviation` (`M04b:515-672`) · bảng lịch sử bước

---

##### `[DEV TASK]` E10-18-BE-04 — Move the step matrix into a table instead of two hardcoded copies

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- Ma trận bước **viết cứng ở hai nơi**: `case v_dev.step` trong SQL và `DEVIATION_ACTIONS` trong
  TypeScript. **Không có bảng chuyển bước nào trong migration**
- Comment ở cả hai phía **dặn phải sửa cùng nhau**, nhưng **không có gì cưỡng chế**
- Dự án đã có khuôn sẵn: `lot_status_transitions` là bảng — làm theo lối đó
- **AC-33-27** / **AC-33-28** vẫn đúng — mỗi bước **chỉ một** nút đi tiếp trong DOM
- **AC-33-46** vẫn đúng — nhảy bước bị chặn
- Cùng họ với `E08-07-BE-01` và `E08-07-BE-02` — **luật cài hai bản, không ai gom**

**Impact Range**
- Bảng chuyển bước (mới) · `M04b:553-560` · `LBL:52-63`

---

##### `[DEV TASK]` E10-18-BE-05 — Enforce the 1000-character note limit below zod

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` hoặc `RPC / luật`

**Specification**
- **zod chặt hơn RPC ở hai chỗ**: trần **1000 ký tự** của ba ô ghi chú chỉ sống ở zod; RPC không
  kiểm, ba cột `text` không có `check`. Và `.strict()` từ chối khoá lạ ở zod trong khi **RPC bỏ
  qua khoá thừa**
- **AC-33-32** — Given ghi chú hơn 1000 ký tự dán vào · Then chặn ở trình duyệt
- **AC-33-52** — Given gọi thẳng **RPC** với `p_payload` là một mảng · Then bị từ chối
- Cùng họ lỗi với `E06-01-BE-01` · `E07-05-BE-02` · `E08-06-BE-01` · `E09-09-BE-02` —
  **năm màn, một họ**

**Impact Range**
- `Z:10, 17` · `TBL3:83-86` · `advance_deviation`

---

##### `[DEV TASK]` E10-18-BE-06 — Move the Japanese history strings out of SQL

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `dùng chung`

**Specification**
- Lý do ghi vào lý lịch lô là **chuỗi dựng thẳng trong SQL**:
  `format('逸脱 %s 決定（%s）: %s', …)`. Nó **không đi qua tệp nhãn nào**
- Cùng họ với `入荷時隔離: …` của `receive_line` và chuỗi của `import_logger_csv` → **ba chỗ, một
  vấn đề**: chuỗi tiếng Nhật nằm trong DB, người bản ngữ **không duyệt được**
- `[tự viết]` Given mọi chuỗi JA sinh trong SQL · When rà soát · Then mỗi chuỗi có một mã trong
  đăng ký chung, hoặc được ghi là **cố ý để trong SQL** kèm lý do

**Impact Range**
- `M04b:648-649` · `receive_line` · `import_logger_csv` · `_common/thong-bao-ja.md`

---

#### `[PARENT][FE]` E10-18-FE — Make the deviation queue behave like a queue

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 4 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `LIST:24, 77-79` · `LIST:93` · `LIST:101` · `P2:101`

---

##### `[DEV TASK]` E10-18-FE-01 — Default the step filter to not-closed and add paging

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `API route`

**Specification**
- Ô lọc `手順` mặc định `すべて`, nên mở màn ra là thấy **lẫn hồ sơ đang xử lý với hồ sơ đã đóng**.
  Màn là **hàng đợi công việc**, nhưng bộ lọc mặc định **không nói điều đó**
- Cộng: danh sách **cắt ở 200 dòng và không báo gì** — `rows.length` in ra đúng `200件` **như thể
  đó là toàn bộ**. Bộ lọc mặc định `すべて` làm chuyện này **chắc chắn xảy ra** trên dữ liệu thật
- **Wireframe 7.4 đã quyết:** thêm tuỳ chọn gộp `未クローズ` và đặt nó làm mặc định
- **AC-33-67** — Given mở `/deviations` lần đầu · Then ô `手順` ở `未クローズ`
- **AC-33-68** — Given 240 hồ sơ khớp · Then phân trang, dòng đếm nói đúng tổng
- **AC-33-69** ghi lại hiện trạng (200 hàng, không báo)
- **AC-33-70** / **AC-33-71** — hai ô lọc theo khoảng ngày lập phiếu, đảo ngược thì **422**

**Impact Range**
- `LIST:93` · `LIST:101` · `LQ:11-12` · `app/api/deviations/`

---

##### `[DEV TASK]` E10-18-FE-02 — Render the three error messages that are currently dropped

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- **Ba câu lỗi được dựng ra rồi rơi mất**: `fields.payload` của `VALIDATION_DEVIATION_PAYLOAD`,
  `fields.source` của `VALIDATION_LOT_STATUS_SOURCE`, và `fields.toStep` của zod — **không
  component nào render** ba khoá đó
- Cộng: mô tả thao tác của bước `決定` **chưa bao giờ hiện trên màn** — `StepForm` render
  `action.description` nhưng bước `決定` dùng form riêng, và form đó **không render** mô tả
- **AC-33-37** — Given form `決定` chưa chọn gì và ô `根拠` trống · Then câu hiện đúng chỗ
- **AC-33-44** — Given máy chủ trả `RULE_DEVIATION_LOT_STATUS` · Then câu hiện được
- **AC-33-72** — Given thẻ bước `決定` ở `今の手順` · Then mô tả thao tác hiện ngay dưới tiêu đề

**Impact Range**
- `ERR:70` · `Z:39` · `PANEL:53` · `DeviationDecisionForm`

---

##### `[DEV TASK]` E10-18-FE-03 — Split the shared 409 and list-load messages

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **Mọi lỗi 409 hiện cùng một câu** *"Thao tác khác đã đẩy bước đi tiếp…"*, kể cả
  `conflict_concurrent_update` và `conflict_duplicate` vốn **không liên quan tới bước**
- **Lỗi tải danh sách gộp một câu** cho 401, 403, 422 lọc sai, 500 và mất mạng
- Cộng **hai mã mượn nói sai việc**: `NOT_FOUND` của `apply_lot_status` hiện *"Không tìm thấy sai
  lệch"* trong khi thứ không tìm thấy là **lô**
- Cộng: `notFound()` của trang chi tiết rơi vào **trang 404 mặc định của Next.js** — tiếng Anh,
  không khung ứng dụng. Dùng `not-found.tsx` của `E07-05-FE-02`
- **AC-33-73** — Given HTTP ≥ 500 · Then câu riêng
- **AC-33-74** — Given 409 `conflict_concurrent_update` · Then câu riêng
- **AC-33-75** — Given mã hồ sơ không tồn tại · Then trang 404 hiện `M_61`

**Impact Range**
- `statusMessage(409)` · `LIST:24, 77-79` · `app/not-found.tsx`

---

##### `[DEV TASK]` E10-18-FE-04 — Rewrite the severity note so it stops stating an assumption as fact

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- ⚠ **Màn tự nói ra giả định như một kết luận đã chốt.** Câu ghi chú `I-2` viết
  `重大度は「重大」「軽微」の2段階です（Q19）。` — **trích số hiệu câu hỏi theo cách đọc được là
  "đã có đáp án"**, trong khi Q19 **chưa ai trả lời**
- Người dùng đọc màn sẽ tin đây là luật đã chốt
- **AC-33-57** đảo chiều — Given khối `注記` · When đọc gạch đầu dòng thứ nhất · Then câu đó nói
  rõ đây là **giả định vendor chờ khách xác nhận**
- **AC-33-53** / **AC-33-54** ghi lại hiện trạng: `severity` NULL cho nguồn `入荷検品` và `出荷前点検`
- **AC-33-55** / **AC-33-56** — hai hồ sơ khác mức đi **cùng một** luồng năm bước, và thứ tự danh
  sách **không ưu tiên** `重大`

**Impact Range**
- `P2:101`

---

#### `[INVESTIGATION]` E10-INV-01 — Confirm Q19: how many deviation severity levels and who approves each

**Overview**
- Hỏi khách: hồ sơ sai lệch có **những mức nghiêm trọng nào**, mỗi mức **ai thao tác / ai xem xét /
  ai duyệt**, và **những tệp đính kèm bắt buộc nào** thì mới đóng được hồ sơ
- **Giả định vendor:** **3 mức** · code đang có **2** (`重大`/`軽微`, dùng lại enum `alarm_severity`)
- **Mức đổi:** *"Mỗi mức có luồng duyệt khác nhau → thêm workflow"*
- ⚠ **Câu hỏi đắt nhất của epic.** Nó chặn `E10-18-BE-02` (tệp bắt buộc) và `E10-18-BE-03` (tách
  người duyệt), và chạm cả **E06** (`E06-INV-05`) và **E09**
- **Cùng một câu hỏi với `E06-INV-05`** — gửi **một lần**, trả lời xong thì cả hai epic cùng mở

**References**
- SCR-33 §6.3 #1 #5 · SCR-31 §6.3 #2 · `client-qa-list.md:43` · `PREMISE` `GĐ-6`

---

#### `[INVESTIGATION]` E10-INV-02 — Confirm Q36: how long out of range before it becomes an alarm

**Overview**
- Hỏi khách: vượt ngưỡng **bao lâu** thì thành cảnh báo. Cột Nguồn ghi **"Ngoài RFP"** — tức là
  RFP **không nói gì** về việc này
- **Giả định vendor:** `excursion_minutes = 30` cho cả ba dải, so bằng `>=` nên **đúng 30 phút là
  cảnh báo**; *"cấu hình theo phút"*
- Giá trị **đã nằm trong bảng có phiên bản** nên đổi là đổi dữ liệu, không đổi code
- **AC-31-57** / **AC-31-58** nghiệm thu đúng giả định đang cài

**References**
- SCR-31 §6.3 #1 · SCR-32 §6.3 #1 · `SEED2:16-18`

---

#### `[INVESTIGATION]` E10-INV-03 — Confirm Q17: is the 15-minute deadline measured from reading or import

**Overview**
- **US-17** đòi hạn xem cảnh báo **15 phút**, nhưng **không nói tính từ đâu**
- **Giả định vendor:** tính từ **lúc nạp tệp** — vì không có kết nối máy ghi nhiệt trực tiếp nên
  **không có mốc nào khác**
- Hệ quả: **mọi cảnh báo của cùng một lần nạp có cùng một hạn**
- **Mức đổi:** tính từ lúc đo → một tệp nạp muộn có thể sinh ra cảnh báo **đã quá hạn ngay khi
  vừa sinh**
- Chặn `E10-15-BE-01`

**References**
- SCR-31 §6.3 #9 · SCR-32 §6.3 #4 · `M04b:246`

---

#### `[INVESTIGATION]` E10-INV-04 — Confirm Q46: does an alarm quarantine lots automatically

**Overview**
- **US-18 AC1** nói *"mỗi cảnh báo tạo một hồ sơ sai lệch **và cách ly lô liên quan**"*
- ⚠ **RFP tự mâu thuẫn**: tr.37 nói cách ly ngay; Hình 10 (tr.36) lại vẽ **đo lại trong 15 phút,
  tái diễn mới cách ly**. Và RFP **không nói** việc này do hệ tự làm hay `品質管理` thao tác tay
- **Giả định vendor:** **thao tác tay** — nhưng **code đang tự làm** (`AC-31-70`, `AC-31-71`)
- ⚠ Giả định và hiện trạng **không khớp nhau** — phải nêu rõ khi hỏi khách
- Hệ quả nặng: lô bị cách ly **kể cả khi cảnh báo chỉ `軽微`**, và **màn không báo gì** (`AC-32-45`)

**References**
- SCR-31 §6.3 #5 · SCR-32 §6.3 #2 · SCR-33 §6.3 #20

---

#### `[INVESTIGATION]` E10-INV-05 — Confirm the frozen-zone lower bound and the severity comparison operator

**Overview**
- **Cận dưới dải đông:** RFP chỉ ghi `冷凍帯 ≤ −18°C`, **không có cận dưới**. Seed đặt
  `min_c = -30` → kho đông `−32℃` bị tính **ngoài dải**, mở Sai lệch, **cách ly lô**
- **Biên toán tử tự mâu thuẫn trong chính dự án:** code dùng `>` (`8.00 → 軽微`, `8.01 → 重大`);
  comment seed ghi `≥ 3 °C` — **ngược nhau**. Hai nơi viết hai kiểu, **chưa ai hoà giải**
- **Giả định vendor:** cận dưới `−30℃` · toán tử `>` (theo code)
- **Mức đổi:** đổi cận dưới → thay đổi số lượng cảnh báo và số lô bị cách ly trên dữ liệu thật
- **AC-31-50** · **AC-31-60** · **AC-31-61** nghiệm thu đúng giả định đang cài

**References**
- SCR-31 §6.3 #3 #4 · `SEED2:13` `SEED2:17` · `M04b:303-304` · `PREMISE` `GĐ-3` `GĐ-4`

---

### E11 · Truy xuất nguồn gốc

| | |
|---|---|
| **Màn** | SCR-35 (17 dòng 6.3) |
| **Nhóm LAB-1 đối chiếu** | F08 — 60 SP / 35 MD |
| **Số item** | 1 epic + 3 story + 6 parent + 10 dev task + 2 investigation = **22** |

```
[EPIC] E11 Make the traceability chain complete, fast and safe to read
├── [STORY] US-19 Quality manager traces a lot both ways in one search
│   ├── [PARENT][BE] E11-19-BE Make one broken lot stop breaking the whole search
│   │   ├── E11-19-BE-01 Skip a lot with a missing lot_state instead of failing the search
│   │   ├── E11-19-BE-02 Bound the eleven unlimited history queries
│   │   └── E11-19-BE-03 Stop repeating every lot of an order inside each lot chain
│   └── [PARENT][FE] E11-19-FE Give the search a way to narrow and messages that differ
│       ├── E11-19-FE-01 Build the two narrowing filters above the 30-lot ceiling
│       └── E11-19-FE-02 Split the 401, 409 and 500 messages
├── [STORY] US-32 Internal lot lanes link back to the partner that supplied them
│   ├── [PARENT][BE] E11-32-BE Make the trace lane a real constraint and keep the cattle id
│   │   ├── E11-32-BE-01 Validate the search kind against the SKU trace lane
│   │   └── E11-32-BE-02 Keep the cattle id on a quarantined beef lot
│   └── [PARENT][FE] E11-32-FE Show the partner behind every code
│       └── E11-32-FE-01 Print the customer and supplier name next to every code
└── [STORY] US-20 Quality manager opens a recall case straight from a trace result
    ├── [PARENT][BE] E11-20-BE Prepare the recall hand-off contract
    │   └── E11-20-BE-01 Define what a recall case receives from a trace result
    └── [PARENT][FE] E11-20-FE Make the recall button reachable
        └── E11-20-FE-01 Show the recall button only when SCR-36 is enabled
[INVESTIGATION] E11-INV-01 Confirm whether SCR-36 recall management is in scope
[INVESTIGATION] E11-INV-02 Confirm the 60-second trace target and who supplies the test dataset
```

---

#### `[EPIC]` E11 — Make the traceability chain complete, fast and safe to read

**Overview & Goal**
- As a `品質管理` (*"Quản lý chất lượng"*) hoặc `監査者` (*"Kiểm toán viên"*)
- I want truy ngược và truy xuôi một lô trong một lần tìm, thấy đủ sáu mắt xích
- So that khi có thu hồi, biết hàng từ đâu tới và đã đi tới khách nào

**Scope & Features**
- Một lô hỏng **không được làm hỏng cả lần tìm**
- Giới hạn 11 truy vấn lịch sử đang **không có `.limit()` nào**
- Hai bộ lọc thu hẹp — hôm nay màn **nhắc thu hẹp mà không cho công cụ nào**
- Tên khách và tên nhà cung cấp đứng cạnh mã

**Ngoài phạm vi**
- Mắt xích ❸ `移動` → phụ thuộc **E09** (`E09-09-BE-04` ghi `movements`) và SCR-15 (ngoài 15 màn)
- SCR-36 Quản lý thu hồi — `enabled: false`, xem `E11-INV-01`
- NFR-PERF-02 (3 năm dữ liệu ≤ 60 giây) — **cắt khỏi phạm vi v6**, xem `E11-INV-02`

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-35-52** đảo chiều — Given một lô trong tập kết quả thiếu `lot_state` · When tìm · Then các
  lô còn lại **vẫn hiện** (hôm nay: API trả **500**, không lô nào hiện)
- **AC-35-30** vẫn đúng — mỗi thẻ lô có **đúng sáu** mắt xích

**References & Dependencies**
- Spec: `scr-35-truy-xuat-nguon-goc.md` §6.3 #1…#17 · §6.4.1…§6.4.9
- Estimate LAB-1: F08 — 60 SP / 35 MD

---

#### `[STORY]` US-19 — Quality manager traces a lot both ways in one search

**Overview**
- **Who:** `品質管理`, `監査者`
- **What:** tìm theo 5 cách, mỗi lô hiện một chuỗi sáu mắt xích
- **Why:** FR-TRC-01 (P0) — thu hồi bắt đầu từ đây

**Acceptance Criteria**
- **AC-35-15**…**AC-35-23** — năm cách tìm; `lot_code` khớp một phần không phân biệt hoa thường;
  `%` so như **ký tự thường**, không phải ký tự đại diện
- **AC-35-10** / **AC-35-11** — không khớp thì **200 + `lots: []`**, không phải 404
- **AC-35-30** — Given một lô bất kỳ · Then **đúng sáu** mắt xích
- **AC-35-31**…**AC-35-36** — mắt xích đứt có nghĩa riêng, khác mắt xích rỗng
- **AC-35-38** — Given bất kỳ sự kiện nào · Then hai dòng cuối có `関連: ロット…`
- **AC-35-43** / **AC-35-44** — **đúng 30** lô thì `truncated: false`; **31 trở lên** thì `true`
- **AC-35-45** — Given kết quả bị cắt · When tìm nút sang trang · Then **không có nút nào** —
  màn **không** phân trang (quyết định wireframe 7.1)
- **AC-35-46** / **AC-35-47** — hai bộ lọc thu hẹp: khoảng ngày nhập và trạng thái lô
- **AC-35-59** / **AC-35-60** — ngày đảo ngược và sai định dạng đều **422**

**References & Dependencies**
- Spec: SCR-35 §6.4.3 · §6.4.5 · §6.4.7

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E11-19-BE — Make one broken lot stop breaking the whole search

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `API route` + `RPC / luật`

**Impact Range**
- `findTraceLots` · `app/api/trace/` · `LOAD`

---

##### `[DEV TASK]` E11-19-BE-01 — Skip a lot with a missing lot_state instead of failing the search

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- ⚠ **Một lô thiếu dòng `lot_state` làm hỏng CẢ lần tìm**: `findTraceLots` trả `LOT_STATE_MISSING`
  ngay tại lô đó, route đổi thành **500**, **không lô nào hiện ra**
- Comment tuyên bố rõ: thiếu `lot_state` là **dữ liệu hỏng**, không phải mắt xích đứt — nên không
  bỏ qua lô đó. **Lý do đúng, hệ quả thì không chấp nhận được**: một lô hỏng làm mù cả màn
- Hướng: vẫn báo là dữ liệu hỏng, nhưng **báo ở mức lô**, các lô khác vẫn hiện
- **AC-35-52** đảo chiều

**Impact Range**
- `FIND:95` · `FIND:55` · `app/api/trace/`

---

##### `[DEV TASK]` E11-19-BE-02 — Bound the eleven unlimited history queries

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- Mỗi lần tìm chạy tới **14 truy vấn**, trong đó **11 truy vấn lịch sử không có `.limit()` nào**,
  và `locations` được đọc **trọn bảng** mỗi lần. Chi phí tăng theo số lô, trần là 30 lô
- Comment tuyên bố chủ ý: *"history tables are read whole, nothing is cut"* — **đúng về nghiệp vụ**
  (chuỗi truy xuất không được cắt), **rủi ro về hiệu năng**
- Hai đường: đặt trần có báo, **hoặc** giữ không cắt và ghi thành quyết định kèm số đo thật
- `[tự viết]` Given 30 lô mỗi lô 500 dòng lịch sử · When tìm · Then thời gian phản hồi được đo và
  ghi lại — **có số trước khi quyết**
- Liên quan `E11-INV-02` (NFR-PERF-02)

**Impact Range**
- `LOAD:8` · `LOAD:42` · 11 truy vấn lịch sử

---

##### `[DEV TASK]` E11-19-BE-03 — Stop repeating every lot of an order inside each lot chain

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- Sự kiện `ピッキング確認`/`積込確認` in **toàn bộ** danh sách lô của đơn vào `detail` của **mọi**
  lô — xem lô A **vẫn thấy dòng của lô B**. Một đơn chia 5 lô thì mỗi chuỗi lặp cùng một khối chữ
- `entries` là jsonb ở mức đơn, không ở mức lô → phải lọc khi dựng chuỗi
- **AC-35-56** — Given đơn gồm nhiều lô · When xem chuỗi của lô A ở mắt xích `積込/出荷` ·
  Then chỉ thấy phần của lô A

**Impact Range**
- `DOWN:16, 22`

---

#### `[PARENT][FE]` E11-19-FE — Give the search a way to narrow and messages that differ

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `VIEW:128` · `FORM:28`

---

##### `[DEV TASK]` E11-19-FE-01 — Build the two narrowing filters above the 30-lot ceiling

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Màn **chỉ có một ô tìm**. Trần 30 lô đã có lời nhắc `条件を絞り込んでください` nhưng **không có
  công cụ nào để thu hẹp** ngoài việc gõ thêm ký tự
- **Wireframe 7.1 đã quyết: KHÔNG phân trang**, thay bằng hai bộ lọc thu hẹp
- **AC-35-46** — Given khối thu hẹp · When đặt `入荷日（開始）` · Then kết quả thu hẹp đúng
- **AC-35-47** — Given ô `状態` chọn `隔離` · Then chỉ lô cách ly
- **AC-35-45** vẫn đúng — **không** nút sang trang
- 4 câu `M_69`–`M_72` và 3 nhãn riêng của màn **spec đã soạn xong**, chỉ cần người bản ngữ duyệt

**Impact Range**
- Khối thu hẹp SCR-35 · `_common/thong-bao-ja.md` (`M_69`–`M_72`)

---

##### `[DEV TASK]` E11-19-FE-02 — Split the 401, 409 and 500 messages

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- **401, 409 và 500 rơi chung một câu** — người dùng không phân biệt được *"hệ thống hỏng"* với
  *"phiên hết hạn"*
- Cộng: tham số lạ trong query string làm `.strict()` từ chối, câu trả về là **tiếng Anh mặc định
  của zod** `Unrecognized key: "x"` → dùng `M_52`
- **AC-35-48**…**AC-35-51** — mạng hỏng · 403 · 500 · 401, bốn câu khác nhau; 401 chuyển `/login`
- **AC-35-29** — Given `?extra=1` · Then **422** với câu tiếng Nhật
- **Cùng một sửa đổi với** `E06-01-FE-02` · `E07-26-FE-03` · `E08-06-FE-02` · `E09-09-FE-04` —
  **năm màn, một việc**

**Impact Range**
- `FORM:28` · `Z:17` · `_common/thong-bao-ja.md` (`M_52`, `M_53`)

---

#### `[STORY]` US-32 — Internal lot lanes link back to the partner that supplied them

**Overview**
- **Who:** `品質管理`
- **What:** làn truy xuất (`beef` / `rice` / `none`) là ràng buộc thật, và mã luôn đi kèm tên đối tác
- **Why:** BR-TRACE-03 — thu hồi phải đi được từ lô nội bộ tới liên kết đối tác

**Acceptance Criteria**
- **AC-35-22** — Given `kind=beef_id` và `q=1234567890` · Then ra **đúng một** lô
- **AC-35-26** / **AC-35-27** / **AC-35-28** — mã bò phải đúng 10 chữ số, cắt khoảng trắng hai đầu
- **AC-35-42** — Given bất kỳ chỗ nào in mã khách · Then **tên khách đứng ngay sau mã**
- **AC-35-40** — Given `LT-BEF-1` (dòng lịch sử giao không có đơn) · Then vẫn truy được tới đối tác
- **AC-35-54** / **AC-35-55** — Given lô làn `beef` nhận vào `隔離` vì **thiếu mã cá thể** ·
  When tìm theo `beef_id` · Then màn nói rõ vì sao không tìm thấy

**References & Dependencies**
- Spec: SCR-35 §6.3 #1 #2 #8 · §6.4.6 · BR-TRACE-02 (tr.40)

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E11-32-BE — Make the trace lane a real constraint and keep the cattle id

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `RPC / luật` + `DB (migration)`

**Impact Range**
- `trace_lane` · `lots.beef_individual_id` · `app/api/trace/`

---

##### `[DEV TASK]` E11-32-BE-01 — Validate the search kind against the SKU trace lane

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật`

**Specification**
- Enum `trace_lane` **tồn tại** nhưng **luồng truy xuất không đọc nó**: 5 cách tìm khai riêng,
  **không nối về enum**
- ⚠ Hệ quả hôm nay: **nhập mã cá thể bò cho một SKU làn gạo không bị chặn ở tầng nào**
- Cùng gốc với `E06-01-BE-02` (SCR-12 cũng không kiểm làn ở RPC) — **hai màn, một lỗ hổng**
- `[tự viết]` Given SKU làn `rice` · When gán mã cá thể bò · Then bị chặn ở tầng dữ liệu

**Impact Range**
- `TYPES:8` · `MASTER:19` · `ENUM:50-54` · `receive_line`

---

##### `[DEV TASK]` E11-32-BE-02 — Keep the cattle id on a quarantined beef lot

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật`

**Specification**
- **BR-TRACE-02** đòi truy được một cá thể bò từ mã của nó, trả về **toàn bộ giao dịch liên quan**
  — **đây là ca nghiệp vụ mà truy xuất tồn tại để phục vụ** (thu hồi thịt bò)
- Một lô làn `beef` nhập **thiếu** mã cá thể bị đưa vào `隔離` ngay lúc nhập, **nhưng cột
  `lots.beef_individual_id` để trống** → lô đó **không bao giờ truy được** bằng mã bò
- **AC-35-54** — ghi lại hiện trạng này
- **AC-35-55** — Given kết quả rỗng và `kind=beef_id` · Then màn nói rõ nguyên nhân có thể là lô bị
  cách ly vì thiếu mã

**Impact Range**
- `lots.beef_individual_id` · `receive_line` · SCR-12 (E06)

---

#### `[PARENT][FE]` E11-32-FE — Show the partner behind every code

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Impact Range**
- `DOWN:78` · `VIEW:20`

---

##### `[DEV TASK]` E11-32-FE-01 — Print the customer and supplier name next to every code

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- **US-19 AC2** đòi kết quả có **quan hệ**; **US-32 AC2** đòi tìm recall đi được từ lô tới liên
  kết đối tác
- Chuỗi chỉ in **mã khách** — **không có tên khách ở đâu**. Người đọc phải tự tra mã
- Cộng: nếu embed `skus` hoặc `suppliers` không về, `toSummary` để các trường thành **chuỗi rỗng**
  — thẻ lô hiện tiêu đề thiếu chữ, **không báo gì**. Khác hẳn `lot_state` vốn thiếu là lỗi
- **AC-35-42** — Given bất kỳ chỗ nào in mã khách · Then tên đứng ngay sau mã
- `[tự viết]` Given embed `skus` không về · When thẻ render · Then màn **báo** thay vì để trống

**Impact Range**
- `DOWN:78` · `VIEW:20` · `FIND:60-63`

---

#### `[STORY]` US-20 — Quality manager opens a recall case straight from a trace result

**Overview**
- **Who:** `品質管理`
- **What:** từ kết quả truy xuất, mở hồ sơ thu hồi và đối chiếu số lượng
- **Why:** FR-TRC-02 (P0) — **không phủ** trong v6

**Acceptance Criteria**
- **AC-35-57** — Given `SCR-36` vẫn `enabled: false` · Then nút `回収ケース作成` **không** hiện
- **AC-35-58** — Given `SCR-36` được bật · When `品質管理` xem kết quả · Then nút hiện và dẫn
  sang hồ sơ thu hồi mang theo tập lô
- `[tự viết]` Given một tập lô đã truy ra · When mở hồ sơ thu hồi · Then hồ sơ nhận đủ mã lô,
  số lượng và danh sách khách đã nhận

**References & Dependencies**
- Spec: SCR-35 §6.3 #13 · §6.4.9 · `MENU:52`
- ⚠ Nút `回収ケース作成` **có trong code** nhưng **không bao giờ hiện** vì SCR-36 `enabled: false`
- Phụ thuộc `E11-INV-01`

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E11-20-BE — Prepare the recall hand-off contract

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `API route`

**Impact Range**
- `app/api/trace/` · SCR-36 (chưa bật)

---

##### `[DEV TASK]` E11-20-BE-01 — Define what a recall case receives from a trace result

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` · **Phụ thuộc:** `E11-INV-01`

**Specification**
- Chốt hợp đồng dữ liệu giữa SCR-35 và SCR-36: tập lô, số lượng, danh sách khách đã nhận
- `[tự viết]` Given kết quả truy xuất của một lô · When chuyển sang hồ sơ thu hồi · Then hồ sơ
  nhận đủ ba thứ trên, **không** phải truy lại từ đầu
- ⚠ Chỉ làm được sau khi `E11-INV-01` chốt SCR-36 có trong phạm vi hay không

**Impact Range**
- Hợp đồng dữ liệu SCR-35 → SCR-36

---

#### `[PARENT][FE]` E11-20-FE — Make the recall button reachable

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 1 dev task con)
- **Tầng:** `UI`

**Impact Range**
- `VIEW:104-108` · `MENU:52`

---

##### `[DEV TASK]` E11-20-FE-01 — Show the recall button only when SCR-36 is enabled

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E11-20-BE-01`

**Specification**
- Nút đã có trong code, chỉ không hiện. Việc của LAB-5: nối nút với màn khi SCR-36 bật, và **giữ
  nút ẩn** khi chưa bật — không để nút dẫn tới 404
- **AC-35-57** / **AC-35-58**

**Impact Range**
- `VIEW:104-108`

---

#### `[INVESTIGATION]` E11-INV-01 — Confirm whether SCR-36 recall management is in scope

**Overview**
- **US-20 / FR-TRC-02 (P0)** đòi mở hồ sơ thu hồi và đối chiếu số lượng ngay sau khi truy ra lô
- Nút `回収ケース作成` **có trong code** nhưng **không bao giờ hiện** vì SCR-36 `enabled: false`.
  Màn truy xuất **dừng ở chỗ hiện kết quả**
- **Hỏi khách:** SCR-36 có trong phạm vi lần này không
- **Giả định vendor:** chưa — nằm ngoài 15 màn
- **Mức đổi:** có → **một màn mới**, cộng bảng hồ sơ thu hồi và luồng đối chiếu số lượng. **Lớn**
- ⚠ Đây là **P0 không phủ** — phải nêu rõ trong bài nộp, không để lẫn vào nợ nhỏ

**References**
- SCR-35 §6.3 #13 · `MENU:52`

---

#### `[INVESTIGATION]` E11-INV-02 — Confirm the 60-second trace target and who supplies the test dataset

**Overview**
- **US-19 AC4 / NFR-PERF-02** đòi truy xuất dữ liệu **3 năm** xong trong **≤ 60 giây**, đo trên
  **300.000 dòng giao hàng** và **2,5 triệu giá trị đo nhiệt độ**
- **Không đo, không có bộ dữ liệu kiểm thử ở quy mô đó.** Seed hiện tại là **vài chục dòng mỗi bảng**
- AC này **bị cắt khỏi phạm vi v6** có tuyên bố
- **Hỏi khách:** ai cấp bộ dữ liệu ở quy mô thật để đo, và đo vào lúc nào trong dự án
- **Mức đổi:** phải đo → cần sinh dữ liệu giả 3 năm, cộng việc tối ưu 11 truy vấn của
  `E11-19-BE-02`. **Lớn**

**References**
- SCR-35 §6.3 #4 #10 · NFR-PERF-02 (tr.58)

---

### E12 · Nền tảng dùng chung & phân quyền

| | |
|---|---|
| **Màn** | SCR-00 (16 dòng 6.3) + xuyên màn |
| **Nhóm LAB-1 đối chiếu** | C · D · F11 — 297 SP / 159 MD |
| **Số item** | 1 epic + 2 story + 4 parent + 10 dev task + 3 investigation = **20** |

⚠ **Hai dev task của epic này được các epic khác viện dẫn** — `app/error.tsx` và
`app/not-found.tsx` (`E07-05-FE-02`), và **bảng mã lỗi gom chung** `E12-ST-BE-01` — task này **thay
hẳn** hai task đăng ký mã lỗi từng dự kiến ở E08 và E09, cộng phần mã 413 của `E10-15-BE-04`.

```
[EPIC] E12 Build the shared app shell, error boundaries and role surface
├── [STORY] US-31 Pending work reaches the right person instead of waiting on a screen
│   ├── [PARENT][BE] E12-31-BE Build the notification path the RFP asks for
│   │   ├── E12-31-BE-01 Build a queued, retrying notification dispatcher
│   │   └── E12-31-BE-02 Add the alarm and deviation counters quality control actually needs
│   └── [PARENT][FE] E12-31-FE Make the home cards tell the truth about pending work
│       ├── E12-31-FE-01 Stop swallowing home count errors
│       ├── E12-31-FE-02 Add the two missing quality-control cards
│       └── E12-31-FE-03 Reserve space for the cards so the grid stops jumping
└── [STORY] E12-ST Shared shell behaves the same on every screen
    ├── [PARENT][BE] E12-ST-BE Unify the error catalogue and the role-to-screen map
    │   ├── E12-ST-BE-01 Publish one error catalogue covering DB codes and route codes
    │   ├── E12-ST-BE-02 Derive the home cards from the role menu instead of a second array
    │   └── E12-ST-BE-03 Fix the SCR-19 menu href and enable the screens LAB-5 builds
    └── [PARENT][FE] E12-ST-FE Build the shared boundaries every screen is missing
        ├── E12-ST-FE-01 Build app-wide error.tsx and not-found.tsx in Japanese
        ├── E12-ST-FE-02 Tell an account with no profile row what to do
        └── E12-ST-FE-03 Fix the duplicated heading and unlabelled card numbers
[INVESTIGATION] E12-INV-01 Confirm whether per-warehouse and per-person access control is required
[INVESTIGATION] E12-INV-02 Confirm which wave-2 and wave-3 screens belong to this release
[INVESTIGATION] E12-INV-03 Record the three deliberate read-permission gaps as written decisions
```

---

#### `[EPIC]` E12 — Build the shared app shell, error boundaries and role surface

**Overview & Goal**
- As a người dùng bất kỳ trong bảy vai
- I want khung ứng dụng cư xử giống nhau ở mọi màn, và việc chờ tới được đúng người
- So that không ai gặp trang lỗi tiếng Anh, và không việc nào nằm chờ mà không ai biết

**Scope & Features**
- `app/error.tsx` và `app/not-found.tsx` — **cả hai đều chưa có**
- Một **bảng mã lỗi duy nhất** gồm 42 mã DB cộng các mã tầng route
- Thẻ việc chờ trên trang chủ: **không nuốt lỗi đếm**, và thêm hai thẻ `品質管理` đang thiếu
- Đường thông báo (**IF-MAIL-01**) — hôm nay **không gửi mail**, việc chờ chỉ hiện ở trang chủ

**Ngoài phạm vi**
- Bật các màn wave 2 / wave 3 (master, kiểm toán) → `E12-INV-02`
- Siết quyền theo kho / theo người → `E12-INV-01` (cùng câu với `E07-INV-01`, `E09-INV-04`)

**Acceptance Criteria**
- Toàn bộ story và dev task con đã đóng
- **AC-00-47** — Given mở một URL không tồn tại · Then hiện câu tiếng Nhật
  `お探しの画面は見つかりません…`, **không** phải trang mặc định của Next.js
- **AC-00-44** đảo chiều — Given `GET /api/home/summary` trả 500 · Then khối thẻ **không** biến mất
  im lặng

**References & Dependencies**
- Spec: `scr-00-home-trang-chu.md` §6.3 #1…#16 · §6.4.1…§6.4.7 ·
  `01-architecture.md` §9.1 · §12
- Estimate LAB-1: C · D · F11 — 297 SP / 159 MD
- **Cung cấp cho:** `E07-05-FE-02` · `E08-07-FE-01` · `E09-10-FE-01` · `E10-15-BE-04` · `E10-18-FE-03`

---

#### `[STORY]` US-31 — Pending work reaches the right person instead of waiting on a screen

**Overview**
- **Who:** cả bảy vai, rõ nhất là `品質管理`
- **What:** việc chờ được thông báo chủ động, không chỉ hiện trên trang chủ khi người ta nhớ mở
- **Why:** IF-MAIL-01 đòi mail relay **theo từng sự kiện**, retry theo hàng đợi, **không được hỏng
  im lặng**

**Acceptance Criteria**
- **AC-00-27**…**AC-00-31** — con số trên thẻ khớp đúng số dòng trong DB cho từng vai
- **AC-00-32** — Given cùng bộ dữ liệu · Then hai vai thấy con số nhất quán
- **AC-00-35** — Given một truy vấn đếm trả `count = null` · Then thẻ tương ứng xử lý được
- **AC-00-36** — Given **một** trong hai truy vấn đếm lỗi · Then màn nói rõ, không ẩn cả khối
- **AC-00-42** / **AC-00-43** — 403/409/500 và mạng hỏng: màn **nói ra**, không im lặng
- **AC-00-52** — Given cuộn xuống chân trang chủ · Then nhãn mock `メール通知` hiện ra
- `[tự viết]` Given một cảnh báo nhiệt mới sinh · When hàng đợi thông báo chạy · Then có một lần
  gửi, và lần gửi hỏng được thử lại — **không hỏng im lặng**

**References & Dependencies**
- Spec: SCR-00 §6.3 #1 #4 #5 · §6.4.4 · §6.4.6 · IF-MAIL-01 (`rfp-vi.md:1082`)
- ⚠ **M7** là mock — xem **E13**

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E12-31-BE — Build the notification path the RFP asks for

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `API route` + `DB (migration)`

**Impact Range**
- Bảng hàng đợi thông báo (mới) · `app/api/home/summary/`

---

##### `[DEV TASK]` E12-31-BE-01 — Build a queued, retrying notification dispatcher

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `API route`

**Specification**
- **Không gửi mail.** Việc chờ **chỉ** hiện ở trang chủ; chân trang nói thẳng đây là mock
- IF-MAIL-01 đòi: gửi **theo từng sự kiện** (alarm, phê duyệt, báo cáo), **retry theo hàng đợi**,
  **không được hỏng im lặng**. US-31 thêm yêu cầu thông báo **có phiên bản và người duyệt**
- `[tự viết]` Given một sự kiện cần thông báo · When hàng đợi chạy · Then có một dòng hàng đợi,
  một lần gửi, và trạng thái gửi ghi lại được
- `[tự viết]` Given lần gửi hỏng · When thử lại · Then số lần thử ghi lại, và **không** hỏng im lặng
- ⚠ Phụ thuộc **M7** — xem `E13`

**Impact Range**
- Bảng hàng đợi thông báo (mới) · `events`

---

##### `[DEV TASK]` E12-31-BE-02 — Add the alarm and deviation counters quality control actually needs

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route`

**Specification**
- ⚠ Trang chủ của `品質管理` có **đúng một thẻ**, và nó đếm **lô cách ly** — **không** đếm cảnh
  báo chưa xác nhận (**US-17**, hạn 15 phút) và **không** đếm hồ sơ sai lệch đang mở (**US-18**)
- Tức là người có hạn **15 phút** để xử lý lại **không có thẻ nào nhắc việc đó**
- **AC-00-31** vẫn đúng cho thẻ lô cách ly
- `[tự viết]` Given có n cảnh báo chưa xác nhận và m hồ sơ sai lệch chưa đóng · When `品質管理`
  mở `/` · Then hai thẻ mới hiện đúng hai con số
- **AC-00-40** — Given một lượt tới `/` · Then số truy vấn đếm không phình quá mức đã đo

**Impact Range**
- `COUNT:34-45` · `app/api/home/summary/` · `temperature_alarms` · `deviations`

---

#### `[PARENT][FE]` E12-31-FE — Make the home cards tell the truth about pending work

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `CARDS:13-25` · `COUNT:34-45`

---

##### `[DEV TASK]` E12-31-FE-01 — Stop swallowing home count errors

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- ⚠ **Lỗi đếm bị nuốt im lặng.** Máy chủ trả 403 / 500 / 409, hoặc mạng hỏng → `CARDS:16-18` chỉ
  nhận khi `result.ok`, **khối thẻ biến mất**
- Người dùng **không phân biệt được "không có việc chờ" với "đếm hỏng"** — và với một hàng đợi
  có hạn 15 phút, đây là chỗ hỏng nguy hiểm
- **AC-00-16** — Given `summary` trả 500 · Then tiêu đề `未処理の業務` **vẫn hiện** kèm câu lỗi
- **AC-00-42** / **AC-00-43** — 403/409/500 và mạng hỏng đều nói ra
- **AC-00-44** đảo chiều — ghi lại hiện trạng hôm nay
- **AC-00-45** — Given 401 · Then chuyển `/login`

**Impact Range**
- `CARDS:16-18` · `CLIENT:51`

---

##### `[DEV TASK]` E12-31-FE-02 — Add the two missing quality-control cards

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E12-31-BE-02`

**Specification**
- Thêm thẻ cảnh báo chưa xác nhận và thẻ hồ sơ sai lệch đang mở cho vai `品質管理`
- ⚠ Chú thích ghi **"at most 3"** thẻ mỗi vai, nhưng `CARDS_BY_ROLE` tối đa **2** — lưới ba cột
  **luôn chừa một cột trống**. Thêm hai thẻ này làm `品質管理` thành **3 thẻ**, đúng với chú thích
- **AC-00-11** vẫn đúng — không lô cách ly nào thì thẻ hiện 0, không ẩn
- `[tự viết]` Given `品質管理` có cả ba thẻ · When mở `/` · Then lưới ba cột đầy, không cột trống

**Impact Range**
- `CARDS_BY_ROLE` (`COUNT:34-45`) · `SUMMARY:7` · `CARDS:8`

---

##### `[DEV TASK]` E12-31-FE-03 — Reserve space for the cards so the grid stops jumping

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Khối thẻ chèn vào **sau** khi fetch xong và **đẩy lưới ô menu xuống**; không skeleton, không ô
  giữ chỗ. Vì gọi API **mỗi lần** tới trang chủ nên **lưới nhảy chỗ mỗi lần**
- Dựng ô giữ chỗ theo S2: n ô xám cao bằng thẻ
- **AC-00-09** — Given vai có thẻ và `summary` chưa về · Then có ô giữ chỗ, lưới **không** nhảy
- **AC-00-38** / **AC-00-39** — Given quay lại trang chủ · Then số đếm nạp lại, lưới vẫn ổn định

**Impact Range**
- `CARDS:13, 21`

---

#### `[STORY]` E12-ST — Shared shell behaves the same on every screen

> ⚠ **Story này không có mã US trong spec.** Nó được dựng từ chính các dev task con — bốn chỗ hở
> của khung ứng dụng mà **mọi màn đều chạm** nhưng **không màn nào sở hữu**. Ghi rõ là story kỹ
> thuật để bảng đối chiếu `estimate.md` không đi tìm một US không tồn tại.

**Overview**
- **Who:** cả bảy vai
- **What:** trang lỗi, trang 404, bảng mã lỗi và bản đồ vai–màn **nhất quán trên toàn ứng dụng**
- **Why:** hôm nay mỗi màn tự xử một kiểu, và hai trang lỗi dùng chung thì **chưa tồn tại**

**Acceptance Criteria**
- **AC-00-47** — Given mở URL không tồn tại · Then câu tiếng Nhật, có khung ứng dụng, có đường
  quay lại
- **AC-00-46** — Given tra bảng `profiles` hỏng · Then trang **500** với câu tiếng Nhật
- **AC-00-08** — Given URL của màn `enabled: false` · Then **404**, không phải 403
- **AC-00-04** / **AC-00-05** / **AC-00-48** — tài khoản **không có dòng `profiles`**: trang 403,
  header hiện email, thanh điều hướng **nói rõ phải làm gì**
- **AC-00-24** — Given sáu vai non-driver · Then `ロット状態` **không** xuất hiện trong menu
- **AC-00-25** / **AC-00-26** — mục `ホーム` nhất quán giữa thanh điều hướng và lưới ô
- **AC-00-54** — Given khối `未処理の業務` có thẻ · When đọc bằng trình đọc màn hình · Then
  **không** đọc trùng tiêu đề, và số trên thẻ **có nhãn trợ năng**

**References & Dependencies**
- Spec: SCR-00 §6.3 #2 #3 #9 #10 #11 #12 #14 · §6.4.3 · §6.4.6 · §6.4.7 ·
  `01-architecture.md` §12 mục 1 #2 #3
- ⚠ Cung cấp hai trang lỗi cho `E07-05-FE-02` và `E10-18-FE-03`

**Technical Approach**
- [x] Frontend
- [x] Backend

---

#### `[PARENT][BE]` E12-ST-BE — Unify the error catalogue and the role-to-screen map

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `API route` + `dùng chung`

**Impact Range**
- Danh mục mã lỗi · `ROLE_MENU` · `CARDS_BY_ROLE` · `MENU`

---

##### `[DEV TASK]` E12-ST-BE-01 — Publish one error catalogue covering DB codes and route codes

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` + `dùng chung`

**Specification**
- Ánh xạ lỗi đi theo **tiền tố**, không theo bảng tra — và **giá phải trả là mã sai tiền tố im
  lặng thành 500**
- Có **ít nhất bảy mã tầng route** nằm ngoài 42 mã DB: `RULE_BUSINESS_REVIEW` ·
  `RULE_INSUFFICIENT_STOCK` (E08) · `RULE_PICK_BLOCKED` · `RULE_LOAD_BLOCKED` ·
  `RULE_DISPATCH_BLOCKED` (E09) · `LOGGER_FILE_TOO_LARGE` (E10) · `LOT_STATE_MISSING` (E07)
- Chúng **viết hoa như mã DB nhưng không phải mã DB**. Người đọc danh mục 42 mã sẽ kết luận chúng
  **không tồn tại**
- `[tự viết]` Given danh mục mã lỗi · When rà · Then mọi mã mà API có thể trả đều nằm trong đó,
  kèm tầng sinh ra nó và mã HTTP
- ⚠ Task này **thay hẳn** hai task đăng ký mã lỗi từng dự kiến ở E08 và E09 (đã xoá khỏi backlog),
  cộng phần mã 413 của `E10-15-BE-04`. Gom một chỗ, không rải ba epic

**Impact Range**
- Danh mục mã lỗi (mới) · `mapRpcError` · `MAP:27-33`

---

##### `[DEV TASK]` E12-ST-BE-02 — Derive the home cards from the role menu instead of a second array

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `dùng chung`

**Specification**
- `CARDS_BY_ROLE` và `ROLE_MENU` là **hai mảng độc lập**; thẻ **không suy ra từ menu**
- Hôm nay năm `href` của thẻ đều trỏ tới màn mà vai có trong menu — **đã đối chiếu từng cặp**.
  Nhưng **sửa một bên mà quên bên kia** thì thẻ trỏ tới màn vai **không mở được**
- `[tự viết]` Given một vai bất kỳ · When so `CARDS_BY_ROLE` với `ROLE_MENU` · Then mọi `href` của
  thẻ đều nằm trong menu của vai đó — kiểm tự động, không kiểm bằng mắt

**Impact Range**
- `COUNT:34` · `MENU:26`

---

##### `[DEV TASK]` E12-ST-BE-03 — Fix the SCR-19 menu href and enable the screens LAB-5 builds

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `dùng chung`

**Specification**
- Mục `SCR-19 ロット状態` khai `href: '/lots'` nhưng **chỉ tồn tại** `[lotId]/page.tsx`. Link hỏng,
  và nó nằm **trong chính mảng dữ liệu mà trang chủ dựng menu từ đó**. `navHidden: true` che đi
- Sửa `href` thành `/inventory` hoặc bỏ hẳn mục — theo `E07-INV-04`
- Lật `enabled: true` cho **SCR-28** và **SCR-29** khi E01/E03 xong: `配送計画者` từ 4 mục thành 5
  và lưới từ 3 ô thành 4 ô; SCR-29 `navHidden` nên **chỉ SCR-28 hiện**
- **AC-00-20** — Given vai `配送計画者` · Then thanh điều hướng đúng số mục sau khi bật
- **AC-00-24** vẫn đúng — `ロット状態` không xuất hiện

**Impact Range**
- `MENU:31` · `MENU:46-47`

---

#### `[PARENT][FE]` E12-ST-FE — Build the shared boundaries every screen is missing

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 3 dev task con)
- **Tầng:** `UI` + `dùng chung`

**Impact Range**
- `app/error.tsx` · `app/not-found.tsx` · `LAYOUT:19-26` · `CARDS:24-25`

---

##### `[DEV TASK]` E12-ST-FE-01 — Build app-wide error.tsx and not-found.tsx in Japanese

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- `app/` **không có `not-found.tsx` lẫn `error.tsx`**. Gõ URL của 1 trong 10 màn chưa bật ra trang
  404 **mặc định của Next, tiếng Anh**; lỗi máy chủ ra trang lỗi mặc định, cũng tiếng Anh, và
  **không có khung ứng dụng nên không có đường quay lại**
- **AC-00-47** — Given URL không tồn tại · Then câu tiếng Nhật đúng
- **AC-00-08** — Given URL của màn `enabled: false` · Then **404**, không phải 403
- **AC-00-46** — Given tra `profiles` hỏng · Then **500** với câu tiếng Nhật
- ⚠ **Hai trang này phục vụ cả ứng dụng** — `E07-05-FE-02` (SCR-19) và `E10-18-FE-03` (SCR-33)
  **dùng lại**, không dựng riêng

**Impact Range**
- `app/error.tsx` · `app/not-found.tsx` · mục 4.2.4

---

##### `[DEV TASK]` E12-ST-FE-02 — Tell an account with no profile row what to do

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` + `dùng chung`

**Specification**
- Tài khoản có phiên mà **không có dòng `profiles`**: `items = []` → `<ul>` rỗng. Trang trả 403 và
  câu 403 bảo *"mở từ menu trang chủ"* **trong khi menu trống** — chỉ dẫn mâu thuẫn với hiện trạng
- Thêm dòng **`M_59`** vào thanh điều hướng rỗng
- Cộng: **hai nguồn tên người dùng** — header dùng `auth?.displayName ?? email`, nội dung trang
  dùng `displayName` của `requirePageRole`. Tài khoản không có profile thì header hiện email còn
  nội dung trang là 403. **Giữ nguyên** (`profiles` không lưu email là lệch có chủ đích), nhưng
  ghi thành quyết định
- **AC-00-04** / **AC-00-05** / **AC-00-48**

**Impact Range**
- `LAYOUT:26` · `LAYOUT:19` · `_common/thong-bao-ja.md` (`M_59`)

---

##### `[DEV TASK]` E12-ST-FE-03 — Fix the duplicated heading and unlabelled card numbers

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Khối thẻ mang `aria-label="未処理の業務"` **và** `<h2>未処理の業務</h2>` — **cùng một chữ ở hai
  chỗ, trình đọc màn hình đọc hai lần**. Số trên thẻ **không có nhãn trợ năng**
- **AC-00-54** — Given khối có thẻ · When đọc bằng trình đọc màn hình · Then không đọc trùng, và
  mỗi số có nhãn
- **AC-00-50** / **AC-00-51** — nhãn trợ năng của thanh điều hướng, và bố cục dưới ngưỡng `md`

**Impact Range**
- `CARDS:24-25`

---

#### `[INVESTIGATION]` E12-INV-01 — Confirm whether per-warehouse and per-person access control is required

**Overview**
- **NFR-SEC-02** đòi quyền tối thiểu **theo vai và theo người**; **US-26 AC2** đòi *"tôn trọng
  quyền theo kho"*
- Hôm nay **RLS lược còn hai nhóm** (tài xế / không phải tài xế), lọc theo **dòng**, không theo
  **cột** và không theo **người**. **Lệch có chủ đích, đã ghi vết 4 chỗ** — code làm **đúng thiết
  kế**, thứ nó lệch là **yêu cầu khách**
- Ba hệ quả cụ thể đã đo được:
  - sáu vai non-driver **thấy mọi lô ở mọi kho** (`E07-INV-01`)
  - **mọi tài xế thao tác được trên mọi đơn** của bước mình (`E09-INV-04`)
  - **tài xế đọc được `orders.seal_no`** qua API dù UI đã giấu — Postgres RLS **không lọc được
    theo cột**
- **Mức đổi:** Lớn — chạm RLS của nhiều bảng, và cần cột người phụ trách
- ⚠ **Gộp ba câu hỏi rải ở E07, E09 và đây thành MỘT câu gửi khách** — chúng cùng một gốc

**References**
- SCR-00 §6.3 #8 · SCR-18 §6.3 #2 · SCR-24 §6.3 #2 #9 · SCR-26 §6.3 #22 ·
  `00-context/README.md` §5.2

---

#### `[INVESTIGATION]` E12-INV-02 — Confirm which wave-2 and wave-3 screens belong to this release

**Overview**
- `マスター管理者` mở được **đúng một màn**; `監査者` mở được **hai**. Bốn màn master và hai màn
  kiểm toán đều `enabled: false` — **wave 2 và wave 3 bị cắt khỏi phạm vi v6**
- Hệ quả đo được: `監査者` **đọc được dữ liệu ở tầng DB nhưng không có màn nào để đọc** — việc
  này lặp ở SCR-21 (`evidence`), SCR-29 (`route_versions`), SCR-32 (`temperature_alarms`),
  SCR-33 (`deviations`)
- **Hỏi khách:** màn nào trong wave 2 / wave 3 vào phạm vi lần này
- **Giả định vendor:** không màn nào — giữ nguyên 15 màn
- **Mức đổi:** Lớn — mỗi màn bật thêm là một epic mới

**References**
- SCR-00 §6.3 #8 · `MENU:38-40, 49-51` · SCR-29 §6.3 #12 · SCR-33 §6.3 #9

---

#### `[INVESTIGATION]` E12-INV-03 — Record the three deliberate read-permission gaps as written decisions

**Overview**
- Ba chỗ **vai không mở được màn vẫn đọc được dữ liệu** qua PostgREST, cả ba **đúng nghiệp vụ**
  nhưng **chưa ai ghi lại là cố ý**:
  - `品質管理` và `監査者` đọc được **ảnh `receiving/`** dù không mở được `/receiving` (E06)
  - năm vai không liên quan lập tuyến đọc được **tuyến NHÁP** (E01)
  - bốn vai không mở được SCR-35 đọc được **từng bảng của chuỗi truy xuất**, trong đó có
    `loading_checks.seal_no` và `profiles.display_name` (E11)
- **Khuyến nghị:** giữ nguyên, nhưng **ghi thành quyết định có văn bản** thay vì để ngầm — đọc
  code hai màn cạnh nhau sẽ tưởng một trong hai sai
- **Không sinh dòng code nào** — tầng `không code`

**References**
- SCR-12 §6.3 #14 · SCR-28 §6.3 #12 · SCR-35 §6.3 #14 · `01-architecture.md` §6

---

### E13 · Điểm tích hợp ngoài, mở từ mock M1–M8

| | |
|---|---|
| **Nguồn** | `01-architecture.md` §9.1 (8 mock) · §12 |
| **Nhóm LAB-1 đối chiếu** | F10 — 47 SP / 27 MD |
| **Số item** | 1 epic + 1 story + 2 parent + 8 dev task + 2 investigation = **14** |

⚠ **Epic này không bám màn nào.** Mỗi dev task là **một điểm nối ra ngoài hệ** mà prototype đang
thay bằng mock. Tám mock đều **có nhãn trên màn** (trừ M4 và M8), nên người dùng biết đó là giả lập.

⚠ **Story kỹ thuật, không có mã US.** Dựng từ chính tám dev task con — mỗi mock là một điểm nối,
không mock nào thuộc về một user story riêng. Ghi rõ để bảng đối chiếu không đi tìm US không tồn tại.

```
[EPIC] E13 Replace the eight prototype mocks with real integration points
└── [STORY] E13-ST Each mocked boundary becomes a real integration with its own failure handling
    ├── [PARENT][BE] E13-ST-BE Build the seven server-side integration points
    │   ├── E13-ST-BE-01 Replace demo auth with the customer OIDC provider (M1)
    │   ├── E13-ST-BE-02 Accept all three logger file formats (M3)
    │   ├── E13-ST-BE-03 Replace the fixed travel-time matrix with a map API (M4)
    │   ├── E13-ST-BE-04 Build the mail relay queue (M7)
    │   ├── E13-ST-BE-05 Convert the six real customer data sources (M8)
    │   └── E13-ST-BE-06 Store a real signature image with its hash (M6)
    └── [PARENT][FE] E13-ST-FE Build the two device-side integration points
        ├── E13-ST-FE-01 Build barcode scanning on receiving and loading (M2)
        └── E13-ST-FE-02 Build the encrypted eight-hour offline POD queue (M5)
[INVESTIGATION] E13-INV-01 Confirm Q37 — the file formats of the three logger models
[INVESTIGATION] E13-INV-02 Confirm which of the eight integration points this release must cover
```

---

#### `[EPIC]` E13 — Replace the eight prototype mocks with real integration points

**Overview & Goal**
- As a đội vận hành của Yuki Cold
- I want mỗi chỗ prototype đang giả lập được nối vào hệ thật
- So that hệ chạy được ngoài môi trường demo

**Scope & Features**
- Tám mock `M1`…`M8` của `01-architecture.md` §9.1
- Mỗi điểm nối phải có: cách xử lý khi bên kia hỏng, timeout, và cách báo cho người dùng

**Ngoài phạm vi**
- Những gì mock đang che **bên trong hệ** (ví dụ chỗ lưu điểm nghỉ) → thuộc epic nghiệp vụ tương ứng

**Acceptance Criteria**
- Toàn bộ dev task con đã đóng, hoặc được ghi rõ là **ngoài phạm vi lần này** với lý do
- `[tự viết]` Given mỗi mock đã thay · When rà giao diện · Then **không** còn nhãn `モック` nào
  cho điểm đó
- **AC-20-64** vẫn đúng cho SCR-20 — màn đó **không** có nhãn mock nào

**References & Dependencies**
- `01-architecture.md` §9.1 (bảng 8 mock) · §12
- Estimate LAB-1: F10 — 47 SP / 27 MD

---

#### `[STORY]` E13-ST — Each mocked boundary becomes a real integration with its own failure handling

> ⚠ **Story kỹ thuật, không có mã US trong spec.** Nội dung dựng từ tám dev task con.

**Overview**
- **Who:** đội vận hành và người dùng cuối của từng màn có mock
- **What:** mỗi điểm nối ra ngoài có đường thật, có xử lý hỏng, có nhãn gỡ đi khi xong
- **Why:** tám mock là ranh giới giữa prototype và hệ chạy thật

**Acceptance Criteria**
- `[tự viết]` Given mỗi điểm nối · When bên kia hỏng hoặc quá hạn · Then hệ báo rõ, **không** hỏng
  im lặng, và trạng thái ghi lại được
- `[tự viết]` Given mỗi điểm nối đã thay · Then nhãn mock tương ứng được gỡ khỏi màn

**References & Dependencies**
- `01-architecture.md` §9.1 · §12
- Phụ thuộc: **M4** cần **E01** (SCR-28 chưa bật thì mock M4 chưa hiện) · **M7** cần `E12-31-BE-01`

**Technical Approach**
- [x] Frontend
- [x] Backend
- [x] Infrastructure

---

#### `[PARENT][BE]` E13-ST-BE — Build the seven server-side integration points

- **Task Type:** Development - Backend · **Task Category:** **Feature** (gom 6 dev task con)
- **Tầng:** `API route` + `DB (migration)` + `dùng chung`

**Impact Range**
- Auth · `import_logger_csv` · `travel_times` · hàng đợi thông báo · seed · `pods`

---

##### `[DEV TASK]` E13-ST-BE-01 — Replace demo auth with the customer OIDC provider (M1)

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` + `dùng chung`

**Specification**
- Hôm nay: Supabase Auth email/mật khẩu, **7 tài khoản demo**, nhãn mock ở `/login`
- Cần: **IdP OIDC của khách**, MFA cho vai đặc quyền, xác thực managed device cho tài xế,
  **phiên ngắn ở thiết bị cửa**
- `[tự viết]` Given tài khoản của khách qua OIDC · When đăng nhập · Then vai ánh xạ đúng sang
  `profiles.role`, và tài khoản **không có dòng `profiles`** rơi vào ca đã xử ở `E12-ST-FE-02`
- `[tự viết]` Given vai đặc quyền · When đăng nhập · Then MFA bắt buộc
- ⚠ Phiên ngắn ở thiết bị cửa chạm **mọi màn** — mọi ca 401 của 15 màn phải cư xử đúng

**Impact Range**
- `/login` · `profiles` · toàn bộ đường 401 của 15 màn

---

##### `[DEV TASK]` E13-ST-BE-02 — Accept all three logger file formats (M3)

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `RPC / luật` + `API route` · **Phụ thuộc:** `E13-INV-01`

**Specification**
- Hôm nay: **một** định dạng CSV mẫu, người dùng tự tải lên, nhãn mock ở `/temperature/imports`
- Cần: định dạng của **cả ba loại** `DL-A01` / `C01` / `F01`, và **quy trình lấy file từ thiết bị**
- ⚠ **Q37 chưa trả lời** — không biết ba định dạng trông thế nào
- `[tự viết]` Given tệp của mỗi loại trong ba loại · When nạp · Then parser nhận đúng, và loại
  không nhận ra thì báo rõ **loại nào**
- Chạm `E10-15-BE-04` (hai nơi đếm 5000) — parser mới phải theo cùng quy ước

**Impact Range**
- `PARSE` · `import_logger_csv` · `samples/logger/`

---

##### `[DEV TASK]` E13-ST-BE-03 — Replace the fixed travel-time matrix with a map API (M4)

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` + `DB (migration)` · **Phụ thuộc:** `E01-BE-01`

**Specification**
- Hôm nay: bảng thời gian di chuyển **cố định 56 dòng** trong seed. Mock **không hiện** vì SCR-28/29
  chưa bật
- Cần: **gọi theo batch, timeout + cache**, và **quy tắc 24 giờ** (Q16)
- ⚠ Ma trận cố định **đủ cho v6** và là lý do quyết định *"tính lại ngay"* của SCR-28 rẻ. Nối bản
  đồ thật thì phải xử lý **cache và timeout** mà RFP đã nêu là **điểm đau**
- **AC-28-13** vẫn phải đúng — thiếu một chặng thì **không** tính là 0 phút
- `[tự viết]` Given API bản đồ quá hạn · When dựng tuyến · Then màn báo rõ, **không** rơi về 0 phút

**Impact Range**
- `travel_times` · `lib/rules/driver-hours.ts` · SCR-28 (E01, E02)

---

##### `[DEV TASK]` E13-ST-BE-04 — Build the mail relay queue (M7)

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `API route` + `DB (migration)` · **Phụ thuộc:** `E12-31-BE-01`

**Specification**
- Hôm nay: **không gửi**; việc chờ hiện trên trang chủ, nhãn mock ở chân trang
- Cần: **mail relay doanh nghiệp** với **hàng đợi có retry**
- `E12-31-BE-01` dựng hàng đợi; task này nối hàng đợi đó vào relay thật
- `[tự viết]` Given relay trả lỗi · When hàng đợi chạy · Then thử lại theo chính sách, và sau n
  lần thì báo cho người vận hành — **không hỏng im lặng** (yêu cầu đích danh của IF-MAIL-01)

**Impact Range**
- Hàng đợi thông báo · cấu hình relay

---

##### `[DEV TASK]` E13-ST-BE-05 — Convert the six real customer data sources (M8)

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)`

**Specification**
- Hôm nay: seed SQL chạy lại được, ảnh mẫu sinh bằng script. Mock **không hiện** — là lớp dữ liệu
- Cần: **chuyển đổi dữ liệu thật từ 6 nguồn** của khách (F12)
- `[tự viết]` Given dữ liệu của mỗi nguồn · When chuyển đổi · Then dòng không chuyển được **có báo
  cáo riêng**, không bị bỏ im lặng
- ⚠ Liên quan `E11-INV-02`: bộ dữ liệu thật cũng là thứ cần để đo NFR-PERF-02

**Impact Range**
- Toàn bộ bảng master · seed · `E11-INV-02`

---

##### `[DEV TASK]` E13-ST-BE-06 — Store a real signature image with its hash (M6)

- **Task Type:** Development - Backend · **Task Category:** Task · **Parent:** `[PARENT][BE]`
- **Tầng:** `DB (migration)` + `RPC / luật` · **Phụ thuộc:** `E09-11-BE-03`

**Specification**
- Hôm nay: nhập tên + tick `署名確認` — **chữ ký là một ô tick**
- Cần: **ô ký trên màn cảm ứng**, lưu **ảnh chữ ký + hash**, và **sửa = phiên bản mới**
- Vế *"sửa = phiên bản mới"* chính là `E09-11-BE-03` (chuỗi supersedes cho POD) — task này thêm
  **ảnh chữ ký và hash**
- **AC-26-33** đổi — Given đơn `車上渡し` · Then khu vực bằng chứng có ô ký thật, không chỉ ô tick
- **AC-26-48** mở rộng — hash của ảnh chữ ký cũng phải khớp như hash ảnh POD

**Impact Range**
- `pods.signature_mock_checked` → cột ảnh chữ ký · `complete_pod` · Storage

---

#### `[PARENT][FE]` E13-ST-FE — Build the two device-side integration points

- **Task Type:** Development - Frontend · **Task Category:** **Feature** (gom 2 dev task con)
- **Tầng:** `UI`

**Impact Range**
- `/receiving` · `/loading` · `/pod`

---

##### `[DEV TASK]` E13-ST-FE-01 — Build barcode scanning on receiving and loading (M2)

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI`

**Specification**
- Hôm nay: **ô nhập tay + chọn từ danh sách**, nhãn mock ở `/receiving` và `/loading`
- Cần: **máy quét / camera + thư viện đọc mã**, **nhãn mã vạch trên lô**, và quy tắc *"nhập tay
  có kiểm soát"*
- ⚠ Vế **nhãn mã vạch trên lô** là việc **ngoài phần mềm** — in nhãn, dán nhãn, quy trình kho.
  Phải nêu rõ khi ước công
- `[tự viết]` Given quét một mã lô · When mã hợp lệ · Then ô điền tự động; mã không đọc được thì
  **vẫn nhập tay được**, và lần nhập tay đó **ghi lại được**
- Chạm `E06-01-FE-01` (danh sách dòng đã nhập) và `E09-09-FE-01` (bốn trần ở trình duyệt)

**Impact Range**
- Form SCR-12 · form SCR-23 · quy trình dán nhãn (ngoài phần mềm)

---

##### `[DEV TASK]` E13-ST-FE-02 — Build the encrypted eight-hour offline POD queue (M5)

- **Task Type:** Development - Frontend · **Task Category:** Task · **Parent:** `[PARENT][FE]`
- **Tầng:** `UI` · **Phụ thuộc:** `E09-11-BE-01`

**Specification**
- Hôm nay: **chỉ chạy khi có mạng**, `端末ラベル` điền cứng, nhãn mock ở `/pod`
- **US-11 AC3 / NFR-AVL-02** đòi hàng đợi POD **mã hoá, giữ tối đa 8 giờ**, đồng bộ lại **đúng
  một lần, không trùng, không xung đột**
- Cần: **IndexedDB + Service Worker**
- ⚠ *"Đồng bộ lại đúng một lần"* nối thẳng vào `AC-26-54` (hai yêu cầu POD đồng thời) và
  `AC-26-27` (gọi lại cho đơn đã POD) — **hàng đợi phải dùng cùng cơ chế chống trùng đó**
- `[tự viết]` Given tài xế ghi POD khi mất mạng · When có mạng lại · Then **đúng một** dòng `pods`
  được tạo, kể cả khi ứng dụng bị đóng mở lại giữa chừng
- `[tự viết]` Given hàng đợi quá 8 giờ · When đồng bộ · Then xử theo chính sách đã chốt, không
  mất dữ liệu im lặng

**Impact Range**
- `/pod` · IndexedDB · Service Worker · `complete_pod`

---

#### `[INVESTIGATION]` E13-INV-01 — Confirm Q37: the file formats of the three logger models

**Overview**
- Hỏi khách: định dạng file của ba loại logger `DL-A01` / `C01` / `F01`, và **quy trình lấy file
  từ thiết bị**
- **Giả định vendor:** M3 hiện chỉ nhận **một** định dạng
- **Mức đổi:** ba định dạng khác nhau → ba parser, hoặc một parser có bộ nhận dạng
- ⚠ Nếu thêm thẻ cảnh báo ở trang chủ (`E12-31-BE-02`) thì con số trên thẻ **phụ thuộc việc nạp
  được bao nhiêu loại logger**
- Chặn `E13-ST-BE-02`

**References**
- `01-architecture.md` §9.1 M3 · SCR-00 §6.3 #16

---

#### `[INVESTIGATION]` E13-INV-02 — Confirm which of the eight integration points this release must cover

**Overview**
- Tám mock có **chi phí rất khác nhau**: M8 (chuyển 6 nguồn dữ liệu) và M1 (OIDC + MFA) là hạ
  tầng; M6 (ô ký) là một component; M4 (bản đồ) phụ thuộc cả module lập lịch chưa dựng
- **Hỏi khách:** điểm nối nào bắt buộc trong lần phát hành này, điểm nào để sau
- **Giả định vendor:** chưa điểm nào — tám mock giữ nguyên tới khi khách chốt
- **Mức đổi:** mỗi điểm bật thêm là một nhánh công riêng; M8 và M1 **Lớn**
- ⚠ Không có đáp án thì `estimate.md` phải ghi E13 là **ước theo giả định**, không phải cam kết

**References**
- `01-architecture.md` §9.1 toàn bảng

---

### 2.14 Phần spec chưa thành issue và vì sao

#### 2.14.1 Số đo gốc

| Số | Nghĩa | Đã kiểm lại ngày 2026-10-24 |
|---|---|---|
| **272** | dòng mục 6.3 của 15 screen spec | ✅ khớp — đếm lại từ file, xem 4.2 |
| **43** | dòng có `Tầng` đúng bằng `không code` | ✅ khớp |
| **229** | dòng có tầng code → ước công được | ✅ khớp (272 − 43) |

#### 2.14.2 Phân bố 272 dòng theo màn

| Màn | Dòng 6.3 | `không code` | Có tầng code | Epic |
|---|---|---|---|---|
| SCR-00 | 16 | 3 | 13 | E12 |
| SCR-12 | 15 | 3 | 12 | E06 |
| SCR-18 | 14 | 3 | 11 | E07 |
| SCR-19 | 15 | 2 | 13 | E07 |
| SCR-20 | 16 | 3 | 13 | E08 |
| SCR-21 | 23 | 6 | 17 | E08 |
| SCR-23 | 16 | 1 | 15 | E09 |
| SCR-24 | 21 | 2 | 19 | E09 |
| SCR-26 | 23 | 1 | 22 | E09 |
| SCR-28 | 19 | 3 | 16 | E01 · E02 · E04 · E05 |
| SCR-29 | 18 | 1 | 17 | E03 · E04 |
| SCR-31 | 22 | 4 | 18 | E10 |
| SCR-32 | 16 | 3 | 13 | E10 |
| SCR-33 | 21 | 3 | 18 | E10 |
| SCR-35 | 17 | 5 | 12 | E11 |
| **Tổng** | **272** | **43** | **229** | 13 epic |

#### 2.14.3 Chỗ thật sự không thành dev task

Theo luật §1.6, **mọi dòng trong 229 dòng ước được phải truy về một dev task**. Ba nhóm dưới đây
là chỗ **cố ý không** thành dev task thi công:

| Nhóm | Số dòng | Đi về đâu | Vì sao |
|---|---|---|---|
| Dòng `Tầng = không code` | **43** | `[INVESTIGATION]` hoặc `PREMISE.md` | Không sinh dòng code nào. Phần cần khách trả lời thành investigation; phần chỉ cần ghi thành văn bản vào `PREMISE` hoặc `E12-INV-03` |
| Hai ngưỡng bình quân nhiều ngày | **2** (trong 229) | **E05**, chờ `E05-INV-01` | Thiếu **nguồn dữ liệu**, không phải thiếu cột. Vẫn ước theo giả định LAB-1, kèm mức đổi **Vừa → Lớn** ghi rõ |
| `US-30` ghi sự cố có bằng chứng | — | **ngoài phạm vi** | SCR-30, spec ghi thẳng *"ngoài phạm vi 15 màn"*. Không epic nào nhận |

#### 2.14.4 Việc **không** đến từ 272 dòng

Ba nguồn khác cũng sinh dev task, nêu ở đây để bảng truy ngược không bị hiểu là đã đủ:

| Nguồn | Sinh ra gì | Epic |
|---|---|---|
| `01-architecture.md` §9.1 — 8 mock | 8 dev task điểm tích hợp ngoài | **E13** |
| `01-architecture.md` §12 — 7 mục *"cái KHÔNG có trong code"* | đã hoà vào các epic tương ứng: phân trang (E07, E08, E10) · `/lots` (E07) · làm mới số đếm (E12) · `movements` (E09) · hiệu ứng lên `allocations` (E07) · `available` ngõ cụt (E07) · luồng duyệt theo mức (E10) | rải |
| `00-pham-vi…` §8 — 4 AC của khách chưa đạt | **US-05 AC3** (E07) · **US-11 AC3** (E13) · **US-11 AC4** (E09 `E09-11-BE-03`) · **US-14 AC2** (E03 `E03-BE-08`) | rải |

#### 2.14.5 Năm P0 chưa phủ — danh sách rút gọn cho bảng rủi ro

Không phải nợ kỹ thuật nhỏ; mỗi cái gắn thẳng một tiêu chí nghiệm thu của khách:

| # | Tiêu chí | Hiện trạng | Dev task |
|---|---|---|---|
| 1 | **US-12 AC3** đơn chưa phân công + lý do từ chối | không có chỗ sinh, không có chỗ lưu | `E01-BE-07` · `E01-FE-04` |
| 2 | **US-05 AC3** đổi trạng thái lô cập nhật phân bổ theo thời gian thực | `apply_lot_status` **không chạm** `allocations` | `E07-05-BE-04`, chờ `E07-INV-02` |
| 3 | **US-11 AC4** POD sửa = phiên bản mới liên kết bản cũ | `pods.order_id` **unique** → **không có đường sửa nào** | `E09-11-BE-03` |
| 4 | **US-14 AC2** tài xế **nhận** bản tuyến mới nhất | đọc được nhưng **không được báo** | `E03-BE-08`, chờ `E03-INV-01` |
| 5 | **US-20** mở hồ sơ thu hồi từ kết quả truy xuất | nút có trong code, SCR-36 `enabled: false` | `E11-20-BE-01`, chờ `E11-INV-01` |

#### 2.14.6 Hai câu hỏi hỏi sai, phải gửi lại

| # | Chỗ | Vấn đề |
|---|---|---|
| **Q54** | SCR-21 §6.3 #6 | Hỏi *"dòng lịch sử giao không có hạn thì xử lý thế nào"* — nhưng `delivery_history.expiry_date` là `not null`, **ca đó không dựng được**. Câu thật sự cần hỏi là giả định code đang mang: nhiều lô cùng một lần giao → lấy **hạn lớn nhất** (`E08-INV-06`) |
| **Q13/Q16** | SCR-28 §6.3 #17 | Comment của `routes_driver_service_date_key` viện dẫn hai câu này, nhưng **không câu nào hỏi về "một tuyến mỗi ngày"**. Ràng buộc **chưa có căn cứ nào từ khách** → câu hỏi mới (`E01-INV-03`) |



## 3. Hạng mục chịu ràng buộc đặc thù của đề — cụm giờ lái 2024

Đề đòi cụm này tách đủ **bốn ngưỡng** và **sáu hạng mục**. Mục này là chỗ đối chiếu một lần, để
không ai phải lần lại 13 epic mà đếm.

### 3.1 Điều kiện kích hoạt

Detail design **có** module lập lịch — SCR-28 tạo tuyến, SCR-29 công bố. Hai màn **chưa có một
dòng code nào**, nên khác 13 màn còn lại: ở đây mục 6.3 gần như toàn `[LAB-5] dựng`, không phải
bịt chỗ hở.

### 3.2 Bốn ngưỡng — bốn dev task, không gộp

Bản luật `DRV-RULE-2026-v1`, `valid_from = 2026-01-01`:

| # | Ngưỡng | Cột | Giá trị | Toán tử | Cách người dùng sửa | Dev task |
|---|---|---|---|---|---|---|
| ① | `連続運転` Lái liên tục | `max_continuous_drive_min` | 240 phút | `>` **nghiêm** | đổi thứ tự điểm giao, hoặc chèn nghỉ | `E02-BE-04` |
| ② | `拘束時間` Thời gian ràng buộc | `max_binding_min_per_day` | 780 phút/ngày | `>` **nghiêm** | bớt điểm giao, hoặc đổi tài xế | `E02-BE-05` |
| ③ | nghỉ reset chuỗi lái | `break_reset_min` | 30 phút | `>=` **không nghiêm** | kéo một điểm dừng lên ≥30 phút | `E02-BE-06` |
| ④ | `ルート時間` Thời lượng tuyến | `max_route_hours` | 24 giờ | `>` **nghiêm** | chia hai ngày | `E02-BE-07` |

**Vì sao bốn task, không phải một:** bốn **cách sửa khác nhau** và **hai toán tử biên khác nhau**.
`AC-28-34` cấm gộp thành một câu `このルートは法定基準を満たしていません` — spec nói thẳng
*"một câu gộp không nói được phải làm gì"*.

Ca mẫu `R-SEED-02` (`AC-28-36`): ① `超過` 410/240 · ② `OK` 455/780 · ③ `超過` · ④ `OK` 7h35/24h.

### 3.3 Sáu hạng mục — ở đâu, vì sao ở đó

| # | Hạng mục | Epic · task | Vì sao tách khỏi bốn ngưỡng |
|---|---|---|---|
| 1 | Khoảng vi phạm chính xác (`12:20 → 15:35`, vượt 170 phút) | **E02** · `E02-BE-04` (gộp vào ①) | Thuật toán riêng — ① chỉ cần biết *có vượt không*, `C-13` cần biết *vượt từ mấy giờ tới mấy giờ*. `FR-SCH-02` nghiệm thu đích danh `正確な違反時間範囲を表示` |
| 2 | Chọn bản luật theo `service_date` | **E02** · `E02-BE-08` | Lối tra khác hẳn; mốc là **ngày chạy tuyến**, không phải `now()`. Phụ thuộc `E02-BE-01` (`unique(valid_from)`) |
| 3 | Ghim `driver_rule_version_id` lúc công bố | **E03** · `E03-BE-03` | Tầng khác (SCR-29), và phải **từ chối** nếu bản luật đổi giữa lúc kiểm và lúc ghi (`AC-29-48`) |
| 4 | Cấu trúc `check_result` jsonb | **E02** · `E02-BE-09` | Hợp đồng dữ liệu; `PREMISE` §3 `V-3` đã chốt hình dạng. E03 tiêu thụ |
| 5 | Chỗ lưu điểm nghỉ `休憩` | **E04** · cả epic | `DB (migration)` + đổi `snapshot`, không phải phép tính. **M-1 đẩy E04 lên trước E03** |
| 6 | 8/11 ngưỡng chưa phủ | **E02** `E02-BE-02` (6 cái) + **E05** (2 cái) | Hai nhóm **chi phí khác hẳn** — xem 3.4 |

### 3.4 Mười một ngưỡng của FR-SCH-02 — ranh giới chi phí quan trọng nhất của bài

Bảng `driver_rule_versions` có **4 cột**, phủ **3** ngưỡng (cộng ④ đến từ IF-MAP-01).

| Nhóm | Ngưỡng | Thiếu gì | Ước được? | Đi về đâu |
|---|---|---|---|---|
| **(a) Thiếu cột** | 960h/năm · 3.300h/năm · 284h/tháng · trần 15h ngày ngoại lệ · nghỉ giữa ca 11h · 9h | chỉ thiếu **cột** | **Có** — thêm cột, nhớ bảng **append-only** nên bản cũ phải nhận giá trị mặc định **có chủ ý** | **E02** · `E02-BE-02` |
| **(b) Thiếu nguồn dữ liệu** | lái bình quân **9h/ngày qua 2 ngày** · **44h/tuần qua 2 tuần** | thiếu **giờ đã làm của những ngày trước** — hệ **chưa có bảng nào** ghi | **Không**, tới khi có Q13 | **E05** · chờ `E05-INV-01` |

Đây là **ranh giới duy nhất trong cả bài** nơi một yêu cầu không ước được công. Bảy điểm chờ
khách còn lại của module lập lịch đều có giả định vendor và **ước được**.

### 3.5 Ba mâu thuẫn — trạng thái xử lý

| # | Mâu thuẫn | Chốt | Nằm ở |
|---|---|---|---|
| **M-1** | Chèn nghỉ → SCR-28 cho bốn ngưỡng `OK` → nút công bố bật → SCR-29 tính lại từ CSDL, nghỉ **không được lưu** → vi phạm lại → **ngõ cụt** | **Chỗ lưu điểm nghỉ lên trước**, E04 chặn E03 (`PREMISE` §3 `V-1`) | `E04-BE-01` · `E04-FE-02` · ghi chéo ở `E02-BE-06` và `E03-FE-04` |
| **M-2** | `AC-28-33` đòi kiểm biên ④ ở 1.440/1.441 phút, nhưng `Đ-3` (không vắt qua nửa đêm) + ② (780 phút/ngày) làm **không dựng được ca dữ liệu hợp lệ nào** | ④ nghiệm thu ở **unit test của hàm thuần**, không qua CSDL | `E02-BE-07` |
| **M-3** | `client_request_id` thiếu ở cả `routes` (SCR-28 #11) và `route_versions` (SCR-29 #10) — hai dòng spec, một lỗ hổng | **Một** task migration, không tách theo màn | `E01-BE-02` — ca mẫu của luật gộp §1.3 |

### 3.6 Bảy điểm chờ khách của module lập lịch

| Q | Hỏi gì | Giả định vendor | Mức đổi | Investigation |
|---|---|---|---|---|
| Q12 | người điều phối dựng tuyến hay hệ tự sinh | người dựng, hệ kiểm | **màn khác hẳn**, bật FT-06-02 | `E01-INV-01` |
| Q13 | giờ đã làm của ngày trước lấy từ đâu | từ tuyến + sự kiện tài xế, số dư đầu kỳ nhập tay | **Vừa → Lớn** | `E05-INV-01` |
| Q34 | có áp ca đặc biệt (phà, đường dài, ca chia đôi) | không áp | Vừa | `E02-INV-01` |
| Q56 | tuyến có 6 trạng thái hay 2 | 2 (`draft` · `published`) | Nhỏ, thành Vừa nếu cần sự kiện tài xế | `E01-INV-04` |
| — | quy ước mã tuyến `route_code` | `R<YYMMDD>-<4 số>` | Thấp | `E01-INV-02` |
| — | một tài xế một tuyến/ngày | giữ nguyên | **Lớn** nếu khách cần nhiều tuyến/ngày | `E01-INV-03` |
| — | cách báo tài xế khi có bản tuyến mới | chỉ báo trên màn, không thông báo đẩy | **Lớn** nếu đòi thông báo đẩy | `E03-INV-01` |

Riêng ràng buộc *một tài xế một tuyến/ngày* là **câu hỏi mới phải gửi khách** — không có trong
`client-qa-list.md`, phát hiện khi đọc `R-15`: comment viện dẫn Q13/Q16 mà **hai câu đó hỏi việc
khác**.

---



## 4. Chỗ hở và mâu thuẫn của spec LAB-4 phát hiện khi break

Sáu chỗ. Cột **Xử lý** ghi đúng một trong bốn: *đã sửa thiết kế* (trỏ dòng `PREMISE.md`) · *giả định*
(trỏ dòng `PREMISE.md`) · *tạo issue làm rõ* (`#số`) · *để mở và vì sao*.

| Spec | Chỗ hở / mâu thuẫn | Xử lý |
|---|---|---|
| `scr-28` `R-13` `AC-28-49` `AC-28-45` · `scr-29` `R-14` `AC-29-35` | **M-1 — ngõ cụt im lặng.** Chèn 2 điểm nghỉ 30 phút → SCR-28 cho bốn ngưỡng `OK` → bật nút `公開へ進む`. Nhưng SCR-29 tính lại từ CSDL, nơi **điểm nghỉ không có chỗ lưu** → trả 422 `RULE_ROUTE_VIOLATION`. Không dòng spec LAB-4 nào xử lý luồng này | **Đã sửa thiết kế** — `PREMISE.md` §1 dòng 1 + §3 `V-1` `V-2`: thêm chỗ lưu điểm nghỉ trên `route_stops`, E04 thành chặn của E03. Sinh epic `#57`–`#66` |
| `scr-28` `AC-28-33` · `Đ-3` · `R-10` | **M-2 — mã chết.** `AC-28-33` đòi nghiệm thu biên ngưỡng ④ ở 1.440/1.441 phút bằng ca dữ liệu qua CSDL. Nhưng `Đ-3` chốt tuyến không vắt qua nửa đêm, và ② chặn ở 780 phút/ngày ⇒ **không ca dữ liệu hợp lệ nào** chạm tới ④ | **Đã sửa thiết kế** — `PREMISE.md` §1 dòng 2: chuyển nghiệm thu ④ sang unit test của hàm thuần `lib/rules/driver-hours.ts`, không qua CSDL. Issue `#30` |
| `scr-28` §6.3 #11 · `scr-29` §6.3 #10 | **M-3 — một lỗ hổng, hai dòng spec.** `client_request_id` thiếu ở **cả** `routes` lẫn `route_versions`; hai màn mô tả rời nhau nên không ai thấy đó là cùng một chỗ chống gửi trùng | **Đã sửa thiết kế** — gộp thành một dev task duy nhất `#6` (`E01-BE-02`), thêm cột cho cả hai bảng trong một migration |
| `scr-29` §2.2 · §6.3 #2 | **Hợp đồng để ngỏ.** `check_result.violations` luôn là mảng rỗng; hình dạng một phần tử vi phạm *"chưa có ví dụ nào ở đâu"*, LAB-4 ghi thẳng `[LAB-5] chốt`. Không chốt thì E02 (phép tính) và E03 (`publish_route` ghi kết quả) **không ráp vào nhau được** | **Đã sửa thiết kế** — `PREMISE.md` §3 `V-3` chốt hình dạng phần tử, giữ nguyên 3 khoá cấp trên để không phá bản seed `R-SEED-01`. Issue `#32` (`E02-BE-09`) |
| `scr-28` §6.3 #10 — bảng `driver_rule_versions` | **Dữ liệu cho phép trạng thái vô định.** Thiếu `unique (valid_from)` ⇒ hai bản luật cùng ngày hiệu lực thì câu tra ra kết quả **không xác định**. Bảng cùng họ `temperature_threshold_versions` thì đã có ràng buộc này | **Đã sửa thiết kế** — `PREMISE.md` §3 `V-4`: thêm `unique (valid_from)` thay vì vá bằng tiebreaker `created_at desc`. Issue `#24` (`E02-BE-01`) |
| `scr-28` §6.3 #17 — chỉ mục `routes_driver_service_date_key` | **Ràng buộc không có căn cứ.** Comment viện dẫn `(Q13/Q16)`, nhưng **không câu nào trong hai câu đó hỏi về việc này** — tức luật "một tài xế một tuyến mỗi ngày" chưa từng được khách xác nhận | **Giả định** — `PREMISE.md` §2 `GĐ-L5-3`: giữ nguyên ràng buộc, 0 công thêm; ghi sẵn mức đổi nếu khách cần nhiều tuyến/ngày. Cần một câu hỏi mới gửi khách, xem §2.14.6 |

Ba mâu thuẫn `M-1` `M-2` `M-3` còn có bảng trạng thái xử lý ở §3.5. Bảy điểm chờ khách của riêng
module lập lịch ở §3.6; toàn bộ 38 câu hỏi khách nằm trên board dưới nhãn `type:investigation`,
không ước công.
