# Báo cáo cá nhân — BuiThanhTan-2A202603304

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Bùi Thanh Tân
- MSSV:2A202603304
- Email: tanbtt29042004@gmail.com
- Link repository:
- Phiên bản CVAT (Help → About) :2.74.1
- Máy: hệ điều hành Window · RAM 16 GB · chạy CVAT chế độ đầy đủ 
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có 
- Giờ bắt đầu: 17h 12/11/2026
- Giờ kết thúc: 18h30 12/11/2026

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có | Có | 19 |
| `face` | Skeleton | 13 | Có | Có | 13 |


Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có 

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):
trong trang, rê chuột vào một điểm rồi bấm `Q` để bật/tắt `occluded` (v=1), hoặc bấm `O` để bật/tắt `outside` (v=0); cũng có thể chuột phải vào điểm để chọn trong menu.
...

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 2 | 0 | 15 |
| `occluded` | 3 | 5 | 0 | 0 | 12 |
| `back` | 2 | 3 | 2 | 0 | 9 |
| `small` | 1 | 0 | 5 | 0 | 4 |
| `crowd` | 1 | 3 | 2 | 0 | 10 |
| `faces` | 8 | 8 | — | 0 | 20 |

- Số ảnh người đã xong ở mốc phút 105: 10 / 10 (xong cả 12 ảnh trước mốc này)
- Thời gian thực tế (phút): CP1 50 · CP2 20 · CP3 10
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?

Ảnh `crowd` 000000309169 (ném đĩa): hai cô gái chồng lên nhau, tay giơ cao đan vào nhau, nên phải lần theo từng chi vai → khuỷu → cổ tay để không gán nhầm tay người này sang người kia; người phía sau bị che một phần tay và chân nên phải cân nhắc cờ `occluded` / `outside` cho từng điểm.

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| `000000030960` (occluded) | #1 cô dâu | `right_shoulder`, `right_hip`, `right_knee` | 0 | `v = 1` / `v = 0` | Nửa phải của cô dâu nằm hẳn sau người chú rể, chỉ thấy vai trái và tay; ba người ước lượng sẽ đặt hông, gối phải rất tản mát → `outside` |
| `000000030960` (occluded) | #1, #2 | `left_ankle`, `right_ankle` | 0 | `v = 1` / `v = 0` | Cổ chân bị cắt ở mép dưới ảnh và bị váy che; không kéo điểm về mép ảnh |
| `000000122199` (occluded) | #2 người áo cam | `right_shoulder`, `right_hip`, `right_knee` | 1 | `v = 1` / `v = 0` | Người quay nghiêng, nửa phải bị balo và thân tự che; vị trí suy được chắc từ vai trái, đùi và độ rộng thân → `occluded` |
| `000000122199` (occluded) | #1 người phía sau | `left_ankle`, `right_ankle` | 1 | `v = 1` / `v = 0` | Cổ chân lún trong tuyết nhưng ống quần thẳng tới mặt tuyết, vị trí suy chắc |
| `000000090646` (occluded) | #1 người quay lưng | `left_ear` | 0 | `v = 2` / `v = 0` | Đầu hơi quay sang phải nên tai trái không thấy viền; chỉ tai phải `v = 2` |
| `000000518966` (back) | #1 cô gái quay lưng | `left_elbow`, `left_wrist` | 0 | `v = 1` / `v = 0` | Tay trái khuất trước thân, phía sau balo, không thấy đoạn nào. Trái/phải đã đổi chỗ theo hướng người trước khi tinh chỉnh |
| `000000023424` (back) | #2 người áo trắng xa | đầu (5 điểm), hai cổ tay | 0 | `v = 1` / `v = 0` | Người cao 66 px (vừa trên ngưỡng 60 px), quay lưng, mặt và cổ tay quá nhỏ để đoán chắc |
| `000000309169` (crowd) | #3 cô gái áo đen | `left_eye`, `left_ear`, `left_shoulder` | 1 | `v = 1` / `v = 0` | Bên trái bị đầu và tay cô áo vàng che một phần; vẫn thấy đường viền mặt và cánh tay trên nên ước lượng chắc |
| `000000309169` (crowd) | #1 người xa bên trái | `left_ear`, `left_hip` | 1 | `v = 1` / `v = 0` | Người cao 89 px, chạy nghiêng; hông trái bị tay che, suy từ đùi trái |


