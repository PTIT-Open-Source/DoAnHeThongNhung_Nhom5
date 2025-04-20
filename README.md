# ⚡ Máy Đo Nồng Độ Cồn

Hiện nay, tình trạng lạm dụng rượu bia đang là một trong những nguyên nhân hàng đầu dẫn đến tai nạn giao thông nghiêm trọng, gây thiệt hại lớn về con người và tài sản. Việc kiểm soát nồng độ cồn của người tham gia giao thông trở thành một biện pháp quan trọng giúp giảm thiểu rủi ro và đảm bảo an toàn cho cả người lái xe và những người xung quanh. Tuy nhiên, các thiết bị đo nồng độ cồn truyền thống thường có kích thước lớn, giá thành cao và chưa thực sự tiện lợi trong việc sử dụng hàng ngày. Sự ra đời của một thiết bị đo nồng độ cồn nhỏ gọn, chính xác và dễ dàng kết nối với các thiết bị di động sẽ là giải pháp hiệu quả nhằm hỗ trợ người dùng kiểm soát tốt hơn nồng độ cồn trong cơ thể trước khi tham gia giao thông.


## 📋 Mục Lục
- [Giới Thiệu](#giới-thiệu)
- [Thông Số Kỹ Thuật](#thông-số-kỹ-thuật)
- [Danh Sách Linh Kiện](#danh-sách-linh-kiện)
- [Sơ Đồ Nguyên Lý và PCB](#sơ-đồ-nguyên-lý-và-pcb)
- [Hướng Dẫn Lắp Ráp](#hướng-dẫn-lắp-ráp)
- [Lập Trình Firmware](#lập-trình-firmware)
- [Cách Sử Dụng](#cách-sử-dụng)
- [Kiểm Thử](#kiểm-thử)
- [Ảnh/Video Demo](#ảnhvideo-demo)
- [Đóng Góp](#đóng-góp)
- [Giấy Phép](#giấy-phép)

---

## Giới Thiệu

**Dự án làm gì?**  
Thiết bị đo nồng độ cồn trong hơi thở, hiển thị kết quả trên OLED và gửi dữ liệu qua WiFi/MQTT.  

**Người dùng chính?**  
- Cá nhân kiểm tra sức khỏe.  
- Cơ quan giao thông, doanh nghiệp vận tải.  

**Mục tiêu thiết kế?**  
- Thực tiễn: Tạo sản phẩm nhỏ gọn, chi phí thấp. 
- Giáo dục: Tìm hiểu ESP32 và hệ thống nhúng.  
 

---

## Thông Số Kỹ Thuật

| Thành phần      | Thông tin                          |
|-----------------|------------------------------------|
| MCU             | ESP32-WROOM-32                    |
| Nguồn vào       | pin Lithium 3.7V  |
| Cảm biến        | MQ3 (đo nồng độ cồn)              |
| Màn hình        | OLED SSD1306 128x64, giao tiếp I2C|
| Kết nối         | WiFi, MQTT                        |

---

## Danh Sách Linh Kiện

| Tên linh kiện      | Số lượng | Ghi chú                     |
|--------------------|----------|-----------------------------|
| ESP32 DevKit v1    | 1        | Vi điều khiển chính         |
| Cảm biến MQ3       | 1        | Đo nồng độ cồn             |
| Màn hình OLED      | 1        | Hiển thị kết quả           |
| Nút nhấn           | 3        | Chọn chế độ và reset       |

---

## Sơ Đồ Nguyên Lý và PCB

- **Sơ đồ nguyên lý**:  
  - MQ3 --> GPIO34 (ADC) của ESP32.  
  - OLED --> I2C (SDA: GPIO21, SCL: GPIO22).  
  - Nút nhấn: GPIO18, GPIO19, GPIO25.  
- **PCB**: Thiết kế bằng Altium Designer.
![image](https://github.com/user-attachments/assets/793693da-2b94-4a5c-bd82-42da41618ccf)
![image](https://github.com/user-attachments/assets/15787af9-e7f9-46d6-9917-20bc672e29de)
![image](https://github.com/user-attachments/assets/37571db1-3703-4fbc-a94a-2ef8a225ca8f)

---

## Hướng Dẫn Lắp Ráp

1. Hàn điện trở kéo lên (4.7kΩ) cho I2C.  
2. Hàn ESP32, MQ3, và OLED theo sơ đồ.  
3. Kiểm tra ngắn mạch bằng đồng hồ vạn năng.  
4. Cấp nguồn và nạp firmware để kiểm tra.  

---

## Lập Trình Firmware

- **Ngôn ngữ**: C++ (Arduino).  
- **File chính**: `main.ino` (trang 26-30 trong báo cáo).  
- **Cách nạp**:  
  ```bash
  platformio run --target upload
