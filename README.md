# 安防 Cursor 技能树（云端备份）

将 **`F:\C\git\.cursor\skills`** 与全局 **`rules/*.mdc`** 纳入 Git，便于换机、重装 Cursor 后一键恢复 Agent 技能与总指挥规则。

| 项 | 值 |
|----|-----|
| GitHub | https://github.com/van7171/anfang-cursor-skills |
| 克隆 | `git clone https://github.com/van7171/anfang-cursor-skills.git` |
| 本地建议路径 | `F:\C\git\安防开发总仓\安防-cursor-skills\` |

## 目录结构

| 路径 | 说明 |
|------|------|
| `skills/` | 技能主副本（与 `F:\C\git\.cursor\skills` 对齐） |
| `rules/` | 全局 `alwaysApply` 规则指针（`00-agent-commander.mdc` 等） |
| `skills/superpowers/` | 上游 [obra/superpowers](https://github.com/obra/superpowers)（快照提交；可改子模块，见 `skills/UPSTREAM-SUBMODULES.md`） |
| `skills/obsidian-skills/` | 上游 [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)（同上） |

同步流程见 [SYNC.md](SYNC.md)。

## 新机器初始化

```powershell
# 1. 克隆本仓（或 pull 已有副本）
cd F:\C\git\安防开发总仓
git clone https://github.com/van7171/anfang-cursor-skills.git
cd 安防-cursor-skills
git submodule update --init --recursive

# 2. 技能 → Cursor 用户目录（默认扫描路径）
robocopy ".\skills" "$env:USERPROFILE\.cursor\skills" /MIR /XD .git

# 3. 规则 → 用户目录
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\rules" | Out-Null
Copy-Item -Force ".\rules\*.mdc" "$env:USERPROFILE\.cursor\rules\"

# 4.（可选）第二工作区根，与 F:\C\git 并行
if (Test-Path "D:\git\.cursor\skills") {
  robocopy ".\skills" "D:\git\.cursor\skills" /MIR /XD .git
  New-Item -ItemType Directory -Force -Path "D:\git\.cursor\rules" | Out-Null
  Copy-Item -Force ".\rules\*.mdc" "D:\git\.cursor\rules\"
}

# 5. 若仍以 F:\C\git 为工作区根，可把本仓 skills 镜像回主副本
robocopy ".\skills" "F:\C\git\.cursor\skills" /MIR /XD .git
Copy-Item -Force ".\rules\*.mdc" "F:\C\git\.cursor\rules\"
```

## 与四仓关系

本仓为 **第五仓**（仅技能与全局规则），与 [安防开发总仓](../README.md) 下 n8n / 专利 / 官网 / 全局指挥 **独立提交、独立推送**。工作区根 `F:\C\git\.cursor\skills` 仍为 Cursor 物理主路径；本仓为 **云端备份与换机源**。

## 注意

- 勿将 `mcp.json` 或含密钥文件放入本仓（已 `.gitignore`）。
- 更新 `superpowers` / `obsidian-skills` 子模块后执行 `git submodule update --remote` 再提交指针变更。
