# Huan Xu 学术网站维护指南

这套网站可以通过修改 Markdown、HTML 和 YAML 文件长期维护；日常更新不需要重新建站，也不要直接修改自动生成的 `_site/` 目录。

- 正式网站：<https://xuhuanhydro.github.io/>
- 源代码仓库：<https://github.com/XuHuanHydro/xuhuanhydro.github.io>
- 默认分支：`main`
- GitHub Pages 来源：`main / (root)`
- 技术框架：Academic Pages `v0.8.4`、Jekyll、GitHub Pages

## 1. 先理解网站的文件结构

| 要维护的内容 | 修改位置 | 当前状态 |
|---|---|---|
| 首页正文 | `_pages/about.md` | 公开 |
| 顶部导航 | `_data/navigation.yml` | 公开入口只有 Home、Publications、Writing |
| 姓名、职位、单位、头像、外部账号 | `_config.yml` | 公开 |
| 出版物 | `_pages/publications.html` | 公开，依据 Google Scholar |
| Writing 页面 | `_pages/writing.md` | 公开 |
| 写作文章 | `_posts/` | 暂无正式文章 |
| 写作草稿模板 | `_drafts/writing-template.md` | 不公开 |
| Research 页面 | `_pages/research.md` | `published: false`，隐藏 |
| Software 页面 | `_pages/software.md` | `published: false`，隐藏 |
| CV 页面 | `_pages/cv.md` | `published: false`，隐藏 |
| 图片 | `images/` | 公开静态文件 |
| PDF、Word、Excel、压缩包等下载文件 | `files/` | 公开静态文件 |
| 网站样式 | `_sass/` 和 `assets/` | 非必要不要修改 |
| 本地生成的网站 | `_site/` | 自动生成，禁止手工维护 |

核心原则：

1. 只修改源文件，不修改 `_site/`。
2. 所有放入 `images/` 和 `files/` 的内容都会公开，不要上传隐私数据、密钥、内部审稿材料或未授权文件。
3. 文件名尽量使用小写英文字母、数字和连字符，例如 `catchment-map-2026.png`。
4. GitHub Pages 路径区分大小写。文件名和链接必须完全一致。
5. 不确定的个人信息或论文信息宁可留空，不要猜测。

## 2. 两种维护方式

### 2.1 方式 A：直接在 GitHub 网页修改

适合修改少量文字、替换一张图片或上传一个 PDF。

1. 打开仓库：<https://github.com/XuHuanHydro/xuhuanhydro.github.io>
2. 进入目标文件或目录。
3. 修改文字时，打开文件后点击铅笔图标 **Edit this file**。
4. 上传文件时，进入目标目录，点击 **Add file → Upload files**。
5. 在 **Commit changes** 中填写简短说明，例如：

   ```text
   Update homepage research interests
   ```

6. 提交到 `main`。
7. 打开仓库的 **Actions** 页面，等待 `pages build and deployment` 显示绿色成功标记。
8. 打开正式网站检查结果。GitHub Pages 更新通常不是瞬时可见，先等待部署成功，再刷新页面。

网页方式的限制：

- 不适合一次修改很多文件。
- 无法在提交前完整执行本地 Jekyll 构建。
- YAML 或 HTML 修改错误可能导致部署失败。

涉及导航、配置或多页面更新时，优先使用本地方式。

### 2.2 方式 B：在本地 PowerShell 修改

网站本地目录为：

```text
C:\personalWeb
```

每次开始前：

```powershell
Set-Location C:\personalWeb
git status
git pull --ff-only origin main
```

`git status` 如果显示未提交修改，先确认这些修改是什么，不要直接覆盖。

修改完成后：

```powershell
git diff
git diff --check
git status
```

确认无误后提交：

```powershell
git add 具体修改过的文件
git commit -m "简短的英文修改说明"
git push origin main
```

例如：

```powershell
git add _pages/about.md images/profile-photo.jpg
git commit -m "Update profile and portrait"
git push origin main
```

不建议使用 `git add .`，因为它可能把临时文件或不应公开的材料一起加入提交。

## 3. 修改首页

首页文件：

```text
_pages/about.md
```

当前结构：

