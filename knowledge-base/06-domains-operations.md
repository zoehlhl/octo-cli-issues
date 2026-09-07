# 06 功能域与操作

> 来源: `octo-cli --help`; 各域 --help; octo-cli skills

## 域总览

| 域 | 操作数 | 备注 |
|----|--------|------|
| `auth` | 4 | login/logout/list/status；凭证管理 |
| `bot` | 6 | heartbeat/register/set-commands/space-members/typing/user-info |
| `message` | 5+6搜索 | send/edit/sync/read-receipt/search |
| `group` | 10 | create/get/list/md-get/md-update/member-add/member-remove/members/update；User Bot 完整操作 |
| `thread` | 8 | create/get/join/leave/list/md-get/md-update/members；**仅 User Bot** |
| `event` | 2 | list/ack；事件轮询 |
| `file` | 4 | upload/download/credentials/presigned |
| `docs` | 15+ | 文档/表格/白板 CRUD、成员、分享、版本、附件 |
| `html` | 12+ | HTML 文档发布、草稿、分享、资产、评论、Agent 元素替换 |
| `marketplace` | 8 | skill/mcp 搜索、安装、发布、更新 |
| `schema` | — | 离线 API 探索，不需要网络 |
| `skills` | — | 内嵌 skill 文档：octo-docs/octo-files/octo-html/octo-marketplace/octo-messaging/octo-shared |
| `config` | 1 | show：显示已解析配置（token 掩码） |

## 关键域：messaging

```bash
# 发消息（payload.type=1 为文本）
octo-cli message send \
  --channel-id <channel_id> \
  --channel-type 2 \          # 1=DM, 2=群, 5=Thread
  --data '{"payload":{"type":1,"content":"@主考 消息内容"}}'

# 查群列表
octo-cli group list --page-all

# 查群成员
octo-cli group members <group_no>

# 读取 GROUP.md
octo-cli group md-get <group_no>
```

## 关键域：event（事件轮询）

```bash
# 拉取待处理事件（游标式）
octo-cli event list [--limit 20]

# 确认事件（消费后必须 ack，否则下次仍会返回）
octo-cli event ack <event_id>
```

事件类型包括：消息事件、群组事件、@事件等，Agent 通过轮询 event list 感知群里的消息。

## 暂不可用的域

- `matter`（事项/任务）：**temporarily withheld**，后端 API 仍在稳定中，当前版本不可用

来源: `octo-cli --help`; `octo-cli skills octo-shared` → "Domain skills"; `octo-cli skills octo-messaging`
