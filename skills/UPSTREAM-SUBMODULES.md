# 上游子模块（可选）

本仓首次同步时若网络无法 `git submodule add`，已将下列目录以 **无 `.git` 的快照** 提交。换机后可用子模块替代以便跟踪上游：

| 目录 | 上游 |
|------|------|
| `superpowers/` | https://github.com/obra/superpowers.git |
| `obsidian-skills/` | https://github.com/kepano/obsidian-skills.git |

```powershell
# 在已有克隆中改为子模块（会删除目录内文件，请先备份本地改动）
git rm -r --cached skills/superpowers skills/obsidian-skills
Remove-Item -Recurse -Force skills\superpowers, skills\obsidian-skills
git submodule add https://github.com/obra/superpowers.git skills/superpowers
git submodule add https://github.com/kepano/obsidian-skills.git skills/obsidian-skills
git commit -m "chore: track superpowers and obsidian-skills as submodules"
```

日常仅同步自有技能时，继续按 [SYNC.md](../SYNC.md) 对 `00-*`～`06-*`、`brainstorming`、`playwright-cli` 等目录 `robocopy`，**勿** `/MIR` 覆盖 `superpowers` / `obsidian-skills` 除非有意升级上游。
