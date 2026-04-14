# Metadata Register — Verified / Estimated / To be measured

## Verified
- N, label counts, length stats: outputs/datacard_stats.json
- Split counts: outputs/datacard_stats.json
- HTML artifacts and duplicate counts: outputs/datacard_stats.json
- GE pass/fail summary: outputs/ge/validation_summary.md
- Cleanlab suspected issues: outputs/logs/cleanlab_summary.md
- Preprocessing audit before/after: outputs/logs/audit_before.md, outputs/logs/audit_after.md

## Estimated
- Production readiness score: ~85/100
- Genre and domain coverage: ước tính dựa trên nội dung phim chung
- Nhân khẩu học người đánh giá: không xác định; cần bổ sung phân tích nếu có dữ liệu phụ

## To be measured
- Root cause cho GE failure: cần kiểm tra detailed expectation suite
- Manual review 5 mẫu Cleanlab top-200: outputs/logs/cleanlab_label_issues.csv
- Class balance trên mỗi split nếu chưa có bảng chi tiết
- Phân phối thể loại/phạm vi phim trong train/val/test
- Hiệu quả xử lý bản sao trùng lặp trong bộ kiểm tra
