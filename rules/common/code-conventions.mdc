---
description: 前端通用编码约定；函数/方法必须有备注；导入优先用 @ 别名；链式调用要兜底；文件不要过碎也不要过长
alwaysApply: true
---

# 编码规范（前端通用）

**本文件**：全前端共用的写法。渠道 / 项目差异见各层 `code-conventions`。命名见 `naming-conventions`。别名表见各层 `directory-conventions`。

## 1. 函数与方法备注

**强制**：新增或修改的 **每一个函数 / 方法**（含组件内事件处理、工具函数、API 导出、Hook / 组合式函数对外方法、状态层具名辅助函数）**必须**有备注。

### 1.1 写什么

备注说明 **做什么**；参数、返回值、副作用非显而易见时一并写明。语言与项目一致（默认 **中文**）。

| 场景 | 备注形式 |
|------|----------|
| 模块导出（api、utils、hooks） | 函数上方 **`/** ... */`**（JSDoc 风格） |
| 组件内 `function` / 箭头处理函数 / Vue `methods` | 函数上方 **`//`** 或 **`/** ... */`** |
| 仅本文件使用的短辅助函数 | 同上，一行亦可 |

### 1.2 不要求备注的情况

- **无**：不以「代码已自解释」为由省略；副作用 / 缓存回调（如 `useEffect` / `useMemo` / Vue `watch`）若逻辑超过 3 行，在回调上方用 `//` 说明意图。
- **禁止**用备注重复代码字面意思（如 `// 设置 loading 为 true` 紧挨 `setLoading(true)`）；应写业务意图（如 `// 提交前锁定按钮，防止重复请求`）。

### 1.3 示例

```javascript
/**
 * 从接口响应或 Error 对象提取可展示的错误文案。
 * @param {unknown} error axios 错误或业务 reject
 * @returns {string}
 */
function getErrorMessage(error) {
  // ...
}

/**
 * 获取资源列表。
 * @param {{ status?: string, page?: number, size?: number }} params 筛选条件
 * @returns {Promise<Item[]>}
 */
export async function getList(params) {
  // ...
}
```

```javascript
// 选择模式：未开放项提示，已开放项跳转对应路由
const handleSelect = (mode) => {
  if (mode.disabled) {
    message.info('暂未开放');
    return;
  }
  navigate(mode.path);
};
```

```javascript
/**
 * 封装某业务能力：状态、副作用与对外方法。
 * @returns {{ data, loading, submit, reset }}
 */
export default function useFeature() {
  /** 提交表单并刷新列表 */
  const submit = async () => { /* ... */ };
  // ...
}
```

### 1.4 Agent / 人工协作

- 生成或修改业务代码时，**先写备注再写实现**；交付前自检：文件内是否每个函数都有对应备注。
- 存量代码可随改动文件补齐，不要求一次性全库刷备注。

## 2. 导入路径

只管 **`import` / `require` / 样式 `@import`**，不管接口 URL、页面跳转。

- 跨目录 / 跨模块 **优先用 `@` 别名**（`@/` 或项目别名表），**少用 `../`**。
- **禁止** `../../../` 这类深层相对路径。
- 仅同目录或页面私有就近文件可用 `./`（如 `./index.less`、同目录子组件）。

## 3. 链式调用兜底

来源不确定的值（接口、props、store、路由参数）再链式调用时：**先 `?.`，再给与后续用法匹配的默认值**。不要直接 `list.map(...)`。

```javascript
list?.map((item) => item.id) ?? []
obj?.name ?? ''
res?.data?.records ?? []
```

- 默认值用 **`??`**，不要用 `||`（避免把 `0` / `''` / `false` 当成空）。
- 本文件已保证是数组 / 对象的局部变量不必再套一层。

## 4. 文件拆分：不要过碎，也不要过长

**过碎**：仅本页 / 本模块用的常量、校验、小函数写在使用方同文件，或收成 **一个** `utils.ts`。禁止按「一个函数一个文件」拆出 `xxx-defaults.ts`、`xxx-rules.ts` 这种几行文件。

**过长**：一个文件只承担一个主职责，打开后要能快速找到改点。

- 页面 / 组件建议控制在 **400 行以内**；超过就把一块能独立理解的 UI 拆到同目录 `components/`，或把数据 / 转换收到 hook、同模块 `utils`。
- **禁止**继续往已经很长的文件里堆。到 **800 行** 仍不拆、上千行的上帝组件，没有可读性。
- 拆的是职责（画布、属性栏、列表、弹窗），不是把 10 行函数拆出去凑文件数。
