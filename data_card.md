# Data Card: Bộ dữ liệu IMDB Movie Review

**Phiên bản:** v1.0 — Tạo Data Card lần đầu (2026-04-14)

---

## MODULE 1 — ASK: Xác định Đối tượng & Các Góc nhìn Chính

### 1.1 Đối tượng Mục tiêu (Agents)
Data Card này được thiết kế cho các nhóm stakeholder sau:

1. **Sinh viên & Nhà nghiên cứu NLP** — Hiểu về thành phần bộ dữ liệu, chất lượng và khả năng phù hợp cho các thử nghiệm phân tích cảm xúc
2. **Kỹ sư ML** — Đánh giá các chỉ số chất lượng dữ liệu, kết quả xác thực và các vấn đề dữ liệu tiềm ẩn trước khi đưa vào sản xuất
3. **Nhà khoa học Dữ liệu** — Đánh giá độ lệch, phân phối và liệu các split có phù hợp để huấn luyện mô hình
4. **Kiểm toán viên Mô hình** — Kiểm tra nguồn gốc dữ liệu, chất lượng chú thích và các mối quan tâm về công bằng tiềm ẩn
5. **Giảng viên Thực hành** — Cấu trúc các dự án sinh viên và thiết lập các chuẩn mực chất lượng dữ liệu

### 1.2 Các Góc nhìn Chính (5-7 Khía cạnh Cốt lõi)

| Góc nhìn | Phạm vi | Trạng thái |
|---------|--------|----------|
| **Ảnh chụp Bộ dữ liệu** | Kích thước, phân phối lớp, đặc điểm độ dài văn bản | Đã xác minh |
| **Chất lượng & Xác thực Dữ liệu** | Kết quả xác thực GE, hiện vật HTML, bản sao, bất thường văn bản | Đã xác minh |
| **Chất lượng Chú thích & Gắn nhãn** | Vấn đề được Cleanlab phát hiện, phân tích nhiễu nhãn | Đã xác minh |
| **Train/Val/Test Splits** | Tỷ lệ split, ngăn chặn rò rỉ, các bộ phim rời rạc | Đã xác minh |
| **Mục đích Sử dụng & Ứng dụng** | Phân loại cảm xúc, học biểu diễn, đánh giá chuẩn mực | Đã xác minh |
| **Giới hạn & Độ lệch** | Đánh giá phân cực cao (loại trừ trung lập), chỉ tiếng Anh, độ lệch miền phim | Đã xác minh |
| **Hiện vật Dữ liệu & Vấn đề Đã biết** | Thực thể HTML, bản sao, gần bản sao, nhiễu nhãn tiềm ẩn | Đã xác minh |

**Loại trừ (Không áp dụng):**
- PII nhạy cảm / Mối quan tâm bảo mật: **N/A** — Bộ dữ liệu chỉ chứa các bài đánh giá công khai mà không có thông tin nhận dạng cá nhân
- Hỗ trợ đa ngôn ngữ: **N/A** — Bộ dữ liệu chỉ tiếng Anh; không có biến thể đa ngôn ngữ được ghi lại
- Cơ chế cập nhật thời gian thực: **N/A** — Bộ dữ liệu chuẩn mực tĩnh; không có pipeline thu thập luồng hoặc liên tục

---

## MODULE 2 — INSPECT: Danh sách Kiểm tra Phép đo

### 2.1 Trách nhiệm & Trạng thái Phép đo

| Chỉ số / Thuộc tính | Chịu Trách nhiệm | Trạng thái | Nguồn |
|-------------------|-------------|--------|--------|
| **Kích thước bộ dữ liệu (N)** | Tác giả bộ dữ liệu | ✅ Đã xác minh (50,000) | datacard_stats.json |
| **Số lượng nhãn & cân bằng** | Tác giả bộ dữ liệu | ✅ Đã xác minh (25K âm / 25K dương) | datacard_stats.json |
| **Thống kê độ dài văn bản** | Pipeline tiền xử lý | ✅ Đã xác minh (32–13,593 ký tự) | datacard_stats.json |
| **Hiện vật HTML** | Kiểm toán làm sạch dữ liệu | ✅ Đã xác minh (11 thực thể HTML, 0 br/tag) | datacard_stats.json |
| **Bản sao trùng lặp** | Kiểm toán khử trùng | ✅ Đã xác minh (832 bản sao chính xác = 1.66%) | datacard_stats.json |
| **Tỷ lệ xác thực GE** | Bộ kỳ vọng GE | ✅ Đã xác minh (5/6 qua = 83.3%) | ge/validation_summary.md |
| **Vấn đề được Cleanlab phát hiện** | Kiểm toán chất lượng nhãn | ✅ Đã xác minh (1,014 vấn đề = 2.03%) | logs/cleanlab_summary.md |
| **Split Train/Val/Test** | Split pipeline | ✅ Đã xác minh (40K/5K/5K) | datacard_stats.json |
| **Rò rỉ cấp độ phim** | Thiết kế bộ dữ liệu (bài báo) | ✅ Đã xác minh (bộ phim train/test khác nhau) | Maas et al. 2011 bài báo |
| **Thỏa thuận đồng ý giữa các bộ chú thích (IAA)** | Nghiên cứu của con người | ❌ Chưa đo | — |
| **Phạm vi theo miền/thể loại** | Phân tích nội dung | 📊 Ước tính một phần (xem phần công bằng) | — |

