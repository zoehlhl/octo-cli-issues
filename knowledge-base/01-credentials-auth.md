# 01 凭证与权限

> 来源: octo-cli skills octo-shared

## Token 类型

| Token 前缀 | 类型 | 能干什么 |
|-----------|------|---------|
| `app_*` | App Bot | 只能发 DM（channel_type=1），不能操作群组/Thread；不能跨频道搜索 |
| `bf_*` | User Bot（Bot-Friend） | 可发消息到 DM+群+Thread，可搜索，完整群组操作 |
| `uk_*` | User API Key | 真人身份，搜索路由到 `/v1/user/*`，OBO 操作 |

## 掩码规则

- `octo-cli config show` 显示 token 已掩码（masked），不明文展示
- `octo-cli auth list` 只列 profile 名，不显示 token
- token **永远不能**出现在群聊消息、git commit、日志里
- 存储位置：octo-cli 内置 keystore（`~/.config/octo-cli/` 或系统 keychain）

## 配置与环境变量

| 变量 | 含义 | 必填 |
|------|------|------|
| `OCTO_BOT_TOKEN` | Bot token，优先级低于 profile | 二选一 |
| `OCTO_API_BASE_URL` | API 基础地址 | 是 |
| `OCTO_BOT_ID` | 指定 bot credential（与 --profile 二选一） | 否 |

```bash
# 确认当前凭证
octo-cli config show       # 已掩码，安全
octo-cli auth status       # 显示当前 bot identity
octo-cli auth list         # 列出所有 profile
```

## 不同 Bot 类型权限矩阵

| 域 | App Bot | User Bot (bf_*) |
|----|---------|----------------|
| message (DM) | ✅ | ✅ |
| message (群/Thread) | ❌ FORBIDDEN | ✅ |
| group 读 | ✅ | ✅ |
| group 写（创建/改名/加人） | ❌ | ✅ |
| thread | ❌ blocked | ✅ |
| message search | ❌ 本地拒绝 | ✅ (bf_*) |

来源: `octo-cli skills octo-shared` → "Auth" 节; `octo-cli skills octo-messaging` → 权限矩阵表
