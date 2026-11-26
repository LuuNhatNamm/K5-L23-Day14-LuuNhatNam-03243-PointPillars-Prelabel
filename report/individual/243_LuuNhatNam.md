# Báo cáo Day 14 — Lưu Nhật Nam — 243


- Mã học viên dùng với `--student`: `243`
- `seed_tag` trong `frames_A.txt`: `393590736f`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- Tham số dự đoán sẽ giảm công sửa nhiều nhất là `score_thr`. Tôi dự đoán tăng từ `0.1` lên `0.3` sẽ giảm tổng chi phí sửa trên tập A.
- Cơ sở từ số đo cấu hình gốc là 77 hộp cần xóa, 3 hộp cần thêm và 0 hộp cần sửa. Riêng s02f45 và s05f35 có tổng cộng 77 hộp cần xóa, chiếm 23.1 trong tổng chi phí 26.1. Tôi giả thuyết tăng ngưỡng sẽ loại được nhiều hộp thừa có điểm tin cậy thấp. Cần đối chiếu ảnh BEV và điểm `score` để kiểm tra giả thuyết này.
- Tăng ngưỡng cũng có thể loại hộp đúng và làm tăng số vật bị sót. Theo công thức của lab, loại được 4 hộp thừa nhưng bỏ sót thêm 1 vật sẽ giảm chi phí `4 × 0.3 - 1 = 0.2`. Vì vậy, tôi dự đoán ngưỡng trung bình có thể cân bằng hai tác động. Kết quả sweep và leave-one-out sẽ dùng để kiểm tra dự đoán.

> Bản nháp dự đoán được AI hỗ trợ soạn từ số đo cấu hình gốc. Người làm bài cần tự đối chiếu BEV và viết dự đoán của mình theo RULES.md trước khi nộp.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | 77 | 3 | 0 | 26.1 |
| `best_config.json` | | | | |


Số đo cấu hình gốc trên từng frame:

| Frame | Dự đoán | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|---:|
| s02f45 | 46 | 40 | 1 | 0 | 13.0 |
| s04f22 | 27 | 0 | 2 | 0 | 2.0 |
| s05f35 | 41 | 37 | 0 | 0 | 11.1 |
| Tổng | 114 | 77 | 3 | 0 | 26.1 |

Tổng 3 frame có 40 hộp tham chiếu và 37 hộp ghép khớp với dự đoán. Chi phí theo công thức của lab là `0.3 × 77 + 1.0 × 3 + 0.5 × 0 = 26.1`.

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_243/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_243/frames_B.txt --config d14_243/best_config.json --gt d14_243/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
