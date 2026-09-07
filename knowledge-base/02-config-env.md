# 02 配置与环境变量

> 来源: octo-cli skills octo-shared

## 必填配置

| 配置项 | 环境变量 | CLI flag | 说明 |
|-------|---------|----------|------|
| API 地址 | `OCTO_API_BASE_URL` | — | 必填，所有请求的基础 URL |
| Bot Token | `OCTO_BOT_TOKEN` | `--profile` / `--bot-id` | 二选一，profile 优先 |

## Profile 管理

```bash
# 登录（token 从隐藏提示输入，不从命令行参数传——防止泄露到 shell history）
octo-cli auth login [--profile mybot]

# 查看当前激活的 bot
octo-cli auth status

# 列出所有 profile（不显示 token）
octo-cli auth list

# 删除 profile
octo-cli auth logout --profile mybot
```

## 多 Bot 切换

```bash
# 用 profile 名切换
octo-cli group list --profile bot-a
octo-cli message send --bot-id <robot_id> --data '...'
```

## 查看解析后配置

```bash
octo-cli config show   # 输出已掩码的配置，安全，适合调试
```

## Space（空间）

- 大多数命令不需要显式传 `--space`，服务端从 token 解析
- `bot` 和 `file` 域需要 `--space <space_id>` 时才传

来源: `octo-cli skills octo-shared` → "Config" 节; `octo-cli auth --help`
