# LonAC 项目 Git 操作指南

本文档用于记录 **LonAC** 项目的 Git 常用命令与操作流程。

- **仓库地址**: https://github.com/FeijoaLi/LonAC
- **主分支**: master

---

## 1. 环境配置 (首次使用)

如果你在一台新电脑上开始工作，请执行以下命令将项目下载到本地：

    git clone https://github.com/FeijoaLi/LonAC.git

---

## 2. 日常开发流程 (核心)

每次编写代码时，请严格遵守 **"拉取 -> 提交 -> 推送"** 的流程，以避免版本冲突。

### 第一步：同步最新代码
在开始工作前，**务必**先拉取远程仓库的最新修改：

    git pull origin master

### 第二步：提交本地修改
当你完成某个阶段的工作（如写完了一节内容或修改了代码）后：

    # 1. 将所有修改添加到暂存区
    git add .

    # 2. 提交到本地仓库 (请将引号内的文字替换为本次修改的简述)
    git commit -m "update: 添加了第三章的内容"

### 第三步：推送到 GitHub
将本地的提交同步到远程服务器：

    git push origin master

---

## 3. LaTeX 项目专属配置 (.gitignore)

由于 LaTeX 编译会生成大量中间文件（如 .aux, .log, .out），这些文件**不应该**被上传到 Git。
请确保项目根目录下存在 .gitignore 文件，并包含以下内容：

    # LaTeX 忽略规则
    *.aux
    *.bbl
    *.blg
    *.log
    *.out
    *.toc
    *.lot
    *.lof
    *.synctex.gz
    *.fls
    *.fdb_latexmk
    *.dvi
    *.pdf
    # 注意：如果你希望在仓库中保存 PDF，请删除上面一行 (*.pdf)

**如何清理已经误传的垃圾文件？**
如果在配置忽略规则前已经上传了这些文件，请执行：

    git rm -r --cached .
    git add .
    git commit -m "chore: 清理 LaTeX 中间文件"
    git push origin master

---

## 4. 常见报错解决

### 情况 A：提示 "fetch first" 或 "rejected"
**现象**：git push 时报错，提示远程包含你本地没有的工作。
**原因**：远程仓库比你本地新（可能是你在网页端改了文件，或在别的电脑推过代码）。
**解决**：

    # 1. 先拉取合并
    git pull origin master

    # 2. 如果有冲突，手动修改文件解决冲突后保存

    # 3. 再次提交并推送
    git add .
    git commit -m "merge: 解决合并冲突"
    git push origin master

### 情况 B：需要强制覆盖远程
**注意**：此操作极度危险，仅在**确定远程代码完全作废，必须以本地版本为准**时使用。

    git push -u origin master -f
