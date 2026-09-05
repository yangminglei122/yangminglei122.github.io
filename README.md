# 杨明雷的个人主页

经典学术风格静态个人主页（参考 xiaodongml.github.io 版式），纯 HTML + CSS，无任何构建依赖，可直接托管在 GitHub Pages。

内容全部来自简历《CV of Yang Minglei, v3.0》，未作改写。

## 页面结构

| 文件 | 内容 |
|------|------|
| `index.html` | 简介（亮点）+ 荣誉奖励 |
| `education.html` | 教育背景 |
| `experience.html` | 工作经历 |
| `projects.html` | 项目经历 |
| `achievements.html` | 成果展示（机器人/系统图片与视频链接） |
| `grants.html` | 科研课题 |
| `publications.html` | 论文（期刊/会议/摘要）+ 专利 + 软件著作权 |
| `contact.html` | 联系方式 |
| `pagestyle.css` | 全站样式 |
| `images/` | 证件照 + 成果图片 |

## 部署到 GitHub Pages

本目录即仓库根目录，直接推送到 `yangminglei122.github.io` 仓库的 `main` 分支即可：

```bash
cd site   # 本目录

git init
git add .
git commit -m "初始化个人主页"
git branch -M main
git remote add origin https://github.com/yangminglei122/yangminglei122.github.io.git
git push -u origin main
```

推送后在 GitHub 仓库 **Settings → Pages** 确认：

- Source: **Deploy from a branch**
- Branch: **main**，目录 **/ (root)**

等待 1~2 分钟，即可访问 <https://yangminglei122.github.io>。

> 如果仓库已有内容，`git push` 前先执行 `git pull origin main --allow-unrelated-histories` 合并，或确认可以覆盖后使用 `git push -f origin main`。

## 本地预览

直接双击任意 `.html` 文件即可在浏览器中查看；或启动本地服务器：

```bash
cd site
python -m http.server 8000
# 浏览器打开 http://localhost:8000
```

## 修改内容

- 文字内容：直接编辑对应 `.html` 文件中的正文；
- 颜色/字体：编辑 `pagestyle.css` 顶部的各类样式（菜单蓝 `#000099`、悬停橙 `#FF6600`、分隔线深蓝 `#03188D` 等）；
- 图片：替换 `images/` 下同名文件（建议保持相近尺寸）；
- 每次修改后同步更新页脚的 `Last updated on ...` 日期。

## 注意

- 邮箱按参考站惯例做了防爬虫处理，显示为 `yangminglei122(at)163.com`；
- 成果视频存放在百度网盘，链接指向简历中给出的原始地址。
