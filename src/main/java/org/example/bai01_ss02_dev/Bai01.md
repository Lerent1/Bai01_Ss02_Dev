# EX1 - Khởi tạo Droplet trên DigitalOcean

## 1. Mục tiêu

- Khởi tạo một Droplet trên DigitalOcean.
- Sử dụng Ubuntu Server 22.04 LTS hoặc phiên bản mới nhất.
- Sử dụng cấu hình Basic, CPU Shared, Regular SSD để tiết kiệm chi phí.
- Chọn Region Singapore.
- Sử dụng SSH Key để xác thực thay cho mật khẩu.
- Kết nối thành công tới Droplet bằng tài khoản `root`.

## 2. Tạo SSH Key trên máy cá nhân

Mở Terminal hoặc PowerShell và chạy:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Nhấn `Enter` để sử dụng đường dẫn mặc định.

Sau khi tạo thành công, kiểm tra khóa:

```bash
cat ~/.ssh/id_ed25519.pub
```

Trên Windows PowerShell có thể dùng:

```powershell
Get-Content ~/.ssh/id_ed25519.pub
```

Copy toàn bộ nội dung khóa công khai có dạng:

```text
ssh-ed25519 AAAA... your_email@example.com
```

> Không chia sẻ file `id_ed25519`. Đây là private key.

## 3. Tạo Droplet trên DigitalOcean

Đăng nhập DigitalOcean và chọn:

**Create → Droplets**

Thiết lập:

- **Region:** Singapore
- **Image:** Ubuntu 22.04 LTS hoặc phiên bản Ubuntu mới nhất được yêu cầu
- **Plan:** Basic
- **CPU:** Shared CPU
- **Storage:** Regular SSD
- **Size:** Chọn cấu hình rẻ nhất phù hợp yêu cầu bài tập

Tại mục **Authentication**, chọn:

**SSH Key**

Nếu chưa có SSH Key trên DigitalOcean:

1. Chọn **New SSH Key**.
2. Đặt tên cho SSH Key.
3. Dán nội dung file `id_ed25519.pub`.
4. Lưu SSH Key.
5. Chọn SSH Key vừa tạo cho Droplet.

Sau đó chọn **Create Droplet**.

## 4. Lấy địa chỉ IP của Droplet

Sau khi Droplet được tạo thành công, DigitalOcean sẽ hiển thị địa chỉ IPv4 của máy chủ.

Ví dụ:

```text
IP_ADDRESS = 123.456.78.90
```

Lưu lại địa chỉ IP này để thực hiện kết nối SSH.

## 5. Kết nối tới Droplet bằng SSH

Mở Terminal trên máy cá nhân và chạy:

```bash
ssh -i ~/.ssh/id_ed25519 root@IP_ADDRESS
```

Ví dụ:

```bash
ssh -i ~/.ssh/id_ed25519 root@123.456.78.90
```

Nếu sử dụng Windows và khóa nằm trong thư mục `.ssh` mặc định:

```powershell
ssh -i "$env:USERPROFILE\.ssh\id_ed25519" root@IP_ADDRESS
```

Lần đầu kết nối, Terminal có thể hỏi:

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Nhập:

```text
yes
```

Nếu cấu hình đúng, máy tính sẽ đăng nhập vào Droplet mà không yêu cầu mật khẩu.

## 6. Kiểm tra kết nối

Sau khi đăng nhập thành công, chạy:

```bash
whoami
```

Kết quả:

```text
root
```

Kiểm tra phiên bản Ubuntu:

```bash
lsb_release -a
```

Hoặc:

```bash
cat /etc/os-release
```

Có thể kiểm tra thông tin máy chủ bằng:

```bash
hostnamectl
```

## 7. Kết quả

Kết nối SSH thành công tới Droplet DigitalOcean bằng tài khoản:

```text
root
```

Việc xác thực được thực hiện thông qua SSH Key và không cần nhập mật khẩu.

Ví dụ log kết nối:

```text
Welcome to Ubuntu ...

root@ubuntu:~# whoami
root

root@ubuntu:~# lsb_release -a
Distributor ID: Ubuntu
Description: Ubuntu ...
```

## 8. Minh chứng

Đính kèm các ảnh chụp sau:

### Ảnh 1 - Cấu hình Droplet

Ảnh giao diện DigitalOcean Console thể hiện:

- Ubuntu
- Region Singapore
- Basic Plan
- Shared CPU
- Regular SSD

### Ảnh 2 - SSH Key

Ảnh phần Authentication cho thấy Droplet sử dụng SSH Key.

Không chụp hoặc công khai private key.

### Ảnh 3 - Kết nối SSH thành công

Ảnh Terminal thể hiện:

```text
root@ubuntu:~#
```

và kết quả:

```bash
whoami
```

trả về:

```text
root
```

## 9. Kết luận

Đã hoàn thành việc khởi tạo Droplet trên DigitalOcean với hệ điều hành Ubuntu Server, cấu hình Basic sử dụng Shared CPU và Regular SSD, đặt Region tại Singapore.

Droplet được cấu hình xác thực bằng SSH Key và đã kết nối thành công từ máy cá nhân thông qua SSH với tài khoản `root`.