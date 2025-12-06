# Survival Game (Dart/Flutter)

Một dự án trò chơi sinh tồn 2D, xây dựng bằng [Dart](https://dart.dev/) và [Flutter](https://flutter.dev/).  
Bạn sẽ điều khiển nhân vật vượt qua các thử thách trong môi trường tự nhiên: khai thác, chế tạo, chiến đấu, xây dựng, và sống sót qua ngày.

---

## 📁 Kiến trúc thư mục

```
lib/
│
├─ main.dart                    # Điểm khởi tạo game
├─ core/                        # Các thành phần cốt lõi
│   ├─ constants/               # Biến, cấu hình, hệ số cân bằng game
│   ├─ utils/                   # Hàm tiện ích toán học, vector, random...
│   └─ services/                # Dịch vụ hệ thống: âm thanh, dialog, lưu game...
│
├─ game/                        # Logic chính của game
│   ├─ survival_game.dart       # Lớp game tổng
│   ├─ player/                  # Các lớp về người chơi
│   ├─ world/                   # Quản lý thế giới, tile, object, ánh sáng, thời tiết...
│   ├─ items/                   # Định nghĩa vật phẩm, công cụ, vũ khí...
│   ├─ crafting/                # Quản lý chế tạo và công thức
│   ├─ combat/                  # Hệ thống chiến đấu, sát thương...
│   ├─ enemy/                   # Định nghĩa quái vật, AI
│   ├─ building/                # Xây dựng công trình và quản lý
│   ├─ physics/                 # Va chạm (collision)
│   └─ systems/                 # Hệ thống gameplay: đói, stamina, lưu tự động, sự kiện...
│
├─ ui/                          # Giao diện người dùng
│   ├─ hud/                     # Hiển thị: thanh máu, đói, minimap...
│   ├─ inventory/               # Giao diện kho đồ
│   ├─ crafting/                # Giao diện chế tạo
│   ├─ dialogs/                 # Dialog: info vật phẩm, setting, màn hình chết
│   └─ menu/                    # Menu chính, pause, loading
│
└─ config/                      # Cấu hình tài nguyên, mức khó
```

---

## 📦 Thiết kế mở rộng

Cấu trúc dự án được thiết kế theo hướng module hóa, giúp việc phát triển và mở rộng chức năng trở nên dễ dàng:

- **Tách riêng từng chức năng vào thư mục/module** ví dụ: player, world, enemy, items, crafting, ui...
- **Thêm module mới dễ dàng**: Để thêm một hệ thống hoặc chức năng (ví dụ, hệ thống nhiệm vụ, vật phẩm mới, kiểu quái vật mới, chế độ chơi...), chỉ cần tạo thêm một thư mục hoặc file theo đúng chuẩn trong `game/`, `ui/` hoặc `config/`.
- **Sử dụng các service/lớp quản lý chung**: Các service ở `core/services` và các manager trong `game/` hỗ trợ tích hợp và kết nối những thành phần mới một cách thuận tiện.
- **Tuân thủ chuẩn code và tài liệu**: Khuyến khích viết code rõ ràng, sử dụng comment và tài liệu cho các class chính để việc bảo trì và nâng cấp sau này dễ dàng hơn.
- **Tách biệt UI và Logic**: Giao diện (`ui/`) tách biệt hoàn toàn với logic game (`game/`), giúp team frontend và backend/logic phát triển song song.

Nhờ thiết kế này, dự án phù hợp với phát triển lâu dài, góp ý, đóng góp từ cộng đồng và tích hợp các tính năng mới một cách mạch lạc, ít xung đột.

---

## 🧩 Mô tả hệ thống

### 1. **core/**
- Quản lý các giá trị cố định cho game (màu sắc, cấu hình, cân bằng).
- Các hàm tiện ích toán học, vector, tạo số ngẫu nhiên.
- Các dịch vụ như lưu game, xử lý âm thanh, quản lý hộp thoại.

### 2. **game/**
- **survival_game.dart:** Lớp trung tâm, điều phối mọi hoạt động.
- **player/:** Quản lý trạng thái, inventory, animation, điều khiển và hành vi của nhân vật.
- **world/:** Tạo map theo thuật toán noise, quản lý tile, object (cây, đá, quặng, bụi berry), chu trình ngày đêm, ánh sáng, thời tiết (mưa, tuyết).
- **items/:** Định nghĩa, quản lý các loại vật phẩm, công cụ, vũ khí, đồ tiêu dùng và database vật phẩm.
- **crafting/:** Quản lý công thức, bàn chế tạo và logic chế tạo.
- **combat/:** Hệ thống sát thương, hitbox và quản lý vũ khí.
- **enemy/:** Quản lý các kiểu quái vật như zombie, chó sói, thuật toán AI (chase, patrol, attack).
- **building/:** Quản lý xây dựng (wall, campfire, workbench) và hệ thống đặt công trình.
- **physics/:** Quản lý va chạm (collision) cho vật thể trong game.
- **systems/:** Hệ thống đói, stamina, thời gian, autosave và event bus.

### 3. **ui/**
- **hud/:** Giao diện HUD game (thanh máu, thanh đói, slot công cụ, minimap).
- **inventory/:** Giao diện kho đồ, quản lý slot inventory.
- **crafting/:** Hiển thị giao diện chế tạo, recipe card.
- **dialogs/:** Các dialog thông báo, info vật phẩm, setting, màn hình chết.
- **menu/:** Menu chính, tạm dừng, màn hình loading.

### 4. **config/**
- Quản lý đường dẫn tài nguyên, cấu hình game và độ khó.

---

## 🚀 Hướng dẫn chạy dự án

**Yêu cầu:**  
- Dart SDK  
- Flutter SDK

**Các bước:**  
1. Clone repository về máy:
    ```
    git clone https://github.com/<owner>/<repo>.git
    cd <repo>
    ```
2. Cài đặt package:
    ```
    flutter pub get
    ```
3. Chạy project:
    ```
    flutter run
    ```
   *Có thể chọn thiết bị (device) tương thích với Flutter.*

---

## 💡 Tính năng chính

- Khai thác, chế tạo, xây dựng và sinh tồn trong môi trường mở.
- Quản lý hunger, stamina, chu trình ngày đêm, thời tiết động.
- Đối đầu với quái vật AI, chiến đấu và khám phá thế giới.
- Giao diện trực quan hỗ trợ HUD, inventory, crafting, dialog và menu.
- Lưu dữ liệu và tự động lưu gameplay.
- Hệ thống vật phẩm, công thức chế tạo và công trình đa dạng.

---

## 📖 Đóng góp & phát triển

- Pull requests, báo lỗi và feature request đều hoan nghênh!
- Vui lòng xem lại kiến trúc thư mục, chuẩn code Dart/Flutter trước khi đóng góp.

---

## 📄 Giấy phép

Thông tin license sẽ được bổ sung tại đây.

---

Nếu cần chi tiết hơn cho từng module, hoặc muốn chuẩn bị tài liệu API từng class/file, hãy yêu cầu thêm nhé!