## 4. Bảng tự review (CP3)

Từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Thứ tự review (ngược thứ tự job): người `000000309169` (crowd) → `000000323705` (small) → `000000518966` (back) → `000000023424` (back) → `000000122199` (occluded); mặt `face_175798` → `face_294580` → `face_168953`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| `000000309169` | #2 cô áo vàng | `right_eye`, `right_ear`, `right_shoulder` | `ok` | Quay lưng-nghiêng về trái ảnh, nửa phải khuất sau đầu và tay cô áo đen → `v = 0` đúng. Vai/hông trái nằm bên trái ảnh, khớp hướng quay lưng | — |
| `000000309169` | #3 cô áo đen | cả skeleton | `ok` | Quay về camera, `left_hip` nằm bên phải ảnh đúng. Hai gối bắt chéo là thật (bước lunge), không phải đổi trái/phải | — |
| `000000518966` | #1 cô gái quay lưng | `nose`, `left_eye`, `right_eye` | `vis_flag` | Người quay lưng hẳn, không thấy mặt. Guideline (bảng mục 4): quay lưng mà mũi, mắt không thấy và không đoán chắc → `v = 0`. Đang để `v = 1`, nên model sẽ học vị trí đoán trên gáy | Chưa, đổi sang `outside` |
| `000000518966` | #1 cô gái quay lưng | trái/phải, `left_elbow`, `left_wrist` | `ok` | Quay lưng nên điểm `left_*` nằm bên trái ảnh: đúng (`left_shoulder` x = 103 < `right_shoulder` 190). Tay trái khuất trước thân → `v = 0` đúng | — |
| `000000023424` | #1 cô gái đeo túi, #2 người áo trắng (66 px) | mũi, mắt, cổ tay | `ok` | Cả hai quay lưng, mặt không thấy → `v = 0`; tai thấy viền → `v = 2`. Người #2 cao 66 px, trên ngưỡng nên vẫn gán | — |
| `000000122199` | #2 người áo cam | `knee`, `ankle` | `ok` | Script cảnh báo gối và cổ chân ngược phía. Người đứng nghiêng quay sang trái ảnh, mặt ngoái về camera; mỗi chân lần liền hông → gối → cổ chân không vắt chéo xương, nên đây là chân bước chéo thật. Giữ nguyên | — |
| `face_175798` | mặt tóc xoăn | 13 điểm | `ok` | Mặt chính diện, `left_eye_*` nằm bên phải ảnh đúng; khóe miệng và môi đúng chỗ | — |
| `face_294580` | mặt đeo kính râm | 8 điểm mắt | `vis_flag` | Kính râm tối trên ảnh màu → guideline yêu cầu `occluded` (`v = 1`), đặt sau tròng theo gọng. Đang `v = 0`, và vị trí vẫn là mẫu: `right_eye_outer` x = 51 nằm trên tóc, cả hai mắt ở y = 177–215, cao hơn tròng kính. Đổi `v = 1` và đặt lại theo gọng | Chưa |
| `face_168953` | mặt đeo kính trong | 13 điểm | `ok` | Kính trong, thấy mắt → `v = 2` đúng; 8 điểm mắt ôm sát khóe và mí | — |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 1 | 3 | 0 | 0 | 0 | 8 |

Điểm còn phân vân giữa `v = 1` và `v = 0`:

- `000000518966` #1 `nose`, `left_eye`, `right_eye`. Lựa chọn `v = 1`: có thể ước lượng theo hướng đầu và búi tóc. Lựa chọn `v = 0`: ba người ước lượng sẽ đặt mũi lệch nhau nhiều vì không thấy tai trước hay đường viền má. **Chọn `v = 0`** theo bốn câu hỏi của guideline.
- `000000030960` #1 cô dâu `right_shoulder`. Lựa chọn `v = 1`: suy từ vai trái và cổ. Lựa chọn `v = 0`: vai phải nằm hẳn sau người chú rể, không thấy đoạn tay trên nào. **Giữ `v = 0`.**
- `000000122199` #1 `left_elbow`, `left_wrist`. Lựa chọn `v = 1`: tay trái buông dọc thân, ước lượng được theo vai. Lựa chọn `v = 0`: sát mép ảnh và bị dây balo che. **Giữ `v = 0`**, kiểm lại khi sửa vai.

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `BuiThanhTan_persons.zip` | `000000030960`, #1 cô dâu (annotation id 3) | 51 | Có: 6 điểm `outside` (`right_ear`, `right_shoulder`, `right_hip`, `right_knee`, hai cổ chân) ra `v = 0`; không có điểm `occluded` | Có: 11 = 17 − 6 |
| `BuiThanhTan_persons.zip` | `000000122199`, #2 người áo cam (id 7) | 51 | Có: `right_shoulder`, `right_hip`, `right_knee` `occluded` ra `v = 1`; `right_ear` `outside` ra `v = 0` | Có: 16 = 17 − 1 |
| `BuiThanhTan_faces.zip` | `face_294580`, mặt duy nhất (id 4) | 39 | Có: 8 điểm mắt `outside` ra `v = 0` | Có: 5 = 13 − 8 |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? **Tọa độ cũ** (ví dụ `right_shoulder` của cô dâu vẫn là `287.93, 161.54`; hai cổ chân có y = 651 > chiều cao ảnh 612, tức nằm ngoài khung và không bị kéo về mép).

Hai job đã chuyển sang completed trên CVAT? Có / Không

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
- File person: BuiThanhTan_persons.zip
  Số ảnh: 12 · số skeleton `person`: 16 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000023424=2, 000000030960=2, 000000090646=1, 000000122199=2, 000000177889=1, 000000241837=1, 000000261732=1, 000000309169=3, 000000323705=0, 000000431893=1, 000000518966=1, 000000564304=1
  Cờ v: v=2 211 (78%) · v=1 21 (8%) · v=0 40 (15%)
  num_keypoints trung bình: 14.5
- File face: BuiThanhTan_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_125051=1, face_168953=1, face_175798=1, face_294580=1, face_300399=1, face_356144=1, face_442231=1, face_559185=1
  Cờ v: v=2 96 (92%) · v=1 0 (0%) · v=0 8 (8%)
  num_keypoints trung bình: 12.0
- Ghi chú: 48 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 3
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