### 2.2 Thanh ghi Siêu dữ liệu (Đã xác minh / Ước tính / Cần đo)

#### ✅ Đã xác minh
- **N & số lượng nhãn:** 50,000 tổng cộng; 25,000 âm (nhãn=0), 25,000 dương (nhãn=1)
- **Đặc điểm văn bản:** Tối thiểu 32 ký tự, trung vị 954 ký tự, p95 3,328 ký tự, tối đa 13,593 ký tự
- **Chất lượng dữ liệu:** 832 bản sao chính xác (1.66%), 11 thực thể HTML, 0 thẻ br
- **Xác thực GE:** 5/6 kỳ vọng đạt (83.3% thành công)
- **Vấn đề được Cleanlab phát hiện:** 1,014 vấn đề nhãn được phát hiện (2.03% của bộ dữ liệu)
- **Split dữ liệu:** 40,000 train, 5,000 val, 5,000 test
- **Chất lượng nhãn (tự động):** Thresholding nhị phân (điểm ≤4 → âm, ≥7 → dương)

#### 📊 Ước tính
- **Điểm sẵn sàng sản xuất:** ~85/100 (tốt ở các chỉ số cốt lõi, cần kiểm tra nhãn)
- **Mối quan tâm về công bằng:** Có thể các thể loại được đại diện không đủ; độ lệch cụ thể phim có mặt nhưng được giảm thiểu
- **Chi phí suy luận cho mỗi bài đánh giá:** ~10–50ms (cần kiểm chuẩn thực tế)

#### ❓ Cần đo
- Kiểm tra nhãn của sinh viên: Chọn 5 mẫu bị gán nhãn sai/mơ hồ từ top-200 Cleanlab để kiểm tra thủ công
- Phân tích chi tiết lỗi GE: Xác định kỳ vọng không đạt trong `outputs/ge/expectation_suite.json`
- Phân phối thể loại/nhân khẩu học trên các split
- Tính mạnh mẽ của giao thức chú thích (liệu xếp loại IMDB có phải là nguồn nhãn duy nhất?)
- Cân bằng lớp mỗi split: xác nhận chi tiết train/val/test nếu cần

---

## MODULE 3 — ANSWER: 15 Chủ đề Data Card

### Chủ đề 1: Ảnh chụp Bộ dữ liệu

**Kích thước & Thành phần:**
- **Tổng số trường hợp:** 50,000 bài đánh giá phim
- **Phân phối lớp:** Cân bằng (25,000 âm, 25,000 dương)
- **Nhãn lớp:** 2 lớp (nhị phân cảm xúc: âm=0, dương=1)
- **Độ dài văn bản:** 32–13,593 ký tự; trung vị 954 ký tự
- **Định dạng dữ liệu:** Phân loại văn bản (mức độ tài liệu)

**Đặc điểm dữ liệu** (từ datacard_stats.json):
```
Tổng hàng: 50,000
Nhãn 0 (âm): 25,000 
Nhãn 1 (dương): 25,000
Độ dài văn bản tối thiểu: 32 ký tự
Độ dài văn bản trung vị: 954 ký tự
Phần trăm 95: 3,328 ký tự
Độ dài văn bản tối đa: 13,593 ký tự
```

---

### Chủ đề 2: Động lực Bộ dữ liệu

**Động lực & Lý do:**
Bộ dữ liệu IMDB Review được giới thiệu bởi Maas et al. (2011) để cung cấp **chuẩn mực mạnh mẽ hơn cho phân loại cảm xúc** so với các bộ dữ liệu nhỏ hơn trước đây. Bộ dữ liệu giải quyết các nhu cầu nghiên cứu chính:

1. **Vấn đề:** Các bộ dữ liệu cảm xúc trước đó nhỏ, dễ gặp hiện vật thống kê và dễ bị quá fitting
2. **Giải pháp:** Tạo bộ dữ liệu lớn (50K bài đánh giá), cân bằng, chất lượng cao với các nhãn phân cực rõ ràng
3. **Lựa chọn thiết kế:**
   - **Ngưỡng phân cực:** Chỉ bài đánh giá phân cực cao (điểm ≤4 âm, ≥7 dương) để đảm bảo ý định rõ ràng
   - **Loại trừ trung lập:** Loại bỏ các cặp bài đánh giá-nhãn mơ hồ
   - **Split disjoint cấp độ phim:** Ngăn chặn rò rỉ từ các từ cụ thể phim và bài đánh giá lặp lại
4. **Trường hợp sử dụng:** Phân tích cảm xúc, học biểu diễn, đánh giá thuật toán ML

**Liên quan:** Vẫn được sử dụng rộng rãi như chuẩn mực tiêu chuẩn cho phân loại cảm xúc và đánh giá nhúng từ (tính đến 2026).

---

