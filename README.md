# 📘 Tài Liệu Training Thực Tập - Java Developer

> Tài liệu tổng hợp kiến thức từ cơ bản đến nâng cao, phục vụ cho kỳ thực tập lập trình Java.

---

# Phần 1: Cấu Trúc Máy Tính Căn Bản

## 📌 Mục lục

1. [Kiến trúc máy tính và các thành phần cơ bản](#1-kiến-trúc-máy-tính-và-các-thành-phần-cơ-bản)
2. [Sự khác nhau giữa RAM và SSD/HDD](#2-sự-khác-nhau-giữa-ram-và-ssdhdd)
3. [Hệ điều hành, Firmware, Driver](#3-hệ-điều-hành-firmware-driver)
4. [Hệ thống quản lý file (Windows vs Linux)](#4-hệ-thống-quản-lý-file-windows-vs-linux)
5. [Tại sao file .exe không thể chạy trên Linux](#5-tại-sao-file-exe-không-thể-chạy-trên-linux)
6. [Ngôn ngữ lập trình là gì](#6-ngôn-ngữ-lập-trình-là-gì)
7. [Trình biên dịch và thông dịch](#7-trình-biên-dịch-và-thông-dịch)
8. [Tại sao file Java có thể chạy ở nhiều môi trường khác nhau](#8-tại-sao-file-java-có-thể-chạy-ở-nhiều-môi-trường-khác-nhau)

---

## 1. Kiến trúc máy tính và các thành phần cơ bản

### 1.1 Kiến trúc Von Neumann

Hầu hết máy tính hiện đại đều tuân theo **kiến trúc Von Neumann** (được đề xuất bởi John von Neumann năm 1945). Kiến trúc này có đặc điểm:

- **Chương trình và dữ liệu được lưu chung** trong bộ nhớ (stored-program concept).
- Máy tính hoạt động theo chu trình **Fetch → Decode → Execute** (Nạp lệnh → Giải mã → Thực thi).

```
┌──────────────────────────────────────────────────────────┐
│                    MÁY TÍNH (Computer)                   │
│                                                          │
│   ┌──────────────┐      Bus hệ thống       ┌─────────┐  │
│   │     CPU      │◄───────────────────────►│   RAM   │  │
│   │ ┌──────────┐ │                          │ (Bộ nhớ │  │
│   │ │   ALU    │ │                          │  chính) │  │
│   │ │(Tính toán)│ │                          └─────────┘  │
│   │ └──────────┘ │                                       │
│   │ ┌──────────┐ │      Bus hệ thống       ┌─────────┐  │
│   │ │    CU    │ │◄───────────────────────►│HDD/SSD  │  │
│   │ │(Điều khiển)│                          │ (Bộ nhớ │  │
│   │ └──────────┘ │                          │  phụ)   │  │
│   │ ┌──────────┐ │                          └─────────┘  │
│   │ │ Register │ │                                       │
│   │ └──────────┘ │      Bus hệ thống       ┌─────────┐  │
│   └──────────────┘◄───────────────────────►│  I/O    │  │
│                                             │(Vào/Ra) │  │
│                                             └─────────┘  │
└──────────────────────────────────────────────────────────┘
```

### 1.2 CPU (Central Processing Unit - Bộ xử lý trung tâm)

CPU là **"bộ não"** của máy tính, chịu trách nhiệm thực hiện mọi phép tính và điều khiển hoạt động.

**Các thành phần chính của CPU:**

| Thành phần | Chức năng | Ví dụ |
|---|---|---|
| **ALU** (Arithmetic Logic Unit) | Thực hiện các phép toán số học (+, -, ×, ÷) và logic (AND, OR, NOT) | `3 + 5 = 8`, `true AND false = false` |
| **CU** (Control Unit) | Điều khiển luồng hoạt động, giải mã lệnh, phối hợp các thành phần | Đọc lệnh từ RAM, gửi tín hiệu đến ALU |
| **Register** | Bộ nhớ cực nhanh bên trong CPU, lưu dữ liệu tạm thời | Thanh ghi `AX`, `BX`, `PC` (Program Counter) |
| **Cache** | Bộ nhớ đệm tốc độ cao, nằm giữa CPU và RAM | Cache L1 (nhanh nhất), L2, L3 |

**Chu trình hoạt động của CPU (Instruction Cycle):**

```
   ┌─────────┐     ┌─────────┐     ┌──────────┐     ┌─────────┐
   │  FETCH   │────►│ DECODE  │────►│ EXECUTE  │────►│  STORE  │
   │(Nạp lệnh)│     │(Giải mã)│     │(Thực thi)│     │(Lưu KQ) │
   └─────────┘     └─────────┘     └──────────┘     └────┬────┘
        ▲                                                  │
        └──────────────────────────────────────────────────┘
                        (Lặp lại)
```

1. **Fetch**: CPU lấy lệnh từ RAM dựa vào địa chỉ trong thanh ghi **Program Counter (PC)**.
2. **Decode**: CU giải mã lệnh để hiểu cần thực hiện phép toán gì.
3. **Execute**: ALU thực hiện phép toán hoặc CU thực hiện lệnh điều khiển.
4. **Store**: Kết quả được lưu vào Register hoặc ghi ngược lại RAM.

**Các thông số quan trọng của CPU:**

| Thông số | Ý nghĩa | Ví dụ |
|---|---|---|
| **Xung nhịp (Clock Speed)** | Số chu kỳ xử lý mỗi giây (GHz) | Intel i7: 3.6 GHz = 3.6 tỷ chu kỳ/giây |
| **Số nhân (Cores)** | Số đơn vị xử lý song song | Quad-core = 4 nhân |
| **Số luồng (Threads)** | Số luồng xử lý đồng thời | 8 cores / 16 threads (Hyper-threading) |
| **Kiến trúc** | Tập lệnh CPU hỗ trợ | x86 (32-bit), x86_64 (64-bit), ARM |

### 1.3 RAM (Random Access Memory - Bộ nhớ truy cập ngẫu nhiên)

RAM là **bộ nhớ chính** của máy tính, lưu trữ **tạm thời** dữ liệu và chương trình đang chạy.

**Đặc điểm chính:**

- ⚡ **Tốc độ rất nhanh**: Truy cập dữ liệu trong vài **nanosecond** (ns).
- 💨 **Volatile (bay hơi)**: Mất dữ liệu khi tắt nguồn.
- 🎯 **Random Access**: Truy cập bất kỳ ô nhớ nào với thời gian như nhau (O(1)).

**Các loại RAM phổ biến:**

| Loại | Đặc điểm | Tốc độ |
|---|---|---|
| **DDR4** | Phổ biến hiện tại | 2133 - 3200 MHz |
| **DDR5** | Thế hệ mới nhất | 4800 - 8400 MHz |
| **SRAM** | Dùng làm Cache CPU, đắt tiền | Cực nhanh (< 1ns) |
| **DRAM** | RAM thông thường, rẻ hơn | Nhanh (~10ns) |

**Cách RAM hoạt động:**

```
Khi bạn mở một chương trình (VD: Chrome):

1. HDD/SSD ──[tải chương trình]──► RAM
2. RAM ──[cung cấp lệnh & dữ liệu]──► CPU
3. CPU ──[xử lý và ghi kết quả]──► RAM
4. RAM ──[lưu trữ lâu dài nếu cần]──► HDD/SSD
```

### 1.4 HDD/SSD (Bộ nhớ thứ cấp - Storage)

Bộ nhớ thứ cấp lưu trữ dữ liệu **lâu dài**, không mất khi tắt nguồn.

#### HDD (Hard Disk Drive - Ổ cứng cơ)

```
Cấu tạo HDD:
      ┌─────────────────┐
      │   Đầu đọc/ghi   │ ◄── Đầu từ (read/write head)
      │       ↓          │
      │   ╭───────╮      │
      │   │ Track │      │ ◄── Các rãnh tròn đồng tâm
      │   │╭─────╮│      │
      │   ││Sector││     │ ◄── Đơn vị lưu trữ nhỏ nhất (512 bytes)
      │   │╰─────╯│      │
      │   ╰───────╯      │
      │  [Đĩa từ quay]   │ ◄── Quay 5400/7200 RPM
      └─────────────────┘
```

- **Nguyên lý**: Đĩa từ quay, đầu đọc/ghi di chuyển cơ học để đọc/ghi dữ liệu.
- **Ưu điểm**: Giá rẻ, dung lượng lớn (lên đến 20TB+).
- **Nhược điểm**: Chậm, dễ hỏng do va đập (có bộ phận cơ học).

#### SSD (Solid State Drive - Ổ cứng thể rắn)

- **Nguyên lý**: Sử dụng chip nhớ **NAND Flash** (bán dẫn), không có bộ phận chuyển động.
- **Ưu điểm**: Nhanh hơn HDD rất nhiều (5-100 lần), bền, ít tốn điện.
- **Nhược điểm**: Giá đắt hơn, số lần ghi có giới hạn (TBW - Terabytes Written).

### 1.5 I/O (Input/Output - Thiết bị vào/ra)

Các thiết bị cho phép máy tính tương tác với thế giới bên ngoài.

| Loại | Thiết bị | Chức năng |
|---|---|---|
| **Input** (Đầu vào) | Bàn phím, chuột, microphone, scanner, webcam | Nhận dữ liệu từ người dùng |
| **Output** (Đầu ra) | Màn hình, loa, máy in | Hiển thị/xuất kết quả |
| **Input + Output** | Màn hình cảm ứng, ổ USB, card mạng | Vừa nhận vừa xuất dữ liệu |

---

## 2. Sự khác nhau giữa RAM và SSD/HDD

### 2.1 Bảng so sánh chi tiết

| Tiêu chí | RAM | SSD | HDD |
|---|---|---|---|
| **Loại bộ nhớ** | Bộ nhớ chính (Primary) | Bộ nhớ thứ cấp (Secondary) | Bộ nhớ thứ cấp (Secondary) |
| **Tốc độ đọc** | ~50 GB/s (DDR5) | ~500 MB/s (SATA) / ~7 GB/s (NVMe) | ~100-200 MB/s |
| **Tốc độ ghi** | ~50 GB/s | ~500 MB/s (SATA) / ~5 GB/s (NVMe) | ~100-150 MB/s |
| **Lưu trữ khi tắt nguồn** | ❌ Mất dữ liệu (Volatile) | ✅ Giữ dữ liệu (Non-volatile) | ✅ Giữ dữ liệu (Non-volatile) |
| **Dung lượng phổ biến** | 8 - 64 GB | 256 GB - 4 TB | 500 GB - 20 TB |
| **Giá/GB (ước tính)** | ~3-5 $/GB | ~0.08-0.15 $/GB | ~0.02-0.04 $/GB |
| **Vai trò** | Lưu dữ liệu đang xử lý | Lưu trữ lâu dài | Lưu trữ lâu dài |
| **Độ bền cơ học** | Không có bộ phận cơ | Không có bộ phận cơ | Có đĩa quay, dễ hỏng |

### 2.2 Tại sao cần cả RAM lẫn HDD/SSD?

**Ví dụ thực tế - So sánh với bàn làm việc:**

```
📚 HDD/SSD = TỦ SÁCH (Kho lưu trữ)
   → Chứa rất nhiều sách (dữ liệu), nhưng phải đi lấy mỗi lần cần

📖 RAM = MẶT BÀN LÀM VIỆC (Không gian làm việc)
   → Chỉ để vài cuốn sách đang đọc, nhưng lấy sách trên bàn rất nhanh

🧠 CPU = BẠN (Người đọc sách)
   → Đọc và xử lý thông tin từ sách trên bàn

🔖 Cache = BOOKMARK (Đánh dấu trang)
   → Nhanh nhất, đánh dấu chính xác nơi đang đọc
```

**Hệ thống phân cấp bộ nhớ (Memory Hierarchy):**

```
    Nhanh nhất                                    Chậm nhất
    Đắt nhất                                      Rẻ nhất
    Nhỏ nhất                                      Lớn nhất

    ┌──────────┐
    │ Register │  ~ 1 ns    (vài KB)
    ├──────────┤
    │ Cache L1 │  ~ 1 ns    (32-64 KB)
    ├──────────┤
    │ Cache L2 │  ~ 4 ns    (256 KB - 1 MB)
    ├──────────┤
    │ Cache L3 │  ~ 10 ns   (4 - 64 MB)
    ├──────────┤
    │   RAM    │  ~ 50 ns   (8 - 64 GB)
    ├──────────┤
    │   SSD    │  ~ 100 μs  (256 GB - 4 TB)
    ├──────────┤
    │   HDD    │  ~ 10 ms   (1 - 20 TB)
    └──────────┘
```

> **Lưu ý**: 1 ms = 1,000 μs = 1,000,000 ns. HDD chậm hơn RAM khoảng **200,000 lần**!

### 2.3 Tại sao không dùng RAM để thay thế HDD/SSD?

1. **RAM mất dữ liệu khi tắt nguồn** → Không thể lưu trữ lâu dài.
2. **RAM đắt hơn SSD ~40-60 lần** → 64GB RAM giá ~$150-300, 64GB SSD chỉ ~$5-10.
3. **Dung lượng RAM giới hạn** → Mainboard thường hỗ trợ tối đa 64-128GB RAM.

---

## 3. Hệ điều hành, Firmware, Driver

### 3.1 Hệ điều hành (Operating System - OS)

**Hệ điều hành** là phần mềm hệ thống **trung gian** giữa phần cứng và người dùng/ứng dụng. Nó quản lý toàn bộ tài nguyên của máy tính.

```
┌──────────────────────────────────────────┐
│        ỨNG DỤNG (Applications)           │
│    Chrome, Word, IntelliJ, Game...       │
├──────────────────────────────────────────┤
│        HỆ ĐIỀU HÀNH (OS)                │
│   ┌──────────┬──────────┬──────────┐     │
│   │ Quản lý  │ Quản lý  │ Quản lý  │     │
│   │ Tiến trình│  Bộ nhớ  │  File    │     │
│   ├──────────┼──────────┼──────────┤     │
│   │ Quản lý  │ Bảo mật  │ Giao diện│     │
│   │ Thiết bị │          │ người dùng│    │
│   └──────────┴──────────┴──────────┘     │
├──────────────────────────────────────────┤
│       PHẦN CỨNG (Hardware)               │
│    CPU, RAM, HDD/SSD, GPU, NIC...        │
└──────────────────────────────────────────┘
```

**Các chức năng chính của OS:**

| Chức năng | Mô tả | Ví dụ |
|---|---|---|
| **Quản lý tiến trình** | Phân chia CPU cho các chương trình | Task Manager hiển thị CPU usage |
| **Quản lý bộ nhớ** | Cấp phát/thu hồi RAM cho các chương trình | Windows phân bổ 2GB RAM cho Chrome |
| **Quản lý file** | Tổ chức file/thư mục trên ổ đĩa | File Explorer, Terminal `ls` |
| **Quản lý thiết bị** | Giao tiếp với phần cứng qua driver | Nhận tín hiệu từ bàn phím, hiển thị lên màn hình |
| **Bảo mật** | Phân quyền truy cập, bảo vệ dữ liệu | User accounts, permissions, firewall |

**Các hệ điều hành phổ biến:**

| OS | Kernel | Sử dụng chính |
|---|---|---|
| **Windows** | Windows NT | Desktop, doanh nghiệp |
| **macOS** | XNU (Darwin) | Desktop Apple |
| **Linux** | Linux | Server, embedded, developer |
| **Android** | Linux (modified) | Smartphone |
| **iOS** | XNU (Darwin) | iPhone, iPad |

### 3.2 Firmware

**Firmware** là phần mềm **nhúng trực tiếp** vào phần cứng, được lưu trong bộ nhớ ROM/Flash. Nó là **phần mềm cấp thấp nhất**, chạy trước cả hệ điều hành.

```
Khi bạn bấm nút nguồn máy tính:

1. ⚡ BIOS/UEFI (Firmware) khởi động đầu tiên
   → Kiểm tra phần cứng (POST - Power-On Self-Test)
   → Tìm ổ đĩa chứa OS

2. 🔄 Bootloader tải OS từ ổ đĩa vào RAM
   → GRUB (Linux), Windows Boot Manager

3. 🖥️ Hệ điều hành khởi động
   → Tải drivers, services, giao diện người dùng
```

**Ví dụ Firmware phổ biến:**

| Firmware | Thiết bị | Chức năng |
|---|---|---|
| **BIOS/UEFI** | Bo mạch chủ | Khởi động máy tính, cấu hình phần cứng |
| **Firmware SSD** | Ổ cứng SSD | Quản lý đọc/ghi, cân bằng hao mòn chip nhớ |
| **Firmware Router** | Bộ định tuyến | Quản lý kết nối mạng, chuyển tiếp gói tin |
| **Firmware Printer** | Máy in | Điều khiển quá trình in ấn |

**So sánh Firmware vs OS:**

| Tiêu chí | Firmware | Hệ điều hành |
|---|---|---|
| **Vị trí lưu** | ROM/Flash trên phần cứng | HDD/SSD |
| **Thứ tự chạy** | Chạy đầu tiên khi bật nguồn | Chạy sau firmware |
| **Cập nhật** | Hiếm khi, cẩn thận | Thường xuyên |
| **Kích thước** | Vài KB - vài MB | Hàng GB |
| **Phức tạp** | Đơn giản, chuyên biệt | Rất phức tạp, đa năng |

### 3.3 Driver (Trình điều khiển)

**Driver** là phần mềm **cầu nối** giữa hệ điều hành và phần cứng cụ thể. Mỗi thiết bị phần cứng cần một driver tương ứng để OS có thể giao tiếp với nó.

```
┌──────────────┐      ┌──────────┐      ┌──────────────┐
│  Ứng dụng    │      │    OS    │      │  Phần cứng   │
│  (Muốn in    │─────►│  (Gọi   │─────►│  (Máy in     │
│   tài liệu)  │      │  Driver) │      │   Canon)     │
└──────────────┘      └──────────┘      └──────────────┘
                           │
                      ┌────▼─────┐
                      │  DRIVER  │
                      │ (Canon   │
                      │ Printer  │
                      │ Driver)  │
                      └──────────┘

Driver dịch lệnh chung của OS thành lệnh riêng mà phần cứng hiểu được.
```

**Tại sao cần Driver?**

- Mỗi hãng sản xuất phần cứng có cách giao tiếp riêng.
- OS không thể biết trước mọi loại phần cứng trên thế giới.
- Driver đóng vai trò **"phiên dịch viên"** giữa OS và phần cứng cụ thể.

**Ví dụ**: Khi bạn cắm card đồ họa NVIDIA vào máy:
- Không có driver → Màn hình hiển thị cơ bản, không chơi game được.
- Cài driver NVIDIA → Card đồ họa hoạt động đầy đủ, chơi game mượt mà.

---

## 4. Hệ thống quản lý file (Windows vs Linux)

### 4.1 Khái niệm File System

**File System** (Hệ thống tệp) là cách hệ điều hành **tổ chức, lưu trữ và truy xuất** dữ liệu trên ổ đĩa. Nó quy định:
- Cách đặt tên file
- Cách tổ chức file vào thư mục
- Cách lưu trữ vật lý trên ổ đĩa
- Cách quản lý quyền truy cập

### 4.2 So sánh Windows và Linux File System

| Tiêu chí | Windows | Linux |
|---|---|---|
| **Định dạng phổ biến** | NTFS, FAT32, exFAT | ext4, XFS, Btrfs |
| **Thư mục gốc** | `C:\`, `D:\` (mỗi ổ đĩa 1 chữ cái) | `/` (duy nhất một gốc) |
| **Dấu phân cách đường dẫn** | `\` (backslash) | `/` (forward slash) |
| **Phân biệt hoa/thường** | ❌ Không (`File.txt` = `file.txt`) | ✅ Có (`File.txt` ≠ `file.txt`) |
| **Ký tự đặc biệt trong tên file** | Cấm: `\ / : * ? " < > \|` | Cấm: `/` và null character |
| **Độ dài tên file tối đa** | 255 ký tự (path: 260) | 255 ký tự (path: 4096) |
| **Quyền truy cập** | ACL (Access Control List) | rwx (read/write/execute) cho owner/group/others |
| **Ẩn file** | Thuộc tính "Hidden" | Tên bắt đầu bằng dấu `.` |

### 4.3 Cấu trúc thư mục

**Windows:**

```
C:\                          ← Ổ đĩa hệ thống
├── Windows\                 ← Thư mục hệ điều hành
│   ├── System32\            ← File hệ thống (DLL, EXE)
│   └── Fonts\               ← Font chữ
├── Program Files\           ← Phần mềm 64-bit
├── Program Files (x86)\     ← Phần mềm 32-bit
├── Users\                   ← Thư mục người dùng
│   ├── ADMIN\
│   │   ├── Desktop\
│   │   ├── Documents\
│   │   ├── Downloads\
│   │   └── AppData\         ← Cấu hình ứng dụng (ẩn)
│   └── Public\
└── ProgramData\             ← Dữ liệu chung (ẩn)

D:\                          ← Ổ đĩa phụ (tùy chọn)
└── ...
```

**Linux:**

```
/                            ← Thư mục gốc (root)
├── bin/                     ← Lệnh cơ bản (ls, cp, mv...)
├── boot/                    ← File khởi động (kernel, GRUB)
├── dev/                     ← Thiết bị phần cứng (device files)
├── etc/                     ← File cấu hình hệ thống
├── home/                    ← Thư mục người dùng
│   └── dungpt/
│       ├── Desktop/
│       ├── Documents/
│       └── Downloads/
├── lib/                     ← Thư viện hệ thống
├── mnt/                     ← Điểm mount ổ đĩa tạm
├── opt/                     ← Phần mềm cài thêm
├── proc/                    ← Thông tin tiến trình (virtual)
├── root/                    ← Thư mục của user root
├── tmp/                     ← File tạm
├── usr/                     ← Chương trình & thư viện người dùng
│   ├── bin/
│   ├── lib/
│   └── share/
└── var/                     ← Dữ liệu thay đổi (log, cache)
```

### 4.4 Điểm khác biệt quan trọng

**1. Triết lý "Everything is a file" của Linux:**

Trong Linux, **mọi thứ đều được biểu diễn như file**, kể cả phần cứng:

```bash
# Ổ cứng đầu tiên
/dev/sda

# Phân vùng đầu tiên của ổ cứng
/dev/sda1

# Thông tin CPU
/proc/cpuinfo

# Bộ nhớ ngẫu nhiên
/dev/urandom
```

**2. Mount point trong Linux:**

Linux không dùng ký tự ổ đĩa (C:, D:), mà **mount** ổ đĩa vào một thư mục:

```bash
# USB được mount vào thư mục
/mnt/usb/

# Ổ đĩa phụ mount vào
/home/          (mount /dev/sda2 vào /home)
```

**3. Phân quyền file trong Linux:**

```bash
# Xem quyền file
$ ls -la myfile.txt
-rw-r--r-- 1 dungpt staff 1024 Jun 29 10:00 myfile.txt

# Giải thích:  -rw-r--r--
#              │├─┤├─┤├─┤
#              │ │   │  │
#              │ │   │  └── Others: r-- (chỉ đọc)
#              │ │   └── Group: r-- (chỉ đọc)
#              │ └── Owner: rw- (đọc + ghi)
#              └── Loại: - (file thường), d (thư mục)

# r = read (đọc)      = 4
# w = write (ghi)      = 2
# x = execute (chạy)   = 1

# chmod 755 myfile.txt
# 7 (rwx) cho owner, 5 (r-x) cho group, 5 (r-x) cho others
```

---

## 5. Tại sao file .exe không thể chạy trên Linux

### 5.1 Có 3 lý do chính

#### Lý do 1: Định dạng file thực thi khác nhau

Mỗi OS sử dụng **định dạng file thực thi (executable format)** riêng:

| Hệ điều hành | Định dạng | Phần mở rộng | Magic Number |
|---|---|---|---|
| **Windows** | PE (Portable Executable) | `.exe`, `.dll` | `MZ` (4D 5A) |
| **Linux** | ELF (Executable and Linkable Format) | Không bắt buộc | `\x7fELF` |
| **macOS** | Mach-O | Không bắt buộc | `0xFEEDFACE` |

Khi OS tải một file để chạy, nó kiểm tra **header** (phần đầu file):
- Windows kiểm tra thấy header `MZ` → OK, đây là file PE, chạy được.
- Linux kiểm tra thấy header `MZ` → **Không nhận ra**, từ chối chạy.

```
File .exe (PE format):
┌──────────────────────────────────────┐
│ MZ Header │ PE Header │ Sections ... │  ← Linux không hiểu format này
└──────────────────────────────────────┘

File ELF (Linux):
┌──────────────────────────────────────┐
│ \x7fELF   │ ELF Header │ Sections...│  ← Windows không hiểu format này
└──────────────────────────────────────┘
```

#### Lý do 2: System Call (lời gọi hệ thống) khác nhau

Chương trình khi cần thực hiện các thao tác hệ thống (đọc file, hiển thị lên màn hình, tạo tiến trình...) phải gọi **System Call** của OS. Mỗi OS có bộ System Call **hoàn toàn khác nhau**:

```
Chương trình muốn ghi file:

Windows System Call:           Linux System Call:
─────────────────              ──────────────────
CreateFile()                   open()
WriteFile()                    write()
CloseHandle()                  close()

→ File .exe được biên dịch với các lời gọi Windows.
→ Linux không có các hàm CreateFile(), WriteFile()...
→ Chương trình không thể chạy!
```

#### Lý do 3: Thư viện liên kết động khác nhau

Chương trình thường sử dụng **thư viện chia sẻ (shared libraries)** của OS:

| Windows | Linux |
|---|---|
| `.dll` (Dynamic Link Library) | `.so` (Shared Object) |
| `kernel32.dll`, `user32.dll` | `libc.so`, `libpthread.so` |
| Nằm trong `C:\Windows\System32\` | Nằm trong `/lib/`, `/usr/lib/` |

File `.exe` cần các file `.dll` của Windows → Linux không có → **Không chạy được**.

### 5.2 Giải pháp chạy chương trình Windows trên Linux

| Giải pháp | Cách hoạt động | Ví dụ |
|---|---|---|
| **Wine** | Giả lập lớp Windows API trên Linux | `wine program.exe` |
| **Máy ảo (VM)** | Chạy Windows trong máy ảo | VirtualBox, VMware |
| **WSL** | Windows Subsystem for Linux (ngược lại) | Chạy Linux trên Windows |
| **Cross-compile** | Biên dịch lại mã nguồn cho từng OS | GCC cho Linux, MSVC cho Windows |

---

## 6. Ngôn ngữ lập trình là gì

### 6.1 Định nghĩa

**Ngôn ngữ lập trình** là một ngôn ngữ hình thức (formal language) dùng để viết các **tập lệnh** (instructions) mà máy tính có thể hiểu và thực thi. Nó là cầu nối giữa **tư duy con người** và **mã máy (machine code)** mà CPU thực thi.

```
Con người                                         Máy tính (CPU)
   │                                                   │
   │  "Tính tổng 2 số"                                │
   │         │                                         │
   │         ▼                                         │
   │  ┌─────────────────┐                             │
   │  │ Ngôn ngữ lập    │     Biên dịch/              │
   │  │ trình (Java):   │     Thông dịch              │
   │  │                 │─────────────────►  01001011  │
   │  │ int sum = a + b;│                    10110100  │
   │  └─────────────────┘                    11010010  │
   │                                         (Mã máy)  │
```

### 6.2 Phân loại theo mức độ trừu tượng

```
Mức cao (Gần con người)          Mức thấp (Gần máy)
     ▲                                    ▲
     │                                    │
┌─────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
│ Python   │  │  Java    │  │    C     │  │ Assembly │  → Mã máy (0/1)
│ "print"  │  │ System.  │  │ printf() │  │ MOV AX,1 │
│          │  │ out.     │  │          │  │ INT 21h  │
│          │  │ println()│  │          │  │          │
└─────────┘  └──────────┘  └──────────┘  └──────────┘
  Rất dễ        Dễ đọc       Gần phần      Gần mã
  đọc/viết                    cứng          máy nhất
```

**Ví dụ cùng một thao tác "In ra Hello World":**

| Ngôn ngữ | Code | Mức độ |
|---|---|---|
| **Python** | `print("Hello World")` | Rất cao |
| **Java** | `System.out.println("Hello World");` | Cao |
| **C** | `printf("Hello World\n");` | Trung bình |
| **Assembly (x86)** | `mov ah, 09h` / `int 21h` | Rất thấp |
| **Mã máy** | `10110100 00001001 11001101 00100001` | Máy tính hiểu trực tiếp |

### 6.3 Phân loại theo paradigm (mô hình lập trình)

| Paradigm | Mô tả | Ngôn ngữ tiêu biểu |
|---|---|---|
| **Hướng đối tượng (OOP)** | Tổ chức code thành các đối tượng | Java, C#, C++ |
| **Hướng thủ tục** | Tổ chức code thành các hàm/thủ tục | C, Pascal |
| **Hàm (Functional)** | Code dựa trên hàm thuần túy, tránh trạng thái | Haskell, Scala |
| **Script** | Thực thi tuần tự, thường dùng cho automation | Python, JavaScript, Bash |
| **Đa mô hình** | Kết hợp nhiều paradigm | Python, Kotlin, Scala |

---

## 7. Trình biên dịch và thông dịch

### 7.1 Trình biên dịch (Compiler)

**Compiler** dịch **toàn bộ** mã nguồn thành mã máy **một lần**, tạo ra file thực thi. Sau đó chạy file thực thi trực tiếp mà không cần mã nguồn nữa.

```
     Mã nguồn                 Compiler               File thực thi
  ┌─────────────┐         ┌──────────────┐         ┌──────────────┐
  │ program.c   │────────►│   GCC/Clang  │────────►│ program.exe  │
  │             │  Biên   │              │  Tạo ra │              │
  │ int main() {│  dịch   │  Kiểm tra    │  file   │  01001011    │
  │   printf(   │  toàn   │  cú pháp,    │  thực   │  10110100    │
  │   "Hello"); │  bộ     │  tối ưu hóa, │  thi    │  11010010    │
  │   return 0; │  ----►  │  dịch sang   │  ----►  │  ...         │
  │ }           │         │  mã máy      │         │              │
  └─────────────┘         └──────────────┘         └──────────────┘
                                                         │
                                                         ▼
                                                   Chạy trực tiếp
                                                   (không cần mã nguồn)
```

**Đặc điểm của Compiler:**

| Ưu điểm | Nhược điểm |
|---|---|
| ✅ Chạy **rất nhanh** (mã máy trực tiếp) | ❌ Phải chờ biên dịch toàn bộ trước khi chạy |
| ✅ Phát hiện lỗi trước khi chạy (compile-time) | ❌ File thực thi phụ thuộc vào OS & CPU |
| ✅ Mã nguồn được bảo mật (chỉ phát hành .exe) | ❌ Khó debug hơn |
| ✅ Tối ưu hóa tốt hơn | ❌ Sửa code → phải biên dịch lại toàn bộ |

**Ngôn ngữ sử dụng Compiler:** C, C++, Go, Rust, Swift

### 7.2 Trình thông dịch (Interpreter)

**Interpreter** đọc và thực thi mã nguồn **từng dòng một**, không tạo file thực thi riêng.

```
     Mã nguồn              Interpreter
  ┌─────────────┐       ┌──────────────┐
  │ script.py   │       │   Python     │
  │             │       │ Interpreter  │
  │ Line 1 ─────────►  │ Đọc dòng 1  │──► Thực thi ngay
  │ Line 2 ─────────►  │ Đọc dòng 2  │──► Thực thi ngay
  │ Line 3 ─────────►  │ Đọc dòng 3  │──► Thực thi ngay
  │ ...         │       │ ...          │
  └─────────────┘       └──────────────┘

  → Mỗi lần chạy đều cần mã nguồn + interpreter
```

**Đặc điểm của Interpreter:**

| Ưu điểm | Nhược điểm |
|---|---|
| ✅ Chạy ngay, không cần chờ biên dịch | ❌ **Chậm hơn** compiler (dịch từng dòng) |
| ✅ Dễ debug (dừng ngay tại dòng lỗi) | ❌ Phát hiện lỗi khi **đang chạy** (runtime) |
| ✅ Chạy được trên nhiều nền tảng (chỉ cần interpreter) | ❌ Phải phát hành mã nguồn |
| ✅ Sửa code → chạy lại ngay | ❌ Tốn tài nguyên hơn (interpreter luôn chạy cùng) |

**Ngôn ngữ sử dụng Interpreter:** Python, JavaScript, Ruby, PHP

### 7.3 Hybrid (Biên dịch + Thông dịch) - Java

Java sử dụng cách **kết hợp cả hai**: biên dịch thành **bytecode** rồi thông dịch/JIT compile trên **JVM**.

```
  Mã nguồn         Compiler (javac)        Bytecode          JVM
┌──────────┐      ┌──────────────┐      ┌──────────┐    ┌──────────┐
│Hello.java│─────►│  javac       │─────►│Hello     │───►│   JVM    │
│          │      │  (biên dịch) │      │.class    │    │(thông dịch│
│          │      └──────────────┘      │          │    │ + JIT)   │
│public    │                            │Bytecode: │    │          │
│class     │                            │CA FE     │    │Chạy trên │
│Hello {   │                            │BA BE     │    │mọi OS có │
│ ...      │                            │...       │    │JVM       │
│}         │                            └──────────┘    └──────────┘
└──────────┘
```

### 7.4 Bảng so sánh tổng hợp

| Tiêu chí | Compiler | Interpreter | Hybrid (Java) |
|---|---|---|---|
| **Quá trình** | Dịch toàn bộ → chạy | Dịch từng dòng & chạy | Dịch → bytecode → JVM chạy |
| **Tốc độ chạy** | ⚡ Nhanh nhất | 🐢 Chậm nhất | 🏃 Nhanh (nhờ JIT) |
| **Tốc độ phát triển** | Chậm (chờ compile) | Nhanh (chạy ngay) | Trung bình |
| **Đa nền tảng** | ❌ Phải compile lại | ✅ (cần interpreter) | ✅ (cần JVM) |
| **Phát hiện lỗi** | Compile-time | Runtime | Compile-time + Runtime |
| **Output** | File thực thi (.exe) | Không tạo file | Bytecode (.class) |
| **Ví dụ** | C, C++, Go, Rust | Python, JS, Ruby | Java, Kotlin, Scala |

---

## 8. Tại sao file Java có thể chạy ở nhiều môi trường khác nhau

### 8.1 Nguyên lý "Write Once, Run Anywhere" (WORA)

Java được thiết kế với triết lý **"Viết một lần, chạy mọi nơi"**. Bí mật nằm ở **JVM (Java Virtual Machine)**.

```
                    WRITE ONCE
                        │
                  ┌─────▼─────┐
                  │ Hello.java│  ← Mã nguồn Java
                  └─────┬─────┘
                        │  javac (biên dịch)
                  ┌─────▼─────┐
                  │Hello.class│  ← Bytecode (trung gian)
                  └─────┬─────┘
                        │
          ┌─────────────┼─────────────┐
          │             │             │
    RUN ANYWHERE   RUN ANYWHERE  RUN ANYWHERE
          │             │             │
   ┌──────▼──────┐ ┌───▼────┐ ┌──────▼──────┐
   │  JVM for    │ │ JVM for│ │  JVM for    │
   │  Windows    │ │ Linux  │ │  macOS      │
   │             │ │        │ │             │
   │ Dịch byte-  │ │ Dịch   │ │ Dịch byte-  │
   │ code → mã   │ │ byte-  │ │ code → mã   │
   │ máy Windows │ │ code → │ │ máy macOS   │
   └──────┬──────┘ │ mã máy │ └──────┬──────┘
          │        │ Linux  │        │
          ▼        └───┬────┘        ▼
   Windows OS         │        macOS
                       ▼
                   Linux OS
```

### 8.2 JVM (Java Virtual Machine) - Máy ảo Java

JVM là **máy ảo** đóng vai trò **trung gian** giữa bytecode Java và hệ điều hành thực. Mỗi OS có một **phiên bản JVM riêng**, nhưng tất cả đều hiểu cùng một bytecode.

**Cách JVM hoạt động:**

```
┌─────────────────────────────────────────────────────────────┐
│                          JVM                                │
│                                                             │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐  │
│  │ Class Loader │───►│ Bytecode     │───►│ Execution    │  │
│  │              │    │ Verifier     │    │ Engine       │  │
│  │ Tải file     │    │              │    │              │  │
│  │ .class vào   │    │ Kiểm tra     │    │ ┌──────────┐ │  │
│  │ bộ nhớ       │    │ bytecode     │    │ │Interpreter│ │  │
│  │              │    │ hợp lệ       │    │ └──────────┘ │  │
│  └──────────────┘    └──────────────┘    │ ┌──────────┐ │  │
│                                          │ │JIT       │ │  │
│                                          │ │Compiler  │ │  │
│  ┌──────────────────────────────────┐    │ └──────────┘ │  │
│  │        Runtime Data Areas        │    └──────────────┘  │
│  │  ┌──────┐ ┌─────┐ ┌──────────┐  │                      │
│  │  │ Heap │ │Stack│ │Method    │  │                      │
│  │  │      │ │     │ │Area      │  │                      │
│  │  └──────┘ └─────┘ └──────────┘  │                      │
│  └──────────────────────────────────┘                      │
└─────────────────────────────────────────────────────────────┘
```

### 8.3 Bytecode là gì?

**Bytecode** là tập lệnh **trung gian** - không phải mã nguồn, cũng không phải mã máy. Nó được thiết kế để JVM có thể hiểu và thực thi.

**Ví dụ: Biên dịch code Java thành Bytecode**

```java
// Hello.java
public class Hello {
    public static void main(String[] args) {
        int a = 5;
        int b = 10;
        int sum = a + b;
        System.out.println(sum);
    }
}
```

**Sau khi biên dịch (`javac Hello.java`), bytecode trong Hello.class:**

```
// Xem bằng lệnh: javap -c Hello.class
public static void main(java.lang.String[]);
  Code:
     0: iconst_5          // Đẩy hằng số 5 vào stack
     1: istore_1           // Lưu vào biến cục bộ 1 (a = 5)
     2: bipush 10          // Đẩy hằng số 10 vào stack
     4: istore_2           // Lưu vào biến cục bộ 2 (b = 10)
     5: iload_1            // Tải biến 1 (a) lên stack
     6: iload_2            // Tải biến 2 (b) lên stack
     7: iadd               // Cộng 2 giá trị trên stack
     8: istore_3           // Lưu kết quả vào biến 3 (sum)
     9: getstatic #2       // Lấy System.out
    12: iload_3            // Tải sum lên stack
    13: invokevirtual #3   // Gọi println()
    16: return             // Kết thúc
```

### 8.4 JIT Compiler (Just-In-Time Compiler)

JVM ban đầu **thông dịch** bytecode (chậm). Nhưng nó có **JIT Compiler** để tối ưu:

```
Lần 1-1000: Thông dịch (chậm)
     │
     ▼ JVM phát hiện: "Đoạn code này được gọi rất nhiều lần!"
                       (Hot spot detection)
     │
     ▼ JIT biên dịch đoạn đó thành mã máy native
     │
Lần 1001+: Chạy mã máy native (NHANH!)
```

**JIT làm cho Java gần bằng tốc độ C/C++ trong nhiều trường hợp.**

### 8.5 So sánh: Tại sao C/C++ không chạy đa nền tảng như Java?

```
C/C++:
  main.c ──[GCC Windows]──► main.exe     (chỉ chạy trên Windows)
  main.c ──[GCC Linux]────► main (ELF)   (chỉ chạy trên Linux)
  main.c ──[Clang macOS]──► main (Mach-O)(chỉ chạy trên macOS)

  → Phải biên dịch lại cho MỖI nền tảng!

Java:
  Hello.java ──[javac]──► Hello.class (Bytecode)
                               │
                     ┌─────────┼─────────┐
                     ▼         ▼         ▼
                JVM Windows JVM Linux JVM macOS
                     │         │         │
                     ▼         ▼         ▼
                 Chạy được  Chạy được  Chạy được

  → Biên dịch MỘT LẦN, chạy MỌI NƠI có JVM!
```

### 8.6 Các ngôn ngữ khác cũng chạy trên JVM

Nhờ JVM, nhiều ngôn ngữ khác cũng có thể biên dịch thành bytecode và chạy đa nền tảng:

| Ngôn ngữ | Biên dịch thành | Chạy trên |
|---|---|---|
| **Java** | `.class` (bytecode) | JVM |
| **Kotlin** | `.class` (bytecode) | JVM |
| **Scala** | `.class` (bytecode) | JVM |
| **Groovy** | `.class` (bytecode) | JVM |
| **Clojure** | `.class` (bytecode) | JVM |

### 8.7 Tóm tắt

```
┌─────────────────────────────────────────────────────┐
│          TẠI SAO JAVA CHẠY ĐA NỀN TẢNG?            │
│                                                     │
│  1. Java biên dịch thành BYTECODE (không phải mã    │
│     máy), nên bytecode KHÔNG phụ thuộc vào OS/CPU   │
│                                                     │
│  2. JVM đóng vai trò "phiên dịch viên" - dịch       │
│     bytecode thành mã máy phù hợp với từng OS       │
│                                                     │
│  3. Mỗi OS có JVM riêng, nhưng tất cả đều hiểu     │
│     cùng một bytecode                               │
│                                                     │
│  4. JIT Compiler giúp Java chạy nhanh gần bằng      │
│     ngôn ngữ biên dịch native (C/C++)               │
│                                                     │
│  → "Write Once, Run Anywhere"                       │
└─────────────────────────────────────────────────────┘
```

---

> **📌 Kết thúc Phần 1: Cấu Trúc Máy Tính Căn Bản**

---

# Phần 2: Lập Trình Cơ Bản (Java)

## 📌 Mục lục

1. [Khai báo biến](#1-khai-báo-biến)
2. [Kiểu dữ liệu](#2-kiểu-dữ-liệu)
3. [Giá trị thập phân của int, long](#3-giá-trị-thập-phân-của-int-long)
4. [Sự khác nhau giữa double và float](#4-sự-khác-nhau-giữa-double-và-float)
5. [Cộng 100 lần số 0.2f và kiểm tra kết quả](#5-cộng-100-lần-số-02f-và-kiểm-tra-kết-quả)
6. [Lệnh rẽ nhánh (if, switch)](#6-lệnh-rẽ-nhánh-if-switch)
7. [Lệnh lặp (for, while, do-while, foreach)](#7-lệnh-lặp-for-while-do-while-foreach)
8. [Chuyển đổi hệ thập phân, nhị phân, hexa](#8-chuyển-đổi-hệ-thập-phân-nhị-phân-hexa)
9. [Toán tử dịch bit, AND/OR bit, so sánh & và &&](#9-toán-tử-dịch-bit-andor-bit-so-sánh--và-)
10. [Viết và sử dụng hàm, đệ quy, khử đệ quy](#10-viết-và-sử-dụng-hàm-đệ-quy-khử-đệ-quy)
11. [Các ký tự chuỗi đặc biệt](#11-các-ký-tự-chuỗi-đặc-biệt)
12. [Cách xử lý dữ liệu tiền tệ bằng số nguyên](#12-cách-xử-lý-dữ-liệu-tiền-tệ-bằng-số-nguyên)
13. [Lập trình với mảng](#13-lập-trình-với-mảng)

---

## 1. Khai báo biến

### 1.1 Biến là gì?

**Biến (Variable)** là một **vùng nhớ được đặt tên** dùng để lưu trữ dữ liệu trong chương trình. Giá trị của biến có thể thay đổi trong quá trình chạy.

```
Bộ nhớ RAM:
┌─────────────┬─────────────┬─────────────┬─────────────┐
│ Địa chỉ:   │ Địa chỉ:   │ Địa chỉ:   │ Địa chỉ:   │
│ 0x001       │ 0x002       │ 0x003       │ 0x004       │
│             │             │             │             │
│ Tên: age    │ Tên: name   │ Tên: score  │   (trống)   │
│ Giá trị: 22 │ Giá trị:    │ Giá trị:    │             │
│ Kiểu: int   │ "Dung"      │ 9.5         │             │
│ (4 bytes)   │ Kiểu:String │ Kiểu:double │             │
│             │             │ (8 bytes)   │             │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

### 1.2 Cú pháp khai báo biến trong Java

```java
// Cú pháp: <kiểu_dữ_liệu> <tên_biến>;
// Hoặc:    <kiểu_dữ_liệu> <tên_biến> = <giá_trị>;

public class VariableDemo {
    public static void main(String[] args) {
        // --- 1. Khai báo rồi gán giá trị sau ---
        int age;            // Khai báo biến kiểu int
        age = 22;           // Gán giá trị

        // --- 2. Khai báo và gán giá trị cùng lúc ---
        String name = "Dung";
        double score = 9.5;
        boolean isStudent = true;
        char grade = 'A';

        // --- 3. Khai báo nhiều biến cùng kiểu ---
        int x = 1, y = 2, z = 3;

        // --- 4. Hằng số (constant) - không thể thay đổi giá trị ---
        final double PI = 3.14159265358979;
        // PI = 3.14; // ❌ LỖI! Không thể gán lại giá trị cho biến final

        // --- In ra giá trị ---
        System.out.println("Tên: " + name);       // Tên: Dung
        System.out.println("Tuổi: " + age);        // Tuổi: 22
        System.out.println("Điểm: " + score);      // Điểm: 9.5
        System.out.println("Sinh viên: " + isStudent); // Sinh viên: true
        System.out.println("Xếp loại: " + grade);  // Xếp loại: A
        System.out.println("PI = " + PI);           // PI = 3.14159265358979
    }
}
```

### 1.3 Quy tắc đặt tên biến

| Quy tắc | Đúng ✅ | Sai ❌ | Lý do |
|---|---|---|---|
| Bắt đầu bằng chữ cái, `_`, hoặc `$` | `age`, `_count`, `$price` | `1name`, `@value` | Không bắt đầu bằng số hoặc ký tự đặc biệt khác |
| Không dùng từ khóa Java | `myClass`, `score` | `class`, `int`, `static` | Đây là từ khóa dành riêng |
| Phân biệt hoa/thường | `name` ≠ `Name` ≠ `NAME` | | Java case-sensitive |
| Quy ước **camelCase** | `studentName`, `totalScore` | `student_name`, `StudentName` | Convention Java cho biến và hàm |
| Tên có ý nghĩa | `studentAge`, `maxRetry` | `a`, `x1`, `temp123` | Dễ đọc, dễ hiểu |

### 1.4 Phạm vi biến (Variable Scope)

```java
public class ScopeDemo {
    // Biến instance (thuộc tính của đối tượng)
    int instanceVar = 10;       // Tồn tại khi đối tượng tồn tại

    // Biến static (biến lớp)
    static int classVar = 20;   // Tồn tại khi class được load

    public void myMethod() {
        // Biến cục bộ (local variable)
        int localVar = 30;      // Chỉ tồn tại trong method này

        if (true) {
            // Biến block
            int blockVar = 40;  // Chỉ tồn tại trong khối if này
        }
        // System.out.println(blockVar); // ❌ LỖI! blockVar không tồn tại ở đây
    }
}
```

```
Phạm vi biến:
┌────────────────────────────────── Class ──────────────────────────────┐
│  classVar (static) - sống khi class được load                        │
│  instanceVar - sống khi đối tượng tồn tại                           │
│  ┌──────────────────── Method ────────────────────┐                  │
│  │  localVar - sống trong method                  │                  │
│  │  ┌──────────── Block (if/for) ───────────┐     │                  │
│  │  │  blockVar - sống trong block           │     │                  │
│  │  └───────────────────────────────────────┘     │                  │
│  └────────────────────────────────────────────────┘                  │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 2. Kiểu dữ liệu

### 2.1 Tổng quan kiểu dữ liệu trong Java

Java có **2 nhóm kiểu dữ liệu**:

```
Kiểu dữ liệu Java
├── Kiểu nguyên thủy (Primitive) - 8 kiểu
│   ├── Số nguyên: byte, short, int, long
│   ├── Số thực: float, double
│   ├── Ký tự: char
│   └── Logic: boolean
│
└── Kiểu tham chiếu (Reference)
    ├── String
    ├── Array
    ├── Class / Object
    └── Interface
```

### 2.2 Bảng chi tiết 8 kiểu nguyên thủy

| Kiểu | Kích thước | Giá trị min | Giá trị max | Giá trị mặc định | Ví dụ |
|---|---|---|---|---|---|
| `byte` | 1 byte (8 bit) | -128 | 127 | 0 | `byte b = 100;` |
| `short` | 2 bytes (16 bit) | -32,768 | 32,767 | 0 | `short s = 30000;` |
| `int` | 4 bytes (32 bit) | -2,147,483,648 | 2,147,483,647 | 0 | `int i = 100000;` |
| `long` | 8 bytes (64 bit) | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807 | 0L | `long l = 100000L;` |
| `float` | 4 bytes (32 bit) | ~1.4E-45 | ~3.4E+38 | 0.0f | `float f = 3.14f;` |
| `double` | 8 bytes (64 bit) | ~4.9E-324 | ~1.8E+308 | 0.0d | `double d = 3.14;` |
| `char` | 2 bytes (16 bit) | '\u0000' (0) | '\uffff' (65,535) | '\u0000' | `char c = 'A';` |
| `boolean` | ~1 bit* | false | true | false | `boolean b = true;` |

> \* JVM thường dùng 1 byte cho boolean trong thực tế.

### 2.3 Code ví dụ

```java
public class DataTypeDemo {
    public static void main(String[] args) {
        // ===== SỐ NGUYÊN =====
        byte  myByte  = 127;          // -128 đến 127
        short myShort = 32000;        // -32,768 đến 32,767
        int   myInt   = 2_000_000_000; // Dùng _ để dễ đọc (Java 7+)
        long  myLong  = 9_000_000_000L; // Phải có hậu tố 'L'

        // ===== SỐ THỰC =====
        float  myFloat  = 3.14f;      // Phải có hậu tố 'f'
        double myDouble = 3.141592653589793; // Mặc định là double

        // ===== KÝ TỰ =====
        char myChar   = 'A';          // Một ký tự Unicode
        char charNum  = 65;           // Cũng là 'A' (mã ASCII)
        char charUni  = '\u0041';     // Cũng là 'A' (Unicode)

        // ===== LOGIC =====
        boolean isJavaFun = true;
        boolean isFishTasty = false;

        // ===== KIỂU THAM CHIẾU =====
        String greeting = "Xin chào!"; // Chuỗi ký tự

        // In ra thông tin
        System.out.println("byte:    " + myByte);      // 127
        System.out.println("short:   " + myShort);      // 32000
        System.out.println("int:     " + myInt);         // 2000000000
        System.out.println("long:    " + myLong);        // 9000000000
        System.out.println("float:   " + myFloat);       // 3.14
        System.out.println("double:  " + myDouble);      // 3.141592653589793
        System.out.println("char:    " + myChar);         // A
        System.out.println("boolean: " + isJavaFun);      // true
        System.out.println("String:  " + greeting);       // Xin chào!

        // Kích thước của từng kiểu
        System.out.println("\n--- Kích thước (bytes) ---");
        System.out.println("byte:    " + Byte.BYTES);     // 1
        System.out.println("short:   " + Short.BYTES);    // 2
        System.out.println("int:     " + Integer.BYTES);  // 4
        System.out.println("long:    " + Long.BYTES);     // 8
        System.out.println("float:   " + Float.BYTES);    // 4
        System.out.println("double:  " + Double.BYTES);   // 8
        System.out.println("char:    " + Character.BYTES);// 2
    }
}
```

### 2.4 Kiểu nguyên thủy vs Kiểu tham chiếu

```
Kiểu nguyên thủy (Primitive):          Kiểu tham chiếu (Reference):
┌──────────────┐                       ┌──────────────┐
│  Stack       │                       │  Stack       │     Heap
│              │                       │              │    ┌─────────────┐
│  int a = 5;  │                       │  ref ────────┼───►│ Object      │
│  ┌────┐      │                       │  ┌────┐      │    │ "Xin chào!" │
│  │ 5  │      │                       │  │0x3F│      │    └─────────────┘
│  └────┘      │                       │  └────┘      │
│              │                       │              │
│ Giá trị lưu  │                       │ Địa chỉ lưu  │
│ TRỰC TIẾP    │                       │ trên Stack,   │
│ trên Stack   │                       │ Object trên   │
│              │                       │ Heap          │
└──────────────┘                       └──────────────┘

→ Primitive: so sánh bằng ==  (so sánh giá trị)
→ Reference: so sánh bằng .equals()  (so sánh nội dung)
             == chỉ so sánh địa chỉ tham chiếu!
```

---

## 3. Giá trị thập phân của int, long

### 3.1 Cách tính giá trị min/max

Máy tính dùng **hệ nhị phân** (0 và 1). Mỗi bit có thể lưu 0 hoặc 1.

**Công thức cho số có dấu (signed):**
- **n bit** → biểu diễn từ **-2^(n-1)** đến **2^(n-1) - 1**
- Bit đầu tiên (MSB) dùng làm **bit dấu**: 0 = dương, 1 = âm

### 3.2 Kiểu int (32 bit)

```
int (32 bit - 4 bytes):

Bit dấu (1 bit)    Giá trị (31 bit)
    ↓               ↓
┌───┬───────────────────────────────────────────────────────┐
│ 0 │ 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 │
└───┴───────────────────────────────────────────────────────┘

Giá trị MAX = 2^31 - 1 = 2,147,483,647          (~2.1 tỷ)
Giá trị MIN = -2^31   = -2,147,483,648          (~-2.1 tỷ)

Nhớ nhanh: int ≈ ±2.1 tỷ
```

### 3.3 Kiểu long (64 bit)

```
long (64 bit - 8 bytes):

Giá trị MAX = 2^63 - 1 = 9,223,372,036,854,775,807    (~9.2 x 10^18)
Giá trị MIN = -2^63   = -9,223,372,036,854,775,808

Nhớ nhanh: long ≈ ±9.2 quintillion (tỷ tỷ)
```

### 3.4 Code kiểm chứng

```java
public class IntLongRange {
    public static void main(String[] args) {
        // ===== INT =====
        System.out.println("===== INT (32 bit) =====");
        System.out.println("MIN: " + Integer.MIN_VALUE);  // -2147483648
        System.out.println("MAX: " + Integer.MAX_VALUE);  //  2147483647
        System.out.println("Tính tay: 2^31 = " + (long) Math.pow(2, 31)); // 2147483648

        // Tràn số (overflow) - rất nguy hiểm!
        int maxInt = Integer.MAX_VALUE;
        System.out.println("\nmax + 1 = " + (maxInt + 1));
        // Kết quả: -2147483648 (tràn sang số âm nhỏ nhất!)

        // ===== LONG =====
        System.out.println("\n===== LONG (64 bit) =====");
        System.out.println("MIN: " + Long.MIN_VALUE);  // -9223372036854775808
        System.out.println("MAX: " + Long.MAX_VALUE);  //  9223372036854775807

        // Tràn số long
        long maxLong = Long.MAX_VALUE;
        System.out.println("\nmax + 1 = " + (maxLong + 1));
        // Kết quả: -9223372036854775808

        // ===== TỔNG HỢP =====
        System.out.println("\n===== TỔNG HỢP TẤT CẢ SỐ NGUYÊN =====");
        System.out.println("byte:  " + Byte.MIN_VALUE + " đến " + Byte.MAX_VALUE);
        System.out.println("short: " + Short.MIN_VALUE + " đến " + Short.MAX_VALUE);
        System.out.println("int:   " + Integer.MIN_VALUE + " đến " + Integer.MAX_VALUE);
        System.out.println("long:  " + Long.MIN_VALUE + " đến " + Long.MAX_VALUE);
    }
}
```

**Output:**
```
===== INT (32 bit) =====
MIN: -2147483648
MAX: 2147483647
Tính tay: 2^31 = 2147483648

max + 1 = -2147483648

===== LONG (64 bit) =====
MIN: -9223372036854775808
MAX: 9223372036854775807

max + 1 = -9223372036854775808

===== TỔNG HỢP TẤT CẢ SỐ NGUYÊN =====
byte:  -128 đến 127
short: -32768 đến 32767
int:   -2147483648 đến 2147483647
long:  -9223372036854775808 đến 9223372036854775807
```

### 3.5 Hiện tượng tràn số (Integer Overflow)

```
Hình dung int như đồng hồ quay vòng:

          0
         /|\
        / | \
   MAX /  |  \ MIN
      ↗   |   ↘
  ... 2   |  -2 ...
      1   |  -1
       \  |  /
        \ | /
         \|/
    MAX+1 = MIN  (quay vòng!)

int: 2,147,483,647 + 1 = -2,147,483,648
     (MAX_VALUE)          (MIN_VALUE)
```

```java
// Ví dụ thực tế - Lỗi tràn số nguy hiểm
int population = 2_100_000_000;  // 2.1 tỷ dân
int growth = 100_000_000;         // tăng 100 triệu
int newPop = population + growth;  // Kết quả: -2,094,967,296 (SAI!)

// ✅ Giải pháp: Dùng long
long safePop = (long) population + growth; // 2,200,000,000 (ĐÚNG)
```

---

## 4. Sự khác nhau giữa double và float

### 4.1 Bảng so sánh

| Tiêu chí | `float` | `double` |
|---|---|---|
| **Kích thước** | 4 bytes (32 bit) | 8 bytes (64 bit) |
| **Độ chính xác** | ~6-7 chữ số thập phân | ~15-16 chữ số thập phân |
| **Giá trị max** | ~3.4 × 10^38 | ~1.8 × 10^308 |
| **Hậu tố khai báo** | Bắt buộc `f` hoặc `F` | Mặc định (không cần) |
| **Tiêu chuẩn** | IEEE 754 single precision | IEEE 754 double precision |
| **Dùng khi** | Tiết kiệm bộ nhớ, đồ họa game | Mặc định cho phép tính thập phân |

### 4.2 Cấu trúc lưu trữ theo IEEE 754

```
float (32 bit):
┌────┬──────────┬───────────────────────┐
│Sign│ Exponent │       Mantissa        │
│1bit│  8 bit   │       23 bit          │
└────┴──────────┴───────────────────────┘
Độ chính xác: ~7 chữ số thập phân

double (64 bit):
┌────┬─────────────┬────────────────────────────────────────────────────┐
│Sign│  Exponent   │                    Mantissa                       │
│1bit│   11 bit    │                    52 bit                         │
└────┴─────────────┴────────────────────────────────────────────────────┘
Độ chính xác: ~15-16 chữ số thập phân
```

### 4.3 Code so sánh

```java
public class FloatVsDouble {
    public static void main(String[] args) {
        // ===== ĐỘ CHÍNH XÁC =====
        float  fPI = 3.141592653589793f;  // Bắt buộc có hậu tố 'f'
        double dPI = 3.141592653589793;   // Mặc định là double

        System.out.println("PI thực tế: 3.141592653589793...");
        System.out.println("float  PI = " + fPI);   // 3.1415927 (chỉ 7 chữ số)
        System.out.println("double PI = " + dPI);    // 3.141592653589793 (15 chữ số)
        //                                              ↑ float mất chính xác ở đây!

        // ===== SAI SỐ TÍCH LŨY =====
        float  fSum = 0.0f;
        double dSum = 0.0;

        for (int i = 0; i < 1000; i++) {
            fSum += 0.1f;
            dSum += 0.1;
        }

        System.out.println("\nCộng 0.1 x 1000 lần:");
        System.out.println("float  = " + fSum);   // 99.99905 (sai lệch!)
        System.out.println("double = " + dSum);    // 99.9999999999986 (chính xác hơn)
        System.out.println("Kỳ vọng = 100.0");

        // ===== KHI NÀO DÙNG FLOAT? =====
        // Khi cần tiết kiệm bộ nhớ (xử lý hàng triệu giá trị)
        float[] pixels = new float[1920 * 1080]; // 8 MB (float)
        // double[] pixels = new double[1920 * 1080]; // 16 MB (double) - gấp đôi!

        // ===== KHI NÀO DÙNG DOUBLE? =====
        // Hầu hết trường hợp, dùng double (chính xác hơn, là mặc định)
        double bankBalance = 1_000_000.50;
        double interestRate = 0.0325;
    }
}
```

---

## 5. Cộng 100 lần số 0.2f và kiểm tra kết quả

### 5.1 Thí nghiệm

```java
public class FloatPrecision {
    public static void main(String[] args) {
        // ===== THÍ NGHIỆM: Cộng 0.2f x 100 lần =====
        float sum = 0.0f;
        for (int i = 0; i < 100; i++) {
            sum += 0.2f;
        }

        System.out.println("Cộng 0.2f x 100 lần:");
        System.out.println("Kết quả:  " + sum);       // 20.000004
        System.out.println("Kỳ vọng:  20.0");
        System.out.println("Bằng 20? " + (sum == 20.0f)); // false !!!

        // So sánh với double
        double sumD = 0.0;
        for (int i = 0; i < 100; i++) {
            sumD += 0.2;
        }
        System.out.println("\nCộng 0.2 (double) x 100 lần:");
        System.out.println("Kết quả:  " + sumD);      // 19.999999999999996
        System.out.println("Bằng 20? " + (sumD == 20.0)); // false !!!
    }
}
```

**Output:**
```
Cộng 0.2f x 100 lần:
Kết quả:  20.000004
Kỳ vọng:  20.0
Bằng 20? false

Cộng 0.2 (double) x 100 lần:
Kết quả:  19.999999999999996
Bằng 20? false
```

### 5.2 Lý giải: Tại sao kết quả không phải 20.0?

**Nguyên nhân gốc:** Số 0.2 trong hệ thập phân **KHÔNG THỂ** biểu diễn chính xác trong hệ nhị phân.

```
Chuyển 0.2 (thập phân) sang nhị phân:

0.2 × 2 = 0.4 → 0
0.4 × 2 = 0.8 → 0
0.8 × 2 = 1.6 → 1
0.6 × 2 = 1.2 → 1
0.2 × 2 = 0.4 → 0  ← Lặp lại!
0.4 × 2 = 0.8 → 0
0.8 × 2 = 1.6 → 1
...

0.2₁₀ = 0.001100110011001100110011... (lặp vô hạn!)
                                       ↑
                              Giống như 1/3 = 0.333... trong thập phân
```

```
Vì float chỉ có 23 bit mantissa, nó phải CẮT BỎ:

Giá trị thực: 0.00110011001100110011001100110011... (vô hạn)
float lưu:    0.00110011001100110011001 (cắt tại 23 bit)
                                       ↑
                              Sai số nhỏ ở đây!

Sai số mỗi lần cộng: ~0.000000004 (rất nhỏ)
Nhưng cộng 100 lần:  ~0.000004 (tích lũy thành đáng kể!)

→ Kết quả: 20.000004 thay vì 20.0
```

### 5.3 Cách so sánh số thực đúng cách

```java
public class FloatComparison {
    public static void main(String[] args) {
        float sum = 0.0f;
        for (int i = 0; i < 100; i++) {
            sum += 0.2f;
        }

        // ❌ SAI: So sánh trực tiếp
        if (sum == 20.0f) {
            System.out.println("Bằng 20");
        } else {
            System.out.println("Không bằng 20"); // ← Kết quả này!
        }

        // ✅ ĐÚNG: So sánh với epsilon (sai số cho phép)
        float EPSILON = 0.0001f;
        if (Math.abs(sum - 20.0f) < EPSILON) {
            System.out.println("Gần bằng 20 (trong sai số cho phép)"); // ← Kết quả này!
        }

        // ✅ ĐÚNG: Dùng BigDecimal cho tính toán chính xác
        java.math.BigDecimal bdSum = java.math.BigDecimal.ZERO;
        java.math.BigDecimal bdVal = new java.math.BigDecimal("0.2");
        for (int i = 0; i < 100; i++) {
            bdSum = bdSum.add(bdVal);
        }
        System.out.println("BigDecimal: " + bdSum);                    // 20.0
        System.out.println("Bằng 20? " + bdSum.compareTo(
            new java.math.BigDecimal("20")) == 0 ? "true" : "false");  // true
    }
}
```

### 5.4 Bảng tóm tắt vấn đề số thực

| Vấn đề | Giải pháp |
|---|---|
| So sánh `==` không chính xác | Dùng `Math.abs(a - b) < EPSILON` |
| Tính toán tài chính | Dùng `BigDecimal` hoặc số nguyên (cent) |
| Tích lũy sai số trong vòng lặp | Dùng `BigDecimal` hoặc thuật toán Kahan |
| Cần lưu số thập phân chính xác | Dùng `BigDecimal` |

---

## 6. Lệnh rẽ nhánh (if, switch)

### 6.1 Lệnh if - else

```java
public class IfElseDemo {
    public static void main(String[] args) {
        int score = 75;

        // --- 1. if đơn giản ---
        if (score >= 50) {
            System.out.println("Đậu!");
        }

        // --- 2. if - else ---
        if (score >= 50) {
            System.out.println("Đậu!");
        } else {
            System.out.println("Rớt!");
        }

        // --- 3. if - else if - else (nhiều nhánh) ---
        if (score >= 90) {
            System.out.println("Xuất sắc (A)");
        } else if (score >= 80) {
            System.out.println("Giỏi (B)");
        } else if (score >= 70) {
            System.out.println("Khá (C)");        // ← In ra dòng này
        } else if (score >= 60) {
            System.out.println("Trung bình (D)");
        } else {
            System.out.println("Yếu (F)");
        }

        // --- 4. Toán tử 3 ngôi (ternary) ---
        String result = (score >= 50) ? "Đậu" : "Rớt";
        System.out.println(result); // Đậu

        // --- 5. if lồng nhau ---
        boolean isRegistered = true;
        if (isRegistered) {
            if (score >= 50) {
                System.out.println("Đã đăng ký và đậu!");
            } else {
                System.out.println("Đã đăng ký nhưng rớt!");
            }
        }
    }
}
```

### 6.2 Lệnh switch

```java
public class SwitchDemo {
    public static void main(String[] args) {
        // --- 1. switch truyền thống ---
        int dayOfWeek = 3;
        switch (dayOfWeek) {
            case 1:
                System.out.println("Chủ nhật");
                break;                             // ← PHẢI có break!
            case 2:
                System.out.println("Thứ hai");
                break;
            case 3:
                System.out.println("Thứ ba");      // ← In ra
                break;
            case 4:
                System.out.println("Thứ tư");
                break;
            case 5:
                System.out.println("Thứ năm");
                break;
            case 6:
                System.out.println("Thứ sáu");
                break;
            case 7:
                System.out.println("Thứ bảy");
                break;
            default:
                System.out.println("Ngày không hợp lệ");
        }

        // --- 2. switch gộp case (fall-through có chủ đích) ---
        switch (dayOfWeek) {
            case 2: case 3: case 4: case 5: case 6:
                System.out.println("Ngày làm việc");  // ← In ra
                break;
            case 7: case 1:
                System.out.println("Cuối tuần");
                break;
        }

        // --- 3. switch với String (Java 7+) ---
        String month = "January";
        switch (month.toLowerCase()) {
            case "january": case "february": case "march":
                System.out.println("Quý 1");
                break;
            case "april": case "may": case "june":
                System.out.println("Quý 2");
                break;
            case "july": case "august": case "september":
                System.out.println("Quý 3");
                break;
            case "october": case "november": case "december":
                System.out.println("Quý 4");
                break;
        }

        // --- 4. Switch expression (Java 14+) ---
        String dayName = switch (dayOfWeek) {
            case 1  -> "Chủ nhật";
            case 2  -> "Thứ hai";
            case 3  -> "Thứ ba";
            case 4  -> "Thứ tư";
            case 5  -> "Thứ năm";
            case 6  -> "Thứ sáu";
            case 7  -> "Thứ bảy";
            default -> "Không hợp lệ";
        };
        System.out.println(dayName); // Thứ ba
    }
}
```

### 6.3 So sánh if vs switch

| Tiêu chí | if - else | switch |
|---|---|---|
| **Kiểm tra** | Bất kỳ biểu thức boolean nào | Giá trị cụ thể (bằng) |
| **Kiểu dữ liệu** | Mọi kiểu | `byte`, `short`, `int`, `char`, `String`, `enum` |
| **Điều kiện phức tạp** | ✅ `if (x > 5 && x < 10)` | ❌ Không hỗ trợ phạm vi |
| **Nhiều giá trị cụ thể** | Dài dòng | ✅ Gọn gàng hơn |
| **Hiệu năng** | Kiểm tra tuần tự | Có thể dùng jump table (nhanh hơn) |

---

## 7. Lệnh lặp (for, while, do-while, foreach)

### 7.1 Vòng lặp for

```java
public class ForLoopDemo {
    public static void main(String[] args) {
        // --- 1. for cơ bản ---
        // for (khởi tạo; điều_kiện; cập_nhật)
        System.out.println("=== Đếm từ 1 đến 5 ===");
        for (int i = 1; i <= 5; i++) {
            System.out.print(i + " ");  // 1 2 3 4 5
        }
        System.out.println();

        // --- 2. for đếm ngược ---
        System.out.println("=== Đếm ngược từ 5 ===");
        for (int i = 5; i >= 1; i--) {
            System.out.print(i + " ");  // 5 4 3 2 1
        }
        System.out.println();

        // --- 3. for bước nhảy ---
        System.out.println("=== Số chẵn từ 0-10 ===");
        for (int i = 0; i <= 10; i += 2) {
            System.out.print(i + " ");  // 0 2 4 6 8 10
        }
        System.out.println();

        // --- 4. for lồng nhau (bảng cửu chương) ---
        System.out.println("=== Bảng cửu chương 2-3 ===");
        for (int i = 2; i <= 3; i++) {
            for (int j = 1; j <= 9; j++) {
                System.out.printf("%d x %d = %2d%n", i, j, i * j);
            }
            System.out.println("---");
        }

        // --- 5. break và continue ---
        System.out.println("=== break: dừng khi gặp 5 ===");
        for (int i = 1; i <= 10; i++) {
            if (i == 5) break;          // Thoát vòng lặp
            System.out.print(i + " ");  // 1 2 3 4
        }
        System.out.println();

        System.out.println("=== continue: bỏ qua số 5 ===");
        for (int i = 1; i <= 10; i++) {
            if (i == 5) continue;       // Bỏ qua lần lặp này
            System.out.print(i + " ");  // 1 2 3 4 6 7 8 9 10
        }
        System.out.println();
    }
}
```

### 7.2 Vòng lặp while

```java
public class WhileLoopDemo {
    public static void main(String[] args) {
        // --- 1. while cơ bản ---
        // Kiểm tra điều kiện TRƯỚC khi thực thi
        System.out.println("=== while: Đếm từ 1 đến 5 ===");
        int i = 1;
        while (i <= 5) {
            System.out.print(i + " ");  // 1 2 3 4 5
            i++;
        }
        System.out.println();

        // --- 2. while với điều kiện phức tạp ---
        System.out.println("=== Chia liên tục cho 2 ===");
        int number = 100;
        while (number > 1) {
            System.out.print(number + " → ");
            number /= 2;
        }
        System.out.println(number);  // 100 → 50 → 25 → 12 → 6 → 3 → 1

        // --- 3. while vô hạn (cần break để thoát) ---
        int count = 0;
        while (true) {
            count++;
            if (count > 3) break;
            System.out.println("Lần lặp: " + count);
        }
    }
}
```

### 7.3 Vòng lặp do-while

```java
public class DoWhileDemo {
    public static void main(String[] args) {
        // do-while: Thực thi ÍT NHẤT 1 LẦN, rồi mới kiểm tra điều kiện
        
        // --- 1. do-while cơ bản ---
        int i = 1;
        do {
            System.out.print(i + " ");  // 1 2 3 4 5
            i++;
        } while (i <= 5);
        System.out.println();

        // --- 2. Khác biệt: while vs do-while khi điều kiện SAI ngay từ đầu ---
        System.out.println("=== while (điều kiện sai từ đầu) ===");
        int x = 10;
        while (x < 5) {
            System.out.println("while: " + x);  // KHÔNG in gì cả!
            x++;
        }

        System.out.println("=== do-while (điều kiện sai từ đầu) ===");
        int y = 10;
        do {
            System.out.println("do-while: " + y);  // In ra 1 lần: "do-while: 10"
            y++;
        } while (y < 5);

        // --- 3. Ứng dụng: Menu chương trình ---
        // int choice;
        // do {
        //     System.out.println("1. Thêm");
        //     System.out.println("2. Xóa");
        //     System.out.println("3. Thoát");
        //     choice = scanner.nextInt();
        //     // xử lý...
        // } while (choice != 3);  // Lặp đến khi chọn Thoát
    }
}
```

### 7.4 Vòng lặp for-each (Enhanced for)

```java
public class ForEachDemo {
    public static void main(String[] args) {
        // for-each: Duyệt qua TOÀN BỘ phần tử trong mảng/collection
        // Cú pháp: for (kiểu phần_tử : tập_hợp) { ... }

        // --- 1. Duyệt mảng ---
        int[] numbers = {10, 20, 30, 40, 50};
        System.out.println("=== for-each với mảng int ===");
        for (int num : numbers) {
            System.out.print(num + " ");  // 10 20 30 40 50
        }
        System.out.println();

        // --- 2. Duyệt mảng String ---
        String[] fruits = {"Táo", "Cam", "Xoài", "Nho"};
        System.out.println("=== for-each với mảng String ===");
        for (String fruit : fruits) {
            System.out.println("- " + fruit);
        }

        // --- 3. So sánh for truyền thống vs for-each ---
        System.out.println("=== for truyền thống (có index) ===");
        for (int i = 0; i < fruits.length; i++) {
            System.out.println(i + ": " + fruits[i]);
        }

        System.out.println("=== for-each (không có index) ===");
        for (String fruit : fruits) {
            System.out.println("  " + fruit);  // Không biết index
        }

        // --- 4. for-each với mảng 2 chiều ---
        int[][] matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        System.out.println("=== Ma trận ===");
        for (int[] row : matrix) {
            for (int val : row) {
                System.out.printf("%3d", val);
            }
            System.out.println();
        }
    }
}
```

### 7.5 So sánh các vòng lặp

| Tiêu chí | `for` | `while` | `do-while` | `for-each` |
|---|---|---|---|---|
| **Biết trước số lần lặp** | ✅ Tốt nhất | Được | Được | ✅ Duyệt hết |
| **Không biết số lần lặp** | Được | ✅ Tốt nhất | ✅ Tốt | ❌ |
| **Chạy ít nhất 1 lần** | ❌ | ❌ | ✅ | Phụ thuộc mảng |
| **Cần index** | ✅ | ✅ | ✅ | ❌ Không có index |
| **Duyệt collection** | Được | Được | Được | ✅ Tốt nhất |
| **Sửa phần tử trong vòng lặp** | ✅ | ✅ | ✅ | ❌ Không nên |

---

## 8. Chuyển đổi hệ thập phân, nhị phân, hexa

### 8.1 Tổng quan 3 hệ số

| Hệ | Cơ số | Ký tự sử dụng | Tiền tố Java | Ví dụ |
|---|---|---|---|---|
| **Thập phân** (Decimal) | 10 | 0-9 | (không có) | `42` |
| **Nhị phân** (Binary) | 2 | 0, 1 | `0b` | `0b101010` |
| **Bát phân** (Octal) | 8 | 0-7 | `0` | `052` |
| **Thập lục phân** (Hex) | 16 | 0-9, A-F | `0x` | `0x2A` |

### 8.2 Cách chuyển đổi thủ công

```
===== THẬP PHÂN → NHỊ PHÂN (Chia liên tục cho 2, lấy dư ngược) =====

42 ÷ 2 = 21 dư 0  ↑
21 ÷ 2 = 10 dư 1  │
10 ÷ 2 = 5  dư 0  │  Đọc ngược
 5 ÷ 2 = 2  dư 1  │  từ dưới lên
 2 ÷ 2 = 1  dư 0  │
 1 ÷ 2 = 0  dư 1  │

→ 42₁₀ = 101010₂

===== NHỊ PHÂN → THẬP PHÂN (Nhân từng bit với 2^vị_trí) =====

101010₂ = 1×2⁵ + 0×2⁴ + 1×2³ + 0×2² + 1×2¹ + 0×2⁰
         = 32   + 0    + 8    + 0    + 2    + 0
         = 42₁₀

===== THẬP PHÂN → HEXA (Chia liên tục cho 16, lấy dư ngược) =====

255 ÷ 16 = 15 dư 15 (F)  ↑
 15 ÷ 16 = 0  dư 15 (F)  │ Đọc ngược

→ 255₁₀ = FF₁₆

===== NHỊ PHÂN → HEXA (Nhóm 4 bit từ phải sang trái) =====

101010₂ = 0010 1010
           ↓    ↓
           2    A

→ 101010₂ = 2A₁₆

Bảng chuyển đổi nhanh:
Hex | Bin  | Dec    Hex | Bin  | Dec
 0  | 0000 | 0       8  | 1000 | 8
 1  | 0001 | 1       9  | 1001 | 9
 2  | 0010 | 2       A  | 1010 | 10
 3  | 0011 | 3       B  | 1011 | 11
 4  | 0100 | 4       C  | 1100 | 12
 5  | 0101 | 5       D  | 1101 | 13
 6  | 0110 | 6       E  | 1110 | 14
 7  | 0111 | 7       F  | 1111 | 15
```

### 8.3 Code Java chuyển đổi

```java
public class NumberSystemDemo {
    public static void main(String[] args) {
        int decimal = 42;

        // ===== THẬP PHÂN → CÁC HỆ KHÁC =====
        System.out.println("===== Chuyển đổi từ thập phân: " + decimal + " =====");
        System.out.println("Nhị phân:     " + Integer.toBinaryString(decimal));  // 101010
        System.out.println("Bát phân:     " + Integer.toOctalString(decimal));   // 52
        System.out.println("Thập lục phân: " + Integer.toHexString(decimal));     // 2a

        // ===== CÁC HỆ KHÁC → THẬP PHÂN =====
        int fromBinary = Integer.parseInt("101010", 2);    // Từ nhị phân
        int fromOctal  = Integer.parseInt("52", 8);         // Từ bát phân
        int fromHex    = Integer.parseInt("2A", 16);        // Từ hexa

        System.out.println("\n===== Chuyển về thập phân =====");
        System.out.println("101010 (bin) = " + fromBinary);  // 42
        System.out.println("52 (oct)     = " + fromOctal);   // 42
        System.out.println("2A (hex)     = " + fromHex);     // 42

        // ===== KHAI BÁO TRỰC TIẾP BẰNG LITERAL =====
        int binLiteral = 0b101010;  // Nhị phân (tiền tố 0b)
        int octLiteral = 052;       // Bát phân (tiền tố 0)
        int hexLiteral = 0x2A;      // Hexa (tiền tố 0x)

        System.out.println("\n===== Literal trong Java =====");
        System.out.println("0b101010 = " + binLiteral);  // 42
        System.out.println("052      = " + octLiteral);   // 42
        System.out.println("0x2A     = " + hexLiteral);   // 42

        // ===== CHUYỂN ĐỔI THỦ CÔNG: Thập phân → Nhị phân =====
        System.out.println("\n===== Chuyển thủ công: " + decimal + " → nhị phân =====");
        decimalToBinary(decimal);

        // ===== CHUYỂN ĐỔI THỦ CÔNG: Nhị phân → Thập phân =====
        System.out.println("\n===== Chuyển thủ công: 101010 → thập phân =====");
        binaryToDecimal("101010");

        // ===== FORMAT ĐẸP =====
        System.out.printf("\n===== Format =====\n");
        System.out.printf("Decimal: %d%n", decimal);          // 42
        System.out.printf("Octal:   %o%n", decimal);          // 52
        System.out.printf("Hex:     %x (hoặc %X)%n", decimal, decimal); // 2a (hoặc 2A)
        // Không có format nhị phân trong printf, dùng toBinaryString
    }

    static void decimalToBinary(int n) {
        StringBuilder result = new StringBuilder();
        int original = n;
        System.out.println("Quá trình chia:");
        while (n > 0) {
            int remainder = n % 2;
            result.insert(0, remainder);
            System.out.printf("  %d ÷ 2 = %d dư %d%n", n, n / 2, remainder);
            n /= 2;
        }
        System.out.println("→ " + original + "₁₀ = " + result + "₂");
    }

    static void binaryToDecimal(String binary) {
        int result = 0;
        int length = binary.length();
        System.out.println("Quá trình tính:");
        for (int i = 0; i < length; i++) {
            int bit = binary.charAt(i) - '0';
            int power = length - 1 - i;
            int value = bit * (int) Math.pow(2, power);
            if (bit == 1) {
                System.out.printf("  %d × 2^%d = %d%n", bit, power, value);
            }
            result += value;
        }
        System.out.println("→ " + binary + "₂ = " + result + "₁₀");
    }
}
```

---

## 9. Toán tử dịch bit, AND/OR bit, so sánh & và &&

### 9.1 Các toán tử bitwise (thao tác trên bit)

```
Bảng tóm tắt toán tử bitwise:

Toán tử    Tên               Ví dụ         Kết quả
───────    ────               ─────         ───────
   &       AND bit            5 & 3         1
   |       OR bit             5 | 3         7
   ^       XOR bit            5 ^ 3         6
   ~       NOT bit (đảo)      ~5            -6
   <<      Dịch trái          5 << 1        10
   >>      Dịch phải (có dấu) 20 >> 2       5
   >>>     Dịch phải (không dấu) -1 >>> 28  15
```

### 9.2 AND, OR, XOR, NOT bit

```java
public class BitwiseDemo {
    public static void main(String[] args) {
        int a = 5;  // Nhị phân: 0101
        int b = 3;  // Nhị phân: 0011

        // ===== AND bit (&) - Cả hai bit đều 1 → 1 =====
        System.out.println("=== AND (&) ===");
        System.out.println("  0101 (5)");
        System.out.println("& 0011 (3)");
        System.out.println("------");
        System.out.println("  0001 (1)");
        System.out.println("5 & 3 = " + (a & b));  // 1

        // ===== OR bit (|) - Ít nhất một bit là 1 → 1 =====
        System.out.println("\n=== OR (|) ===");
        System.out.println("  0101 (5)");
        System.out.println("| 0011 (3)");
        System.out.println("------");
        System.out.println("  0111 (7)");
        System.out.println("5 | 3 = " + (a | b));  // 7

        // ===== XOR bit (^) - Hai bit khác nhau → 1 =====
        System.out.println("\n=== XOR (^) ===");
        System.out.println("  0101 (5)");
        System.out.println("^ 0011 (3)");
        System.out.println("------");
        System.out.println("  0110 (6)");
        System.out.println("5 ^ 3 = " + (a ^ b));  // 6

        // ===== NOT bit (~) - Đảo tất cả bit =====
        System.out.println("\n=== NOT (~) ===");
        System.out.println("~5 = " + (~a));  // -6
        // 5  = 00000000 00000000 00000000 00000101
        // ~5 = 11111111 11111111 11111111 11111010 = -6 (bù 2)

        // ===== Bảng chân lý =====
        System.out.println("\n=== Bảng chân lý ===");
        System.out.println("A | B | A&B | A|B | A^B | ~A");
        System.out.println("0 | 0 |  0  |  0  |  0  |  1");
        System.out.println("0 | 1 |  0  |  1  |  1  |  1");
        System.out.println("1 | 0 |  0  |  1  |  1  |  0");
        System.out.println("1 | 1 |  1  |  1  |  0  |  0");
    }
}
```

### 9.3 Dịch bit (Shift operators)

```java
public class ShiftDemo {
    public static void main(String[] args) {
        // ===== DỊCH TRÁI << (Nhân với 2^n) =====
        int x = 5; // 00000101

        System.out.println("=== Dịch trái << ===");
        System.out.println("5 << 1 = " + (x << 1));  // 10  (00001010) = 5 × 2¹
        System.out.println("5 << 2 = " + (x << 2));  // 20  (00010100) = 5 × 2²
        System.out.println("5 << 3 = " + (x << 3));  // 40  (00101000) = 5 × 2³

        // Minh họa:
        // 00000101 (5)
        // 0000101_ (dịch trái 1, thêm 0 vào phải) → 00001010 (10)
        // 000101__ (dịch trái 2, thêm 00)          → 00010100 (20)

        // ===== DỊCH PHẢI >> (Chia cho 2^n, giữ dấu) =====
        int y = 20; // 00010100

        System.out.println("\n=== Dịch phải >> ===");
        System.out.println("20 >> 1 = " + (y >> 1));  // 10  (00001010) = 20 ÷ 2¹
        System.out.println("20 >> 2 = " + (y >> 2));  // 5   (00000101) = 20 ÷ 2²
        System.out.println("20 >> 3 = " + (y >> 3));  // 2   (00000010) = 20 ÷ 2³

        // Với số âm: >> giữ bit dấu
        int neg = -8;
        System.out.println("\n-8 >> 1 = " + (neg >> 1));   // -4 (giữ dấu âm)
        System.out.println("-8 >>> 1 = " + (neg >>> 1));   // 2147483644 (không giữ dấu)

        // ===== ỨNG DỤNG THỰC TẾ =====
        System.out.println("\n=== Ứng dụng ===");

        // 1. Nhân/chia nhanh cho lũy thừa 2 (nhanh hơn * và /)
        int multiply8 = 7 << 3;  // 7 × 8 = 56
        int divide4   = 100 >> 2; // 100 ÷ 4 = 25
        System.out.println("7 × 8 (bằng <<) = " + multiply8);
        System.out.println("100 ÷ 4 (bằng >>) = " + divide4);

        // 2. Kiểm tra bit thứ n
        int num = 42; // 101010
        int n = 3;    // Kiểm tra bit thứ 3 (tính từ 0)
        boolean bitSet = ((num >> n) & 1) == 1;
        System.out.println("Bit thứ " + n + " của " + num + " = " + (bitSet ? "1" : "0"));
        // bit thứ 3 của 101010 → dịch phải 3 → 000101, AND 1 → 1

        // 3. Set bit thứ n
        int setResult = num | (1 << 2);  // Set bit thứ 2 (101010 → 101110)
        System.out.println("Set bit 2 của " + num + " = " + setResult); // 46

        // 4. Hoán đổi 2 số không dùng biến tạm (XOR trick)
        int p = 10, q = 20;
        System.out.println("\nTrước: p=" + p + ", q=" + q);
        p = p ^ q;  // p = 10 ^ 20
        q = p ^ q;  // q = (10 ^ 20) ^ 20 = 10
        p = p ^ q;  // p = (10 ^ 20) ^ 10 = 20
        System.out.println("Sau:   p=" + p + ", q=" + q); // p=20, q=10
    }
}
```

### 9.4 So sánh `&` và `&&`, `|` và `||`

```java
public class AndComparison {
    public static void main(String[] args) {
        // ===== && (Short-circuit AND) vs & (Non-short-circuit AND) =====
        // && : Nếu vế trái FALSE → KHÔNG kiểm tra vế phải (tối ưu)
        // &  : LUÔN kiểm tra CẢ HAI vế

        int x = 0;

        // --- Ví dụ 1: && (short-circuit) ---
        System.out.println("=== && (short-circuit) ===");
        if (x != 0 && (10 / x > 2)) {
            // x != 0 là FALSE → KHÔNG tính 10/x → KHÔNG bị lỗi chia cho 0
            System.out.println("OK");
        } else {
            System.out.println("x = 0, bỏ qua phép chia"); // ← In ra
        }

        // --- Ví dụ 2: & (non-short-circuit) ---
        System.out.println("\n=== & (non-short-circuit) ===");
        // if (x != 0 & (10 / x > 2)) {
        //     // x != 0 là FALSE nhưng VẪN tính 10/x
        //     // → ArithmeticException: / by zero !!!
        // }
        System.out.println("Nếu dùng &, sẽ bị ArithmeticException!");

        // --- Ví dụ 3: Null check an toàn với && ---
        String str = null;
        if (str != null && str.length() > 0) {
            // str != null là FALSE → KHÔNG gọi str.length()
            // → KHÔNG bị NullPointerException
            System.out.println("Chuỗi: " + str);
        } else {
            System.out.println("Chuỗi null hoặc rỗng"); // ← In ra
        }

        // --- Minh họa side-effect ---
        System.out.println("\n=== Side-effect demo ===");
        int a = 5, b = 5;

        boolean result1 = (a > 10) && (++b > 5);
        System.out.println("&&: b = " + b);  // b = 5 (++b KHÔNG chạy)

        boolean result2 = (a > 10) & (++b > 5);
        System.out.println("& : b = " + b);  // b = 6 (++b CHẠY dù vế trái false)
    }
}
```

**Bảng so sánh:**

| Tiêu chí | `&` / `\|` (Bitwise) | `&&` / `\|\|` (Logic short-circuit) |
|---|---|---|
| **Kiểu toán hạng** | `int`, `long`, `byte`... VÀ `boolean` | Chỉ `boolean` |
| **Đánh giá** | LUÔN tính cả 2 vế | Dừng sớm nếu đã biết kết quả |
| **Khi nào dùng** | Thao tác bit, cần side-effect | Hầu hết trường hợp logic |
| **An toàn** | Có thể gây lỗi (chia cho 0, null) | An toàn hơn nhờ short-circuit |

---

## 10. Viết và sử dụng hàm, đệ quy, khử đệ quy

### 10.1 Viết và sử dụng hàm (Method)

```java
public class MethodDemo {
    // ===== CÚ PHÁP HÀM =====
    // <access_modifier> <static?> <kiểu_trả_về> <tên_hàm>(<tham_số>) {
    //     // thân hàm
    //     return giá_trị; // nếu kiểu trả về khác void
    // }

    // --- 1. Hàm không trả về giá trị (void) ---
    public static void sayHello(String name) {
        System.out.println("Xin chào, " + name + "!");
    }

    // --- 2. Hàm có trả về giá trị ---
    public static int add(int a, int b) {
        return a + b;
    }

    // --- 3. Hàm có nhiều tham số ---
    public static double calculateBMI(double weight, double height) {
        return weight / (height * height);
    }

    // --- 4. Hàm với varargs (số lượng tham số không cố định) ---
    public static int sum(int... numbers) {
        int total = 0;
        for (int num : numbers) {
            total += num;
        }
        return total;
    }

    // --- 5. Hàm trả về mảng ---
    public static int[] getMinMax(int[] arr) {
        int min = arr[0], max = arr[0];
        for (int val : arr) {
            if (val < min) min = val;
            if (val > max) max = val;
        }
        return new int[]{min, max};
    }

    public static void main(String[] args) {
        // Gọi hàm
        sayHello("Dũng");                         // Xin chào, Dũng!
        int result = add(3, 5);
        System.out.println("3 + 5 = " + result);  // 3 + 5 = 8

        double bmi = calculateBMI(70, 1.75);
        System.out.printf("BMI = %.1f%n", bmi);   // BMI = 22.9

        System.out.println("Sum = " + sum(1, 2, 3, 4, 5)); // Sum = 15

        int[] arr = {3, 1, 7, 2, 9, 4};
        int[] minMax = getMinMax(arr);
        System.out.println("Min = " + minMax[0] + ", Max = " + minMax[1]); // Min=1, Max=9
    }
}
```

### 10.2 Đệ quy (Recursion)

**Đệ quy** là kỹ thuật trong đó một hàm **gọi lại chính nó** để giải quyết bài toán con nhỏ hơn.

```java
public class RecursionDemo {
    // ===== 1. TÍNH GIAI THỪA (n!) =====
    // 5! = 5 × 4 × 3 × 2 × 1 = 120
    // n! = n × (n-1)!
    // 0! = 1 (base case)
    public static long factorial(int n) {
        // Base case (điều kiện dừng)
        if (n <= 1) return 1;
        // Recursive case (gọi đệ quy)
        return n * factorial(n - 1);
    }

    // ===== 2. DÃY FIBONACCI =====
    // 0, 1, 1, 2, 3, 5, 8, 13, 21, 34...
    // F(n) = F(n-1) + F(n-2)
    // F(0) = 0, F(1) = 1
    public static int fibonacci(int n) {
        if (n <= 0) return 0;  // Base case
        if (n == 1) return 1;  // Base case
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    // ===== 3. TÌM KIẾM NHỊ PHÂN (Binary Search) =====
    public static int binarySearch(int[] arr, int target, int left, int right) {
        if (left > right) return -1;  // Base case: không tìm thấy

        int mid = left + (right - left) / 2;

        if (arr[mid] == target) return mid;       // Tìm thấy
        else if (arr[mid] < target)
            return binarySearch(arr, target, mid + 1, right); // Tìm bên phải
        else
            return binarySearch(arr, target, left, mid - 1);  // Tìm bên trái
    }

    public static void main(String[] args) {
        // Giai thừa
        System.out.println("5! = " + factorial(5));   // 120
        System.out.println("10! = " + factorial(10)); // 3628800

        // Fibonacci
        System.out.print("Fibonacci: ");
        for (int i = 0; i <= 10; i++) {
            System.out.print(fibonacci(i) + " ");
        }
        System.out.println(); // 0 1 1 2 3 5 8 13 21 34 55

        // Binary Search
        int[] sorted = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
        int index = binarySearch(sorted, 23, 0, sorted.length - 1);
        System.out.println("Tìm 23 tại index: " + index); // 5
    }
}
```

**Minh họa stack đệ quy (Giai thừa 5):**

```
factorial(5)
│ return 5 * factorial(4)
│   │ return 4 * factorial(3)
│   │   │ return 3 * factorial(2)
│   │   │   │ return 2 * factorial(1)
│   │   │   │   │ return 1  ← Base case (dừng)
│   │   │   │ return 2 * 1 = 2
│   │   │ return 3 * 2 = 6
│   │ return 4 * 6 = 24
│ return 5 * 24 = 120

Call Stack:
┌─────────────────┐
│ factorial(1) = 1│ ← Top (gọi cuối, trả về đầu)
├─────────────────┤
│ factorial(2)    │
├─────────────────┤
│ factorial(3)    │
├─────────────────┤
│ factorial(4)    │
├─────────────────┤
│ factorial(5)    │ ← Bottom (gọi đầu, trả về cuối)
└─────────────────┘
```

### 10.3 Khử đệ quy (Converting Recursion to Iteration)

**Khử đệ quy** là kỹ thuật thay thế đệ quy bằng vòng lặp + stack thủ công, giúp:
- Tránh **stack overflow** khi đệ quy quá sâu
- Thường **nhanh hơn** (không tốn chi phí gọi hàm)
- Tiết kiệm bộ nhớ stack

```java
import java.util.Stack;

public class DeRecursionDemo {
    // ===== GIAI THỪA =====

    // Đệ quy:
    public static long factorialRecursive(int n) {
        if (n <= 1) return 1;
        return n * factorialRecursive(n - 1);
    }

    // Khử đệ quy (dùng vòng lặp):
    public static long factorialIterative(int n) {
        long result = 1;
        for (int i = 2; i <= n; i++) {
            result *= i;
        }
        return result;
    }

    // ===== FIBONACCI =====

    // Đệ quy (chậm - O(2^n)):
    public static int fibRecursive(int n) {
        if (n <= 0) return 0;
        if (n == 1) return 1;
        return fibRecursive(n - 1) + fibRecursive(n - 2);
    }

    // Khử đệ quy (nhanh - O(n)):
    public static int fibIterative(int n) {
        if (n <= 0) return 0;
        if (n == 1) return 1;

        int prev2 = 0; // F(n-2)
        int prev1 = 1; // F(n-1)
        int current = 0;

        for (int i = 2; i <= n; i++) {
            current = prev1 + prev2;
            prev2 = prev1;
            prev1 = current;
        }
        return current;
    }

    // ===== DUYỆT CÂY (ví dụ phức tạp hơn) =====
    // Khử đệ quy bằng Stack thủ công

    // Đệ quy: Tính tổng các chữ số
    public static int digitSumRecursive(int n) {
        if (n < 10) return n;
        return (n % 10) + digitSumRecursive(n / 10);
    }

    // Khử đệ quy:
    public static int digitSumIterative(int n) {
        int sum = 0;
        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }
        return sum;
    }

    // ===== KHỬ ĐỆ QUY BẰNG STACK THỦ CÔNG =====
    // Ví dụ: Tính giai thừa bằng Stack
    public static long factorialWithStack(int n) {
        Stack<Integer> stack = new Stack<>();

        // Push tất cả giá trị cần tính
        for (int i = n; i >= 1; i--) {
            stack.push(i);
        }

        // Pop ra và nhân dần
        long result = 1;
        while (!stack.isEmpty()) {
            result *= stack.pop();
        }
        return result;
    }

    public static void main(String[] args) {
        System.out.println("===== GIAI THỪA =====");
        System.out.println("Đệ quy:   10! = " + factorialRecursive(10));   // 3628800
        System.out.println("Vòng lặp:  10! = " + factorialIterative(10));   // 3628800
        System.out.println("Stack:     10! = " + factorialWithStack(10));    // 3628800

        System.out.println("\n===== FIBONACCI =====");
        System.out.println("Đệ quy:   F(10) = " + fibRecursive(10));   // 55
        System.out.println("Vòng lặp:  F(10) = " + fibIterative(10));  // 55

        // So sánh tốc độ
        System.out.println("\n===== SO SÁNH TỐC ĐỘ FIBONACCI =====");
        int n = 40;

        long start = System.currentTimeMillis();
        fibRecursive(n);
        long timeRecursive = System.currentTimeMillis() - start;

        start = System.currentTimeMillis();
        fibIterative(n);
        long timeIterative = System.currentTimeMillis() - start;

        System.out.println("Đệ quy F(" + n + "): " + timeRecursive + " ms");
        System.out.println("Vòng lặp F(" + n + "): " + timeIterative + " ms");
        // Đệ quy: ~500-1000 ms, Vòng lặp: 0 ms!

        System.out.println("\n===== TỔNG CHỮ SỐ =====");
        System.out.println("Đệ quy:   digitSum(12345) = " + digitSumRecursive(12345)); // 15
        System.out.println("Vòng lặp:  digitSum(12345) = " + digitSumIterative(12345)); // 15
    }
}
```

### 10.4 So sánh đệ quy vs khử đệ quy

| Tiêu chí | Đệ quy | Khử đệ quy (Iterative) |
|---|---|---|
| **Code** | Ngắn gọn, dễ hiểu | Dài hơn, phức tạp hơn |
| **Tốc độ** | Chậm hơn (overhead gọi hàm) | Nhanh hơn |
| **Bộ nhớ** | Tốn stack (mỗi lần gọi = 1 stack frame) | Tiết kiệm hơn |
| **Stack overflow** | Có thể (đệ quy quá sâu) | Không |
| **Phù hợp** | Cây, đồ thị, chia để trị | Bài toán tuyến tính |

---

## 11. Các ký tự chuỗi đặc biệt

### 11.1 Escape characters (Ký tự thoát)

| Ký tự | Tên | Ý nghĩa | ASCII |
|---|---|---|---|
| `\n` | Newline | Xuống dòng mới | 10 |
| `\t` | Tab | Thụt lề (tab ngang) | 9 |
| `\r` | Carriage Return | Đưa con trỏ về đầu dòng | 13 |
| `\b` | Backspace | Xóa ký tự phía trước | 8 |
| `\\` | Backslash | In dấu `\` | 92 |
| `\"` | Double quote | In dấu `"` | 34 |
| `\'` | Single quote | In dấu `'` | 39 |
| `\0` | Null | Ký tự null | 0 |

### 11.2 Format specifiers (Ký tự định dạng - dùng trong printf)

| Ký tự | Kiểu dữ liệu | Ví dụ | Kết quả |
|---|---|---|---|
| `%d` | Số nguyên (int, long) | `printf("%d", 42)` | `42` |
| `%f` | Số thực (float, double) | `printf("%f", 3.14)` | `3.140000` |
| `%.2f` | Số thực (2 chữ số thập phân) | `printf("%.2f", 3.14159)` | `3.14` |
| `%s` | Chuỗi (String) | `printf("%s", "Hello")` | `Hello` |
| `%c` | Ký tự (char) | `printf("%c", 'A')` | `A` |
| `%b` | Boolean | `printf("%b", true)` | `true` |
| `%x` | Hex | `printf("%x", 255)` | `ff` |
| `%o` | Octal | `printf("%o", 8)` | `10` |
| `%e` | Khoa học (scientific) | `printf("%e", 123456.789)` | `1.234568e+05` |
| `%n` | Xuống dòng (platform-independent) | `printf("Hi%n")` | `Hi\n` hoặc `Hi\r\n` |
| `%%` | In dấu % | `printf("100%%")` | `100%` |

### 11.3 Code ví dụ

```java
public class SpecialCharsDemo {
    public static void main(String[] args) {
        // ===== ESCAPE CHARACTERS =====
        System.out.println("===== Escape Characters =====");

        // \n - Xuống dòng
        System.out.println("Dòng 1\nDòng 2\nDòng 3");
        // Dòng 1
        // Dòng 2
        // Dòng 3

        // \t - Tab
        System.out.println("Tên\tTuổi\tĐiểm");
        System.out.println("Dũng\t22\t9.5");
        System.out.println("An\t21\t8.0");
        // Tên     Tuổi    Điểm
        // Dũng    22      9.5
        // An      21      8.0

        // \r - Carriage Return (đưa về đầu dòng, ghi đè)
        System.out.println("ABCDEF\rXY");
        // Kết quả: XYCDEF (XY ghi đè AB)

        // \b - Backspace (xóa 1 ký tự trước)
        System.out.println("Hello\b World");
        // Kết quả: Hell World (xóa ký tự 'o')

        // \\ - In dấu backslash
        System.out.println("Đường dẫn: C:\\Users\\Admin");
        // Đường dẫn: C:\Users\Admin

        // \" - In dấu ngoặc kép
        System.out.println("Anh ấy nói: \"Xin chào!\"");
        // Anh ấy nói: "Xin chào!"

        // ===== FORMAT SPECIFIERS (printf) =====
        System.out.println("\n===== Format Specifiers =====");

        String name = "Dũng";
        int age = 22;
        double gpa = 8.567;
        boolean active = true;

        // %s - String, %d - int, %f - float/double, %b - boolean
        System.out.printf("Tên: %s, Tuổi: %d, GPA: %.2f, Active: %b%n",
                name, age, gpa, active);
        // Tên: Dũng, Tuổi: 22, GPA: 8.57, Active: true

        // Căn lề và padding
        System.out.printf("|%-15s|%5d|%8.2f|%n", "Nguyễn Dũng", 22, 8.567);
        System.out.printf("|%-15s|%5d|%8.2f|%n", "Trần An", 21, 9.123);
        // |Nguyễn Dũng    |   22|    8.57|
        // |Trần An        |   21|    9.12|
        // %-15s : căn trái, chiếm 15 ký tự
        // %5d   : căn phải, chiếm 5 ký tự
        // %8.2f : căn phải, chiếm 8 ký tự, 2 số thập phân

        // Padding với số 0
        System.out.printf("Mã: %05d%n", 42);  // Mã: 00042

        // ===== SỰ KHÁC NHAU \n VÀ \r\n =====
        System.out.println("\n===== \\n vs \\r\\n =====");
        System.out.println("Linux/Mac dùng:   \\n    (LF - Line Feed)");
        System.out.println("Windows dùng:     \\r\\n  (CR+LF)");
        System.out.println("Java %n tự chọn:  phù hợp theo OS");
    }
}
```

---

## 12. Cách xử lý dữ liệu tiền tệ bằng số nguyên

### 12.1 Vấn đề: Tại sao KHÔNG dùng float/double cho tiền?

```java
public class MoneyProblem {
    public static void main(String[] args) {
        // ❌ SAI: Dùng double cho tiền
        double price = 0.10;
        double total = 0;
        for (int i = 0; i < 10; i++) {
            total += price;
        }
        System.out.println("10 × $0.10 = $" + total);
        // Kết quả: $0.9999999999999999 (KHÔNG PHẢI $1.00!)

        // ❌ SAI: Phép trừ tiền
        double balance = 1.00;
        balance -= 0.10;
        balance -= 0.20;
        balance -= 0.30;
        System.out.println("$1.00 - $0.10 - $0.20 - $0.30 = $" + balance);
        // Kết quả: $0.40000000000000013 (KHÔNG PHẢI $0.40!)

        // ❌ NGUY HIỂM: So sánh tiền
        if (balance == 0.40) {
            System.out.println("Đúng $0.40");
        } else {
            System.out.println("KHÔNG phải $0.40!"); // ← Kết quả này!
        }
    }
}
```

### 12.2 Giải pháp 1: Dùng số nguyên (cent)

```java
public class MoneyAsInteger {
    public static void main(String[] args) {
        // ✅ ĐÚNG: Lưu tiền bằng CENT (số nguyên)
        // $0.02 = 2 cent
        // $1.50 = 150 cent
        // $99.99 = 9999 cent

        // Quy tắc: GIÁ TRỊ THẬT = giá_trị_lưu / 100

        // --- Ví dụ: $0.02 ---
        int priceInCents = 2;  // $0.02 = 2 cent
        System.out.println("$0.02 = " + priceInCents + " cent");

        // --- Tính toán ---
        int item1 = 199;   // $1.99
        int item2 = 350;   // $3.50
        int item3 = 2;     // $0.02
        int total = item1 + item2 + item3;  // 551 cent

        System.out.printf("Tổng: %d cent = $%.2f%n", total, total / 100.0);
        // Tổng: 551 cent = $5.51

        // --- Kiểm tra lại vấn đề ban đầu ---
        int price10c = 10;  // $0.10 = 10 cent
        int sum = 0;
        for (int i = 0; i < 10; i++) {
            sum += price10c;
        }
        System.out.printf("10 × $0.10 = %d cent = $%.2f%n", sum, sum / 100.0);
        // 10 × $0.10 = 100 cent = $1.00 (CHÍNH XÁC!)

        // --- Trừ tiền ---
        int balance = 100;   // $1.00
        balance -= 10;       // - $0.10
        balance -= 20;       // - $0.20
        balance -= 30;       // - $0.30
        System.out.printf("Còn lại: %d cent = $%.2f%n", balance, balance / 100.0);
        // Còn lại: 40 cent = $0.40 (CHÍNH XÁC!)

        // --- So sánh chính xác ---
        if (balance == 40) {
            System.out.println("Đúng $0.40 ✅");  // ← Kết quả này!
        }

        // --- Hiển thị đẹp ---
        System.out.println(formatMoney(9999));   // $99.99
        System.out.println(formatMoney(2));       // $0.02
        System.out.println(formatMoney(150));     // $1.50
        System.out.println(formatMoney(1000000)); // $10,000.00
    }

    // Hàm format tiền từ cent sang $
    static String formatMoney(int cents) {
        int dollars = cents / 100;
        int remainCents = cents % 100;

        // Format có dấu phẩy phân cách hàng nghìn
        return String.format("$%,d.%02d", dollars, remainCents);
    }
}
```

### 12.3 Giải pháp 2: Dùng BigDecimal

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

public class MoneyBigDecimal {
    public static void main(String[] args) {
        // ✅ BigDecimal: Chính xác tuyệt đối cho tính toán tiền tệ
        // QUAN TRỌNG: Luôn dùng String constructor, KHÔNG dùng double!

        BigDecimal price = new BigDecimal("0.02");  // ✅ Đúng
        // BigDecimal wrong = new BigDecimal(0.02);  // ❌ Sai (vẫn lỗi floating point)

        BigDecimal item1 = new BigDecimal("1.99");
        BigDecimal item2 = new BigDecimal("3.50");
        BigDecimal item3 = new BigDecimal("0.02");

        BigDecimal total = item1.add(item2).add(item3);
        System.out.println("Tổng: $" + total);  // Tổng: $5.51

        // Thuế 8.5%
        BigDecimal taxRate = new BigDecimal("0.085");
        BigDecimal tax = total.multiply(taxRate).setScale(2, RoundingMode.HALF_UP);
        BigDecimal grandTotal = total.add(tax);

        System.out.println("Thuế: $" + tax);          // Thuế: $0.47
        System.out.println("Tổng cộng: $" + grandTotal); // Tổng cộng: $5.98

        // Chia đều tiền (chia 100$ cho 3 người)
        BigDecimal amount = new BigDecimal("100.00");
        BigDecimal perPerson = amount.divide(new BigDecimal("3"), 2, RoundingMode.HALF_UP);
        System.out.println("Mỗi người: $" + perPerson); // $33.33
        // Còn dư: $100 - $33.33 × 3 = $0.01
    }
}
```

### 12.4 So sánh các phương pháp

| Phương pháp | Ưu điểm | Nhược điểm | Dùng khi |
|---|---|---|---|
| **int/long (cent)** | Nhanh nhất, chính xác, đơn giản | Phải tự chia/nhân 100 | Game, hệ thống đơn giản |
| **BigDecimal** | Chính xác tuyệt đối, nhiều hàm hỗ trợ | Chậm hơn, code dài | Ngân hàng, tài chính, kế toán |
| **double/float** | ❌ Nhanh nhưng không chính xác | Sai số tích lũy | ❌ KHÔNG BAO GIỜ dùng cho tiền! |

---

## 13. Lập trình với mảng

### 13.1 Khai báo mảng

```java
public class ArrayDeclaration {
    public static void main(String[] args) {
        // ===== CÁCH 1: Khai báo rồi khởi tạo kích thước =====
        int[] numbers = new int[5];  // Mảng 5 phần tử, mặc định = 0
        // numbers = [0, 0, 0, 0, 0]

        // ===== CÁCH 2: Khai báo và khởi tạo giá trị =====
        int[] scores = {90, 85, 78, 92, 88};
        // Hoặc: int[] scores = new int[]{90, 85, 78, 92, 88};

        // ===== CÁCH 3: Khai báo kiểu C (không khuyến khích) =====
        int grades[] = {70, 80, 90}; // Hợp lệ nhưng không theo convention Java

        // ===== CÁC KIỂU DỮ LIỆU =====
        String[] names    = {"Dũng", "An", "Bình"};
        double[] prices   = {1.99, 3.50, 0.02};
        boolean[] flags   = {true, false, true};
        char[] vowels     = {'a', 'e', 'i', 'o', 'u'};

        // ===== TRUY CẬP PHẦN TỬ =====
        System.out.println("Phần tử đầu: " + scores[0]);           // 90
        System.out.println("Phần tử cuối: " + scores[scores.length - 1]); // 88
        System.out.println("Kích thước: " + scores.length);         // 5

        // ===== THAY ĐỔI GIÁ TRỊ =====
        scores[2] = 95;  // Thay 78 → 95

        // In mảng
        System.out.println("Mảng: " + java.util.Arrays.toString(scores));
        // [90, 85, 95, 92, 88]

        // ===== MẢNG 2 CHIỀU =====
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };
        System.out.println("matrix[1][2] = " + matrix[1][2]); // 6
    }
}
```

```
Bộ nhớ của mảng:
int[] scores = {90, 85, 78, 92, 88};

Stack                    Heap
┌──────────┐            ┌────┬────┬────┬────┬────┐
│ scores ──┼──────────► │ 90 │ 85 │ 78 │ 92 │ 88 │
│ (tham    │            ├────┼────┼────┼────┼────┤
│  chiếu)  │            │ [0]│ [1]│ [2]│ [3]│ [4]│
└──────────┘            └────┴────┴────┴────┴────┘
                         Các phần tử liên tiếp trong bộ nhớ
                         length = 5
```

### 13.2 Thêm phần tử (mở rộng mảng)

Mảng Java có **kích thước cố định** → phải tạo mảng mới lớn hơn.

```java
import java.util.Arrays;

public class ArrayAdd {
    // Thêm phần tử vào cuối mảng
    public static int[] addElement(int[] original, int newElement) {
        int[] newArray = new int[original.length + 1];

        // Copy toàn bộ mảng cũ
        for (int i = 0; i < original.length; i++) {
            newArray[i] = original[i];
        }
        // Hoặc dùng: System.arraycopy(original, 0, newArray, 0, original.length);

        // Thêm phần tử mới
        newArray[newArray.length - 1] = newElement;
        return newArray;
    }

    // Thêm phần tử tại vị trí index
    public static int[] insertAt(int[] original, int index, int newElement) {
        int[] newArray = new int[original.length + 1];

        for (int i = 0, j = 0; i < newArray.length; i++) {
            if (i == index) {
                newArray[i] = newElement;
            } else {
                newArray[i] = original[j++];
            }
        }
        return newArray;
    }

    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40};
        System.out.println("Ban đầu: " + Arrays.toString(arr));

        arr = addElement(arr, 50);
        System.out.println("Thêm 50: " + Arrays.toString(arr));
        // [10, 20, 30, 40, 50]

        arr = insertAt(arr, 2, 25);
        System.out.println("Chèn 25 tại index 2: " + Arrays.toString(arr));
        // [10, 20, 25, 30, 40, 50]

        // ✅ Cách nhanh hơn: dùng Arrays.copyOf
        int[] arr2 = {1, 2, 3};
        arr2 = Arrays.copyOf(arr2, arr2.length + 1);
        arr2[arr2.length - 1] = 4;
        System.out.println("copyOf: " + Arrays.toString(arr2)); // [1, 2, 3, 4]
    }
}
```

### 13.3 Đổi chỗ phần tử (Swap)

```java
import java.util.Arrays;

public class ArraySwap {
    // Đổi chỗ 2 phần tử
    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Đảo ngược mảng (sử dụng swap)
    public static void reverse(int[] arr) {
        int left = 0;
        int right = arr.length - 1;
        while (left < right) {
            swap(arr, left, right);
            left++;
            right--;
        }
    }

    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40, 50};

        // Đổi chỗ phần tử index 1 và 3
        System.out.println("Trước swap: " + Arrays.toString(arr));
        swap(arr, 1, 3);
        System.out.println("Sau swap(1,3): " + Arrays.toString(arr));
        // [10, 40, 30, 20, 50]

        // Đảo ngược mảng
        int[] arr2 = {1, 2, 3, 4, 5};
        System.out.println("\nTrước reverse: " + Arrays.toString(arr2));
        reverse(arr2);
        System.out.println("Sau reverse:   " + Arrays.toString(arr2));
        // [5, 4, 3, 2, 1]
    }
}
```

### 13.4 Copy mảng

```java
import java.util.Arrays;

public class ArrayCopy {
    public static void main(String[] args) {
        int[] original = {10, 20, 30, 40, 50};

        // ===== CÁCH 1: Vòng lặp (thủ công) =====
        int[] copy1 = new int[original.length];
        for (int i = 0; i < original.length; i++) {
            copy1[i] = original[i];
        }

        // ===== CÁCH 2: System.arraycopy (nhanh nhất) =====
        int[] copy2 = new int[original.length];
        System.arraycopy(original, 0, copy2, 0, original.length);
        // arraycopy(src, srcPos, dest, destPos, length)

        // ===== CÁCH 3: Arrays.copyOf =====
        int[] copy3 = Arrays.copyOf(original, original.length);

        // Copy một phần
        int[] partial = Arrays.copyOfRange(original, 1, 4);
        // [20, 30, 40] (index 1 đến 3, không bao gồm 4)

        // ===== CÁCH 4: clone() =====
        int[] copy4 = original.clone();

        // ===== KIỂM TRA =====
        System.out.println("Original: " + Arrays.toString(original));
        System.out.println("Copy 1:   " + Arrays.toString(copy1));
        System.out.println("Copy 2:   " + Arrays.toString(copy2));
        System.out.println("Copy 3:   " + Arrays.toString(copy3));
        System.out.println("Copy 4:   " + Arrays.toString(copy4));
        System.out.println("Partial:  " + Arrays.toString(partial));

        // ===== QUAN TRỌNG: Shallow copy vs Deep copy =====
        // Với mảng primitive (int, double...): copy giá trị → OK
        copy1[0] = 999;
        System.out.println("\nSau sửa copy1[0] = 999:");
        System.out.println("Original: " + Arrays.toString(original)); // [10,...] (không ảnh hưởng)
        System.out.println("Copy 1:   " + Arrays.toString(copy1));    // [999,...]

        // ⚠️ Với mảng Object: chỉ copy tham chiếu (shallow copy)!
        String[] names = {"Dũng", "An"};
        String[] namesCopy = names.clone();
        // names và namesCopy trỏ đến cùng các String object
    }
}
```

### 13.5 Sắp xếp mảng

```java
import java.util.Arrays;

public class ArraySort {
    // ===== BUBBLE SORT (Sắp xếp nổi bọt) =====
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Đổi chỗ
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            if (!swapped) break; // Đã sắp xếp xong
        }
    }

    // ===== SELECTION SORT (Sắp xếp chọn) =====
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            // Đổi chỗ arr[i] và arr[minIdx]
            int temp = arr[i];
            arr[i] = arr[minIdx];
            arr[minIdx] = temp;
        }
    }

    // ===== INSERTION SORT (Sắp xếp chèn) =====
    public static void insertionSort(int[] arr) {
        for (int i = 1; i < arr.length; i++) {
            int key = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }
            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        // ===== SẮP XẾP BẰNG HÀM THỦ CÔNG =====
        int[] arr1 = {64, 34, 25, 12, 22, 11, 90};
        System.out.println("Ban đầu:       " + Arrays.toString(arr1));

        bubbleSort(arr1);
        System.out.println("Bubble Sort:   " + Arrays.toString(arr1));

        int[] arr2 = {64, 34, 25, 12, 22, 11, 90};
        selectionSort(arr2);
        System.out.println("Selection Sort:" + Arrays.toString(arr2));

        int[] arr3 = {64, 34, 25, 12, 22, 11, 90};
        insertionSort(arr3);
        System.out.println("Insertion Sort:" + Arrays.toString(arr3));
        // Tất cả: [11, 12, 22, 25, 34, 64, 90]

        // ===== SẮP XẾP BẰNG Arrays.sort() (khuyến khích) =====
        int[] arr4 = {64, 34, 25, 12, 22, 11, 90};
        Arrays.sort(arr4);  // Dùng Dual-Pivot Quicksort (rất nhanh)
        System.out.println("Arrays.sort(): " + Arrays.toString(arr4));

        // Sắp xếp một phần
        int[] arr5 = {5, 3, 1, 4, 2};
        Arrays.sort(arr5, 1, 4);  // Sắp xếp từ index 1 đến 3
        System.out.println("Sort(1,4):     " + Arrays.toString(arr5)); // [5, 1, 3, 4, 2]

        // ===== SẮP XẾP GIẢM DẦN =====
        Integer[] arr6 = {64, 34, 25, 12, 22, 11, 90};
        Arrays.sort(arr6, java.util.Collections.reverseOrder());
        System.out.println("Giảm dần:      " + Arrays.toString(arr6));
        // [90, 64, 34, 25, 22, 12, 11]

        // ===== TÌM KIẾM SAU KHI SẮP XẾP =====
        int[] sorted = {11, 12, 22, 25, 34, 64, 90};
        int idx = Arrays.binarySearch(sorted, 25);
        System.out.println("Tìm 25 tại index: " + idx);  // 3
    }
}
```

### 13.6 Minh họa Bubble Sort

```
Bubble Sort - Mỗi vòng lặp, phần tử lớn nhất "nổi" lên cuối:

Ban đầu: [64, 34, 25, 12, 22, 11, 90]

Lượt 1: So sánh và đổi chỗ từ trái sang phải
  [64, 34, ...] → 64 > 34 → đổi → [34, 64, 25, 12, 22, 11, 90]
  [.., 64, 25, ...] → 64 > 25 → đổi → [34, 25, 64, 12, 22, 11, 90]
  [.., 64, 12, ...] → 64 > 12 → đổi → [34, 25, 12, 64, 22, 11, 90]
  [.., 64, 22, ...] → 64 > 22 → đổi → [34, 25, 12, 22, 64, 11, 90]
  [.., 64, 11, ...] → 64 > 11 → đổi → [34, 25, 12, 22, 11, 64, 90]
  [.., 64, 90]      → 64 < 90 → giữ → [34, 25, 12, 22, 11, 64, 90]
                                                              ↑ 90 cố định

Lượt 2: (bỏ phần tử cuối - đã đúng vị trí)
  [34, 25, 12, 22, 11, 64] → ... → [25, 12, 22, 11, 34, 64, 90]
                                                    ↑ 64 cố định

...tiếp tục cho đến khi sắp xếp xong.

Kết quả: [11, 12, 22, 25, 34, 64, 90]
```

### 13.7 Tổng hợp các thao tác với mảng

| Thao tác | Phương pháp | Độ phức tạp |
|---|---|---|
| **Khai báo** | `int[] arr = new int[n]` hoặc `{1,2,3}` | O(n) |
| **Truy cập** | `arr[index]` | O(1) |
| **Tìm kiếm** (chưa sort) | Duyệt tuần tự | O(n) |
| **Tìm kiếm** (đã sort) | `Arrays.binarySearch()` | O(log n) |
| **Thêm cuối** | Tạo mảng mới, copy | O(n) |
| **Chèn giữa** | Tạo mảng mới, copy + dịch | O(n) |
| **Xóa** | Tạo mảng mới, copy bỏ qua | O(n) |
| **Sắp xếp** | `Arrays.sort()` | O(n log n) |
| **Copy** | `Arrays.copyOf()`, `System.arraycopy()` | O(n) |
| **So sánh** | `Arrays.equals()` | O(n) |

> **💡 Nhận xét**: Mảng có kích thước **cố định** và thêm/xóa phần tử **tốn kém** (O(n)). Khi cần thêm/xóa thường xuyên, hãy dùng `ArrayList` (sẽ học trong phần Collection).

---

> **📌 Kết thúc Phần 2: Lập Trình Cơ Bản**

---

# Phần 3: Lập Trình Hướng Đối Tượng (OOP)

## 📌 Mục lục

1. [Tính đóng gói (Encapsulation)](#1-tính-đóng-gói-encapsulation)
2. [Tính kế thừa (Inheritance)](#2-tính-kế-thừa-inheritance)
3. [Tính trừu tượng (Abstraction)](#3-tính-trừu-tượng-abstraction)
4. [Tính đa hình (Polymorphism) & Interface](#4-tính-đa-hình-polymorphism--interface)
5. [Cấu trúc Class và khai báo đối tượng](#5-cấu-trúc-class-và-khai-báo-đối-tượng)
6. [Hàm khởi tạo Constructor](#6-hàm-khởi-tạo-constructor)
7. [Từ khóa this và super](#7-từ-khóa-this-và-super)
8. [Nạp chồng và ghi đè phương thức](#8-nạp-chồng-overloading-và-ghi-đè-overriding-phương-thức)
9. [Mảng đối tượng cùng implement 1 interface](#9-mảng-đối-tượng-cùng-implement-1-interface)
10. [Sự khác nhau giữa Abstract và Interface](#10-sự-khác-nhau-giữa-abstract-và-interface)
11. [Từ khóa static](#11-từ-khóa-static)
12. [Access Modifier](#12-access-modifier)
13. [Nạp chồng hàm (các hàm cùng tên khác tham số)](#13-nạp-chồng-hàm---các-hàm-cùng-tên-khác-tham-số)
14. [Từ khóa final](#14-từ-khóa-final)
15. [Biến static, biến final, hằng số](#15-biến-static-biến-final-hằng-số)
16. [Toán tử instanceof](#16-toán-tử-instanceof)
17. [Các lớp Wrapper](#17-các-lớp-wrapper)
18. [Chuyển đổi (cast) kiểu dữ liệu](#18-chuyển-đổi-cast-kiểu-dữ-liệu)
19. [Parse giá trị từ String sang số](#19-parse-giá-trị-từ-string-sang-số)
20. [Danh sách liên kết (Linked List)](#20-danh-sách-liên-kết-linked-list)
21. [So sánh DSLK và Mảng truyền thống](#21-so-sánh-dslk-và-mảng-truyền-thống)
22. [Khai báo chuỗi, cắt chuỗi, nối chuỗi](#22-khai-báo-chuỗi-cắt-chuỗi-nối-chuỗi)
23. [StringBuilder và StringTokenizer](#23-stringbuilder-và-stringtokenizer)
24. [So sánh cộng String và StringBuilder](#24-so-sánh-cộng-string-và-stringbuilder)
25. [Nạp chồng toString](#25-nạp-chồng-tostring)
26. [Hashing](#26-hashing)
27. [Tự tạo hàm hashing 3 số nguyên](#27-tự-tạo-hàm-hashing-3-số-nguyên)
28. [Sử dụng MD5 / CRC32 để hash chuỗi](#28-sử-dụng-md5--crc32-để-hash-chuỗi)
29. [Hashing để ẩn password](#29-hashing-để-ẩn-password)
30. [Hashtable và bảng băm](#30-hashtable-và-bảng-băm)
31. [Ghi đè hashCode và equals](#31-ghi-đè-hashcode-và-equals)

---

## 1. Tính đóng gói (Encapsulation)

### 1.1 Đóng gói là gì?

**Đóng gói** là việc **gói dữ liệu (thuộc tính) và phương thức (hành vi)** vào trong **một class**, đồng thời **ẩn giấu** chi tiết bên trong, chỉ cho phép truy cập thông qua các phương thức public (getter/setter).

```
Đóng gói = Gói (thuộc tính + phương thức) VÀO trong Class
         + Ẩn giấu (dùng private) chi tiết bên trong
         + Chỉ cho truy cập qua giao diện public (getter/setter)

  ┌───────────────── Class BankAccount ─────────────────┐
  │                                                      │
  │  🔒 private (ẨN - bên ngoài KHÔNG thấy)             │
  │  ┌────────────────────────────────────────────┐      │
  │  │  - balance: double                         │      │
  │  │  - accountNumber: String                   │      │
  │  │  - pin: String                             │      │
  │  └────────────────────────────────────────────┘      │
  │                                                      │
  │  🔓 public (MỞ - bên ngoài có thể gọi)              │
  │  ┌────────────────────────────────────────────┐      │
  │  │  + getBalance(): double                    │      │
  │  │  + deposit(amount): void                   │      │
  │  │  + withdraw(amount): boolean               │      │
  │  └────────────────────────────────────────────┘      │
  └──────────────────────────────────────────────────────┘

Bên ngoài:
  account.balance = -1000;  // ❌ KHÔNG THỂ truy cập trực tiếp
  account.deposit(500);     // ✅ Phải gọi qua phương thức public
```

### 1.2 Code ví dụ

```java
// ===== KHÔNG ĐÓNG GÓI (SAI) =====
class BadBankAccount {
    public double balance;      // Ai cũng truy cập được
    public String accountNumber;
    public String pin;
    // → Bên ngoài có thể: account.balance = -99999; (NGUY HIỂM!)
}

// ===== CÓ ĐÓNG GÓI (ĐÚNG) =====
class BankAccount {
    // 🔒 Thuộc tính private - ẨN dữ liệu bên trong
    private double balance;
    private String accountNumber;
    private String ownerName;

    // 🔓 Constructor public
    public BankAccount(String accountNumber, String ownerName, double initialBalance) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = initialBalance;
    }

    // 🔓 Getter - chỉ cho đọc, KHÔNG cho sửa trực tiếp
    public double getBalance() {
        return balance;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public String getOwnerName() {
        return ownerName;
    }

    // 🔓 Setter có kiểm tra dữ liệu (validation)
    public void setOwnerName(String ownerName) {
        if (ownerName == null || ownerName.trim().isEmpty()) {
            throw new IllegalArgumentException("Tên không được rỗng!");
        }
        this.ownerName = ownerName;
    }
    // Lưu ý: KHÔNG có setBalance() - không cho phép sửa trực tiếp!

    // 🔓 Phương thức nghiệp vụ (có kiểm tra logic)
    public void deposit(double amount) {
        if (amount <= 0) {
            System.out.println("❌ Số tiền gửi phải lớn hơn 0!");
            return;
        }
        balance += amount;
        System.out.printf("✅ Gửi $%.2f thành công. Số dư: $%.2f%n", amount, balance);
    }

    public boolean withdraw(double amount) {
        if (amount <= 0) {
            System.out.println("❌ Số tiền rút phải lớn hơn 0!");
            return false;
        }
        if (amount > balance) {
            System.out.println("❌ Số dư không đủ!");
            return false;
        }
        balance -= amount;
        System.out.printf("✅ Rút $%.2f thành công. Số dư: $%.2f%n", amount, balance);
        return true;
    }
}

// ===== SỬ DỤNG =====
public class EncapsulationDemo {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount("ACC001", "Nguyễn Dũng", 1000.0);

        // acc.balance = -5000;    // ❌ LỖI BIÊN DỊCH! balance là private
        // acc.balance += 999999;  // ❌ LỖI! Không thể hack

        acc.deposit(500);          // ✅ Gửi $500.00 thành công. Số dư: $1500.00
        acc.withdraw(200);         // ✅ Rút $200.00 thành công. Số dư: $1300.00
        acc.withdraw(5000);        // ❌ Số dư không đủ!
        acc.deposit(-100);         // ❌ Số tiền gửi phải lớn hơn 0!

        System.out.println("Số dư: $" + acc.getBalance()); // 1300.0
    }
}
```

### 1.3 Ý nghĩa thực tế

| Lợi ích | Giải thích |
|---|---|
| **Bảo vệ dữ liệu** | Không ai sửa `balance` thành -99999 được |
| **Kiểm soát logic** | Gửi/rút tiền phải qua kiểm tra (amount > 0, đủ số dư) |
| **Dễ bảo trì** | Thay đổi logic bên trong mà không ảnh hưởng code bên ngoài |
| **Tái sử dụng** | Class độc lập, dùng ở đâu cũng được |

---

## 2. Tính kế thừa (Inheritance)

### 2.1 Kế thừa là gì?

**Kế thừa** cho phép một class con (**subclass**) **thừa hưởng** thuộc tính và phương thức từ class cha (**superclass**). Dùng từ khóa `extends`.

```
          ┌──────────────────┐
          │     Animal       │  ← Class CHA (superclass)
          │  - name: String  │
          │  - age: int      │
          │  + eat()         │
          │  + sleep()       │
          └───────┬──────────┘
                  │ extends
        ┌─────────┴─────────┐
        │                   │
  ┌─────▼──────┐     ┌─────▼──────┐
  │    Dog     │     │    Cat     │  ← Class CON (subclass)
  │  + bark()  │     │  + meow()  │
  │  + fetch() │     │  + purr()  │
  └────────────┘     └────────────┘

  Dog kế thừa: name, age, eat(), sleep() từ Animal
  Dog có thêm: bark(), fetch() riêng
```

### 2.2 Code ví dụ

```java
// ===== CLASS CHA =====
class Animal {
    protected String name;
    protected int age;

    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
        System.out.println("→ Constructor Animal được gọi");
    }

    public void eat() {
        System.out.println(name + " đang ăn...");
    }

    public void sleep() {
        System.out.println(name + " đang ngủ...");
    }

    public String info() {
        return name + " (" + age + " tuổi)";
    }
}

// ===== CLASS CON 1: Dog extends Animal =====
class Dog extends Animal {
    private String breed; // Thuộc tính riêng

    public Dog(String name, int age, String breed) {
        super(name, age); // Gọi constructor của class cha
        this.breed = breed;
        System.out.println("→ Constructor Dog được gọi");
    }

    // Phương thức riêng của Dog
    public void bark() {
        System.out.println(name + " sủa: Gâu gâu! 🐕");
    }

    public void fetch(String item) {
        System.out.println(name + " đang nhặt " + item);
    }

    // OVERRIDE (ghi đè) phương thức của class cha
    @Override
    public void eat() {
        System.out.println(name + " đang gặm xương... 🦴");
    }

    @Override
    public String info() {
        return super.info() + " - Giống: " + breed;
    }
}

// ===== CLASS CON 2: Cat extends Animal =====
class Cat extends Animal {
    private boolean isIndoor;

    public Cat(String name, int age, boolean isIndoor) {
        super(name, age);
        this.isIndoor = isIndoor;
    }

    public void meow() {
        System.out.println(name + " kêu: Meo meo! 🐱");
    }

    @Override
    public void eat() {
        System.out.println(name + " đang ăn cá... 🐟");
    }
}

// ===== SỬ DỤNG =====
public class InheritanceDemo {
    public static void main(String[] args) {
        Dog dog = new Dog("Buddy", 3, "Golden Retriever");
        Cat cat = new Cat("Mimi", 2, true);

        System.out.println("\n--- Dog ---");
        System.out.println(dog.info());  // Buddy (3 tuổi) - Giống: Golden Retriever
        dog.eat();   // Buddy đang gặm xương... 🦴  (overridden)
        dog.sleep(); // Buddy đang ngủ...            (kế thừa từ Animal)
        dog.bark();  // Buddy sủa: Gâu gâu! 🐕      (riêng của Dog)

        System.out.println("\n--- Cat ---");
        cat.eat();   // Mimi đang ăn cá... 🐟
        cat.sleep(); // Mimi đang ngủ...
        cat.meow();  // Mimi kêu: Meo meo! 🐱
    }
}
```

### 2.3 Override - Ghi đè phương thức

**Override** = class con **viết lại** phương thức đã có ở class cha để thay đổi hành vi.

```java
// Trong class Animal:
public void eat() {
    System.out.println(name + " đang ăn...");  // Hành vi chung
}

// Trong class Dog (override):
@Override
public void eat() {
    System.out.println(name + " đang gặm xương...");  // Hành vi riêng của Dog
}

// @Override: annotation KHÔNG bắt buộc nhưng NÊN dùng
// → Giúp compiler kiểm tra: nếu tên hàm sai → báo lỗi ngay
```

---

## 3. Tính trừu tượng (Abstraction)

### 3.1 Abstract là gì?

**Trừu tượng** là việc **ẩn giấu chi tiết triển khai**, chỉ **hiển thị chức năng** cho người dùng. Abstract class là class **chưa hoàn chỉnh**, chứa các phương thức chưa có thân hàm (abstract method).

```
Khi nào dùng Abstract Class?
→ Khi có một nhóm class LIÊN QUAN, chia sẻ một phần code chung,
  nhưng MỖI class con có CÁCH TRIỂN KHAI RIÊNG cho một số phương thức.

Ví dụ thực tế: Hình dạng (Shape)
- Mọi hình đều có diện tích, chu vi → khai báo abstract
- Nhưng CÁCH TÍNH diện tích hình tròn ≠ hình chữ nhật → mỗi class con tự triển khai
```

### 3.2 Code ví dụ

```java
// ===== ABSTRACT CLASS =====
abstract class Shape {
    protected String color;
    protected String name;

    public Shape(String name, String color) {
        this.name = name;
        this.color = color;
    }

    // Abstract method - KHÔNG có thân hàm
    // → Bắt buộc class con PHẢI triển khai
    public abstract double getArea();
    public abstract double getPerimeter();

    // Phương thức BÌNH THƯỜNG - có thân hàm
    // → Class con kế thừa được luôn
    public void displayInfo() {
        System.out.printf("%s [%s]: Diện tích = %.2f, Chu vi = %.2f%n",
                name, color, getArea(), getPerimeter());
    }
}

// ===== CLASS CON 1: Hình tròn =====
class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super("Hình tròn", color);
        this.radius = radius;
    }

    @Override
    public double getArea() {
        return Math.PI * radius * radius;  // πr²
    }

    @Override
    public double getPerimeter() {
        return 2 * Math.PI * radius;  // 2πr
    }
}

// ===== CLASS CON 2: Hình chữ nhật =====
class Rectangle extends Shape {
    private double width, height;

    public Rectangle(String color, double width, double height) {
        super("Hình chữ nhật", color);
        this.width = width;
        this.height = height;
    }

    @Override
    public double getArea() {
        return width * height;
    }

    @Override
    public double getPerimeter() {
        return 2 * (width + height);
    }
}

// ===== CLASS CON 3: Hình tam giác =====
class Triangle extends Shape {
    private double a, b, c; // 3 cạnh

    public Triangle(String color, double a, double b, double c) {
        super("Hình tam giác", color);
        this.a = a;
        this.b = b;
        this.c = c;
    }

    @Override
    public double getArea() {
        double s = (a + b + c) / 2;  // Nửa chu vi
        return Math.sqrt(s * (s - a) * (s - b) * (s - c)); // Công thức Heron
    }

    @Override
    public double getPerimeter() {
        return a + b + c;
    }
}

// ===== SỬ DỤNG =====
public class AbstractDemo {
    public static void main(String[] args) {
        // Shape s = new Shape("test", "red"); // ❌ LỖI! Không thể tạo đối tượng abstract

        Shape circle = new Circle("Đỏ", 5);
        Shape rect = new Rectangle("Xanh", 4, 6);
        Shape tri = new Triangle("Vàng", 3, 4, 5);

        circle.displayInfo();  // Hình tròn [Đỏ]: Diện tích = 78.54, Chu vi = 31.42
        rect.displayInfo();    // Hình chữ nhật [Xanh]: Diện tích = 24.00, Chu vi = 20.00
        tri.displayInfo();     // Hình tam giác [Vàng]: Diện tích = 6.00, Chu vi = 12.00

        // Mảng đa hình
        Shape[] shapes = {circle, rect, tri};
        double totalArea = 0;
        for (Shape s : shapes) {
            totalArea += s.getArea();
        }
        System.out.printf("Tổng diện tích: %.2f%n", totalArea);
    }
}
```

---

## 4. Tính đa hình (Polymorphism) & Interface

### 4.1 Đa hình là gì?

**Đa hình** = "Nhiều hình thái" — cùng một hành động nhưng **biểu hiện khác nhau** tùy theo đối tượng thực tế.

```
Cùng gọi hàm speak():
  Animal a1 = new Dog();   → a1.speak() → "Gâu gâu!"
  Animal a2 = new Cat();   → a2.speak() → "Meo meo!"
  Animal a3 = new Duck();  → a3.speak() → "Quạc quạc!"

  → Cùng kiểu Animal, cùng gọi speak(), nhưng KẾT QUẢ KHÁC NHAU
  → Đây chính là ĐA HÌNH!
```

### 4.2 Interface là gì?

**Interface** là một **"hợp đồng"** định nghĩa các phương thức mà class **bắt buộc phải triển khai**. Interface chỉ có khai báo, không có triển khai (trước Java 8).

```
Interface giống như "bản mô tả việc cần làm",
class implement interface giống như "người nhận việc và làm theo cách riêng"

  ┌───────────────────┐
  │ «interface»       │
  │   Drawable         │
  │  + draw(): void   │
  │  + resize(): void │
  └────────┬──────────┘
           │ implements
     ┌─────┴──────┐
     │            │
  ┌──▼───┐   ┌───▼──┐
  │Circle│   │Square│  ← Mỗi class triển khai draw() theo cách riêng
  └──────┘   └──────┘
```

### 4.3 Code ví dụ

```java
// ===== INTERFACE =====
interface Playable {
    // Phương thức abstract (mặc định đã là public abstract)
    void play();
    void stop();
    String getType();

    // Default method (Java 8+) - có thân hàm
    default void pause() {
        System.out.println("⏸ Tạm dừng " + getType());
    }

    // Static method trong interface
    static void about() {
        System.out.println("Interface Playable - Định nghĩa hành vi phát media");
    }
}

// ===== INTERFACE THỨ 2 =====
interface Recordable {
    void record();
    void stopRecording();
}

// ===== CLASS IMPLEMENT 1 INTERFACE =====
class MusicPlayer implements Playable {
    private String songName;

    public MusicPlayer(String songName) {
        this.songName = songName;
    }

    @Override
    public void play() {
        System.out.println("🎵 Đang phát nhạc: " + songName);
    }

    @Override
    public void stop() {
        System.out.println("⏹ Dừng phát nhạc: " + songName);
    }

    @Override
    public String getType() {
        return "Music Player";
    }
}

// ===== CLASS IMPLEMENT 2 INTERFACE (đa kế thừa interface) =====
class VideoPlayer implements Playable, Recordable {
    private String videoName;

    public VideoPlayer(String videoName) {
        this.videoName = videoName;
    }

    @Override
    public void play() {
        System.out.println("🎬 Đang phát video: " + videoName);
    }

    @Override
    public void stop() {
        System.out.println("⏹ Dừng video: " + videoName);
    }

    @Override
    public String getType() {
        return "Video Player";
    }

    @Override
    public void record() {
        System.out.println("⏺ Đang ghi hình...");
    }

    @Override
    public void stopRecording() {
        System.out.println("⏹ Dừng ghi hình");
    }
}

// ===== GAME implement Playable =====
class Game implements Playable {
    private String gameName;

    public Game(String gameName) {
        this.gameName = gameName;
    }

    @Override
    public void play() {
        System.out.println("🎮 Đang chơi game: " + gameName);
    }

    @Override
    public void stop() {
        System.out.println("⏹ Thoát game: " + gameName);
    }

    @Override
    public String getType() {
        return "Game";
    }
}

// ===== SỬ DỤNG =====
public class PolymorphismDemo {
    public static void main(String[] args) {
        // Đa hình: cùng kiểu Playable, nhưng hành vi khác nhau
        Playable music = new MusicPlayer("Hoa Nở Không Màu");
        Playable video = new VideoPlayer("Java Tutorial");
        Playable game  = new Game("Minecraft");

        System.out.println("===== ĐA HÌNH =====");
        music.play();  // 🎵 Đang phát nhạc: Hoa Nở Không Màu
        video.play();  // 🎬 Đang phát video: Java Tutorial
        game.play();   // 🎮 Đang chơi game: Minecraft

        // Default method
        music.pause(); // ⏸ Tạm dừng Music Player

        // Static method
        Playable.about();

        // Duyệt mảng đa hình
        System.out.println("\n===== Duyệt mảng =====");
        Playable[] players = {music, video, game};
        for (Playable p : players) {
            p.play();
            p.stop();
            System.out.println("---");
        }
    }
}
```

---

## 5. Cấu trúc Class và khai báo đối tượng

### 5.1 Cấu trúc đầy đủ của một Class

```java
// ===== CẤU TRÚC ĐẦY ĐỦ CỦA MỘT CLASS =====
public class Student {
    // ========== 1. THUỘC TÍNH (Fields/Attributes) ==========
    // Biến static (dùng chung cho tất cả đối tượng)
    private static int studentCount = 0;
    public static final String SCHOOL_NAME = "HCMUS"; // Hằng số

    // Biến instance (riêng cho từng đối tượng)
    private int id;
    private String name;
    private double gpa;
    private String major;

    // ========== 2. CONSTRUCTOR (Hàm khởi tạo) ==========
    // Constructor mặc định
    public Student() {
        studentCount++;
        this.id = studentCount;
        this.name = "Unknown";
        this.gpa = 0.0;
        this.major = "Undeclared";
    }

    // Constructor có tham số
    public Student(String name, double gpa, String major) {
        studentCount++;
        this.id = studentCount;
        this.name = name;
        this.gpa = gpa;
        this.major = major;
    }

    // ========== 3. GETTER / SETTER ==========
    public int getId() { return id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public double getGpa() { return gpa; }
    public void setGpa(double gpa) {
        if (gpa >= 0.0 && gpa <= 10.0) {
            this.gpa = gpa;
        } else {
            throw new IllegalArgumentException("GPA phải từ 0 đến 10!");
        }
    }

    public String getMajor() { return major; }
    public void setMajor(String major) { this.major = major; }

    // ========== 4. PHƯƠNG THỨC (Methods) ==========
    public String getGrade() {
        if (gpa >= 9.0) return "Xuất sắc";
        if (gpa >= 8.0) return "Giỏi";
        if (gpa >= 7.0) return "Khá";
        if (gpa >= 5.0) return "Trung bình";
        return "Yếu";
    }

    // ========== 5. STATIC METHOD ==========
    public static int getStudentCount() {
        return studentCount;
    }

    // ========== 6. TOSTRING (Ghi đè từ Object) ==========
    @Override
    public String toString() {
        return String.format("Student{id=%d, name='%s', gpa=%.1f, major='%s', grade='%s'}",
                id, name, gpa, major, getGrade());
    }
}

// ===== KHAI BÁO VÀ SỬ DỤNG ĐỐI TƯỢNG =====
public class ClassDemo {
    public static void main(String[] args) {
        // Cách 1: Dùng constructor mặc định
        Student s1 = new Student();
        System.out.println(s1); // Student{id=1, name='Unknown', gpa=0.0, ...}

        // Cách 2: Dùng constructor có tham số
        Student s2 = new Student("Nguyễn Dũng", 8.5, "CNTT");
        Student s3 = new Student("Trần An", 9.2, "KHMT");

        System.out.println(s2); // Student{id=2, name='Nguyễn Dũng', gpa=8.5, ...}
        System.out.println(s3); // Student{id=3, name='Trần An', gpa=9.2, ...}

        // Sử dụng getter/setter
        s2.setGpa(9.0);
        System.out.println(s2.getName() + " xếp loại: " + s2.getGrade());

        // Static method
        System.out.println("Tổng sinh viên: " + Student.getStudentCount()); // 3
        System.out.println("Trường: " + Student.SCHOOL_NAME); // HCMUS
    }
}
```

---

## 6. Hàm khởi tạo Constructor

```java
public class ConstructorDemo {
    // ===== CLASS VỚI NHIỀU LOẠI CONSTRUCTOR =====
    static class Product {
        private String name;
        private double price;
        private int quantity;
        private String category;

        // 1. Constructor mặc định (no-arg)
        public Product() {
            this.name = "Unknown";
            this.price = 0.0;
            this.quantity = 0;
            this.category = "General";
            System.out.println("→ Gọi constructor mặc định");
        }

        // 2. Constructor có 2 tham số
        public Product(String name, double price) {
            this.name = name;
            this.price = price;
            this.quantity = 1;
            this.category = "General";
            System.out.println("→ Gọi constructor 2 tham số");
        }

        // 3. Constructor đầy đủ
        public Product(String name, double price, int quantity, String category) {
            this.name = name;
            this.price = price;
            this.quantity = quantity;
            this.category = category;
            System.out.println("→ Gọi constructor đầy đủ");
        }

        // 4. Constructor gọi constructor khác (this)
        public Product(String name) {
            this(name, 0.0); // Gọi constructor 2 tham số
            System.out.println("→ Gọi constructor 1 tham số (đã gọi this(name, 0.0))");
        }

        // 5. Copy constructor
        public Product(Product other) {
            this.name = other.name;
            this.price = other.price;
            this.quantity = other.quantity;
            this.category = other.category;
            System.out.println("→ Gọi copy constructor");
        }

        @Override
        public String toString() {
            return String.format("%s - $%.2f x%d [%s]", name, price, quantity, category);
        }
    }

    public static void main(String[] args) {
        Product p1 = new Product();                                // Constructor mặc định
        Product p2 = new Product("Laptop", 999.99);               // 2 tham số
        Product p3 = new Product("Phone", 699.0, 5, "Electronics"); // Đầy đủ
        Product p4 = new Product("Tablet");                        // 1 tham số → gọi this()
        Product p5 = new Product(p2);                              // Copy constructor

        System.out.println("\n--- Kết quả ---");
        System.out.println("p1: " + p1);
        System.out.println("p2: " + p2);
        System.out.println("p3: " + p3);
        System.out.println("p4: " + p4);
        System.out.println("p5: " + p5);
    }
}
```

---

## 7. Từ khóa this và super

```java
class Vehicle {
    protected String brand;
    protected int year;

    public Vehicle(String brand, int year) {
        this.brand = brand;  // this = đối tượng hiện tại
        this.year = year;
    }

    public void start() {
        System.out.println(brand + " đang khởi động...");
    }

    public void displayInfo() {
        System.out.println("Xe: " + brand + " (" + year + ")");
    }
}

class Car extends Vehicle {
    private int numDoors;
    private String engineType;

    public Car(String brand, int year, int numDoors, String engineType) {
        super(brand, year);         // super() → gọi constructor của class CHA
        this.numDoors = numDoors;   // this → phân biệt tham số và thuộc tính
        this.engineType = engineType;
    }

    // this - trả về chính đối tượng (method chaining)
    public Car setNumDoors(int numDoors) {
        this.numDoors = numDoors;
        return this;  // Trả về chính đối tượng hiện tại
    }

    public Car setEngineType(String engineType) {
        this.engineType = engineType;
        return this;
    }

    @Override
    public void start() {
        super.start();  // super.method() → gọi phương thức của class CHA
        System.out.println("Động cơ " + engineType + " đã sẵn sàng!");
    }

    @Override
    public void displayInfo() {
        super.displayInfo();  // Gọi displayInfo() của Vehicle
        System.out.println("Số cửa: " + numDoors + ", Động cơ: " + engineType);
    }
}

public class ThisSuperDemo {
    public static void main(String[] args) {
        Car car = new Car("Toyota", 2024, 4, "Hybrid");

        car.start();
        // Toyota đang khởi động...       ← super.start()
        // Động cơ Hybrid đã sẵn sàng!     ← code riêng của Car

        car.displayInfo();
        // Xe: Toyota (2024)               ← super.displayInfo()
        // Số cửa: 4, Động cơ: Hybrid      ← code riêng

        // Method chaining với this
        Car car2 = new Car("Honda", 2023, 2, "Gasoline");
        car2.setNumDoors(4).setEngineType("Electric"); // Chuỗi gọi liên tiếp
        car2.displayInfo();
    }
}
```

**Tóm tắt:**

| Từ khóa | Ý nghĩa | Ví dụ |
|---|---|---|
| `this.field` | Thuộc tính của **đối tượng hiện tại** | `this.name = name;` |
| `this()` | Gọi **constructor khác** cùng class | `this(name, 0.0);` |
| `this` | Trả về **đối tượng hiện tại** | `return this;` (method chaining) |
| `super.field` | Thuộc tính của **class cha** | `super.name` |
| `super()` | Gọi **constructor** của class cha | `super(brand, year);` |
| `super.method()` | Gọi **phương thức** của class cha | `super.start();` |

---

## 8. Nạp chồng (Overloading) và Ghi đè (Overriding) phương thức

```java
class Calculator {
    // ===== NẠP CHỒNG (OVERLOADING): Cùng tên, KHÁC tham số =====
    public int add(int a, int b) {
        System.out.println("add(int, int)");
        return a + b;
    }

    public double add(double a, double b) {
        System.out.println("add(double, double)");
        return a + b;
    }

    public int add(int a, int b, int c) {
        System.out.println("add(int, int, int)");
        return a + b + c;
    }

    public String add(String a, String b) {
        System.out.println("add(String, String)");
        return a + b;
    }
}

class ScientificCalculator extends Calculator {
    // ===== GHI ĐÈ (OVERRIDING): Cùng tên, CÙNG tham số, khác class =====
    @Override
    public int add(int a, int b) {
        System.out.println("ScientificCalculator.add(int, int)");
        int result = super.add(a, b); // Có thể gọi hàm cha
        System.out.println("(Đã ghi log kết quả: " + result + ")");
        return result;
    }

    // Phương thức MỚI chỉ có trong class con
    public double power(double base, double exp) {
        return Math.pow(base, exp);
    }
}

public class OverloadOverrideDemo {
    public static void main(String[] args) {
        Calculator calc = new Calculator();

        // Nạp chồng - Java tự chọn phương thức phù hợp dựa vào tham số
        System.out.println(calc.add(1, 2));          // add(int, int) → 3
        System.out.println(calc.add(1.5, 2.5));      // add(double, double) → 4.0
        System.out.println(calc.add(1, 2, 3));       // add(int, int, int) → 6
        System.out.println(calc.add("Hello", " World")); // add(String, String)

        System.out.println("\n--- Ghi đè ---");
        ScientificCalculator sci = new ScientificCalculator();
        sci.add(10, 20); // Gọi phiên bản override của ScientificCalculator
    }
}
```

| Tiêu chí | Nạp chồng (Overloading) | Ghi đè (Overriding) |
|---|---|---|
| **Vị trí** | Cùng class HOẶC class con | Class con ghi đè class cha |
| **Tên hàm** | Giống nhau | Giống nhau |
| **Tham số** | **Khác** (số lượng, kiểu, thứ tự) | **Giống hệt** |
| **Kiểu trả về** | Có thể khác | Phải giống (hoặc kiểu con) |
| **Thời điểm xác định** | Compile-time (static binding) | Runtime (dynamic binding) |
| **Annotation** | Không cần | `@Override` (nên dùng) |

---

## 9. Mảng đối tượng cùng implement 1 interface

```java
interface Taxable {
    double calculateTax();
    String getTaxInfo();
}

class Employee implements Taxable {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    @Override
    public double calculateTax() {
        return salary * 0.1; // Thuế 10% lương
    }

    @Override
    public String getTaxInfo() {
        return String.format("NV: %-15s | Lương: %10.0f | Thuế: %10.0f",
                name, salary, calculateTax());
    }
}

class FreelanceWorker implements Taxable {
    private String name;
    private double projectIncome;

    public FreelanceWorker(String name, double projectIncome) {
        this.name = name;
        this.projectIncome = projectIncome;
    }

    @Override
    public double calculateTax() {
        return projectIncome * 0.05; // Thuế 5%
    }

    @Override
    public String getTaxInfo() {
        return String.format("FL: %-15s | Thu nhập: %8.0f | Thuế: %10.0f",
                name, projectIncome, calculateTax());
    }
}

class Business implements Taxable {
    private String name;
    private double revenue;
    private double expenses;

    public Business(String name, double revenue, double expenses) {
        this.name = name;
        this.revenue = revenue;
        this.expenses = expenses;
    }

    @Override
    public double calculateTax() {
        double profit = revenue - expenses;
        return profit > 0 ? profit * 0.2 : 0; // Thuế 20% lợi nhuận
    }

    @Override
    public String getTaxInfo() {
        return String.format("DN: %-15s | Lợi nhuận: %6.0f | Thuế: %10.0f",
                name, (revenue - expenses), calculateTax());
    }
}

public class InterfaceArrayDemo {
    public static void main(String[] args) {
        // Mảng đối tượng KHÁC NHAU cùng implement 1 interface
        Taxable[] taxpayers = {
            new Employee("Nguyễn Dũng", 20_000_000),
            new Employee("Trần An", 15_000_000),
            new FreelanceWorker("Lê Hùng", 30_000_000),
            new Business("TechCorp", 500_000_000, 300_000_000),
            new FreelanceWorker("Phạm Mai", 10_000_000),
            new Business("SmallShop", 50_000_000, 60_000_000)
        };

        System.out.println("========= BÁO CÁO THUẾ =========");
        double totalTax = 0;
        for (Taxable t : taxpayers) {
            System.out.println(t.getTaxInfo());
            totalTax += t.calculateTax();
        }
        System.out.println("==================================");
        System.out.printf("TỔNG THUẾ THU ĐƯỢC: %,.0f VNĐ%n", totalTax);
    }
}
```

---

## 10. Sự khác nhau giữa Abstract và Interface

| Tiêu chí | Abstract Class | Interface |
|---|---|---|
| **Từ khóa** | `extends` | `implements` |
| **Số lượng kế thừa** | Chỉ extends **1** class | Implements **nhiều** interface |
| **Constructor** | ✅ Có | ❌ Không |
| **Thuộc tính** | Mọi loại (private, protected, public) | Chỉ `public static final` (hằng số) |
| **Phương thức** | Có cả abstract và bình thường | Mặc định abstract (Java 8+: có default, static) |
| **Mối quan hệ** | **IS-A** (Chó **là một** Động vật) | **CAN-DO** (Chó **có thể** Bơi) |
| **Khi nào dùng** | Các class có quan hệ **cha-con** tự nhiên | Các class **không liên quan** nhưng cùng khả năng |
| **Ví dụ** | `Animal` → Dog, Cat | `Swimmable` → Dog, Fish, Person |

```java
// Abstract: Quan hệ IS-A
abstract class Animal { }
class Dog extends Animal { }  // Dog IS-A Animal ✅

// Interface: Quan hệ CAN-DO
interface Swimmable { void swim(); }
interface Trainable { void train(); }

class Dog extends Animal implements Swimmable, Trainable {
    // Dog IS-A Animal
    // Dog CAN swim
    // Dog CAN be trained
    public void swim() { System.out.println("Chó bơi 🐕"); }
    public void train() { System.out.println("Chó được huấn luyện"); }
}

class Fish extends Animal implements Swimmable {
    // Fish IS-A Animal
    // Fish CAN swim
    // Fish CANNOT be trained
    public void swim() { System.out.println("Cá bơi 🐟"); }
}
```

---

## 11. Từ khóa static

```java
public class StaticDemo {

    // ===== 1. STATIC FIELD (Biến tĩnh) =====
    // Dùng CHUNG cho tất cả đối tượng, thuộc về CLASS (không thuộc đối tượng)
    static int instanceCount = 0;
    static final String COMPANY = "TechCorp"; // Hằng số

    // Instance field (mỗi đối tượng có riêng)
    String name;

    public StaticDemo(String name) {
        this.name = name;
        instanceCount++; // Mỗi lần tạo đối tượng → tăng biến dùng chung
    }

    // ===== 2. STATIC METHOD (Phương thức tĩnh) =====
    // Gọi qua TÊN CLASS, không cần tạo đối tượng
    // KHÔNG thể truy cập biến instance (vì không có đối tượng cụ thể)
    public static int getInstanceCount() {
        // System.out.println(name); // ❌ LỖI! Không truy cập instance field trong static method
        return instanceCount;
    }

    public static double celsiusToFahrenheit(double c) {
        return c * 9.0 / 5.0 + 32;
    }

    // ===== 3. STATIC BLOCK (Khối tĩnh) =====
    // Chạy MỘT LẦN khi class được load vào bộ nhớ
    static {
        System.out.println("⚡ Static block chạy khi class được load");
    }

    // ===== 4. STATIC INNER CLASS =====
    static class Helper {
        public static String formatName(String name) {
            return name.trim().toUpperCase();
        }
    }

    public static void main(String[] args) {
        // Gọi static method KHÔNG cần tạo đối tượng
        System.out.println("25°C = " + celsiusToFahrenheit(25) + "°F");

        // Static field dùng chung
        StaticDemo a = new StaticDemo("A");
        StaticDemo b = new StaticDemo("B");
        StaticDemo c = new StaticDemo("C");
        System.out.println("Đã tạo " + StaticDemo.getInstanceCount() + " đối tượng"); // 3

        // Static inner class
        System.out.println(StaticDemo.Helper.formatName("  hello  ")); // HELLO
    }
}
```

**Tóm tắt static:**

| Vị trí `static` | Ý nghĩa | Cách truy cập |
|---|---|---|
| `static` **field** | Biến dùng chung cho tất cả đối tượng | `ClassName.field` |
| `static` **method** | Hàm thuộc class, không cần đối tượng | `ClassName.method()` |
| `static` **block** | Chạy 1 lần khi class được load | Tự động |
| `static` **inner class** | Class lồng không cần đối tượng bao ngoài | `Outer.Inner` |

---

## 12. Access Modifier

```java
// File: AccessModifierDemo.java

class MyClass {
    public    String pubField  = "public";     // Truy cập MỌI NƠI
    protected String proField  = "protected";  // Cùng package + class con (kể cả khác package)
              String defField  = "default";    // Chỉ cùng package (package-private)
    private   String priField  = "private";    // Chỉ trong CHÍNH class này

    public    void pubMethod()  { System.out.println("public method"); }
    protected void proMethod()  { System.out.println("protected method"); }
              void defMethod()  { System.out.println("default method"); }
    private   void priMethod()  { System.out.println("private method"); }

    public void testInsideClass() {
        // Trong chính class → truy cập ĐƯỢC TẤT CẢ
        System.out.println(pubField);  // ✅
        System.out.println(proField);  // ✅
        System.out.println(defField);  // ✅
        System.out.println(priField);  // ✅
    }
}

// Class cùng package
class SamePackageClass {
    public void test() {
        MyClass obj = new MyClass();
        System.out.println(obj.pubField);  // ✅ public
        System.out.println(obj.proField);  // ✅ protected (cùng package)
        System.out.println(obj.defField);  // ✅ default (cùng package)
        // System.out.println(obj.priField); // ❌ private
    }
}

// Class con khác package
// class ChildDiffPackage extends MyClass {
//     void test() {
//         System.out.println(pubField);  // ✅ public
//         System.out.println(proField);  // ✅ protected (class con)
//         // System.out.println(defField); // ❌ default (khác package)
//         // System.out.println(priField); // ❌ private
//     }
// }
```

| Modifier | Cùng Class | Cùng Package | Class Con (khác Package) | Khác Package |
|---|---|---|---|---|
| `public` | ✅ | ✅ | ✅ | ✅ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `default` (không viết gì) | ✅ | ✅ | ❌ | ❌ |
| `private` | ✅ | ❌ | ❌ | ❌ |

```
Phạm vi: public > protected > default > private

Quy tắc ngón tay cái:
- Thuộc tính → private (đóng gói)
- Getter/Setter → public
- Method nội bộ → private
- Method cho class con → protected
- Method cho bên ngoài → public
```

---

## 13. Nạp chồng hàm - Các hàm cùng tên khác tham số

```java
public class OverloadingDemo {

    // Cùng tên "print", nhưng KHÁC tham số
    public static void print(String message) {
        System.out.println("[String] " + message);
    }

    public static void print(int number) {
        System.out.println("[int] " + number);
    }

    public static void print(double number) {
        System.out.println("[double] " + number);
    }

    public static void print(String message, int times) {
        for (int i = 0; i < times; i++) {
            System.out.println("[repeat " + (i + 1) + "] " + message);
        }
    }

    public static void print(int... numbers) {
        System.out.print("[varargs] ");
        for (int n : numbers) System.out.print(n + " ");
        System.out.println();
    }

    public static void main(String[] args) {
        print("Hello");           // [String] Hello
        print(42);                // [int] 42
        print(3.14);             // [double] 3.14
        print("Java", 3);       // [repeat 1] Java, [repeat 2] Java, [repeat 3] Java
        print(1, 2, 3, 4, 5);    // [varargs] 1 2 3 4 5
    }
}
```

---

## 14. Từ khóa final

```java
// ===== 1. final CLASS - Không thể kế thừa =====
final class ImmutablePoint {
    private final int x, y;

    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() { return x; }
    public int getY() { return y; }
}
// class ExtendedPoint extends ImmutablePoint {} // ❌ LỖI! Không thể extends final class

// ===== 2. final METHOD - Không thể ghi đè =====
class Base {
    public final void criticalMethod() {
        System.out.println("Phương thức quan trọng - KHÔNG được ghi đè!");
    }

    public void normalMethod() {
        System.out.println("Có thể ghi đè");
    }
}

class Child extends Base {
    // @Override
    // public void criticalMethod() {} // ❌ LỖI! Không thể override final method

    @Override
    public void normalMethod() {
        System.out.println("Đã ghi đè thành công");
    }
}

// ===== 3. final VARIABLE - Không thể gán lại =====
public class FinalDemo {
    // final field - phải gán giá trị (khi khai báo hoặc trong constructor)
    private final String name;
    private final int id;

    public FinalDemo(String name, int id) {
        this.name = name;  // Gán trong constructor → OK
        this.id = id;
    }

    public static void main(String[] args) {
        final int MAX = 100;
        // MAX = 200; // ❌ LỖI! Không thể gán lại final variable

        final int[] arr = {1, 2, 3};
        arr[0] = 99;         // ✅ OK - sửa NỘI DUNG mảng được
        // arr = new int[5]; // ❌ LỖI - không thể gán THAM CHIẾU mới

        // Ví dụ tổng hợp
        final double PI = 3.14159265;
        final String GREETING = "Hello";
        System.out.println("PI = " + PI);
        System.out.println("GREETING = " + GREETING);
    }
}
```

| Vị trí `final` | Ý nghĩa |
|---|---|
| `final` **class** | Class **không thể bị kế thừa** (VD: `String`, `Integer`) |
| `final` **method** | Method **không thể bị override** |
| `final` **variable** | Biến **không thể gán lại** (hằng số) |

---

## 15. Biến static, biến final, hằng số

```java
public class StaticFinalConst {
    // Biến static - dùng chung cho tất cả đối tượng
    static int count = 0;                // Có thể thay đổi

    // Biến final - gán 1 lần, không đổi
    final String name;                    // Mỗi đối tượng 1 giá trị khác nhau

    // HẰNG SỐ = static + final - dùng chung VÀ không đổi
    static final double PI = 3.14159265;
    static final int MAX_SIZE = 100;
    static final String APP_NAME = "MyApp";

    public StaticFinalConst(String name) {
        this.name = name;
        count++;
    }

    public static void main(String[] args) {
        StaticFinalConst a = new StaticFinalConst("A");
        StaticFinalConst b = new StaticFinalConst("B");

        System.out.println("count = " + StaticFinalConst.count);  // 2 (static: dùng chung)
        System.out.println("a.name = " + a.name);  // A (final: riêng mỗi đối tượng)
        System.out.println("b.name = " + b.name);  // B

        System.out.println("PI = " + PI);            // static final: hằng số
        System.out.println("MAX = " + MAX_SIZE);
    }
}
```

| Loại biến | `static` | `final` | Đặc điểm | Ví dụ |
|---|---|---|---|---|
| Biến thường | ❌ | ❌ | Mỗi đối tượng riêng, thay đổi được | `int age = 20;` |
| Biến static | ✅ | ❌ | Dùng chung, thay đổi được | `static int count = 0;` |
| Biến final | ❌ | ✅ | Riêng mỗi đối tượng, gán 1 lần | `final String name;` |
| **Hằng số** | ✅ | ✅ | Dùng chung, không đổi | `static final double PI = 3.14;` |

---

## 16. Toán tử instanceof

```java
class Animal { }
class Dog extends Animal { }
class Cat extends Animal { }

interface Swimmable { }
class Labrador extends Dog implements Swimmable { }

public class InstanceOfDemo {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        Animal myCat = new Cat();
        Animal myLab = new Labrador();

        // instanceof kiểm tra đối tượng có phải là instance của class/interface không
        System.out.println(myDog instanceof Dog);       // true
        System.out.println(myDog instanceof Animal);    // true  (Dog IS-A Animal)
        System.out.println(myDog instanceof Cat);       // false
        System.out.println(myLab instanceof Swimmable); // true  (Labrador implements Swimmable)
        System.out.println(myLab instanceof Dog);       // true  (Labrador extends Dog)
        System.out.println(null instanceof Animal);     // false (null luôn là false)

        // Ứng dụng: Ép kiểu an toàn
        Animal[] animals = {new Dog(), new Cat(), new Labrador()};
        for (Animal a : animals) {
            if (a instanceof Labrador lab) {        // Pattern matching (Java 16+)
                System.out.println("Labrador tìm thấy!");
            } else if (a instanceof Dog) {
                System.out.println("Đây là chó");
                Dog d = (Dog) a;  // Ép kiểu an toàn vì đã kiểm tra instanceof
            } else if (a instanceof Cat) {
                System.out.println("Đây là mèo");
            }
        }
    }
}
```

---

## 17. Các lớp Wrapper

```java
public class WrapperDemo {
    public static void main(String[] args) {
        // Wrapper = Bọc kiểu nguyên thủy thành ĐỐI TƯỢNG
        // int → Integer, double → Double, char → Character, boolean → Boolean...

        // ===== AUTOBOXING (tự động primitive → Wrapper) =====
        Integer num1 = 42;           // int → Integer (autoboxing)
        Double  num2 = 3.14;        // double → Double
        Boolean flag = true;         // boolean → Boolean
        Character ch = 'A';          // char → Character

        // ===== UNBOXING (tự động Wrapper → primitive) =====
        int x = num1;                // Integer → int (unboxing)
        double y = num2;             // Double → double

        // ===== TẠI SAO CẦN WRAPPER? =====
        // 1. Collection chỉ chứa Object, không chứa primitive
        java.util.List<Integer> list = new java.util.ArrayList<>();
        list.add(10);    // autoboxing: int 10 → Integer.valueOf(10)
        list.add(20);
        int sum = list.get(0) + list.get(1); // unboxing

        // 2. Có thể là null (primitive không thể null)
        Integer nullableAge = null;  // ✅ OK
        // int age = null;           // ❌ LỖI!

        // 3. Các hàm tiện ích
        System.out.println("Max int: " + Integer.MAX_VALUE);
        System.out.println("Parse: " + Integer.parseInt("123"));
        System.out.println("Hex: " + Integer.toHexString(255));
        System.out.println("Binary: " + Integer.toBinaryString(42));
        System.out.println("Compare: " + Integer.compare(5, 10)); // -1

        // ===== BẢNG WRAPPER =====
        // byte → Byte       | short → Short
        // int → Integer      | long → Long
        // float → Float      | double → Double
        // char → Character   | boolean → Boolean

        // ⚠️ CHÚ Ý: So sánh Wrapper phải dùng .equals()
        Integer a = 200, b = 200;
        System.out.println(a == b);       // false! (so sánh tham chiếu)
        System.out.println(a.equals(b));  // true   (so sánh giá trị)

        // Nhưng Integer cache từ -128 đến 127:
        Integer c = 100, d = 100;
        System.out.println(c == d);       // true! (cùng object trong cache)
    }
}
```

---

## 18. Chuyển đổi (cast) kiểu dữ liệu

```java
public class CastingDemo {
    public static void main(String[] args) {
        // ===== 1. WIDENING (Mở rộng - tự động, an toàn) =====
        // byte → short → int → long → float → double
        byte b = 42;
        int i = b;       // byte → int (tự động)
        long l = i;      // int → long (tự động)
        double d = l;    // long → double (tự động)
        System.out.println("Widening: byte " + b + " → double " + d);

        // ===== 2. NARROWING (Thu hẹp - thủ công, có thể mất dữ liệu) =====
        double pi = 3.99;
        int intPi = (int) pi;           // double → int (mất phần thập phân)
        System.out.println("Narrowing: " + pi + " → " + intPi); // 3 (cắt, không làm tròn!)

        long bigNum = 130;
        byte smallNum = (byte) bigNum;   // long → byte (tràn số!)
        System.out.println("Overflow: long " + bigNum + " → byte " + smallNum); // -126

        // ===== 3. ÉP KIỂU OBJECT (Upcasting / Downcasting) =====
        // Upcasting: class con → class cha (tự động, an toàn)
        Animal animal = new Dog();    // Dog → Animal (upcasting)
        animal.eat();                  // Gọi eat() của Dog (đa hình)
        // animal.bark();             // ❌ LỖI! Animal không có bark()

        // Downcasting: class cha → class con (thủ công, cần kiểm tra)
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal;    // Animal → Dog (downcasting)
            dog.bark();                // ✅ OK! Bây giờ gọi được bark()
        }

        // Ép kiểu giữa các primitive
        char c = 'A';
        int ascii = c;                // char → int: 65
        char fromInt = (char) 66;     // int → char: 'B'
        System.out.println("'A' = " + ascii + ", 66 = '" + fromInt + "'");
    }
}

class Animal { public void eat() { System.out.println("Eating..."); } }
class Dog extends Animal { public void bark() { System.out.println("Woof!"); } }
```

---

## 19. Parse giá trị từ String sang số

```java
public class ParseDemo {
    public static void main(String[] args) {
        // ===== STRING → SỐ =====
        int i    = Integer.parseInt("123");
        long l   = Long.parseLong("9999999999");
        float f  = Float.parseFloat("3.14");
        double d = Double.parseDouble("2.71828");
        byte b   = Byte.parseByte("100");
        short s  = Short.parseShort("30000");

        System.out.println("int:    " + i);    // 123
        System.out.println("long:   " + l);    // 9999999999
        System.out.println("float:  " + f);    // 3.14
        System.out.println("double: " + d);    // 2.71828

        // ===== SỐ → STRING =====
        String s1 = String.valueOf(42);
        String s2 = Integer.toString(42);
        String s3 = "" + 42;                  // Nối chuỗi (kém hiệu quả nhất)

        // ===== XỬ LÝ LỖI KHI PARSE =====
        try {
            int bad = Integer.parseInt("abc"); // NumberFormatException!
        } catch (NumberFormatException e) {
            System.out.println("❌ Không thể parse 'abc' → int: " + e.getMessage());
        }

        // Parse số với hệ cơ số
        int fromBin = Integer.parseInt("1010", 2);   // Binary → 10
        int fromHex = Integer.parseInt("FF", 16);     // Hex → 255
        System.out.println("1010 (bin) = " + fromBin);
        System.out.println("FF (hex) = " + fromHex);
    }
}
```

---

## 20. Danh sách liên kết (Linked List)

```java
// ===== TỰ TẠO CLASS DANH SÁCH LIÊN KẾT =====
class MyLinkedList {
    // Node: phần tử trong danh sách liên kết
    private static class Node {
        int data;
        Node next;

        Node(int data) {
            this.data = data;
            this.next = null;
        }
    }

    private Node head; // Phần tử đầu tiên
    private int size;

    public MyLinkedList() {
        this.head = null;
        this.size = 0;
    }

    // ===== THÊM PHẦN TỬ VÀO CUỐI =====
    public void add(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
        size++;
    }

    // ===== THÊM PHẦN TỬ VÀO ĐẦU =====
    public void addFirst(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
        size++;
    }

    // ===== XÓA PHẦN TỬ THEO GIÁ TRỊ =====
    public boolean remove(int data) {
        if (head == null) return false;

        // Xóa phần tử đầu
        if (head.data == data) {
            head = head.next;
            size--;
            return true;
        }

        // Xóa phần tử ở giữa/cuối
        Node current = head;
        while (current.next != null) {
            if (current.next.data == data) {
                current.next = current.next.next; // Bỏ qua node cần xóa
                size--;
                return true;
            }
            current = current.next;
        }
        return false; // Không tìm thấy
    }

    // ===== KIỂM TRA PHẦN TỬ CÓ TỒN TẠI =====
    public boolean contains(int data) {
        Node current = head;
        while (current != null) {
            if (current.data == data) return true;
            current = current.next;
        }
        return false;
    }

    // ===== KÍCH THƯỚC =====
    public int size() { return size; }

    // ===== IN DANH SÁCH =====
    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder("[");
        Node current = head;
        while (current != null) {
            sb.append(current.data);
            if (current.next != null) sb.append(" → ");
            current = current.next;
        }
        sb.append("]");
        return sb.toString();
    }
}

// ===== SỬ DỤNG =====
public class LinkedListDemo {
    public static void main(String[] args) {
        MyLinkedList list = new MyLinkedList();

        // Thêm phần tử
        list.add(10);
        list.add(20);
        list.add(30);
        list.addFirst(5);
        System.out.println("Sau khi thêm: " + list);
        // [5 → 10 → 20 → 30]

        // Kiểm tra tồn tại
        System.out.println("Có 20? " + list.contains(20));  // true
        System.out.println("Có 99? " + list.contains(99));  // false

        // Xóa phần tử
        list.remove(20);
        System.out.println("Sau xóa 20: " + list);  // [5 → 10 → 30]
        System.out.println("Size: " + list.size());   // 3
    }
}
```

```
Cấu trúc Linked List trong bộ nhớ:

head
  │
  ▼
┌───┬───┐    ┌───┬───┐    ┌───┬───┐    ┌───┬──────┐
│ 5 │ ──┼───►│10 │ ──┼───►│20 │ ──┼───►│30 │ null │
└───┴───┘    └───┴───┘    └───┴───┘    └───┴──────┘
 data next    data next    data next    data  next

Xóa phần tử 20:
  Trước: 10.next → [20] → 30
  Sau:   10.next → 30  (bỏ qua 20, GC thu hồi)
```

---

## 21. So sánh DSLK và Mảng truyền thống

| Tiêu chí | Mảng (Array) | Danh sách liên kết (Linked List) |
|---|---|---|
| **Kích thước** | **Cố định** khi khởi tạo | **Linh hoạt**, thêm/xóa tự do |
| **Bộ nhớ** | Liên tiếp (contiguous) | Rời rạc (scattered) |
| **Truy cập phần tử** | **O(1)** - trực tiếp qua index | **O(n)** - phải duyệt từ đầu |
| **Thêm/Xóa đầu** | **O(n)** - phải dịch chuyển | **O(1)** - chỉ đổi con trỏ |
| **Thêm/Xóa cuối** | **O(1)** (nếu còn chỗ) | **O(n)** (phải duyệt đến cuối) |
| **Thêm/Xóa giữa** | **O(n)** - phải dịch chuyển | **O(1)** (nếu đã có vị trí) |
| **Bộ nhớ phụ** | Không tốn thêm | Tốn thêm cho con trỏ `next` |
| **Cache friendly** | ✅ Tốt (bộ nhớ liên tiếp) | ❌ Kém (bộ nhớ rời rạc) |
| **Khi nào dùng** | Biết trước kích thước, truy cập ngẫu nhiên nhiều | Thêm/xóa nhiều, kích thước thay đổi |

---

## 22. Khai báo chuỗi, cắt chuỗi, nối chuỗi

```java
public class StringDemo {
    public static void main(String[] args) {
        // ===== KHAI BÁO =====
        String s1 = "Hello World";                // String literal (String pool)
        String s2 = new String("Hello World");    // new object (Heap)
        String s3 = "Hello" + " " + "World";     // Nối chuỗi

        // ===== CẮT CHUỖI =====
        String text = "Java Programming Language";

        // substring(beginIndex) - từ vị trí đến hết
        System.out.println(text.substring(5));       // "Programming Language"

        // substring(beginIndex, endIndex) - từ vị trí đến trước endIndex
        System.out.println(text.substring(5, 16));   // "Programming"

        // charAt(index) - lấy ký tự tại vị trí
        System.out.println(text.charAt(0));           // 'J'

        // split(regex) - tách chuỗi
        String csv = "Dũng,22,CNTT,9.5";
        String[] parts = csv.split(",");
        // parts = ["Dũng", "22", "CNTT", "9.5"]

        // trim() - xóa khoảng trắng đầu cuối
        String padded = "  Hello  ";
        System.out.println(padded.trim());            // "Hello"

        // ===== NỐI CHUỖI =====
        // Cách 1: Toán tử +
        String full = "Hello" + " " + "World";

        // Cách 2: concat()
        String joined = "Hello".concat(" World");

        // Cách 3: String.format()
        String formatted = String.format("%s có %d tuổi, GPA: %.1f", "Dũng", 22, 8.5);

        // Cách 4: String.join() (Java 8+)
        String result = String.join(", ", "Java", "Python", "C++");
        // "Java, Python, C++"

        // ===== CÁC HÀM HỮU ÍCH =====
        System.out.println("Hello".length());             // 5
        System.out.println("Hello".toUpperCase());        // "HELLO"
        System.out.println("HELLO".toLowerCase());        // "hello"
        System.out.println("Hello".contains("ell"));      // true
        System.out.println("Hello".startsWith("He"));     // true
        System.out.println("Hello".endsWith("lo"));       // true
        System.out.println("Hello".indexOf("l"));         // 2 (vị trí đầu tiên)
        System.out.println("Hello".lastIndexOf("l"));     // 3
        System.out.println("Hello".replace("l", "L"));    // "HeLLo"
        System.out.println("Hello".equals("hello"));      // false
        System.out.println("Hello".equalsIgnoreCase("hello")); // true
        System.out.println("  Hi  ".strip());             // "Hi" (Java 11+)
        System.out.println("Hello".isEmpty());            // false
        System.out.println("Hello".isBlank());            // false (Java 11+)
    }
}
```

---

## 23. StringBuilder và StringTokenizer

```java
import java.util.StringTokenizer;

public class StringBuilderTokenizerDemo {
    public static void main(String[] args) {
        // ===== STRINGBUILDER =====
        // String là IMMUTABLE (bất biến) - mỗi lần sửa = tạo object mới
        // StringBuilder là MUTABLE (thay đổi được) - sửa trực tiếp

        StringBuilder sb = new StringBuilder();

        // Thêm vào cuối
        sb.append("Hello");
        sb.append(" ");
        sb.append("World");
        System.out.println(sb);  // "Hello World"

        // Chèn vào vị trí
        sb.insert(5, " Beautiful");
        System.out.println(sb);  // "Hello Beautiful World"

        // Xóa
        sb.delete(5, 15);  // Xóa từ index 5 đến 14
        System.out.println(sb);  // "Hello World"

        // Thay thế
        sb.replace(6, 11, "Java");
        System.out.println(sb);  // "Hello Java"

        // Đảo ngược
        sb.reverse();
        System.out.println(sb);  // "avaJ olleH"

        sb.reverse(); // Đảo lại

        // Chuyển thành String
        String result = sb.toString();

        // Method chaining
        String chain = new StringBuilder()
                .append("Tên: ").append("Dũng")
                .append(", Tuổi: ").append(22)
                .append(", GPA: ").append(8.5)
                .toString();
        System.out.println(chain);

        // ===== STRINGTOKENIZER =====
        // Tách chuỗi theo delimiter (tương tự split nhưng cũ hơn)
        String data = "Nguyễn Dũng;22;CNTT;Hà Nội";
        StringTokenizer st = new StringTokenizer(data, ";");

        System.out.println("\n===== StringTokenizer =====");
        System.out.println("Số token: " + st.countTokens()); // 4

        while (st.hasMoreTokens()) {
            System.out.println("Token: " + st.nextToken());
        }
        // Token: Nguyễn Dũng
        // Token: 22
        // Token: CNTT
        // Token: Hà Nội

        // Nhiều delimiter
        String mixed = "apple,banana;cherry:date";
        StringTokenizer st2 = new StringTokenizer(mixed, ",;:");
        while (st2.hasMoreTokens()) {
            System.out.println(st2.nextToken());
        }
    }
}
```

---

## 24. So sánh cộng String và StringBuilder

```java
public class StringVsBuilderPerf {
    public static void main(String[] args) {
        int iterations = 100_000;

        // ===== STRING CONCATENATION (CHẬM) =====
        long start = System.currentTimeMillis();
        String s = "";
        for (int i = 0; i < iterations; i++) {
            s += "a"; // Mỗi lần tạo ĐỐI TƯỢNG MỚI trên heap!
        }
        long timeString = System.currentTimeMillis() - start;

        // ===== STRINGBUILDER (NHANH) =====
        start = System.currentTimeMillis();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < iterations; i++) {
            sb.append("a"); // Sửa trực tiếp buffer bên trong
        }
        String result = sb.toString();
        long timeBuilder = System.currentTimeMillis() - start;

        System.out.printf("String +:      %d ms%n", timeString);    // ~3000-5000 ms
        System.out.printf("StringBuilder: %d ms%n", timeBuilder);   // ~2-5 ms
        System.out.printf("Nhanh hơn: ~%dx%n", timeString / Math.max(timeBuilder, 1));
    }
}
```

```
Tại sao String + chậm?

Mỗi lần s += "a":
  Lần 1: s = "" + "a"         → tạo mới "a" (1 object)
  Lần 2: s = "a" + "a"        → tạo mới "aa" (1 object, "a" cũ bị bỏ)
  Lần 3: s = "aa" + "a"       → tạo mới "aaa" (1 object, "aa" bị bỏ)
  ...
  → 100,000 vòng = tạo 100,000 đối tượng String trên Heap → rất chậm!

StringBuilder sửa trực tiếp buffer:
  sb.append("a") → Thêm 'a' vào mảng char[] bên trong
  → Chỉ 1 object từ đầu đến cuối → rất nhanh!
```

| Tiêu chí | String + | StringBuilder |
|---|---|---|
| **Tốc độ** | ❌ Chậm (tạo object mới mỗi lần) | ✅ Nhanh (sửa trực tiếp) |
| **Bộ nhớ** | ❌ Tốn (nhiều object tạm) | ✅ Tiết kiệm |
| **Thread-safe** | ✅ (immutable) | ❌ (dùng `StringBuffer` nếu cần thread-safe) |
| **Dùng khi** | Nối ít chuỗi, code đơn giản | Nối nhiều chuỗi, trong vòng lặp |

---

## 25. Nạp chồng toString

```java
class Employee {
    private int id;
    private String name;
    private String department;
    private double salary;

    public Employee(int id, String name, String department, double salary) {
        this.id = id;
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    // KHÔNG override toString() → in ra: Employee@1b6d3586 (địa chỉ hash)

    // GHI ĐÈ toString() → in ra thông tin dễ đọc
    @Override
    public String toString() {
        return String.format("Employee{id=%d, name='%s', dept='%s', salary=$%,.2f}",
                id, name, department, salary);
    }
}

public class ToStringDemo {
    public static void main(String[] args) {
        Employee emp = new Employee(1, "Nguyễn Dũng", "IT", 25_000_000);

        // toString() được gọi tự động khi:
        System.out.println(emp);                // 1. In đối tượng
        String info = "Nhân viên: " + emp;      // 2. Nối chuỗi
        System.out.println(info);

        // Mảng đối tượng
        Employee[] team = {
            new Employee(1, "Dũng", "IT", 25_000_000),
            new Employee(2, "An", "HR", 20_000_000),
            new Employee(3, "Bình", "Sales", 22_000_000)
        };
        for (Employee e : team) {
            System.out.println(e); // Tự gọi toString()
        }
    }
}
```

---

## 26. Hashing

### 26.1 Hashing là gì?

**Hashing** là quá trình biến đổi dữ liệu đầu vào (có kích thước **bất kỳ**) thành một giá trị đầu ra có kích thước **cố định** (gọi là **hash value** hoặc **digest**).

```
Đầu vào (bất kỳ kích thước)              Hàm Hash          Đầu ra (kích thước cố định)
─────────────────────────                 ────────           ──────────────────────────
"Hello"                        ──────►   hash()   ────────► 0x5D41402A (32 bit)
"Hello World, xin chào!"      ──────►   hash()   ────────► 0xA3B2C1D4 (32 bit)
(File 10GB)                    ──────►   hash()   ────────► 0x7E8F9A0B (32 bit)
```

### 26.2 Các phương pháp và thuật toán hashing phổ biến

| Thuật toán | Kích thước output | Tốc độ | Bảo mật | Dùng cho |
|---|---|---|---|---|
| **Division** (chia dư) | Tùy chọn | Rất nhanh | ❌ | Hash table |
| **Multiplication** | Tùy chọn | Nhanh | ❌ | Hash table |
| **MD5** | 128 bit (32 hex) | Nhanh | ❌ Đã bị phá | Checksum file (không dùng cho mật khẩu) |
| **SHA-1** | 160 bit (40 hex) | Nhanh | ❌ Đã bị phá | Git commit hash |
| **SHA-256** | 256 bit (64 hex) | Trung bình | ✅ An toàn | Blockchain, chữ ký số |
| **CRC32** | 32 bit | Rất nhanh | ❌ | Kiểm tra lỗi truyền dữ liệu |
| **BCrypt** | 60 chars | Chậm (cố ý) | ✅ Rất an toàn | Hash mật khẩu |

---

## 27. Tự tạo hàm hashing 3 số nguyên

```java
public class CustomHashDemo {
    // ===== TỰ TẠO HÀM HASH 3 SỐ NGUYÊN → 1 SỐ NGUYÊN =====

    // Cách 1: Phương pháp chia dư (Division method)
    public static int hashDivision(int a, int b, int c) {
        int combined = a * 31 * 31 + b * 31 + c;
        return Math.abs(combined % 1000); // Hash value trong khoảng 0-999
    }

    // Cách 2: Phương pháp nhân (Multiplication method - Knuth)
    public static int hashMultiplication(int a, int b, int c) {
        double A = 0.6180339887; // (√5 - 1) / 2 (tỷ lệ vàng)
        int combined = a * 31 * 31 + b * 31 + c;
        double frac = (combined * A) - Math.floor(combined * A); // Phần thập phân
        return (int) (frac * 1000); // Hash value trong khoảng 0-999
    }

    // Cách 3: XOR + shift (phổ biến trong thực tế)
    public static int hashXOR(int a, int b, int c) {
        int hash = 17;
        hash = hash * 31 + a;
        hash = hash * 31 + b;
        hash = hash * 31 + c;
        return Math.abs(hash);
    }

    public static void main(String[] args) {
        int a = 10, b = 20, c = 30;

        System.out.printf("hash(%d, %d, %d):%n", a, b, c);
        System.out.println("  Division:       " + hashDivision(a, b, c));
        System.out.println("  Multiplication: " + hashMultiplication(a, b, c));
        System.out.println("  XOR:            " + hashXOR(a, b, c));

        // Kiểm tra: cùng input → cùng output
        System.out.println("\nCùng input → cùng hash?");
        System.out.println("  " + hashXOR(10, 20, 30) == hashXOR(10, 20, 30)); // true

        // Khác input → (thường) khác output
        System.out.println("Khác input → khác hash?");
        System.out.println("  hash(10,20,30) = " + hashXOR(10, 20, 30));
        System.out.println("  hash(30,20,10) = " + hashXOR(30, 20, 10));
    }
}
```

---

## 28. Sử dụng MD5 / CRC32 để hash chuỗi

```java
import java.security.MessageDigest;
import java.util.zip.CRC32;

public class HashAlgorithmDemo {
    // ===== MD5 HASH =====
    public static String md5Hash(String input) throws Exception {
        MessageDigest md = MessageDigest.getInstance("MD5");
        byte[] hashBytes = md.digest(input.getBytes("UTF-8"));

        // Chuyển byte[] thành hex string
        StringBuilder sb = new StringBuilder();
        for (byte b : hashBytes) {
            sb.append(String.format("%02x", b));
        }
        return sb.toString();
    }

    // ===== CRC32 HASH =====
    public static long crc32Hash(String input) {
        CRC32 crc = new CRC32();
        crc.update(input.getBytes());
        return crc.getValue();
    }

    // ===== SHA-256 HASH =====
    public static String sha256Hash(String input) throws Exception {
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        byte[] hashBytes = md.digest(input.getBytes("UTF-8"));

        StringBuilder sb = new StringBuilder();
        for (byte b : hashBytes) {
            sb.append(String.format("%02x", b));
        }
        return sb.toString();
    }

    public static void main(String[] args) throws Exception {
        String text = "Hello World";

        System.out.println("Input: \"" + text + "\"");
        System.out.println("MD5:    " + md5Hash(text));
        System.out.println("CRC32:  " + crc32Hash(text));
        System.out.println("SHA256: " + sha256Hash(text));

        // Cùng input → cùng hash
        System.out.println("\nCùng input → cùng hash:");
        System.out.println("MD5(\"Hello World\") = " + md5Hash("Hello World"));
        System.out.println("MD5(\"Hello World\") = " + md5Hash("Hello World")); // Giống!

        // Khác 1 ký tự → hash hoàn toàn khác (Avalanche effect)
        System.out.println("\nAvalanche effect:");
        System.out.println("MD5(\"Hello World\")  = " + md5Hash("Hello World"));
        System.out.println("MD5(\"Hello World!\") = " + md5Hash("Hello World!"));
    }
}
```

---

## 29. Hashing để ẩn password

```java
import java.security.MessageDigest;
import java.security.SecureRandom;
import java.util.Base64;
import java.util.HashMap;
import java.util.Map;

public class PasswordHashDemo {
    // ===== Sinh salt ngẫu nhiên =====
    private static byte[] generateSalt() {
        SecureRandom random = new SecureRandom();
        byte[] salt = new byte[16];
        random.nextBytes(salt);
        return salt;
    }

    // ===== Hash password với salt =====
    private static String hashPassword(String password, byte[] salt) throws Exception {
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        md.update(salt);
        byte[] hashedBytes = md.digest(password.getBytes("UTF-8"));

        // Lưu cả salt + hash
        byte[] combined = new byte[salt.length + hashedBytes.length];
        System.arraycopy(salt, 0, combined, 0, salt.length);
        System.arraycopy(hashedBytes, 0, combined, salt.length, hashedBytes.length);

        return Base64.getEncoder().encodeToString(combined);
    }

    // ===== Kiểm tra password =====
    private static boolean verifyPassword(String inputPassword, String storedHash)
            throws Exception {
        byte[] combined = Base64.getDecoder().decode(storedHash);

        // Tách salt (16 bytes đầu)
        byte[] salt = new byte[16];
        System.arraycopy(combined, 0, salt, 0, 16);

        // Hash input password với cùng salt
        String inputHash = hashPassword(inputPassword, salt);

        return storedHash.equals(inputHash);
    }

    public static void main(String[] args) throws Exception {
        // Mô phỏng đăng ký
        String password = "MySecretPass123";
        byte[] salt = generateSalt();
        String hashedPassword = hashPassword(password, salt);

        System.out.println("Password gốc:  " + password);
        System.out.println("Password hash:  " + hashedPassword);
        System.out.println("(Lưu hash vào DB, KHÔNG lưu password gốc!)");

        // Mô phỏng đăng nhập
        System.out.println("\n--- Kiểm tra đăng nhập ---");
        System.out.println("Đúng pass:  " + verifyPassword("MySecretPass123", hashedPassword)); // true
        System.out.println("Sai pass:   " + verifyPassword("WrongPassword", hashedPassword));   // false
    }
}
```

```
Quy trình hash password:

ĐĂNG KÝ:
  1. User nhập: "MySecretPass123"
  2. Sinh salt ngẫu nhiên: "x7k9m2..."
  3. Hash: SHA256("x7k9m2..." + "MySecretPass123") = "a3b2c1..."
  4. Lưu DB: salt + hash = "x7k9m2...a3b2c1..."
  ❌ KHÔNG lưu "MySecretPass123" vào DB!

ĐĂNG NHẬP:
  1. User nhập: "MySecretPass123"
  2. Lấy salt từ DB: "x7k9m2..."
  3. Hash lại: SHA256("x7k9m2..." + "MySecretPass123") = "a3b2c1..."
  4. So sánh với hash trong DB → ✅ TRÙNG → Đăng nhập thành công!
```

---

## 30. Hashtable và bảng băm

```java
public class HashTableDemo {

    // ===== TỰ XÂY DỰNG HASH TABLE ĐƠN GIẢN =====
    static class MyHashTable {
        private static class Entry {
            String key;
            String value;
            Entry next; // Xử lý va chạm bằng chaining

            Entry(String key, String value) {
                this.key = key;
                this.value = value;
            }
        }

        private Entry[] buckets;
        private int size;
        private int capacity;

        public MyHashTable(int capacity) {
            this.capacity = capacity;
            this.buckets = new Entry[capacity];
            this.size = 0;
        }

        // Hàm hash: key → index
        private int hash(String key) {
            return Math.abs(key.hashCode() % capacity);
        }

        // Thêm / cập nhật
        public void put(String key, String value) {
            int index = hash(key);
            Entry current = buckets[index];

            // Kiểm tra key đã tồn tại chưa
            while (current != null) {
                if (current.key.equals(key)) {
                    current.value = value; // Cập nhật
                    return;
                }
                current = current.next;
            }

            // Thêm mới vào đầu danh sách (chaining)
            Entry newEntry = new Entry(key, value);
            newEntry.next = buckets[index];
            buckets[index] = newEntry;
            size++;
        }

        // Tìm kiếm
        public String get(String key) {
            int index = hash(key);
            Entry current = buckets[index];

            while (current != null) {
                if (current.key.equals(key)) {
                    return current.value;
                }
                current = current.next;
            }
            return null; // Không tìm thấy
        }

        // In bảng băm
        public void display() {
            for (int i = 0; i < capacity; i++) {
                System.out.printf("Bucket[%d]: ", i);
                Entry current = buckets[i];
                while (current != null) {
                    System.out.printf("(%s=%s) → ", current.key, current.value);
                    current = current.next;
                }
                System.out.println("null");
            }
        }
    }

    public static void main(String[] args) {
        MyHashTable ht = new MyHashTable(7);

        ht.put("name", "Dũng");
        ht.put("age", "22");
        ht.put("city", "Hà Nội");
        ht.put("major", "CNTT");
        ht.put("gpa", "8.5");

        System.out.println("===== Cấu trúc bảng băm =====");
        ht.display();

        System.out.println("\n===== Tìm kiếm =====");
        System.out.println("name = " + ht.get("name"));   // Dũng
        System.out.println("age = " + ht.get("age"));     // 22
        System.out.println("phone = " + ht.get("phone")); // null
    }
}
```

```
Cấu trúc Hash Table:

hash("name") = 3    hash("age") = 5    hash("city") = 3 (va chạm!)

Bucket[0]: null
Bucket[1]: null
Bucket[2]: (gpa=8.5) → null
Bucket[3]: (city=Hà Nội) → (name=Dũng) → null    ← Chaining (xử lý va chạm)
Bucket[4]: (major=CNTT) → null
Bucket[5]: (age=22) → null
Bucket[6]: null

Tìm kiếm "name":
  1. hash("name") = 3
  2. Đến Bucket[3]
  3. Duyệt: city ≠ name → name == name → TÌM THẤY! → "Dũng"

→ Tìm kiếm trung bình O(1), xấu nhất O(n) (tất cả va chạm cùng bucket)
```

---

## 31. Ghi đè hashCode và equals

### 31.1 Tại sao phải ghi đè CẢ HAI?

```java
import java.util.HashSet;
import java.util.Objects;

class Student {
    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // ===== GHI ĐÈ equals() =====
    // Quy tắc: Hai đối tượng "bằng nhau" nếu có cùng id
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;              // Cùng tham chiếu → bằng
        if (obj == null) return false;              // null → không bằng
        if (getClass() != obj.getClass()) return false; // Khác class → không bằng

        Student other = (Student) obj;
        return this.id == other.id &&
               Objects.equals(this.name, other.name);
    }

    // ===== GHI ĐÈ hashCode() =====
    // QUY TẮC BẮT BUỘC: Nếu a.equals(b) == true → a.hashCode() == b.hashCode()
    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }

    @Override
    public String toString() {
        return "Student{id=" + id + ", name='" + name + "'}";
    }
}

public class HashCodeEqualsDemo {
    public static void main(String[] args) {
        Student s1 = new Student(1, "Dũng");
        Student s2 = new Student(1, "Dũng"); // Cùng dữ liệu với s1
        Student s3 = new Student(2, "An");

        // equals()
        System.out.println("s1.equals(s2): " + s1.equals(s2)); // true
        System.out.println("s1.equals(s3): " + s1.equals(s3)); // false

        // hashCode()
        System.out.println("s1.hashCode(): " + s1.hashCode());
        System.out.println("s2.hashCode(): " + s2.hashCode()); // Giống s1
        System.out.println("s3.hashCode(): " + s3.hashCode()); // Khác

        // ===== TẠI SAO PHẢI GHI ĐÈ CẢ HAI? =====
        HashSet<Student> set = new HashSet<>();
        set.add(s1);
        set.add(s2); // s2 equals s1 → KHÔNG thêm vào (đúng!)

        System.out.println("\nHashSet size: " + set.size()); // 1 (không trùng)
        System.out.println("Có s2? " + set.contains(s2));    // true

        // Nếu KHÔNG ghi đè hashCode():
        // → s1 và s2 có hashCode khác nhau (mặc định theo địa chỉ bộ nhớ)
        // → HashSet đặt chúng vào KHÁC bucket
        // → set.contains(s2) trả về false (SAI!)
        // → set.size() = 2 (có 2 "Dũng" trùng nhau - SAI!)
    }
}
```

### 31.2 Hợp đồng giữa equals và hashCode

```
QUY TẮC BẮT BUỘC (Contract):

1. Nếu a.equals(b) == true  → a.hashCode() == b.hashCode()  (BẮT BUỘC)
2. Nếu a.hashCode() == b.hashCode() → a.equals(b) CÓ THỂ true hoặc false
                                       (hash có thể va chạm)
3. Nếu a.equals(b) == false → hashCode có thể giống hoặc khác

Vi phạm quy tắc 1 → HashSet, HashMap, HashTable hoạt động SAI!
```

```
HashSet tìm kiếm đối tượng:

1. Tính hashCode() → xác định bucket
2. Trong bucket, dùng equals() để so sánh từng phần tử

     hashCode()           equals()
  ┌─────────────┐     ┌──────────────┐
  │ Xác định    │────►│ So sánh chính│
  │ bucket nào  │     │ xác trong    │
  │ (nhanh)     │     │ bucket (chậm)│
  └─────────────┘     └──────────────┘

→ Phải ghi đè CẢ HAI để đảm bảo hoạt động đúng!
```

---

> **📌 Kết thúc Phần 3: Lập Trình Hướng Đối Tượng (OOP)**
>
> Phần tiếp theo: [Phần 4: Xử Lý Ngoại Lệ](#phần-4-xử-lý-ngoại-lệ) *(sẽ được bổ sung)*
