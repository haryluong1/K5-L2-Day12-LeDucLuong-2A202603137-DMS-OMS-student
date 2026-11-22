# TEAM — Ngày 12

Mã bộ ảnh: **G04** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Lê Đức Lượng | 2A202603137 | có | Bùi Thắng (`adminbuithang` - cùng mã G04) | 112 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `D01.png` (`face13.mouth_left.occluded`, `face13.lip_lower.occluded`): Mức độ che khuất nhẹ ở vùng khóe miệng và môi dưới khi mặt tài xế quay nghiêng trên ảnh NIR xoay 90° (đã đánh dấu `ambiguous` trong `disagreement_log.csv`).

## Cá nhân

Mỗi người một mục, 1–2 dòng mỗi ý.

### LeDucLuong-2A202603137
- Phần mình làm (ngoài 22 ảnh của mình, ví dụ ai review ai, ai tổng hợp ca hỏi coach): Tự gán đủ 22 ảnh cốt lõi bộ `G04`, tự kiểm qua 3 chặng `cabin_check.py`, thực hiện đối chiếu chéo (`diff`) toàn bộ 112 dòng khác biệt với bạn cùng mã `G04` (`peer_export_final.zip`) và xuất bản sửa lỗi `export_final_v2.zip` + `check_final_v2.txt`.
- Điều mình học được hôm nay: Nắm vững quy tắc quy chiếu vị trí ghế theo chiều xe (`trái ảnh = rear_right` khi camera nhìn về sau), quy chiếu trái/phải theo cơ thể người lái trên ảnh NIR xoay 90° (`mắt trái có y lớn hơn`), và cách đồng bộ giữa cờ `occluded` của `face13` với thuộc tính `eye_* = unknown` của box `face`.
