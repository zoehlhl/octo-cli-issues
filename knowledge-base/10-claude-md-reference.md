# 10 CLAUDE.md 关键摘录

> 来源: https://github.com/Mininglamp-OSS/octo-cli/blob/main/CLAUDE.md
> 纳入时间: 2026-09-04

## 域数量与操作数（L1-Q6）

> 来源: CLAUDE.md — "Command Structure" 节标题行

```
## Command Structure (12 active domains, 308 operations)
```

- **12 个活跃域**（active domains）
- **308 个操作**（operations）
- 最大域：`drive`（browse + space/member/folder/file/blob/upload/download/doc/share/invite/im-transfer，操作数最多）
- 其次：`docs`（15+ 操作）、`matter`（10 操作，withheld）

来源: CLAUDE.md#L48（"Command Structure (12 active domains, 308 operations)"）

---

## 不可用域（L1-Q7）

> 来源: CLAUDE.md — "Command Structure" 节注释块

**`matter` 域**（事项/任务）：temporarily withheld
> backend API not yet stable. The spec stays embedded — `octo-cli schema matter.*` still introspects it — but the command subtree and the `octo-matter` skill are hidden via the `x-octo-disabled` spec flag (`internal/registry/specs/matter.json`) and the skill's `disabled: true` frontmatter.

**`octo-summary` skill**（摘要）：withheld
> `octo-summary` (withheld — see CHANGELOG "Currently withheld" note)

注意：`summary` 是 skill 层面的 withheld，不一定是独立的命令域；matter 是命令域层面的 withheld。

来源: CLAUDE.md — Command Structure 注释块（matter 说明段）；skills 列表行

---

## matter 域重新启用方法（L1-Q8）

> 来源: CLAUDE.md — Command Structure 注释块

> Flip both off to re-enable:
> 1. `x-octo-disabled` spec flag in `internal/registry/specs/matter.json`
> 2. skill's `disabled: true` frontmatter（`octo-matter` skill）

两处都要关闭（flip off）才能重新启用 matter 域。

来源: CLAUDE.md — "matter is temporarily withheld" 注释段

---

## 凭证优先级（补充 L1-Q4）

> 来源: CLAUDE.md — Environment 表格

优先级：`OCTO_TOKEN` > `OCTO_BOT_TOKEN`（显式 `--bot-id`/`--profile` selector 在此之上）

```
OCTO_TOKEN        — 首选 env slot
OCTO_BOT_TOKEN    — OCTO_TOKEN 未设置时使用
```

来源: CLAUDE.md — Environment 表格（OCTO_TOKEN / OCTO_BOT_TOKEN 行）

---

## token 存储路径（补充 L1-Q5）

> 来源: CLAUDE.md — Identity Model

- 默认存储目录：`~/.octo-cli`（可通过 `OCTO_CONFIG_DIR` 覆盖）
- metadata：明文 `config.json`
- token：AES-256-GCM 加密的 `credentials.enc`

来源: CLAUDE.md — Identity Model（"Stored profiles live in `~/.octo-cli`"）
