---
title: protocol buffer
toc: false
date: 2017-05-12 16:06:17
updated: 2017-05-12 16:06:17
description:
tags:
categories:
---

protobuf在Windows环境下获取，编译器(c++ version)生成和一般使用方法。  

<!-- more -->  

- **Protocol Buffer**  

> Protocol Buffers (a.k.a., protobuf) are Google's language-neutral, platform-neutral, extensible mechanism for serializing structured data. You can find protobuf's documentation on the Google Developers site.  

> To install protobuf, you need to install the protocol compiler (used to compile .proto files) and the protobuf runtime for your chosen programming language.

项目地址 [google/protobuf - github](https://github.com/google/protobuf)  
依据README描述，需要做的是搞定compiler和runtime，其中compiler由C++实现，只有runtime提供各语言版本。  
我的主要使用方式是Win/C++，关注`src`和`cmake`目录。  
准备工具，`CMake`([下载](https://cmake.org/download/))和`Virtual Studio`  

> 若只使用发布版本，可直接下载，参考protobuf项目[README](https://github.com/google/protobuf/blob/master/src/README.md)中的C++ Installation - Windows部分 ：
> > C++ Installation - Windows  
> > If you only need the protoc binary, you can download it from the release page:  
> > https://github.com/google/protobuf/releases  
> > In the downloads section, download the zip file protoc-$VERSION-win32.zip. It contains the protoc binary as well as public proto files of protobuf library.  
> > To build from source using Microsoft Visual C++, see cmake/README.md.  
> > To build from source using Cygwin or MinGW, follow the Unix installation instructions, above.

- **compiler**  

建立安装目录
```cmd
C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\bin\amd64>d:
D:\>cd git\protobuf
D:\git\protobuf>mkdir install
```
gmock  
```cmd
// 不做unit test，所以不处理gmock模块，下一步生成工程文件时需添加命令选项
-Dprotobuf_BUILD_TESTS=OFF
```

生成Virtual Studio 2012(11.0)工程文件
```cmd
D:\git\protobuf>cd ..\cmake
D:\git\protobuf\cmake>mkdir build & cd build
D:\git\protobuf\cmake\build>mkdir solution & cd solution
D:\git\protobuf\cmake\build\solution>cmake -G "Visual Studio 11 2012 Win64" -DCMAKE_INSTALL_PREFIX=../../../../install ../.. -Dprotobuf_BUILD_TESTS=OFF
```
至此，`solution`目录下已经生成vs 2012的工程文件。
下一步，编译protobuf源码