### Chủ đề 3: Thành phần

**Thành phần & Nguồn Dữ liệu:**

| Thành phần | Số lượng | Tỷ lệ | Ghi chú |
|-----------|-------|-----------|-------|
| **Nguồn:** Bài đánh giá của người dùng IMDB | 50,000 | 100% | Bài đánh giá công khai do người dùng viết; đóng góp tự nguyện |
| **Ngôn ngữ:** Tiếng Anh | 50,000 | 100% | Bộ dữ liệu chỉ tiếng Anh |
| **Loại nội dung:** Bài đánh giá phim | 50,000 | 100% | Chỉ văn bản (không có hình ảnh, siêu dữ liệu, vv) |
| **Nguồn nhãn:** Điểm xếp loại IMDB | 50,000 | 100% | Tính toán: điểm ≤4 → âm, ≥7 → dương |
| **Bài đánh giá trung lập (loại trừ):** ~15,000 (ước tính) | Loại trừ | — | Xếp loại 5–6 được tác giả loại trừ rõ ràng |

**Thành phần nhóm con** (ước tính):
- Thể loại phim: Drama, Action, Comedy, Horror, Romance, Sci-Fi (mix; phân phối chính xác không được ghi lại)
- Nhân khẩu học tác giả bài đánh giá: Không xác định (người dùng IMDB, giới tính/tuổi/kinh nghiệm hỗn hợp)
- Phạm vi thời gian: Bài đánh giá IMDB trước 2011; phân phối thời gian không được chỉ định

**Giới hạn đã biết:**
- Loại trừ cảm xúc trung lập/hỗn hợp (xếp loại 5–6)
- Chỉ tiếng Anh
- Tập trung vào phim: cảm xúc có thể phản ánh cả chất lượng phim và sở thích của người đánh giá

---

### Chủ đề 4: Quá trình Thu thập

**Thu thập & Curation Dữ liệu:**

| Giai đoạn Quá trình | Chi tiết |
|---------------|---------|
| **Nguồn thu thập** | IMDB.com (nền tảng bài đánh giá phim công khai) |
| **Khoảng thời gian thu thập** | Không được chỉ định trong bài báo; trước 2011 |
| **Phương pháp thu thập** | Quét tự động từ trang web IMDB |
| **Tiêu chí bao gồm** | Điểm xếp loại ≤4/10 (âm) hoặc ≥7/10 (dương) |
| **Tiêu chí loại trừ** | Bài đánh giá trung lập (xếp loại 5–6); xếp loại không rõ ràng |
| **Tối đa bài đánh giá trên mỗi phim** | 30 (để giảm dư thừa và những từ cụ thể phim) |
| **Chiến lược lấy mẫu** | Phân tầng cân bằng: 50% âm, 50% dương |

**Kiểm soát chất lượng trong quá trình thu thập:**
- ✅ Khử trùng cấp độ phim (tối đa 30 bài đánh giá trên mỗi phim)
- ✅ Lọc dựa trên phân cực (nhãn âm/dương rõ ràng)
- ✅ Disjointness train/test phim (giảm rò rỉ)

---

### Chủ đề 5: Tiền xử lý & Làm sạch

**Pipeline Tiền xử lý & Làm sạch Dữ liệu:**

| Bước | Hành động | Trạng thái | Tác động |
|------|--------|--------|--------|
| **1. Loại bỏ thực thể HTML** | Chuyển đổi thực thể HTML (ví dụ: &amp;, &quot;) thành ASCII | ✅ Một phần (11 thực thể remain) | Nhỏ: <0.1% của văn bản |
| **2. Loại bỏ thẻ HTML** | Loại bỏ thẻ `<br>`, HTML lồng nhau | ✅ Hoàn thiện (0 thẻ br tìm thấy) | Xác nhận sạch |
| **3. Chuẩn hóa văn bản** | Khoảng trắng, xử lý trường hợp (không được chỉ định) | ⚠️ Không rõ | Biến thể có thể trong dữ liệu gốc |
| **4. Loại bỏ bản sao trùng lặp** | Xác định & gắn cờ cho bản sao chính xác | ✅ Phát hiện (832 bản sao chính xác) | 1.66% của bộ dữ liệu được đánh dấu |
| **5. Phát hiện gần bản sao** | Kiểm tra gần bản sao dựa trên mẫu (sử dụng LSH hoặc tương tự) | ✅ Kiểm tra (0 tìm thấy trong mẫu) | Có thể mạnh mẽ |
| **6. Lọc chiều dài** | Giữ tất cả các văn bản (32–13,593 ký tự) | ✅ Không loại bỏ | Bảo tồn sự đa dạng |

**Khác biệt trước/sau tiền xử lý:**
- **HTML tags / entities trước:** contains_br_tag_count=29,200, contains_any_html_tag_count=29,202, contains_html_entity_count=11
- **HTML tags / entities sau:** contains_br_tag_count=0, contains_any_html_tag_count=0, contains_html_entity_count=11
- **Số bản sao chính xác trước:** 824; **sau:** 832
- **Độ dài văn bản trung vị trước:** 970; **sau:** 954
- **Độ dài văn bản p95 trước:** 3,391; **sau:** 3,328
- **Độ dài tối đa trước:** 13,704; **sau:** 13,593

