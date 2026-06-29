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

---

# Phần 4: Xử Lý Ngoại Lệ (Exception Handling)

## 📌 Mục lục

1. [Ngoại lệ là gì](#1-ngoại-lệ-là-gì)
2. [Cấu trúc bắt ngoại lệ (try-catch)](#2-cấu-trúc-bắt-ngoại-lệ-try-catch)
3. [Khối finally](#3-khối-finally)
4. [Từ khóa throw và throws](#4-từ-khóa-throw-và-throws)
5. [Tạo ngoại lệ riêng (Custom Exception)](#5-tạo-ngoại-lệ-riêng-custom-exception)

---

## 1. Ngoại lệ là gì

### 1.1 Định nghĩa

**Ngoại lệ (Exception)** là một sự kiện **bất thường** xảy ra trong quá trình chạy chương trình, làm **gián đoạn** luồng thực thi bình thường. Nếu không được xử lý, chương trình sẽ **crash** (dừng đột ngột).

```
Chương trình bình thường:
  Lệnh 1 → Lệnh 2 → Lệnh 3 → Lệnh 4 → Kết thúc ✅

Chương trình có ngoại lệ (KHÔNG xử lý):
  Lệnh 1 → Lệnh 2 → 💥 EXCEPTION → CRASH! ❌
                     (chia cho 0)    (Lệnh 3, 4 KHÔNG chạy)

Chương trình có ngoại lệ (CÓ xử lý):
  Lệnh 1 → Lệnh 2 → 💥 EXCEPTION → [catch xử lý] → Lệnh 4 → Kết thúc ✅
                                      (thông báo lỗi)
```

### 1.2 Các loại ngoại lệ thường gặp

```java
public class CommonExceptionsDemo {
    public static void main(String[] args) {
        // 1. ArithmeticException - Chia cho 0
        // int result = 10 / 0; // 💥 ArithmeticException: / by zero

        // 2. NullPointerException - Gọi method trên null
        // String str = null;
        // str.length(); // 💥 NullPointerException

        // 3. ArrayIndexOutOfBoundsException - Truy cập index ngoài phạm vi
        // int[] arr = {1, 2, 3};
        // int x = arr[5]; // 💥 ArrayIndexOutOfBoundsException

        // 4. NumberFormatException - Parse chuỗi sai định dạng
        // int num = Integer.parseInt("abc"); // 💥 NumberFormatException

        // 5. ClassCastException - Ép kiểu sai
        // Object obj = "Hello";
        // Integer num = (Integer) obj; // 💥 ClassCastException

        // 6. StackOverflowError - Đệ quy không có điều kiện dừng
        // recursiveForever(); // 💥 StackOverflowError

        // 7. FileNotFoundException - File không tồn tại
        // FileReader fr = new FileReader("khong_co.txt"); // 💥 FileNotFoundException

        // 8. StringIndexOutOfBoundsException
        // "Hi".charAt(99); // 💥 StringIndexOutOfBoundsException
    }
}
```

### 1.3 Cây phân cấp Exception trong Java

```
                        java.lang.Object
                              │
                      java.lang.Throwable ← Tổ tiên của mọi lỗi/ngoại lệ
                         ╱           ╲
                        ╱             ╲
               java.lang.Error    java.lang.Exception
               (Lỗi nghiêm trọng)  (Ngoại lệ xử lý được)
                     │                      │
               ┌─────┤              ┌───────┼──────────────┐
               │     │              │       │              │
          StackOver  OutOf     IOException  SQL        RuntimeException
          flowError  MemoryErr             Exception   (Unchecked)
                                    │                      │
                              ┌─────┤              ┌───────┼──────────┐
                              │     │              │       │          │
                         FileNot  IO          NullPointer Arithmetic ArrayIndex
                         Found   Exception   Exception   Exception  OutOfBounds
                         Exception                                  Exception
```

### 1.4 Checked vs Unchecked Exception

| Tiêu chí | Checked Exception | Unchecked Exception |
|---|---|---|
| **Kế thừa từ** | `Exception` (trừ RuntimeException) | `RuntimeException` |
| **Kiểm tra khi** | **Compile-time** (biên dịch) | **Runtime** (chạy) |
| **Bắt buộc xử lý?** | ✅ Phải try-catch hoặc throws | ❌ Không bắt buộc |
| **Ví dụ** | `IOException`, `SQLException`, `FileNotFoundException` | `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException` |
| **Nguyên nhân** | Lỗi bên ngoài (file, mạng, DB) | Lỗi lập trình (bug trong code) |
| **Phòng tránh** | Không thể phòng tránh hoàn toàn | Có thể phòng tránh bằng code tốt |

```java
import java.io.*;

public class CheckedVsUncheckedDemo {
    // ===== CHECKED EXCEPTION - Compiler BẮT BUỘC xử lý =====
    public static void readFile() {
        // FileReader ném FileNotFoundException (checked)
        // → Compiler yêu cầu PHẢI try-catch hoặc throws

        // ❌ Không xử lý → LỖI BIÊN DỊCH!
        // FileReader fr = new FileReader("test.txt");

        // ✅ Cách 1: try-catch
        try {
            FileReader fr = new FileReader("test.txt");
            System.out.println("Đọc file thành công");
        } catch (FileNotFoundException e) {
            System.out.println("File không tồn tại: " + e.getMessage());
        }
    }

    // ✅ Cách 2: throws (đẩy trách nhiệm cho hàm gọi)
    public static void readFile2() throws FileNotFoundException {
        FileReader fr = new FileReader("test.txt");
    }

    // ===== UNCHECKED EXCEPTION - Compiler KHÔNG bắt buộc =====
    public static void divide(int a, int b) {
        // ArithmeticException (unchecked) - không bắt buộc try-catch
        // Nhưng NÊN kiểm tra để tránh lỗi
        if (b == 0) {
            System.out.println("❌ Không thể chia cho 0");
            return;
        }
        System.out.println(a + " / " + b + " = " + (a / b));
    }

    public static void main(String[] args) {
        readFile();
        divide(10, 0);
        divide(10, 3);
    }
}
```

---

## 2. Cấu trúc bắt ngoại lệ (try-catch)

### 2.1 Cú pháp cơ bản

```java
public class TryCatchDemo {
    public static void main(String[] args) {
        // ===== 1. TRY-CATCH CƠ BẢN =====
        System.out.println("===== 1. try-catch cơ bản =====");
        try {
            // Khối TRY: chứa code có thể gây ngoại lệ
            int result = 10 / 0;  // 💥 ArithmeticException
            System.out.println("Kết quả: " + result);  // ← KHÔNG chạy đến đây
        } catch (ArithmeticException e) {
            // Khối CATCH: xử lý ngoại lệ
            System.out.println("❌ Lỗi chia cho 0: " + e.getMessage());
            // getMessage() → "/ by zero"
        }
        System.out.println("Chương trình vẫn tiếp tục...\n");  // ← VẪN chạy!

        // ===== 2. NHIỀU KHỐI CATCH (bắt nhiều loại ngoại lệ) =====
        System.out.println("===== 2. Nhiều catch =====");
        try {
            String str = null;
            // int num = Integer.parseInt("abc");  // NumberFormatException
            System.out.println(str.length());      // NullPointerException
        } catch (NumberFormatException e) {
            System.out.println("❌ Lỗi parse số: " + e.getMessage());
        } catch (NullPointerException e) {
            System.out.println("❌ Lỗi null: " + e.getMessage());
        } catch (Exception e) {
            // Catch chung - bắt TẤT CẢ ngoại lệ còn lại
            // ⚠️ PHẢI đặt CUỐI CÙNG (từ cụ thể → chung)
            System.out.println("❌ Lỗi khác: " + e.getMessage());
        }

        // ===== 3. MULTI-CATCH (Java 7+) - Gộp nhiều exception =====
        System.out.println("\n===== 3. Multi-catch =====");
        try {
            int[] arr = {1, 2, 3};
            arr[10] = 99;  // ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException | NullPointerException e) {
            // Bắt 2 loại exception bằng 1 catch
            System.out.println("❌ Lỗi mảng hoặc null: " + e.getMessage());
        }

        // ===== 4. THÔNG TIN CHI TIẾT VỀ EXCEPTION =====
        System.out.println("\n===== 4. Thông tin exception =====");
        try {
            int[] arr = {1, 2, 3};
            System.out.println(arr[5]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("getMessage():  " + e.getMessage());
            // → "Index 5 out of bounds for length 3"

            System.out.println("getClass():    " + e.getClass().getName());
            // → "java.lang.ArrayIndexOutOfBoundsException"

            System.out.println("toString():    " + e.toString());
            // → "java.lang.ArrayIndexOutOfBoundsException: Index 5 out of..."

            System.out.println("\nStack trace:");
            e.printStackTrace();
            // → In ra stack trace đầy đủ (file, dòng, method)
        }

        // ===== 5. TRY LỒNG NHAU =====
        System.out.println("\n===== 5. Try lồng nhau =====");
        try {
            System.out.println("Try ngoài - bắt đầu");
            try {
                int x = 10 / 0;
            } catch (ArithmeticException e) {
                System.out.println("  Catch trong: " + e.getMessage());
            }
            System.out.println("Try ngoài - tiếp tục");

            String s = null;
            s.length(); // NullPointerException

        } catch (NullPointerException e) {
            System.out.println("Catch ngoài: " + e.getMessage());
        }
    }
}
```

### 2.2 Luồng thực thi try-catch

```
Trường hợp 1: KHÔNG có ngoại lệ
┌───────────────────────┐
│ try {                 │
│   Lệnh 1 ✅ (chạy)   │
│   Lệnh 2 ✅ (chạy)   │
│   Lệnh 3 ✅ (chạy)   │
│ }                     │
│ catch (Exception e) { │
│   Xử lý lỗi ⏭ (BỎ QUA)│
│ }                     │
│ Code sau try-catch ✅  │
└───────────────────────┘

Trường hợp 2: CÓ ngoại lệ tại Lệnh 2
┌───────────────────────┐
│ try {                 │
│   Lệnh 1 ✅ (chạy)   │
│   Lệnh 2 💥 (LỖI!)  │
│   Lệnh 3 ⏭ (BỎ QUA)  │ ← Không chạy
│ }                     │
│ catch (Exception e) { │
│   Xử lý lỗi ✅ (CHẠY) │ ← Nhảy vào catch
│ }                     │
│ Code sau try-catch ✅  │ ← Vẫn chạy tiếp
└───────────────────────┘
```

---

## 3. Khối finally

### 3.1 finally là gì?

Khối `finally` **LUÔN LUÔN chạy**, bất kể có ngoại lệ hay không. Thường dùng để **giải phóng tài nguyên** (đóng file, đóng kết nối DB, đóng socket...).

```
try {
   // Code có thể gây lỗi
} catch (Exception e) {
   // Xử lý lỗi
} finally {
   // LUÔN CHẠY dù có lỗi hay không
   // → Dùng để dọn dẹp tài nguyên
}
```

### 3.2 Code ví dụ

```java
import java.io.*;

public class FinallyDemo {
    public static void main(String[] args) {
        // ===== 1. FINALLY LUÔN CHẠY =====
        System.out.println("===== 1. Finally luôn chạy =====");

        // Trường hợp A: KHÔNG có exception
        try {
            System.out.println("Try: 10 / 2 = " + (10 / 2));
        } catch (ArithmeticException e) {
            System.out.println("Catch: " + e.getMessage());
        } finally {
            System.out.println("Finally: LUÔN chạy! ✅");
        }

        System.out.println();

        // Trường hợp B: CÓ exception
        try {
            System.out.println("Try: 10 / 0 = " + (10 / 0)); // 💥
        } catch (ArithmeticException e) {
            System.out.println("Catch: " + e.getMessage());
        } finally {
            System.out.println("Finally: VẪN chạy dù có lỗi! ✅");
        }

        // ===== 2. FINALLY VỚI RETURN =====
        System.out.println("\n===== 2. Finally với return =====");
        System.out.println("Kết quả: " + testReturn());
        // Finally vẫn chạy TRƯỚC khi return!

        // ===== 3. ỨNG DỤNG THỰC TẾ: Đóng tài nguyên =====
        System.out.println("\n===== 3. Đóng tài nguyên =====");

        // Cách truyền thống (trước Java 7):
        FileReader reader = null;
        try {
            reader = new FileReader("test.txt");
            // Đọc file...
            System.out.println("Đọc file thành công");
        } catch (FileNotFoundException e) {
            System.out.println("❌ File không tồn tại");
        } finally {
            // LUÔN đóng file, dù thành công hay thất bại
            if (reader != null) {
                try {
                    reader.close();
                    System.out.println("Đã đóng file (finally)");
                } catch (IOException e) {
                    System.out.println("Lỗi khi đóng file");
                }
            }
        }

        // ===== 4. TRY-WITH-RESOURCES (Java 7+) - Thay thế finally =====
        System.out.println("\n===== 4. Try-with-resources =====");
        // Tự động đóng tài nguyên khi kết thúc khối try
        // Resource phải implement AutoCloseable

        try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
            String line = br.readLine();
            System.out.println("Đọc: " + line);
        } catch (FileNotFoundException e) {
            System.out.println("❌ File không tồn tại");
        } catch (IOException e) {
            System.out.println("❌ Lỗi đọc file");
        }
        // br tự động được close() khi ra khỏi try!
        // Không cần finally để đóng nữa!

        // ===== 5. TRY-WITH-RESOURCES nhiều resource =====
        // try (
        //     FileInputStream fis = new FileInputStream("input.txt");
        //     FileOutputStream fos = new FileOutputStream("output.txt");
        //     BufferedReader br = new BufferedReader(new InputStreamReader(fis))
        // ) {
        //     // Sử dụng 3 resource
        //     // Tất cả tự động close() theo thứ tự NGƯỢC (fos → fis → br... thực tế LIFO)
        // } catch (IOException e) {
        //     e.printStackTrace();
        // }
    }

    // Finally vẫn chạy trước return
    public static int testReturn() {
        try {
            System.out.println("  Try block");
            return 1;
        } catch (Exception e) {
            System.out.println("  Catch block");
            return 2;
        } finally {
            System.out.println("  Finally block (chạy TRƯỚC return!)");
            // ⚠️ KHÔNG nên return trong finally (sẽ ghi đè return của try/catch)
        }
    }
}
```

### 3.3 Bảng tóm tắt hành vi finally

| Tình huống | try | catch | finally |
|---|---|---|---|
| **Không có exception** | ✅ Chạy hết | ⏭ Bỏ qua | ✅ **Luôn chạy** |
| **Có exception, được bắt** | ✅ Chạy đến chỗ lỗi | ✅ Chạy | ✅ **Luôn chạy** |
| **Có exception, KHÔNG bắt được** | ✅ Chạy đến chỗ lỗi | ⏭ Không khớp | ✅ **Luôn chạy** (rồi crash) |
| **Có return trong try** | ✅ return | ⏭ | ✅ **Chạy trước return** |
| **Có System.exit(0)** | ✅ | - | ❌ KHÔNG chạy (duy nhất trường hợp này) |

### 3.4 So sánh try-finally vs try-with-resources

```java
// ❌ CŨ: Dài dòng, dễ quên đóng, xử lý exception lồng nhau
FileReader reader = null;
try {
    reader = new FileReader("file.txt");
    // đọc file...
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (reader != null) {
        try {
            reader.close();  // Lại phải try-catch nữa!
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// ✅ MỚI (Java 7+): Gọn gàng, tự động đóng
try (FileReader reader2 = new FileReader("file.txt")) {
    // đọc file...
} catch (IOException e) {
    e.printStackTrace();
}
// reader2 tự động close()!
```

---

## 4. Từ khóa throw và throws

### 4.1 Phân biệt throw và throws

| Tiêu chí | `throw` | `throws` |
|---|---|---|
| **Vị trí** | **Trong thân hàm** | **Tại khai báo hàm** |
| **Mục đích** | **Ném** (tạo ra) một ngoại lệ cụ thể | **Khai báo** hàm có thể ném ngoại lệ |
| **Số lượng** | Ném **1** exception tại 1 thời điểm | Khai báo **nhiều** exception |
| **Theo sau là** | **Đối tượng** exception (`new Exception()`) | **Tên class** exception |
| **Cú pháp** | `throw new ArithmeticException("Lỗi");` | `void method() throws IOException, SQLException` |

### 4.2 Code ví dụ chi tiết

```java
import java.io.*;

public class ThrowThrowsDemo {

    // ===== THROW: Ném ngoại lệ trong thân hàm =====

    // 1. throw unchecked exception
    public static int divide(int a, int b) {
        if (b == 0) {
            // TẠO và NÉM ngoại lệ
            throw new ArithmeticException("Không thể chia cho 0! (a=" + a + ", b=" + b + ")");
        }
        return a / b;
    }

    // 2. throw để validate dữ liệu
    public static void setAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("Tuổi không thể âm: " + age);
        }
        if (age > 150) {
            throw new IllegalArgumentException("Tuổi không hợp lệ: " + age);
        }
        System.out.println("✅ Tuổi hợp lệ: " + age);
    }

    // 3. throw null check
    public static String processName(String name) {
        if (name == null) {
            throw new NullPointerException("Tên không được null!");
        }
        if (name.trim().isEmpty()) {
            throw new IllegalArgumentException("Tên không được rỗng!");
        }
        return name.trim().toUpperCase();
    }

    // ===== THROWS: Khai báo hàm có thể ném ngoại lệ =====

    // 4. throws checked exception (BẮT BUỘC khai báo)
    public static String readFirstLine(String filePath) throws FileNotFoundException, IOException {
        // FileReader ném FileNotFoundException (checked)
        // BufferedReader.readLine() ném IOException (checked)
        // → PHẢI khai báo throws ở method signature

        BufferedReader br = new BufferedReader(new FileReader(filePath));
        String line = br.readLine();
        br.close();
        return line;
    }

    // 5. throws kết hợp throw
    public static double sqrt(double number) throws IllegalArgumentException {
        if (number < 0) {
            throw new IllegalArgumentException(
                "Không thể tính căn bậc 2 của số âm: " + number);
        }
        return Math.sqrt(number);
    }

    // ===== MAIN: Xử lý các exception =====
    public static void main(String[] args) {
        // --- Test throw ---
        System.out.println("===== THROW =====");

        try {
            int result = divide(10, 0);
        } catch (ArithmeticException e) {
            System.out.println("❌ " + e.getMessage());
        }

        try {
            setAge(-5);
        } catch (IllegalArgumentException e) {
            System.out.println("❌ " + e.getMessage());
        }

        setAge(25);  // ✅ Tuổi hợp lệ: 25

        try {
            processName(null);
        } catch (NullPointerException e) {
            System.out.println("❌ " + e.getMessage());
        }

        System.out.println("Name: " + processName("  dũng  ")); // DŨNG

        // --- Test throws ---
        System.out.println("\n===== THROWS =====");

        // Hàm khai báo throws → người gọi PHẢI xử lý
        try {
            String line = readFirstLine("test.txt");
            System.out.println("Dòng đầu: " + line);
        } catch (FileNotFoundException e) {
            System.out.println("❌ File không tồn tại: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("❌ Lỗi IO: " + e.getMessage());
        }

        try {
            System.out.println("√16 = " + sqrt(16));   // 4.0
            System.out.println("√-4 = " + sqrt(-4));    // 💥
        } catch (IllegalArgumentException e) {
            System.out.println("❌ " + e.getMessage());
        }
    }
}
```

### 4.3 Chuỗi ném ngoại lệ (Exception Propagation)

```
Khi exception không được bắt, nó TỰ TRUYỀN NGƯỢC lên caller:

main() ──gọi──► methodA() ──gọi──► methodB() ──gọi──► methodC()
                                                          │
                                                    💥 Exception!
                                                          │
                              methodC() không catch   ◄───┘
                              → truyền lên methodB()
                    methodB() không catch   ◄──────────
                    → truyền lên methodA()
          methodA() có catch → XỬ LÝ!  ◄──────────
```

```java
public class PropagationDemo {
    public static void main(String[] args) {
        try {
            methodA();
        } catch (Exception e) {
            System.out.println("main() bắt được: " + e.getMessage());
            System.out.println("\nStack trace:");
            e.printStackTrace();
        }
    }

    static void methodA() {
        System.out.println("→ methodA() gọi methodB()");
        methodB();  // Không catch → exception truyền lên main()
    }

    static void methodB() {
        System.out.println("→ methodB() gọi methodC()");
        methodC();  // Không catch → exception truyền lên methodA()
    }

    static void methodC() {
        System.out.println("→ methodC() ném exception!");
        throw new RuntimeException("Lỗi tại methodC!");
        // Exception truyền ngược: methodC → methodB → methodA → main
    }
}
```

**Output:**
```
→ methodA() gọi methodB()
→ methodB() gọi methodC()
→ methodC() ném exception!
main() bắt được: Lỗi tại methodC!

Stack trace:
java.lang.RuntimeException: Lỗi tại methodC!
    at PropagationDemo.methodC(PropagationDemo.java:21)
    at PropagationDemo.methodB(PropagationDemo.java:16)
    at PropagationDemo.methodA(PropagationDemo.java:11)
    at PropagationDemo.main(PropagationDemo.java:4)
```

### 4.4 Re-throw (Ném lại ngoại lệ)

```java
public class ReThrowDemo {
    public static void processData(String data) {
        try {
            int num = Integer.parseInt(data);
            System.out.println("Số: " + num);
        } catch (NumberFormatException e) {
            System.out.println("⚠️ Log lỗi: Dữ liệu sai định dạng - " + data);
            // Xử lý một phần (log), rồi NÉM LẠI cho caller xử lý tiếp
            throw e;  // Re-throw nguyên exception
        }
    }

    // Hoặc bọc vào exception khác (Exception chaining)
    public static void processData2(String data) throws Exception {
        try {
            int num = Integer.parseInt(data);
        } catch (NumberFormatException e) {
            // Bọc exception gốc vào exception mới (giữ nguyên cause)
            throw new Exception("Lỗi xử lý dữ liệu: " + data, e);
            // e là "cause" - có thể lấy bằng getCause()
        }
    }

    public static void main(String[] args) {
        try {
            processData("abc");
        } catch (NumberFormatException e) {
            System.out.println("main() bắt re-throw: " + e.getMessage());
        }

        System.out.println();

        try {
            processData2("xyz");
        } catch (Exception e) {
            System.out.println("Exception: " + e.getMessage());
            System.out.println("Cause: " + e.getCause().getMessage());
        }
    }
}
```

---

## 5. Tạo ngoại lệ riêng (Custom Exception)

### 5.1 Tại sao cần Custom Exception?

- Tên exception **mô tả rõ lỗi nghiệp vụ** (VD: `InsufficientBalanceException`)
- Có thể **thêm thuộc tính riêng** (VD: `errorCode`, `currentBalance`)
- Code **dễ đọc, dễ debug** hơn

### 5.2 Code ví dụ đầy đủ

```java
// ===== CUSTOM CHECKED EXCEPTION =====
class InsufficientBalanceException extends Exception {
    private double currentBalance;
    private double withdrawAmount;

    public InsufficientBalanceException(double currentBalance, double withdrawAmount) {
        // Gọi constructor của Exception với message
        super(String.format(
            "Số dư không đủ! Số dư: $%.2f, Yêu cầu rút: $%.2f, Thiếu: $%.2f",
            currentBalance, withdrawAmount, withdrawAmount - currentBalance
        ));
        this.currentBalance = currentBalance;
        this.withdrawAmount = withdrawAmount;
    }

    public double getCurrentBalance() { return currentBalance; }
    public double getWithdrawAmount() { return withdrawAmount; }
    public double getDeficit() { return withdrawAmount - currentBalance; }
}

// ===== CUSTOM UNCHECKED EXCEPTION =====
class InvalidAccountException extends RuntimeException {
    private String accountNumber;
    private String errorCode;

    public InvalidAccountException(String accountNumber, String errorCode, String message) {
        super(message);
        this.accountNumber = accountNumber;
        this.errorCode = errorCode;
    }

    public String getAccountNumber() { return accountNumber; }
    public String getErrorCode() { return errorCode; }
}

// ===== CUSTOM EXCEPTION VỚI ENUM ERROR CODE =====
class BankException extends Exception {
    public enum ErrorCode {
        INVALID_AMOUNT("E001", "Số tiền không hợp lệ"),
        ACCOUNT_LOCKED("E002", "Tài khoản bị khóa"),
        DAILY_LIMIT("E003", "Vượt quá hạn mức giao dịch trong ngày"),
        INSUFFICIENT_BALANCE("E004", "Số dư không đủ");

        private final String code;
        private final String description;

        ErrorCode(String code, String description) {
            this.code = code;
            this.description = description;
        }

        public String getCode() { return code; }
        public String getDescription() { return description; }
    }

    private final ErrorCode errorCode;

    public BankException(ErrorCode errorCode) {
        super(errorCode.getDescription());
        this.errorCode = errorCode;
    }

    public BankException(ErrorCode errorCode, String additionalInfo) {
        super(errorCode.getDescription() + " - " + additionalInfo);
        this.errorCode = errorCode;
    }

    public ErrorCode getErrorCode() { return errorCode; }
}

// ===== SỬ DỤNG CUSTOM EXCEPTION =====
class BankAccount2 {
    private String accountNumber;
    private double balance;
    private boolean isLocked;
    private double dailyWithdrawn;
    private static final double DAILY_LIMIT = 50_000_000;

    public BankAccount2(String accountNumber, double balance) {
        if (accountNumber == null || accountNumber.length() != 10) {
            throw new InvalidAccountException(accountNumber, "ACC_INVALID",
                "Số tài khoản phải có 10 ký tự!");
        }
        this.accountNumber = accountNumber;
        this.balance = balance;
        this.isLocked = false;
        this.dailyWithdrawn = 0;
    }

    public void withdraw(double amount) throws BankException, InsufficientBalanceException {
        // Kiểm tra 1: Tài khoản bị khóa
        if (isLocked) {
            throw new BankException(BankException.ErrorCode.ACCOUNT_LOCKED);
        }

        // Kiểm tra 2: Số tiền hợp lệ
        if (amount <= 0) {
            throw new BankException(BankException.ErrorCode.INVALID_AMOUNT,
                "Số tiền phải lớn hơn 0, nhận được: " + amount);
        }

        // Kiểm tra 3: Hạn mức trong ngày
        if (dailyWithdrawn + amount > DAILY_LIMIT) {
            throw new BankException(BankException.ErrorCode.DAILY_LIMIT,
                String.format("Đã rút: $%,.0f, Yêu cầu: $%,.0f, Hạn mức: $%,.0f",
                    dailyWithdrawn, amount, DAILY_LIMIT));
        }

        // Kiểm tra 4: Số dư
        if (amount > balance) {
            throw new InsufficientBalanceException(balance, amount);
        }

        // Thực hiện rút
        balance -= amount;
        dailyWithdrawn += amount;
        System.out.printf("✅ Rút $%,.0f thành công. Số dư: $%,.0f%n", amount, balance);
    }

    public double getBalance() { return balance; }
    public void lock() { this.isLocked = true; }
}

// ===== MAIN =====
public class CustomExceptionDemo {
    public static void main(String[] args) {
        System.out.println("===== Custom Exception Demo =====\n");

        // 1. Tạo tài khoản - InvalidAccountException (unchecked)
        try {
            BankAccount2 bad = new BankAccount2("123", 1000);
        } catch (InvalidAccountException e) {
            System.out.println("❌ [" + e.getErrorCode() + "] " + e.getMessage());
            System.out.println("   Tài khoản: " + e.getAccountNumber());
        }

        System.out.println();

        // 2. Tạo tài khoản hợp lệ
        BankAccount2 account = new BankAccount2("1234567890", 10_000_000);
        System.out.println("Tài khoản tạo thành công! Số dư: $" +
            String.format("%,.0f", account.getBalance()));

        // 3. Test các trường hợp lỗi
        System.out.println("\n--- Test rút tiền ---");

        // Rút thành công
        try {
            account.withdraw(2_000_000);
        } catch (BankException | InsufficientBalanceException e) {
            System.out.println("❌ " + e.getMessage());
        }

        // Rút số tiền âm
        try {
            account.withdraw(-100);
        } catch (BankException e) {
            System.out.println("❌ [" + e.getErrorCode().getCode() + "] " + e.getMessage());
        } catch (InsufficientBalanceException e) {
            System.out.println("❌ " + e.getMessage());
        }

        // Rút vượt số dư
        try {
            account.withdraw(100_000_000);
        } catch (BankException e) {
            System.out.println("❌ [" + e.getErrorCode().getCode() + "] " + e.getMessage());
        } catch (InsufficientBalanceException e) {
            System.out.println("❌ " + e.getMessage());
            System.out.printf("   Thiếu: $%,.0f%n", e.getDeficit());
        }

        // Khóa tài khoản rồi rút
        account.lock();
        try {
            account.withdraw(1_000);
        } catch (BankException e) {
            System.out.println("❌ [" + e.getErrorCode().getCode() + "] " + e.getMessage());
        } catch (InsufficientBalanceException e) {
            System.out.println("❌ " + e.getMessage());
        }
    }
}
```

**Output:**
```
===== Custom Exception Demo =====

❌ [ACC_INVALID] Số tài khoản phải có 10 ký tự!
   Tài khoản: 123

Tài khoản tạo thành công! Số dư: $10,000,000

--- Test rút tiền ---
✅ Rút $2,000,000 thành công. Số dư: $8,000,000
❌ [E001] Số tiền không hợp lệ - Số tiền phải lớn hơn 0, nhận được: -100.0
❌ Số dư không đủ! Số dư: $8,000,000.00, Yêu cầu rút: $100,000,000.00, Thiếu: $92,000,000.00
   Thiếu: $92,000,000
❌ [E002] Tài khoản bị khóa
```

### 5.3 Cách tạo Custom Exception

```
Muốn tạo:                        Extend từ:
─────────────────────────         ──────────────────
Checked Exception (bắt buộc xử lý)  → extends Exception
Unchecked Exception (không bắt buộc) → extends RuntimeException

Quy tắc đặt tên: Kết thúc bằng "Exception"
✅ InsufficientBalanceException
✅ InvalidAccountException
✅ UserNotFoundException
❌ BalanceError (sai quy ước)
```

### 5.4 Best Practices xử lý ngoại lệ

| Quy tắc | Đúng ✅ | Sai ❌ |
|---|---|---|
| **Bắt exception cụ thể** | `catch (FileNotFoundException e)` | `catch (Exception e)` (quá chung) |
| **Không bỏ trống catch** | `catch (E e) { log(e); }` | `catch (E e) { }` (nuốt lỗi) |
| **Dùng finally/try-with-resources** | Luôn đóng tài nguyên | Quên đóng file/connection |
| **Message có ý nghĩa** | `"User ID 123 not found"` | `"Lỗi"` |
| **Log trước khi throw** | Ghi log → throw | Throw mà không log |
| **Không dùng exception cho logic** | `if (x != null)` | `try { x.method() } catch (NPE)` |
| **Custom exception cho nghiệp vụ** | `InsufficientBalanceException` | `RuntimeException("Thiếu tiền")` |

### 5.5 Tổng hợp so sánh

```
┌──────────────────────────────────────────────────────────────┐
│                   TỔNG HỢP EXCEPTION                         │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ try {                                                  │  │
│  │    // Code có thể gây exception                        │  │
│  │    riskyMethod();        // có thể throw               │  │
│  │ } catch (SpecificException e) {                        │  │
│  │    // Xử lý exception cụ thể                          │  │
│  │    log(e);                                             │  │
│  │ } catch (Exception e) {                                │  │
│  │    // Xử lý exception chung (đặt cuối)                │  │
│  │    throw new CustomException("msg", e);  // re-throw   │  │
│  │ } finally {                                            │  │
│  │    // LUÔN chạy - dọn dẹp tài nguyên                  │  │
│  │    cleanup();                                          │  │
│  │ }                                                      │  │
│  └────────────────────────────────────────────────────────┘  │
│                                                              │
│  // Hoặc:                                                    │
│  try (Resource r = new Resource()) {  // Tự đóng resource    │
│      r.use();                                                │
│  } catch (Exception e) {                                     │
│      handle(e);                                              │
│  }                                                           │
│                                                              │
│  // Khai báo hàm:                                            │
│  void myMethod() throws IOException, CustomException {       │
│      if (error) throw new CustomException("msg");            │
│  }                                                           │
│                                                              │
│  throw  = NÉM exception (trong thân hàm)                    │
│  throws = KHAI BÁO hàm có thể ném exception (tại signature) │
└──────────────────────────────────────────────────────────────┘
```

---

> **📌 Kết thúc Phần 4: Xử Lý Ngoại Lệ**

---

# Phần 5: Đọc Ghi (File I/O & Mạng)

## 📌 Mục lục
1. [Tổng quan về I/O Stream trong Java](#1-tổng-quan-về-io-stream-trong-java)
2. [Các cách đọc ghi File Text (Văn bản)](#2-các-cách-đọc-ghi-file-text-văn-bản)
3. [Các cách đọc ghi File Binary (Nhị phân)](#3-các-cách-đọc-ghi-file-binary-nhị-phân)
4. [Lưu và đọc List Sinh viên với File Text](#4-lưu-và-đọc-list-sinh-viên-với-file-text)
5. [Lưu và đọc List Sinh viên với File Binary (Serialization)](#5-lưu-và-đọc-list-sinh-viên-với-file-binary-serialization)
6. [Đọc dữ liệu từ một HTTP URL (GET Method)](#6-đọc-dữ-liệu-từ-một-http-url-get-method)

---

## 1. Tổng quan về I/O Stream trong Java

Trong Java, dòng dữ liệu (Stream) được chia làm 2 loại chính:

| Tiêu chí | Byte Stream (Dòng byte) | Character Stream (Dòng ký tự) |
|---|---|---|
| **Đơn vị xử lý** | 1 byte (8 bits) | 1 ký tự (16 bits - Unicode) |
| **Class gốc** | `InputStream` / `OutputStream` | `Reader` / `Writer` |
| **Loại file** | File nhị phân (Ảnh, Video, PDF, file `.bin`) | File văn bản (Text, CSV, JSON, `.txt`) |
| **Ví dụ Class** | `FileInputStream`, `FileOutputStream` | `FileReader`, `FileWriter`, `BufferedReader` |

> 💡 **Quy tắc vàng**:
> - Đọc/ghi chữ, văn bản con người đọc được → Dùng **Character Stream** (hậu tố là `Reader/Writer`).
> - Đọc/ghi dữ liệu thô, hình ảnh, âm thanh, object được mã hóa → Dùng **Byte Stream** (hậu tố là `InputStream/OutputStream`).

---

## 2. Các cách đọc ghi File Text (Văn bản)

### 2.1 Các class phổ biến
- **`FileWriter` / `FileReader`**: Cách cơ bản nhất, đọc/ghi từng ký tự. (Chậm nếu file lớn)
- **`BufferedWriter` / `BufferedReader`**: Bọc FileReader/FileWriter, dùng bộ đệm (buffer) để tăng tốc độ. Rất phổ biến vì có hàm `readLine()`.
- **`PrintWriter`**: Tiện lợi khi ghi file vì hỗ trợ các hàm in giống như in ra màn hình (`print`, `println`, `printf`).
- **`Scanner`**: Rất dễ để đọc theo từng token, parse số (`nextInt()`, `nextDouble()`).
- **`java.nio.file.Files`** (Java 7+): Class tiện ích, thao tác cực kỳ nhanh gọn cho các file nhỏ/vừa.

### 2.2 Code ví dụ: Đọc ghi File Text

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.List;
import java.util.Scanner;

public class TextFileDemo {
    public static void main(String[] args) {
        String fileName = "data.txt";

        // ==========================================
        // 1. GHI FILE TEXT
        // ==========================================
        System.out.println("--- GHI FILE TEXT ---");
        
        // Cách 1: Dùng BufferedWriter (Nhanh, khuyên dùng)
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(fileName))) {
            bw.write("Dòng 1: Hello World");
            bw.newLine(); // Xuống dòng
            bw.write("Dòng 2: Java I/O");
            System.out.println("Ghi bằng BufferedWriter thành công.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Cách 2: Dùng PrintWriter (Tiện lợi, có println, printf)
        // true: enable auto-flush
        try (PrintWriter pw = new PrintWriter(new FileWriter(fileName, true))) { 
            pw.println("Dòng 3: Ghi nối tiếp (Append)");
            pw.printf("Dòng 4: Số Pi là %.2f\n", 3.14);
            System.out.println("Ghi bằng PrintWriter thành công.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // ==========================================
        // 2. ĐỌC FILE TEXT
        // ==========================================
        System.out.println("\n--- ĐỌC FILE TEXT ---");

        // Cách 1: Dùng BufferedReader (Tốt nhất cho đọc từng dòng)
        System.out.println(">> Đọc bằng BufferedReader:");
        try (BufferedReader br = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Cách 2: Dùng Scanner (Tốt cho việc parse dữ liệu)
        System.out.println("\n>> Đọc bằng Scanner:");
        try (Scanner scanner = new Scanner(new File(fileName))) {
            while (scanner.hasNextLine()) {
                System.out.println(scanner.nextLine());
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }

        // Cách 3: Dùng java.nio.file.Files (Nhanh gọn, Java 7+)
        // CHÚ Ý: Chỉ dùng cho file không quá lớn (vừa đủ vào RAM)
        System.out.println("\n>> Đọc bằng java.nio.file.Files:");
        try {
            List<String> lines = Files.readAllLines(Paths.get(fileName));
            for (String l : lines) {
                System.out.println(l);
            }
            
            // Nếu muốn lấy cả file dạng 1 String duy nhất (Java 11+):
            // String content = Files.readString(Paths.get(fileName));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 3. Các cách đọc ghi File Binary (Nhị phân)

### 3.1 Các class phổ biến
- **`FileOutputStream` / `FileInputStream`**: Cơ bản nhất, đọc/ghi từng byte hoặc mảng byte.
- **`BufferedOutputStream` / `BufferedInputStream`**: Có buffer, tăng tốc độ đọc/ghi.
- **`DataOutputStream` / `DataInputStream`**: Tiện lợi khi muốn đọc/ghi các kiểu dữ liệu nguyên thủy (`int`, `double`, `boolean`...) trực tiếp vào file nhị phân.
- **`ObjectOutputStream` / `ObjectInputStream`**: Dùng để đọc/ghi trực tiếp ĐỐI TƯỢNG (Object) vào file (gọi là Serialization - Tuần tự hóa).

### 3.2 Code ví dụ: Đọc ghi File Binary

```java
import java.io.*;

public class BinaryFileDemo {
    public static void main(String[] args) {
        String fileName = "data.bin";

        // ==========================================
        // 1. GHI FILE BINARY (Dùng DataOutputStream)
        // ==========================================
        try (DataOutputStream dos = new DataOutputStream(
                new BufferedOutputStream(new FileOutputStream(fileName)))) {
            
            dos.writeInt(12345);          // Ghi số nguyên (4 bytes)
            dos.writeDouble(3.14159);     // Ghi số thực (8 bytes)
            dos.writeBoolean(true);       // Ghi boolean (1 byte)
            dos.writeUTF("Chuỗi UTF-8");  // Ghi chuỗi (tự kèm độ dài)
            
            System.out.println("Ghi file nhị phân thành công.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // ==========================================
        // 2. ĐỌC FILE BINARY (Dùng DataInputStream)
        // LƯU Ý: Phải đọc ĐÚNG THỨ TỰ như khi đã ghi
        // ==========================================
        try (DataInputStream dis = new DataInputStream(
                new BufferedInputStream(new FileInputStream(fileName)))) {
            
            int i = dis.readInt();
            double d = dis.readDouble();
            boolean b = dis.readBoolean();
            String s = dis.readUTF();
            
            System.out.println("\nĐọc từ file nhị phân:");
            System.out.println("Int: " + i);
            System.out.println("Double: " + d);
            System.out.println("Boolean: " + b);
            System.out.println("String: " + s);
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 4. Lưu và đọc List Sinh viên với File Text

Việc lưu một List Object vào file text thường sử dụng định dạng **CSV (Comma Separated Values)**. Mỗi dòng là 1 đối tượng, các thuộc tính cách nhau bởi dấu phẩy (hoặc dấu chấm phẩy).

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

class Student {
    int id;
    String name;
    double gpa;

    public Student(int id, String name, double gpa) {
        this.id = id; this.name = name; this.gpa = gpa;
    }
    
    // Hàm tiện ích để chuyển Object thành 1 dòng CSV
    public String toCSV() {
        return id + "," + name + "," + gpa;
    }

    // Hàm tiện ích để parse từ dòng CSV thành Object
    public static Student fromCSV(String csvLine) {
        String[] parts = csvLine.split(",");
        return new Student(
            Integer.parseInt(parts[0]), 
            parts[1], 
            Double.parseDouble(parts[2])
        );
    }

    @Override
    public String toString() {
        return "Student{id=" + id + ", name='" + name + "', gpa=" + gpa + '}';
    }
}

public class TextListDemo {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(1, "Nguyễn Văn A", 8.5));
        students.add(new Student(2, "Trần Thị B", 9.0));
        students.add(new Student(3, "Lê Hoàng C", 7.5));

        String fileCsv = "students.txt";

        // ===== 1. GHI LIST VÀO FILE TEXT =====
        try (PrintWriter pw = new PrintWriter(new FileWriter(fileCsv))) {
            for (Student s : students) {
                pw.println(s.toCSV());
            }
            System.out.println("Đã ghi List vào file Text (CSV)");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // ===== 2. ĐỌC LIST TỪ FILE TEXT =====
        List<Student> loadedList = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new FileReader(fileCsv))) {
            String line;
            while ((line = br.readLine()) != null) {
                loadedList.add(Student.fromCSV(line));
            }
            
            System.out.println("\nĐã đọc List từ file Text:");
            for (Student s : loadedList) {
                System.out.println(s);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 5. Lưu và đọc List Sinh viên với File Binary (Serialization)

Với File Binary, chúng ta không cần phải parse chuỗi (như `split(",")`). Java cung cấp cơ chế **Serialization (Tuần tự hóa)** để biến cả một khối Object (hoặc List các Object) thành chuỗi byte và lưu thẳng xuống file, lúc đọc lên nó tự động thành lại cấu trúc Object ban đầu.

**⚠️ Điều kiện BẮT BUỘC:** Class `Student` và tất cả thuộc tính bên trong nó đều PHẢI implement interface `java.io.Serializable`.

```java
import java.io.*;
import java.util.ArrayList;
import java.util.List;

// ĐIỀU KIỆN 1: implements Serializable
class StudentBin implements Serializable {
    // ĐIỀU KIỆN 2 (Tùy chọn nhưng NÊN có): serialVersionUID để kiểm soát phiên bản class
    private static final long serialVersionUID = 1L; 
    
    int id;
    String name;
    
    // Từ khóa "transient": Bỏ qua thuộc tính này, KHÔNG lưu vào file
    transient String password; 
    
    double gpa;

    public StudentBin(int id, String name, String password, double gpa) {
        this.id = id; this.name = name; this.password = password; this.gpa = gpa;
    }

    @Override
    public String toString() {
        return "StudentBin{id=" + id + ", name='" + name + "', pass='" + password + "', gpa=" + gpa + '}';
    }
}

public class BinaryListDemo {
    public static void main(String[] args) {
        List<StudentBin> students = new ArrayList<>();
        students.add(new StudentBin(1, "Nguyễn Văn A", "secret1", 8.5));
        students.add(new StudentBin(2, "Trần Thị B", "secret2", 9.0));

        String fileDat = "students.dat";

        // ===== 1. GHI OBJECT (LIST) VÀO FILE BINARY =====
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(fileDat))) {
            // Ghi CẢ List trong 1 câu lệnh duy nhất!
            oos.writeObject(students); 
            System.out.println("Đã ghi List vào file Binary thành công.");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // ===== 2. ĐỌC OBJECT (LIST) TỪ FILE BINARY =====
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream(fileDat))) {
            // Đọc cục dữ liệu lên và Ép kiểu về List
            @SuppressWarnings("unchecked")
            List<StudentBin> loadedList = (List<StudentBin>) ois.readObject();
            
            System.out.println("\nĐã đọc List từ file Binary:");
            for (StudentBin s : loadedList) {
                // Nhận xét: Thuộc tính password (transient) sẽ có giá trị null
                System.out.println(s);
            }
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### 5.1 So sánh Lưu File Text vs Lưu File Binary (Serialization)

| Tiêu chí | File Text (CSV / JSON) | File Binary (Serialization) |
|---|---|---|
| **Định dạng file** | Có thể đọc bằng con người (Notepad, Excel) | Ký tự lạ, máy mới đọc được |
| **Tốc độ / Kích thước** | Chậm hơn (vì phải parse string), file nặng hơn | Nhanh hơn, file thường nhỏ gọn hơn |
| **Tính bảo mật** | Dễ bị sửa đổi bên ngoài | Khó đọc/sửa hơn (nhưng vẫn có thể decode) |
| **Dễ bảo trì** | Cao, nếu class thay đổi cấu trúc, vẫn parse text dễ | Thấp, nếu class đổi cấu trúc mà khác `serialVersionUID`, lúc đọc lại sẽ bị văng lỗi `InvalidClassException` |
| **Khả năng tích hợp** | Java có thể giao tiếp với C#, Python, Web dễ dàng | Thường chỉ Java đọc được file Serialize của Java |

---

## 6. Đọc dữ liệu từ một HTTP URL (GET Method)

Khi bạn muốn gọi API hoặc lấy nội dung từ một trang web qua giao thức HTTP (phương thức GET). Java có 2 cách phổ biến:
1. Dùng **`HttpURLConnection`** (Cách cũ, có từ Java 1.1)
2. Dùng **`java.net.http.HttpClient`** (Cách hiện đại, có từ Java 11+, dễ dùng và hỗ trợ bất đồng bộ)

### 6.1 Code ví dụ: Dùng `HttpURLConnection` (Cách truyền thống)

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class HttpOldDemo {
    public static void main(String[] args) {
        String urlString = "https://jsonplaceholder.typicode.com/posts/1"; // Demo API URL
        
        try {
            // 1. Tạo đối tượng URL
            URL url = new URL(urlString);
            
            // 2. Mở kết nối
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            
            // 3. Cài đặt phương thức GET
            connection.setRequestMethod("GET");
            connection.setConnectTimeout(5000); // Timeout kết nối (5s)
            connection.setReadTimeout(5000);    // Timeout đọc dữ liệu (5s)
            
            // 4. Lấy mã phản hồi (HTTP Status Code)
            int status = connection.getResponseCode();
            System.out.println("HTTP Status Code: " + status);
            
            if (status == 200) { // 200 = OK
                // 5. Đọc dữ liệu trả về từ InputStream
                // Dữ liệu từ mạng cũng chỉ là 1 luồng InputStream như đọc file!
                BufferedReader in = new BufferedReader(
                    new InputStreamReader(connection.getInputStream())
                );
                
                String inputLine;
                StringBuilder content = new StringBuilder(); // Dùng StringBuilder gom data
                
                while ((inputLine = in.readLine()) != null) {
                    content.append(inputLine).append("\n");
                }
                in.close(); // Đóng stream
                
                System.out.println("Dữ liệu nhận được:");
                System.out.println(content.toString());
            } else {
                System.out.println("Lỗi gọi API. HTTP Code: " + status);
            }
            
            connection.disconnect(); // Ngắt kết nối
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 6.2 Code ví dụ: Dùng `HttpClient` (Java 11+ / Đề xuất dùng)

Class này được thêm vào từ Java 11, giải quyết tính dài dòng của `HttpURLConnection`.

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class HttpNewDemo {
    public static void main(String[] args) {
        String urlString = "https://jsonplaceholder.typicode.com/posts/1";
        
        // 1. Tạo HttpClient
        HttpClient client = HttpClient.newHttpClient();
        
        // 2. Tạo HttpRequest với phương thức GET
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create(urlString))
                .GET()
                .header("Accept", "application/json") // Header báo cho server kiểu data muốn nhận
                .build();
                
        try {
            // 3. Gửi Request đồng bộ (Gửi và đợi nhận về HttpResponse)
            // HttpResponse.BodyHandlers.ofString() báo rằng ta muốn lấy dữ liệu kiểu String
            HttpResponse<String> response = client.send(
                request, 
                HttpResponse.BodyHandlers.ofString()
            );
            
            // 4. Đọc kết quả
            System.out.println("HTTP Status Code: " + response.statusCode());
            if (response.statusCode() == 200) {
                System.out.println("Dữ liệu nhận được:");
                System.out.println(response.body());
            }
            
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

> 💡 **Giải thích cách hoạt động của GET request:**
> 1. Client tạo một Connection tới Server theo cái URL.
> 2. Gửi một gói tin chuẩn HTTP có Method = `GET`.
> 3. Server xử lý và trả về 1 Response gồm 2 phần: Header (chứa Status Code: 200 OK, 404 Not Found...) và Body (chứa data dưới dạng Text, HTML hoặc JSON).
> 4. Phía Java dùng Input Stream / BodyHandler để hứng cái Body đó về thành chuỗi String.

---

> **📌 Kết thúc Phần 5: Đọc Ghi File & Mạng**

---

# Phần 6: Cách Sử Dụng Các Kiểu Dữ Liệu Đặc Biệt

## 📌 Mục lục
1. [Enum - Kiểu dữ liệu liệt kê](#1-enum---kiểu-dữ-liệu-liệt-kê)
2. [Các cấu trúc dữ liệu cơ bản (BitSet, Vector, Stack, Queue)](#2-các-cấu-trúc-dữ-liệu-cơ-bản-bitset-vector-stack-queue)
3. [Sử dụng Stack để khử đệ quy](#3-sử-dụng-stack-để-khử-đệ-quy)
4. [Sử dụng Queue để duyệt đồ thị (BFS)](#4-sử-dụng-queue-để-duyệt-đồ-thị-bfs)
5. [Properties - Đọc/Ghi file cấu hình (config.properties)](#5-properties---đọc-ghi-file-cấu-hình-configproperties)
6. [Xử lý Ngày Tháng (Date và LocalDate)](#6-xử-lý-ngày-tháng-date-và-localdate)
7. [Chuyển đổi Date sang String (DateFormat)](#7-chuyển-đổi-date-sang-string-dateformat)

---

## 1. Enum - Kiểu dữ liệu liệt kê

### 1.1 Enum cơ bản
**Enum (Enumeration)** là một kiểu dữ liệu đặc biệt dùng để định nghĩa một tập hợp các **hằng số cố định**.
Sử dụng enum giúp code an toàn hơn (type-safe) thay vì dùng các số nguyên hay chuỗi rời rạc (Ví dụ: Trạng thái đơn hàng, Ngày trong tuần).

```java
// Khai báo Enum cơ bản
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

public class EnumBasicDemo {
    public static void main(String[] args) {
        Day today = Day.MONDAY;
        
        // So sánh enum
        if (today == Day.MONDAY) {
            System.out.println("Hôm nay là Thứ Hai");
        }
        
        // Dùng enum trong switch-case rất tiện
        switch (today) {
            case MONDAY:
            case TUESDAY:
                System.out.println("Đầu tuần làm việc");
                break;
            case SUNDAY:
                System.out.println("Cuối tuần nghỉ ngơi");
                break;
        }
        
        // Duyệt qua tất cả các giá trị của Enum
        for (Day d : Day.values()) {
            System.out.print(d + " "); // MONDAY TUESDAY WEDNESDAY...
        }
    }
}
```

### 1.2 Tạo Enum bằng giá trị (Custom Enum)
Trong Java, Enum bản chất là một Class. Bạn có thể thêm **thuộc tính, constructor và phương thức** cho Enum.

```java
// Khai báo Enum có chứa giá trị tùy chỉnh
enum OrderStatus {
    PENDING(0, "Chờ xử lý"),
    PROCESSING(1, "Đang xử lý"),
    SHIPPED(2, "Đã giao hàng"),
    CANCELLED(-1, "Đã hủy");

    // Các thuộc tính của Enum
    private final int code;
    private final String description;

    // Constructor của Enum (Bắt buộc phải là private hoặc không ghi gì)
    OrderStatus(int code, String description) {
        this.code = code;
        this.description = description;
    }

    // Getter
    public int getCode() { return code; }
    public String getDescription() { return description; }

    // Viết một hàm tiện ích để tìm Enum từ Code
    public static OrderStatus fromCode(int code) {
        for (OrderStatus status : OrderStatus.values()) {
            if (status.getCode() == code) {
                return status;
            }
        }
        throw new IllegalArgumentException("Mã trạng thái không hợp lệ: " + code);
    }
}

public class EnumValueDemo {
    public static void main(String[] args) {
        OrderStatus status = OrderStatus.SHIPPED;
        
        System.out.println("Status: " + status);                     // SHIPPED
        System.out.println("Mã code: " + status.getCode());          // 2
        System.out.println("Mô tả: " + status.getDescription());     // Đã giao hàng
        
        // Chuyển từ số (lấy từ Database) sang Enum
        OrderStatus dbStatus = OrderStatus.fromCode(-1);
        System.out.println("Từ DB code -1: " + dbStatus.getDescription()); // Đã hủy
    }
}
```

---

## 2. Các cấu trúc dữ liệu cơ bản (BitSet, Vector, Stack, Queue)

### 2.1 BitSet
`BitSet` là một mảng đặc biệt chỉ lưu các bit (`0` hoặc `1` / `false` hoặc `true`). 
**Ưu điểm:** Cực kỳ tiết kiệm bộ nhớ khi cần lưu mảng hàng triệu cờ boolean, vì nó nén 8 bit vào 1 byte.

```java
import java.util.BitSet;

public class BitSetDemo {
    public static void main(String[] args) {
        BitSet bits1 = new BitSet(16);
        BitSet bits2 = new BitSet(16);

        // Đặt bit 1 (true) tại các index
        bits1.set(0); bits1.set(1); bits1.set(2);
        bits2.set(1); bits2.set(2); bits2.set(3);

        System.out.println("Bits1: " + bits1); // {0, 1, 2}
        System.out.println("Bits2: " + bits2); // {1, 2, 3}

        // Các phép toán bit logic
        bits2.and(bits1); // Bits2 = Bits2 AND Bits1
        System.out.println("Sau AND (Bits2): " + bits2); // {1, 2} (phần giao nhau)
    }
}
```

### 2.2 Vector
`Vector` giống hệt `ArrayList` (mảng động tự giãn kích thước), nhưng các phương thức của nó được **đồng bộ hóa (Synchronized)**.
- **Nhược điểm:** Chậm hơn ArrayList trong môi trường đơn luồng (single-thread).
- Hiện nay ít dùng, thường thay bằng `ArrayList` hoặc `CopyOnWriteArrayList` cho đa luồng.

```java
import java.util.Vector;

public class VectorDemo {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("Apple");
        vector.add("Banana");
        System.out.println("Kích thước: " + vector.size());
        System.out.println("Phần tử 0: " + vector.get(0));
    }
}
```

### 2.3 Stack (Ngăn xếp)
- Nguyên lý: **LIFO** (Last In First Out - Vào sau ra trước). Giống như chồng đĩa.
- Kế thừa từ `Vector`. Cung cấp các hàm `push()` (thêm), `pop()` (lấy ra và xóa), `peek()` (xem phần tử đầu mà không xóa).

```java
import java.util.Stack;

public class StackDemo {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        
        stack.push(10); // Đáy stack
        stack.push(20);
        stack.push(30); // Đỉnh stack

        System.out.println("Đỉnh stack (peek): " + stack.peek()); // 30
        System.out.println("Lấy ra (pop): " + stack.pop());       // 30
        System.out.println("Còn lại trong stack: " + stack);      // [10, 20]
    }
}
```

### 2.4 Queue (Hàng đợi)
- Nguyên lý: **FIFO** (First In First Out - Vào trước ra trước). Giống như xếp hàng mua vé.
- `Queue` là một Interface. Thông thường ta dùng `LinkedList` để khởi tạo nó.
- Cung cấp các hàm: `offer()`/`add()` (thêm), `poll()`/`remove()` (lấy ra), `peek()` (xem đầu hàng).

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueDemo {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>();
        
        queue.offer("Người A"); // Đầu hàng
        queue.offer("Người B");
        queue.offer("Người C"); // Cuối hàng

        System.out.println("Đầu hàng (peek): " + queue.peek()); // Người A
        System.out.println("Phục vụ (poll): " + queue.poll());  // Phục vụ Người A và xóa khỏi Queue
        System.out.println("Còn lại trong Queue: " + queue);    // [Người B, Người C]
    }
}
```

---

## 3. Sử dụng Stack để khử đệ quy

Đệ quy bản chất là việc hệ điều hành sử dụng **Call Stack** (Ngăn xếp gọi hàm) của bộ nhớ RAM để lưu trạng thái hàm. Nếu đệ quy quá sâu sẽ bị lỗi `StackOverflowError`. Ta có thể tự định nghĩa một `Stack` (trên bộ nhớ Heap) để viết lại thuật toán bằng vòng lặp, hiện tượng này gọi là **khử đệ quy**.

Dưới đây là ví dụ khử đệ quy hàm In các số từ 1 đến N:

```java
import java.util.Stack;

public class EliminateRecursionDemo {
    
    // ===== 1. CÁCH DÙNG ĐỆ QUY (Dễ tràn bộ nhớ) =====
    public static void recursivePrint(int n) {
        if (n == 0) return;
        recursivePrint(n - 1);       // Đệ quy
        System.out.print(n + " ");
    }

    // ===== 2. CÁCH DÙNG STACK KHỬ ĐỆ QUY =====
    // Ý tưởng mô phỏng lại hành vi của Call Stack
    public static void stackPrint(int n) {
        Stack<Integer> stack = new Stack<>();
        
        // Bước 1: Đẩy tất cả các công việc vào Stack (tương tự như gọi hàm)
        // Vì Stack là LIFO (Vào sau ra trước), ta đẩy n vào trước, 1 vào sau
        // Để khi pop ra, số 1 sẽ ra trước.
        for (int i = n; i >= 1; i--) {
            stack.push(i);
        }

        // Bước 2: Lấy ra và xử lý (tương tự như thực thi hàm)
        while (!stack.isEmpty()) {
            int current = stack.pop();
            System.out.print(current + " ");
        }
    }

    public static void main(String[] args) {
        System.out.print("Đệ quy:  ");
        recursivePrint(5); // 1 2 3 4 5
        
        System.out.print("\nStack:   ");
        stackPrint(5);     // 1 2 3 4 5
    }
}
```

---

## 4. Sử dụng Queue để duyệt đồ thị (BFS)

**BFS (Breadth-First Search - Tìm kiếm theo chiều rộng)** là thuật toán duyệt các đỉnh của Đồ thị/Cây theo từng tầng (level). BFS sử dụng `Queue` (Hàng đợi) để ghi nhớ các đỉnh kề chưa được thăm.

```java
import java.util.*;

// Biểu diễn Đồ thị bằng Danh sách kề (Adjacency List)
class Graph {
    private int V; // Số lượng đỉnh
    private LinkedList<Integer>[] adj; // Mảng các danh sách kề

    @SuppressWarnings("unchecked")
    public Graph(int v) {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<>();
    }

    // Thêm cạnh nối Đỉnh v và Đỉnh w (đồ thị có hướng)
    public void addEdge(int v, int w) {
        adj[v].add(w);
    }

    // ===== THUẬT TOÁN BFS DÙNG QUEUE =====
    public void BFS(int startNode) {
        // Mảng đánh dấu các đỉnh đã thăm để không bị lặp vòng vô tận
        boolean[] visited = new boolean[V];

        // Tạo một Hàng đợi (Queue) cho BFS
        Queue<Integer> queue = new LinkedList<>();

        // Đánh dấu đỉnh bắt đầu là đã thăm và đưa vào hàng đợi
        visited[startNode] = true;
        queue.offer(startNode);

        System.out.print("Thứ tự duyệt BFS từ đỉnh " + startNode + ": ");

        while (!queue.isEmpty()) {
            // 1. Lấy đỉnh ở đầu Queue ra và in
            int current = queue.poll();
            System.out.print(current + " ");

            // 2. Lấy tất cả các đỉnh kề của đỉnh vừa lấy ra
            for (int neighbor : adj[current]) {
                // Nếu đỉnh kề chưa được thăm
                if (!visited[neighbor]) {
                    visited[neighbor] = true; // Đánh dấu đã thăm
                    queue.offer(neighbor);    // Đưa vào cuối Queue để duyệt sau
                }
            }
        }
        System.out.println();
    }
}

public class BFSDemo {
    public static void main(String[] args) {
        /* Tạo đồ thị:
           0 ---> 1
           |      |
           v      v
           2 ---> 3 ---> 4
        */
        Graph g = new Graph(5);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(2, 3);
        g.addEdge(3, 4);

        g.BFS(0); 
        // Kết quả mong đợi: 0 1 2 3 4
        // Tầng 1: Đỉnh 0
        // Tầng 2: Đỉnh 1, 2
        // Tầng 3: Đỉnh 3
        // Tầng 4: Đỉnh 4
    }
}
```

---

## 5. Properties - Đọc ghi file cấu hình config.properties

Class `Properties` (kế thừa `Hashtable`) lưu dữ liệu dưới dạng **Key-Value** theo kiểu chuỗi (String). Nó cực kỳ phổ biến trong Java để lưu các thông số cấu hình ứng dụng (URL Database, port, username...).

### 5.1 Code ví dụ Tạo, Đọc và Thêm cấu hình

```java
import java.io.*;
import java.util.Properties;

public class PropertiesDemo {
    public static void main(String[] args) {
        String fileName = "config.properties";

        // =====================================
        // 1. TẠO RA FILE CONFIG.PROPERTIES
        // =====================================
        Properties props = new Properties();
        // Set các thông số cấu hình
        props.setProperty("db.url", "localhost:3306");
        props.setProperty("db.user", "admin");
        props.setProperty("db.password", "123456");
        
        try (FileOutputStream out = new FileOutputStream(fileName)) {
            // Ghi xuống file kèm comment giải thích
            props.store(out, "Database Configuration File");
            System.out.println("✅ Đã tạo file " + fileName);
        } catch (IOException e) {
            e.printStackTrace();
        }

        // =====================================
        // 2. ĐỌC FILE CONFIG.PROPERTIES
        // =====================================
        Properties readProps = new Properties();
        try (FileInputStream in = new FileInputStream(fileName)) {
            readProps.load(in); // Tự động đọc và parse key-value
            
            System.out.println("\n--- ĐỌC CẤU HÌNH ---");
            System.out.println("URL: " + readProps.getProperty("db.url"));
            System.out.println("User: " + readProps.getProperty("db.user"));
            // Lấy thuộc tính không tồn tại kèm giá trị mặc định
            System.out.println("Timeout: " + readProps.getProperty("db.timeout", "5000 (default)"));
            
        } catch (IOException e) {
            e.printStackTrace();
        }

        // =====================================
        // 3. THÊM CONFIG VÀO FILE (UPDATE)
        // =====================================
        try {
            // Bước A: Phải đọc file cũ lên trước
            Properties updateProps = new Properties();
            try (FileInputStream in = new FileInputStream(fileName)) {
                updateProps.load(in);
            }
            
            // Bước B: Sửa đổi và Thêm mới
            updateProps.setProperty("db.timeout", "8000"); // Thêm mới key
            updateProps.setProperty("db.user", "root");    // Cập nhật key cũ
            
            // Bước C: Ghi đè lại file
            try (FileOutputStream out = new FileOutputStream(fileName)) {
                updateProps.store(out, "Updated Configuration");
            }
            System.out.println("\n✅ Đã cập nhật và thêm config mới vào file.");
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Nội dung file `config.properties` sinh ra:**
```properties
#Updated Configuration
#Mon Jun 29 14:05:00 ICT 2026
db.password=123456
db.url=localhost\:3306
db.user=root
db.timeout=8000
```

---

## 6. Xử lý Ngày Tháng (Date và LocalDate)

Java có hai hệ thống xử lý thời gian chính:
1. **`java.util.Date`** (Cũ): Thiết kế thiếu sót, có thể thay đổi (mutable).
2. **`java.time.LocalDate`** (Từ Java 8): Thiết kế chuẩn quốc tế, không thể thay đổi (immutable), an toàn trong đa luồng (thread-safe). **(Khuyên dùng)**.

### 6.1 So sánh và Cách sử dụng

```java
import java.util.Date;
import java.util.Calendar;
import java.time.LocalDate;
import java.time.LocalDateTime;

public class DateDemo {
    public static void main(String[] args) {
        
        // =====================================
        // 1. CÁCH CŨ: DÙNG java.util.Date
        // =====================================
        System.out.println("--- DÙNG DATE (CŨ) ---");
        
        Date oldDate = new Date(); // Lấy ngày giờ hiện tại
        System.out.println("Date hiện tại: " + oldDate);

        // Date cũ không có hàm cộng trừ ngày! Phải dùng qua class Calendar rất rườm rà
        Calendar cal = Calendar.getInstance();
        cal.setTime(oldDate);
        cal.add(Calendar.DAY_OF_MONTH, 5); // Cộng thêm 5 ngày
        Date newOldDate = cal.getTime();
        System.out.println("Sau khi cộng 5 ngày: " + newOldDate);


        // =====================================
        // 2. CÁCH MỚI: DÙNG java.time (JAVA 8+)
        // =====================================
        System.out.println("\n--- DÙNG LOCALDATE (MỚI) ---");
        
        // Lấy ngày hiện tại (Chỉ có ngày tháng năm, không có giờ)
        LocalDate today = LocalDate.now();
        System.out.println("Hôm nay: " + today);

        // Khởi tạo một ngày cụ thể
        LocalDate specificDate = LocalDate.of(2026, 12, 25);
        System.out.println("Giáng sinh: " + specificDate);

        // CỘNG TRỪ NGÀY THÁNG RẤT DỄ DÀNG
        LocalDate nextWeek = today.plusDays(7);       // Cộng 7 ngày
        LocalDate lastMonth = today.minusMonths(1);   // Trừ 1 tháng
        LocalDate nextYear = today.plusYears(2);      // Cộng 2 năm
        
        System.out.println("Tuần sau: " + nextWeek);
        System.out.println("Tháng trước: " + lastMonth);

        // Các hàm tiện ích
        System.out.println("Năm nhuận? " + today.isLeapYear());
        System.out.println("Ngày trong tuần: " + today.getDayOfWeek()); // Ví dụ: MONDAY

        // Nếu cần cả giờ phút giây thì dùng LocalDateTime
        LocalDateTime nowDateTime = LocalDateTime.now();
        System.out.println("\nNgày giờ hiện tại: " + nowDateTime);
    }
}
```

---

## 7. Chuyển đổi Date sang String (DateFormat)

Để chuyển đổi từ Date/LocalDate sang dạng chuỗi (để in ra) và ngược lại (từ chuỗi nhập vào parse thành Date), ta dùng các Formatters.

| Class Ngày Tháng | Class định dạng tương ứng |
|---|---|
| `java.util.Date` (Cũ) | `java.text.SimpleDateFormat` |
| `java.time.LocalDate` (Mới) | `java.time.format.DateTimeFormatter` |

### 7.1 Code ví dụ

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class DateFormatDemo {
    public static void main(String[] args) {
        
        String pattern = "dd/MM/yyyy"; // Ký hiệu: d (ngày), M (tháng), y (năm)

        System.out.println("===== 1. CHUYỂN ĐỔI VỚI DATE (CŨ) =====");
        
        // Tạo formatter
        SimpleDateFormat sdf = new SimpleDateFormat(pattern);
        
        // A. Date -> String (Format)
        Date now = new Date();
        String dateString = sdf.format(now);
        System.out.println("Date to String: " + dateString);
        
        // B. String -> Date (Parse)
        String inputStr = "25/12/2026";
        try {
            Date parsedDate = sdf.parse(inputStr); // Phải bắt ngoại lệ ParseException
            System.out.println("String to Date: " + parsedDate);
        } catch (ParseException e) {
            System.out.println("Lỗi sai định dạng ngày tháng!");
        }


        System.out.println("\n===== 2. CHUYỂN ĐỔI VỚI LOCALDATE (MỚI) =====");
        
        // Tạo formatter (Thread-safe)
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern(pattern);

        // A. LocalDate -> String (Format)
        LocalDate localToday = LocalDate.now();
        String localStr = localToday.format(formatter);
        System.out.println("LocalDate to String: " + localStr);

        // B. String -> LocalDate (Parse)
        // Không bắt buộc phải try-catch, nhưng có thể ném DateTimeParseException nếu sai
        LocalDate parsedLocal = LocalDate.parse(inputStr, formatter);
        System.out.println("String to LocalDate: " + parsedLocal);
    }
}
```

> 💡 **Bảng tham chiếu ký tự Format (Tương tự cho cả 2 cách):**
> - `yyyy`: Năm (VD: 2026)
> - `MM`: Tháng có số 0 (VD: 01..12)
> - `dd`: Ngày có số 0 (VD: 01..31)
> - `HH`: Giờ hệ 24h (00..23)
> - `mm`: Phút (00..59)
> - `ss`: Giây (00..59)
> 
> *Ví dụ Pattern giờ chuẩn quốc tế:* `"yyyy-MM-dd HH:mm:ss"`

---

> **📌 Kết thúc Phần 6: Data Structures & Các Kiểu Dữ Liệu**

---

# Phần 7: Collections Framework (Bộ sưu tập)

## 📌 Mục lục
1. [Cây giao diện (Interface) của Collection](#1-cây-giao-diện-interface-của-collection)
2. [Sự khác biệt giữa List, Set và Map](#2-sự-khác-biệt-giữa-list-set-và-map)
3. [Phân tích List: ArrayList vs LinkedList](#3-phân-tích-list-arraylist-vs-linkedlist)
4. [Phân tích Set: HashSet và Tầm quan trọng của equals/hashCode](#4-phân-tích-set-hashset-và-tầm-quan-trọng-của-equalshashcode)
5. [LinkedHashSet, TreeSet và Cách sắp xếp Set](#5-linkedhashset-treeset-và-cách-sắp-xếp-set)
6. [Phân tích Map: HashMap, TreeMap và Cách sắp xếp Map theo Value](#6-phân-tích-map-hashmap-treemap-và-cách-sắp-xếp-map-theo-value)
7. [Interface Comparable và Hàm compareTo](#7-interface-comparable-và-hàm-compareto)
8. [Bảng Đánh giá Tốc độ (Độ phức tạp thuật toán Big O)](#8-bảng-đánh-giá-tốc-độ-độ-phức-tạp-thuật-toán-big-o)

---

## 1. Cây giao diện (Interface) của Collection

Trong Java, `Collections Framework` là một kiến trúc hợp nhất để lưu trữ và thao tác với nhóm các đối tượng. Phân cấp (Hierarchy) của nó gồm 2 nhánh chính hoàn toàn độc lập: **Collection** và **Map**.

```text
                  «interface»
                   Iterable
                       ↑ (extends)
                  «interface»
                  Collection
                 /     |     \ (extends)
               /       |       \
       «interface» «interface» «interface»                «interface»
          List       Queue        Set                         Map
           |           |           |                           | (implements)
      (implements) (implements) (implements)                /     \
       ArrayList   LinkedList    HashSet                HashMap  TreeMap
      LinkedList  PriorityQueue  LinkedHashSet          LinkedHashMap
       Vector                    TreeSet
```

> ⚠️ **Lưu ý:** `Map` **KHÔNG** kế thừa từ `Collection`. Nó là một nhánh lưu trữ theo cặp Key-Value hoàn toàn riêng biệt.

---

## 2. Sự khác biệt giữa List, Set và Map

| Đặc điểm | `List` (Danh sách) | `Set` (Tập hợp) | `Map` (Ánh xạ / Từ điển) |
|---|---|---|---|
| **Lưu trữ** | Lưu từng phần tử đơn lẻ | Lưu từng phần tử đơn lẻ | Lưu theo cặp `Key - Value` (Khóa - Giá trị) |
| **Phần tử trùng lặp** | ✅ **Cho phép** trùng lặp | ❌ **Không cho phép** trùng lặp | Key **không** trùng lặp, Value **có thể** trùng lặp. |
| **Thứ tự (Order)** | Giữ nguyên thứ tự khi chèn | Đa số là không có thứ tự | Đa số là không có thứ tự |
| **Truy cập phần tử** | Bằng vị trí (index) `list.get(2)` | Không có index, phải dùng Loop/Iterator | Truy cập bằng Key: `map.get(key)` |

---

## 3. Phân tích List: ArrayList vs LinkedList

Cả 2 đều implement `List`, nhưng cấu trúc dữ liệu nền tảng (underlying data structure) bên dưới lại khác nhau hoàn toàn.

| Tiêu chí | `ArrayList` | `LinkedList` |
|---|---|---|
| **Cấu trúc bên dưới** | Mảng động (Dynamic Array) | Danh sách liên kết kép (Doubly Linked List) |
| **Truy xuất phần tử (get)** | Rất nhanh `O(1)` (Truy xuất qua index) | Rất chậm `O(N)` (Phải duyệt từ đầu tới phần tử đó) |
| **Thêm/Xóa ở cuối** | Nhanh `O(1)` | Nhanh `O(1)` |
| **Thêm/Xóa ở giữa** | Chậm `O(N)` (Vì phải dịch chuyển toàn bộ mảng) | Nhanh `O(1)` (Nếu đã biết vị trí, chỉ cần bẻ lại con trỏ nối) |
| **Ứng dụng thực tế** | Dùng 90% trường hợp (chủ yếu là Đọc dữ liệu) | Dùng khi cần thao tác Thêm/Xóa liên tục ở đầu hoặc giữa danh sách |

---

## 4. Phân tích Set: HashSet và Tầm quan trọng của equals/hashCode

### 4.1 HashSet là gì?
- `HashSet` là implementation phổ biến nhất của Set. Bên dưới nó thực chất sử dụng một `HashMap`.
- Nó lưu trữ các phần tử dựa trên cơ chế **Băm (Hashing)**. Do đó, tốc độ tìm kiếm và thêm mới cực kỳ nhanh (O(1)).

### 4.2 Tại sao bắt buộc phải Override cả `equals` và `hashCode`?
Như đã đề cập ở Phần 3 (OOP), cơ chế làm việc của HashSet khi gọi hàm `add(Object)` như sau:
1. Nó gọi `hashCode()` của đối tượng để tìm ra vị trí "ngăn kéo" (bucket) cần cất đối tượng vào.
2. Nếu ngăn kéo trống → Đưa vào ngay.
3. Nếu ngăn kéo đã có đối tượng (Đụng độ Hash) → Nó tiếp tục gọi hàm `equals()` để so sánh đối tượng mới với các đối tượng đang có trong ngăn kéo.
   - Nếu `equals` trả về `true` → Nhận định là trùng lặp → **TỪ CHỐI THÊM**.
   - Nếu `equals` trả về `false` → Nhận định là khác nhau → Thêm vào cùng ngăn kéo đó (Linked list / Red-Black Tree).

> **HẬU QUẢ NẾU KHÔNG OVERRIDE:**
> Nếu bạn tạo class `Student` mà không ghi đè 2 hàm này, Java sẽ dùng mặc định của class `Object` (so sánh địa chỉ bộ nhớ). Khi đó, dù 2 `Student` có cùng ID và Tên, chúng có địa chỉ bộ nhớ khác nhau $\rightarrow$ `hashCode` khác nhau $\rightarrow$ `HashSet` coi đó là 2 người khác nhau và sẽ thêm cả 2 (Bị trùng lặp logic hệ thống).

```java
import java.util.HashSet;
import java.util.Objects;

class User {
    int id;
    String name;

    public User(int id, String name) { this.id = id; this.name = name; }

    // PHẢI GHI ĐÈ CẢ 2 HÀM
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return id == user.id; // Chỉ so sánh ID
    }

    @Override
    public int hashCode() {
        return Objects.hash(id); // Sinh hash từ ID
    }
}

public class HashSetDemo {
    public static void main(String[] args) {
        HashSet<User> set = new HashSet<>();
        set.add(new User(1, "Alice"));
        
        // Thêm một người có cùng ID = 1
        boolean isAdded = set.add(new User(1, "Bob")); 
        
        System.out.println("Có thêm được Bob không? " + isAdded); // false
        System.out.println("Số lượng User trong set: " + set.size()); // 1
    }
}
```

---

## 5. LinkedHashSet, TreeSet và Cách sắp xếp Set

Nếu `HashSet` lưu dữ liệu lộn xộn (không có thứ tự), thì:
- **`LinkedHashSet`**: Lưu phần tử và **giữ nguyên thứ tự chèn vào**. (Bên dưới kết hợp HashTable và Linked List).
- **`TreeSet`**: Tự động **sắp xếp** các phần tử (theo thứ tự tăng dần của giá trị, hoặc theo một quy tắc tự định nghĩa). (Bên dưới dùng Red-Black Tree).

```java
import java.util.*;

public class SetTypesDemo {
    public static void main(String[] args) {
        // 1. HASH SET (Lộn xộn)
        Set<Integer> hashSet = new HashSet<>(Arrays.asList(50, 10, 30, 20, 40));
        System.out.println("HashSet: " + hashSet); 
        // Kết quả có thể là: [50, 20, 40, 10, 30]

        // 2. LINKED HASH SET (Giữ đúng thứ tự thêm vào)
        Set<Integer> linkedSet = new LinkedHashSet<>(Arrays.asList(50, 10, 30, 20, 40));
        System.out.println("LinkedHashSet: " + linkedSet); 
        // Kết quả CHẮC CHẮN là: [50, 10, 30, 20, 40]

        // 3. TREE SET (Tự động sắp xếp tăng dần)
        Set<Integer> treeSet = new TreeSet<>(Arrays.asList(50, 10, 30, 20, 40));
        System.out.println("TreeSet: " + treeSet); 
        // Kết quả CHẮC CHẮN là: [10, 20, 30, 40, 50]
    }
}
```

---

## 6. Phân tích Map: HashMap, TreeMap và Cách sắp xếp Map theo Value

Map lưu theo cặp Khóa - Giá trị (Key-Value).

- **`HashMap`**: Tìm kiếm siêu tốc, các Key được lưu lộn xộn (Giống HashSet).
- **`LinkedHashMap`**: Giữ nguyên thứ tự thêm vào của các Key.
- **`TreeMap`**: Tự động sắp xếp các phần tử theo **TĂNG DẦN CỦA KEY**.

### Vấn đề khó: Làm sao sắp xếp Map theo VALUE?
`TreeMap` chỉ sắp xếp theo Key. Nếu bạn muốn sắp xếp theo Value (ví dụ: Map lưu Tên -> Điểm số, muốn sắp xếp điểm số từ cao xuống thấp), bạn phải làm theo các bước sau:
1. Lấy toàn bộ `entrySet()` của Map đổ ra một `List`.
2. Dùng `Collections.sort()` để sắp xếp cái List đó (tùy biến thuật toán so sánh Value).
3. Đổ lại danh sách đã sắp xếp vào một `LinkedHashMap` (Vì LinkedHashMap mới giữ được thứ tự thêm vào).

```java
import java.util.*;

public class SortMapByValue {
    public static void main(String[] args) {
        Map<String, Integer> scores = new HashMap<>();
        scores.put("Alice", 85);
        scores.put("Bob", 99);
        scores.put("Charlie", 70);
        scores.put("David", 90);

        System.out.println("Map ban đầu (lộn xộn): " + scores);

        // BƯỚC 1: Lấy danh sách Entry từ Map đổ vào List
        List<Map.Entry<String, Integer>> list = new ArrayList<>(scores.entrySet());

        // BƯỚC 2: Sắp xếp List dựa trên Value (Điểm số giảm dần)
        list.sort(new Comparator<Map.Entry<String, Integer>>() {
            @Override
            public int compare(Map.Entry<String, Integer> o1, Map.Entry<String, Integer> o2) {
                // o2.getValue().compareTo(o1.getValue()) -> Giảm dần
                return o2.getValue().compareTo(o1.getValue());
            }
        });

        // BƯỚC 3: Đổ lại vào LinkedHashMap để giữ thứ tự
        Map<String, Integer> sortedMap = new LinkedHashMap<>();
        for (Map.Entry<String, Integer> entry : list) {
            sortedMap.put(entry.getKey(), entry.getValue());
        }

        System.out.println("Map sắp xếp theo Value (Điểm giảm dần): " + sortedMap);
        // Kết quả: {Bob=99, David=90, Alice=85, Charlie=70}
    }
}
```

---

## 7. Interface Comparable và Hàm compareTo

Trong Java, khi dùng `TreeSet` hoặc `TreeMap`, hệ thống cần biết cách **Sắp xếp** các Object của bạn. Làm sao nó biết `Student A` lớn hơn hay nhỏ hơn `Student B`? 

Để giải quyết, Class của bạn **BẮT BUỘC** phải implements interface `Comparable<T>` và ghi đè hàm `compareTo()`. Nếu không, khi add vào TreeSet sẽ bị văng lỗi `ClassCastException`.

### Quy tắc hàm `compareTo(Object o)`
Hàm này so sánh đối tượng hiện tại (`this`) với đối tượng truyền vào (`o`). Trả về 1 số nguyên `int`:
- **Số ÂM (`< 0`)**: `this` ĐỨNG TRƯỚC `o` (Tức là `this` nhỏ hơn).
- **Số KHÔNG (`== 0`)**: Bằng nhau.
- **Số DƯƠNG (`> 0`)**: `this` ĐỨNG SAU `o` (Tức là `this` lớn hơn).

```java
import java.util.TreeSet;

// 1. implements Comparable
class Product implements Comparable<Product> {
    int price;
    String name;

    public Product(int price, String name) {
        this.price = price; this.name = name;
    }

    // 2. Ghi đè compareTo
    @Override
    public int compareTo(Product other) {
        // Tiêu chí 1: Sắp xếp theo giá TĂNG DẦN
        if (this.price != other.price) {
            return Integer.compare(this.price, other.price);
        }
        // Tiêu chí 2: Nếu giá bằng nhau, sắp xếp theo tên (A-Z)
        return this.name.compareTo(other.name);
    }

    @Override
    public String toString() { return name + "($" + price + ")"; }
}

public class ComparableDemo {
    public static void main(String[] args) {
        // Sử dụng TreeSet
        TreeSet<Product> set = new TreeSet<>();
        set.add(new Product(500, "Laptop"));
        set.add(new Product(200, "Mouse"));
        set.add(new Product(200, "Keyboard")); // Cùng giá 200

        System.out.println(set);
        // Kết quả: [Keyboard($200), Mouse($200), Laptop($500)]
        // (Keyboard đứng trước Mouse vì vần K đứng trước vần M)
    }
}
```
> **Lưu ý:** Nếu bạn không thể sửa mã nguồn của Class để `implements Comparable`, bạn có thể tạo một class riêng `implements Comparator<T>` và truyền nó vào Constructor của TreeSet/TreeMap.

---

## 8. Bảng Đánh giá Tốc độ (Độ phức tạp thuật toán Big O)

Đây là bảng tóm tắt lý do tại sao phải chọn đúng Cấu trúc dữ liệu trong các tình huống thực tế:

| Cấu trúc dữ liệu | Hàm `add(E)` (Thêm) | Hàm `remove(E)` (Xóa) | Hàm `contains(E)` (Kiểm tra tồn tại) | Nhận xét |
|---|---|---|---|---|
| **ArrayList** | Đầu: $O(N)$<br>Cuối: $O(1)$ | Đầu/Giữa: $O(N)$<br>Cuối: $O(1)$ | $O(N)$ (Phải quét hết mảng) | Nhanh khi thêm cuối và truy xuất bằng `get(index)` O(1). |
| **LinkedList** | Đầu/Cuối: $O(1)$ | Đầu/Cuối: $O(1)$<br>Giữa: $O(N)$ | $O(N)$ (Phải quét tuần tự) | Tuyệt vời khi dùng làm Queue / Stack. |
| **HashSet** | $O(1)$ (Tr.bình) | $O(1)$ (Tr.bình) | $O(1)$ (Tr.bình) | Nhanh vô địch trong việc kiểm tra "Phần tử này đã có chưa?". |
| **TreeSet** | $O(\log N)$ | $O(\log N)$ | $O(\log N)$ | Luôn giữ dữ liệu được sắp xếp, nhưng chậm hơn HashSet. |
| **HashMap** | `put`: $O(1)$ | `remove`: $O(1)$ | `containsKey`: $O(1)$ | Map phổ biến nhất, hiệu suất cao nhất. |
| **TreeMap** | `put`: $O(\log N)$| `remove`: $O(\log N)$| `containsKey`: $O(\log N)$| Dùng khi cần các Key luôn được sắp xếp. |

---

> **📌 Kết thúc Phần 7: Collections Framework**

---

# Phần 8: Lập trình Đa luồng (Multi-threading)

## 📌 Mục lục
1. [Tại sao cần lập trình đa luồng?](#1-tại-sao-cần-lập-trình-đa-luồng)
2. [Máy 1 CPU chạy đa luồng có nhanh hơn không? Số luồng bao nhiêu là đủ?](#2-máy-1-cpu-chạy-đa-luồng-có-nhanh-hơn-không-số-luồng-bao-nhiêu-là-đủ)
3. [Đa luồng (Multi-threading) khác gì Đa tiến trình (Multi-processing)?](#3-đa-luồng-multi-threading-khác-gì-đa-tiến-trình-multi-processing)
4. [Cách tạo luồng bằng Thread và Runnable](#4-cách-tạo-luồng-bằng-thread-và-runnable)
5. [Quản lý nhiều luồng bằng Executor (Thread Pool)](#5-quản-lý-nhiều-luồng-bằng-executor-thread-pool)
6. [Executor: Lập lịch chạy (ScheduledExecutorService)](#6-executor-lập-lịch-chạy-scheduledexecutorservice)
7. [Sử dụng Callable và lấy kết quả với Future](#7-sử-dụng-callable-và-lấy-kết-quả-với-future)
8. [Synchronized, Locking và Atomic](#8-synchronized-locking-và-atomic)
9. [Collection Thread-safe và ConcurrentHashMap](#9-collection-thread-safe-và-concurrenthashmap)

---

## 1. Tại sao cần lập trình đa luồng?
Trong lập trình đồng bộ (tuần tự), dòng lệnh 2 phải đợi dòng lệnh 1 chạy xong. Nếu dòng lệnh 1 là một tác vụ rất tốn thời gian (như gọi API, tải file, đọc database), toàn bộ ứng dụng sẽ bị **"đứng" (treo UI)**.

Lập trình đa luồng giúp ứng dụng **thực hiện nhiều công việc cùng một lúc**. 
*Ví dụ:* Trình duyệt web vừa tải xuống file (Luồng 1), vừa cho phép bạn cuộn trang đọc báo (Luồng 2) và vừa phát nhạc (Luồng 3).

## 2. Máy 1 CPU chạy đa luồng có nhanh hơn không? Số luồng bao nhiêu là đủ?
### 2.1 Máy 1 CPU (1 Core) chạy đa luồng có nhanh hơn không?
**Câu trả lời:** Phụ thuộc vào loại công việc (Tác vụ):
- **Tác vụ tính toán (CPU-bound)** (như nén video, tính toán ma trận): **KHÔNG NHANH HƠN**. Thậm chí còn chậm đi vì CPU phải tốn thời gian chuyển đổi ngữ cảnh (Context Switching) giữa các luồng.
- **Tác vụ chờ đợi (I/O-bound)** (như đọc/ghi file, gọi mạng, chờ Database): **NHANH HƠN RẤT NHIỀU**. Khi Luồng 1 phải dừng lại để "chờ" mạng tải dữ liệu về (CPU rảnh rỗi), CPU sẽ lập tức chuyển sang chạy Luồng 2, giúp tận dụng tối đa thời gian rảnh của CPU.

### 2.2 Sử dụng bao nhiêu luồng là đủ?
Công thức tối ưu phổ biến: `Số luồng tối ưu = Số lượng Core CPU * (1 + Thời gian chờ / Thời gian tính toán)`
- Với tác vụ **CPU-bound**: Số luồng = Số Core CPU. (Hoặc `Core + 1`).
- Với tác vụ **I/O-bound**: Số luồng = Hàng chục hoặc hàng trăm luồng (Tùy vào thời gian luồng phải ngủ chờ I/O dài hay ngắn).

## 3. Đa luồng (Multi-threading) khác gì Đa tiến trình (Multi-processing)?

| Tiêu chí | Process (Tiến trình) | Thread (Luồng) |
|---|---|---|
| **Khái niệm** | Là một chương trình đang chạy (Ví dụ: 1 phần mềm Chrome đang mở). | Là 1 đơn vị thực thi nhỏ nhất nằm **bên trong** một Process. |
| **Không gian bộ nhớ** | Mỗi tiến trình có một vùng nhớ **ĐỘC LẬP**. (App A không thể đọc biến của App B). | Các luồng trong cùng 1 tiến trình **CHIA SẺ** chung vùng nhớ (Heap) của tiến trình đó. |
| **Tốc độ tạo/hủy** | Chậm, tốn tài nguyên hệ điều hành. | Rất nhanh (Được gọi là Lightweight process). |
| **Giao tiếp** | Phức tạp (IPC - Interprocess Communication). | Cực kỳ dễ dàng (Thông qua các biến dùng chung). |
| **Sự cố** | Tiến trình A chết không ảnh hưởng tới Tiến trình B. | Một luồng bị lỗi văng Exception chưa được catch có thể làm chết toàn bộ Tiến trình (Tắt luôn App). |

---

## 4. Cách tạo luồng bằng Thread và Runnable

Có 2 cách truyền thống để tạo luồng trong Java. Ngày nay, **Cách 2 (Runnable)** được dùng tới 99% vì Java không cho đa kế thừa, nếu `extends Thread` thì sẽ không thể extends class khác được nữa.

```java
// CÁCH 1: Kế thừa class Thread
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Luồng 1 đang chạy: " + Thread.currentThread().getName());
    }
}

// CÁCH 2: Implements interface Runnable (KHUYÊN DÙNG)
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Luồng 2 đang chạy: " + Thread.currentThread().getName());
    }
}

public class ThreadDemo {
    public static void main(String[] args) {
        // Khởi chạy Cách 1
        MyThread t1 = new MyThread();
        t1.start(); // Bắt buộc gọi start(), NẾU GỌI run() THÌ CHỈ LÀ HÀM BÌNH THƯỜNG

        // Khởi chạy Cách 2
        Thread t2 = new Thread(new MyRunnable());
        t2.start();

        // Cách 2.1: Dùng Lambda (Cực kỳ ngắn gọn)
        Thread t3 = new Thread(() -> {
            System.out.println("Luồng 3 đang chạy: " + Thread.currentThread().getName());
        });
        t3.start();
        
        System.out.println("Luồng chính (Main) đã kết thúc lệnh khởi tạo.");
    }
}
```

---

## 5. Quản lý nhiều luồng bằng Executor (Thread Pool)

**Vấn đề:** Nếu ta có 10,000 công việc, tạo ra 10,000 cái `new Thread()` sẽ làm sập RAM và cháy CPU (Vì chi phí tạo Thread rất tốn kém).
**Giải pháp:** Dùng **Thread Pool (Hồ chứa luồng)** thông qua `ExecutorService`. Ta chỉ tạo tối đa (ví dụ 10 luồng). 10,000 công việc sẽ được bỏ vào 1 hàng đợi (Queue). 10 luồng này sẽ lấy lần lượt từng việc ra làm. Ai làm xong không bị hủy mà quay lại lấy việc tiếp theo.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolDemo {
    public static void main(String[] args) {
        // Tạo Thread Pool với số luồng TỐI ĐA là 3
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Ném vào hồ 10 công việc
        for (int i = 1; i <= 10; i++) {
            final int taskId = i;
            executor.submit(() -> {
                System.out.println("Đang xử lý Task " + taskId + " bởi " + Thread.currentThread().getName());
                try {
                    Thread.sleep(1000); // Giả lập việc nặng mất 1s
                } catch (InterruptedException e) { }
            });
        }

        // Đóng Executor (Không nhận thêm việc, chờ làm xong việc cũ rồi tắt các luồng)
        executor.shutdown(); 
        System.out.println("Main thread đã giao xong 10 công việc.");
        
        // Kết quả chạy: Luôn luôn chỉ có TỐI ĐA 3 luồng (pool-1-thread-1,2,3) chạy cùng lúc.
    }
}
```

---

## 6. Executor: Lập lịch chạy (ScheduledExecutorService)

Dùng để chạy các tác vụ có tính định kỳ (Giống hàm `setInterval` hay `setTimeout` trong JS).

```java
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class ScheduledDemo {
    public static void main(String[] args) {
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);

        // 1. Chạy 1 lần duy nhất sau X giây trễ (VD: Sau 3 giây)
        scheduler.schedule(() -> {
            System.out.println("Tin nhắn nổ chậm (Sau 3s)");
        }, 3, TimeUnit.SECONDS);

        // 2. Lập lịch chạy ĐỊNH KỲ (Lặp đi lặp lại)
        // Thông số: Task, Trễ_ban_đầu, Khoảng_cách_lặp, Đơn_vị_thời_gian
        scheduler.scheduleAtFixedRate(() -> {
            System.out.println("Ping... Cứ mỗi 5s chạy một lần");
        }, 1, 5, TimeUnit.SECONDS);
        
        // Lưu ý: Đừng gọi scheduler.shutdown() ngay nếu muốn nó chạy lặp lại mãi mãi.
    }
}
```

---

## 7. Sử dụng Callable và lấy kết quả với Future

- `Runnable` không có giá trị trả về (`void`).
- `Callable<T>` dùng cho đa luồng nhưng **CÓ THỂ TRẢ VỀ KẾT QUẢ** kiểu `T` và **CÓ THỂ NÉM EXCEPTION**.
- `Future` là cái vỏ hộp, dùng để chứa kết quả của Callable trong tương lai (vì khi luồng khác đang chạy, ta chưa có kết quả ngay).

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.*;

public class CallableDemo {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        
        // List chứa các "Tương lai"
        List<Future<Integer>> results = new ArrayList<>();

        for (int i = 1; i <= 3; i++) {
            final int number = i * 10;
            
            // Khai báo Callable trả về số Integer
            Callable<Integer> task = () -> {
                System.out.println("Tính toán " + number + " (" + Thread.currentThread().getName() + ")");
                Thread.sleep(2000); // Giả lập tính toán mất 2s
                return number * 2;
            };
            
            // Gửi Callable vào Executor, nó trả về 1 cái vỏ Future ngay lập tức
            Future<Integer> future = executor.submit(task);
            results.add(future); 
        }

        System.out.println("Đã gửi hết task. Đi làm việc khác...");

        // Chờ và LẤY KẾT QUẢ từ nhiều luồng
        int totalSum = 0;
        for (Future<Integer> future : results) {
            try {
                // Hàm get() SẼ BỊ CHẶN (BLOCK) cho đến khi luồng đó xử lý xong.
                int value = future.get(); 
                System.out.println("Lấy được kết quả: " + value);
                totalSum += value;
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        
        System.out.println("Tổng tất cả các luồng trả về là: " + totalSum);
        executor.shutdown();
    }
}
```

---

## 8. Synchronized, Locking và Atomic

**Tình huống (Race Condition - Tình trạng tương tranh):** Nếu 2 luồng cùng lúc đọc và tăng biến `count` lên 1. Lẽ ra biến phải là 2, nhưng do đọc cùng lúc `count=0`, cả 2 cùng gán `count = 0 + 1 = 1`. Kết quả bị mất mát dữ liệu (Count = 1).

### 8.1 Từ khóa `synchronized` (Khóa đồng bộ)
Đảm bảo tại 1 thời điểm, **chỉ có duy nhất 1 luồng** được phép chui vào hàm/khối code này. Luồng khác muốn vào phải đứng xếp hàng chờ luồng trước đi ra.

```java
class Counter {
    private int count = 0;

    // Đặt synchronized vào hàm
    public synchronized void increment() {
        count++; 
    }
    
    public int getCount() { return count; }
}
```

### 8.2 Lock (`ReentrantLock`)
Linh hoạt hơn `synchronized`. Cho phép Khóa (`lock()`) và Mở khóa (`unlock()`) ở các vị trí tùy ý. Tuy nhiên luôn phải nhớ `unlock()` trong khối `finally` để tránh Deadlock (Chết kẹt).

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

class LockCounter {
    private int count = 0;
    private Lock lock = new ReentrantLock();

    public void increment() {
        lock.lock(); // Xin chìa khóa
        try {
            count++;
        } finally {
            lock.unlock(); // CHẮC CHẮN phải trả lại chìa khóa dù có Exception
        }
    }
}
```

### 8.3 Atomic Variables (Biến nguyên tử)
Là cách TỐT NHẤT và NHANH NHẤT để đếm số an toàn trong đa luồng. Bên dưới nó dùng thuật toán **CAS (Compare-And-Swap)** của CPU phần cứng chứ không cần cấp phát/chờ chìa khóa như khóa Lock (được gọi là Khóa không khóa - Lock-free).

```java
import java.util.concurrent.atomic.AtomicInteger;

class AtomicCounter {
    // Khai báo biến nguyên tử
    private AtomicInteger count = new AtomicInteger(0);

    public void increment() {
        count.incrementAndGet(); // Tương đương ++count nhưng thread-safe 100%
    }
}
```

---

## 9. Collection Thread-safe và ConcurrentHashMap

Các Collection ở Phần 7 như `ArrayList`, `HashMap`, `HashSet` **đều KHÔNG an toàn** trong môi trường Đa luồng (Not Thread-Safe). Nếu nhiều luồng cùng thêm sửa xóa, nó sẽ văng `ConcurrentModificationException` hoặc lỗi cấu trúc (Mất node, lặp vô tận).

### Giải pháp 1: Gói nó vào hàm đồng bộ (Chậm)
Dùng `Collections.synchronizedList()` hoặc `Collections.synchronizedMap()`.
- **Nhược điểm:** Hiệu năng rất tồi, vì nó khóa TOÀN BỘ cái danh sách. Dù 1 người ghi ở đầu, người ghi ở cuối cũng phải đứng đợi nhau.

### Giải pháp 2: Sử dụng `java.util.concurrent` (Cực Nhanh)
Java cung cấp bộ sưu tập được thiết kế riêng cho Đa luồng: `CopyOnWriteArrayList` và `ConcurrentHashMap`.

**ConcurrentHashMap:**
Được mệnh danh là siêu sao trong giới Collection. 
Thay vì khóa toàn bộ Map, nó sử dụng kỹ thuật **Lock Striping** (Khóa theo phân đoạn/bucket). 
- Nghĩa là: Nếu có 16 cái ngăn kéo (buckets), và Luồng A đang ghi vào ngăn kéo số 1, thì Khóa của ngăn 1 bị đóng lại. Tuy nhiên, Luồng B hoàn toàn có thể cùng lúc ghi vào ngăn kéo số 2 mà không phải chờ đợi Luồng A.
- Đặc biệt, thao tác Đọc (`get`) hầu như không bị Lock.

```java
import java.util.concurrent.ConcurrentHashMap;
import java.util.Map;

public class ConcurrentMapDemo {
    public static void main(String[] args) {
        // Sử dụng thay cho HashMap khi có nhiều luồng
        Map<String, Integer> map = new ConcurrentHashMap<>();
        
        map.put("A", 100);
        map.put("B", 200);
        
        // Phương thức cực kỳ tiện lợi: putIfAbsent (Thêm nếu chưa tồn tại)
        // Hàm này chạy an toàn tuyệt đối trong đa luồng mà không sợ đè giá trị
        map.putIfAbsent("A", 999); // Sẽ KHÔNG thêm vì A đã có rồi
        
        System.out.println(map.get("A")); // Vẫn là 100
    }
}
```

---

> **📌 Kết thúc Phần 8: Lập trình Đa luồng (Multi-threading)**

---

# Phần 9: Lập trình Lambda (Java 8)

## 📌 Mục lục
1. [Functional Interface là gì?](#1-functional-interface-là-gì)
2. [Cấu trúc của một Lambda Expression](#2-cấu-trúc-của-một-lambda-expression)
3. [Viết lại Thread (Runnable) bằng Lambda](#3-viết-lại-thread-runnable-bằng-lambda)
4. [Cách viết một Custom Functional Interface](#4-cách-viết-một-custom-functional-interface)

---

## 1. Functional Interface là gì?
Trước Java 8, muốn truyền một khối lệnh (function) vào một hàm khác, ta phải tạo một đối tượng từ một Interface (dùng class ẩn danh - Anonymous Class). Điều này làm code rất rườm rà.

Để hỗ trợ viết code ngắn gọn (Lambda), Java giới thiệu khái niệm **Functional Interface**.
**Định nghĩa:** Functional Interface là một Interface **CHỈ CÓ DUY NHẤT 1 PHƯƠNG THỨC TRỪU TƯỢNG (Abstract Method)**. 

> 💡 **Lưu ý:**
> - Nó có thể chứa bao nhiêu phương thức `default` hoặc `static` tùy ý, miễn là chỉ có 1 phương thức chưa được triển khai (abstract).
> - Thường được đánh dấu bằng Annotation `@FunctionalInterface` để báo cho trình biên dịch kiểm tra (nếu bạn lỡ viết 2 hàm abstract nó sẽ báo lỗi ngay).
> - Các interface nổi tiếng trong Java là Functional Interface: `Runnable` (chỉ có hàm `run()`), `Callable` (chỉ có hàm `call()`), `Comparator` (chỉ có hàm `compare()`).

## 2. Cấu trúc của một Lambda Expression
Lambda Expression thực chất là **cách viết tắt để triển khai cái hàm duy nhất** của một Functional Interface.

### Cú pháp chung:
```java
(danh_sách_tham_số) -> { thân_hàm_xử_lý }
```

### Các quy tắc rút gọn:
1. **Không cần khai báo kiểu dữ liệu** của tham số (Trình biên dịch tự hiểu).
2. **Nếu chỉ có 1 tham số**, có thể bỏ luôn dấu ngoặc đơn `()`.
3. **Nếu thân hàm chỉ có 1 dòng lệnh**, có thể bỏ dấu ngoặc nhọn `{}` và từ khóa `return`.

### Ví dụ các biến thể:
```java
// 1. Không có tham số
() -> System.out.println("Hello Lambda");

// 2. Có 1 tham số (Bỏ ngoặc đơn)
name -> System.out.println("Hello " + name);

// 3. Có nhiều tham số
(a, b) -> {
    int sum = a + b;
    return sum;
}

// 4. Có nhiều tham số nhưng thân hàm chỉ có 1 dòng (Rút gọn chữ return)
(a, b) -> a + b;
```

---

## 3. Viết lại Thread (Runnable) bằng Lambda

`Runnable` là một Functional Interface vì nó chỉ có đúng 1 hàm `void run()`. Do đó, thay vì viết Class ẩn danh rườm rà, ta có thể thay thế hoàn toàn bằng Lambda.

```java
public class LambdaThreadDemo {
    public static void main(String[] args) {
        
        // ==========================================
        // CÁCH CŨ: DÙNG ANONYMOUS CLASS (Trước Java 8)
        // ==========================================
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("Luồng 1 đang chạy bằng Anonymous Class");
            }
        });
        t1.start();

        // ==========================================
        // CÁCH MỚI: DÙNG LAMBDA (Từ Java 8 trở đi)
        // ==========================================
        // Vì Runnable chỉ có hàm run() không nhận tham số (), và trả về void
        // Nên cấu trúc Lambda của nó sẽ là: () -> { ... }
        Thread t2 = new Thread(() -> {
            System.out.println("Luồng 2 đang chạy bằng Lambda (Nhiều dòng code)");
            System.out.println("Rất gọn gàng!");
        });
        t2.start();

        // Nếu hàm run() chỉ có 1 dòng code, rút gọn tối đa:
        Thread t3 = new Thread(() -> System.out.println("Luồng 3 chạy siêu tốc (1 dòng)"));
        t3.start();
    }
}
```

---

## 4. Cách viết một Custom Functional Interface

Bạn hoàn toàn có thể tự định nghĩa một Functional Interface của riêng mình để phục vụ cho các logic tính toán (ví dụ: Công thức tính lương, Thuật toán mã hóa...) và truyền nó như một tham số (Callback).

### Bước 1: Định nghĩa Functional Interface
```java
@FunctionalInterface // Khuyên dùng để trình biên dịch kiểm soát lỗi
interface MathOperation {
    // Chỉ có DUY NHẤT 1 hàm chưa triển khai
    int calculate(int a, int b); 
    
    // Vẫn được phép có hàm default
    default void printInfo() {
        System.out.println("Đây là một phép toán.");
    }
}
```

### Bước 2: Sử dụng Interface với Lambda
```java
public class CustomLambdaDemo {
    
    // Viết một hàm nhận Functional Interface làm tham số
    // Đây là kĩ thuật truyền HÀM VÀO TRONG HÀM (Higher-order function)
    public static int operate(int a, int b, MathOperation mathOp) {
        return mathOp.calculate(a, b);
    }

    public static void main(String[] args) {
        
        // 1. Định nghĩa phép CỘNG (Thân hàm: a + b)
        MathOperation addition = (a, b) -> a + b;
        
        // 2. Định nghĩa phép TRỪ (Thân hàm: a - b)
        MathOperation subtraction = (a, b) -> a - b;
        
        // 3. Định nghĩa phép NHÂN (Nhiều dòng code)
        MathOperation multiplication = (x, y) -> {
            System.out.println("Đang thực hiện phép nhân...");
            return x * y;
        };

        // GỌI HÀM VÀ TRUYỀN LAMBDA VÀO
        System.out.println("10 + 5 = " + operate(10, 5, addition));       // 15
        System.out.println("10 - 5 = " + operate(10, 5, subtraction));    // 5
        System.out.println("10 * 5 = " + operate(10, 5, multiplication)); // 50
        
        // Thậm chí truyền thẳng Lambda vào hàm mà không cần lưu biến
        System.out.println("10 / 2 = " + operate(10, 2, (a, b) -> a / b)); // 5
    }
}
```

### So sánh tại sao Lambda lại mạnh mẽ?
- **Nếu không có Lambda:** Với mỗi phép toán (Cộng, Trừ, Nhân, Chia), bạn sẽ phải tạo ra 4 class riêng biệt (hoặc 4 cục Anonymous Class dài dòng) chỉ để `implements MathOperation`.
- **Có Lambda:** Bạn chỉ cần truyền trực tiếp cái **công thức tính** (`a + b`, `a - b`) vào hàm `operate()`. Code tập trung 100% vào nghiệp vụ (Logic) thay vì lãng phí vào các thẻ Boilerplate code của OOP truyền thống.

---

> **📌 Kết thúc Phần 9: Lập trình Lambda**
>
> **📌 Kết thúc Phần 9: Lập trình Lambda**

---

# Phần 10: Các Vấn Đề Nâng Cao (Generics, Javadoc, Inner Class, Properties)

## 📌 Mục lục
1. [Generics (Kiểu dữ liệu trừu tượng)](#1-generics-kiểu-dữ-liệu-trừu-tượng)
2. [Cách viết Javadoc chuẩn](#2-cách-viết-javadoc-chuẩn)
3. [Inner Class (Lớp lồng nhau)](#3-inner-class-lớp-lồng-nhau)
4. [Tìm hiểu thêm về Properties và System Properties](#4-tìm-hiểu-thêm-về-properties-và-system-properties)

---

## 1. Generics (Kiểu dữ liệu trừu tượng)

**Generics** cho phép bạn định nghĩa các Class, Interface, hoặc Method với **kiểu dữ liệu là tham số** (Tham số hóa kiểu). Khái niệm này xuất hiện rất nhiều trong Collections (Ví dụ: `List<String>`, `Map<K, V>`).

**Lợi ích của Generics:**
1. **An toàn kiểu (Type-Safety):** Báo lỗi ngay lúc gõ code (Compile-time) nếu truyền sai kiểu, thay vì bị văng lỗi `ClassCastException` lúc đang chạy (Runtime).
2. **Loại bỏ ép kiểu (Casting):** Không cần phải ép kiểu thủ công từ `Object` về `String` hay `Integer`.

### 1.1 Generic Class (Lớp Generic)
Sử dụng kí hiệu hình thoi `< >`. Chữ cái bên trong là tự do, nhưng quy ước chung là: `T` (Type), `E` (Element), `K` (Key), `V` (Value).

```java
// Khai báo một lớp "Hộp" có thể chứa BẤT KỲ kiểu dữ liệu nào
class Box<T> {
    private T item;
    
    public void setItem(T item) { this.item = item; }
    public T getItem() { return item; }
}

public class GenericDemo {
    public static void main(String[] args) {
        // Hộp chứa số nguyên
        Box<Integer> intBox = new Box<>();
        intBox.setItem(100);
        int val = intBox.getItem(); // KHÔNG CẦN ÉP KIỂU: (Integer) intBox.getItem();

        // Hộp chứa chuỗi
        Box<String> strBox = new Box<>();
        strBox.setItem("Hello");
    }
}
```

### 1.2 Generic Method (Phương thức Generic)
Bạn có thể dùng Generic cho 1 phương thức duy nhất mà không cần cả Class phải là Generic.

```java
public class GenericMethod {
    // Kí hiệu <T> phải đặt trước kiểu trả về (void)
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3};
        String[] strArray = {"A", "B", "C"};

        printArray(intArray); // 1 2 3
        printArray(strArray); // A B C
    }
}
```

### 1.3 Ký tự đại diện Wildcard (`?`)
- `<?>`: Không giới hạn kiểu.
- `<? extends Number>` (Upper Bounded): Chỉ chấp nhận Number hoặc con của Number (Ví dụ: Integer, Double).
- `<? super Integer>` (Lower Bounded): Chỉ chấp nhận Integer hoặc cha của Integer (Ví dụ: Number, Object).

---

## 2. Cách viết Javadoc chuẩn

**Javadoc** là hệ thống công cụ giúp tự động tạo tài liệu HTML từ các comment đặc biệt trong mã nguồn Java.

### 2.1 Cú pháp Javadoc
Comment Javadoc bắt đầu bằng `/**` và kết thúc bằng `*/`. Thường được đặt ở trên khai báo Class, Field, hoặc Method.

| Thẻ (Tag) | Ý nghĩa |
|---|---|
| `@author` | Tên tác giả |
| `@version` | Phiên bản |
| `@since` | Tính năng này có từ phiên bản nào |
| `@param` | Giải thích tham số đầu vào của hàm |
| `@return` | Giải thích dữ liệu trả về của hàm |
| `@throws` | Liệt kê các Exception mà hàm có thể ném ra |
| `@deprecated` | Đánh dấu hàm/class này đã cũ, không nên dùng nữa |

### 2.2 Ví dụ đầy đủ

```java
/**
 * Lớp đại diện cho một Máy tính điện tử.
 * Cung cấp các phép toán số học cơ bản.
 * 
 * @author Nguyen Van A
 * @version 1.0
 * @since 2026-06
 */
public class Calculator {

    /**
     * Thực hiện phép chia hai số nguyên.
     * 
     * @param a Số bị chia
     * @param b Số chia
     * @return Kết quả phép chia của a cho b
     * @throws ArithmeticException Nếu số chia b bằng 0
     * @deprecated Hãy sử dụng hàm divideDouble() thay thế để tránh làm tròn
     */
    @Deprecated
    public int divide(int a, int b) throws ArithmeticException {
        if (b == 0) {
            throw new ArithmeticException("Không thể chia cho 0");
        }
        return a / b;
    }
}
```
*Lưu ý:* Hầu hết các IDE (Eclipse, IntelliJ) đều hỗ trợ xuất Javadoc thành một trang web tài liệu (giống hệt trang docs của Oracle) chỉ bằng 1 cú click chuột (Tool -> Generate Javadoc).

---

## 3. Inner Class (Lớp lồng nhau)

Inner Class là việc khai báo **một Class bên trong một Class khác**. Có 4 loại Inner Class chính:

### 3.1 Non-static Inner Class (Lớp lồng thông thường)
- Gắn liền với đối tượng (Object) của lớp ngoài (Outer Class).
- Có thể truy cập thoải mái các biến `private` của lớp ngoài.

```java
class Outer {
    private String secret = "Bí mật Outer";

    class Inner {
        void show() {
            System.out.println("Truy cập từ Inner: " + secret);
        }
    }
}

public class TestInner {
    public static void main(String[] args) {
        // Phải tạo Outer trước thì mới tạo được Inner
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.show();
    }
}
```

### 3.2 Static Nested Class (Lớp lồng tĩnh)
- Khai báo bằng từ khóa `static`. Không gắn với đối tượng Outer.
- Khởi tạo trực tiếp không cần tạo Outer: `Outer.Inner obj = new Outer.Inner();`

### 3.3 Local Inner Class (Lớp lồng trong hàm)
- Được định nghĩa **bên trong một phương thức** (hàm). Phạm vi sử dụng chỉ nằm gọn trong hàm đó. (Rất ít dùng).

### 3.4 Anonymous Inner Class (Lớp ẩn danh)
- Không có tên, dùng để **kế thừa/triển khai một Class/Interface và tạo luôn 1 object** ngay tại chỗ. (Đã học ở phần Lambda).
- Ứng dụng nhiều nhất trong lập trình giao diện (Bắt sự kiện onClick của nút bấm).

```java
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Chạy bằng Anonymous Class");
    }
};
```

---

## 4. Tìm hiểu thêm về Properties và System Properties

> Về thao tác Đọc/Ghi file `config.properties`, bạn có thể xem lại **Phần 6 - Mục 5**. 
> Tuy nhiên, `Properties` còn một ứng dụng cực kì mạnh mẽ khác: **System Properties (Thuộc tính Hệ thống)**.

Khi Java chạy, JVM sẽ khởi tạo sẵn một bảng `Properties` chứa mọi thông tin của hệ điều hành và môi trường chạy.

### Code lấy thông tin Hệ thống:
```java
import java.util.Properties;

public class SystemPropertiesDemo {
    public static void main(String[] args) {
        // 1. Lấy toàn bộ thuộc tính của Hệ thống
        Properties sysProps = System.getProperties();
        
        // In ra tất cả (rất dài)
        // sysProps.list(System.out); 
        
        // 2. Lấy các thông số phổ biến
        System.out.println("--- THÔNG TIN HỆ THỐNG ---");
        System.out.println("Hệ điều hành: " + System.getProperty("os.name"));
        System.out.println("Phiên bản OS: " + System.getProperty("os.version"));
        System.out.println("Tên User máy tính: " + System.getProperty("user.name"));
        
        System.out.println("\n--- THÔNG TIN JAVA ---");
        System.out.println("Phiên bản Java: " + System.getProperty("java.version"));
        System.out.println("Thư mục cài Java: " + System.getProperty("java.home"));
        
        System.out.println("\n--- THÔNG TIN THƯ MỤC ---");
        System.out.println("Thư mục hiện tại (CWD): " + System.getProperty("user.dir"));
        
        // 3. Tự truyền Property từ Terminal lúc chạy code
        // Chạy lệnh: java -DmyEnv="Production" SystemPropertiesDemo
        String myEnv = System.getProperty("myEnv", "Chưa cài đặt");
        System.out.println("\nBiến tự truyền (myEnv): " + myEnv);
    }
}
```
**Ứng dụng thực tế:** Khi chạy ứng dụng trên Docker/Server Linux, ta thường truyền các thông số môi trường qua cờ `-D` (Ví dụ `-Dspring.profiles.active=dev`) lúc khởi động ứng dụng Java để thay đổi cấu hình app mà không cần sửa code.

---

> **📌 KẾT THÚC CÁC PHẦN TRƯỚC**

---

# Phần 11: Tính Năng Mới Java 8 (Stream API, Optional, Method Reference)

## 📌 Mục lục
1. [Default Method trong Interface](#1-default-method-trong-interface)
2. [Method Reference (Tham chiếu phương thức)](#2-method-reference-tham-chiếu-phương-thức)
3. [4 Cột trụ Functional Interface (Predicate, Consumer, Supplier, Function)](#3-4-cột-trụ-functional-interface-predicate-consumer-supplier-function)
4. [Lớp Optional - Khắc tinh của NullPointerException](#4-lớp-optional---khắc-tinh-của-nullpointerexception)
5. [Stream API toàn tập (Map, Filter, Collect, GroupBy, Statistics)](#5-stream-api-toàn-tập-map-filter-collect-groupby-statistics)
6. [Xử lý song song với Parallel Stream](#6-xử-lý-song-song-với-parallel-stream)

---

## 1. Default Method trong Interface

Trước Java 8, mọi phương thức trong Interface bắt buộc phải rỗng (chỉ có chữ ký hàm). Nhưng từ Java 8, Interface được phép có các **phương thức có sẵn thân hàm**, gọi là `default method`.

**Mục đích:** Giúp mở rộng Interface (thêm tính năng mới) mà KHÔNG làm vỡ code của các Class cũ đã implements Interface đó.

```java
interface Vehicle {
    void start(); // Abstract method cũ
    
    // Default method (Đã có thân hàm)
    default void honk() {
        System.out.println("Beep beep!");
    }
}

class Car implements Vehicle {
    @Override
    public void start() { System.out.println("Car started"); }
    // Không BẮT BUỘC phải Override hàm honk()
}

public class DefaultMethodDemo {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start();
        myCar.honk(); // Kế thừa thẳng từ Interface
    }
}
```

---

## 2. Method Reference (Tham chiếu phương thức)

Đây là phiên bản **"Rút gọn cực độ" của Lambda Expression**. Khi một Lambda chỉ làm duy nhất 1 việc là GỌI LẠI một phương thức đã có sẵn, ta dùng dấu `::` để trỏ thẳng tới hàm đó.

Có 4 loại Method Reference:
1. `ClassName::staticMethod` (Trỏ đến hàm Static)
2. `instance::instanceMethod` (Trỏ đến hàm của một Object cụ thể)
3. `ClassName::instanceMethod` (Trỏ đến hàm của 1 kiểu đối tượng)
4. `ClassName::new` (Trỏ đến Constructor)

```java
import java.util.Arrays;
import java.util.List;

public class MethodRefDemo {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Anna", "Bob", "Charlie");

        // 1. Cách dùng Lambda (Thường)
        names.forEach(name -> System.out.println(name));

        // 2. Cách dùng Method Reference (Ngắn gọn tuyệt đối)
        // Thay vì truyền tham số 'name' rồi gọi hàm println, ta Trỏ thẳng tới hàm println
        names.forEach(System.out::println);
    }
}
```

---

## 3. 4 Cột trụ Functional Interface (Predicate, Consumer, Supplier, Function)

Để hỗ trợ Stream API, Java cung cấp sẵn 4 Functional Interface "Trấn phái" trong package `java.util.function`:

| Interface | Dữ liệu VÀO | Dữ liệu RA | Mục đích sử dụng | Hàm thực thi |
|---|---|---|---|---|
| **`Predicate<T>`** | 1 Tham số `T` | `boolean` | Kiểm tra điều kiện (Lọc dữ liệu) | `test(T)` |
| **`Consumer<T>`** | 1 Tham số `T` | `void` | Xử lý nhưng không trả về gì (In ra) | `accept(T)` |
| **`Supplier<T>`** | *Không có* | `T` | Trả về một đối tượng mới (Cung cấp) | `get()` |
| **`Function<T, R>`** | 1 Tham số `T` | Đối tượng `R` | Nhận vào kiểu này, Trả về kiểu khác | `apply(T)` |

### Ví dụ từng loại:
```java
import java.util.function.*;

public class CoreFunctionalDemo {
    public static void main(String[] args) {
        
        // 1. Predicate (Nhận int, Trả boolean) -> Kiểm tra chẵn lẻ
        Predicate<Integer> isEven = num -> num % 2 == 0;
        System.out.println("Là số chẵn? " + isEven.test(10)); // true

        // 2. Consumer (Nhận String, Không trả về) -> In ra màn hình
        Consumer<String> printer = text -> System.out.println("Xin chào " + text);
        printer.accept("Admin");

        // 3. Supplier (Không nhận, Trả String) -> Random dữ liệu
        Supplier<Double> randomGen = () -> Math.random();
        System.out.println("Random: " + randomGen.get());

        // 4. Function (Nhận String, Trả Integer) -> Tính độ dài chuỗi
        Function<String, Integer> lengthFunc = str -> str.length();
        System.out.println("Độ dài chữ 'Java': " + lengthFunc.apply("Java"));
    }
}
```

---

## 4. Lớp Optional - Khắc tinh của NullPointerException

Tránh việc ứng dụng sập do biến bị `null`. `Optional` giống như một **Chiếc hộp**, nó có thể CÓ chứa giá trị (Present) hoặc KHÔNG chứa gì (Empty). Bạn phải mở hộp ra kiểm tra một cách an toàn.

```java
import java.util.Optional;

public class OptionalDemo {
    public static void main(String[] args) {
        String dbResult = null; // Giả sử query DB không ra dữ liệu
        
        // Bọc dữ liệu vào hộp Optional. Tự động nhận diện Null
        Optional<String> opt = Optional.ofNullable(dbResult);

        // 1. Kiểm tra An Toàn (Thay thế cho: if (dbResult != null) )
        opt.ifPresent(val -> System.out.println("Dữ liệu là: " + val));

        // 2. Cung cấp giá trị Mặc Định (Nếu rỗng thì xài cái này)
        String finalName = opt.orElse("Khách Vô Danh");
        System.out.println("Tên: " + finalName); // Sẽ in ra "Khách Vô Danh" vì opt rỗng

        // 3. Ném Exception nếu rỗng
        // String mustHave = opt.orElseThrow(() -> new RuntimeException("Lỗi: Không tìm thấy!"));
    }
}
```

---

## 5. Stream API toàn tập (Map, Filter, Collect, GroupBy, Statistics)

**Stream** là cách duyệt và thao tác với Collection theo phong cách **Tuyên bố (Declarative)**. Bạn chỉ cần nói với Java "TÔI MUỐN GÌ" (Ví dụ: Lọc sinh viên điểm > 5) thay vì viết vòng lặp For dài dòng "TÔI LÀM NHƯ THẾ NÀO".

- **Trung gian (Intermediate):** `filter`, `map`, `sorted` (Trả về một Stream mới, có thể chain tiếp).
- **Kết thúc (Terminal):** `collect`, `forEach`, `count` (Trả về dữ liệu thật, đóng Stream).

```java
import java.util.*;
import java.util.stream.Collectors;

class SinhVien {
    String ten, lop;
    double diem;
    public SinhVien(String t, String l, double d) { ten=t; lop=l; diem=d; }
    public String getTen() { return ten; }
    public String getLop() { return lop; }
    public double getDiem() { return diem; }
    @Override public String toString() { return ten + "-" + diem; }
}

public class StreamAPIDemo {
    public static void main(String[] args) {
        List<SinhVien> list = Arrays.asList(
            new SinhVien("An", "IT1", 8.5),
            new SinhVien("Bình", "IT2", 4.0),
            new SinhVien("Cường", "IT1", 9.0),
            new SinhVien("Dũng", "IT2", 6.5)
        );

        // =====================================
        // 1. FILTER (Lọc) & COLLECT (Gom lại)
        // =====================================
        // Lấy danh sách Sinh Viên Đỗ (Điểm >= 5)
        List<SinhVien> passList = list.stream()
                .filter(sv -> sv.getDiem() >= 5.0)  // Dùng Predicate
                .collect(Collectors.toList());      // Gom thành List mới
        System.out.println("Đỗ: " + passList);

        // =====================================
        // 2. MAP (Biến đổi dữ liệu)
        // =====================================
        // Chỉ lấy ra 1 List chứa toàn "Tên" của các Sinh viên
        List<String> names = list.stream()
                .map(sv -> sv.getTen())  // Dùng Function (Biến SV -> String)
                // .map(SinhVien::getTen) // Dùng Method Reference
                .collect(Collectors.toList());
        System.out.println("Tên: " + names);

        // =====================================
        // 3. COUNT (Đếm)
        // =====================================
        long countIT1 = list.stream().filter(sv -> sv.getLop().equals("IT1")).count();
        System.out.println("Số SV IT1: " + countIT1);

        // =====================================
        // 4. GROUP BY (Nhóm dữ liệu lại theo key)
        // =====================================
        // Gom nhóm sinh viên theo "Lớp" (Map<String, List<SinhVien>>)
        Map<String, List<SinhVien>> groupedByLop = list.stream()
                .collect(Collectors.groupingBy(SinhVien::getLop));
        System.out.println("\nNhóm theo lớp:");
        groupedByLop.forEach((lop, svList) -> System.out.println(lop + ": " + svList));

        // =====================================
        // 5. STATISTICS (Thống kê toán học)
        // =====================================
        // Dùng mapToDouble để lấy ra các con số điểm, rồi tóm tắt (Max, Min, Sum, Avg)
        DoubleSummaryStatistics stats = list.stream()
                .mapToDouble(SinhVien::getDiem)
                .summaryStatistics();
        
        System.out.println("\n--- THỐNG KÊ ĐIỂM SỐ ---");
        System.out.println("Cao nhất: " + stats.getMax());
        System.out.println("Thấp nhất: " + stats.getMin());
        System.out.println("Trung bình: " + stats.getAverage());
    }
}
```

---

## 6. Xử lý song song với Parallel Stream

Nếu bạn có một List chứa 1 Triệu phần tử và muốn tăng tốc xử lý, bạn không cần tự viết Multi-threading rườm rà. Bạn chỉ cần đổi chữ `.stream()` thành `.parallelStream()`.

Java sẽ tự động xé cái List ra thành nhiều mảng nhỏ, chia cho các Core CPU xử lý đồng thời, rồi cuối cùng ráp kết quả lại.

```java
import java.util.ArrayList;
import java.util.List;

public class ParallelDemo {
    public static void main(String[] args) {
        List<String> bigList = new ArrayList<>();
        for (int i = 0; i < 1_000_000; i++) bigList.add("Item " + i);

        long start, end;

        // 1. Duyệt Tuần Tự (Chạy trên 1 Core)
        start = System.currentTimeMillis();
        long countNormal = bigList.stream()
                                  .filter(s -> s.contains("999"))
                                  .count();
        end = System.currentTimeMillis();
        System.out.println("Duyệt Tuần Tự mất: " + (end - start) + "ms");

        // 2. Duyệt Song Song (Chạy trên Toàn bộ Core CPU)
        start = System.currentTimeMillis();
        long countParallel = bigList.parallelStream() // << CÚ PHÁP THẦN THÁNH
                                    .filter(s -> s.contains("999"))
                                    .count();
        end = System.currentTimeMillis();
        System.out.println("Duyệt Song Song mất: " + (end - start) + "ms");
    }
}
```

> ⚠️ **Khi nào NÊN và KHÔNG NÊN dùng Parallel Stream?**
> - **NÊN DÙNG:** Khi số lượng phần tử cực lớn (> 100k) và công việc tính toán nặng (CPU-bound) không dính líu với nhau.
> - **KHÔNG NÊN DÙNG:** Khi List quá nhỏ (tạo luồng còn tốn thời gian hơn), hoặc khi các phần tử có sự lệ thuộc thứ tự, hoặc khi bạn gọi Database/API (I/O-bound) vì Thread Pool của Parallel có giới hạn chung, dễ làm treo cả hệ thống.

---

> **📌 Kết thúc Phần 11: Java 8 Stream API**

---

# Phần 12: Biểu thức chính quy (Regular Expression - Regex)

## 📌 Mục lục
1. [Khái niệm và Cú pháp (Syntax) Regex cơ bản](#1-khái-niệm-và-cú-pháp-syntax-regex-cơ-bản)
2. [Tìm hiểu Lớp Pattern và Matcher](#2-tìm-hiểu-lớp-pattern-và-matcher)
3. [Thực hành sử dụng Pattern & Matcher trong Java](#3-thực-hành-sử-dụng-pattern--matcher-trong-java)
4. [Tài liệu thực hành Regex](#4-tài-liệu-thực-hành-regex)

---

## 1. Khái niệm và Cú pháp (Syntax) Regex cơ bản

**Biểu thức chính quy (Regex - Regular Expression)** là một chuỗi ký tự đặc biệt dùng để mô tả một "mẫu" (pattern) tìm kiếm. Nó cực kỳ mạnh mẽ trong việc:
- **Xác thực (Validation):** Kiểm tra xem Email, Số điện thoại, Mật khẩu người dùng nhập vào có đúng định dạng không.
- **Tìm kiếm (Search) & Trích xuất (Extract):** Tìm tất cả các số điện thoại có trong một đoạn văn bản dài.
- **Thay thế (Replace):** Che giấu các từ nhạy cảm trong đoạn chat.

### Bảng các Syntax cơ bản nhất cần nhớ:

#### Nhóm ký tự đại diện (Metacharacters)
| Cú pháp | Ý nghĩa | Ví dụ khớp |
|---|---|---|
| `.` | Bất kỳ ký tự nào (trừ dấu xuống dòng) | `a.b` khớp `a b`, `a-b`, `a1b` |
| `\d` | Một chữ số (Digit), tương đương `[0-9]` | `\d\d` khớp `01`, `99` |
| `\D` | KHÔNG PHẢI là chữ số | `\D` khớp `a`, ` `, `@` |
| `\w` | Chữ cái, số hoặc dấu gạch dưới (Word character) `[a-zA-Z0-9_]` | `\w` khớp `A`, `1`, `_` |
| `\W` | KHÔNG PHẢI ký tự từ (Word character) | `\W` khớp `!`, `@`, khoảng trắng |
| `\s` | Khoảng trắng (Space, tab, newline) | `\s` khớp ` ` |
| `\S` | KHÔNG PHẢI khoảng trắng | `\S` khớp `a`, `1` |

#### Nhóm tập hợp và Biên (Sets & Anchors)
| Cú pháp | Ý nghĩa | Ví dụ khớp |
|---|---|---|
| `[abc]` | Một ký tự nằm trong ngoặc vuông (a hoặc b hoặc c) | `[abc]` khớp `a` |
| `[^abc]` | Một ký tự KHÔNG nằm trong ngoặc (Phủ định) | `[^abc]` khớp `x`, `y` |
| `[a-z]` | Một ký tự từ a đến z | `[a-z]` khớp `g` |
| `^` | Bắt đầu chuỗi | `^Hello` khớp chuỗi bắt đầu bằng "Hello" |
| `$` | Kết thúc chuỗi | `end$` khớp chuỗi kết thúc bằng "end" |

#### Nhóm số lượng (Quantifiers)
| Cú pháp | Ý nghĩa | Ví dụ khớp |
|---|---|---|
| `*` | Xuất hiện 0 hoặc nhiều lần | `A*` khớp ``, `A`, `AAAA` |
| `+` | Xuất hiện 1 hoặc nhiều lần (Bắt buộc phải có) | `A+` khớp `A`, `AAA` |
| `?` | Xuất hiện 0 hoặc 1 lần (Có hoặc không đều được) | `A?` khớp ``, `A` |
| `{n}` | Xuất hiện chính xác n lần | `A{3}` khớp `AAA` |
| `{n,}` | Xuất hiện từ n lần trở lên | `A{2,}` khớp `AA`, `AAA` |
| `{n,m}`| Xuất hiện từ n đến m lần | `A{2,4}` khớp `AA`, `AAA`, `AAAA` |

> ⚠️ **Lưu ý trong Java:** Vì dấu `\` trong chuỗi Java (String) là ký tự escape (ví dụ `\n`), nên khi viết regex trong chuỗi Java, bạn phải viết là `\\`. (Ví dụ: `\\d` thay vì `\d`).

---

## 2. Tìm hiểu Lớp Pattern và Matcher

Trong Java (package `java.util.regex`), quy trình tiêu chuẩn để sử dụng Regex gồm 2 class chính:

1. **`Pattern` (Khuôn mẫu):** Dùng để biên dịch chuỗi Regex thành một cỗ máy tìm kiếm. Việc biên dịch này tốn tài nguyên, nên ta thường biên dịch 1 lần rồi xài lại.
   - Cú pháp: `Pattern p = Pattern.compile("regex");`
2. **`Matcher` (Bộ khớp lệnh):** Đối tượng thực thi việc áp cái khuôn mẫu `Pattern` lên một chuỗi dữ liệu (String) cụ thể để tìm kiếm hoặc đối chiếu.
   - Cú pháp: `Matcher m = p.matcher("Chuỗi cần kiểm tra");`

### Các hàm quan trọng của Matcher:
- `m.matches()`: Kiểm tra xem **TOÀN BỘ CHUỖI** có khớp hoàn toàn với Regex không (Dùng cho Validation).
- `m.find()`: Quét qua chuỗi để tìm ra **XUYÊN SUỐT** các đoạn nhỏ khớp với Regex (Dùng để Trích xuất dữ liệu).
- `m.group()`: Trả về phần dữ liệu vừa tìm thấy khi gọi hàm `find()`.

---

## 3. Thực hành sử dụng Pattern & Matcher trong Java

### Ví dụ 1: Validate (Xác thực) định dạng Email và Số điện thoại

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexValidationDemo {
    public static void main(String[] args) {
        // 1. Kiểm tra Số điện thoại Việt Nam (10 số, bắt đầu bằng 0)
        // Regex: Bắt đầu ^, số 0, theo sau là 9 chữ số \d{9}, kết thúc $
        String phoneRegex = "^0\\d{9}$";
        Pattern phonePattern = Pattern.compile(phoneRegex);
        
        String phone1 = "0987654321"; // Hợp lệ
        String phone2 = "9876543210"; // Sai (không có 0 đầu)
        String phone3 = "0987abc321"; // Sai (chứa chữ)

        System.out.println("Kiểm tra SĐT:");
        System.out.println(phone1 + " hợp lệ? " + phonePattern.matcher(phone1).matches());
        System.out.println(phone2 + " hợp lệ? " + phonePattern.matcher(phone2).matches());
        
        // 2. Kiểm tra Email
        // Regex: [chữ/số/chấm] + @ + [chữ/số] + . + [chữ (2-4 ký tự)]
        String emailRegex = "^[a-zA-Z0-9._]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,4}$";
        Pattern emailPattern = Pattern.compile(emailRegex);
        
        String email1 = "test.user_1@gmail.com";
        String email2 = "admin@domain"; // Sai (thiếu đuôi .com/.vn)
        
        System.out.println("\nKiểm tra Email:");
        System.out.println(email1 + " hợp lệ? " + emailPattern.matcher(email1).matches());
        System.out.println(email2 + " hợp lệ? " + emailPattern.matcher(email2).matches());
    }
}
```

### Ví dụ 2: Extract (Trích xuất) Dữ liệu từ một đoạn văn bản

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexExtractDemo {
    public static void main(String[] args) {
        String content = "Xin chào, vui lòng liên hệ anh A qua số điện thoại 0912345678. " +
                         "Hoặc gọi cho chị B số 0988777666 vào ngày mai. " +
                         "Số hotline công ty: 19001560 (Không phải số cá nhân).";

        // Regex tìm số điện thoại cá nhân (Bắt đầu bằng số 0, độ dài 10 hoặc 11 số)
        // Dùng biên từ \b để đảm bảo nó là một từ độc lập (không bị dính vào chữ khác)
        String regex = "\\b0\\d{9,10}\\b";
        
        // Bước 1: Biên dịch khuôn mẫu
        Pattern pattern = Pattern.compile(regex);
        
        // Bước 2: Đưa văn bản vào máy quét Matcher
        Matcher matcher = pattern.matcher(content);
        
        // Bước 3: Dùng vòng lặp while(matcher.find()) để quét từ đầu tới cuối văn bản
        System.out.println("Các số điện thoại cá nhân tìm thấy trong đoạn văn:");
        while (matcher.find()) {
            // In ra chuỗi khớp (group) và vị trí bắt đầu (start)
            System.out.println("- Số ĐT: " + matcher.group() + " (Nằm ở vị trí: " + matcher.start() + ")");
        }
    }
}
```

### Phương thức gộp cực tiện lợi (Sử dụng trực tiếp trên String)
Mặc dù dùng `Pattern` và `Matcher` giúp tối ưu hiệu năng (khi dùng lại nhiều lần), nhưng lớp `String` của Java cũng hỗ trợ sẵn các hàm cực kỳ tiện lợi để xử lý Regex ngay lập tức (bên dưới nó tự động tạo Pattern/Matcher cho bạn):
```java
String text = "Lập trình Java 8";

// Kiểm tra khớp toàn chuỗi (Tương đương m.matches())
boolean isMatch = text.matches(".*Java.*"); 

// Tách chuỗi theo dấu phẩy HOẶC khoảng trắng
String[] words = "Apple, Banana  Orange".split("[,\\s]+"); 

// Thay thế tất cả các chữ số thành dấu *
String hidden = "Mật khẩu là 123456".replaceAll("\\d", "*"); // "Mật khẩu là ******"
```

---

## 4. Tài liệu thực hành Regex

Học Regex không thể chỉ dựa vào lý thuyết vì các biểu thức có thể rất phức tạp. Cách tốt nhất để thành thạo là **thực hành gõ Regex trực tiếp** và nhìn thấy kết quả ngay lập tức (Visual learning).

💡 **Trang web thực hành tốt nhất:**
👉 **[RegexOne - Learn Regular Expressions with simple, interactive exercises.](https://regexone.com/)**

**Tại sao nên học trên RegexOne?**
- Có 15+ bài học tương tác đi từ số 0 (cơ bản nhất) đến phức tạp.
- Đưa ra các bài toán thực tế (Ví dụ: Viết regex để trích xuất tên miền từ các chuỗi `https://www.google.com`).
- Bạn gõ regex vào khung, web sẽ highlight chữ màu xanh ngay lập tức nếu bạn viết đúng quy luật.
- Ngôn ngữ Regex độc lập với ngôn ngữ lập trình, học 1 lần dùng được cho cả Java, JavaScript, Python, C#...

> 🛠️ **Công cụ kiểm tra (Tester):** Khi bạn viết Regex thực tế trong dự án, luôn luôn kiểm tra nó trước bằng trang web **[Regex101.com](https://regex101.com/)** để xem phân tích chi tiết cỗ máy Regex của bạn đang hoạt động/quét dữ liệu như thế nào trước khi copy vào code Java.

---

> **📌 Kết thúc Phần 12: Biểu thức chính quy**

---

# Phần 13: Triển khai Ứng dụng (Deploy) & Máy ảo Java (JVM)

## 📌 Mục lục
1. [Máy ảo Java (JVM) là gì?](#1-máy-ảo-java-jvm-là-gì)
2. [Cách chạy chương trình Java bằng dòng lệnh (Terminal/CMD)](#2-cách-chạy-chương-trình-java-bằng-dòng-lệnh-terminalcmd)
3. [Bộ nhớ Heap (Heap Memory) là gì?](#3-bộ-nhớ-heap-heap-memory-là-gì)
4. [Cấu hình dung lượng RAM và lý do phải Set Max (Xmx)](#4-cấu-hình-dung-lượng-ram-và-lý-do-phải-set-max-xmx)
5. [Tổng hợp các câu lệnh chạy Java phổ biến](#5-tổng-hợp-các-câu-lệnh-chạy-java-phổ-biến)

---

## 1. Máy ảo Java (JVM) là gì?

Ngôn ngữ C/C++ khi biên dịch sẽ dịch trực tiếp ra **Mã máy (Machine Code - File .exe)**. Mã máy này phụ thuộc hoàn toàn vào Hệ điều hành và CPU. (File `.exe` biên dịch trên Windows không thể mang sang Linux chạy).

**Java thì khác!** Triết lý của Java là **"Write Once, Run Anywhere" (Viết một lần, chạy mọi nơi)**. Để làm được điều này, Java sinh ra một tầng trung gian gọi là **JVM (Java Virtual Machine - Máy ảo Java)**.

**Cơ chế hoạt động:**
1. Code của bạn (`.java`) được Trình biên dịch (`javac`) dịch ra một dạng mã trung gian gọi là **Bytecode (`.class`)**.
2. File Bytecode này chưa phải là mã máy, CPU không hiểu được.
3. Khi bạn mang file Bytecode đó sang Windows, Linux hay Mac, **Máy ảo JVM** (đã được cài sẵn trên hệ điều hành đó) sẽ đóng vai trò làm phiên dịch viên. Nó đọc Bytecode và dịch lại thành Mã máy tương ứng để hệ điều hành đó hiểu được.

👉 *Kết luận: Máy ảo Java (JVM) là một phần mềm giả lập môi trường chạy độc lập, giúp phiên dịch Bytecode thành mã máy gốc của hệ điều hành mà nó đang đứng trên đó.*

---

## 2. Cách chạy chương trình Java bằng dòng lệnh (Terminal/CMD)

Trong quá trình dev, bạn thường bấm nút "Run" trên IntelliJ hoặc Eclipse. Nhưng khi Deploy lên máy chủ (Server Linux không có giao diện đồ họa), bạn phải làm mọi thứ bằng dòng lệnh.

Giả sử bạn có file `HelloWorld.java`:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello từ Terminal!");
    }
}
```

**Bước 1: Biên dịch code (Compile)**
- Mở Terminal hoặc CMD tại thư mục chứa file.
- Chạy lệnh: `javac HelloWorld.java`
- Nếu không có lỗi cú pháp, lệnh này sẽ sinh ra file `HelloWorld.class` (Đây chính là Bytecode).

**Bước 2: Chạy ứng dụng (Run)**
- Chạy lệnh: `java HelloWorld`
- *Lưu ý:* Khi chạy lệnh `java`, bạn CHỈ GHI TÊN CLASS, tuyệt đối không ghi đuôi `.class` hay `.java`. Màn hình sẽ in ra: `Hello từ Terminal!`.

---

## 3. Bộ nhớ Heap (Heap Memory) là gì?

Khi JVM chạy ứng dụng của bạn, nó được Hệ điều hành cấp cho một vùng RAM. JVM chia vùng RAM này thành nhiều phần, quan trọng nhất là **Stack** và **Heap**.

- **Stack Memory:** Chứa các lời gọi hàm và các biến cục bộ (các biến nguyên thủy như int, float nằm trong hàm). Nó rất nhỏ và tự dọn dẹp ngay khi hàm kết thúc.
- **Heap Memory (Bộ nhớ Heap):** Đây là một khu vực bộ nhớ RẤT LỚN. **Tất cả các đối tượng (Object)** được tạo ra bằng từ khóa `new` đều bị tống vào Heap. (Ví dụ: `new SinhVien()`, `new ArrayList()`).
  - Heap là khu vực được giám sát bởi **Garbage Collector (Trình thu gom rác)**. Khi một Object trong Heap không còn ai sử dụng (không có biến nào trỏ tới), Garbage Collector sẽ quét qua và xóa nó đi để thu hồi RAM.
  - Khi chương trình bạn tạo ra quá nhiều Object mà không chịu xóa đi (Memory Leak), vùng Heap này sẽ bị đầy, và ứng dụng văng lỗi khét tiếng: **`java.lang.OutOfMemoryError: Java heap space`**.

---

## 4. Cấu hình dung lượng RAM và lý do phải Set Max (Xmx)

Khi Deploy lên server thật (Production), chúng ta không bao giờ để JVM tự động quyết định lượng RAM, mà phải cấu hình thủ công bằng 2 tham số:

- `-Xms` (Initial Heap Size): Dung lượng RAM khởi tạo lúc ứng dụng vừa bật lên.
- `-Xmx` (Maximum Heap Size): Dung lượng RAM **Tối đa** mà ứng dụng được phép phình to ra.

**Ví dụ cấu hình:** 
Lệnh khởi động một ứng dụng được cấp ban đầu 512MB và cho phép "ăn" tối đa 2GB RAM:
`java -Xms512m -Xmx2g MyApp`

### Tại sao BẮT BUỘC phải Set Max (-Xmx)?
1. **Tránh làm chết Server (OOM Killer):** Nếu bạn không set Max, JVM (bản tính tham lam) sẽ liên tục xin thêm RAM từ Hệ điều hành mỗi khi nó cần cấp phát Object mới. Khi RAM của cả Server cạn kiệt, Hệ điều hành Linux sẽ kích hoạt cơ chế tự vệ (OOM Killer) và "Bắn bỏ" (Kill) tiến trình Java của bạn một cách đột ngột.
2. **Kiểm soát khi chạy trên Docker/Microservices:** Một máy chủ ngày nay thường chạy hàng chục ứng dụng (Container) cùng lúc. Nếu 1 ứng dụng Java không bị giới hạn bộ nhớ, nó sẽ phình to ra và ăn lẹm vào RAM của các ứng dụng khác đang chạy cùng máy chủ.
3. **Hiệu năng của Garbage Collector (GC):** Việc để Heap quá to hoặc quá nhỏ đều không tốt. Quá nhỏ thì GC phải chạy liên tục làm chậm app. Quá to thì mỗi lần GC đi gom rác (Full GC) sẽ làm toàn bộ ứng dụng bị khựng lại (Pause time) mất vài giây. Việc set `-Xms` và `-Xmx` bằng nhau (Ví dụ: `-Xms2g -Xmx2g`) là một best practice để tránh việc JVM phải mất thời gian xin thêm/trả lại RAM liên tục cho HĐH.

---

## 5. Tổng hợp các câu lệnh chạy Java phổ biến

Trên môi trường thực tế, ứng dụng thường được đóng gói thành file `.jar` (chứa hàng ngàn file `.class` và thư viện bên trong).

**1. Chạy một file JAR cơ bản:**
```bash
java -jar my-app.jar
```

**2. Chạy file JAR với cấu hình RAM (Rất hay dùng khi Deploy):**
```bash
# Phải đặt tham số RAM ĐẰNG TRƯỚC -jar
java -Xms1g -Xmx1g -jar my-app.jar
```

**3. Chạy và truyền tham số đầu vào (Arguments):**
```bash
# Trong hàm main(String[] args), args[0] = "admin", args[1] = "123456"
java -jar my-app.jar admin 123456
```

**4. Chạy và cấu hình Biến hệ thống (System Properties):**
```bash
# Dùng cờ -D (Ví dụ: Định nghĩa môi trường là production)
# Nhớ: -D phải viết liền với tên biến, và đặt TRƯỚC -jar
java -Dspring.profiles.active=prod -Dserver.port=8080 -jar my-app.jar
```

**5. Lệnh Deploy toàn diện (Chạy ngầm trên Linux):**
```bash
# nohup: Giữ cho app chạy ngầm ngay cả khi tắt cửa sổ Terminal
# > app.log: Ghi toàn bộ console output vào file app.log
# &: Đẩy tiến trình xuống chạy dưới background
nohup java -Xms512m -Xmx1024m -Denv=prod -jar my-app.jar > app.log 2>&1 &
```

---

> **📌 Kết thúc Phần 13: Triển khai Ứng dụng**

---

# Phần 14: Quy chuẩn code Java (Java Coding Conventions)

## 📌 Mục lục
1. [Tại sao cần phải có Coding Convention?](#1-tại-sao-cần-phải-có-coding-convention)
2. [Quy tắc đặt tên (Naming Conventions)](#2-quy-tắc-đặt-tên-naming-conventions)
3. [Các cách viết Comment (Bình luận) trong code](#3-các-cách-viết-comment-bình-luận-trong-code)
4. [Viết tài liệu Javadoc chuyên nghiệp](#4-viết-tài-liệu-javadoc-chuyên-nghiệp)

---

## 1. Tại sao cần phải có Coding Convention?
Trong một dự án thực tế, mã nguồn không chỉ do một người viết mà là công sức của cả một tập thể. 
**Coding Convention (Quy chuẩn viết code)** là tập hợp các luật lệ chung giúp:
- **Dễ đọc, dễ hiểu:** Ai cũng có thể đọc code của người khác dễ dàng như đọc code của chính mình.
- **Dễ bảo trì:** Tránh những lỗi ngớ ngẩn do đặt tên biến gây nhầm lẫn.
- **Chuyên nghiệp:** Thể hiện đẳng cấp của lập trình viên và chất lượng của dự án.

---

## 2. Quy tắc đặt tên (Naming Conventions)

Java sử dụng 3 chuẩn đặt tên chính:
- **PascalCase (Viết hoa chữ cái đầu mỗi từ):** `SinhVien`, `QuanLyNhanVien`
- **camelCase (Lạc đà - Chữ cái đầu tiên viết thường, các chữ cái đầu của từ tiếp theo viết hoa):** `hoTen`, `layDanhSach`
- **UPPER_SNAKE_CASE (Viết hoa toàn bộ, cách nhau bởi dấu gạch dưới):** `MAX_VALUE`, `DEFAULT_TIMEOUT`

### Bảng tổng hợp Quy tắc:

| Thành phần | Cú pháp sử dụng | Lưu ý (Best Practice) | Ví dụ Đúng | Ví dụ Sai |
|---|---|---|---|---|
| **Class (Lớp)** | **PascalCase** | Nên là một **Danh từ**. | `Customer`, `UserAccount` | `customer`, `user_account` |
| **Interface** | **PascalCase** | Nên là Tính từ (kết thúc bằng `able`) hoặc Danh từ. | `Runnable`, `Serializable` | `runnable`, `Run` |
| **Method (Hàm)** | **camelCase** | Nên bắt đầu bằng một **Động từ** (get, set, do, is). | `getName()`, `calculateSalary()` | `Salary()`, `Get_name()` |
| **Biến (Variable)** | **camelCase** | Tên phải có ý nghĩa, tránh viết tắt quá ngắn (trừ biến chạy i, j trong vòng lặp). | `studentName`, `totalPrice` | `sn`, `tong_tien` |
| **Hằng số (Constant)** | **UPPER_SNAKE_CASE** | Phải kết hợp từ khóa `static final`. | `MAX_AGE`, `PI` | `maxAge`, `Max_Age` |
| **Gói (Package)** | **lowercase (Chữ thường)** | Thường sử dụng tên miền công ty đảo ngược. | `com.company.project` | `Com.Company.Project` |

### Ví dụ code chuẩn:
```java
package com.company.entity; // Tên package viết thường toàn bộ

// Tên Class là Danh từ, viết theo PascalCase
public class BankAccount {

    // Hằng số: static final, UPPER_SNAKE_CASE
    public static final int MAX_WITHDRAW_LIMIT = 5000000;
    
    // Biến instance: camelCase
    private String accountName;
    private double currentBalance;

    // Tên hàm là Động từ, camelCase
    public void withdrawMoney(double amount) {
        // Biến cục bộ: camelCase
        double fee = 5000.0;
        this.currentBalance -= (amount + fee);
    }
}
```

---

## 3. Các cách viết Comment (Bình luận) trong code

Comment dùng để giải thích MỤC ĐÍCH của đoạn code (Tại sao lại viết như vậy?), chứ không phải dịch đoạn code đó ra tiếng Việt.

### 3.1 Comment một dòng (Single-line Comment)
Sử dụng kí hiệu `//`. Dành cho các dòng giải thích ngắn gọn, thường đặt ở trên đoạn code cần giải thích.
```java
// Kiểm tra nếu người dùng chưa đủ 18 tuổi thì từ chối truy cập
if (age < 18) {
    return false; 
}
```

### 3.2 Comment nhiều dòng (Multi-line / Block Comment)
Sử dụng kí hiệu `/* ... */`. Dành cho việc giải thích các đoạn logic phức tạp hoặc tạm thời "vô hiệu hóa" (comment out) một đoạn code lớn.
```java
/*
 * Thuật toán tính lãi suất kép:
 * 1. Tính lãi suất tháng = Lãi suất năm / 12
 * 2. Cộng dồn vào vốn gốc cho các kỳ tiếp theo
 * 3. Trừ đi chi phí bảo trì tài khoản (nếu có)
 */
public double calculateCompoundInterest(...) { ... }
```

---

## 4. Viết tài liệu Javadoc chuyên nghiệp

**Javadoc** là một loại comment đặc biệt trong Java (bắt đầu bằng `/**` và kết thúc bằng `*/`).
Khác với comment thông thường chỉ để người lập trình đọc trong file mã nguồn, Javadoc sẽ được Trình biên dịch (Compiler) hoặc các IDE trích xuất ra thành một **Trang web Tài liệu HTML** để chia sẻ cho người khác đọc (Giống như đọc API Docs).

### 4.1 Quy tắc đặt Javadoc
- Phải được đặt **NGAY TRÊN** phần khai báo của Class, Interface hoặc Method.
- Cấu trúc chung gồm 2 phần:
  1. Dòng mô tả ngắn gọn về chức năng.
  2. Các thẻ (Tags) đặc biệt để mô tả chi tiết tham số, kết quả, v.v.

### 4.2 Các thẻ (Tags) phổ biến nhất
| Thẻ (Tag) | Nơi sử dụng | Ý nghĩa |
|---|---|---|
| `@author` | Class / Interface | Tên người viết class này. |
| `@version` | Class / Interface | Phiên bản hiện tại của class. |
| `@since` | Class / Interface | Tính năng này xuất hiện từ phiên bản JDK/App nào. |
| `@param` | Method (Hàm) | Mô tả mục đích của tham số truyền vào hàm. |
| `@return` | Method (Hàm) | Mô tả ý nghĩa của giá trị trả về (Nếu hàm void thì không cần). |
| `@throws` / `@exception` | Method (Hàm) | Mô tả trường hợp nào thì hàm sẽ ném ra lỗi (Exception). |
| `@deprecated` | Class / Method | Cảnh báo: Hàm này đã CŨ và sắp bị xóa, khuyên lập trình viên không nên dùng nữa. |

### 4.3 Ví dụ Javadoc thực tế chuẩn mực

```java
/**
 * Lớp cung cấp các tiện ích xử lý chuỗi và mật khẩu.
 * Không cho phép khởi tạo đối tượng từ lớp này (Utility class).
 * 
 * @author Nguyen Van A
 * @version 1.2.0
 * @since 2026-06
 */
public class SecurityUtils {

    // Private constructor (Chặn khởi tạo)
    private SecurityUtils() {}

    /**
     * Mã hóa mật khẩu người dùng sử dụng thuật toán băm SHA-256.
     * <p>
     * Lưu ý: Không lưu trực tiếp mật khẩu gốc vào cơ sở dữ liệu.
     * Hãy gọi hàm này trước khi lưu.
     * </p>
     * 
     * @param rawPassword Mật khẩu thô do người dùng nhập (không được null)
     * @param salt        Chuỗi muối ngẫu nhiên để tăng độ khó giải mã
     * @return            Chuỗi mật khẩu đã được mã hóa dạng HEX
     * @throws IllegalArgumentException Nếu mật khẩu truyền vào là rỗng hoặc null
     * @deprecated Hàm này đã cũ, hãy chuyển sang dùng hàm {@link #hashBcrypt(String)} để bảo mật cao hơn.
     */
    @Deprecated
    public static String hashPassword(String rawPassword, String salt) throws IllegalArgumentException {
        if (rawPassword == null || rawPassword.trim().isEmpty()) {
            throw new IllegalArgumentException("Mật khẩu không được để trống");
        }
        
        // Logic mã hóa ở đây...
        return "hashed_string_123456";
    }
}
```

> 💡 **Mẹo:** Trong IntelliJ IDEA hoặc Eclipse, bạn chỉ cần gõ `/**` ngay phía trên một tên Hàm rồi bấm `Enter`, IDE sẽ tự động sinh ra sẵn các thẻ `@param`, `@return`... tương ứng với chữ ký của hàm đó để bạn điền vào!

---

> **📌 Kết thúc Phần 14: Quy chuẩn code Java**

---

# Phần 15: Cấu trúc dữ liệu và Thuật toán (Data Structures & Algorithms)

## 📌 Mục lục
1. [Cấu trúc dữ liệu cơ bản và So sánh Ưu/Nhược điểm](#1-cấu-trúc-dữ-liệu-cơ-bản-và-so-sánh-ưunhược-điểm)
2. [Thuật toán Tìm kiếm & Sắp xếp](#2-thuật-toán-tìm-kiếm--sắp-xếp)
3. [Cấu trúc dữ liệu Cây (Tree) và Đồ thị (Graph)](#3-cấu-trúc-dữ-liệu-cây-tree-và-đồ-thị-graph)
4. [Các thuật toán Duyệt Đồ thị (BFS & DFS)](#4-các-thuật-toán-duyệt-đồ-thị-bfs--dfs)
5. [Cây Nhị Phân Tìm Kiếm (BST) & Cách cân bằng Cây](#5-cây-nhị-phân-tìm-kiếm-bst--cách-cân-bằng-cây)

---

## 1. Cấu trúc dữ liệu cơ bản và So sánh Ưu/Nhược điểm

### 1.1 Mảng (Array)
Là tập hợp các phần tử CÙNG KIỂU, được lưu trữ LIÊN TIẾP nhau trong bộ nhớ RAM.
- **Ưu điểm:** Tốc độ truy xuất (Đọc) cực kì nhanh `O(1)` thông qua chỉ số index (Ví dụ: `arr[5]`).
- **Nhược điểm:** Kích thước cố định (không thể phình to hay thu nhỏ sau khi tạo). Thêm/Xóa phần tử ở giữa mảng rất chậm `O(n)` vì phải dịch chuyển tất cả các phần tử phía sau.

### 1.2 Danh sách liên kết (Linked List)
Mỗi phần tử (Node) nằm rải rác trên RAM. Một Node chứa dữ liệu và một Con trỏ (Pointer) chỉ đường tới Node tiếp theo.
- **Ưu điểm:** Kích thước co giãn linh hoạt. Thêm/Xóa phần tử ở đầu/cuối hoặc khi đã biết vị trí thì cực nhanh `O(1)` (chỉ cần bẻ lại hướng của con trỏ).
- **Nhược điểm:** Tìm kiếm/Đọc dữ liệu cực chậm `O(n)` vì phải duyệt lần lượt từ phần tử đầu tiên (đầu dây) trở đi.

### 1.3 Ngăn xếp (Stack)
Hoạt động theo nguyên tắc **LIFO (Last In, First Out - Vào sau ra trước)**.
Giống như xếp 1 chồng đĩa: Đĩa nào đặt lên sau cùng sẽ được lấy ra đầu tiên.
- **Ưu điểm:** Hoàn hảo cho các bài toán: Nút Undo (Hoàn tác), Khử đệ quy, Lịch sử trình duyệt.
- **Các hàm chính:** `push()` (Thêm vào đỉnh), `pop()` (Lấy ra và xóa ở đỉnh), `peek()` (Chỉ xem đỉnh).

### 1.4 Hàng đợi (Queue)
Hoạt động theo nguyên tắc **FIFO (First In, First Out - Vào trước ra trước)**.
Giống như xếp hàng mua vé: Ai đến xếp hàng trước sẽ được phục vụ trước.
- **Ưu điểm:** Dùng cho Hàng đợi tin nhắn (Message Queue), Lập lịch tiến trình CPU, Duyệt đồ thị BFS.
- **Các hàm chính:** `enqueue/offer()` (Thêm vào cuối), `dequeue/poll()` (Lấy ra ở đầu).

---

## 2. Thuật toán Tìm kiếm & Sắp xếp

### 2.1 Thuật toán Tìm kiếm (Search)
- **Tìm kiếm tuyến tính (Linear Search):** Duyệt từng phần tử từ đầu đến cuối xem có khớp không. Độ phức tạp `O(n)`. (Dùng cho mảng lộn xộn).
- **Tìm kiếm nhị phân (Binary Search):** ⚠️ *Bắt buộc mảng phải được Sắp Xếp trước.* Thuật toán chia đôi mảng liên tục để loại bỏ một nửa số phần tử mỗi lần tìm. Độ phức tạp cực nhanh `O(log n)`. (Ví dụ: Tìm số trong 1 tỷ số chỉ mất tối đa 30 lần chia đôi).

### 2.2 Thuật toán Sắp xếp (Sort)
- **Bubble Sort (Sắp xếp nổi bọt):** Duyệt từng cặp phần tử liền kề, sai vị trí thì đổi chỗ cho nhau. Chậm nhất, độ phức tạp `O(n^2)`.
- **Quick Sort (Sắp xếp nhanh):** Chọn 1 điểm mốc (Pivot). Ném các số nhỏ hơn Pivot sang trái, lớn hơn sang phải. Sau đó Đệ quy làm tiếp với 2 nửa. Cực nhanh `O(n log n)`, hay được sử dụng thực tế.
- **Merge Sort (Sắp xếp trộn):** Chia mảng làm đôi liên tục cho đến khi chỉ còn 1 phần tử. Sau đó bắt đầu "trộn" 2 mảng nhỏ đã sắp xếp lại thành mảng lớn. Nhanh và Ổn định `O(n log n)`, nhưng tốn thêm RAM để lưu mảng phụ.

---

## 3. Cấu trúc dữ liệu Cây (Tree) và Đồ thị (Graph)

### 3.1 Cây (Tree)
Là cấu trúc dữ liệu phân cấp, có quan hệ **Cha - Con**. Có 1 gốc duy nhất (Root). Một Cha có thể có nhiều Con, nhưng Một Con chỉ có 1 Cha. (Không có vòng lặp).
*Ví dụ:* Sơ đồ tổ chức công ty, Cây thư mục máy tính, Cấu trúc thẻ HTML (DOM).

### 3.2 Đồ thị (Graph)
Là cấu trúc dữ liệu phức tạp hơn, gồm các Đỉnh (Vertex/Node) và các Cạnh (Edge) nối các đỉnh lại với nhau. Không có khái niệm Gốc, Mọi đỉnh đều có thể nối với mọi đỉnh, có thể tạo thành Vòng lặp.
*Ví dụ:* Bản đồ đường đi (Google Maps), Mạng xã hội (A là bạn của B, B là bạn của C).

---

## 4. Các thuật toán Duyệt Đồ thị (BFS & DFS)

Khi đứng ở 1 đỉnh và muốn đi thăm tất cả các đỉnh còn lại trong Đồ thị, ta có 2 chiến thuật:

### 4.1 Duyệt theo chiều rộng (BFS - Breadth-First Search)
- **Chiến thuật:** Lan tỏa như sóng nước. Thăm hết tất cả các "Người quen tầng 1" (Hàng xóm sát vách), rồi mới lan sang "Người quen tầng 2"...
- **Công cụ sử dụng:** `Queue` (Hàng đợi). Ai được nhìn thấy trước sẽ được xếp vào hàng đợi để thăm trước.
- **Ứng dụng:** Tìm **Đường đi ngắn nhất** (Shortest path) trên đồ thị không trọng số (Ví dụ: Tìm bạn chung gần nhất trên Facebook).

### 4.2 Duyệt theo chiều sâu (DFS - Depth-First Search)
- **Chiến thuật:** Đi lạc trong mê cung. Cứ chọn 1 ngã rẽ và đi "Đâm lao theo lao" sâu nhất có thể cho tới khi đâm vào ngõ cụt thì mới quay lui (Backtrack) lại ngã ba gần nhất để đi hướng khác.
- **Công cụ sử dụng:** `Stack` (Ngăn xếp) hoặc viết hàm **Đệ quy**.
- **Ứng dụng:** Tìm đường đi ra khỏi mê cung, Kiểm tra chu trình (Vòng lặp) trong đồ thị.

---

## 5. Cây Nhị Phân Tìm Kiếm (BST) & Cách cân bằng Cây

### 5.1 Cây nhị phân tìm kiếm (Binary Search Tree - BST)
Là một cây tuân thủ 2 quy tắc vàng:
1. Mỗi Node cha có TỐI ĐA 2 node con (Nhị phân - Trái và Phải).
2. Quy tắc tìm kiếm: Tất cả các con bên **TRÁI** phải **NHỎ HƠN** node cha. Tất cả các con bên **PHẢI** phải **LỚN HƠN** node cha.

*Ưu điểm:* Việc tìm kiếm trên BST giống hệt "Tìm kiếm nhị phân". Bất kỳ lúc nào, ta cũng có thể loại bỏ 1 nửa cây. Độ phức tạp `O(log n)`.

### 5.2 Vấn đề mất cân bằng
Nếu bạn chèn lần lượt các số đã được sắp xếp `(1, 2, 3, 4, 5)` vào BST, cây sẽ bị lệch hẳn sang một bên (tất cả đều nằm bên Phải). 
Lúc này, Cây bị thoái hóa biến thành một **Danh sách liên kết (Linked List)**. Việc tìm kiếm không còn là `O(log n)` nữa mà thảm họa trở về `O(n)`.

### 5.3 Cách cân bằng Cây (Tự cân bằng - Self-Balancing Tree)
Để khắc phục, người ta chế tạo ra các loại Cây thông minh, mỗi khi bạn thêm/xóa phần tử làm cây bị lệch, nó sẽ TỰ ĐỘNG THỰC HIỆN "PHÉP XOAY" (Rotation) cấu trúc node để kéo cây về trạng thái cân đối. Hai loại nổi tiếng nhất:

1. **AVL Tree:** Cây cân bằng Cực kì chặt chẽ. Đảm bảo độ cao giữa nhánh Trái và nhánh Phải không bao giờ lệch nhau quá 1. (Rất tốt để Tìm kiếm liên tục).
2. **Red-Black Tree (Cây Đỏ-Đen):** Cây cân bằng tương đối (Bằng cách tô màu Đỏ/Đen cho các Node và xoay theo luật). 
   - Không bị xoay quá nhiều lần khi chèn dữ liệu như AVL.
   - 🏆 *Thực tế:* Trong Java, cấu trúc dữ liệu `TreeMap` và `TreeSet` chính là được cài đặt ẩn bên dưới bằng **Red-Black Tree**.

---

> **📌 KẾT THÚC SERIES LÝ THUYẾT JAVA CORE & DATA STRUCTURES TẠI ĐÂY**
> 
> Bộ tài liệu này đã hệ thống lại một cách đầy đủ và chi tiết toàn bộ kiến thức về Ngôn ngữ Java (từ Cơ bản đến Nâng cao) cùng với Nền tảng Thuật toán.
> Chúc bạn học tập và áp dụng thật hiệu quả trong công việc thực tế!







