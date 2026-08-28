# Web-Design 2026 — Word Search Game

Mini game tìm từ khóa ẩn trong ma trận chữ, xây dựng cho cuộc thi **Web-Design 2026** của câu lạc bộ lập trình. Người chơi tìm 5 từ khóa liên quan đến chủ đề thiết kế web, ẩn trong ma trận 15×15, sau đó xuất ảnh minh chứng hoàn thành để nộp bài.

Dự án là **static website thuần túy** — không backend, không database, không framework — chạy được trực tiếp trên GitHub Pages.

---

## Công nghệ sử dụng

- HTML5, CSS3, JavaScript ES6 Modules (vanilla, không framework)
- [html2canvas](https://html2canvas.hertzen.com/) — thư viện ngoài duy nhất, dùng để xuất ảnh kết quả
- Google Fonts (Montserrat)

---

## Cấu trúc dự án

```
webdesign-2026-wordsearch/
├── index.html              # Khung HTML chính, kết nối toàn bộ CSS/JS
├── README.md
├── .gitignore
│
├── css/
│   ├── style.css            # Reset CSS, biến màu (CSS variables), layout tổng
│   ├── welcome.css          # Style màn hình chào
│   ├── game.css             # Style màn hình chơi (lưới, chip từ khóa, tiến độ)
│   ├── popup.css            # Victory Dialog + capture card (dùng khi xuất ảnh)
│   └── animation.css        # Toàn bộ @keyframes
│
├── js/
│   ├── main.js               # Entry point, điều phối chuyển màn hình
│   ├── config.js             # Hằng số toàn cục (kích thước lưới, từ khóa, hướng...)
│   ├── storage.js            # Đọc/ghi LocalStorage
│   ├── matrix.js             # Thuật toán sinh ma trận + đặt từ khóa
│   ├── selection.js          # Xử lý tap chọn ô, kiểm tra hướng liên tục
│   ├── validator.js          # Kiểm tra chuỗi đã chọn có khớp từ khóa không
│   ├── game.js                # Điều phối trạng thái game, render giao diện
│   ├── animation.js          # Thêm/xóa class CSS để kích hoạt hiệu ứng
│   ├── capture.js            # Xuất ảnh kết quả bằng html2canvas
│   └── utils.js               # Hàm tiện ích dùng chung (random, format, hash...)
│
└── assets/
    ├── logo/                 # Logo cuộc thi
    ├── icons/                # Icon SVG (nếu có)
    └── fonts/                # Font tự host (nếu không dùng Google Fonts CDN)
```

Kiến trúc modular: mỗi file JS chỉ đảm nhiệm đúng 1 trách nhiệm, giao tiếp qua `export`/`import` (ES6 Modules).

---

## Tính năng chính

- Tìm 5 từ khóa: `HTML`, `COLOR`, `LAYOUT`, `BUTTON`, `DESIGN`
- Ma trận chữ 15×15, đặt từ khóa ngẫu nhiên theo thuật toán randomized placement + retry
- Chọn ô bằng cách tap từng ô, tự động nhận diện hướng và nối chuỗi
- Lưu tiến độ vào LocalStorage — refresh trang không mất dữ liệu
- Xuất ảnh kết quả (PNG) kèm watermark và mã xác thực chống gian lận cơ bản
- Giao diện mobile-first, tối ưu thao tác chạm trên điện thoại

---

## Chạy thử trên máy (local)

Dự án dùng ES6 Modules (`type="module"`), **bắt buộc chạy qua local server**, không mở trực tiếp `index.html` bằng trình duyệt (sẽ lỗi CORS).

**Cách 1 — VS Code Live Server (khuyến nghị):**

1. Cài extension **Live Server** (tác giả Ritwick Dey)
2. Chuột phải `index.html` → **Open with Live Server**

**Cách 2 — Python:**

```bash
python -m http.server 8000
```

Mở trình duyệt tại `http://localhost:8000`

### Test trên điện thoại thật (cùng mạng WiFi)

1. Tìm địa chỉ IP nội bộ máy tính: `ipconfig` (Windows) hoặc `ipconfig getifaddr en0` (macOS)
2. Trên điện thoại, truy cập `http://<IP-máy-tính>:5500` (hoặc đúng port Live Server đang chạy)
3. Nếu không kết nối được, kiểm tra Firewall đã cho phép Node.js/port tương ứng

---

## Triển khai lên GitHub Pages

```bash
git init
git add .
git commit -m "feat: khoi tao du an Word Search Game Web-Design 2026"
git remote add origin <URL-repo-cua-ban>
git branch -M main
git push -u origin main
```

Sau đó vào repo trên GitHub → **Settings → Pages** → chọn nhánh `main`, thư mục `/ (root)` → **Save**. Sau vài phút, trang sẽ chạy tại:

```
https://<username>.github.io/<ten-repo>/
```

---

## Quy ước commit

Dự án dùng [Conventional Commits](https://www.conventionalcommits.org/) rút gọn:

| Tiền tố     | Ý nghĩa                                       |
| ----------- | --------------------------------------------- |
| `feat:`     | Thêm tính năng mới                            |
| `fix:`      | Sửa lỗi                                       |
| `style:`    | Thay đổi giao diện/CSS, không ảnh hưởng logic |
| `refactor:` | Tái cấu trúc code, không đổi hành vi          |
| `docs:`     | Cập nhật tài liệu (README...)                 |

Ví dụ: `git commit -m "fix: sua loi freeze khi refresh sau khi thang"`

---

## Giới hạn kỹ thuật cần lưu ý

- **Không có backend/database**: mọi dữ liệu người chơi chỉ lưu cục bộ trên `localStorage` của thiết bị đang chơi, không có nơi tổng hợp tập trung.
- **Mã xác thực (hash) trong ảnh xuất** chỉ là công cụ đối chiếu cơ bản, không phải bằng chứng bảo mật tuyệt đối — phù hợp cho quy mô cuộc thi CLB, không nên dùng cho hệ thống cần bảo mật cao.
- Cấu hình `GRID_SIZE`, danh sách `KEYWORDS`, và hướng đặt từ (`DIRECTIONS`) đều tập trung tại `js/config.js` — mọi thay đổi thông số game chỉ cần sửa đúng file này (lưu ý: `css/popup.css` có 1 chỗ khai báo cứng số cột lưới cho ảnh xuất, cần đồng bộ tay nếu đổi `GRID_SIZE`).

---

## Theo dõi yêu cầu & lỗi

Các yêu cầu chỉnh sửa và báo lỗi được quản lý qua **GitHub Issues** của repo. Xem tab [Issues](../../issues) để biết các thay đổi đang chờ xử lý.

---

## Giấy phép

Dự án phục vụ mục đích học tập và cuộc thi nội bộ câu lạc bộ lập trình, không sử dụng cho mục đích thương mại.
