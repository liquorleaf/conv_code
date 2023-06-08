# Convolutional Code

2023《大数据存储技术》期末项目。

## 简介
该项目实现一个快速的(7,5)_8卷积码算法，并且具有两项主要功能：
1. 可以将一个二进制序列编码，并使用Hard-Viterbi算法译码。
2. 可以二进制读写文件，并且模拟其出现分散损坏或集中损坏时，卷积码的译码纠错效果。

## 已测试环境

* Ubuntu 20.04 LTS
* GNU Make 4.2.1
* cmake version 3.25.0

无第三方依赖软件包。

## 仓库结构
使用apt安装tree软件包进行可视化。注释为人工添加。
```
.
├── CMakeLists.txt
├── data                         # 目录：测试数据及输出 
│   ├── example0.txt             # 文件：测试数据0，字母表和数字
│   ├── example1.jpg             # 文件：测试数据1，一幅图片
│   ├── example2.txt             # 文件：测试数据2，一段较长的中文文本
│   ├── recovered_example0.txt   # 文件：测试0结果，运行时自动生成
│   ├── recovered_example1.jpg   # 文件：测试1结果，运行时自动生成
│   └── recovered_example2.txt   # 文件：测试2结果，运行时自动生成
├── examples                  # 目录：可执行测试程序的源码
│   ├── burst_error.cpp       # 文件：集中损坏测试（源码）
│   ├── spread_error.cpp      # 文件：分散损坏测试（源码）
│   └── storage_file.cpp      # 文件：存储文件读写与损坏测试（源码）
├── exec                   # 目录：可执行测试程序
│   ├── burst_error        # 文件：集中损坏测试
│   ├── spread_error       # 文件：分散损坏测试
│   └── storage_file       # 文件：存储文件读写与损坏测试
├── include             # 目录：存放声明的头文件
│   ├── binary_file.h   # 文件：声明BinaryFile类（源码）
│   └── conv_code.h     # 文件：声明ConvolutionalCode_7_5类（源码）
├── libs                                  # 目录：存放生成的动态库
│   └── libconvolutional_erasure_code.so  # 文件：卷积码和I/O动态库
├── README.md
└── src                     # 目录：存放实现的源码
    ├── binary_file.cpp     # 文件：实现BinaryFile类（源码）
    └── conv_code.cpp       # 文件：实现ConvolutionalCode_7_5类（源码）

```

## 运行
### 1.下载与编译
```
#! /bin/bash
cd /your/workspace/
git clone https://github.com/Yinshideguanghui/conv_code.git
mkdir build && cd build
cmake ..
make -j4
```

### 2.执行
1. 分散损坏实验，可选附加参数：1随机生成文件数、2每文件比特数、3最大损坏比特数。
```
cd conv_code/exec/
./spread_error
```
2. 集中损坏实验，可选附加参数：1随机生成文件数、2每文件比特数、3最大块字节数（每次损坏一块）。
```
cd conv_code/exec/
./burst_error
```
3. 单文件读写与损坏实验，可选附加参数：1文件路径（相对或绝对）、2损坏方式（0为分散，其它为集中）、3分散损坏比特数或集中损坏的块的字节数（位置皆*随机*）、是否十六进制打印文件（0为不打印，其它为打印）。
```
cd conv_code/exec/
./storage_file
```

## I/O示例
1. 分散损坏实验
```
~/conv_code$ ./exec/spread_error 1000 8000 32
当前分散损坏比特数 1/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 2/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 3/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 4/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 5/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 6/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 7/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 8/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 9/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 10/16000bits, 恢复后总误码率 1.25e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 11/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 12/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 13/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 14/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 15/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 16/16000bits, 恢复后总误码率 2.5e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 17/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 18/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 19/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 20/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 21/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 22/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 23/16000bits, 恢复后总误码率 1.25e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 24/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 25/16000bits, 恢复后总误码率 0, 无法恢复的文件数 0/1000
当前分散损坏比特数 26/16000bits, 恢复后总误码率 2.5e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 27/16000bits, 恢复后总误码率 1.25e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 28/16000bits, 恢复后总误码率 2.5e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 29/16000bits, 恢复后总误码率 1.25e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 30/16000bits, 恢复后总误码率 2.5e-07, 无法恢复的文件数 1/1000
当前分散损坏比特数 31/16000bits, 恢复后总误码率 5e-07, 无法恢复的文件数 2/1000
当前分散损坏比特数 32/16000bits, 恢复后总误码率 7.5e-07, 无法恢复的文件数 4/1000
~/conv_code$
```