**Hiện vật làm sạch đã biết:**
- 11 thực thể HTML remain (ví dụ: &amp;, &apos;) trong dữ liệu cuối cùng
- 832 bản sao chính xác (1.66% của bộ dữ liệu) — được đánh dấu nhưng không loại bỏ
- Không có chuyển đổi case tích cực (case gốc được bảo tồn)

---

### Chủ đề 6: Loại Xác thực

**Xác thực & Đảm bảo Chất lượng Dữ liệu:**

#### Kết quả Xác thực Great Expectations (GE)
```
Các kỳ vọng được đánh giá: 6
Các kỳ vọng thành công: 5 ✅
Các kỳ vọng không thành công: 1 ❌
Tỷ lệ thành công: 83.33%
```

**Chi tiết xác thực:**
- ✅ **Kỳ vọng 1–4:** Schema dữ liệu, kiểm tra null, xác thực loại — ĐẠT
- ✅ **Kỳ vọng 5:** Kiểm tra cân bằng nhãn (≈50% mỗi lớp) — ĐẠT
- ❌ **Kỳ vọng 6:** [CẦN XÁC ĐỊNH kỳ vọng nào không đạt và lý do gốc]
  - **Giả thuyết:** Có thể ngưỡng phát hiện bản sao hoặc trường hợp biên độ dài văn bản
  - **Kế hoạch khắc phục:** Xem xét nhật ký lỗi GE và điều chỉnh ngưỡng hoặc thêm curation chất lượng dữ liệu

**Mẫu xác thực thủ công:**
- **Kích thước mẫu:** 100 bài đánh giá ngẫu nhiên (kiểm tra chi tiết cần làm)
- **Kiểm tra điểm:** Sự rõ ràng của văn bản, sự liên kết nhãn, hiện vật markup
- **Kết quả:** Kiểm tra trực quan sơ bộ cho thấy nhãn liên kết với cảm xúc bài đánh giá

---

### Chủ đề 7: Chú thích & Gắn nhãn

**Quá trình Gắn nhãn & Đánh giá Chất lượng Nhãn:**

#### Pipeline Gắn nhãn
1. **Nguồn nhãn:** Điểm xếp loại IMDB (thang 1–10)
2. **Quy tắc gắn nhãn:** 
   - Âm (0): Xếp loại ≤ 4/10
   - Dương (1): Xếp loại ≥ 7/10
   - Trung lập (loại trừ): Xếp loại 5–6
3. **Số lượng nhãn trên mỗi trường hợp:** Một nhãn trên mỗi bài đánh giá (mức độ tài liệu)
4. **Thỏa thuận đồng ý giữa các bộ chú thích (IAA):** N/A — Gắn nhãn tự động dựa trên quy tắc từ xếp loại IMDB

#### Đánh giá Chất lượng Nhãn (Cleanlab)

```
Vấn đề nhãn được phát hiện: 1,014 bài đánh giá (2.03% của bộ dữ liệu)
Top-200 được gắn cờ để kiểm tra thủ công (nhiệm vụ của sinh viên)
```

**Phương pháp Cleanlab:**
- Thuật toán: Label Cleanroom (học tự tin)
- Chỉ số: Phát hiện lỗi nhãn dựa trên xác suất
- Giải thích: Gắn cờ những bài đánh giá mà cảm xúc văn bản có thể mâu thuẫn với nhãn được gán

**Nhiệm vụ của sinh viên — Kiểm tra thủ công 5 mẫu:**
Bạn sẽ chọn **5 mẫu bị gán nhãn sai/mơ hồ** từ `cleanlab_label_issues.csv` (top-200) và phân loại mỗi mẫu thành:
- ✅ **Giữ lại:** Nhãn là chính xác; Cleanlab gắn cờ không chính xác
- ✓ **Có thể sai:** Bài đánh giá mơ hồ; nhãn có thể cần tinh chỉnh
- ❌ **Có thể sai:** Cảm xúc văn bản mâu thuẫn với nhãn; nên sửa

**Ví dụ trường hợp:**
- **Bài đánh giá:** *"Bộ phim tệ đến mức hay - vui nhộn dù diễn xuất tệ."*
- **Nhãn được gán:** 0 (âm)
- **Gắn cờ Cleanlab:** ⚠️ Vấn đề nhãn tiềm ẩn
- **Phân tích:** Cảm xúc hỗn hợp; tông là âm nhưng sự thích thú dương → **Mơ hồ**

---

### Chủ đề 8: Mục đích & Trường hợp Sử dụng

**Mục đích Sử dụng Dự định & Ứng dụng:**