- `000000122199.jpg #2` (gối, cổ chân ngược phía): **giữ nguyên.** Người đứng nghiêng, chân bước chéo thật; mỗi chân lần liền hông → gối → cổ chân.
- `000000309169.jpg #1` (hông, gối, cổ chân ngược phía): **không giữ.** Tự review xác định đây là `lr_swap` ở hông; cần sửa trên CVAT và xuất lại.
- `000000323705.jpg` (không có skeleton): **giữ nguyên.** Cả 5 người trong ảnh đều cao dưới 60 px, theo quy tắc của lab thì không gán.

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![alt text](image.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng]![alt text](image-1.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

  ![alt text](image-2.png)

4. Một đoạn JSON xuất của một người:

   Ảnh `000000261732.jpg` (`image_id` = 7). Đây là người duy nhất trong ảnh, đủ 17 điểm `v = 2`:

   ```json
   {
     "id": 10,
     "image_id": 7,
     "category_id": 1,
     "segmentation": [],
     "area": 35393.0096,
     "bbox": [153.16, 67.99, 133.72, 264.68],
     "iscrowd": 0,
     "attributes": { "occluded": false, "keyframe": false },
     "keypoints": [
       239.35,  72.83, 2,
       244.30,  70.28, 2,
       233.75,  67.99, 2,
       253.39,  78.27, 2,
       223.67,  77.29, 2,
       251.15, 118.13, 2,
       212.18,  88.21, 2,
       243.64, 170.15, 2,
       238.46,  90.10, 2,
       267.67, 130.95, 2,
       286.88,  94.22, 2,
       234.61, 180.51, 2,
       186.19, 176.45, 2,
       257.01, 262.71, 2,
       181.52, 268.29, 2,
       282.33, 332.67, 2,
       153.16, 296.19, 2
     ],
     "num_keypoints": 17
   }
   ```

   Thứ tự 17 bộ ba `[x, y, v]` là thứ tự: nose, left_eye, right_eye, left_ear, right_ear, left_shoulder, right_shoulder, left_elbow, right_elbow, left_wrist, right_wrist, left_h
ip, right_hip, left_knee, right_knee, left_ankle, right_ankle. `bbox` có dạng `[x, y, w, h]` và ôm sát các điểm. `num_keypoints` = 17 bằng số điểm có `v > 0`.



## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   `vis_flag` (3/12 dòng review): đặt cờ theo cảm giác thay vì theo bốn câu hỏi, và có lúc bấm `outside` cho cả nhóm điểm mà không kéo chúng khỏi vị trí mẫu (vai người phía sau ở `000000122199`, mắt kính râm ở `face_294580`). Ở dự án thật tôi sẽ đi qua bốn câu hỏi cho từng điểm bị che. Trước khi Save, tôi rà mọi điểm `v = 0`: nếu tọa độ còn đối xứng y hệt skeleton mẫu thì điểm đó chưa được xử lý.

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

   "Sau khi thả skeleton mẫu, **mọi điểm đều phải được chạm tới**, kể cả điểm sẽ để `outside`. Điểm `v = 0` mà nằm thẳng hàng, đối xứng như mẫu (cùng y ở trái và phải) bị coi là chưa gán." Ví dụ: `000000122199` người #1 có hai vai, hai khuỷu, hai cổ tay cùng y từng đôi, trong khi vai thấy rõ trên ảnh.

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):

   Lỗi: `000000518966`, mũi và hai mắt của người quay lưng để `v = 1`. Với `v > 0`, mỗi điểm sinh một heatmap Gaussian ở tọa độ tôi đặt và có trọng số 1 trong loss, nên model bị dạy phải "thấy mũi" trên gáy, tóc của người quay lưng. Nó học cách bịa điểm mặt với confidence cao, trong khi điều cần học là không có tín hiệu ở đó. Khi chấm OKS, điểm này cũng được tính như điểm thật. Đổi sang `v = 0` thì heatmap đó bị bỏ, trọng số bằng 0. Lỗi `lr_swap` ở `000000309169` còn tệ hơn ở bước lật ảnh: khi lật ngang, augmentation đổi chỉ số `left_hip` ↔ `right_hip`, nên nhãn sai trên ảnh gốc vẫn sai trên ảnh lật. Model nhận tín hiệu mâu thuẫn về trái/phải của hông.

## 8. Khó khăn và lỗi kỹ thuật

- Script `check_submission.py` cho 3 cảnh báo, không có lỗi. Phải đọc từng cảnh báo trên ảnh để tách chân bắt chéo.
- Điểm `outside` vẫn giữ tọa độ cũ khi xuất, nên không nhìn file JSON mà biết được điểm đã được đặt đúng chỗ hay còn ở vị trí mẫu. Phải mở lại trên CVAT để kiểm.
## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| | | | |
| | | | |
| | | | |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
(dán ở đây)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?

...

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Lin, T.-Y. et al. (2014). *Microsoft COCO: Common Objects in Context*. ECCV. Định dạng COCO Keypoints và cờ `v`.
- Tài liệu của lab: `docs/GUIDELINE.md`, `docs/COCO_KEYPOINTS.md`, `docs/CVAT_CHEATSHEET.md`.
- Tài liệu CVAT (skeleton, cờ `occluded` / `outside`, export COCO Keypoints 1.0).