```markdown
I am a Postdoctoral Research Fellow at ...

**Research interests:** keyword 1, keyword 2, keyword 3.

## Explore

- [Publications](/publications/)
- [Writing](/writing/)
```

维护规则：

- 研究兴趣保持关键词级别，不在首页展开研究计划或方法细节。
- 内部页面链接使用以 `/` 开头的路径。
- 外部链接写完整的 `https://...` 地址。
- 首页不放未经核实的论文数量、引用次数或项目状态。

## 4. 修改侧栏个人信息

个人资料位于：

```text
_config.yml
```

主要字段：

```yaml
author:
  avatar:
  name: "Huan Xu"
  bio: "..."
  location: "Ann Arbor, Michigan"
  employer: "..."
  email:
  googlescholar: "https://..."
  orcid:
  github: "XuHuanHydro"
  linkedin:
```

注意：

- YAML 使用空格缩进，不要使用 Tab。
- 含冒号、特殊符号或较长 URL 的值用双引号包住。
- 没有内容时保持字段为空，不要写 `N/A`。
- 修改 `_config.yml` 后必须重新构建；本地预览服务也需要重启。

## 5. 上传和使用图片

### 5.1 图片放在哪里

统一放入：

```text
images/
```

建议按用途建立子目录：

```text
images/
├── profile/
├── research/
├── writing/
└── publications/
```

推荐格式：

- 照片：`.jpg` 或 `.webp`
- 截图和包含文字的图：`.png`
- 简单矢量图或图标：`.svg`

上传前应：

- 裁掉无关区域。
- 压缩文件，避免直接上传相机原始大图。
- 检查图片是否包含个人信息、未公开数据或受限底图。
- 为图片准备有意义的替代文字。

### 5.2 设置个人头像

例如把头像保存为：

```text
images/profile/huan-xu.jpg
```

然后修改 `_config.yml`：

```yaml
author:
  avatar: "profile/huan-xu.jpg"
```

头像最好使用接近正方形的裁剪。若暂时不显示头像，保持：

```yaml
avatar:
```

不要填写不存在的文件名，否则会出现破损图片。

### 5.3 在 Markdown 页面或文章中插图

```markdown
![Map of study catchments](/images/research/study-catchments.png)
```

其中：

- 方括号内容是替代文字，应说明图中是什么。
- `/images/...` 是从网站根目录开始的公开路径。
- 文件名大小写必须与磁盘完全一致。

带图注时可以使用 HTML：

```html
<figure>
  <img src="/images/research/study-catchments.png"
       alt="Map of study catchments">
  <figcaption>Study catchments used in the analysis.</figcaption>
</figure>
```

不要仅写：

```markdown
![](/images/figure.png)
```

因为这会缺少无障碍替代文字，也不利于理解图片内容。

### 5.4 替换已有图片

有两种方式：

1. 保持原文件名并覆盖文件：所有旧链接自动指向新图。
2. 使用新文件名并同步修改所有引用：更利于保留版本和避免浏览器缓存。

涉及正式论文图或重要头像时，推荐使用新文件名，例如：

```text
catchment-map-v2.png
```

上传后用以下命令检查旧文件名是否仍被引用：

```powershell
rg -n "旧文件名.png" .
```

确认没有引用后再决定是否删除旧文件。

## 6. 添加表格

### 6.1 小型表格：直接使用 Markdown

```markdown
| Dataset | Region | Resolution |
|---|---|---|
| Dataset A | United States | Daily |
| Dataset B | Global | Monthly |
```

适合：

- 列数较少。
- 单元格内容较短。
- 不需要合并单元格。

手机屏幕较窄，因此网页主文中的表格应尽量保持简单。详细数值表更适合作为下载文件。

### 6.2 复杂表格：上传 CSV 或 Excel

建议目录：

```text
files/tables/
```

文件示例：

```text
files/tables/publication-metadata.csv
files/tables/catchment-summary.xlsx
```

在页面中添加下载链接：

```markdown
[Download the catchment summary table](/files/tables/catchment-summary.xlsx)
```

建议同时提供 CSV：

```markdown
- [CSV version](/files/tables/catchment-summary.csv)
- [Excel version](/files/tables/catchment-summary.xlsx)
```

