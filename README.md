# Bài 2: Khởi chạy Web Server Nginx với Port Mapping

## Mục tiêu
Chạy Nginx (`nginx:alpine`) ở chế độ ngầm, ánh xạ cổng `8080:80`, kiểm tra bằng `curl` rồi dọn dẹp.

## Các lệnh đã thực hiện

```bash
# 1. Khởi chạy container
docker run -d -p 8080:80 --name my-web nginx:alpine

# Kiểm tra container đang chạy
docker ps --filter "name=my-web"
# CONTAINER ID   IMAGE          PORTS                                     NAMES
# 2e0f39c80fd3   nginx:alpine   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web

# 2. Kiểm tra trang web
curl http://localhost:8080
# -> HTTP 200, trả về trang "Welcome to nginx!"

# 3. Dọn dẹp
docker stop my-web && docker rm my-web
```

## Kết quả `curl http://localhost:8080` (rút gọn)

```html
<title>Welcome to nginx!</title>
...
<h1>Welcome to nginx!</h1>
<p>If you see this page, nginx is successfully installed and working.</p>
```

## Kết luận
- Container `my-web` chạy image nhẹ `nginx:alpine`, lắng nghe cổng 8080 của máy host.
- `curl` trả về mã HTML có dòng `Welcome to nginx!` — đạt yêu cầu.
- Đã `stop` + `rm` container sau thử nghiệm (`docker ps -a --filter "name=my-web"` không còn kết quả).
