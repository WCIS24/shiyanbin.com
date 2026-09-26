# 个人网站 · 测试页

当前版本是纯静态的设计预览，仅含占位文案，没有个人资料、联系方式或真实作品内容。

网站采用 **GitHub 仓库 + GitHub Actions + GitHub Pages**。网站运行在 GitHub 的托管服务上，不依赖本机开机。

测试页面已发布：[打开 HTTPS 测试页](https://wcis24.github.io/shiyanbin.com/)。阿里云自定义域名接入暂被账号实名认证阻挡，验收进度和后续步骤见 [部署记录](DEPLOYMENT.md)。

## 本地预览

在项目目录运行：

```sh
python3 preview.py
```

然后打开终端打印的本地地址。默认端口为 4173，可通过 `python3 preview.py --port 4174` 更换。预览仅绑定本机。

## 文件

- `site/dist/index.html`：页面结构和占位文案。
- `site/dist/styles.css`：桌面、平板和手机布局。
- `site/dist/assets/`：页面使用的本地图片。
- `.github/workflows/deploy-pages.yml`：将 `site/dist` 自动发布到 GitHub Pages。

无需安装依赖或执行构建。可以将 `site/dist` 中的完整内容交给支持静态网站的托管服务。

## 更新网站

修改 `site/dist/` 后提交并推送到 `main`，GitHub Actions 会自动发布。也可以从仓库 Actions 页面手动运行发布流程。网站只发布 `site/dist/` 中的文件。

此仓库目前为公开仓库。网站目录外的资料虽不会作为网页发布，推送到 GitHub 后仍会出现在公开仓库中；私人资料请保留在仓库外。

当前页面通过 `noindex, nofollow` 标记为测试内容；正式上线前应填写确认后的内容，并调整搜索引擎索引设置。
