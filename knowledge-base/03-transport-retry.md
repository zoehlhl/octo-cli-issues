# 03 传输与重试

> 来源: octo-cli skills octo-shared

## 超时

```bash
octo-cli message send --timeout 30s --data '...'
octo-cli message send --timeout 2m  --data '...'   # 格式: 数字 + s/m
```

- 默认超时：由服务端控制，无显式默认值文档
- 建议长轮询操作设置 `--timeout 60s`

## 重试

```bash
# 禁用重试（默认会在瞬时失败时自动重试）
octo-cli event list --no-retry
```

- 瞬时失败（网络抖动、5xx）自动退避重试
- 使用 `--no-retry` 关闭自动重试

## 速率限制（Rate Limit）

| 域 | 限制 | 来源 |
|----|------|------|
| GitHub Search | 30 次/分钟 | 考核要求 |
| GitHub REST | 5000 次/小时 | 考核要求 |
| Octo API | 撞到限流立即停止 | 考核要求红线 |

- 撞到 `RATE_LIMITED` 错误类型 → 停止操作，等待后重试
- 退避策略：指数退避（error.type = `rate_limited`，exit_code = 1）

来源: `octo-cli skills octo-shared` → "Flags & Retry"; 考核文件第六节红线
