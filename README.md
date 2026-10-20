# 个人主页

基于 **Jekyll** 的单页程序员自我介绍站点，通过 **GitHub Pages** 自动构建发布。

- 线上地址：<https://xiaofeng2824.github.io>
- 技术栈：Jekyll（GitHub Pages 内置版本）+ 原生 HTML / CSS / JavaScript
- 无前端框架、无 CDN、无第三方插件

## 目录结构

```
_config.yml              # 站点与个人信息（改这里）
_data/skills.yml         # 技能分组数据
_data/experience.yml     # 经历与方向卡片数据
_layouts/default.html    # 页面骨架
_includes/head.html      # <head>：meta / SEO / 样式
_includes/header.html    # 顶部导航
_includes/footer.html    # 页脚
index.html               # 页面主体（Hero / 关于 / 技能 / 项目 / 联系）
404.html                 # 自定义 404
assets/css/style.css     # 全部样式（设计令牌 + 组件）
assets/js/main.js        # 移动导航、滚动显现、导航高亮
assets/favicon.svg       # 站点图标
```

## 修改内容

### 1. 个人信息

编辑 `_config.yml` 中的 `author` 段：

```yaml
author:
  name: howard.cao
  initial: "H"           # 头像徽章上的字
  role: 软件工程师
  tagline: 一句话简介
  email: xiaofeng2824@163.com
  github: xiaofeng2824   # 只填用户名
  location: ""           # 如：中国 · 上海；留空则不显示
  status: ""             # 如：开放新机会；留空则不显示
```

同时建议更新 `title` 和 `description`（影响浏览器标题与 SEO）。

### 2. 技能

编辑 `_data/skills.yml`，每个分组会自动渲染成一张卡片：

```yaml
- group: 语言
  items:
    - Python
    - Go
```

### 3. 经历与方向

编辑 `_data/experience.yml`，每个条目会自动渲染成一张卡片：

```yaml
- name: Java 后端开发
  description: 一句话说明你做过什么
  tags: [Java, 后端]
```

需要恢复「项目」板块时，可以新建 `_data/projects.yml` 并在 `index.html` 中增加对应的列表区块。

### 4. 自我介绍正文

编辑 `index.html` 中 `#about` 区块里的 `<p>` 段落。

## 部署

本仓库是 GitHub Pages **用户主页**仓库，推送到 `main` 即可自动发布：

```bash
git add .
git commit -m "add personal homepage"
git push origin main
```

首次部署需要在 GitHub 仓库页确认一次 Pages 配置：

> **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**

之后每次 push 都会自动重新构建，通常 1 分钟内生效。

## 本地预览

本机 Windows 侧没有 Ruby，但 **WSL Debian 里已装好 Ruby 3.3 + Jekyll 4.3**，可直接预览：

```bash
wsl -d Debian -- bash -lc 'cd /mnt/d/code/xiaofeng2824.github.io && jekyll serve --host 0.0.0.0 --port 4000'
```

然后打开 <http://127.0.0.1:4000>。停止服务：

```bash
wsl -d Debian -- pkill -f "jekyll serve"
```

> 注意：WSL 访问 `/mnt/d` 时文件监听可能不生效，修改文件后如果没有自动重建，重启服务即可。

本地 Jekyll 4.3 与 GitHub Pages 使用的 Jekyll 3.x 版本不同，但本项目不使用任何插件、Liquid 语法也很基础，两边渲染结果一致。

其他可选方式：

1. **GitHub Codespaces**（预装 Ruby/Jekyll）
   ```bash
   bundle install
   bundle exec jekyll serve --livereload
   ```
2. **安装 RubyInstaller**（Windows：Ruby 3.x + DevKit）
   ```bash
   gem install jekyll bundler
   bundle exec jekyll serve --livereload
   ```
3. 只调样式时，可以用任意静态服务器查看 `assets/` 下的效果，但 Liquid 模板不会渲染。

## 设计说明

- 深色极简风格，青绿强调色，等宽字体点缀
- 移动优先，技能 4 列 / 项目自适应网格
- `IntersectionObserver` 做滚动显现与导航高亮，`prefers-reduced-motion` 下禁用动效
- 语义化结构、跳转链接、键盘可见焦点、Open Graph / favicon 等基础 SEO
