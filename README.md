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
>
> Phần tiếp theo: [Phần 2: Lập Trình Cơ Bản](#phần-2-lập-trình-cơ-bản) *(sẽ được bổ sung)*