原因是 CSV 更容易长期读取和版本比较，Excel 更方便普通用户查看。

不要把 Excel 表格直接复制成大量 HTML；这通常会导致样式复杂、移动端溢出且难以维护。

### 6.3 HTML 表格

只有在确实需要标题、链接或特殊结构时使用：

```html
<table>
  <thead>
    <tr>
      <th>Project</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Project A</td>
      <td>Ongoing</td>
    </tr>
  </tbody>
</table>
```

## 7. 上传 PDF、Word、PPT、数据和压缩包

统一放入：

```text
files/
```

建议分类：

```text
files/
├── cv/
├── papers/
├── presentations/
├── tables/
└── supplementary/
```

### 7.1 PDF

例如：

```text
files/cv/huan-xu-cv.pdf
```

Markdown 链接：

```markdown
[Download my CV (PDF)](/files/cv/huan-xu-cv.pdf)
```

如需在新标签页打开：

```html
<a href="/files/cv/huan-xu-cv.pdf" target="_blank" rel="noopener">
  Download my CV (PDF)
</a>
```

### 7.2 Word、PowerPoint、Excel 和 ZIP

这些文件通常作为下载内容，而不是直接嵌入网页：

```markdown
- [Download the presentation](/files/presentations/talk-2026.pptx)
- [Download the supplementary archive](/files/supplementary/project-files.zip)
```

上传前必须确认：

- 文档属性中没有不应公开的作者批注或修订记录。
- Excel 没有隐藏的敏感工作表。
- ZIP 中没有密钥、缓存、原始受限数据或本地绝对路径。
- PDF 没有未删除的批注、个人信息或内部版本标识。

### 7.3 不建议放入仓库的内容

- 大型原始数据。
- 模型检查点和训练缓存。
- 含受试者或个人身份信息的数据。
- 许可证限制公开的数据。
- API 密钥、访问令牌、密码或 SSH 私钥。

此类内容应存入正式数据仓库或受控存储，只在网站提供说明和授权链接。

## 8. 维护出版物

出版物页面：

```text
_pages/publications.html
```

当前权威来源：

<https://scholar.google.com.hk/citations?hl=zh-CN&user=qPjAasMAAAAJ&view_op=list_works>

维护原则：

1. 只添加 Google Scholar 个人主页中已确认属于本人的成果。
2. 核对标题、作者顺序、期刊或会议、卷号、文章号和年份。
3. 不复制引用次数，因为它会动态变化。
4. 不根据搜索结果猜 DOI。
5. 期刊论文和会议摘要都可以保留，但页面应如实标明来源类型。
6. 每次更新页面顶部的 `Last updated` 日期。

添加一项时，在对应年份的 `<ol>` 中复制：

```html
<li>
  <a href="Google Scholar 记录链接">Paper title</a><br>
  A Author, <strong>H Xu</strong>, B Author.
  <em>Journal Name</em> 12, 123456.
</li>
```

新年份应放在旧年份之前：

```html
<h2>2027</h2>
<ol reversed>
  <!-- 2027 publications -->
</ol>

<h2>2026</h2>
```

如果要删除一条记录，只删除对应的完整 `<li>...</li>`，不要破坏外层 `<ol>`。

更新后检查条目数量：

```powershell
(Select-String -Path "_pages\publications.html" -Pattern "<li>" -AllMatches).Matches.Count
```

## 9. 发布 Writing 文章

草稿模板：

```text
_drafts/writing-template.md
```

正式文章目录：

```text
_posts/
```

### 9.1 创建文章

复制模板，并按日期命名：

```text
_posts/2026-08-15-catchment-classification-notes.md
```

文件名必须以 `YYYY-MM-DD-` 开头。

典型 front matter：

```yaml
---
title: "Article title"
date: 2026-08-15
categories:
  - Research Notes
tags:
  - hydrology
  - catchment classification
excerpt: "One-sentence summary."
published: false
---
```

写作阶段保留：

```yaml
published: false
```

此时文章不会出现在正式网站。

完成内容、链接和图片检查后，删除该行或改为：

```yaml
published: true
```

然后本地构建、提交和部署。

