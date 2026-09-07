# 07 安装与发布

> 来源: `octo-cli version`; npm/go 安装方式

## 版本信息

```json
{
  "version": "0.9.0",
  "commit": "29ec0bcf5daa94c8fd833d2f41a29ab76420ea9f",
  "build_date": "2026-07-27T09:18:56Z"
}
```

## 安装方式

### npm（推荐）

```bash
npm install -g @openclaw/octo-cli
```

### go install

```bash
go install github.com/openclaw/octo-cli@latest
```

### 验证安装

```bash
octo-cli version
which octo-cli
```

## 发布包命名

- npm 包名：`@openclaw/octo-cli`
- 二进制：`octo-cli`
- 伴随工具：`octo-daemon`（Bot 守护进程）

## Bot 注册（发布时一次性操作）

```bash
# 注册 bot（仅需一次；不通过 authBot 中间件，用 token prefix 路由）
octo-cli bot register

# 发布 bot 命令列表
octo-cli bot set-commands --data '{"commands":[{"command":"help","description":"查询 octo-cli 用法"}]}'

# 捕获 owner_uid（只在 register 响应里出现一次，务必缓存）
owner=$(octo-cli bot register --jq '.data.owner_uid')
```

来源: `octo-cli version`; `octo-cli skills octo-files` → "bot register"; `octo-cli skills octo-shared`
