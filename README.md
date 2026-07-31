# blog-assets

静态资源仓库。

## 目录结构

```
blog-assets/
├── images/
│   ├── background/   # 大图背景、信件图
│   ├── decor/        # 装饰与小图
│   └── site/         # 站点级文件
├── font-awesome/     # 通用图标字体库
│   ├── css/          # font-awesome.min.css
│   └── fonts/        # 图标字体文件
├── live2d/           # 看板娘（Live2D）专属资源
│   ├── waifu.css
│   ├── waifu-tips.js
│   ├── live2d.min.js
│   ├── live2dcubismcore.min.js
│   ├── chunk/        # autoload 拆分包
│   └── model/        # 模型文件
└── README.md
```

## 引用方式（在前端代码中）

统一走 `src/utils/cdn.ts` 导出的 `cdn()` 帮助函数：

```ts
import { cdn } from '@/utils/cdn'

// 模板里
<img :src="cdn('images/decor/lazy.gif')" />

// 或 JS 里
const avatarImg = cdn('images/decor/avatar.jpg')
```

`index.html`、`*.css` 等无法使用 TS 变量的地方，直接写完整 jsDelivr URL：

```
https://cdn.jsdelivr.net/gh/JoseHe233/blog-assets/images/site/title.jpg
```

## 发布为可用的 CDN

1. 在本目录初始化并推送到 GitHub（仓库名 `blog-assets`，所有者 `JoseHe233`）：
   ```bash
   cd blog-assets
   git init
   git add -A
   git commit -m "init static assets"
   git branch -M main
   git remote add origin git@github.com:JoseHe233/blog-assets.git
   git push -u origin main
   ```
2. 资源即可通过 `https://cdn.jsdelivr.net/gh/JoseHe233/blog-assets/...` 访问（默认取 main 分支最新提交）。
3. 日后如需锁定版本（避免 jsDelivr 缓存导致线上不更新），打一个 tag 并改 `cdn.ts` 的 `CDN_BASE`：
   ```bash
   git tag v1
   git push origin v1
   ```
   然后把 `cdn.ts` 里的 base 改为 `https://cdn.jsdelivr.net/gh/JoseHe233/blog-assets@v1`。