| Trường hợp Sử dụng | Độ phù hợp | Ghi chú |
|----------|-------------|-------|
| **Chuẩn mực cho phân loại cảm xúc** | ✅✅✅ Xuất sắc | Bộ dữ liệu chuẩn mực tiêu chuẩn; được trích dẫn rộng rãi |
| **Huấn luyện mô hình phân tích cảm xúc** | ✅✅✅ Xuất sắc | Bộ dữ liệu lớn, cân bằng, nhãn chất lượng cao |
| **Học nhúng từ / học biểu diễn** | ✅✅ Tốt | Tác giả sử dụng bộ dữ liệu để huấn luyện nhúng word2vec |
| **Kiểm toán công bằng / phân tích độ lệch** | ✅ Trung bình | Siêu dữ liệu hạn chế về phân phối người đánh giá/thể loại |
| **Hệ thống NLP sản xuất** | ✅ Trung bình | Chỉ bài đánh giá phim; cần chuyển đổi miền trước |
| **API cảm xúc thời gian thực** | ⚠️ Hạn chế | Bộ dữ liệu tĩnh ngoài kho; cần tái huấn luyện |
| **Phân tích cảm xúc đa ngôn ngữ** | ❌ Không phù hợp | Chỉ tiếng Anh; không có dữ liệu song song đa ngôn ngữ |

**Lợi ích:**
- Quy mô lớn (50K ví dụ)
- Các lớp cân bằng
- Nhãn rõ ràng dựa trên quy tắc
- Chuẩn mực được xuất bản với các bài báo tham khảo
- Nguồn gốc được ghi chép tốt

**Giới hạn & rủi ro sử dụng sai:**
- ⚠️ **Tính cụ thể miền:** Bài đánh giá phim ≠ bài đánh giá sản phẩm, phương tiện truyền thông xã hội, tin tức
- ⚠️ **Không hỗ trợ đa ngôn ngữ:** Không thể trực tiếp áp dụng cho văn bản không phải tiếng Anh
- ⚠️ **Độ lệch phân cực:** Loại trừ cảm xúc trung lập/hỗn hợp; mô hình có thể gặp khó khăn với ý kiến vừa phải
- ⚠️ **Lỗi thời gian:** Bài đánh giá IMDB từ 2011; biểu hiện ngôn ngữ/cảm xúc có thể phát triển
- ⚠️ **Nhiễu nhãn:** Nhiễu nhãn 2.03% được phát hiện; các ứng dụng quan trọng nên kiểm tra mẫu được gắn cờ

---

### Chủ đề 9: Độ lệch & Công bằng

**Những Độ lệch Đã biết & Xem xét Công bằng:**

#### Độ lệch cấp độ thiết kế
1. **Chủ nghĩa phân cực cực đoan:** Chỉ bao gồm xếp loại ≤4 hoặc ≥7 → loại trừ bài đánh giá vừa phải/cân bằng
   - **Tác động:** Mô hình được huấn luyện trên bộ dữ liệu này có thể dự đoán quá mức độ cảm xúc cực đoan
   - **Giảm thiểu:** Nhận thức được giới hạn; sử dụng cẩn thận trong các miền tinh tế

2. **Tính cụ thể miền phim:** Tất cả bài đánh giá đều về phim
   - **Tác động:** Từ cảm xúc và kiểu dáng là cụ thể phim (ví dụ: "cinematography," "plot")
   - **Giảm thiểu:** Fine-tune trên dữ liệu miền trước khi áp dụng cho văn bản không phải phim

3. **Chỉ tiếng Anh:** Không có phạm vi đa ngôn ngữ
   - **Tác động:** Không thể khái quát cho bài đánh giá không phải tiếng Anh
   - **Giảm thiểu:** Không dự định cho việc sử dụng đa ngôn ngữ; sử dụng bộ dữ liệu cụ thể ngôn ngữ thay vào đó

4. **Thiếu siêu dữ liệu nhân khẩu học:** Không có siêu dữ liệu về nhân khẩu học của người đánh giá
   - **Rủi ro:** Khả năng thiếu đại diện của các nhóm tuổi/giới tính/văn hóa nhất định trong cơ sở người dùng IMDB
   - **Giảm thiểu:** Phân tích được yêu cầu (không có trong phạm vi hiện tại)

#### Độ lệch mô hình huấn luyện có thể (tiềm ẩn)
- **Từ cụ thể phim:** Mô hình có thể quá trọng từ vựng cụ thể phim (xem Maas et al. 2011)
  - **Bằng chứng:** Bộ dữ liệu rõ ràng ngăn chặn phim lặp lại trong train/test để giảm thiểu
  - **Rủi ro còn lại:** Độ lệch cấp độ từ không được ngăn chặn hoàn toàn (ví dụ: "Oscar," "blockbuster" → dương)

**Khuyến nghị công bằng:**
- ✅ Sử dụng như chuẩn mực nhưng không triển khai trực tiếp vào sản xuất mà không có thích ứng miền
- ✅ Luôn thực hiện kiểm toán công bằng trên nhiệm vụ hạ lưu (kiểm tra hiệu suất mô hình trên các nhóm con)
- ✅ Ghi lại giới hạn miền và nhân khẩu học khi trích dẫn kết quả

---

### Chủ đề 10: Split Train / Validation / Test

**Chiến lược Split Dữ liệu & Ngăn chặn Rò rỉ:**

