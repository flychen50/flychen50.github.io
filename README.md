# flychen50.github.io · Astro Blog Draft

把 GitHub Pages 个人站点迁移到 Astro，首发文章是「Transformer 原理 · 图文速通」，并带来博客技术栈建议。页面使用暗色霓虹视觉与纯 SVG 示意图，可直接作为未来博客的首页或文章模版。

## 技术栈

- [Astro 5](https://astro.build) · 只输出静态文件，适合 GitHub Pages
- 原子化设计的自定义 CSS（`src/styles/global.css`），后续可升级 Tailwind/UnoCSS
- 纯 `.astro` 页面与 layout（`src/pages/index.astro` + `src/layouts/BaseLayout.astro`），方便逐步替换为多篇文章
- 自定义域名 `blog.97551200.xyz` 已复制到 `public/CNAME`，构建时也会带上

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

- `/` Transformer 原理 + 博客技术栈建议
- `/gpt-1` 预训练 + 任务微调
- `/gpt-2` 大规模自回归与 zero-shot
- `/gpt-3` 提示学习与 175B 模型

## 后续方向

- 使用 `src/content/blog` + MDX 撰写更多文章，抽出卡片/图表组件。
- 集成 Tailwind（`npx astro add tailwind`）或 UnoCSS，方便主题扩展。
- 新增 RSS、Sitemap、文章列表与标签导航，并配置 GitHub Actions workflow。
