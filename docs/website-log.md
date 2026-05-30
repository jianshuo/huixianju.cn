# huixianju.cn 网站日志 / Website Log

汇贤居业主委员会网站的运维与变更记录。最新在上。

> 注：本文件为公开仓库的一部分，**只记录非敏感信息**——不写密码、密钥、服务器 IP、实例 ID 等。

## 2026-05-30 — WordPress → Hugo 静态站迁移

- **变更**：把 huixianju.cn 从 WordPress 动态站迁移为 Hugo 静态站，源码托管于 GitHub，经 GitHub Actions 自动构建并发布到 GitHub Pages。
- **内容**：从 WordPress WXR 导出 + 本地 `uploads/` 转换，共 **174 篇文章**。全站 URL 保持 `/archives/<数字>/` 不变。
- **已排除**：8 篇密码保护文章（静态站无法做密码门，故不发布）、7 个 WordPress 系统页（登录/注册/找回密码/示例页等脚手架页）。
- **主题**：手写极简主题（`layouts/`），无第三方依赖。
- **构建**：Hugo extended，`relativeURLs = true`，链接全部页面相对，可在本地、子路径、自定义域名下点击。

### 主机与域名（现状）

- **原 WordPress 主机**：腾讯云（Tencent Cloud / 腾讯云）。迁移完成、观察无误后停机下线。
- **DNS**：迁移至 **Cloudflare** 托管。
- **目标**：GitHub Pages（自定义域名 huixianju.cn，`static/CNAME` 已设）。临时地址 https://jianshuo.github.io/huixianju.cn/ 。

### 待办（DNS 切换，操作者手动执行）

- [ ] 在 GitHub Pages 临时地址验证全站无误后，再切 DNS。
- [ ] 在 **Cloudflare** 把 huixianju.cn 指向 GitHub Pages：
      - apex：A 记录指向 `185.199.108.153 / 109.153 / 110.153 / 111.153`（或 CNAME 到 `jianshuo.github.io`）。
      - 若用 Cloudflare 代理（橙云），SSL/TLS 模式设为 **Full**，避免与 Pages 的 HTTPS 冲突；首次验证证书时可临时设为「仅 DNS / 灰云」。
- [ ] DNS 生效后在 GitHub Pages 勾选 **Enforce HTTPS**。
- [ ] 确认线上稳定数日后，再下线腾讯云上的 WordPress（先停机、保留备份，确认无需回退后再彻底删除）。
