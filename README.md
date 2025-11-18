# flychen50.github.io · Transformer & GPT Notes

这是一个基于 Astro 的静态博客，专注分享 Transformer 以及 GPT-1/2/3 的核心原理、架构与训练技巧。页面使用暗色霓虹视觉与纯 SVG 示意图，内容聚焦技术拆解。

## 技术栈

- [Astro 5](https://astro.build) 生成静态站点
- 自定义 CSS（`src/styles/global.css`），可按需升级 Tailwind/UnoCSS
- 纯 `.astro` 页面与 layout（`src/pages/*` + `src/layouts/BaseLayout.astro`），便于后续迁移到 content collections
- 自定义域名 `blog.97551200.xyz` 通过 `public/CNAME` 保持生效

## 本地开发

```bash
npm install        # 安装依赖（首次）
npm run dev        # 启动开发服务器 http://localhost:4321
npm run build      # 产出静态文件到 dist/
npm run preview    # 预览构建结果
```

## 部署到 GitHub Pages

本仓库已内置 `.github/workflows/deploy.yml`，使用 GitHub 官方 Pages workflow。

1. 在 GitHub → **Settings → Pages** 中将 **Build and deployment** 的 Source 设置为 **GitHub Actions**。
2. 每次向 `main` 推送代码都会触发 workflow：`npm ci && npm run build`，并将 `dist/` 打包成 artifact。
3. `actions/deploy-pages` 负责把 artifact 发布到 Pages 环境；`public/CNAME` 会自动被包含进构建目录，保持自定义域生效。
4. 如需手动触发或回滚，可在 Actions 选项卡中运行/重新运行 workflow（支持 `workflow_dispatch`）。

## 目录结构

```
├── public/          # 静态资源 & CNAME
├── src/
│   ├── components/  # SiteNav 等复用组件
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   ├── index.astro   # Transformer 技术栈 + 原理
│   │   ├── gpt-1.astro   # 2018 GPT-1
│   │   ├── gpt-2.astro   # 2019 GPT-2
│   │   └── gpt-3.astro   # 2020 GPT-3
│   └── styles/
│       └── global.css
├── astro.config.mjs # 站点元数据
├── package.json
└── tsconfig.json
```

## 已完成的文章

- `/` Transformer 原理图解
- `/gpt-1` 预训练 + 任务微调
- `/gpt-2` 大规模自回归与 zero-shot
- `/gpt-3` 提示学习与 175B 模型

## 后续方向

- 使用 `src/content/blog` + MDX 撰写更多文章，抽出卡片/图表组件。
- 集成 Tailwind（`npx astro add tailwind`）或 UnoCSS，方便主题扩展。
- 新增 RSS、Sitemap、文章列表与标签导航，并配置 GitHub Actions workflow。
