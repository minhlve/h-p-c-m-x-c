# Hộp Ký Ức

Web cá nhân gồm 4 mục — **Trang chủ (nhạc)**, **Short Video**, **Sad Photos**, **Caption** —
mỗi mục có 30 ô nội dung. Cần đăng nhập/đăng ký để xem. Admin quản lý toàn bộ nội dung.

```
Nơi Chứa Cảm Xúc/
├── index.html        ← khung trang, không sửa gì cũng được
├── style.css      ← toàn bộ giao diện/màu sắc
├── data.js         ← NỘI DUNG trang + tài khoản admin (file bạn sẽ sửa thường xuyên)
├── app.js          ← logic: đăng nhập, hiển thị, chia sẻ, quản trị
└── README.md
```

## 1. Cách đưa web này lên mạng (GitHub Pages — miễn phí)

1. Tạo một repository mới trên GitHub, để **Public**.
2. Upload toàn bộ nội dung của folder này lên repo đó (kéo-thả từng file/folder vào
   trang GitHub, hoặc dùng GitHub Desktop).
3. Vào **Settings → Pages**, chọn Branch `main`, folder `/ (root)` → **Save**.
4. Sau khoảng 1 phút, trang sẽ có địa chỉ dạng:
   `https://ten-github-cua-ban.github.io/ten-repo/`

Gửi link đó cho ai bạn muốn, họ tự đăng ký tài khoản và vào xem.

## 2. Cách thêm nhạc / video / ảnh (upload từ máy lên GitHub)

Trang không tự lưu file bạn upload trực tiếp — bạn cần host file ở một nơi rồi **dán
link** vào. Cách đơn giản nhất là dùng chính GitHub Pages của bạn:

1. Trong repo, tạo các thư mục `nhac/`, `video/`, `anh/`.
2. Bấm **Add file → Upload files**, kéo file từ máy lên, đặt tên rõ ràng
   (ví dụ `nhac-01.mp3`, `video-05.mp4`, `anh-12.jpg`).
3. Sau khi Pages build lại, link dùng được sẽ là:
   `https://ten-github-cua-ban.github.io/ten-repo/nhac/nhac-01.mp3`
4. Dán link đó vào form **Thêm/Sửa** trong trang quản trị.

**Lưu ý:**
- Upload qua web giới hạn **25MB/file**. Video nặng hơn thì nén bớt trước, hoặc dùng
  app **GitHub Desktop** trên máy tính để đẩy file lớn hơn (tới ~100MB).
- Repo để Public thì link mới truy cập công khai được — nghĩa là ảnh/video không
  riêng tư tuyệt đối, ai có đúng link đều xem được file gốc.
- Đừng dùng Git LFS cho các file media này, GitHub Pages không phát được file qua LFS.

## 3. Cách quản lý nội dung (rất quan trọng, đọc kỹ)

Vì trang này **không có server riêng**, nội dung mọi người cùng thấy được lưu thẳng
trong file `js/data.js`. Quy trình thêm/sửa nội dung:

1. Đăng nhập bằng tài khoản admin: `minh1429` / `122873vn`.
2. Thêm/sửa/xoá nội dung như bình thường — lúc này thay đổi **chỉ lưu tạm trên máy
   bạn** (bản nháp), chưa ai khác thấy được.
3. Bấm nút **"Xuất dữ liệu"** ở góc trên bên phải.
4. Copy toàn bộ đoạn chữ hiện ra.
5. Mở file `data.js` trên GitHub, xoá đoạn `const SITE_DATA = {...};` cũ, dán đè
   đoạn vừa copy vào, bấm **Commit changes**.
6. Đợi khoảng 1 phút để GitHub Pages build lại — vậy là mọi người ghé trang đều thấy
   nội dung mới.

> Nếu bỏ qua bước 4–6, thay đổi chỉ hiện trên máy của bạn, người khác sẽ không thấy.

Nút **"Bỏ bản nháp, lấy lại dữ liệu gốc từ data.js"** trong khung Xuất dữ liệu dùng khi
bạn muốn huỷ các sửa đổi đang làm dở và đồng bộ lại đúng theo file `data.js` mới nhất
(ví dụ sau khi bạn đã commit từ một máy khác).

## 4. Đổi tài khoản admin

Mở file `data.js`, sửa 2 dòng đầu:

```js
const ADMIN_USERNAME = "minh1429";
const ADMIN_PASSWORD = "122873vn";
```

## 5. Vài giới hạn cần biết

- **Tài khoản người dùng thường** (đăng ký/đăng nhập) được lưu trong bộ nhớ của
  trình duyệt (localStorage) — chỉ hoạt động trên đúng thiết bị/trình duyệt đã đăng
  ký. Đây không phải hệ thống tài khoản tập trung thật sự; nếu cần nhiều người dùng
  chung tài khoản từ nhiều thiết bị một cách đồng bộ, sẽ cần một backend thật
  (ví dụ Firebase/Supabase) — nói mình biết nếu bạn muốn nâng cấp.
- Nút **"Lưu về máy"** chỉ tải trực tiếp được nếu link nguồn cho phép; nếu không, nó
  tự mở tab mới để lưu thủ công — đây là giới hạn bảo mật của trình duyệt.
- Link chia sẻ dạng `...#music-3` sẽ tự mở đúng ô đó khi người khác bấm vào — chạy
  tốt một khi trang đã có domain thật (GitHub Pages).
- Video/nhạc host trên GitHub Pages phát trực tiếp được trong trang; ảnh luôn hiển
  thị tốt theo cả 2 cách (Pages hoặc link raw).
