# Khai báo dùng AI — Lê Đức Lượng

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity AI | Tóm tắt yêu cầu của bài Lab Ngày 12, giải thích quy tắc chia 22 ảnh vào Task trên CVAT và lập kế hoạch thực hiện từng bước theo tài liệu repo | Dùng để nắm rõ quy trình 7 bước và chuẩn hóa đường dẫn thư mục `G04/` | Có, đối chiếu trực tiếp với `GUIDE.md`, `CHECKPOINTS.md`, `RULES.md` và kiểm tra bằng lệnh `python scripts/cabin_check.py --help` |
| 2 | Antigravity AI | Giải thích ý nghĩa các thuộc tính `seatbelt`, `gaze_zone`, `infant_seat.facing` và cách chỉnh độ sáng (Brightness/Contrast) trên CVAT khi gặp ảnh tối | Áp dụng để phân biệt đúng `infant_seat` với `child_seat`, chọn đúng hướng `facing`, và bật tăng sáng trên CVAT để gán nhãn chính xác | Có, kiểm tra lại theo mục 4.1–4.8 trong `GUIDE.md` và xác nhận với cập nhật schema của Coach |
| 3 | Antigravity AI | Gợi ý khung nội dung cho bảng danh sách lớp `class_list_v0.md` (DMS/OMS), gộp file XML export của 2 task OMS (16 ảnh) và DMS (6 ảnh) thành `export_final.zip` (22 ảnh), chạy `cabin_check.py check` và `cabin_check.py diff` với `peer_export_final.zip` | Dùng để phát hiện và sửa các lỗi thuộc tính mặc định trên CVAT, phân tích `disagreement_log.csv` và xuất `export_final_v2.zip` + `check_final_v2.txt` đạt 0 lỗi | Có, kiểm tra bằng lệnh `python scripts/cabin_check.py check export_final_v2.zip --expect 22 --manifest G04/oms/manifest.csv --out check_final_v2.txt` và `python -m zipfile -l export_final_v2.zip` |
