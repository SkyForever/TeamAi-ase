---
description: 命名规范
alwaysApply: true
---

# 命名规范

## 1) 总体原则
- 命名以语义清晰为第一优先级，尽量简短明确。
- 命名统一使用英文，避免无意义缩写。
- 可用字符：英文字母、`-`、`_`（按不同场景使用对应风格）。

## 2) 模块与文件命名
- 模块文件夹命名：全小写 + 中划线（kebab-case），如 `my-project-name`。
- 模块通常放在 `pages` 目录下。
- 常见目录命名：`js`、`css`、`img`、`video`、`audio`、`data-models`。
- JS 文件命名：kebab-case，如 `account-model.js`。
- CSS/SCSS 文件命名：kebab-case，如 `retina-sprites.scss`。
- HTML 文件命名：kebab-case，如 `error-report.html`。

## 3) 页面命名
- 页面放在对应模块目录下，页面名不重复带模块前缀。
- 推荐页面文件名：
  - 模块首页：`index`
  - 列表页：`list`（如即首页可直接用 `index`）
  - 详情页：`detail`
  - 编辑页：`edit`
  - 新增页：`create`（若新增/编辑共页，统一用 `edit`）
- 示例（商品模块）：
  - `pages/product/index`
  - `pages/product/detail`
  - `pages/product/edit`

## 4) 路由命名
- 路由 path 与页面命名尽量一致。
- 模块首页子路由 path 使用空字符串 `''`，不使用 `index`。
- 示例：
  - 主路由：`/product`
  - 子路由：首页 `''`，详情 `detail`，编辑 `edit`

## 5) 接口命名（API）
- API 按模块拆分管理，统一放在 `api` 目录，按模块命名，如 `product.service`。
- 接口函数命名规则：`动作 + 模块 + 内容`。
- 动作关键词：
  - 获取：`get`
  - 创建：`create`
  - 编辑：`edit`
  - 删除：`del`
  - 状态变化：`change`
- 示例：
  - `getProductList`
  - `getProductDetail`
  - `createProduct`
  - `editProduct`
  - `delProduct`
  - `changeProductStatus`

## 6) 页面调用接口方法命名
- 页面内调用方法命名：`动作 + 名称`。
- 示例：
  - `getProductList`
  - `getProductDetail`
  - `createProduct`
  - `editProduct`
  - `delProduct`
- 约束：一个方法只处理一个接口请求；多接口组合判断时新建独立编排方法。

## 7) 子模块规则
- 有子模块/子分类时，在模块目录下建立子目录，命名使用子模块语义名。
- 页面命名、路由命名延续主规则。
- 接口可与主模块集中管理，命名可扩展为：`动作 + 主模块 + 子模块 + 内容`。

## 8) 样式命名规则
- `class`：全小写 + 中划线（kebab-case）。
- `id`：驼峰命名（camelCase）。
- scss 的变量、函数、mixin、placeholder：驼峰命名（camelCase）。

## 9) 变量/常量/函数命名
- 变量：驼峰命名（camelCase）。
- 常量：全大写 + 下划线（UPPER_SNAKE_CASE），如 `MAX_COUNT`、`API_BASE_URL`。
- 函数：驼峰命名；构造函数首字母大写。
- 函数前缀语义：
  - `can`：是否可执行（返回布尔）
  - `has`：是否包含（返回布尔）
  - `is`：是否为某状态（返回布尔）
  - `get`：获取值（返回非布尔）
  - `set`：设置值（通常无返回或返回设置结果）

## 10) AI 执行约束
- 涉及新模块开发时，优先读取后端文档/接口定义；仅在无法确定时再询问后生成前端代码。
- 若现有代码与本规范冲突：新增代码按规范执行；存量代码分批治理，不一次性全量重命名。
- 输出代码时优先给出符合规范的目录、路由、API、调用方法命名。
