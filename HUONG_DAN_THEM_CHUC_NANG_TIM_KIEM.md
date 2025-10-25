# Hướng dẫn thêm 3 chức năng tìm kiếm mới

## Tổng quan
Đã thêm thành công 3 chức năng tìm kiếm mới vào ứng dụng e-commerce:
1. **Tìm kiếm theo màu sắc sản phẩm**
2. **Tìm kiếm theo kích thước sản phẩm**
3. **Tìm kiếm theo xuất xứ sản phẩm**

## Các thay đổi đã thực hiện

### 1. Cập nhật Schema Typesense (`scripts/populateTypesenseIndex.js`)
- Thêm trường `color` (string, facet: true)
- Thêm trường `size` (string, facet: true)
- Thêm trường `origin` (string, facet: true)
- Thêm logic tự động phân loại màu sắc, kích thước và xuất xứ dựa trên tên và mô tả sản phẩm

### 2. Cập nhật Frontend (`src/app.js`)
- Thêm 3 widget `refinementList` mới:
  - `#color-list` - Bộ lọc theo màu sắc
  - `#size-list` - Bộ lọc theo kích thước
  - `#origin-list` - Bộ lọc theo xuất xứ
- Cập nhật template hiển thị sản phẩm để hiển thị màu sắc, kích thước và xuất xứ

### 3. Cập nhật HTML (`index.html`)
- Thêm 3 section mới trong sidebar:
  - "Filter by Color"
  - "Filter by Size"
  - "Filter by Origin"

## Cách chạy ứng dụng

### Bước 1: Cài đặt dependencies
```bash
npm install
```

### Bước 2: Khởi động Typesense server
```bash
npm run typesenseServer
```

### Bước 3: Tạo file .env
Tạo file `.env` với nội dung:
```
TYPESENSE_HOST=localhost
TYPESENSE_PORT=8108
TYPESENSE_PROTOCOL=http
TYPESENSE_ADMIN_API_KEY=xyz
TYPESENSE_SEARCH_ONLY_API_KEY=xyz
```

### Bước 4: Index dữ liệu
```bash
npm run indexer
```

### Bước 5: Khởi động ứng dụng
```bash
npm start
```

Mở trình duyệt tại: http://localhost:3001

## Tính năng mới

### 1. Tìm kiếm theo màu sắc
- Hiển thị danh sách các màu sắc có sẵn
- Cho phép tìm kiếm màu sắc
- Hiển thị số lượng sản phẩm cho mỗi màu
- Có thể chọn nhiều màu cùng lúc

### 2. Tìm kiếm theo kích thước
- Hiển thị danh sách các kích thước có sẵn
- Cho phép tìm kiếm kích thước
- Hiển thị số lượng sản phẩm cho mỗi kích thước
- Có thể chọn nhiều kích thước cùng lúc

### 3. Tìm kiếm theo xuất xứ
- Hiển thị danh sách các quốc gia/xuất xứ có sẵn
- Cho phép tìm kiếm xuất xứ
- Hiển thị số lượng sản phẩm cho mỗi xuất xứ
- Có thể chọn nhiều xuất xứ cùng lúc

### 4. Hiển thị sản phẩm
- Mỗi sản phẩm hiện hiển thị:
  - Màu sắc (badge màu xám)
  - Kích thước (badge màu xanh)
  - Xuất xứ (badge màu vàng)

## Logic phân loại tự động

### Màu sắc
- **Red**: red, crimson, scarlet
- **Blue**: blue, navy, azure, turquoise
- **Black**: black, dark, charcoal (mặc định)
- **White**: white, clear, transparent
- **Gray**: gray, grey, silver, brushed
- **Green**: green, emerald, forest
- **Pink**: pink, rose, magenta
- **Yellow**: yellow, gold, golden
- **Purple**: purple, violet, lavender

### Kích thước
- **Small**: mini, small, compact, case, protector
- **Medium**: standard, regular, normal, phone (mặc định)
- **Large**: plus, large, big, max, pro
- **Extra Large**: xl, extra large, jumbo

### Xuất xứ
- **USA**: usa, united states, america, american, made in usa, usa made
- **China**: china, chinese, made in china, china made, hong kong, taiwan (mặc định)
- **Japan**: japan, japanese, made in japan, japan made, tokyo
- **Germany**: germany, german, made in germany, germany made, berlin
- **Italy**: italy, italian, made in italy, italy made, milan, rome
- **France**: france, french, made in france, france made, paris
- **UK**: uk, united kingdom, britain, british, made in uk, england, london
- **Korea**: korea, korean, made in korea, korea made, south korea, seoul
- **India**: india, indian, made in india, india made, mumbai, delhi
- **Vietnam**: vietnam, vietnamese, made in vietnam, vietnam made, ho chi minh, hanoi

## Cách tùy chỉnh

### Thêm màu sắc mới
Chỉnh sửa object `colorKeywords` trong `scripts/populateTypesenseIndex.js`:

```javascript
const colorKeywords = {
  'red': ['red', 'crimson', 'scarlet'],
  'blue': ['blue', 'navy', 'azure', 'turquoise'],
  // Thêm màu mới
  'orange': ['orange', 'amber', 'peach'],
  // ...
};
```

### Thêm kích thước mới
Chỉnh sửa object `sizeKeywords` trong `scripts/populateTypesenseIndex.js`:

```javascript
const sizeKeywords = {
  'Small': ['mini', 'small', 'compact', 'case', 'protector'],
  'Medium': ['standard', 'regular', 'normal', 'phone'],
  // Thêm kích thước mới
  'XXL': ['xxl', 'extra extra large'],
  // ...
};
```

### Thêm xuất xứ mới
Chỉnh sửa object `originKeywords` trong `scripts/populateTypesenseIndex.js`:

```javascript
const originKeywords = {
  'USA': ['usa', 'united states', 'america', 'american', 'made in usa', 'usa made'],
  'China': ['china', 'chinese', 'made in china', 'china made', 'hong kong', 'taiwan'],
  // Thêm xuất xứ mới
  'Canada': ['canada', 'canadian', 'made in canada', 'canada made'],
  // ...
};
```

### Thay đổi giao diện
- Chỉnh sửa CSS classes trong `src/app.js`
- Thay đổi màu sắc badge trong template hiển thị sản phẩm

## Lưu ý
- Sau khi thay đổi schema hoặc logic phân loại, cần chạy lại `npm run indexer`
- Có thể cần xóa collection cũ trước khi tạo mới bằng cách set `FORCE_REINDEX=true` trong file .env
