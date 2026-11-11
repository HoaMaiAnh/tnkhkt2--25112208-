# tnkhkt2--25112208-
bai tap ve nha

bai vidu1
https://wokwi.com/projects/476556798922393601

bai vidu2
https://wokwi.com/projects/476562079369719809
#TH2

## 1. So sánh delay(), millis() và Hardware Timer

### 1.1. Mục tiêu
So sánh delay(), millis() và Hardware Timer trên ESP32.

### 1.2. Thông số thử nghiệm
| Thông số | Giá trị |
|---|---|
| Chu kỳ mục tiêu | 100 ms |
| Thời gian thử nghiệm | 3000 ms |
| Baud rate Serial | 115200 |

### 1.3. Kết quả thực nghiệm
| Phương pháp | Số lần | Độ lệch trung bình (ms) | Độ lệch lớn nhất (ms) |
|---|---:|---:|---:|
| delay() | 29 | 0.000 | 0.000 |
| millis() | 29 | 0.001 | 0.010 |
| Hardware Timer | 28 | 0.001 | 0.001 |

### 1.4. Nhận xét và kết luận
- **delay():** Độ lệch đo được rất nhỏ, tuy nhiên chương trình bị blocking trong thời gian chờ.
- **millis():** Không gây blocking, độ lệch lớn nhất 0.010 ms
- **Hardware Timer:** Độ lệch lớn nhất 0.001 ms, duy trì chu kỳ ổn định.

## 2. Deep Sleep định giờ (Timer Wakeup)

### 2.1. Mục tiêu
Tìm hiểu chế độ Deep Sleep của ESP32 và cách sử dụng Timer Wakeup để tự động đánh thức thiết bị sau một khoảng thời gian xác định.

### 2.2. Kết quả quan sát

Chạy chương trình trên ESP32 với thời gian Deep Sleep được thiết lập là 10 giây, ta thấy:

- ESP32 khởi động và hiển thị thông báo trên Serial Monitor.
- Biến `dem` được khai báo bằng `RTC_DATA_ATTR` và tăng thêm 1 sau mỗi lần thức dậy.
- ESP32 tự động đi vào Deep Sleep sau khi in thông báo.
- Sau khoảng 10 giây, ESP32 thức dậy và chạy lại chương trình từ hàm `setup()`.

**Kết quả Serial Monitor:**

```text
ESP32 da thuc day!
So lan thuc day: 1
Ngu 10 giay...

ESP32 da thuc day!
So lan thuc day: 2
Ngu 10 giay...

ESP32 da thuc day!
So lan thuc day: 3
Ngu 10 giay...
```

### 2.3. Nhận xét và kết luận

ESP32 có thể sử dụng Timer Wakeup để tự động thức dậy sau khoảng thời gian Deep Sleep đã thiết lập.

Chương trình được khởi động lại từ hàm `setup()` sau khi ESP32 thức dậy.

Có thể dùng Deep Sleep kết hợp Timer Wakeup và RTC Memory để tiết kiệm năng lượng và lưu trữ dữ liệu qua các lần ngủ.


# TH4 - ESP32 - REST API - MQTT - Node-RED

## 1. Nội dung thực hành

### Bài 1: REST API

- Kết nối ESP32 với mạng Wi-Fi.
- Trả về dữ liệu cảm biến dưới định dạng JSON.
- Dữ liệu bao gồm nhiệt độ, độ ẩm, thời gian hoạt động và thông tin Wi-Fi.

### Bài 2: MQTT Publish

- Kết nối ESP32 với MQTT Broker.
- Đọc dữ liệu từ cảm biến AHT20.
- Publish dữ liệu định kỳ 2 giây.

### Bài 3: Node-RED Dashboard và MQTT Subscribe

- Hiển thị nhiệt độ và độ ẩm từ ESP32.
- Tạo nút điều khiển LED thông qua MQTT.
- ESP32 subscribe topic điều khiển và xử lý lệnh nhận được.
- LED được điều khiển thông qua GPIO14.
- Payload `1`: Bật LED.
- Payload `0`: Tắt LED.

### Bài 4: MQTT Explorer

- Kết nối MQTT Explorer với MQTT Broker.
- Theo dõi cây topic của nhóm.
- Kiểm tra payload JSON được ESP32 publish.

## 2. Kết quả đạt được

- Kết nối ESP32 với Wi-Fi thành công.
- Đọc dữ liệu nhiệt độ và độ ẩm từ cảm biến AHT20.
- Publish dữ liệu cảm biến lên MQTT Broker.
- Hiển thị dữ liệu trên Node-RED
- Theo dõi và kiểm tra dữ liệu bằng MQTT Explorer
