# Đóng gói "Chấm Bài AI" thành file APK

Repo này biến app web (trong thư mục `www/`) thành **file .apk** cài được trên Android, **build tự động trên GitHub** — không cần cài Android Studio.

## Cấu trúc
```
www/                         ← toàn bộ app (index.html, icons...)
package.json                 ← khai báo Capacitor
capacitor.config.json        ← tên app, mã ứng dụng
.github/workflows/build-apk.yml ← máy chủ GitHub tự build APK
```

## Các bước (làm 1 lần ~10 phút)

### 1. Tạo repo trên GitHub
- Vào github.com → **New repository** → đặt tên (vd `cham-bai-ai`) → Create.

### 2. Tải toàn bộ thư mục này lên repo
- Cách dễ nhất: trên trang repo bấm **Add file → Upload files**, kéo tất cả (gồm cả thư mục `www` và `.github`) vào, rồi **Commit**.
- *(Lưu ý: nếu kéo thả mà thiếu thư mục `.github`, hãy tạo thủ công file `.github/workflows/build-apk.yml` và dán nội dung vào.)*

### 3. Đợi GitHub build
- Vào tab **Actions** trên repo → sẽ thấy "Build APK" đang chạy (mất khoảng 3–5 phút).
- Khi xong (dấu ✓ xanh), bấm vào lần chạy đó.

### 4. Tải file APK
- Kéo xuống mục **Artifacts** → tải `cham-bai-ai-apk` → giải nén ra file `app-debug.apk`.

### 5. Cài lên điện thoại
- Chuyển file `app-debug.apk` vào điện thoại (qua Zalo, USB, Google Drive...).
- Mở file → Android hỏi cho phép "cài từ nguồn không xác định" → đồng ý → Cài đặt.
- Mở app, vào ⚙ nhập Gemini API key một lần là dùng được.

## Cập nhật app sau này
Sửa file trong `www/` rồi commit lại → GitHub tự build APK mới. Tải lại ở tab Actions.

## Ghi chú kỹ thuật
- APK này là bản **debug** (cài trực tiếp, chia sẻ cho đồng nghiệp được). Nếu sau này muốn đưa lên **Google Play**, cần thêm bước ký số (signing) — khi cần sẽ bổ sung workflow ký APK.
- Mã ứng dụng: `vn.edu.chambaiai` (đổi trong `capacitor.config.json` nếu muốn).
- App cần mạng khi gọi AI chấm bài; dữ liệu điểm và ảnh lưu offline trong máy.
