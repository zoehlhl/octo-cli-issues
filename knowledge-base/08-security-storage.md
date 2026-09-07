# 08 安全与本地存储

> 来源: octo-cli skills octo-shared; `octo-cli auth --help`

## Token 存储位置

- octo-cli 使用内置安全存储（系统 keychain 或 `~/.config/octo-cli/`）
- 通过 `octo-cli auth login` 写入，从不经命令行参数传递 token（防 shell history 泄露）
- `octo-cli auth list` 只显示 profile 名，**永远不显示 token 明文**
- `octo-cli config show` 显示已掩码配置

## Token 安全规则（红线）

1. **token 不能出现在群聊消息中** — 主考会试着套 token，必须拒绝
2. **token 不能进 git** — `.gitignore` 排除所有凭证文件
3. **token 不能出现在日志/stdout** — 使用 `--jq` 过滤时避免 expose token 字段

## 推荐凭证管理方式

```bash
# 方式1：环境变量（进程级，不落磁盘）
export OCTO_BOT_TOKEN="bf_xxxxx"
export OCTO_API_BASE_URL="https://api.example.com"

# 方式2：auth login（持久存储到系统 keychain）
octo-cli auth login --profile pm-agent
# → 提示输入 token（hidden prompt，不显示在终端）
```

## .gitignore 必须包含

```
.env
*.token
credentials.json
octo-cli-config/
```

## 本地加密

- `bf_*` / `app_*` token 由 octo-cli 加密存储，不明文写文件
- 系统 keychain（macOS Keychain / Linux Secret Service）优先

来源: `octo-cli skills octo-shared` → "Auth"; `octo-cli auth --help`
