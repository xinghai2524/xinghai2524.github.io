<div  class="container">

# Linux 磁盘管理</div>

# 一    查看磁盘硬件信息

在`Linux`中，磁盘都是以挂载方式挂载到目录的，比如，安装系统的时候，必须有个磁盘挂载到根目录，如果需要添加磁盘，可以挂载到新的目录或者扩展`逻辑卷`

使用`fdisk -l`命令查看硬件信息

```shell
sudo fdisk -l
```

输出结果：

```shell
xinghai@xinghai:~$ sudo fdisk -l
Disk /dev/nvme0n1: 931.51 GiB, 1000204886016 bytes, 1953525168 sectors
Disk model: WD Blue SN580 1TB
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 99FAC4CC-FBF8-4026-ADF7-A8D1D5A0EA2C

Device           Start        End    Sectors   Size Type
/dev/nvme0n1p1    2048    2203647    2201600     1G EFI System
/dev/nvme0n1p2 2203648    6397951    4194304     2G Linux filesystem
/dev/nvme0n1p3 6397952 1953521663 1947123712 928.5G Linux filesystem

Disk /dev/mapper/ubuntu--vg-ubuntu--lv: 928 GiB, 996432412672 bytes, 1946157056 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
xinghai@xinghai:~$
```

具体含义如下

