# 杨明雷的个人主页

经典学术风格静态个人主页（参考 xiaodongml.github.io 版式）。

「数据 + 构建脚本」结构：内容放在 `data\*.ps1`，运行一次构建即可重新生成全部 HTML 页面。纯 PowerShell 实现，无需安装任何环境（Windows 自带）。

## 目录结构

```
site\                        # 本目录
│
├── data\                    # 🔵 数据源（本地文件，不上传 GitHub）
│   ├── site.ps1             #   全局配置：姓名、邮箱、照片、菜单、页脚
│   ├── index.ps1            #   首页：简介 + 荣誉奖励
│   ├── education.ps1        #   教育背景
│   ├── experience.ps1       #   工作经历
│   ├── projects.ps1         #   项目经历
│   ├── achievements.ps1     #   成果展示（图片/视频链接）
│   ├── grants.ps1           #   科研课题
│   ├── publications.ps1     #   论文 + 专利 + 软著
│   └── contact.ps1          #   联系方式
│
├── build.ps1                # 🟡 构建脚本（读取 data，生成 HTML）
├── build.cmd                # 🟡 双击这个 = 重新生成全部页面
│
├── *.html                   # ✅ 生成的 8 个页面（发布到 GitHub Pages）
├── pagestyle.css            # ✅ 全站样式
├── images\                  # ✅ 证件照 + 成果图片
└── README.md                # 本文件
```

## 日常更新：三步

1. **改内容**：用记事本或 VS Code 编辑 `data\` 下对应文件；
2. **重新生成**：双击 `build.cmd`（窗口显示“全部页面生成完毕”即成功，按任意键关闭）；
3. **发布**：

```bash
git add .
git commit -m "更新内容"
git push
```

等待 1~2 分钟 GitHub Pages 生效。发布前建议本地双击 `index.html` 检查效果。

## 数据文件怎么写

每个页面文件 = `title`（浏览器标签标题）+ `blocks`（内容块列表）。常用块类型：

| type | 作用 | 关键字段 |
|------|------|----------|
| `h1` | 大标题（深蓝） | `text` |
| `h2` | 小标题（绿色） | `text` |
| `p` | 段落 | `html`（可含 `<strong>` 等简单 HTML） |
| `ul` / `ol` | 圆点 / 编号列表 | `items`（字符串数组） |
| `item` | 经历/项目条目 | `date`、`org`、`role`、`sub`、`blocks`（嵌套正文） |
| `table` | 表格 | `rows`（label/value），或 `headers` + `rows`（整行数组） |
| `ach` | 成果图组 | `head`、`figures`（file/alt/caption/link） |
| `spacer` | 空白行 | `h`（像素高度） |

**文字规则**（PowerShell 语法）：

- 短文本用单引号：`text = '内容'`；文字里出现英文单引号 `'` 时写成两个 `''`；
- 长段落建议用 here-string（多行原文直接粘贴）：

```powershell
@{ type = 'p'; html = @'
这里是任意多行的段落文字，
中文引号“”、括号（）都不需要转义。
'@ }
```

注意：结束标记 `'@` 必须**顶行**（行首不能有空格）。

- 列表条目之间**不加逗号**（换行即可），但 `education.ps1` 那种“数组套数组”的行之间**必须加逗号**（照抄现有写法最稳妥）；
- 加粗用 `<strong>文字</strong>`；DOI/网盘链接的写法直接照抄现有条目；
- `item` 块里日期、单位、项目名之间用全角空格 `　` 分隔（照抄现有条目）；
- **论文页自动加粗本人姓名**：`publications.ps1` 顶部的 `bold_name = $true` 控制列表条目里 `Yang, M.` / `Yang, M.-L.` / `Minglei Yang` / `杨明雷` 自动加粗，新加的论文无需手写 `<strong>`。

## 常见任务

| 任务 | 操作 |
|------|------|
| 添加一篇论文 | `publications.ps1` → 找到对应小节 → 复制一条现有条目 → 改文字（DOI 链接格式照抄） |
| 添加一个项目 | `projects.ps1` → 复制一个完整的 `@{ type = 'item' ... }` 块 → 修改内容 |
| 改联系方式 | `contact.ps1` → 改 `rows` 里的行 |
| 换照片 | 替换 `images\portrait.jpg`（保持竖版、宽 ≥320px） |
| 改菜单/页脚/邮箱 | `site.ps1` |
| 改颜色/字体 | `pagestyle.css`（菜单蓝 `#000099`、悬停橙 `#FF6600`、分隔线 `#03188D`） |

> 每次内容有实质更新，建议同步修改 `site.ps1` 里的 `footer` 日期。

## 部署到 GitHub Pages

首次部署（本目录即仓库根目录）：

```bash
git init
git add .
git commit -m "初始化个人主页"
git branch -M main
git remote add origin https://github.com/yangminglei122/yangminglei122.github.io.git
git push -u origin main
```

推送后在 GitHub 仓库 **Settings → Pages** 确认：Source = **Deploy from a branch**，Branch = **main**，目录 = **/ (root)**。

访问：<https://yangminglei122.github.io>

## 注意

- `data\`、`build.ps1`、`build.cmd` 已通过 `.gitignore` 排除，**不会上传到 GitHub**——请自行备份这几个文件（例如另建一个私有仓库）；
- 若编辑数据文件后构建出现中文乱码，运行 `E:\Research\LLM\Homepage\add_bom.ps1` 修复编码，再重新构建；
- 邮箱按学术主页惯例做了防爬虫处理：`yangminglei122(at)163.com`；
- 联系页按个人要求：出生信息仅显示到年份，不展示手机号（原始简历中有，如需恢复在 `contact.ps1` 加回对应行即可）。
