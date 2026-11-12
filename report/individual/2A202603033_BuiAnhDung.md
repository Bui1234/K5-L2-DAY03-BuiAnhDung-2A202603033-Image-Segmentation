# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603033
- Ngày / CVAT local: 11/12/2026
- Công cụ đã dùng: CVAT local

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip |  / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh đầu tiên trong task medium_instance, object person (người) ở vị trí dễ quan sát trong ảnh.
- Class và quy tắc tôi dùng để chọn biên: Tôi chọn class person. Khi vẽ mask, tôi dựa vào đường viền cơ thể người quan sát được, bao gồm phần đầu, thân, tay và chân. Tôi cố gắng bám sát biên của đối tượng, không lấy phần nền xung quanh và không gộp người với các đối tượng khác.
- Nếu dùng gợi ý sau đó: Tôi kiểm tra vùng mask được đề xuất bằng cách đối chiếu với đường viền thực tế của người. Những vùng bám đúng đối tượng có thể được giữ lại; những vùng lấn sang nền hoặc đối tượng khác cần được chỉnh sửa hoặc loại bỏ.
- Nếu không dùng gợi ý: Không áp dụng cho quyết định ban đầu. Tôi thực hiện việc xác định class và đường biên thủ công trước khi xem gợi ý tự động, nhằm đảm bảo có thể tự đưa ra quyết định gán nhãn.nh.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.
- Task/ảnh/vùng: cp6_coverage – ảnh 7daa6479-67988f3f.jpg, toàn bộ mask semantic segmentation.
- Lỗi thuộc loại: Khác – lỗi cấu hình nhãn khi import dữ liệu vào CVAT.
- Bằng chứng tôi nhìn thấy: Khi import file cvat_import_cp6_coverage.zip, CVAT hiển thị thông báo:Label 'background' is not registered for this task.
- Quy tắc và hành động sửa: Tôi kiểm tra bảng màu trong labelmap.txt và nhận thấy mask có sử dụng màu đen (0, 0, 0) cho các vùng không thuộc 7 lớp mục tiêu. 
- Kết quả Summary tự đánh giá: Chưa có điểm

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| cp2_slice – vùng tiếp giáp giữa hai xe ô tô đứng cạnh nhau | Có thể gộp thành một đối tượng hoặc tách thành hai đối tượng riêng biệt. | Quan sát đường viền, thân xe và khoảng phân cách giữa hai xe. Mỗi chiếc xe là một instance riêng. | Tách thành hai instance nếu xác định được hai chiếc xe độc lập. |
| cp5_occlusion – vùng chiếc xe bị một vật thể khác che khuất | Có thể chỉ gán phần nhìn thấy hoặc cố gắng vẽ toàn bộ hình dạng chiếc xe. | Không nhìn thấy được toàn bộ đường viền do hiện tượng che khuất; cần phân biệt phần bị che với phần thực sự không thuộc đối tượng. | Giữ một instance cho chiếc xe, không tách thành nhiều đối tượng chỉ vì bị che khuất. |
| cp3_thin – vùng cột hoặc biển báo giao thông có đường viền mảnh | Có thể bỏ qua vùng nhỏ hoặc gán nhãn theo toàn bộ phần đối tượng nhìn thấy. | Dựa vào hình dạng, vị trí và chức năng của đối tượng; chú ý không mở rộng mask sang nền xung quanh. | Ưu tiên giữ phần đối tượng nhìn thấy. Hỏi coach về độ rộng mask tối thiểu đối với các chi tiết rất mảnh. |
