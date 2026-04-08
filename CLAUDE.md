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

## 行为约定

- 当用户询问"有哪些需求"、"查看需求"、"需求列表"、"有哪些任务"、"查看任务"等问题时：
  1. 先检查 memory 中是否存在当前用户的飞书身份信息（feishu_identity）
  2. 如果不存在，先询问用户姓名，然后通过 search_user_info 获取 user_key 并存入 memory
  3. 如果存在，使用该 user_key 作为 current_status_operator 过滤条件，在飞书空间"需求管理-测试"下查询"AI需求管理"工作项类型的数据
  4. 不要查询全空间待办
