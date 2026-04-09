# 项目约定

## 飞书项目空间

- 空间名称: 需求管理-测试
- project_key: `697c3d78d5eaf3ca7de6ffda`
- simple_name: 58wbus

所有飞书项目相关操作（查询工作项、创建任务、添加评论等）默认使用此空间，无需重复指定。

## 默认工作项类型

- 名称: AI需求管理
- type_key: `69a0faf9a0864a3cfb338356`
- api_name: aixqgl

涉及工作项操作时默认使用此类型，无需重复指定。

## 常用字段

| 字段 key | 名称 | 说明 |
|---------|------|------|
| `name` | 名称 | |
| `work_item_status` | 状态 | 值：开始 / 未开始 / 已终止 / 需求整理 / 开发实现 / 测试 |
| `current_status_operator` | 当前负责人 | 多人，用于 WHERE 过滤 |
| `priority` | 优先级 | 值：P0 / P1 / P2 |
| `field_e12cc8` | PRD文档 | |
| `field_30b512` | 分支名称 | |

## 行为约定

- ⚠️ **禁止使用 `list_todo` 工具查询任务/需求**。所有任务/需求查询必须通过 `search_by_mql` 在指定空间下进行。

- 当用户询问"有哪些需求"、"查看需求"、"需求列表"、"有哪些任务"、"查看任务"、"我有什么任务"等问题时，严格按以下流程执行：
  1. 检查 memory/feishu_identity → 不存在则询问用户姓名，通过 search_user_info 获取 user_key 并存入 memory
  2. 使用 `search_by_mql`，固定参数：
     - project_key: `697c3d78d5eaf3ca7de6ffda`
     - FROM: `需求管理-测试`.`AI需求管理`
     - SELECT: `name`, `work_item_status`, `priority`, `field_e12cc8`, `field_30b512`
     - WHERE: `current_status_operator` = 用户的 user_key
     - ORDER BY: `创建时间` DESC
  3. ❌ 禁止使用 `list_todo`
