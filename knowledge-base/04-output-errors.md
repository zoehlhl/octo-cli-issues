# 04 输出与错误

> 来源: octo-cli skills octo-shared

## JSON Envelope 格式

所有成功响应：
```json
{ "ok": true, "data": { ... } }
```

所有失败响应：
```json
{
  "ok": false,
  "error": {
    "type": "auth_error",
    "code": "UNAUTHORIZED",
    "message": "token is invalid",
    "hint": "verify token with `octo-cli auth status`"
  }
}
```

## 错误类型与退出码

| error.type | exit_code | 常见 code |
|-----------|-----------|----------|
| `auth_error` | 3 | `UNAUTHORIZED`, `AUTH_UNAVAILABLE` |
| `validation` | 2 | `VALIDATION_ERROR`, `PAYLOAD_TOO_LARGE` |
| `config` | 2 | 缺少环境变量 |
| `permission` | 1 | `FORBIDDEN`, `SPACE_FORBIDDEN` |
| `rate_limited` | 1 | `RATE_LIMITED` |
| `network` | 1 | `NETWORK_ERROR`, `UPSTREAM_UNAVAILABLE` |
| `api_error` | 1 | `NOT_FOUND`, `INTERNAL_ERROR` |
| `internal` | 1 | CLI 内部 bug |

**Agent 判断顺序：先看 `error.code`（精确），再看 `error.type`（粗分类），最后看 exit_code**

## hint 字段

`error.hint` 是给 Agent 的下一步操作提示，字面意思执行。例：
- `MATTER_NOT_FOUND` → hint: "verify ID with `octo-cli matters list`"

## 输出格式控制

```bash
octo-cli group list --format table    # 表格（人类可读）
octo-cli group list --format json     # JSON（默认，机器友好）
octo-cli group list --format csv      # CSV
octo-cli group list --format ndjson   # 换行 JSON

# jq 过滤
octo-cli group list --jq '.data[].id'
```

## Dry Run（自检）

```bash
octo-cli message send --data '{"channel_id":"chat-1","channel_type":1,"payload":{"type":1,"content":"test"}}' --dry-run
# 只打印请求 URL 和 body，不实际发送
```

来源: `octo-cli skills octo-shared` → "Output & Errors"; "Input patterns" 节
