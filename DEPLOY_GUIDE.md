# 蓝空新芽实践队网站部署指南

## 📋 目录

1. [快速部署到GitHub Pages](#1-快速部署到github-pages)
2. [跨设备编辑方案（github.dev）](#2-跨设备编辑方案githubdev)
3. [自定义域名配置](#3-自定义域名配置)
4. [自动更新机制](#4-自动更新机制)
5. [日常维护指南](#5-日常维护指南)

---

## 1. 快速部署到GitHub Pages

### 步骤1：创建GitHub仓库

1. 打开 [GitHub](https://github.com) 并登录你的账号
2. 点击右上角的 **+** → **New repository**
3. 填写仓库信息：
   - **Repository name**: `lankonxinya`（或你喜欢的名字）
   - **Description**: 北航蓝空新芽实践队招募网站
   - **Visibility**: Public（公开）
   - **不要勾选** "Add a README file"（我们已经有index.html）
4. 点击 **Create repository**

### 步骤2：上传网站文件

#### 方法A：网页上传（简单）

1. 在新建的仓库页面，点击 **uploading an existing file**
2. 将 `lankonxinya_website` 文件夹中的所有文件拖拽到上传区域：
   - `index.html`
   - `qrcode.png`（二维码图片）
3. 点击 **Commit changes**

#### 方法B：使用Git命令

```bash
# 进入网站目录
cd E:\Applications in E\workBuddy\workspace\lankonxinya_website

# 初始化Git（如果还没有）
git init

# 添加所有文件
git add .

# 提交
git commit -m "蓝空新芽实践队网站 v1.0"

# 添加远程仓库（替换YOUR_USERNAME为你的GitHub用户名）
git remote add origin https://github.com/YOUR_USERNAME/lankonxinya.git

# 推送
git push -u origin main
```

### 步骤3：启用GitHub Pages

1. 在仓库页面，点击 **Settings**（设置）
2. 左侧菜单找到 **Pages**
3. 在 **Source** 部分：
   - 选择 **Deploy from a branch**
   - Branch 选择 **main**（或 master）
   - 点击 **Save**
4. 等待 1-2 分钟，你的网站就会上线！

🎉 网站地址：`https://YOUR_USERNAME.github.io/lankonxinya/`

---

## 2. 跨设备编辑方案（github.dev）

### 为什么用github.dev？

- ✅ **无需安装任何软件**：直接在浏览器中编辑
- ✅ **无需配置开发环境**：任何电脑都可以
- ✅ **保存即自动部署**：修改后网站自动更新
- ✅ **版本管理**：所有修改都有记录，可以回退

### 使用github.dev在线编辑

1. 在浏览器中打开你的GitHub仓库页面
2. 按键盘上的 **.**（点号键）
   - 或者将URL中的 `github.com` 改成 `github.dev`
   - 例如：`https://github.com/YOUR_USERNAME/lankonxinya` → `https://github.dev/YOUR_USERNAME/lankonxinya`
3. 仓库会以在线VS Code编辑器的形式打开
4. 直接编辑 `index.html` 文件
5. 按 **Ctrl + S** 保存
6. 等待约1分钟，网站自动更新！

### 修改网站内容的技巧

#### 修改联系方式
直接在HTML中找到并修改：
```html
<div class="value" id="displayPhone">15523090410</div>
```

#### 修改二维码
1. 准备好新的二维码图片
2. 在编辑器中删除旧的 `qrcode.png`
3. 点击 **Add file** → **Upload files** 上传新图片
4. 确保新图片文件名也是 `qrcode.png`

#### 修改招募信息
找到对应的文字直接修改即可，保存后自动生效。

---

## 3. 自定义域名配置

### 为什么需要自定义域名？

- 原地址 `lxs-lab.github.io/lankonxinya/` 看起来不专业
- 使用自定义域名更专业、更易记

### 可选域名方案

| 方案 | 地址示例 | 费用 | 配置难度 |
|------|----------|------|----------|
| 免费子域名 | `lankonxinya.com` | 免费 | 简单 |
| GitHub Pages免费域名 | `lankonxinya.github.io` | 免费 | 简单 |
| 付费域名 | `iyfcs.cn` 等 | ¥20-50/年 | 中等 |

### 配置步骤（以阿里云域名为例）

1. **购买域名**
   - 阿里云万网、腾讯云等平台
   - 推荐 `.cn` 或 `.com` 域名
   - 年费约20-50元

2. **在GitHub仓库配置**
   - 进入仓库 **Settings** → **Pages**
   - 在 **Custom domain** 输入你的域名
   - 勾选 **Enforce HTTPS**（强制HTTPS）

3. **添加DNS解析**
   - 登录域名控制台
   - 添加以下记录：

   | 记录类型 | 主机记录 | 记录值 |
   |----------|----------|--------|
   | CNAME | www | `YOUR_USERNAME.github.io` |
   | A | @ | `185.199.108.153` |

   或者更简单的方式（如果支持）：
   - 添加一条 CNAME 记录指向 `YOUR_USERNAME.github.io`

4. **等待生效**
   - DNS解析通常10分钟-24小时生效
   - 生效后访问你的域名即可

---

## 4. 自动更新机制

### GitHub Actions 自动部署（推荐）

创建 `.github/workflows/deploy.yml` 文件：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
```

这样每次 `git push` 后，网站会自动更新！

### 手动更新流程

1. 修改 `index.html` 内容
2. 打开 GitHub 仓库
3. 点击 **Add file** → **Edit file**
4. 修改后点击 **Commit changes**
5. 等待1-2分钟，网站自动更新

---

## 5. 日常维护指南

### 定期检查事项

| 事项 | 频率 | 说明 |
|------|------|------|
| 二维码有效期 | 每周 | 微信群二维码7天过期 |
| 网站访问 | 每周 | 确认可正常访问 |
| 内容更新 | 按需 | 招募信息、联系方式等 |

### 修改二维码步骤

1. 登录微信获取新二维码截图
2. 打开 https://cli.im 或 https://www.qrcode-monkey.com/
3. 上传截图生成二维码图片
4. 保存为 `qrcode.png`
5. 在GitHub仓库中替换旧文件
6. 同时更新 `CONFIG` 中的日期

### 二维码过期提醒

网站已内置过期检测功能：
- 访问时带 `?admin=buaa2026` 参数会显示过期提醒
- 例如：`https://your-domain.com/?admin=buaa2026`

---

## 📞 技术支持

如有问题，请联系：
- 负责人微信：15523090410

---

*最后更新：2026年5月*