### 9.2 文章中的图片和附件

推荐：

```text
images/writing/2026-catchment-classification/figure-1.png
files/writing/2026-catchment-classification/table-s1.csv
```

文章中引用：

```markdown
![Classification workflow](/images/writing/2026-catchment-classification/figure-1.png)

[Download Table S1](/files/writing/2026-catchment-classification/table-s1.csv)
```

## 10. 显示或隐藏 Research、Software、CV

当前三个页面均包含：

```yaml
published: false
```

因此它们不会被生成。

### 10.1 重新显示某个页面

以 Research 为例：

1. 编辑 `_pages/research.md`。
2. 完成并核实正文。
3. 删除：

   ```yaml
   published: false
   ```

4. 编辑 `_data/navigation.yml`，加入：

   ```yaml
   - title: "Research"
     url: /research/
   ```

5. 本地构建并确认 `/research/` 正常显示。
6. 提交并推送。

Software 和 CV 的处理相同：

```yaml
- title: "Software"
  url: /software/
- title: "CV"
  url: /cv/
```

### 10.2 再次隐藏页面

必须同时完成两件事：

1. 从 `_data/navigation.yml` 删除对应入口。
2. 在页面 front matter 中加入：

   ```yaml
   published: false
   ```

只删除导航并不等于隐藏页面；知道地址的人仍可能访问页面。

## 11. 修改顶部导航

文件：

```text
_data/navigation.yml
```

当前内容：

```yaml
main:
  - title: "Home"
    url: /
  - title: "Publications"
    url: /publications/
  - title: "Writing"
    url: /writing/
```

规则：

- `main:` 下每个入口使用两个空格缩进。
- 导航标题应简短。
- 内部地址以 `/` 开始并以 `/` 结束。
- 只有内容已经准备好的页面才进入导航。
- 修改顺序即可改变顶部菜单顺序。

## 12. Markdown 最常用语法

```markdown
# 一级标题
## 二级标题
### 三级标题

**粗体**
*斜体*

- 无序列表
- 第二项

1. 有序列表
2. 第二项

[链接文字](https://example.com)

![图片说明](/images/example.png)

`行内代码`
```

段落之间留一个空行。不要用连续空格手工对齐内容。

YAML front matter 必须位于文件最上方，并由两行 `---` 包住：

```yaml
---
title: "Page title"
permalink: /page-name/
author_profile: true
---
```

## 13. 本地构建和预览

### 13.1 常规命令

在 PowerShell 中：

```powershell
Set-Location C:\personalWeb
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll build --strict_front_matter
bundle exec jekyll doctor
bundle exec jekyll serve --livereload --host localhost
```

然后打开：

<http://localhost:4000/>

按 `Ctrl+C` 停止本地服务。

如果只修改普通 Markdown，Jekyll 通常会自动更新；修改 `_config.yml` 后应停止并重新启动服务。

### 13.2 本机找不到 Ruby 或 bundle 时

本机 Ruby 安装位置为：

```text
C:\Ruby33-x64
```

先执行：

```powershell
$env:Path = "C:\Ruby33-x64\bin;$env:Path"
ruby --version
bundle --version
```

如果 `bundle exec jekyll` 仍因 Windows 启动脚本失败，可使用本项目已验证的构建命令：

```powershell
& "C:\Ruby33-x64\bin\ruby.exe" `
  -rbundler/setup `
  "vendor\bundle\ruby\3.3.0\bin\jekyll" `
  build --strict_front_matter
```

诊断命令：

```powershell
& "C:\Ruby33-x64\bin\ruby.exe" `
  -rbundler/setup `
  "vendor\bundle\ruby\3.3.0\bin\jekyll" `
  doctor
```

不要把本地生成的 `_site/` 提交到仓库。

## 14. 部署和线上验收

推送到 `main` 后，GitHub Pages 会自动部署。

### 14.1 检查部署

1. 打开 <https://github.com/XuHuanHydro/xuhuanhydro.github.io/actions>。
2. 找到最新的 `pages build and deployment`。
3. 确认状态为 **Success**。
4. 打开 <https://xuhuanhydro.github.io/>。

当前应重点检查：

