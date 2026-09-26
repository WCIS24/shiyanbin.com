# GitHub Pages 部署记录

## 方案

- 源码仓库：https://github.com/WCIS24/shiyanbin.com
- 发布分支：`main`
- 发布流程：`.github/workflows/deploy-pages.yml`
- 公开网站文件：仅 `site/dist/`
- 网站托管：GitHub Pages，不使用本机作为线上服务器。
- 域名管理：阿里云，目标域名 `shiyanbin.com`，兼容 `www.shiyanbin.com`。

## 当前状态（2026-09-27）

- 已确认 GitHub 仓库存在、为公开仓库，浏览器已登录仓库所有者。
- 已准备 GitHub Actions 自动发布配置。
- GitHub Pages 启用、工作流部署、域名绑定和 HTTPS：正在配置，尚未完成验收。
- 阿里云 DNS：当前为 0 条记录，旧 Sites 地址未提交。
- 阿里云提示新注册域名的 NS 可能存在同步延迟；当前公网查询仍返回 NXDOMAIN，需要核对注册状态并等待正式委派。

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
