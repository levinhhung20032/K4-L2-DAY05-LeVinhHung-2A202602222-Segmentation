# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

- Mã học viên theo lớp: 2A202602222
- Ngày / CVAT local: 2026-09-17
- Công cụ đã dùng: AnyLabeling

## 1. Bài đã nộp

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh 000000181542.jpg, vẽ người phụ nữ mặc áo dài ở chính giữa ảnh đầu tiên, sử dụng brush để ôm viền dễ hơn và dễ dàng tẩy phần bị lem
- Class và quy tắc tôi dùng để chọn biên: Dùng Polygon cho những khu vực lớn và cạnh dài, dùng Brush để vẽ các đối tượng có nhiều chi tiết hoặc viền phức tạp 
- Sử dụng gợi ý lên ảnh có nhiều xe, các mô hình xác định biên của các loại xe rất tốt, tận dụng để tiết kiệm thời gian gán nhãn

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: `hard_panoptic` / ảnh `000000460147.jpg`
- Lỗi thuộc loại: phủ vùng
- Bằng chứng tôi nhìn thấy: biên của mask do công cụ gợi ý khúc khuỷu và không bao trọn khi cố gắng chọn đối tượng `road` do có quá nhiều xe trên đường
- Quy tắc và hành động sửa: đánh dấu bằng tay thay vì sử dụng công cụ, quyết định chỉ sử dụng công cụ để đánh dấu các vật thể rõ ràng như `person`, `car`, `truck`, `bus`.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại ZIP, chạy script kiểm tra đạt trạng thái OK.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | `cp2_slice`: Hai xe cùng lớp đỗ sát nhau có cần tách thành 2 instance riêng không? | Hai vật thể độc lập dẫu có phần tiếp giáp/chồng lấn biên. | Quyết định tách thành 2 instance riêng biệt theo đúng yêu cầu instance segmentation. |
| 2 | `cp5_occlusion`: Vật bị che khuất một phần (xe bị che bởi người/vật cản). | Chỉ gán nhãn phần thân thể/vật thể thực tế nhìn thấy được. | Quyết định chỉ vẽ mask ôm trọn phần lộ ra, không tự "đoán" phần bị che khuất hoàn toàn bên trong. |
| 3 | `hard_panoptic`: Vùng ranh giới giao thoa giữa stuff (`road`, `sidewalk`) và thing (`car`). | Stuff phủ nền liên tục, thing nằm đè lên trên lớp stuff. | Đảm bảo lớp thing nằm đè lên trên và không để khoảng trống (hở rìa) giữa các ranh giới. |