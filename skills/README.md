# Cursor Skills · 磁盘主副本（`F:\C\git`）

本目录为 **F 盘全局主副本**；Cursor 运行时通常仍从 `%USERPROFILE%\.cursor\skills\` 加载，请用 [`docs/CURSOR-TOTAL-GUIDE.md`](../../安防开发总仓/安防-全局指挥/docs/CURSOR-TOTAL-GUIDE.md) 中的 `robocopy` 保持同步。

## 已收录（目录级）

| 目录 | 说明 |
|------|------|
| `00-workspace-context` … `06-conversation-notes` | blastum/AgentSkills |
| `superpowers` | obra/superpowers 整仓 |
| `brainstorming` | 联接至 superpowers 子技能 |
| `obsidian-skills` | kepano/obsidian-skills |
| `playwright-cli` | Playwright CLI skills |

## 路由与速记

见 [`安防-全局指挥/docs/agent/agent-skills-routing.md`](../../安防-全局指挥/docs/agent/agent-skills-routing.md) 与 [`F:\C\git\.cursor\rules\00-agent-commander.mdc`](../../.cursor/rules/00-agent-commander.mdc)。

## 更新 Superpowers

```powershell
git -C "F:\C\git\.cursor\skills\superpowers" pull
robocopy "F:\C\git\.cursor\skills" "$env:USERPROFILE\.cursor\skills" /E /XD .git
```