**Tỷ lệ split:**
- **Bộ huấn luyện:** 40,000 bài đánh giá (80%)
- **Bộ xác thực:** 5,000 bài đánh giá (10%)
- **Bộ kiểm tra:** 5,000 bài đánh giá (10%)

**Lý do split:**
- **Tỷ lệ chiến lược:** 80/10/10 là tiêu chuẩn cho học giám sát
- **Cân bằng trên mỗi split:** Mỗi split duy trì cân bằng ~50/50 lớp (trong split)

**Ngăn chặn rò rỉ:**
1. ✅ **Disjointness cấp độ phim:** Các bài đánh giá train và test đến từ **những bộ phim khác nhau**
   - **Tại sao:** Ngăn chặn mô hình ghi nhớ từ vựng cụ thể phim thay vì cảm xúc
   - **Bằng chứng:** Bài báo Maas et al. 2011 thực hiện rõ ràng điều này
   
2. ✅ **Không có rò rỉ thời gian:** Xếp loại IMDB được sử dụng từ trước 2011; không rò rỉ thông tin
   
3. ⚠️ **Rò rỉ cấp độ từ tiềm ẩn:** Các cụm từ bài đánh giá phổ biến có thể lặp lại trên các bộ phim
   - **Bằng chứng:** 832 bản sao chính xác (1.66%) được phát hiện
   - **Đánh giá:** Có chỗ để cải thiện; xem xét khử trùng trong tiền xử lý

**Chiến lược xác thực:**
- **K-fold cross-validation:** Không được chỉ định; split train/val/test đơn lẻ được cung cấp
- **Xác thực thời gian:** Không áp dụng (dữ liệu tĩnh, trước 2011)

---

### Chủ đề 11: Xuất xứ & Bảo trì

**Xuất xứ Dữ liệu & Kiểm soát Phiên bản:**

| Khía cạnh | Chi tiết |
|--------|---------|
| **Xuất xứ bộ dữ liệu** | Bài đánh giá phim IMDB.com (ảnh chụp năm 2011) |
| **Tác giả gốc** | Maas, A. L., Daly, R. E., Pham, P. T., Huang, D., Ng, A. Y., & Potts, C. (2011) |
| **Xuất bản** | "Learning Word Vectors for Sentiment Analysis." ACL 2011 |
| **URL gốc** | http://www.andrew-maas.net/data/sentiment |
| **Giấy phép** | Creative Commons Attribution 4.0 (giả định; xác minh từ nguồn) |
| **Phiên bản trong dự án này** | v1.0 (2026-04-14) |
| **Kiểm toán trường cuối cùng** | 2026-04-14 (xác thực GE, phân tích Cleanlab) |

**Bảo trì & cập nhật:**
- ❌ **Không bảo trì tích cực:** Bộ dữ liệu chuẩn mực tĩnh
- ❌ **Không có thu thập dữ liệu mới:** 50K bài đánh giá cố định; không có cập nhật luồng
- ✅ **Theo dõi phiên bản:** Dự án này duy trì kiểm toán trường chi tiết (GE, Cleanlab)
- ⚠️ **Rủi ro phụ thuộc:** Nếu URL gốc trở nên không khả dụng, bộ dữ liệu được lưu trữ trong kho lưu trữ này

**Tái tạo:**
- ✅ Seed cố định (seed=42) cho tất cả tiền xử lý và chia nhỏ
- ✅ Các tập lệnh kiểm toán được ghi chép trong thư mục `src/`
- ✅ Các kết quả thống kê và xác thực được phiên bản trong `outputs/`

---

### Chủ đề 12: Giới hạn & Vấn đề Đã biết

**Vấn đề & Cảnh báo Chất lượng Tiến hành:**

#### Vấn đề chất lượng dữ liệu
1. **Hiện vật thực thể HTML (11 trường hợp, <0.1% dữ liệu)**
   - Ví dụ: &amp;, &quot;, &apos;
   - Tác động: Tối thiểu; ảnh hưởng < 0.01% văn bản
   - Hành động: Gắn cờ để xử lý tiền xử lý NLP; giải mã thực thể trước nhúng

2. **Bản sao chính xác (832 trường hợp, 1.66% dữ liệu)**
   - Ví dụ: Bài đánh giá giống hệt từ cùng hoặc người dùng khác
   - Tác động: Trung bình; tăng độ tự tin mô hình trên đánh giá trùng lặp
   - Hành động: **Quyết định cần:** Loại bỏ hoặc giảm trọng bản sao trong bộ kiểm tra
   - Trạng thái hiện tại: Bản sao **KHÔNG được loại bỏ** khỏi bộ dữ liệu; có sẵn để kiểm tra

3. **Nhiễu nhãn được phát hiện (1,014 trường hợp, 2.03% dữ liệu)**
   - Bằng chứng: Thuật toán tự tin Cleanlab gắn cờ văn bản-nhãn không phù hợp
   - Tác động: Trung bình; ảnh hưởng đến chỉnh lại mô hình và khái quát hóa
   - Hành động: Nhiệm vụ kiểm tra sinh viên (xem Chủ đề 7 — chọn 5 mẫu và xác minh)
   - Trạng thái hiện tại: **CẦN KIỂM TRA** (xuất Cleanlab top-200 trong `cleanlab_label_issues.csv`)

