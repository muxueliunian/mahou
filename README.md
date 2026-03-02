# Mahou

一句话：这是一个“自动生成日报图片”的项目。  
它会定时抓取几个网站的数据，拼成一张 `output.png`，然后提供在线链接给别的项目直接用。

## 它到底干什么

每天自动做这几步：

1. 抓数据（B 站热词、科技资讯、游戏资讯、一言、番剧日历）。
2. 用前端模板把数据渲染成一张长图。
3. 把图片发布到仓库 `output` 分支。
4. 你就可以用固定 URL 在别的地方引用这张图。

## 在线图片地址（可直接用）

- GitHub Raw（实时，无缓存）：  
  https://raw.githubusercontent.com/muxueliunian/mahou/output/output.png
- jsDelivr（有缓存，访问更稳）：  
  https://cdn.jsdelivr.net/gh/muxueliunian/mahou@output/output.png

## 项目结构（看懂就够）

- `render/common`：图片模板（React），负责“长什么样”。
- `mahiro`：抓取和整理数据。
- `server`：把模板 + 数据渲染成 png，也提供 HTTP 接口。
- `.github/workflows/generate.yml`：GitHub Actions 定时任务（自动生成并发布图片）。

## 本地跑一次（最小流程）

```bash
pnpm i
pnpm --filter @mahou/render-common build
pnpm --filter @xn-sakina/mahiro-mahou sync:bgm
pnpm --filter @mahou/http-server copy
pnpm --filter @mahou/http-server start -- --generate --compress
```

执行完后，图片会在：

```bash
server/output.png
```

## 注意事项

- 建议 Node 18（仓库也是按 Node 18 配的）。

## License

MIT
