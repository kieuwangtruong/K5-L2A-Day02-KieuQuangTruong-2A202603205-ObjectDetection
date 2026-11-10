# Báo cáo cá nhân — Ngày 2 Object Detection

Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Kieu Quang Truong
- MSSV: 2A202603205
- Email: [26ai.truongkq@vinuni.edu.vn](mailto:26ai.truongkq@vinuni.edu.vn)
- Lớp: 2A
- Link repo bài làm: [K5-L2A-Day02-KieuQuangTruong-2A202603205-ObjectDetection](https://github.com/kieuwangtruong/K5-L2A-Day02-KieuQuangTruong-2A202603205-ObjectDetection)
- Link Colab đã chạy: [Google Colab](https://colab.research.google.com/drive/1gInxXHIcIxMLvsX1-wqV_LjOr3emaPxH?usp=sharing)

## 2. Schema và mini guideline

Dùng [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md), với bốn lớp `car`, `truck`, `bus`, `van`. Box ôm phần thân xe nhìn thấy; xe bị che vẫn được gán nếu nhận diện được; xe quá nhỏ/xa mà không xác định chắc lớp và biên box thì bỏ qua. Ba ca ở `drive_001`–`drive_003` áp dụng quy tắc này cho xe nhỏ ở hậu cảnh/dòng xe dày.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: Notebook chạy qua bước xác nhận đủ 50 cặp ảnh/nhãn train và 10 cặp ảnh/nhãn eval. Checker độc lập trên máy này chưa chạy được vì Python chưa được cài (`py` báo “No installed Python found”).
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: Đã xác định ca mơ hồ ở `drive_001`, `drive_002`, `drive_003`; chưa ghi đủ danh sách 10 ảnh.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: Chưa có ghi chép để báo cáo.
- Commit khóa nhãn ban đầu: `ba3d146` (`Add training labels and dataset files`).

## 4. Gold QC và rework

| Chỉ số hiện có trong JSON | Kết quả |
|---|---:|
| TP | 653 |
| FP | 0 |
| FN | 0 |
| Precision | 1.00 |
| Recall | 1.00 |
| F1 | 1.00 |
| mean_iou_of_matches | 1.00 |
| passed | `true` |

Kết quả lấy từ [outputs/annotation_evaluation.json](../../outputs/annotation_evaluation.json), ở ngưỡng IoU 0.50. JSON không ghi rõ đây là số liệu trước hay sau rework; hiện chưa có ghi chép rework. `outputs/` bị `.gitignore` bỏ qua, cần `git add -f outputs/annotation_evaluation.json` nếu đây là JSON được phép nộp.

## 5. Kết quả YOLO

- Runtime: Python 3.13.18, Ultralytics 8.4.208, Torch 2.14.1+cpu, CPU Intel Xeon 2.20 GHz.
- Cấu hình: `yolo26n.pt`, 50 epochs, `imgsz=640`, `batch=-1`, CPU; theo `args.yaml`, các tham số này khớp notebook.
- Best checkpoint trong Colab: `/content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt` (epoch 37).

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.52244 |
| Recall | 0.48994 |
| mAP50 | 0.51740 |
| mAP50–95 | 0.33715 |

Metrics lấy từ epoch tốt nhất (epoch 37) trong [`results.csv`](assets/yolo26_runs/vehicle_annotation/results.csv). Các ảnh dự đoán và biểu đồ nằm trong hai thư mục `assets/eval_predictions/` và `assets/yolo26_runs/`.

Trả lời bốn câu hỏi cuối notebook (các câu cần kết quả model đang chờ lần chạy thành công):

1. `bus` có recall thấp nhất (0 trong confusion matrix); ví dụ xe bus ở [`drive_051.jpg`](assets/eval_predictions/visuals/drive_051.jpg) bị model bỏ sót hoặc phân loại nhầm.
2. Nếu mAP50 cao nhưng mAP50-95 thấp, cần xem box có định vị chưa sát: lệch tâm, kích thước quá lớn/nhỏ, hoặc chưa ôm sát biên vật thể.
3. `bus` có thể bị nhầm với `car`: confusion matrix cho thấy 50% nhãn bus thật bị dự đoán thành car và 50% bị bỏ sót. Đây là dấu hiệu để rà lại phân biệt lớp và guideline, chưa đủ để kết luận guideline là nguyên nhân.
4. Không dùng eval để cập nhật trọng số train để giữ bộ ảnh đánh giá riêng. Notebook dùng `eval` làm validation để theo dõi metric/chọn checkpoint; đây không phải ảnh train nhưng kết quả validation vẫn được dùng trong quá trình chọn model.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Train/eval YOLO trên Colab | Lần chạy đầu báo `data.yaml` thiếu khóa `val`; tải ZIP bằng trình duyệt báo `Failed to fetch`. | Cấu hình đã được sửa để notebook chạy; lấy các thư mục kết quả train/eval vào `report/individual/assets/`. | Có `results.csv`, confusion matrix và đủ 10 ảnh dự đoán. |

## 7. Tự đánh giá theo rubric

Đã có 50 file nhãn train, notebook xác nhận các cặp ảnh/nhãn, JSON QC ghi `passed: true`, và có kết quả train/eval cùng artifacts. Nhật ký rà bằng mắt 10 ảnh vẫn chưa ghi đủ; đối chiếu thêm [RUBRIC.md](../../RUBRIC.md) và hoàn thiện nhật ký trước khi nộp.

## 8. Công cụ AI và tài liệu tham khảo

Đã dùng ChatGPT/Codex để hỗ trợ điền metadata/link báo cáo và chẩn đoán lỗi cấu hình `data.yaml`; thông tin báo cáo cần được chủ bài kiểm tra lại với kết quả Colab thực tế. Nguồn tham khảo: tài liệu và notebook trong repo này. Không ghi mật khẩu/token hoặc đính kèm gold train.
