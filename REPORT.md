# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu.

* Mã học viên theo lớp: 2A202602190
* Ngày / CVAT local: 17/09/2026
* Công cụ đã dùng: CVAT localhost:8080

## 1. Bài đã nộp

| Task            | File ZIP đúng tên     | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau)|
| --------------- | --------------------- | -----------------: | --------------------------:|
| easy_semantic   | `easy_semantic.zip`   |              3 / 3 |                            |
| medium_instance | `medium_instance.zip` |              3 / 3 |                            |
| hard_panoptic   | `hard_panoptic.zip`   |              2 / 2 |                            |
| cp1_holes       | `cp1_holes.zip`       |              1 / 1 |                            |
| cp2_slice       | `cp2_slice.zip`       |              1 / 1 |                            |
| cp5_occlusion   | `cp5_occlusion.zip`   |              1 / 1 |                            |
| cp3_thin        | `cp3-thin.zip`        |              1 / 1 |                            |
| cp4_curb        | `cp4_curb.zip`        |              1 / 1 |                            |
| cp6_coverage    | `cp6_coverage.zip`    |              1 / 1 |                            |
| **Tổng tối đa** |                       |                    |                      **** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh đầu tiên là `000000181542.jpg`, object đầu tiên là **motorcycle**, ở góc phải màn hình.
- Class và quy tắc tôi dùng để chọn biên: **motorcycle; tôi vẽ theo phần xe thực sự nhìn thấy, bám sát đường viền bên ngoài của xe và không lấy phần nền hoặc các vật thể tách biệt xung quanh.**
- Nếu dùng gợi ý sau đó: **vùng gợi ý được đối chiếu với ảnh gốc; nếu gợi ý lấn sang nền hoặc thiếu một phần của motorcycle thì tôi chỉnh lại mask theo đường biên nhìn thấy, phần đúng thì giữ lại.**
- Nếu không dùng gợi ý: **không dùng.**

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: **`medium_instance` — ảnh `000000181542.jpg`, vùng motorcycle ở góc phải.**
- Lỗi thuộc loại: **biên.**
- Bằng chứng tôi nhìn thấy: **Khi kiểm tra lại mask với ảnh gốc, một số điểm biên ở phần thân/bánh xe chưa bám sát đường viền của motorcycle, có nguy cơ lấy sang phần nền xung quanh.**
- Quy tắc và hành động sửa: **Tôi chỉnh lại các điểm biên theo phần motorcycle thực sự nhìn thấy, loại phần mask bị dư vào nền và kiểm tra lại để không làm mất phần xe.**
- Sau sửa đã Save và export lại chưa? **Đã Save và export lại ZIP.**
- Kết quả tự đánh giá trên GitHub Actions hoặc script liên quan đến lỗi vừa sửa: **chưa có điểm.**

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Ảnh `000000181542.jpg`, motorcycle ở góc phải, khu vực bánh xe và thân xe | 1. Lấy cả phần nền/chi tiết nằm sát xe. 2. Chỉ lấy phần thuộc motorcycle. | Đường biên của motorcycle có thể phân biệt với nền và các vật thể xung quanh. | Tôi chọn **chỉ lấy phần motorcycle nhìn thấy**, không lấy nền. |
| Ảnh đường phố có nhiều xe, các xe nằm gần hoặc che nhau | 1. Gộp các xe gần nhau thành một vùng. 2. Tách từng xe thành từng instance. | Các xe có đường viền và vị trí riêng dù có thể bị chồng lấn. | Tôi chọn **tách từng xe thành từng instance**, không gộp các xe khác nhau. |
| Ảnh có người đi bộ và nhiều motorcycle, khu vực người bị xe che một phần | 1. Vẽ theo hình dạng hoàn chỉnh suy đoán của người. 2. Chỉ vẽ phần người thực sự nhìn thấy. | Một phần cơ thể bị motorcycle che khuất nên không quan sát được đường biên. | Tôi chọn **theo phần nhìn thấy**, không tự suy đoán phần bị che khuất; nếu quy tắc task yêu cầu xử lý khác thì hỏi coach. |
