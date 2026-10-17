# CNTT1_NhapMonCNTT_Session10_Ex05
﻿# Bài Tập Về Nhà 
# Smart-Farm IoT: Tự Động Hóa Vườn Lan
> **Hệ thống điều hòa vi khí hậu cho vườn phong lan** tích hợp vi xử lý **RikkeiSmartStar**, giúp tự động kiểm soát nhiệt độ - độ ẩm, tối ưu tài nguyên và ngăn ngừa sốc nhiệt.
## Cài Đặt Nhanh
```bash
git clone https://github.com/GreenTech/Smart-Farm-Orchid.git
cd Smart-Farm-Orchid && pip install -r requirements.txt
cp config.example.json config.json
python3 main.py
```
## Tính Năng
- [x] Giám sát nhiệt độ, độ ẩm giá thể và không khí theo thời gian thực.
- [x] Tự động kích hoạt bơm phun sương làm mát khi trời nóng quá mức.
- [x] Tự động kéo lưới che lan khi cường độ sáng quá cao.
- [x] Gửi cảnh báo mất điện/hết nước qua Telegram.
## Thông Số Phần Cứng
| Thành phần | Linh kiện | Giao tiếp | Vai trò (IPO) |
| :--- | :--- | :--- | :--- |
| **SoC** | Rikkeicore  | Wi-Fi / BLE | Xử lý trung tâm |
| **Cảm biến** | Rik30, BH1750 | I2C | Thu thập vi khí hậu |
| **Chấp hành** | Relay 4CH + Bơm phun sương | GPIO Digital | Làm mát, tưới nước |
## Chu Kỳ Fetch–Decode–Execute Khi Tưới Lan
> 1. **Fetch:** CPU nạp mã lệnh `CHECK_AND_PUMP` từ Flash vào thanh ghi chỉ lệnh 
> 2. **Decode:** Control Unit giải mã lệnh so sánh nhiệt độ với ngưỡng an toàn 
> 3. **Execute:** ALU thực thi so sánh; CPU kích GPIO mức `HIGH` đóng rơ-le bật bơm.
## Kim Tự Tháp DIKW: Từ Dữ Liệu Đến Tưới Tiêu
* **Data:** Cảm biến trả số thô `35.2`.
* **Information:** Nhiệt độ giàn lan là 35.2°C
* **Knowledge:** Nhiệt độ trên 32°C kéo dài sẽ làm lan cháy lá và rụng nụ.
* **Wisdom:** Tự kích hoạt chu kỳ phun ngắt quãng để hạ nhiệt an toàn.
## Lưu Ý Xử Lý Khi RAM Đầy Nhật Ký 
* **Bộ đệm vòng:** Tự động ghi đè log cũ nhất khi RAM đạt 85%.
* **Xả dữ liệu:** Lưu tạm log xuống thẻ nhớ/Flash khi chạm 90% dung lượng.
* **Bảo vệ phần cứng:** Tự ngắt bơm trước khi reset để tránh tưới úng lan.
* **Thao tác thủ công:** Giữ nút đỏ `RESET LOG` 5 giây trên hộp máy để giải phóng RAM.