> 1. `Disk /dev/nvme0n1: 931.51 GiB, 1000204886016 bytes, 1953525168 sectors`
>
> - `/dev/nvme0n1`：这是磁盘的设备名称。`nvme0n1` 表示这是一块 NVMe 固态硬盘（SSD），`nvme0` 表示第一个 NVMe 控制器，`n1` 表示第一个命名空间（Namespace）。
> - `931.51 GiB`：磁盘的总容量，以 GiB（Gibibyte，1 GiB = 1024 MiB）为单位。
> - `1000204886016 bytes`：磁盘的总容量，以字节为单位。
> - `1953525168 sectors`：磁盘的总扇区数。每个扇区通常是 512 字节。
>
> ------
>
> 2. `Disk model: WD Blue SN580 1TB`
>
> - 这是磁盘的型号信息，表示这是一块西部数据（WD）的 Blue SN580 系列 NVMe 固态硬盘，标称容量为 1TB。
>
> ------
>
> 3. `Units: sectors of 1 \* 512 = 512 bytes`
>
> - 这里说明了磁盘的扇区大小。每个扇区的大小是 512 字节。
> - 在计算分区大小时，工具会以扇区为单位进行计算。
>
> ------
>
> 4. `Sector size (logical/physical): 512 bytes / 512 bytes`
>
> - `logical`：逻辑扇区大小，通常是操作系统看到的扇区大小。
> - `physical`：物理扇区大小，是磁盘硬件实际的扇区大小。
> - 这里逻辑扇区和物理扇区大小都是 512 字节，表示磁盘使用的是传统的 512 字节扇区。
>
> ------
>
> 5. `I/O size (minimum/optimal): 512 bytes / 512 bytes`
>
> - `minimum`：最小的 I/O 操作大小。
> - `optimal`：最优的 I/O 操作大小。
> - 这里最小和最优的 I/O 大小都是 512 字节，表示磁盘的最佳性能是在每次读写 512 字节时。
>
> ------
>
> 6. `Disklabel type: gpt`
>
> - 这表示磁盘的分区表类型是 GPT（GUID Partition Table）。
> - GPT 是一种现代的分区表格式，支持大于 2TB 的磁盘和更多的分区。
>
> ------
>
> 7. `Disk identifier: 99FAC4CC-FBF8-4026-ADF7-A8D1D5A0EA2C`
>
> - 这是磁盘的唯一标识符（GUID），用于区分不同的磁盘。
> - 这个标识符是 GPT 分区表的一部分，确保磁盘的唯一性。
>
> <h3>磁盘分区信息</h3>
>
> 1. `/dev/nvme0n1p1`
>
> - 设备名称：`/dev/nvme0n1p1`，表示这是磁盘 `/dev/nvme0n1` 的第一个分区。
> - 起始扇区：`2048`。
> - 结束扇区：`2203647`。
> - 扇区数量：`2201600`。
> - 大小：`1G`（1 GB）。
> - 类型：`EFI System`。
>   - 这是一个 EFI 系统分区（ESP），通常用于 UEFI 启动的系统。它存储引导加载程序（如 GRUB）和 UEFI 相关的文件。
>   - 该分区通常是 FAT32 文件系统。
>
> ------
>
> 2. `/dev/nvme0n1p2`
>
> - 设备名称：`/dev/nvme0n1p2`，表示这是磁盘 `/dev/nvme0n1` 的第二个分区。
> - 起始扇区：`2203648`。
> - 结束扇区：`6397951`。
> - 扇区数量：`4194304`。
> - 大小：`2G`（2 GB）。
> - 类型：`Linux filesystem`。
>   - 这是一个 Linux 文件系统分区，通常用于挂载 `/boot` 目录，存储内核和初始化内存盘（initramfs）等启动文件。
>   - 该分区通常是 ext4 文件系统。
>
> ------
>
> 3. `/dev/nvme0n1p3`
>
> - 设备名称：`/dev/nvme0n1p3`，表示这是磁盘 `/dev/nvme0n1` 的第三个分区。
> - 起始扇区：`6397952`。
> - 结束扇区：`1953521663`。
> - 扇区数量：`1947123712`。
> - 大小：`928.5G`（928.5 GB）。
> - 类型：`Linux filesystem`。
>   - 这是一个 Linux 文件系统分区，通常是根分区（`/`），用于存储操作系统和用户数据。
>   - 该分区通常是 ext4 或 btrfs 文件系统。
>
> <h3>磁盘逻辑卷信息</h3>
>
> 1. `Disk /dev/mapper/ubuntu--vg-ubuntu--lv: 928 GiB, 996432412672 bytes, 1946157056 sectors`
>
> - `/dev/mapper/ubuntu--vg-ubuntu--lv`：这是逻辑卷的设备名称。
>   - `ubuntu--vg` 是卷组（Volume Group）的名称。
>   - `ubuntu--lv` 是逻辑卷（Logical Volume）的名称。
>   - LVM 允许你将多个物理磁盘或分区组合成一个卷组，然后从卷组中创建逻辑卷。
> - `928 GiB`：逻辑卷的总容量，以 GiB（Gibibyte，1 GiB = 1024 MiB）为单位。
> - `996432412672 bytes`：逻辑卷的总容量，以字节为单位。
> - `1946157056 sectors`：逻辑卷的总扇区数。每个扇区通常是 512 字节。
>
> ------
>
> 2. `Units: sectors of 1 \* 512 = 512 bytes`
>
> - 这里说明了逻辑卷的扇区大小。每个扇区的大小是 512 字节。
> - 在计算逻辑卷大小时，工具会以扇区为单位进行计算。
>
> ------
>
> 3. `Sector size (logical/physical): 512 bytes / 512 bytes`
>
> - `logical`：逻辑扇区大小，通常是操作系统看到的扇区大小。
> - `physical`：物理扇区大小，是底层物理磁盘的扇区大小。
> - 这里逻辑扇区和物理扇区大小都是 512 字节，表示底层磁盘使用的是传统的 512 字节扇区。
>
> ------
>
> 4. `I/O size (minimum/optimal): 512 bytes / 512 bytes`
>
> - `minimum`：最小的 I/O 操作大小。
> - `optimal`：最优的 I/O 操作大小。
> - 这里最小和最优的 I/O 大小都是 512 字节，表示逻辑卷的最佳性能是在每次读写 512 字节时。
>
> ------
>
> 总结
>
> - 这是一个 LVM 逻辑卷，设备名称为 `/dev/mapper/ubuntu--vg-ubuntu--lv`。
> - 逻辑卷的总容量为 928 GiB。
> - 逻辑卷的扇区大小为 512 字节，与底层物理磁盘一致。
> - 该逻辑卷可能是用于存储操作系统或用户数据的根分区（`/`）或其他挂载点。
>
> ------
>
> 补充：LVM 的基本概念
>
> 1. 物理卷（Physical Volume, PV）：实际的磁盘或分区，被 LVM 管理。
> 2. 卷组（Volume Group, VG）：由一个或多个物理卷组成，形成一个存储池。
> 3. 逻辑卷（Logical Volume, LV）：从卷组中划分出来的逻辑分区，可以被格式化和挂载。

