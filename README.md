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

1. 推荐使用 [`peaceiris/actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages) 工作流，在 `main` push 后执行 `npm install && npm run build`。
2. 将 `dist/` 发布到 `gh-pages` 分支（或 `docs/` 目录）以保持 `main` 干净。
3. 若使用自定义域名，确保 workflow 把 `public/CNAME` 同步到发布分支；本仓库已经内置该文件。
4. 在仓库的 **Pages** 设置中把发布源指向 `gh-pages` → `/`。

## 目录结构

```
├── public/          # 静态资源 & CNAME
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css
├── astro.config.mjs # 站点元数据
├── package.json
└── tsconfig.json
```

## 后续方向

- 使用 `src/content/blog` + MDX 撰写更多文章，抽出卡片/图表组件。
- 集成 Tailwind（`npx astro add tailwind`）或 UnoCSS，方便主题扩展。
- 新增 RSS、Sitemap、文章列表与标签导航，并配置 GitHub Actions workflow。
