# octo-cli 需求池

本仓库是 [octo-cli](https://github.com/Mininglamp-OSS/octo-cli) 的产品需求池，用于收集 Bug 反馈和功能需求，由 **产品管家-HL** Agent 自动维护。

## 关于 octo-cli

octo-cli 是面向 AI Agent 的命令行客户端，提供 Octo 生态的消息收发、群管理、文件上传等能力，支持 App Bot 和 User Bot 两种凭证模式。

## Issue 类型

| Label | 含义 |
|-------|------|
| `bug` | Bug 反馈，描述复现步骤、预期行为与实际行为 |
| `enhancement` | 功能需求/新特性请求 |
| `wontfix` | 经评估决定不做的需求 |
| `prd-ready` | 已自动生成 PRD，等待评审 |
| `P1` | 高优先级需求 |
| `PRD撰写中` | PRD 正在撰写中 |

## 工作流

1. **收单**：用户在 Octo 群中反馈 Bug / 提出需求 → 产品管家自动创建 Issue 并分类打标签
2. **PRD 撰写**：`enhancement` 类型 Issue 自动生成 PRD（只写 What，不写 How），以评论形式附在 Issue 中
3. **定时巡检**：每 15 分钟自动扫描仓库变更（关单、wontfix、新 label），有变更时通知考试群
4. **闭环**：Issue 关闭 / 标记 wontfix → 自动通知相关人员

## 目录结构

- 知识库：覆盖 octo-cli 的 9 个产品模块（凭证、配置、传输、输出、通用参数、功能域、安装、安全、Agent Skills）
- PRD 模板：以用户视角描述需求和验收标准，不涉及技术实现

## 相关仓库

- **目标产品**：[Mininglamp-OSS/octo-cli](https://github.com/Mininglamp-OSS/octo-cli)（只读）
- **本仓库**：需求池，用于 Issue 跟踪和 PRD 归档