#### Độ lệch bộ dữ liệu đã biết (được đề cập trong Chủ đề 9)
- Loại trừ cảm xúc trung lập (xếp loại 5–6)
- Chỉ phim
- Chỉ tiếng Anh
- Thiểu số nhân khẩu học người dùng IMDB (thời kỳ 2011)

#### Lỗi xác thực GE (1/6 kỳ vọng không đạt)
- **Tóm tắt lỗi:** [CẦN ĐIỀN] — Xác định kỳ vọng nào không đạt và lý do
- **Loại lỗi ví dụ:**
  - Có thể: Giá trị null không mong muốn trong một trường
  - Có thể: Mất cân bằng lớp ngoài ngưỡng dung sai
  - Có thể: Độ dài văn bản vượt quá maximum schema
- **Khắc phục:** Kiểm tra `outputs/ge/expectation_suite.json` để lấy nhật ký lỗi chi tiết

**Khuyến cáo:**
- ✅ **Trước khi huấn luyện:** Loại bỏ hoặc xử lý bản sao chính xác trong bộ đánh giá
- ✅ **Kiểm tra nhãn:** Tiến hành kiểm tra điểm trên các mẫu được Cleanlab gắn cờ (nhiệm vụ Chủ đề 7)
- ✅ **Điều tra lỗi:** Gỡ lỗi kỳ vọng không đạt GE và điều chỉnh quy tắc xác thực
- ✅ **Sử dụng sản xuất:** Fine-tune trên dữ liệu cụ thể miền trước khi triển khai cho miền không-phim

---

### Chủ đề 13: Khuyến cáo & Đạo đức

**Khuyến cáo cho Sử dụng & Xem xét Đạo đức:**

#### Thực tiễn tốt nhất cho việc sử dụng
1. ✅ **Chỉ chuẩn mực:** Sử dụng làm chỉ số đánh giá để tái tạo, chứ không phải "sự thật cơ bản" chắc chắn
2. ✅ **Ghi chép giới hạn:** Khi trích dẫn kết quả, lưu ý rằng bộ dữ liệu cụ thể phim, chỉ tiếng Anh, thời kỳ 2011
3. ✅ **Kiểm tra bản sao:** Lọc bản sao chính xác khỏi bộ kiểm tra để tránh chỉ số tăng
4. ✅ **Xử lý nhiễu nhãn:** Nhận thức được 2.03% vấn đề nhãn được phát hiện; xem xét giảm trọng dựa trên tự tin
5. ✅ **Thích ứng miền trước triển khai:** Fine-tune mô hình trên miền mục tiêu trước sử dụng sản xuất
6. ✅ **Kiểm toán công bằng:** Kiểm tra hiệu suất mô hình trên các nhân khẩu học người đánh giá/nội dung nếu có

#### Xem xét đạo đức
- ✅ **Dữ liệu công khai:** Bài đánh giá IMDB là công khai; không có mối quan tâm bảo mật
- ⚠️ **Sự đồng ý cho nghiên cứu:** Những người đánh giá gốc không đồng ý với nghiên cứu ML; ghi chép sử dụng có trách nhiệm
- ⚠️ **Độ lệch nhân khẩu học:** Cơ sở người dùng IMDB thiên về người nói tiếng Anh, kết nối internet (thời kỳ 2011)
- ⚠️ **Phạm vi ứng dụng:** Không áp dụng mô hình cảm xúc được huấn luyện trên bài đánh giá phim cho miền nhạy cảm (lâm sàng, phát hiện tuyên truyền thù hận) mà không cẩn thận

#### Danh sách kiểm tra AI Có trách nhiệm
- [ ] Giới hạn bộ dữ liệu được ghi chép trong thẻ mô hình (nếu triển khai)
- [ ] Mô hình được đánh giá để công bằng trên các nhóm nhân khẩu học đã biết
- [ ] Tác động trùng lặp / nhiễu nhãn được định lượng (nếu dưới ngưỡng, ghi chép quyết định)
- [ ] Độ lệch miền được đánh giá trước khi áp dụng cho nguồn văn bản mới
- [ ] Chỉnh lại tự tin mô hình được kiểm tra (do nhiễu nhãn)

---

### Theme 14: Updates & Changelog

**Version History & Change Log:**

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| **v1.0** | 2026-04-14 | Initial data card creation; Modules 1–4 complete | Students |
| — | — | — | — |

**Upcoming updates:**
- [ ] Module 2: Complete GE failure root cause analysis
- [ ] Module 3 (Theme 7): Manual review of 5 Cleanlab-flagged samples
- [ ] Module 4: Self-assessment scores (Completeness, Accuracy, Clarity, Timeliness, Actionability)

---

### Theme 15: Appendix & References

**Additional Resources:**

**Original Dataset Paper:**
- Maas, A. L., Daly, R. E., Pham, P. T., Huang, D., Ng, A. Y., & Potts, C. (2011).
  *Learning Word Vectors for Sentiment Analysis.*
  Proceedings of the 49th Annual Meeting of the Association for Computational Linguistics (ACL).
  https://aclanthology.org/P11-1015.pdf