- 首页：<https://xuhuanhydro.github.io/>
- 出版物：<https://xuhuanhydro.github.io/publications/>
- Writing：<https://xuhuanhydro.github.io/writing/>

当前隐藏页面应保持不可访问：

- `/research/`
- `/software/`
- `/cv/`

### 14.2 每次部署后的最低检查

- 顶部导航没有多余入口。
- 页面标题和正文正确。
- 图片全部显示。
- PDF 或下载链接可以打开。
- 外部链接指向预期网站。
- 手机宽度下没有明显横向滚动。
- 没有模板示例内容或占位符。

## 15. 常见故障

### 15.1 Actions 构建失败

先打开失败任务，查找第一条实际错误。常见原因：

- YAML 缩进错误。
- front matter 缺少结束的 `---`。
- HTML 标签没有闭合。
- Liquid 语法中的 `{% %}` 或 `{{ }}` 不完整。
- 文件编码或特殊字符错误。
- 配置项拼写错误。

本地复现：

```powershell
bundle exec jekyll build --strict_front_matter
bundle exec jekyll doctor
```

修正后重新提交，不要通过强制推送覆盖历史。

### 15.2 图片不显示

逐项检查：

1. 文件是否已提交并推送。
2. 链接是否以 `/images/` 开头。
3. 文件名大小写是否一致。
4. 扩展名是否一致，例如 `.jpg` 与 `.jpeg`。
5. `_config.yml` 中头像是否只填写 `images/` 下的相对文件名。

### 15.3 文件下载出现 404

检查：

- 文件是否位于 `files/`。
- Markdown 链接是否以 `/files/` 开头。
- 文件名是否包含错误的空格、大小写或括号。
- 文件是否被 `.gitignore` 忽略。

### 15.4 页面仍显示旧内容

先确认最新 Actions 已成功，再：

- 强制刷新浏览器。
- 用无痕窗口检查。
- 等待短时间后再访问。
- 确认推送的是 `main`。

### 15.5 本地有冲突

不要删除 `.git`，也不要执行 `git reset --hard`。

先查看：

```powershell
git status
git diff
```

如果无法判断冲突内容，停止操作并保留现场，再请求协助。

## 16. 安全与公开边界

永远不要提交：

- 密码、API Token、GitHub Personal Access Token。
- `.env` 文件。
- SSH 私钥。
- 受限数据或未脱敏数据。
- 含评审意见、修订记录或私人批注的文档。
- 未获得公开许可的图片、论文 PDF 或第三方材料。

提交前可以执行定向检查：

```powershell
rg -n -i "github_pat_|ghp_|BEGIN.*PRIVATE KEY|AKIA|xox[baprs]-" `
  --glob "!vendor/**" `
  --glob "!_site/**" `
  --glob "!.git/**" .
```

如果密钥曾经被提交，之后再删除文件并不能使密钥恢复安全；应立即撤销或轮换密钥，并进一步清理 Git 历史。

## 17. 回退错误更新

先查看提交历史：

```powershell
git log --oneline -10
```

如果某个已推送提交需要撤销，使用可审计的反向提交：

```powershell
git revert 提交哈希
git push origin main
```

不要使用：

```text
git push --force
git reset --hard
```

除非已经明确理解影响并完成备份。

## 18. 推荐的日常维护流程

每次更新都按以下顺序：

1. `git status`
2. `git pull --ff-only origin main`
3. 只修改必要文件
4. 检查新增图片和文档是否适合公开
5. `git diff`
6. `git diff --check`
7. 本地 Jekyll 构建
8. 在本地浏览器检查页面
9. `git add` 指定文件
10. `git commit`
11. `git push origin main`
12. 等待 GitHub Actions 成功
13. 检查正式网站和新增下载链接

## 19. 更新请求应提供的信息

如果希望由 Codex 协助更新，最好一次提供：

- 要修改的页面。
- 最终文案。
- 图片或文档文件。
- 图片替代文字和图注。
- 下载文件的公开名称。
- 是否立即上线。
- 论文的 Scholar、DOI 或期刊正式链接。
- 页面是否应进入顶部导航。

材料不完整时，应先保留隐藏或草稿状态，不应自行补造公开信息。
