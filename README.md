# Mô phỏng thiết bị sát hạch lái xe

Ứng dụng web tĩnh (thuần HTML/CSS/JS, không framework, không build step) mô
phỏng lại nguyên lý hoạt động của thiết bị chấm điểm dùng trong kỳ thi sát
hạch lái xe ô tô: khẩu lệnh âm thanh, chấm điểm trừ dần từ 100, lỗi liệt (loại
trực tiếp), đếm giờ 20s/30s ở bài xuất phát, và hai chế độ **Sa hình** /
**Đường trường**.

Đây là bản dựng lại độc lập theo đúng nghiệp vụ chấm điểm (viết mới hoàn toàn
HTML/CSS/JS), không sao chép mã nguồn hay thương hiệu của bất kỳ ứng dụng nào
khác. Chỉ có phần âm thanh khẩu lệnh (`audio/sat-hach/*.wav`) và tên file gốc
được giữ nguyên để đảm bảo trải nghiệm nghe sát với thiết bị thật.

## Nghiệp vụ chấm điểm (tóm tắt)

- Mỗi lượt thi bắt đầu với 100 điểm; **đạt** khi kết thúc còn ≥ 80 điểm.
- Mỗi lỗi bị trừ điểm theo mức riêng (mặc định 5, có lỗi 1/2/10/25 điểm).
- Một số lỗi là **lỗi liệt** (LOẠI): phạm phải là trượt ngay bất kể điểm còn lại.
- **Sa hình**: 11 bài + bài tình huống khẩn cấp; riêng bài Xuất phát tự đếm
  ngược — quá 20s trừ 5 điểm, quá 30s bị đánh trượt ngay lập tức.
- **Đường trường**: 4 giai đoạn (xuất phát, tăng số, giảm số, dừng xe kết
  thúc), tập trung vào kỹ năng côn — số — ga — phanh và tuân thủ hiệu lệnh sát
  hạch viên.

Chi tiết đầy đủ từng lỗi/điểm trừ xem trong mục "Bảng điểm" ngay trên trang,
hoặc đọc trực tiếp dữ liệu `MODES` trong `index.html`.

## Chạy thử local

```bash
python3 -m http.server 8080
# mở http://localhost:8080/
```

## Deploy lên Netlify

1. Kéo thả thư mục này vào [app.netlify.com/drop](https://app.netlify.com/drop), hoặc
2. Kết nối repo GitHub này với Netlify (New site from Git) — `netlify.toml` đã có sẵn `publish = "."`.

## Deploy lên GitHub Pages

- Cách 1 (khuyến nghị): **Settings → Pages → Build and deployment → Source: GitHub Actions**.
  Workflow tại `.github/workflows/pages.yml` tự deploy mỗi khi push lên `main`/`master`.
- Cách 2: **Settings → Pages → Source: Deploy from a branch**, chọn nhánh và thư mục `/ (root)`.

## Cấu trúc

- `index.html` — toàn bộ giao diện + logic (CSS/JS inline), không phụ thuộc backend.
- `audio/sat-hach/*.wav` — 147 file khẩu lệnh/hiệu ứng âm thanh.
- `favicon.svg`, `manifest.json` — icon và khai báo PWA tối giản, tự thiết kế.
