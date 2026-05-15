# 自定义域名配置指南 - lankonxinya.com

## 概述

本指南教你如何配置自定义域名 `lankonxinya.com`，让网站看起来更专业。

---

## 步骤一：购买域名

1. 访问域名注册商（推荐）：
   - 阿里云：https://wanwang.aliyun.com/
   - 腾讯云：https://dnspod.cloud.tencent.com/
   - 华为云：https://www.huaweicloud.com/product/dns.html

2. 搜索并购买 `lankonxinya.com`
   - 价格约 50-80 元/年

---

## 步骤二：配置DNS解析

购买域名后，进入域名管理后台，添加以下记录：

### 必须添加的记录：

| 记录类型 | 主机记录 | 记录值 | TTL |
|---------|---------|--------|-----|
| A | @ | 185.199.108.153 | 600 |
| A | @ | 185.199.109.153 | 600 |
| A | @ | 185.199.110.153 | 600 |
| A | @ | 185.199.111.153 | 600 |
| CNAME | www | lxs-lab.github.io | 600 |

### 说明：
- `@` 表示主域名（lankonxinya.com）
- `www` 表示带 www 的域名（www.lankonxinya.com）
- 4 个 A 记录是 GitHub Pages 的 IP 地址
- CNAME 记录让 www 子域名指向 GitHub Pages

---

## 步骤三：在GitHub上启用HTTPS

1. 访问：https://github.com/lxs-lab/lankonxinya/settings/pages
2. 找到 **Custom domain** 部分
3. 输入：`lankonxinya.com`
4. 点击 **Save**
5. 勾选 **Enforce HTTPS**（推荐）

---

## 步骤四：等待生效

- DNS 传播通常需要 **5分钟 - 48小时**
- 可以用以下命令检查：
  ```bash
  nslookup lankonxinya.com
  ```

---

## 完成后的访问地址

| 地址 | 说明 |
|------|------|
| https://lankonxinya.com | 主域名（推荐） |
| https://www.lankonxinya.com | 带 www |
| https://lxs-lab.github.io/lankonxinya/ | GitHub 原始地址（自动跳转） |

---

## 常见问题

**Q: 为什么访问显示 404？**
A: DNS 还没生效，等待几小时再试。

**Q: HTTPS 证书错误？**
A: GitHub 会自动申请 Let's Encrypt 证书，可能需要 24 小时。

**Q: 想换其他域名？**
A: 修改 CNAME 文件中的域名，重新推送，然后重复步骤二。

---

## 管理员访问方式

网站内容编辑需要密码访问：
```
https://lankonxinya.com/?admin=buaa2026
```

添加 `?admin=buaa2026` 参数后，右下角才会显示"编辑内容"按钮。

---

*配置完成时间：2026-05-15*
