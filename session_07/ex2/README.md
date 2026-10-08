# Bài 2: Quản trị Tường lửa UFW cho Cụm Dịch vụ Multi-port

## 1. Cấu hình các luật UFW
Các lệnh đã sử dụng để cấu hình tường lửa:

```bash
# Khai báo các chính sách mặc định
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Cho phép kết nối SSH
sudo ufw allow 22/tcp

# Cho phép cổng kết nối Web HTTP
sudo ufw allow 80/tcp

# Cho phép cổng ứng dụng Spring Boot
sudo ufw allow 8082/tcp

# Kích hoạt UFW
sudo ufw enable
```

*Lưu ý: Không thêm luật cho cổng MySQL (3306) để nó bị chặn theo cấu hình mặc định (deny incoming).*

## 2. Kết quả kiểm tra
Đầu ra của lệnh `sudo ufw status verbose`:

```
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
80/tcp                     ALLOW IN    Anywhere
8082/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
80/tcp (v6)                ALLOW IN    Anywhere (v6)
8082/tcp (v6)              ALLOW IN    Anywhere (v6)
```

**Nhận xét kết quả:**
- Trạng thái tường lửa đang là `active`.
- Các cổng `22/tcp`, `80/tcp` và `8082/tcp` đều có trạng thái `ALLOW IN` từ `Anywhere` cho cả IPv4 và IPv6.
- Cổng `3306` (MySQL) không có trong danh sách cho phép, do đó hoàn toàn bị chặn từ bên ngoài theo chính sách mặc định `deny incoming`.
