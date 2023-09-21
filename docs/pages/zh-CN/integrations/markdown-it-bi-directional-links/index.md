# 双向链接

## 效果演示

[[双向链接示例页面]]

## 介绍

**双向链接** （也被称之为内部链接，英文 Bi-directional links 和 Internal links），和也许你也了解和听说过另一个有关的概念 [WikiLinks](https://en.wikipedia.org/wiki/Help:Link)，在文档工程中有着非常重要的地位，它通常用于快速的建立一个页面到另一个页面的连接（或者链接），在 [Wikipedia](https://wikipedia.org) 这样的 Wiki 框架中，以及现在所流行的 [Obsidian](https://obsidian.md/) 和 [Logseq](https://logseq.com/) 中都被广泛使用。

这个插件是 [Obsidian](https://obsidian.md) 的[内部链接](https://help.obsidian.md/Linking+notes+and+files/Internal+links)的兼容实现版本，它遵循两条规则：

1. 一个页面的文件名称（不包含扩展名）可以作为一个链接的目标，例如：`[[双向链接示例页面]]` 将会被解析为一个指向全局唯一的 `双向链接示例页面.md` 文件的链接。
2. 一个链接的目标可以是一个绝对路径，例如：`[[某个文件夹/双向链接示例页面]]` 将会被解析为一个指向 `某个文件夹/双向链接示例页面.md` 的链接，通常出现在你有多个同名文件的时候。

### 用法示例

```markdown
[[双向链接目标页面的文件名称]]
```

## 如何使用

### 安装

通过下面的命令将 `@nolebase/markdown-it-bi-directional-links` 安装到你的项目依赖中：

::: code-group

```shell [pnpm]
pnpm add @nolebase/markdown-it-bi-directional-links
```

```shell [npm]
npm install @nolebase/markdown-it-bi-directional-links
```

```shell [yarn]
yarn add @nolebase/markdown-it-bi-directional-links
```

:::

### 为 VitePress 配置

在 VitePress 的配置文件中（通常为 `docs/.vitepress/config.ts`，文件路径和拓展名也许会有区别），将 `@nolebase/markdown-it-bi-directional-links` 作为一个插件导入，并将其作为 `markdown` 选项的 `markdown-it` 插件使用：

<!--@include: @/pages/zh-CN/snippets/details-colored-diff.md-->

```typescript
import process from 'node:process' // [!code ++]
import { defineConfigWithTheme } from 'vitepress'
import { MarkdownItBiDirectionalLinks } from '@nolebase/markdown-it-bi-directional-links' // [!code ++]

export default defineConfigWithTheme({
  lang: 'zh-CN',
  title: '网站名称', // 仅供参考，请不要直接复制
  description: '某些介绍', // 仅供参考，请不要直接复制
  themeConfig: {
    // 其他各种配置...
  },
  markdown: {
    config: (md) => {
      md.use(MarkdownItBiDirectionalLinks({ // [!code ++]
        dir: process.cwd(), // 注意这行不要漏掉了哦 // [!code ++]
      })) // [!code ++]
    },
  },
})
```

### 自由配置

<!--@include: @/pages/zh-CN/snippets/configure-on-your-own-warning.md-->

在 [`markdown-it`](https://github.com/markdown-it/markdown-it) 的实例可被访问的地方先使用 `import` 语句将双向链接插件导入到文件中：

```typescript
import MarkdownItBiDirectionalLinks from '@nolebase/markdown-it-bi-directional-links' // [!code ++]
```

然后使用 `markdown-it` 实例的 `use()` 函数将导入后的 `MarkdownItBiDirectionalLinks` 作为插件使用，并配置一个包含有 `dir` 字段的对象，这个所谓的 `dir` 字段通常可以直接通过 `import` 语句导入来自 `process` 或者 `node:process` 包内的 `cwd()` 函数来获取：

```typescript
import MarkdownItBiDirectionalLinks from '@nolebase/markdown-it-bi-directional-links'
import { cwd } from 'process' // [!code ++]

// 中间剩余的其他代码...

markdownIt.use(MarkdownItBiDirectionalLinks({ // [!code ++]
  dir: process.cwd() // [!code ++]
})) // [!code ++]
```