# AiCode 插件索引

## 概述

本仓库是 AiCode 的插件索引仓库，仅维护一个 `index.json`，用于描述可用插件及其发布信息。

插件源码与安装包不存放在本仓库。每个插件由作者在自己的 GitHub 仓库中维护，并通过该仓库的 Release 发布安装包。

## 仓库结构

```text
.
├── index.json
└── schema/
    └── index.schema.json
```

- `index.json`：插件索引的唯一数据文件。
- `schema/index.schema.json`：索引的 JSON Schema，用于编辑器和校验工具检查格式。

## 索引格式

### 顶层字段

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `schema_version` | integer | 是 | 索引格式版本，当前固定为 `1` |
| `plugins` | array | 是 | 插件条目列表 |

### `plugins[]` 字段

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `id` | string | 是 | 插件唯一标识，必须与包内 `plugin.json` 的 `id` 一致，格式为 `发布者.插件名` |
| `name` | string | 是 | 插件展示名称 |
| `description` | string | 是 | 插件简介 |
| `author` | string | 是 | 发布者标识，必须与包内 `plugin.json` 的 `publisher` 一致 |
| `repository` | string | 是 | 插件源码仓库，必须为 GitHub 仓库地址 |
| `logo` | string | 否 | 插件图标地址，必须为 https URL |
| `homepage` | string | 否 | 项目主页地址，必须为 https URL |
| `license` | string | 否 | 许可证标识，例如 `MIT` |
| `tags` | array | 否 | 分类标签；填写时 1–4 个且不可重复 |
| `version` | string | 否 | 当前版本，SemVer，不能以 `v` 开头；未填写时默认最新版 |
| `min_app_version` | string | 否 | 最低兼容的 App 版本，SemVer 格式 |

`tags` 可选值：

`provider`、`tool`、`skill`、`agent`、`mcp`、`ui`、`integration`、`other`。

## 示例

```json
{
  "schema_version": 1,
  "plugins": [
    {
      "id": "author-name.aicode-sample-plugin",
      "name": "AiCode Sample Plugin",
      "description": "An AiCode sample plugin.",
      "author": "author-name",
      "repository": "https://github.com/author-name/aicode-sample-plugin",
      "logo": "https://raw.githubusercontent.com/author-name/aicode-sample-plugin/main/logo.png",
      "homepage": "https://github.com/author-name/aicode-sample-plugin",
      "license": "MIT",
      "tags": ["tool"],
      "version": "1.0.0",
      "min_app_version": "1.14.0"
    }
  ]
}
```

## Release 规范

- 资产文件名为 `{id}_{version}.zip`。

## 维护约定

- 一个插件对应 `plugins` 数组中的一个对象。
- 插件作者更新时修改自己的对象并提交 PR。
