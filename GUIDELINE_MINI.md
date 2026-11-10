# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |	Xe chở người dạng xe con; gồm sedan, hatchback, SUV, taxi và xe bán tải. |Sedan thường có khoang động cơ, khoang hành khách và cốp sau; SUV cao, thân lớn nhưng vẫn là xe con. Xe bán tải thuộc car, dù có thùng hàng phía sau. |
| `truck` |	Xe tải chở hàng hoặc xe đầu kéo. | Thường có cabin tách biệt với thùng hàng lớn, thùng kín hoặc rơ-moóc. Xe tải lớn thuộc truck, còn xe bán tải/cabin nhỏ thuộc car.|
| `bus` | 	Xe buýt hoặc minibus dùng để chở khách.|Xe thân dài, nhiều cửa sổ và ghế hành khách; minibus chở khách cũng thuộc bus. Phân biệt với van bằng thiết kế chuyên chở hành khách kiểu xe buýt, không chỉ dựa vào kích thước. |
| `van` |	Xe van/minivan dùng để chở hàng hoặc chở người. |Thường có thân hộp, nóc tương đối cao và khoang sau liền với cabin. Van chở hàng hoặc minivan thuộc van; xe buýt lớn thuộc bus; xe con thông thường thuộc car. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Box ôm sát phần thân xe nhìn thấy được, không lấy thêm mặt đường, trời hay xe bên cạnh.
- Vật thể bị che khuất: Vật thể bị che một phần vẫn gán box quanh phần nhìn thấy được nếu nhận diện được lớp.
- Vật thể bị cắt bởi rìa ảnh: Box chạm đúng rìa ảnh khi vật thể bị cắt khung; không đoán phần nằm ngoài ảnh.
- Vật thể rất nhỏ/mơNếu không chắc chắn 100% về lớp và không thể suy luận, không gán box .

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_...` | | | |
| `drive_...` | | | |
| `drive_...` | | | |
