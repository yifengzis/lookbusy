# lookbusy - 系统负载生成器

`lookbusy` 是一个用于在 Linux 系统上生成合成负载的工具。它可以模拟 CPU 活动、内存使用和磁盘 I/O，让系统“看起来很忙”。

本项目已进行汉化，命令行输出均为中文。

## 功能特性

*   **CPU 负载**:
    *   支持固定百分比利用率。
    *   支持正弦曲线波动利用率（模拟昼夜负载变化）。
    *   自动检测多核 CPU 并启动对应数量的进程。
*   **内存负载**:
    *   分配并持续访问指定大小的内存，防止被交换出（Swap）。
    *   支持正弦曲线波动内存使用量。
*   **磁盘负载**:
    *   在指定目录生成文件并进行读写操作，产生 I/O 压力。

## 编译与安装

本项目使用 GNU Autotools 构建系统。

### 依赖
*   C 编译器 (GCC/Clang)
*   Make

### 构建步骤

1.  生成配置脚本：
    ```bash
    ./autogen.sh
    ```

2.  配置项目：
    ```bash
    ./configure
    ```

3.  编译：
    ```bash
    make
    ```

4.  安装 (可选)：
    ```bash
    sudo make install
    ```

## 使用方法

编译完成后，构建产物位于当前目录下的 `targets/` 目录中。

### 常用示例

*   **CPU 负载**: 保持所有 CPU 核心 50% 利用率
    ```bash
    ./targets/lookbusy -c 50
    ```

*   **CPU 负载 (曲线模式)**: 负载在 20% 到 80% 之间波动，周期为 24 小时，峰值在下午 2 点 (14h)
    ```bash
    ./targets/lookbusy -c 20-80 -r curve -P 24h -p 14h
    ```

*   **内存负载**: 占用 1GB 内存
    ```bash
    ./targets/lookbusy -m 1GB
    ```

*   **内存负载 (曲线模式)**: 内存使用在 512MB 到 1GB 之间波动，周期为 24 小时，峰值在下午 2 点 (14h)
    ```bash
    ./targets/lookbusy -m 512MB-1GB -R curve --mem-curve-period 24h --mem-curve-peak 14h
    ```

*   **磁盘负载**: 在 `/tmp` 目录下生成 10GB 文件并进行 I/O 操作
    ```bash
    ./targets/lookbusy -d 10GB -f /tmp
    ```

*   **组合使用**: 同时产生 CPU (30%) 和内存 (512MB) 负载
    ```bash
    ./targets/lookbusy -c 30 -m 512MB
    ```

### 命令行选项

使用 `-h` 或 `--help` 查看完整帮助信息：

```text
  -h, --help           命令行帮助
  -v, --verbose        详细输出
  -q, --quiet          静默模式
  -c, --cpu-util=PCT   CPU 利用率百分比
  -n, --ncpus=NUM      CPU 核心数
  -r, --cpu-mode=MODE  利用率模式 ('fixed' 或 'curve')
  -m, --mem-util=SIZE  内存使用量 (支持范围)
  -R, --mem-mode=MODE  内存模式 ('fixed' 或 'curve')
  -d, --disk-util=SIZE 磁盘文件大小
  ...
```

## 项目结构

*   `src/`: 源代码目录
*   `man/`: 手册页文档
*   `build-aux/`: 构建辅助脚本

## 许可证

GPL v2
