# Simple Auth

Thư mục này chứa các ví dụ về xác thực cơ bản bằng Node.js.

## Cấu trúc thư mục
- `basic_auth.js`: Xác thực cơ bản bằng username/password.
- `cookie_auth.js`: Xác thực sử dụng cookie.
- `img/`: Thư mục chứa hình ảnh minh họa.
- `package.json`: Thông tin dự án và các package phụ thuộc.

## Cài đặt

1. Cài đặt Node.js (>=14).
2. Cài đặt các package phụ thuộc:

```powershell
npm install
```

## Sử dụng

### Chạy xác thực cơ bản
```powershell
node basic_auth.js
```

#### Các chức năng:
- Truy cập `http://localhost:3000/`  
![Welcome! Visit first public resource.](img/image15.png)
- Truy cập `http://localhost:3000/public`: Trang public, không cần đăng nhập.
![Welcome! Visit second public resource.](img/image16.png)
- Truy cập `http://localhost:3000/secure`: Yêu cầu xác thực Basic Auth.
  - Sử dụng header `Authorization: Basic <base64(username:password)>`.
  - Username mặc định: `admin`, Password: `12345`.
  - Nếu xác thực thành công sẽ nhận được thông báo truy cập thành công.
![You have accessed a protected resource](img/image1.png)
## Test lỗi

## Các lỗi được xử lý trong code

### basic_auth.js
- Truy cập `/secure` không có header Authorization:
  - Trả về: `401 Authentication required.`
![Authentication required.](img/image2.png)

- Truy cập `/secure` với sai username/password:
  - Trả về: `403 Access denied.`
![Access denied.](img/image3.png)


### Chạy xác thực bằng cookie
```powershell
node cookie_auth.js
```

#### Các chức năng:
- Đăng nhập: Gửi POST tới `http://localhost:3001/login` với JSON body `{ "username": "admin", "password": "12345" }`.
  - Nếu thành công sẽ nhận được cookie xác thực.
![Logged in!](img/image4.png)
![MongoDB cookie](img/image7.png)
![auth_cookie_token](img/image17.png)

- Đăng nhập sai username/password:
  - Trả về: `401 Invalid credentials`
![Invalid credentials](img/image5.png)

##
- Truy cập profile: Gửi GET tới `http://localhost:3001/profile` kèm cookie `auth_cookie_token`.
  - Nếu cookie hợp lệ sẽ nhận được thông tin người dùng.
![Welcome user 1, your cookie is valid.](img/image14.png)
![auth_cookie_token](img/image6.png)

- Truy cập `/profile` không có cookie hoặc cookie không hợp lệ/hết hạn:
  - Trả về: `401 No cookie found` hoặc `401 Invalid or expired cookie`
  ![No cookie found](img/image10.png)

  ![MongoDB not cookie](img/image12.png)
  ![browser still has cookies](img/image13.png)
  ![Invalid or expired cookie](img/image11.png)

##
- Đăng xuất: Gửi POST tới `http://localhost:3001/logout` để xóa cookie xác thực.
![Logged out.](img/image8.png)
![Not cookie MongoDB](img/image9.png)
![Not cookie logout](img/image18.png)

Các lỗi khác sẽ được trả về theo logic xử lý trong từng route.
