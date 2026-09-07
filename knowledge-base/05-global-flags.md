# 05 通用参数

> 来源: octo-cli skills octo-shared; `octo-cli --help`

## 所有命令通用 flags

| Flag | 说明 | 示例 |
|------|------|------|
| `--format` | 输出格式: json(默认)/table/csv/ndjson | `--format table` |
| `--jq` | jq 表达式过滤输出 | `--jq '.data[].id'` |
| `--dry-run` | 打印请求不执行 | `--dry-run` |
| `--no-retry` | 禁用自动重试 | `--no-retry` |
| `--timeout` | 请求超时 | `--timeout 30s` |
| `--verbose` | 输出请求/响应 trace 到 stderr | `--verbose` |
| `--profile` | 指定 bot profile 名 | `--profile mybot` |
| `--bot-id` | 通过 robot_id 选 credential | `--bot-id aibi_xxx` |
| `--space` | Space ID（按需传） | `--space sp_123` |

## 分页：`--page-all`

```bash
# 自动拉取所有页（cursor-based 列表）
octo-cli group list --page-all --page-limit 20
```

- 适用于返回 `_pagination` cursor 的列表操作
- 合并输出为扁平 `data` 数组，丢弃 `_pagination`
- **不适用** docs list（page-based，用 `--page`/`--pageSize`）

## `--data` 与 promoted flags

```bash
# 简单字段用 flags
octo-cli thread create group-abc --name "design review"

# 复杂对象用 --data
octo-cli message send --data '{"channel_id":"chat-1","channel_type":1,"payload":{"type":1,"content":"hi"}}'

# 从文件读
octo-cli message send --data @body.json

# 从 stdin
echo '{"payload":...}' | octo-cli message send --data @-
```

**Flags 优先级高于 --data 中同名字段**

## 发现 API

```bash
octo-cli schema --list           # 所有域 + operation IDs
octo-cli schema --list message   # 某域的操作列表
octo-cli schema message.send     # 某操作完整 schema

# 低级 API passthrough
octo-cli api GET  /api/v1/messages --params '{"chat_id":"chat-1"}'
octo-cli api POST /api/v1/messages --data @body.json
```

来源: `octo-cli skills octo-shared` → "Input patterns"; `octo-cli --help` 全局 flags
