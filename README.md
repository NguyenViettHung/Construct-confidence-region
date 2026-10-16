# Bài tập: Ước lượng điểm và khoảng tin cậy

Xây dựng khoảng tin cậy (KTC) 95% trên bộ dữ liệu dinh dưỡng ngũ cốc ăn sáng (`cleaned_cereal.csv`), cài đặt các công thức thống kê bằng Python.

## Cấu trúc thư mục

```
.
├── xayDungKhoangTinCay.ipynb   # Notebook: lý thuyết + code + kết quả
├── cleaned_cereal.csv          # Dữ liệu (77 loại ngũ cốc, 16 cột)
└── README.md
```

## Dữ liệu

77 loại ngũ cốc từ các hãng lớn (Kellogg's, General Mills, Post, Quaker Oats, ...). Các cột chính dùng trong bài:

| Cột | Ý nghĩa |
|-----|---------|
| `carbo` | Lượng carbohydrate (g) mỗi khẩu phần, biến định lượng |
| `shelf` | Vị trí kệ trưng bày (1 = dưới, 3 = trên), biến định tính |

### Tiền xử lý

- Loại các sản phẩm ở kệ 2 để `shelf` trở thành biến nhị phân (kệ 1: ở dưới, kệ 3: ở trên).
- Loại dòng có `carbo = -1` (mã dữ liệu thiếu).
- Mẫu cuối cùng: n = 70 (kệ 1: 34, kệ 3: 36).

## Nội dung

| Câu | Yêu cầu | Phương pháp |
|-----|---------|-------------|
| (a) | KTC 95% cho kỳ vọng `carbo` | Thống kê Z (n > 30, định lý giới hạn trung tâm), dùng S thay σ |
| (b) | KTC 95% cho phương sai `carbo` | Thống kê χ² với n-1 bậc tự do |
| (c) | KTC 95% cho tỷ lệ sản phẩm ở kệ dưới | Xấp xỉ chuẩn cho tỷ lệ mẫu (kiểm tra np̂ > 5, n(1-p̂) > 5) |
| (d) | KTC 95% cho hiệu kỳ vọng µ₁ - µ₂ giữa kệ dưới và kệ trên | Thống kê Z hai mẫu độc lập |

## Kết quả

| Câu | Khoảng tin cậy 95% |
|-----|--------------------|
| (a) Kỳ vọng `carbo` | (13.8389 ; 15.7039) |
| (b) Phương sai `carbo` | (11.6491 ; 22.8140) |
| (c) Tỷ lệ kệ dưới | (0.3686 ; 0.6028) |
| (d) µ₁ - µ₂ |  (-1.3098 ; 2.4274) |

Kết luận (d): khoảng chứa 0 nên chưa đủ bằng chứng cho thấy lượng carbohydrate trung bình giữa hai nhóm kệ khác nhau.

## Ghi chú

- Các hàm `mean`, `var_sample`, `std_sample` tự cài đặt bằng NumPy, không dùng hàm thống kê có sẵn của pandas.
- Dùng `scipy.stats.norm` và `scipy.stats.chi2` để lấy giá trị tới hạn.
