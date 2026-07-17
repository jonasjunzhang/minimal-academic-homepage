# Minimal Academic Homepage

一个内容优先、加载迅速、易于维护的极简学术主页模板。页面由原生 HTML、CSS 和本地图片组成，适合直接部署到 GitHub Pages，也适合网络条件较差的访问者。

## 开发原则

- **内容优先的极简主义**：以白色背景、清晰的字体层级和克制的留白突出研究者本人及其工作，不添加与内容无关的装饰或交互。
- **把加载速度当作功能**：不使用框架、JavaScript、外部字体、CDN 或统计脚本；采用系统字体和压缩后的本地图片，减少网络请求与渲染延迟。
- **桌面优先，完整响应式**：优先保证电脑端的信息密度与阅读节奏，同时使用弹性网格和少量媒体查询适配手机，不维护两套页面。
- **直接编辑，容易扩展**：个人信息和所有条目集中在 `index.html`，视觉规则集中在 `styles.css`；News、Publications 和 Experience 都使用可复制的语义化区块。
- **语义与可访问性优先**：使用合适的标题层级、`time`、图片替代文本、键盘焦点样式和 `prefers-reduced-motion`，让页面在不同设备和辅助技术中保持可用。
- **保持部署无关**：图片、样式和页内链接均使用相对路径，不绑定域名、构建平台或服务端环境。

Contributor 添加功能时，应优先使用原生 HTML 和 CSS，只有在明确解决实际问题时才引入脚本或第三方依赖；新增资源应尽量保存在本地并压缩，同时检查桌面端和手机端的可读性。

## 模板特性

- 个人简介、照片，以及 Google Scholar、GitHub 和邮箱链接。
- News、Publications、Experience；Experience 支持本地机构 Logo。
- 白色背景的响应式单页设计，兼顾桌面端信息密度和手机端阅读体验。
- 零运行时依赖、零构建步骤，克隆后即可本地预览。
- 适用于个人域名、`username.github.io` 和 GitHub Pages 项目子路径。

## 目录结构

```text
.
├── index.html                    # 所有页面内容
├── styles.css                   # 视觉样式与响应式规则
├── assets/
│   ├── profile-placeholder.svg   # 示例头像，请替换
│   └── logo-*.webp               # 可选的机构 Logo
├── .nojekyll                    # 防止 GitHub Pages 执行 Jekyll
└── README.md
```

## Contributor：环境配置

本项目没有构建步骤，也没有 npm/pip 依赖。你只需要：

1. Git，用于克隆与提交修改。
2. 任意现代浏览器。
3. 用于本地服务的 Python 3（可选，macOS/Linux 通常已安装）。

克隆仓库后进入目录：

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
cd YOUR_REPOSITORY
```

## 本地调试

在项目根目录运行：

```bash
python3 -m http.server 8000
```

然后访问 [http://localhost:8000](http://localhost:8000)。修改 HTML 或 CSS 后刷新页面即可看到结果，停止服务请按 `Ctrl+C`。

如果 Windows 上的 Python 命令是 `py`，使用：

```powershell
py -m http.server 8000
```

也可以使用 VS Code Live Server 等纯静态服务器。不建议双击 `index.html` 作为日常调试方式，因为本地文件协议与 GitHub Pages 的 HTTP 环境不完全相同。

## 填写个人信息

在 `index.html` 中搜索以下注释，即可快速定位：

| 要修改的内容 | 搜索标记 | 说明 |
| --- | --- | --- |
| 中英文姓名、职位、简介、个人链接 | `PERSONAL INFO START` | 同时修改 `<title>` 和 `description` |
| 新闻 | `NEWS START` | 复制一个 `<article class="news-item">` |
| 工作或学术经历 | `EXPERIENCE START` | 复制一个 `<article class="experience-item">` |
| 论文 | `PUBLICATIONS START` | 复制一个 `<article class="publication">` |
| 页脚 | `<footer>` | 更新年份和姓名 |

### 替换照片

1. 准备一张竖版照片，建议比例为 `4:5`。
2. 将宽度压缩到约 `640px`，优先导出为 WebP，建议文件小于 `150 KB`。
3. 将文件保存为 `assets/profile.webp`。
4. 在 `index.html` 中把：

```html
src="./assets/profile-placeholder.svg"
```

改为：

```html
src="./assets/profile.webp"
```

并把 `alt="Portrait of Your Name"` 中的姓名改为你的姓名。不要把照片放在外部图床；本地图片通常更快、更可靠。

### 修改颜色和宽度

`styles.css` 开头的 `:root` 集中定义了设计变量：

```css
:root {
  --ink: #171714;
  --muted: #6f6e68;
  --line: #deddd7;
  --soft: #f4f3ee;
  --accent: #e44f2a;
  --page: 1240px;
}
```

只修改这几个值就可以完成大部分品牌定制。

## 添加 News

按照已有项目复制并修改：

```html
<article class="news-item">
  <time datetime="2026-08">Aug 2026</time>
  <p>Your update, with an optional <a href="#">link</a>.</p>
