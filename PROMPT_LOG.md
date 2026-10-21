# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)
- **Họ và tên:** Trần Tấn Tài
- **MSSV:** 125000374
- **Tên đề tài Website:** Landing Page Quán Cà Phê Nghệ Thuật - Mộc Roastery & Coffee
- **Công cụ AI đã sử dụng:** Gemini / ChatGPT / Cursor

## 1. Yêu cầu ban đầu (System/Initial Prompt)
> "Đóng vai một Senior Frontend Developer chuyên về UI/UX. Hãy giúp tôi xây dựng một Landing Page giới thiệu quán cà phê specialty mang tên 'Mộc Roastery'. Yêu cầu bắt buộc:
> 1. Sử dụng chuẩn Semantic HTML5 (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`), tuyệt đối không lạm dụng thẻ `<div>`.
> 2. Quản lý toàn bộ hệ thống màu sắc (tông nâu cà phê, kem sữa, vàng caramel), font chữ và khoảng cách bằng CSS Variables trong `:root`.
> 3. Dàn trang responsive bằng CSS Flexbox và CSS Grid.
> 4. Tích hợp thư viện Animate.css cho Hero Section và AOS (Animate On Scroll) cho các phân đoạn nội dung bên dưới."

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variable
- **Prompt đã dùng:**
  > "Hãy viết file `index.html` và `style.css` cho Mộc Roastery gồm các phần: Thanh điều hướng, Hero Banner, Câu chuyện thương hiệu, Thực đơn 3 món Signature, Không gian quán, Form đặt bàn và Footer. Hãy gom toàn bộ mã màu và khoảng cách vào `:root`."
- **Kết quả AI tạo ra:**
  AI tạo được giao diện có màu sắc khá đẹp, tuy nhiên ở phần danh sách món nước và phần hình ảnh giới thiệu, AI vẫn dùng `<div class="card">` và `<div class="img-box">` theo thói quen thông thường.
- **Nhận xét & Tinh chỉnh của SV:**
  Cấu trúc chưa đạt điểm tối đa về Semantic HTML5. Tôi đã yêu cầu AI thay thế các thẻ `<div class="card">` bằng thẻ `<article class="menu-card">`, bọc hình ảnh kèm giá tiền vào thẻ `<figure>`, và tách phần tiêu đề của từng section vào thẻ `<header class="section-header">` để mã nguồn rõ nghĩa hơn.

### Lần 2: Tích hợp thư viện Animate.css & AOS
- **Prompt đã dùng:**
  > "Tích hợp CDN của Animate.css v4.1.1 vào phần Hero (tiêu đề trượt từ dưới lên, nút CTA phóng to nhẹ) và gắn thuộc tính `data-aos` của thư viện AOS vào các thẻ `<article>` trong phần Thực đơn với độ trễ (delay) tăng dần 100ms, 200ms, 300ms."
- **Thách thức gặp phải:**
  1. Khi áp dụng hiệu ứng `data-aos="fade-left"` ở phần "Câu chuyện thương hiệu", trên màn hình điện thoại xuất hiện thanh cuộn ngang (horizontal scrollbar) gây vỡ khung trang.
  2. Hiệu ứng AOS bị lặp lại liên tục mỗi khi cuộn lên xuống gây rối mắt.
- **Cách sửa prompt (Debug prompt):**
  > "Hiện tại hiệu ứng `fade-left` của AOS làm trang web bị tràn chiều ngang (overflow-x) trước khi phần tử bay vào, và hiệu ứng chạy lại nhiều lần gây rối mắt. Hãy bổ sung `overflow-x: hidden` vào `html, body` trong `style.css`, đồng thời cấu hình hàm `AOS.init({ once: true, offset: 100, duration: 800 })` để hiệu ứng chỉ chạy mượt 1 lần duy nhất khi cuộn tới."

### Lần 3: Tối ưu hiệu ứng `:hover` và `:focus` bằng CSS thuần
- **Prompt đã dùng:**
  > "Bổ sung hiệu ứng `:hover` và `:focus` tự viết bằng CSS cho các nút bấm (`.btn`, `.btn-card`) và các thẻ sản phẩm (`.menu-card`). Khi di chuột hoặc dùng phím Tab (`:focus`), thẻ bài viết phải nổi nhẹ lên (`translateY`), ảnh bên trong zoom nhẹ và có viền `outline` màu `var(--accent-color)` để hỗ trợ Accessibility."
- **Kết quả & Tinh chỉnh của SV:**
  AI bổ sung thuộc tính `tabindex="0"` vào thẻ `<article class="menu-card">` và kết hợp `:focus-within` trong CSS, giúp cả người dùng chuột lẫn bàn phím đều thấy rõ hiệu ứng chuyển động mượt mà.

## 3. Đánh giá cá nhân về quá trình Vibe Coding
- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?**
  AI giúp tiết kiệm đến 70% thời gian ở khâu khởi tạo bộ khung HTML/CSS cơ bản, gợi ý bảng màu (Color Palette) hài hòa với chủ đề quán cà phê, tìm kiếm đường dẫn ảnh Unsplash phù hợp và viết sẵn nội dung (copywriting) hấp dẫn cho từng món nước mà không cần dùng chữ giả *Lorem ipsum*.
- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?**
  1. **Càng chi tiết về ràng buộc kỹ thuật, kết quả càng chuẩn:** Nếu chỉ bảo "tạo web quán cà phê", AI sẽ sinh ra rất nhiều thẻ `<div>` và viết mã CSS rời rạc. Phải chỉ định rõ danh sách thẻ Semantic HTML5 và biến `:root` ngay từ đầu.
  2. **Kiểm tra chéo và chủ động Debug:** AI thường không tự lường trước các lỗi giao diện thực tế như tràn khung ngang (`overflow-x`) khi dùng thư viện animation. Sinh viên cần hiểu bản chất HTML/CSS để phát hiện lỗi và ra lệnh tinh chỉnh chính xác.