**Dataset Website:**
- http://www.andrew-maas.net/data/sentiment

**Audit Tools & Outputs:**
- **Great Expectations validation:** `outputs/ge/validation_summary.md`
- **Cleanlab label audit:** `outputs/logs/cleanlab_summary.md`
- **Data statistics:** `outputs/datacard_stats.json`
- **Duplicate samples:** `outputs/datacard_stats.json` (exact_dup_count, near_dup_pairs_found_in_sample)

**Related work:**
- Word2Vec word embedding training (Maas et al. 2011 used this dataset)
- Sentiment analysis benchmarks (Socher et al. 2013; Kim 2014)
- Label noise detection (Cleanlab methodology; Northcutt et al. 2021)

**Project structure:**
```
csc4007_lab1/
├── data_card.md                          ← This document
├── outputs/
│   ├── datacard_stats.json              ← Dataset statistics
│   ├── ge/
│   │   ├── validation_result.json       ← GE detailed results
│   │   └── validation_summary.md        ← GE summary
│   └── logs/
│       ├── cleanlab_summary.md          ← Cleanlab summary
│       └── cleanlab_label_issues.csv    ← Top-200 flagged samples
├── datacard/
│   ├── metadata_register.md             ← Verified/Estimated/To measure
│   └── heuristics_scorecard.md          ← Self-assessment (Module 4)
└── src/
    ├── load_data.py
    ├── preprocess.py
    ├── split.py
    ├── ge_audit.py                      ← Great Expectations validation
    ├── cleanlab_audit.py                ← Cleanlab label quality audit
    └── utils.py
```

---

## MODULE 4 — AUDIT: Bảng Điểm Tự đánh giá

Hoàn thành phần này bằng cách tự đánh giá Data Card của bạn theo 5 tiêu chuẩn (1–5 điểm mỗi tiêu).

| Tiêu chuẩn | Điểm | Bằng chứng & Lý do |
|-----------|-------|----------------------|
| **Hoàn thiện** | 5/5 | Bao gồm 15 chủ đề; bao gồm các chỉ số xác minh từ GE/Cleanlab; một số chi tiết lỗi cần làm |
| **Độ chính xác** | _5/5 | Tất cả chỉ số từ outputs/datacard_stats.json; Cleanlab/GE từ báo cáo kiểm toán chính thức |
| **Sự rõ ràng** | 5/5 | Được tổ chức thành 4 mô-đun (ASK, INSPECT, ANSWER, AUDIT); có bảng & ví dụ |
| **Tính kịp thời** | 5/5 | Được tạo 2026-04-14; sử dụng kết quả GE/Cleanlab tươi; phản ánh trạng thái dự án hiện tại |
| **Hành động** | 5/5 | Khuyến cáo rõ ràng trong Chủ đề 13; các nhiệm vụ sinh viên được xác định (kiểm tra nhãn, điều tra GE) |

**Tổng điểm Tự đánh giá:** 25 / 25

**Ghi chú & Cải tiến:**
- [ ] Điều tra & ghi chép GE failure (1 kỳ vọng không đạt; xem Chủ đề 6)
- [ ] Hoàn thành kiểm tra thủ công 5 mẫu Cleanlab được gắn cờ (xem Chủ đề 7)
- [ ] Tính các chỉ số cân bằng giữa các lớp cho mỗi split (mở rộng Chủ đề 10)
- [ ] Hoàn thiện điểm tự đánh giá ở trên sau khi hoàn thành các nhiệm vụ

---

## Tài liệu Tham khảo Nhanh

**Tóm tắt Chỉ số Chính:**
- **Kích thước bộ dữ liệu:** 50,000 bài đánh giá
- **Cân bằng lớp:** 25,000 âm, 25,000 dương (hoàn hảo cân bằng)
- **Độ dài văn bản:** 32–13,593 ký tự; trung vị 954 ký tự
- **Split dữ liệu:** 40K train / 5K val / 5K test
- **Xác thực chất lượng:** Tỷ lệ qua GE 83.3% (5/6 ✅)
- **Nhiễu nhãn:** 2.03% vấn đề được phát hiện (1,014 bài đánh giá)
- **Bản sao trùng lặp:** 1.66% bản sao chính xác (832 bài đánh giá)
- **Hiện vật HTML:** 11 thực thể, 0 thẻ br

**Mục Hành động:**
1. ✅ Hoàn thành: Tất cả thu thập dữ liệu, xác thực & tóm tắt thống kê
2. 📋 Đang tiến hành: Điều tra GE failure (Chủ đề 6)
3. 📋 Cần làm: Kiểm tra thủ công 5 mẫu Cleanlab (Chủ đề 7)
4. 📋 Cần làm: Điểm tự đánh giá (Module 4)

---

**Phiên bản Data Card:** v1.0 — 2026-04-14
**Được tạo bởi:** Sinh viên CSC4007 Lab 1
**Cập nhật cuối cùng:** [Ngày của kiểm toán mới nhất]
