# Thiết bị giả lập thi sát hạch

Bản sao tĩnh (static mirror) của trang mô phỏng thiết bị giám sát sát hạch lái xe
tại https://thithu.app/gia-lap-thiet-bi-sat-hach — gồm toàn bộ HTML, CSS, JS,
font và 147 file âm thanh khẩu lệnh, không phụ thuộc backend nào, có thể chạy
trực tiếp như một site tĩnh.

## Chạy thử local

```bash
python3 -m http.server 8080
# mở http://localhost:8080/
```

## Deploy lên Netlify

1. Kéo thả thư mục này vào [app.netlify.com/drop](https://app.netlify.com/drop), hoặc
2. Kết nối repo GitHub này với Netlify (New site from Git) — `netlify.toml` đã cấu hình sẵn
   `publish = "."`.

## Deploy lên GitHub Pages

- Cách 1 (khuyến nghị): Vào **Settings → Pages → Build and deployment → Source: GitHub Actions**.
  Workflow tại `.github/workflows/pages.yml` sẽ tự deploy mỗi khi push lên `main`/`master`.
- Cách 2: **Settings → Pages → Source: Deploy from a branch**, chọn nhánh và thư mục `/ (root)`.
  File `.nojekyll` đã có sẵn để GitHub Pages không bỏ qua thư mục `_next`.

## Ghi chú

- Toàn bộ asset (`_next/static`, `audio/sat-hach`, `icons`, `og`) được tải trực tiếp
  từ thithu.app, giữ nguyên tên file gốc.
- 21/168 file âm thanh không tồn tại trên server gốc (là các tên file dự phòng
  không được dùng tới trong bản build hiện tại) nên không có trong bản sao này.
- Trang không gọi API backend nào, mọi logic mô phỏng chạy hoàn toàn phía client.
