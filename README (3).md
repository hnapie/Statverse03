# STATVERSE – Learn. Play. Solve. Level Up.

Website tĩnh (HTML/CSS/JS thuần + KaTeX qua CDN). Không cần build, không cần backend.

## Cấu trúc
- `index.html` – toàn bộ ứng dụng
- `netlify.toml` – cấu hình Netlify (publish thư mục gốc, header bảo mật, cho phép camera/micro)

## Triển khai GitHub → Netlify
1. Tạo repo mới trên GitHub, tải 4 tệp này lên (kéo thả trong giao diện web, hoặc `git push`).
2. Vào app.netlify.com → **Add new site → Import an existing project** → chọn GitHub → chọn repo.
3. Build command để trống, Publish directory: `.` → **Deploy**. Netlify cấp HTTPS (cần cho camera/micro).

## Khóa AI (Gemini)
Mỗi người dùng tự lấy khóa miễn phí tại https://aistudio.google.com/apikey, rồi bấm **🔑 Khóa AI** trên thanh điều hướng:
dán khóa → *Tải danh sách model* → *Thử kết nối* → *Lưu*. Khóa lưu trong `localStorage` (`sv_gkey`, `sv_gmodel`) của chính trình duyệt đó.
Hàm `SM()` trong `index.html` gọi Gemini trực tiếp từ trình duyệt; khóa không nằm trong mã nguồn nên repo công khai vẫn an toàn.

## Đã có / chưa có
Đã có: trang chủ, nền vũ trụ, giải bài 5 bước + lời giải 4 bước, nhập đề bằng gõ/ảnh/camera/dán ảnh/Word (.docx)/PDF/giọng nói + nhận dạng bằng Gemini, thanh ký hiệu, KaTeX, bảng Laplace, chatbot nổi, đọc tiếng Việt, TUTOR, Chơi trò chơi (7 chương x 10 câu, hỏi AI bằng giọng sau mỗi câu), Ôn tập (thống kê thật từ lịch sử chơi), Diễn đàn (bài đăng, dán ảnh, xem trước KaTeX, thẻ mở/thu gọn, trả lời, AI gợi ý).
Hạn chế: Diễn đàn lưu trên từng thiết bị (localStorage), chưa chia sẻ giữa người dùng; công thức Word (OMML) chưa tự chuyển LaTeX; chưa có bảng viết ảo.
Chưa có: đăng nhập, kết bạn, chat 1-1, QR (cần thêm bảng dữ liệu Supabase).

## Supabase (tài khoản + Diễn đàn dùng chung)
1. supabase.com → **New project** (chọn vùng gần bạn, đặt và lưu mật khẩu database).
2. **SQL Editor → New query** → dán toàn bộ `supabase-setup.sql` → **Run**.
3. **Authentication → Sign In / Providers → Email**: với lớp học nên tắt "Confirm email" (email xác nhận miễn phí bị giới hạn số lượng gửi; tên mục có thể khác tùy giao diện).
4. **Authentication → URL Configuration**: đặt Site URL là địa chỉ Netlify của bạn.
5. **Project Settings → API**: sao chép **Project URL** và **publishable key** (hoặc anon key). Không dùng secret/service_role key.
6. Deploy lên Netlify, mở site → **☁️ Tài khoản** → dán URL + key → *Lưu & kết nối* → đăng ký. Hoặc điền sẵn vào `supabase-config.js` để cả lớp khỏi phải dán.

Lưu ý: cả lớp dùng cùng một dự án Supabase mới thấy chung Diễn đàn. Gói miễn phí tự tạm dừng nếu 1 tuần không có hoạt động; vào trang quản trị bấm khởi động lại. Khóa Gemini thì mỗi người tự nhập khóa riêng ở nút 🔑 Khóa AI.