2. 集中损坏实验
```
~/conv_code$ ./exec/burst_error 100 80000 32
当前集中损坏块大小 8bits/160000bits, 恢复后总误码率 2.5e-05, 无法恢复的文件数 100/100
当前集中损坏块大小 16bits/160000bits, 恢复后总误码率 5e-05, 无法恢复的文件数 100/100
当前集中损坏块大小 24bits/160000bits, 恢复后总误码率 5e-05, 无法恢复的文件数 100/100
当前集中损坏块大小 32bits/160000bits, 恢复后总误码率 7.5e-05, 无法恢复的文件数 100/100
当前集中损坏块大小 40bits/160000bits, 恢复后总误码率 0.0001, 无法恢复的文件数 100/100
当前集中损坏块大小 48bits/160000bits, 恢复后总误码率 0.0001, 无法恢复的文件数 100/100
当前集中损坏块大小 56bits/160000bits, 恢复后总误码率 0.000125, 无法恢复的文件数 100/100
当前集中损坏块大小 64bits/160000bits, 恢复后总误码率 0.00015, 无法恢复的文件数 100/100
当前集中损坏块大小 72bits/160000bits, 恢复后总误码率 0.00015, 无法恢复的文件数 100/100
当前集中损坏块大小 80bits/160000bits, 恢复后总误码率 0.000175, 无法恢复的文件数 100/100
当前集中损坏块大小 88bits/160000bits, 恢复后总误码率 0.0002, 无法恢复的文件数 100/100
当前集中损坏块大小 96bits/160000bits, 恢复后总误码率 0.0002, 无法恢复的文件数 100/100
当前集中损坏块大小 104bits/160000bits, 恢复后总误码率 0.000225, 无法恢复的文件数 100/100
当前集中损坏块大小 112bits/160000bits, 恢复后总误码率 0.00025, 无法恢复的文件数 100/100
当前集中损坏块大小 120bits/160000bits, 恢复后总误码率 0.00025, 无法恢复的文件数 100/100
当前集中损坏块大小 128bits/160000bits, 恢复后总误码率 0.000275, 无法恢复的文件数 100/100
当前集中损坏块大小 136bits/160000bits, 恢复后总误码率 0.0003, 无法恢复的文件数 100/100
当前集中损坏块大小 144bits/160000bits, 恢复后总误码率 0.0003, 无法恢复的文件数 100/100
当前集中损坏块大小 152bits/160000bits, 恢复后总误码率 0.000325, 无法恢复的文件数 100/100
当前集中损坏块大小 160bits/160000bits, 恢复后总误码率 0.00035, 无法恢复的文件数 100/100
当前集中损坏块大小 168bits/160000bits, 恢复后总误码率 0.00035, 无法恢复的文件数 100/100
当前集中损坏块大小 176bits/160000bits, 恢复后总误码率 0.000375, 无法恢复的文件数 100/100
当前集中损坏块大小 184bits/160000bits, 恢复后总误码率 0.0004, 无法恢复的文件数 100/100
当前集中损坏块大小 192bits/160000bits, 恢复后总误码率 0.0004, 无法恢复的文件数 100/100
当前集中损坏块大小 200bits/160000bits, 恢复后总误码率 0.000425, 无法恢复的文件数 100/100
当前集中损坏块大小 208bits/160000bits, 恢复后总误码率 0.00045, 无法恢复的文件数 100/100
当前集中损坏块大小 216bits/160000bits, 恢复后总误码率 0.00045, 无法恢复的文件数 100/100
当前集中损坏块大小 224bits/160000bits, 恢复后总误码率 0.000475, 无法恢复的文件数 100/100
当前集中损坏块大小 232bits/160000bits, 恢复后总误码率 0.0005, 无法恢复的文件数 100/100
当前集中损坏块大小 240bits/160000bits, 恢复后总误码率 0.0005, 无法恢复的文件数 100/100
当前集中损坏块大小 248bits/160000bits, 恢复后总误码率 0.000525, 无法恢复的文件数 100/100
当前集中损坏块大小 256bits/160000bits, 恢复后总误码率 0.00055, 无法恢复的文件数 100/100
~/conv_code$
```

