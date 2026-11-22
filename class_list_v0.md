# Danh sách lớp v0 — Lê Đức Lượng · G04

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face.eye_left` / `face.eye_right` | `open` / `closed` / `unknown` | Theo dõi trạng thái đóng/mở từng mắt theo thời gian (PERCLOS) để phát hiện buồn ngủ, ngủ gật hoặc mất khả năng quan sát | Có, trừ khi bị đốm phản xạ LED trên tròng kính hoặc kính râm quá tối che khuất |
| 2 | `face.gaze_zone` | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Xác định vùng nhìn của tài xế để cảnh báo mất tập trung (distraction) khi mắt rời mặt đường (`road`) quá ngưỡng thời gian an toàn | Có (dựa vào hướng đầu và vị trí con ngươi trên ảnh NIR) |
| 3 | `face.glasses` | `none` / `clear` / `sun` / `unknown` | Nhận diện loại kính đang đeo để điều chỉnh thuật toán ước lượng mắt/ánh nhìn và chọn chế độ xử lý phản xạ LED phù hợp | Có thấy gọng kính, nhưng trên NIR tròng kính râm có thể trở nên trong suốt giống kính cận (`clear`) |
| 4 | `face13` (13 điểm mặt + cờ `occluded`/`outside`) | Toạ độ `(x, y)` của 13 mốc mắt, mũi, miệng + cờ che khuất | Ước lượng góc quay đầu 3D (yaw, pitch, roll), độ mở mí mắt/miệng (ngáp) và xác định vùng mặt nào đang bị che khuất để không tính sai | Có, miễn là khuôn mặt đủ lớn ($\ge 60\text{ px}$) và không bị vật cản che kín |
| 5 | `hand` (`whose`, `side`, `on_wheel`) | `driver`/`passenger` · `left`/`right` · `yes`/`no`/`unknown` | Kiểm tra tay tài xế có đặt trên vô lăng hay không (Hands-On-Wheel Detection), phục vụ cảnh báo an toàn và chuyển giao quyền lái (takeover) trên xe tự hành | Có (nhận diện tốt theo hình dáng bàn tay và vị trí tiếp xúc với vành vô lăng) |
| 6 | `phone` (`state`) | `held` / `mounted` / `lap` | Phát hiện hành vi sử dụng điện thoại khi lái xe (cầm tay nghe/nhắn tin hoặc nhìn xuống đùi) để phát cảnh báo xao nhãng mức độ cao | Có (nhận diện qua hình dáng cạnh, góc vuông hoặc màn hình phát sáng của điện thoại) |
| 7 | `person.seatbelt` (`seat = driver`) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Nhắc nhở tài xế thắt dây an toàn và cảnh báo khi thắt sai quy cách (luồn dưới nách/sau lưng làm giảm hiệu quả bảo vệ khi va chạm) | Có nếu đủ tương phản, nhưng dễ bị mất chi tiết (`unknown`) nếu dây trùng độ phản xạ NIR với áo hoặc bị bóng tối che |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`) | `driver` / `front_passenger` / `rear_left` / `rear_middle` / `rear_right` | Đếm số lượng hành khách và xác định vị trí ghế có người ngồi để tối ưu điều hòa, cảnh báo dây an toàn và điều khiển bung túi khí theo ghế | Có (nhận diện rõ theo hình khối cơ thể và đầu người ngồi trên từng ghế) |
| 2 | `person.seatbelt` (hành khách) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Phát hiện hành khách ở hàng ghế trước và hàng ghế sau chưa thắt hoặc thắt sai dây an toàn để hiển thị cảnh báo lên màn hình trung tâm | Một phần (phụ thuộc vào độ tương phản giữa dải dây và trang phục dưới đèn hồng ngoại; nếu tối hoặc bị khuất phải gán `unknown`) |
| 3 | `child_seat` (`seat`, `occupied`) | Vị trí ghế · `no` / `unknown` | Nhận biết ghế phụ trẻ em lắp ở từng vị trí ghế để cấu hình chế độ an toàn khoang xe và kiểm tra trạng thái ghế đang trống hay bị che khuất | Có (dựa vào khung hình học đặc trưng của ghế trẻ em, không phụ thuộc màu sắc) |
| 4 | `infant_seat` (`seat`, `facing`) | Vị trí ghế · `rear` / `front` | Phát hiện nôi em bé (đặc biệt là loại quay ngược `facing = rear`) để tự động vô hiệu hóa túi khí ghế phụ phía trước và kích hoạt cảnh báo bỏ quên trẻ (CPD) | Có (nhận diện rõ qua hình dáng nôi xách và hướng đặt nôi theo trục xe) |
| 5 | `object` (`seat`, `type`) | Vị trí ghế · `bag` / `box` / `cup` / `other` | Phân biệt đồ vật đặt trên ghế với người/trẻ em (tránh báo động giả cảm biến trọng lượng ghế) và nhắc hành khách không quên hành lý khi rời xe | Có về mặt hình dáng tổng thể, nhưng mất thông tin màu sắc/họa tiết nên một số vật khó phân loại chi tiết hơn so với ảnh RGB |
| 6 | `frame_meta` (`modality`, `light`, `camera_blocked`) | `rgb`/`ir` · `day`/`night`/`unknown` · `yes`/`no` | Giám sát tình trạng hoạt động của chính camera cabin: phát hiện ngay khi ống kính bị che khuất (`camera_blocked = yes`) để báo lỗi hệ thống thay vì đưa ra dự đoán sai | Có (biết được toàn khung hình bị tối đen hoặc bị vật cản che sát ống kính) |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Trên ảnh OMS hàng ghế sau, khi có một đồ vật (`object`) hoặc ghế trẻ em (`child_seat` / `infant_seat`) có kích thước lớn hoặc nằm lệch sang ranh giới giữa hai ghế (ví dụ đè lên cả phần ghế bên và ghế giữa `rear_middle`), tiêu chí ưu tiên để gán thuộc tính `seat` là dựa theo vị trí tâm đáy của vật hay dựa theo khóa cài/tựa lưng chính?
   Khung ví dụ: `S01_rgb` (ghế trẻ em có em bé/hình nộm ngồi bên trong và booster seat bên cạnh).
   Bạn tạm gán thế nào và vì sao: Tạm gán `seat` theo vị trí ghế mà phần đáy/thân chính của đối tượng tựa lên nhiều nhất (theo hệ quy chiếu của xe: trái ảnh là `rear_right`, giữa là `rear_middle`, phải ảnh là `rear_left`), vì đó là ghế chịu tải trọng chính của vật.
2. Câu hỏi: Trên ảnh DMS (`D##`), khi tài xế đeo kính hoặc quay đầu nghiêng khiến một phần mắt bị gọng kính/đốm sáng LED che khuất một nửa (vẫn thấy một góc mí mắt nhưng không nhìn rõ khe mắt mở hay khép toàn bộ), ngưỡng che khuất cụ thể là bao nhiêu phần trăm thì chuyển `eye_left`/`eye_right` từ `open`/`closed` sang `unknown`?
   Khung ví dụ: `D01`, `D06` (tài xế đeo kính, vùng mí mắt bị đốm phản xạ đèn NIR và gọng kính đè lên).
   Bạn tạm gán thế nào và vì sao: Áp dụng Quy tắc chung 4.4-1 ("Không thấy thì `unknown`, không đoán"), khi không phân biệt được chắc chắn khe mắt đang mở hay hai mí đã khép kín thì tạm gán `eye_* = unknown` và bật cờ `occluded = 1` cho các điểm `face13` tại vị trí bị che để tránh dạy dữ liệu nhiễu cho model.
