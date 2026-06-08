# BÁO CÁO BÀI TẬP LỚN
## MÔN: PHÁT TRIỂN ỨNG DỤNG TRÊN THIẾT BỊ DI ĐỘNG - TEE0419

---

# PHẦN 1: MIT APP INVENTOR

## 1.1 Giới thiệu MIT App Inventor

MIT App Inventor là công cụ lập trình kéo-thả giúp tạo ứng dụng Android mà không cần viết code truyền thống.

### Các thành phần chính
- **Designer**: Thiết kế giao diện.
- **Blocks**: Kéo-thả block để lập trình logic.

### Giao diện làm việc

![Giao diện App Inventor](anh/1.png)

**Các bước chứng minh đã làm bài:**
1. Truy cập MIT App Inventor.
2. Tạo project mới.
3. Quan sát giao diện Designer.

---

    ## 1.2 Thanh công cụ, kéo thả và thuộc tính

    ### Các thanh công cụ

    | Thành phần | Công dụng |
    |---|---|
    | Palette | Chứa component |
    | Viewer | Màn hình thiết kế |
    | Components | Danh sách component |
    | Properties | Chỉnh thuộc tính |

    ### Cách kéo thả

    1. Chọn component ở **Palette**.
    2. Kéo vào **Viewer**.
    3. Chỉnh thuộc tính ở **Properties**.

    ![Kéo thả component](anh/2.png)

### Ví dụ thay đổi thuộc tính
- Text
- Width/Height
- BackgroundColor
- FontSize

![Chỉnh thuộc tính](anh/3.png)

---

## 1.3 Blocks

### Bản chất kéo thả block
Block là các khối lệnh logic được ghép lại để tạo chức năng ứng dụng.

### Ưu điểm
- Không cần nhớ cú pháp.
- Dễ học.
- Trực quan.

### Nhược điểm
- Khó quản lý project lớn.
- Ít linh hoạt hơn code.

### Backpack (Copy/Paste Block)
Cho phép copy block giữa nhiều Screen.

![Backpack](anh/4.png)

---

## 1.4 App 3 Screen

### Screen 1: About bản thân

**Chức năng**
- Hiển thị ảnh cá nhân.
- Họ tên, MSSV, lớp.
- 2 nút sang Screen2 và Screen3.

### Các bước làm

1. Tạo Screen1.
2. Kéo Label, Image, Button.
3. Đặt text.
4. Tạo Button điều hướng.

![Screen1 Designer](anh/5.png)

### Block chuyển màn hình

```text
when Button1.Click
open another screen "Screen2"

when Button2.Click
open another screen "Screen3"
```

![Screen1 Blocks](anh/6.png)

---

### Screen 2: Giải toán đơn giản

**Ví dụ bài toán:** Tính BMI

### Giao diện
- TextBox nhập chiều cao
- TextBox nhập cân nặng
- Button tính
- Label kết quả

### Các bước làm

1. Tạo Screen2.
2. Thêm TextBox.
3. Thêm Button.
4. Viết block tính.

![Screen2 Designer](anh/7.png)

### Block xử lý

```text
BMI = weight / (height * height)
```

![Screen2 Blocks](anh/8.png)

---

### Screen 3: WebView

**Website:** https://k58kmt.tdh.io.vn

### Các bước làm
1. Tạo Screen3.
2. Kéo WebViewer.
3. Nhập URL.

![Screen3 Designer](anh/9.png)

![Screen3 chạy web](anh/10.png)

---

# PHẦN 2: ANDROID STUDIO

## 2.1 AndroidManifest.xml

### Công dụng
- Khai báo quyền.
- Khai báo Activity.
- Cấu hình ứng dụng.

### Permission

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.CAMERA"/>
```

### Các bước chứng minh
1. Mở Android Studio.
2. Vào AndroidManifest.xml.
3. Thêm permission.

![Manifest](anh/11.png)

---

## 2.2 Vòng đời Activity

Các hàm chính:

- onCreate()
- onStart()
- onResume()
- onPause()
- onStop()
- onDestroy()

`onCreate()` có sẵn vì đây là điểm khởi tạo đầu tiên của Activity.

![Lifecycle](anh/12.png)

---

## 2.3 Check quyền Runtime

```java
if (ContextCompat.checkSelfPermission(this,
Manifest.permission.CAMERA)
!= PackageManager.PERMISSION_GRANTED) {

ActivityCompat.requestPermissions(this,
new String[]{Manifest.permission.CAMERA},1);
}
```

### Ý nghĩa
Xin quyền khi ứng dụng cần dùng camera.

![Permission runtime](anh/13.png)

---

## 2.4 XML Layout

### Hardcode

```xml
android:text="Xin chao"
```

### Tham chiếu

```xml
android:text="@string/app_name"
```

### Ưu điểm
- Đổi ngôn ngữ.
- Hỗ trợ dark mode.
- Dễ chỉnh sửa.

![Layout XML](anh/14.png)

---

## 2.5 Layout chứa component

Ví dụ `LinearLayout`:

```xml
<LinearLayout
android:orientation="vertical"/>
```

### Gravity
- `gravity`: căn nội dung.
- `layout_gravity`: căn vị trí view.

![LinearLayout](anh/15.png)

---

## 2.6 Event

### Cách 1

```xml
android:onClick="handleClick"
```

### Cách 2

```java
button.setOnClickListener(v -> {
});
```

![Event click](anh/16.png)

---

## 2.7 Assets

### Công dụng
Lưu file dữ liệu offline.

### Truy cập

```java
InputStream is = getAssets().open("data.json");
```

### Ứng dụng
App hướng dẫn món ăn offline.

![Assets](anh/17.png)

---

# PHẦN 3: APP1 - DỮ LIỆU TỪ ASSETS

## Ý tưởng app

**App tra cứu món ăn Việt Nam**

### Dữ liệu
- File JSON trong Assets.

### Thuật toán
1. Đọc file JSON.
2. Parse dữ liệu.
3. Hiển thị RecyclerView.

### Các bước làm

1. Tạo thư mục assets.
2. Thêm foods.json.
3. Tạo RecyclerView.

![App1 danh sách](anh/18.png)

![Chi tiết món ăn](anh/19.png)

![Chi tiết món ăn](anh/23.png)

![Chi tiết món ăn](anh/24.png)

---

# PHẦN 4: APP2 - ANDROID STUDIO

## Activity 1: About

- Hiển thị thông tin cá nhân.
- Button chuyển Activity.

![Activity1](anh/20.png)

---

## Activity 2: Giải toán + API

### Ví dụ
Giải phương trình bậc 2.

### Gửi API

```json
{
"app_by":"MSSV",
"input":{"a":1,"b":2,"c":3},
"output":{"ketluan":"vo nghiem"}
}
```

API:
https://k58kmt.tdh.io.vn/api

![Activity2](anh/21.png)

![Kết quả API](anh/22.png)

---

## Activity 3: WebView

URL:

```text
https://k58kmt.tdh.io.vn?masv=MSSV
```

![Activity3](anh/23.png)

---





