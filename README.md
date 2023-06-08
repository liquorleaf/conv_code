# Convolutional Code

《大数据存储技术》期末项目。

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
使用apt安装tree软件包进行可视化。
```
.
├── CMakeLists.txt
├── data                         # 目录：测试数据及输出 
│   ├── example0.txt             # 文件：测试数据0，字母表和数字
│   ├── example1.jpg             # 文件：测试数据2，一段较长的中文文本
│   ├── example2.txt             # 文件：测试数据2，一段较长的中文文本
│   ├── recovered_example0.txt   # 文件：测试0结果，运行时自动生成
│   ├── recovered_example1.png   # 文件：测试1结果，运行时自动生成
│   └── recovered_example2.txt   # 文件：测试2结果，运行时自动生成
├── examples
│   ├── burst_error.cpp
│   ├── spread_error.cpp
│   └── storage_file.cpp
├── exec
│   ├── burst_error
│   ├── spread_error
│   └── storage_file
├── include
│   ├── binary_file.h
│   └── conv_code.h
├── libs
│   └── libconvolutional_erasure_code.so
├── README.md
└── src
    ├── binary_file.cpp
    └── conv_code.cpp

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
3. 单文件读写与损坏实验，可选附加参数：1文件路径（相对或绝对）、2损坏方式（0为分散，其它为集中）、3分散损坏比特数或集中损坏的块的字节数（位置皆为随机）、是否十六进制打印文件内容（0为不打印，其它为打印）。
```
cd conv_code/exec/
./storage_file
```

## I/O示例
1. 分散损坏实验
```


```

2. 集中损坏实验
```



```

3. 单文件读写与损坏实验
```

```
