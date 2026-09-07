# 09 Agent Skills（内嵌技能）

> 来源: `octo-cli skills --help`; `octo-cli skills <name>`

## 可用内嵌 Skill

```bash
# 列出方式（无 list 子命令，用 --help 看 hint）
octo-cli skills --help
# hint: available: octo-docs, octo-files, octo-html, octo-marketplace, octo-messaging, octo-shared
```

| Skill 名 | 版本 | 覆盖范围 |
|---------|------|---------|
| `octo-shared` | — | 认证、多服务配置、输出 envelope、通用 flags、错误处理、常见模式。**所有其他 skill 依赖此项，先加载** |
| `octo-messaging` | 0.4.1 | 消息发送/编辑/同步/已读回执、消息搜索、群组、Thread、事件轮询 |
| `octo-files` | 0.4.0 | 文件上传/下载/预签名、Bot 日常操作（register/heartbeat/typing/user-info） |
| `octo-docs` | 0.2.0 | 文档/表格/白板 CRUD，成员分享，评论，版本快照，附件 |
| `octo-html` | 0.1.0 | HTML 文档（octo-doc）发布、草稿、分享、资产、评论、Agent 元素替换。**与 octo-docs 是不同后端** |
| `octo-marketplace` | 0.3.0 | Skill 和 MCP 服务器的搜索、安装、发布、更新 |

## 加载方式

```bash
# 查看一个 skill 的完整内容
octo-cli skills octo-messaging

# 安装所有 skill 到目录（SKILL.md + references）
octo-cli skills --install ./my-skills-dir/
```

## 依赖关系

- **必须先加载 `octo-shared`**，其他 skill 都依赖它
- octo-docs 加载时建议按任务选 reference 文件（sheet.md / doc.md / board.md / common.md），不要全读

## 使用场景举例

| 需求 | 用哪个 Skill |
|------|------------|
| 在群里发消息、@某人 | `octo-messaging` |
| 监听群里的消息事件 | `octo-messaging`（event 轮询） |
| 上传文件发附件 | `octo-files` |
| 读写 Octo 文档/表格 | `octo-docs` |
| 发布 HTML 报告页面 | `octo-html` |
| 搜索/安装 marketplace skill | `octo-marketplace` |

来源: `octo-cli skills --help`; `octo-cli skills <name>`（各 skill SKILL.md frontmatter）