</article>
```

`datetime` 建议使用 `YYYY-MM` 或 `YYYY-MM-DD`，便于搜索引擎和辅助技术理解日期。

## 添加 Experience

复制一个完整的 `<article class="experience-item">...</article>` 区块，然后修改：

- `experience-logo`：默认显示机构缩写，也可以替换为本地 Logo 图片。
- `experience-period`：开始和结束时间；当前职位可使用 `Present`。
- `experience-location`：城市、国家或 `Remote`。
- `<h3>`：职位和机构名称，机构可添加官网链接。
- 最后一个 `<p>`：用一到两句话描述主要工作。

示例：

```html
<article class="experience-item">
  <div class="experience-logo" aria-hidden="true">
    <span>YI</span>
  </div>
  <div class="experience-meta">
    <p class="experience-period">
      <time datetime="2024-09">Sep 2024</time> — Present
    </p>
    <p class="experience-location">Your City</p>
  </div>
  <div class="experience-body">
    <h3>Research Scientist <span>at <a href="#">Your Institution</a></span></h3>
    <p>A concise description of your work and research focus.</p>
  </div>
</article>
```

### 添加机构 Logo

将机构 Logo 保存到 `assets/`，建议使用透明背景的横向 WebP 或 PNG，比例约为 `2:1`～`3:1`、宽度约 `240`～`360px`，并控制在 `40 KB` 以内。然后把缩写占位：

```html
<div class="experience-logo" aria-hidden="true">
  <span>YI</span>
</div>
```

替换为：

```html
<div class="experience-logo" aria-hidden="true">
  <img
    src="./assets/logo-your-institution.webp"
    alt=""
    width="320"
    height="120"
    loading="lazy"
  />
</div>
```

机构名称已经出现在同一条经历的标题中，因此 Logo 作为装饰图片使用空 `alt`，避免屏幕阅读器重复朗读。桌面端 Logo 容器固定为 `128px` 宽，高度自动与同一条经历的文字区域对齐，图片在白色留白中居中完整显示；手机端则使用紧凑的 `96 × 54px` 横向尺寸，避免长段文字把 Logo 拉得过高。`object-fit: contain` 会自动适配不同比例，无需为每个机构单独调整样式。

## 添加 Publications

复制完整的 `<article class="publication">...</article>` 区块，然后修改：

- `venue`：会议/期刊与年份。
- `<h3>`：论文标题。
- `authors`：作者列表，用 `<strong>` 标记你的姓名。
- `paper-links`：Paper、Code、Project 等链接，不需要的按钮可直接删除。

## GitHub Pages 部署

这是纯静态项目，可直接从分支根目录发布，不需要 GitHub Actions 或构建产物。

1. 在 GitHub 新建一个仓库，并将本项目推送到 `main` 分支。
2. 进入仓库的 **Settings → Pages**。
3. 在 **Build and deployment** 的 Source 中选择 **Deploy from a branch**。
4. Branch 选择 `main`，目录选择 `/(root)`，点击 **Save**。
5. 稍等片刻，Pages 页面会显示公开地址。

如果仓库名为 `YOUR_USERNAME.github.io`，地址通常为：

```text
https://YOUR_USERNAME.github.io/
```

如果是普通项目仓库，地址通常为：

```text
https://YOUR_USERNAME.github.io/YOUR_REPOSITORY/
```

模板中的 CSS、图片和页内链接全部使用相对路径，因此无需为项目子路径修改代码。

详细说明可查看 [GitHub 官方文档：Configuring a publishing source for your GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

### 自定义域名（可选）

在 **Settings → Pages → Custom domain** 中填写域名，按 GitHub 提示配置 DNS。建议开启 **Enforce HTTPS**。如果希望把域名配置也纳入版本控制，可在根目录添加文件 `CNAME`，内容只写域名，例如 `academic.example.com`。

## 提交前检查

- 在宽度约 `375px` 的手机视图和宽度约 `1440px` 的桌面视图中各检查一次。
- 逐个点击 Scholar、GitHub、Email 以及每篇论文的链接。
- 检查照片 `alt` 文本、页面 `<title>` 和 `description`。
- 确保没有遗留 `href="#"`、`Your Name` 或 `you@example.com` 等占位内容。
- 压缩图片，并保持所有资源在本地，避免引入外部字体或不必要的脚本。

## License

你可以自由使用、修改和发布这个模板。如果准备对外开源，建议根据你的需求补充正式的 `LICENSE` 文件。
