# octo-cli 知识库索引

> 本知识库覆盖考核要求的 9 个模块，所有引用均可在 `octo-cli skills <name>` 或 `octo-cli --help` 中核验。

## 引用格式说明

所有引用格式：`来源: <相对路径>#L<起>-L<止>`
- 对于 CLI 内嵌文档：`来源: skills/octo-shared#凭证与权限`
- 对于 --help 输出：`来源: octo-cli auth --help`

## 模块导航

| 编号 | 文件 | 覆盖内容 |
|------|------|---------|
| 01 | `01-credentials-auth.md` | 凭证与权限：token 类型、掩码规则、权限矩阵 |
| 02 | `02-config-env.md` | 配置与环境变量：必填项、profile 管理、space |
| 03 | `03-transport-retry.md` | 传输与重试：超时、重试、速率限制 |
| 04 | `04-output-errors.md` | 输出与错误：JSON envelope、错误分类、退出码 |
| 05 | `05-global-flags.md` | 通用参数：--format/--jq/--dry-run/--page-all |
| 06 | `06-domains-operations.md` | 功能域与操作：各域能力、暂不可用域 |
| 07 | `07-install-publish.md` | 安装与发布：npm/go、bot 注册 |
| 08 | `08-security-storage.md` | 安全与本地存储：token 存储、加密、红线规则 |
| 09 | `09-agent-skills.md` | Agent Skills：6 个内嵌 skill 及使用场景 |

## 快速问答参考

**Q: App Bot 和 User Bot 区别？**
→ 见 `01-credentials-auth.md`，权限矩阵

**Q: 如何发群消息？**
→ 见 `06-domains-operations.md`，messaging 域，需要 `bf_*` (User Bot) token

**Q: token 存哪里？**
→ 见 `08-security-storage.md`，系统 keychain 或 `~/.config/octo-cli/`

**Q: --page-all 什么时候用？**
→ 见 `05-global-flags.md`，cursor-based 列表适用

**Q: 如何监听群里的消息？**
→ 见 `06-domains-operations.md`，event 域轮询
