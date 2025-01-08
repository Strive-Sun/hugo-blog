# 个人博客系统

这是一个基于 Hugo 框架开发的个人博客系统，提供了文章发布、分类管理、标签管理等功能。

## 功能特点

* 文章管理：支持 Markdown 格式写作
* 分类管理：文章分类功能
* 标签系统：文章标签管理
* 响应式设计：适配各种设备屏幕
* 文章归档：按时间归档文章
* 深色模式：支持自动/手动切换主题
* 代码高亮：支持多种编程语言
* SEO 优化：搜索引擎友好

## 技术栈

* Hugo 0.125.7+
* PaperMod 主题
* Markdown
* GitHub Actions（自动部署）
* Cloudflare Pages（静态网站托管）

## 环境要求

* Hugo Extended 0.125.7 或更高版本
* Git
* 文本编辑器（推荐使用 VS Code）

## 安装步骤

1. 克隆项目到本地：
```bash
git clone https://github.com/Strive-Sun/hugo-blog.git
cd hugo-blog
```

2. 安装 Hugo（Windows）：
```bash
# 方法1：使用 Chocolatey
choco install hugo-extended

# 方法2：手动安装
# 从 https://github.com/gohugoio/hugo/releases 下载 Hugo Extended
# 解压并添加到系统环境变量
```

## 本地预览

1. 启动 Hugo 服务器：
```bash
hugo server -D
```

2. 在浏览器中访问：
* 博客预览：http://localhost:1313/

## 项目结构

```
hugo-blog/
├── content/              # 文章内容
│   └── posts/           # 博客文章
├── static/              # 静态文件
│   └── images/         # 图片资源
├── themes/              # 主题文件
│   └── PaperMod/      # PaperMod 主题
├── config.yaml          # 部署配置
├── hugo.toml           # Hugo 配置
└── README.md           # 项目说明
```

## 写作指南

1. 创建新文章：
```bash
hugo new content posts/my-first-post.md
```

2. 文章格式：
```markdown
---
title: "文章标题"
date: 2024-01-08
tags: ["标签1", "标签2"]
categories: ["分类"]
draft: false
---

文章内容...
```

## 部署说明

1. 推送到 GitHub：
```bash
git add .
git commit -m "更新内容"
git push
```

2. Cloudflare Pages 会自动：
   - 检测代码更新
   - 构建静态文件
   - 部署到 CDN 网络

## 注意事项

1. 确保 Hugo 版本 >= 0.125.7
2. 文章图片放在 static/images 目录
3. 定期备份文章内容
4. 推送前先本地预览

## 许可证

本项目采用 MIT 许可证 