# GitHub Pages 部署记录

## 方案

- 源码仓库：https://github.com/WCIS24/shiyanbin.com
- 发布分支：`main`
- 发布流程：`.github/workflows/deploy-pages.yml`
- 公开网站文件：仅 `site/dist/`
- 网站托管：GitHub Pages，不使用本机作为线上服务器。
- 域名管理：阿里云，目标域名 `shiyanbin.com`，兼容 `www.shiyanbin.com`。

## 当前状态（2026-09-27）

- GitHub Pages 已启用，Source 为 GitHub Actions。
- 提交 `f083d1b6ba142cae9a0c8b0b7b8b510508a1c39b` 已推送到公开仓库。
- [发布运行 #1，第 2 次尝试](https://github.com/WCIS24/shiyanbin.com/actions/runs/36271431008) 已成功；第一次运行在 Pages 启用前失败。
- 公网测试地址：**https://wcis24.github.io/shiyanbin.com/**。
- 已验证首页、CSS 和主图均返回 HTTP 200，内容与本地发布文件逐字节一致；HTTPS 证书验证成功。
- 自定义域名尚未完成接入：尝试保存四条 A 记录时，阿里云明确返回 `Identity.Uncertified` / `账号未完成实名认证`。账号认证页面也显示尚未认证。
- DNS 记录未保存成功，阿里云权威服务器查询仍没有 A 记录；www 记录尚未提交。
- 注册局 RDAP 显示域名已注册，NS 为 `dns19.hichina.com` 和 `dns20.hichina.com`，同时处于 `client hold` 状态；公网查询返回 NXDOMAIN。此状态与账号认证阻碍分别记录，不能仅归因于 DNS 缓存。
- 已暂时移除 GitHub 中的自定义域名绑定，保留可访问的默认测试网址。自定义域名的 HTTPS 尚未签发、未验收。

## 接通自定义域名的剩余步骤

1. 域名持有人在 [阿里云账号认证](https://myaccount.console.aliyun.com/cert-info) 完成本人认证。身份资料不提交到此仓库。
2. 在阿里云域名控制台检查域名本身的实名认证/审核状态，确认 `client hold` 解除。
3. 在 GitHub Settings → Pages 重新绑定 `shiyanbin.com`，再添加下表 DNS 记录。
4. 核对公网 A/CNAME 解析，等待 GitHub 签发证书后启用 Enforce HTTPS。
5. 实际访问 `https://shiyanbin.com/`、`https://www.shiyanbin.com/` 和图片资源，确认 www 跳转、页面内容和 TLS 均正常后记录最终验收。

## GitHub Pages 需要的 DNS 记录

先在仓库 Settings → Pages 绑定自定义域名，再在阿里云添加：

| 类型 | 主机记录 | 记录值 |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `wcis24.github.io` |

DNS 和证书验证通过后，启用 GitHub Pages 的 Enforce HTTPS，并实际访问根域名、www 域名和图片资源。

参考：[GitHub 自定义域名官方文档](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)、[GitHub Pages 自动发布官方文档](https://docs.github.com/en/get-started/start-your-journey/deploying-your-website-automatically)。

## 日常维护

更新 `site/dist/` 后提交并推送到 `main`，工作流会自动发布。仓库里的其他文件不会打包成网站。`preview.py` 仅用于本地设计预览，不参与线上运行。

注意：当前仓库本身公开，提交到仓库的资料也会公开，即使它们不在网站发布目录内。

## 先前的 Sites 测试

切换到 GitHub Pages 之前曾完成一次 Sites 测试部署：

- 预览：https://shiyanbin-test-site.rosy-dune-1106.chatgpt.site
- 项目：`appgprj_6ab82d6f4d9c8191b32b310fcb65bdeb`
- 域名占位记录：`appgdom_6ab82e5b78ac8191a59eb84ae73fa399`（尚未解析到 Sites）。
- 独立源码历史保留在忽略目录 `.sites-runtime/publish-checkout/`。

后续正式更新使用 GitHub Pages 流程，不再使用 Sites 发布流程。
