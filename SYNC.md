# 技能树同步约定

## 旧电脑（有改动要备份）

```powershell
cd F:\C\git\安防开发总仓\安防-cursor-skills

# 从工作区主副本写入本仓（排除嵌套 .git，子模块目录勿用 /MIR 覆盖）
robocopy "F:\C\git\.cursor\skills" ".\skills" /MIR /XD .git superpowers obsidian-skills
Copy-Item -Force "F:\C\git\.cursor\rules\*.mdc" ".\rules\"

git status
git add -A
git commit -m "chore(skills): sync from F:\C\git\.cursor"
git push origin main
```

若只改了子模块上游版本：

```powershell
cd skills\superpowers
git fetch origin
git checkout main
git pull
cd ..\..
git add skills/superpowers
git commit -m "chore: bump superpowers submodule"
git push
```

## 新电脑（拉取并装到 Cursor）

```powershell
cd F:\C\git\安防开发总仓\安防-cursor-skills
git pull origin main
git submodule update --init --recursive

robocopy ".\skills" "$env:USERPROFILE\.cursor\skills" /MIR /XD .git
Copy-Item -Force ".\rules\*.mdc" "$env:USERPROFILE\.cursor\rules\"
robocopy ".\skills" "F:\C\git\.cursor\skills" /MIR /XD .git
Copy-Item -Force ".\rules\*.mdc" "F:\C\git\.cursor\rules\"
```

## 代理（推送失败时）

```powershell
$env:HTTP_PROXY="http://127.0.0.1:3067"
$env:HTTPS_PROXY="http://127.0.0.1:3067"
git push -u origin main
```

## 远程尚未创建

若 `git push` 报 repository not found，请在 GitHub 创建 **空仓库**（不要勾选 README）：

- 名称：`anfang-cursor-skills`
- 所有者：`van7171`
- URL：`https://github.com/van7171/anfang-cursor-skills.git`

然后在本目录重试 `git push -u origin main`。
