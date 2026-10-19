# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Phạm Vũ Minh Tâm
- **MSSV:** 15000472
- **Tên đề tài Website:** AURA Coffee Roasters - Landing Page Quán Cà Phê Specialty Hiện Đại
- **Công cụ AI đã sử dụng:** ChatGPT-4o, Gemini 3.8, Google Studio AI, Antigravity

---

## 1. Yêu cầu ban đầu (System / Initial Prompt)

> **Prompt đã dùng:**
> *"Tôi là sinh viên ngành CNTT đang làm bài thi thực hành Thiết kế Web. Đóng vai trò là một Senior Front-end Developer và chuyên gia UI/UX hàng đầu:
> 1. Xây dựng một Landing Page mang phong cách tối giản, sang trọng cho quán Specialty Coffee tên 'AURA COFFEE'.
> 2. Sử dụng 100% chuẩn Semantic HTML5 (bắt buộc đầy đủ `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`). Tuyệt đối không lạm dụng thẻ `<div>` bừa bãi.
> 3. Tích hợp thư viện Animate.css trên Hero Section và AOS (Animate On Scroll) cho toàn bộ các section cuộn trang.
> 4. Viết file `style.css` riêng biệt, bắt buộc khai báo hệ thống biến `:root` (CSS Variables) để quản lý màu sắc, typography và spacing. Dùng CSS Grid & Flexbox, tuân thủ responsive mobile-friendly.
> Hãy viết code mẫu đầy đủ, không viết tắt, chú thích rõ ràng."*

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iterations)

### Lần 1: Dựng khung Semantic HTML & CSS Variables
- **Prompt đã dùng:**
  > *"Xem lại mã HTML và CSS vừa tạo:
  > - Ở phần danh sách sản phẩm thực đơn (Menu), bạn đang dùng các thẻ `<div class='card'>`. Hãy sửa lại thành thẻ `<article class='product-card'>` để đúng ngữ nghĩa bài viết/sản phẩm độc lập.
  > - Thêm các biến CSS Variables cho dark background `#121316` và màu nhấn vàng đồng `#c59b6d` trong `:root` để toát lên vibe sang trọng."*
- **Kết quả AI tạo ra:**
  - AI đã thay thế hoàn toàn thẻ `<div>` thành `<article>` cho 3 card sản phẩm.
  - Bổ sung hệ thống CSS Tokens trong `:root`: `--bg-dark`, `--primary-color`, `--text-main`, `--transition-smooth`.
- **Nhận xét & Tinh chỉnh của SV:**
  - Cấu trúc cây DOM đã chặt chẽ và đạt chuẩn W3C. 
  - Đã chủ động yêu cầu AI thêm hiệu ứng `:focus` bên cạnh `:hover` trên nút bấm để đảm bảo tính tiếp cận (Accessibility - a11y).

---

### Lần 2: Tích hợp thư viện Animate.css & AOS (Animate On Scroll)
- **Prompt đã dùng:**
  > *"Tích hợp link CDN của Animate.css (phiên bản 4.1.1) và thư viện AOS.js (phiên bản 2.3.1). Thêm hiệu ứng `animate__fadeInUp` cho phần tiêu đề Hero, và thuộc tính `data-aos='fade-up'` có delay so le cho 3 thẻ trong About và Menu."*
- **Thách thức gặp phải:**
  - Sau khi gắn thẻ `data-aos="fade-up"`, khi cuộn chuột các section nội dung bị biến mất (opacity = 0) hoặc không kích hoạt hiệu ứng cuộn.
- **Cách sửa prompt (Debug prompt):**
  > *"Thư viện AOS không kích hoạt khi cuộn trang, các phần tử bị ẩn mất. Hãy kiểm tra xem: Tôi đã gọi hàm `AOS.init()` sau khi nhúng file script chưa? Có xung đột `overflow-x: hidden` giữa `html` và `body` không? Hãy cung cấp đoạn mã cấu hình chuẩn cho AOS."*
- **Giải pháp AI & Kết quả khắc phục:**
  - AI phát hiện thiếu đoạn script `AOS.init({ duration: 800, once: true });` ở cuối thẻ `<body>`.
  - Đồng thời chỉ ra thuộc tính `overflow-x: hidden` trên thẻ `html` đôi khi làm ngắt sự kiện cuộn (scroll event) của AOS, chuyển thuộc tính này chỉ nằm ở `body`.
  - Hiệu ứng cuộn trang mượt mà ngay lập tức.

---

### Lần 3: Tối ưu UI/UX & Responsive Layout
- **Prompt đã dùng:**
  > *"Hãy tối ưu hóa giao diện trên màn hình di động (<768px): Khi thu nhỏ, các card ở phần Menu và About phải co giãn linh hoạt bằng CSS Grid `minmax()`, typography co giãn theo hàm `clamp()`, và menu header ẩn đi gọn gàng."*
- **Kết quả AI tạo ra:**
  - Đã thêm Media Queries xử lý Grid từ 3 cột về 2 cột và 1 cột.
  - Dùng `font-size: clamp(2.5rem, 5vw, 4rem);` giúp tiêu đề co giãn chuẩn trên cả điện thoại lẫn màn hình 4K.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?**
  - AI giúp sinh nhanh khung mẫu boilerplate HTML ban đầu, tra cứu chuẩn xác cú pháp CDN và tạo các bảng màu tương phản phối sẵn cực kỳ nhanh chóng. Thay vì mất 2 tiếng gõ thủ công từng dòng CSS flexbox/grid, tôi chỉ mất 20 phút để dựng xong khung tổng thể.
- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web:**
  1. **Prompt phải có ngữ cảnh rõ ràng:** Chỉ định rõ role ("Senior Front-end Engineer"), phong cách thiết kế ("Minimalist Specialty Coffee"), và tiêu chuẩn kỹ thuật cụ thể (thẻ Semantic HTML5 nào, thư viện nào).
  2. **Tư duy kiểm soát (Human-in-the-loop):** AI rất hay có thói quen lạm dụng thẻ `<div>` hoặc quên khởi tạo hàm JavaScript của thư viện bên thứ 3. Người lập trình phải hiểu sâu kiến trúc HTML/CSS để review và kịp thời đưa ra prompt chỉnh sửa (Iteration).