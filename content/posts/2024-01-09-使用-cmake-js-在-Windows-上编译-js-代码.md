---
title: "使用 cmake.js 在 Windows 上编译 js 代码"
date: 2024-01-09T20:25:00+08:00
draft: false
tags: ["Node.js", "CMake", "Windows", "C++"]
categories: ["技术笔记"]
---

这是一份详细的 cmake.js 编译指南，教你如何在 Windows 上编译 js 代码。包含环境搭建、编译配置、使用说明等完整操作流程。

## 前言 🚀

因要给鸿蒙手机提供打包好的 C++ 库，鸿蒙系统的应用层是 js 写的，底层是 C++ 写的，故为提高鸿蒙开发效率，需要将其他端的 C++ 库通过 napi 打包成能 node.js 下运行的动态库。

但是平时多用 Windows 开发，所以要在 Windows 本地调试 js 代码，查看接口是否正常，如果正常就可以通过鸿蒙工具链打包成 arm64 的动态库了。

## 环境说明 💻

而 Windows 是 x86 架构，即要将所有 C++ 库依赖的三方库都编译成 native，即 dll 或者 lib，再通过 cmake.js 提供的编译工具，打包成 .node 库就可以本地调试了。

> ⚠️ 注意：鸿蒙库是 arm64 的 so 库，不可以在非 arm64 架构上调试和运行，此处指 Windows 之类的 x86 架构。譬如你想在 Mac 上调试 js 代码，那就要使用 Mac 提供的工具链对所有的三方库 native 化（重新编译），才可以调试和运行。

## 开发准备 📝

cmake.js 官方文档：[cmake-js](https://github.com/cmake-js/cmake-js)

开发需要准备：
1. C++ 源码 📄
2. CMakeLists.txt 📄

这两个缺一不可，其中 C++ 源码中需要包含写好的 napi 代码，即通过 napi 函数打包 C++ 代码。

napi 相关文档可以参考：[Node.js v20.17.0 文档](https://nodejs.org/docs/latest-v20.x/api/n-api.html)

## 环境搭建 🛠️

1. 安装 Node.js 📦
   - 打开命令行窗口（bash 或者 powershell）
   - 下载安装好 node.js 就可以使用 npm 命令了

2. 安装 cmake-js ⚙️
```bash
npm install cmake-js
```

3. 配置环境 🔧
在 CMakeLists.txt 同级目录下配置（这步很重要，不配置的话就找不到 napi 函数的符号文件）：
```bash
cmake-js configure
```

4. 指定 Visual Studio 版本 🎯
Windows 编译库默认使用 msvc，需要指定 Visual Studio 版本：
```bash
npm config set cmake_js_G "Visual Studio 16"
```

> - Visual Studio 16 对应 vs2019
> - Visual Studio 17 对应 vs2022

## 编译说明 🔨

1. cmake-js 默认是 x64 编译，如果需要编译成 x86，可以使用：
```bash
npm config set cmake_js_arch ia32
cmake-js compile cmake -G "Visual Studio 16 2019" -A Win32
```

⚠️ 注意：第二行命令容易在访问 ia32 cmake.js 资源时出现失败的问题，暂时没有找到解决方法（可能先在本地下载好 ia32 的资源就能解决）。

2. 使用 x64 时，CMakeLists.txt 需要指定平台：
```cmake
if(WIN32 OR CMAKE_SYSTEM_NAME STREQUAL "Windows")
  if(CMAKE_GENERATOR MATCHES "Visual Studio")
    set(CMAKE_GENERATOR_PLATFORM x64)
    set(CMAKE_GENERATOR_TOOLSET "host=x64" CACHE STRING "Platform Toolset" FORCE)
  else()
    set(CMAKE_C_COMPILER clang-cl)
    set(CMAKE_CXX_COMPILER clang-cl)
  endif()
endif()
```

3. 编译命令 ⚡
```bash
cmake-js compile
```

## 使用生成的库 📚

编译完成后会生成 .node 文件，在 js 代码中使用：

```javascript
const { Lib } = require('./build/Release/xxx.node');
// ... 其他代码
```

测试运行：
```bash
node test.js
```

## 常用配置命令 ⚙️

```bash
# 关闭 SSL 验证
npm set strict-ssl false

# 设置编译架构
npm config set cmake_js_arch x64

# 设置代理
set HTTP_PROXY=[IP]:[PROT]
set HTTPS_PROXY=[IP]:[PROT]

# 清除代理
npm config set proxy null
```

## 其他说明 📌

有些文章推荐使用 ffi 和 ref 去加载库文件调试，但实际安装会遇到很多问题，特别是安装 windows-build-tools 时：

```bash
npm install --global windows-build-tools
```

❌ 常见错误：
```
npm ERR! command C:\Windows\system32\cmd.exe /d /s /c node ./dist/index.js
Downloading python-2.7.15.amd64.msi
npm ERR! Error: GET https://npm.taobao.org/mirrors/python/2.7.15/python-2.7.15.amd64.msi returned 404
```

由于解决这些问题比较耗时，建议使用本文介绍的 cmake.js 方案。 