3. 单文件读写与损坏实验（若显示，则依次十六进制打印源文件、编码码字、随机损坏后码字、译码结果）
```
~/conv_code$ ./exec/storage_file ../data/example0.txt 0 32 1
-----------------------------------------------------------------------
  \col|  00  01  02  03  04  05  06  07  08  09  0a  0b  0c  0d  0e  0f
row\  |
------|----------------------------------------------------------------
0000  |  61  62  63  64  65  66  67  68  69  6a  6b  6c  6d  6e  6f  70
0001  |  71  72  73  74  75  76  77  78  79  7a  31  32  33  34  35  36
0002  |  37  38  39  30  0a  61  62  63  64  65  66  67  68  69  6a  6b
0003  |  6c  6d  6e  6f  70  71  72  73  74  75  76  77  78  79  7a  31
0004  |  32  33  34  35  36  37  38  39  30  0a  61  62  63  64  65  66
0005  |  67  68  69  6a  6b  6c  6d  6e  6f  70  71  72  73  74  75  76
0006  |  77  78  79  7a  31  32  33  34  35  36  37  38  39  30  0a  00
-----------------------------------------------------------------------
-----------------------------------------------------------------------
  \col|  00  01  02  03  04  05  06  07  08  09  0a  0b  0c  0d  0e  0f
row\  |
------|----------------------------------------------------------------
0000  |  35  c3  85  ce  f5  cd  45  fb  35  f8  85  f5  f5  f6  45  2c
0001  |  35  2f  85  22  f5  21  45  17  35  14  85  19  f5  1a  46  70
0002  |  36  73  86  7e  f6  7d  46  4b  36  48  86  45  f6  46  46  9c
0003  |  36  9f  86  92  cd  73  bd  7e  cd  7d  7d  4b  0d  48  bd  45
0004  |  cd  46  7d  9c  0d  9f  bd  70  00  e2  f5  c3  85  ce  f5  cd
0005  |  45  fb  35  f8  85  f5  f5  f6  45  2c  35  2f  85  22  f5  21
0006  |  45  17  35  14  85  19  f5  1a  46  70  36  73  86  7e  f6  7d
0007  |  46  4b  36  48  86  45  f6  46  46  9c  36  9f  86  92  cd  73
0008  |  bd  7e  cd  7d  7d  4b  0d  48  bd  45  cd  46  7d  9c  0d  9f
0009  |  bd  70  00  e2  f5  c3  85  ce  f5  cd  45  fb  35  f8  85  f5
000a  |  f5  f6  45  2c  35  2f  85  22  f5  21  45  17  35  14  85  19
000b  |  f5  1a  46  70  36  73  86  7e  f6  7d  46  4b  36  48  86  45
000c  |  f6  46  46  9c  36  9f  86  92  cd  73  bd  7e  cd  7d  7d  4b
000d  |  0d  48  bd  45  cd  46  7d  9c  0d  9f  bd  70  00  e2  c0  00
-----------------------------------------------------------------------
-----------------------------------------------------------------------
  \col|  00  01  02  03  04  05  06  07  08  09  0a  0b  0c  0d  0e  0f
row\  |
------|----------------------------------------------------------------
0000  |  35  c1  85  ce  f5  cd  45  fb  35  f8  85  f5  f5  f6  c5  2c
0001  |  35  2f  85  22  f5  21  55  17  37  14  85  19  f5  1a  46  70
0002  |  36  73  c6  7e  f6  7d  46  cb  36  49  86  45  f2  46  46  9c
0003  |  3e  9f  8e  92  cd  73  bd  7e  cd  7d  7d  4b  0d  48  bd  45
0004  |  cd  c6  7d  bc  0d  9f  bd  70  00  e2  f5  c3  87  ce  f7  cf
0005  |  45  fb  35  f8  85  f5  f5  d6  45  2c  35  2f  85  32  f5  21
0006  |  45  17  35  14  85  11  f5  1a  46  70  36  73  86  7e  f4  7d
0007  |  46  4b  36  48  86  45  f6  46  46  9c  36  9f  87  92  cd  73
0008  |  bd  7e  cd  7d  7d  0b  0d  48  bd  45  cd  46  7d  9c  0d  9f
0009  |  fd  70  00  e2  f5  c3  85  cc  f5  cd  45  fb  35  f8  85  75
000a  |  f5  f6  47  2c  35  2f  85  22  f5  21  45  17  35  14  85  19
000b  |  f5  1a  46  70  36  73  86  7e  f6  7d  46  4b  36  48  86  45
000c  |  f6  46  47  9c  36  9f  86  92  cd  73  bd  76  cd  7d  5d  4b
000d  |  09  48  bd  4d  49  46  7d  9c  0d  9f  bd  70  00  e2  c0  00
-----------------------------------------------------------------------
-----------------------------------------------------------------------
  \col|  00  01  02  03  04  05  06  07  08  09  0a  0b  0c  0d  0e  0f
row\  |
------|----------------------------------------------------------------
0000  |  61  62  63  64  65  66  67  68  69  6a  6b  6c  6d  6e  6f  70
0001  |  71  72  73  74  75  76  77  78  79  7a  31  32  33  34  35  36
0002  |  37  38  39  30  0a  61  62  63  64  65  66  67  68  69  6a  6b
0003  |  6c  6d  6e  6f  70  71  72  73  74  75  76  77  78  79  7a  31
0004  |  32  33  34  35  36  37  38  39  30  0a  61  62  63  64  65  66
0005  |  67  68  69  6a  6b  6c  6d  6e  6f  70  71  72  73  74  75  76
0006  |  77  78  79  7a  31  32  33  34  35  36  37  38  39  30  0a  00
-----------------------------------------------------------------------
~/conv_code$
```
