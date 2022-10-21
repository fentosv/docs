---
title: 部署你的 Astro 站点至 Vercel
description: 如何使用 Vercel 将你的 Astro 网站部署到网络上。
layout: ~/layouts/DeployGuideLayout.astro
---

您可以使用 [Vercel](http://vercel.com/) 零配置的将 Astro 站点部署到其全球边缘网络中。

本指南包括通过 Vercel 网站 UI 或 Vercel 的 CLI 将 Astro 站点部署到 Vercel 的相关说明。

## 项目配置

你的 Astro 项目可以作为静态站点或服务端渲染站点（SSR）部署到 Vercel。

### 静态站点

默认情况下，你的 Astro 项目是一个静态站点。你无需任何额外配置即可将静态 Astro 站点部署到 Vercel。

:::note
目前在 Vercel 上显示 Astro 网站的 404 页面存在一些问题。在解决这些问题之前，你需要在项目的根目录中添加以下配置文件：

```json title="vercel.json"
{
  "cleanUrls": true
}
```

:::

### SSR 适配器

要在 Astro 项目中启用 SSR 并在 Vercel 上部署：

使用以下 `astro add` 命令为你的 Astro 项目中添加 [Vercel 适配器](/zh-cn/guides/integrations-guide/vercel/) 以开启 SSR。此命令将安装适配器并同时自动对你的 `astro.config.mjs` 文件进行适当的配置。

```bash
npx astro add vercel
```

如果你更喜欢手动安装适配器，你需要完成以下两个步骤：

1. 使用你喜欢的包管理器将 [`@astrojs/vercel` 适配器](/zh-cn/guides/integrations-guide/vercel/) 安装到项目的依赖项中。如果你正在使用 npm 或不确定想要使用什么包管理器，请在终端中运行：

    ```bash
      npm install @astrojs/vercel
    ```

2. 在你的 `astro.config.mjs` 配置文件中添加以下配置。

    ```js title="astro.config.mjs" ins={2, 5-6}
    import { defineConfig } from 'astro/config';
    import vercel from '@astrojs/vercel/serverless';

    export default defineConfig({
      output: 'server',
      adapter: vercel(),
    });
    ```

## 如何部署

您可以通过 Vercel 的网站 UI 或使用 Vercel 提供的官方 CLI（命令行界面）部署 Astro 站点到 Vercel。部署静态站点和 SSR 站点的过程相同。

### 通过网站 UI 部署

1. 将你的代码推送到你的在线 Git 存储库（GitHub、GitLab、BitBucket 等）。
2. [导入你的项目](https://vercel.com/new) 至 Vercel。
3. Vercel 将自动检测 Astro 项目并自动为其配置正确的设置。
4. 你的应用程序已部署完成了！（例如：[astro.vercel.app](https://astro.vercel.app/)）

在你的项目完成导入和部署后，所有后续内容推送到（生产分支外的）分支都将自动生成 [预览部署（Preview Deployments）](https://vercel.com/docs/concepts/deployments/environments#preview)，以及对生产分支（通常是名为“main”的分支）所做的任何更改都将自动被部署为 [生产部署（Production Deployment）](https://vercel.com/docs/concepts/deployments/environments#production)。

📚 详细请参考 Vercel 文档的 [Git 集成](https://vercel.com/docs/concepts/git)部分。

### 通过 CLI 部署

1. 安装 [Vercel CLI](https://vercel.com/cli) 并运行 `vercel` 以进行部署。

    ```bash
    npm install -g vercel
    vercel
    ```

2. Vercel 将自动检测 Astro 项目并自动为其配置正确的设置。
3. 当被问及 `Want to override the settings? [y/N]`（想要覆盖配置吗？），选择 `N`（No）。
4. 你的应用程序已部署完成了！（例如：[astro.vercel.app](https://astro.vercel.app/)）