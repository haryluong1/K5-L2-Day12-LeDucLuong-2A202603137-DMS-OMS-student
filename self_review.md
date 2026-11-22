# Tự đánh giá — Lê Đức Lượng · G04

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S04_ir.png` | `person` (`rear_right`) | `seat_flip` | Lúc đầu copy box sang quên đổi giá trị mặc định `seat = driver`, đã sửa lại thành `seat = rear_right` khớp với `S04_rgb.png` | Có |
| `S05_rgb.png` | `infant_seat` (`rear_left`) | `seat_flip` | Để nhầm giá trị mặc định `seat = driver` khi mới vẽ box, đã sửa thành `seat = rear_left` theo hệ quy chiếu của xe | Có |
| `D01.png` | `hand` & `face13` | `lr_flip` | Hai bàn tay của `driver` ban đầu bị gán trùng `side = left` và thiếu `face13`; đã sửa 1 tay thành `side = right` và bổ sung đủ 13 điểm `face13` | Có |
| `D06.png` | `face` & `face13` | `flag` | Cả 4 điểm `right_eye_*` đều bật `occluded = 1` nhưng `face.eye_right` lại để `open`; sau review chéo đã sửa `eye_right = unknown` trong `export_final_v2.zip` | Có |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Quên đổi giá trị thuộc tính mặc định của CVAT khi vừa vẽ box mới (như `seat = driver` trên ảnh OMS `S04_ir`, `S05_rgb` hoặc `side = left` cho cả 2 bàn tay trên `D01`).

Vì sao mình mắc: CVAT tự động gán giá trị đầu tiên trong danh sách cho mọi box mới vẽ (`seat = driver`, `side = left`). Khi tập trung căn chỉnh khung hình chữ nhật cho sát mép đối tượng, mình dễ chuyển sang vẽ box tiếp theo mà quên mở bảng **DETAILS** bên phải để chọn lại thuộc tính.

Lần sau tránh bằng cách: Tạo thói quen bắt buộc "Vẽ xong 1 box $\rightarrow$ nhìn sang bảng **DETAILS** chỉnh ngay `seat` / `side` $\rightarrow$ rồi mới vẽ box tiếp theo", kết hợp chạy `cabin_check.py` ngay sau mỗi chặng để phát hiện sớm.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
- Tại dòng `D06.png | face | eye_right | khác giá trị (IoU=0.79) | mine=open | peer=unknown`: Khi cả 4 điểm mốc của mắt phải (`right_eye_outer`, `right_eye_inner`, `right_eye_upper`, `right_eye_lower`) trên `face13` đều bị viền/phản xạ kính che khuất (`occluded = 1`), thuộc tính `eye_right` của box `face` phải gán là `unknown` theo Quy tắc 4.4-1 và 4.5 (bạn review chéo gán `unknown` là đúng, và `cabin_check.py` cũng cảnh báo điểm này). Mình đã tiếp thu và sửa `eye_right = unknown` trên `D06.png` trong bản `export_final_v2.zip`.
