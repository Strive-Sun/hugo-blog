---
title: "使用 VSCode 调试 Node.js 代码"
date: 2025-01-06
lastmod: 2025-01-06
draft: false
description: "详细介绍如何使用 VSCode 调试 Node.js 代码，包括环境配置、调试技巧、断点设置等内容，帮助开发者更高效地进行代码调试。"
tags: ['VSCode', 'Node.js', '调试']
categories: ['技术教程']
---


# 使用 VSCode 调试 Node.js 代码指南 🔍

本文将详细介绍如何使用 Visual Studio Code (VSCode) 来调试 Node.js 代码，帮助你更高效地进行开发和问题排查。

## 1. 环境准备 🛠️

### 1.1 必要软件安装

1. **Node.js**
   - 访问 [Node.js 官网](https://nodejs.org/)
   - 下载并安装最新的 LTS 版本
   - 验证安装：
     ```bash
     node --version
     npm --version
     ```

2. **Visual Studio Code**
   - 下载并安装 [VSCode](https://code.visualstudio.com/)
   - 安装 Node.js 调试插件（内置）

## 2. 调试配置 ⚙️

### 2.1 创建调试配置文件

1. 在 VSCode 中打开你的项目
2. 点击左侧的调试图标（或按 `Ctrl+Shift+D`）
3. 点击 "创建 launch.json 文件"
4. 选择 "Node.js" 环境

VSCode 会自动创建 `.vscode/launch.json` 文件，基本配置如下：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "启动程序",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}/app.js"
        }
    ]
}
```

### 2.2 配置说明

- **type**: 调试器类型，使用 "node" 表示 Node.js 调试器
- **request**: 请求类型，"launch" 表示启动新进程
- **name**: 配置名称，显示在调试配置下拉菜单中
- **program**: 启动时运行的文件
- **skipFiles**: 调试时要跳过的文件

## 3. 开始调试 🚀

### 3.1 设置断点

1. 在代码行号左侧点击设置断点
2. 或在代码行使用 `F9` 快捷键
3. 断点会显示为红色圆点

### 3.2 启动调试

1. 按 `F5` 启动调试
2. 或点击调试面板中的绿色播放按钮
3. 程序会在断点处暂停

### 3.3 调试控制

使用调试工具栏或快捷键：
- **继续 (F5)**: 继续执行到下一个断点
- **单步跳过 (F10)**: 执行当前行，不进入函数
- **单步调试 (F11)**: 进入函数内部
- **单步跳出 (Shift+F11)**: 跳出当前函数
- **重启 (Ctrl+Shift+F5)**: 重新启动调试
- **停止 (Shift+F5)**: 终止调试会话

## 4. 高级调试功能 💡

### 4.1 条件断点

1. 右键点击断点
2. 选择"编辑断点"
3. 输入条件表达式，如：`count > 5`

### 4.2 监视变量

1. 在调试面板中展开"监视"
2. 点击 + 添加表达式
3. 输入要监视的变量或表达式

### 4.3 调试控制台

1. 使用调试控制台执行命令
2. 在暂停状态下查看变量值
3. 使用 `console.log` 输出信息

## 5. 常见调试场景 🎯

### 5.1 异步代码调试

```javascript
async function fetchData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}
```

### 5.2 Express 应用调试

```json
{
    "type": "node",
    "request": "launch",
    "name": "启动 Express",
    "program": "${workspaceFolder}/app.js",
    "env": {
        "PORT": "3000"
    }
}
```

## 6. 调试技巧 💪

1. **使用 logpoints**
   - 右键断点选择"添加 logpoint"
   - 输入日志消息，不会暂停执行

2. **使用 source maps**
   - 确保启用 source maps
   - 在 `launch.json` 中设置 `"sourceMaps": true`

3. **调试生产环境**
   - 使用 `--inspect` 标志启动 Node.js
   - 配置远程调试

## 总结 📝

通过本文的学习，你应该能够：
- 配置 VSCode 的 Node.js 调试环境
- 使用断点和调试控制器
- 处理常见的调试场景
- 运用高级调试技巧

记住：
- 合理使用断点
- 熟练使用调试快捷键
- 善用监视和调试控制台

祝你调试顺利！🎉

> 参考链接：[使用 vscode 调试 nodejs 代码](https://www.cnblogs.com/strive-sun/p/18560976)

