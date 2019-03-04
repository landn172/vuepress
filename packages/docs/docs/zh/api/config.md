---
sidebarDepth: 3
---

# 配置

## 基本配置

### base

- 类型: `string`
- 默认值: `/`

部署站点的基础路径，如果你想让你的网站部署到一个子路径下，你将需要设置它。如 Github pages，如果你想将你的网站部署到 `https://foo.github.io/bar/`，那么 `base` 应该被设置成 `"/bar/"`，它的值应当总是以斜杠开始，并以斜杠结束。

`base` 将会自动地作为前缀插入到所有以 `/` 开始的其他选项的链接中，所以你只需要指定一次。

**参考:**

- [Base URL](../guide/assets.md#基础路径)
- [部署指南 > Github Pages](../guide/deploy.md#github-pages)

### title

- 类型: `string`
- 默认值: `undefined`

网站的标题，它将会被用作所有页面标题的前缀，同时，默认主题下，它将显示在导航栏（navbar）上。

### description

- 类型: `string`
- 默认值: `undefined`

网站的描述，它将会以 `<meta>` 标签渲染到当前页面的 HTML 中。

### head

- 类型: `Array`
- 默认值: `[]`

额外的需要被注入到当前页面的 HTML `<head>` 中的标签，每个标签都可以以 `[tagName, { attrName: attrValue }, innerHTML?]` 的格式指定，举个例子，增加一个自定义的 favicon：

``` js
module.exports = {
  head: [
    ['link', { rel: 'icon', href: '/logo.png' }]
  ]
}
```

### host

- 类型: `string`
- 默认值: `'0.0.0.0'`

指定用于 dev server 的主机名。

### port

- 类型: `number`
- 默认值: `8080`

指定 dev server 的端口。

### temp

- Type: `number`
- Default: `@vuepress/core/.temp`

指定客户端文件的临时目录。

### dest

- 类型: `string`
- 默认值: `.vuepress/dist`

指定 `vuepress build` 的输出目录。如果传入的是相对路径，则会基于 `process.cwd()` 进行解析。

### ga

- 类型: `string`
- 默认值: `undefined`

提供一个 Google Analytics ID 来使 GA 生效。

::: tip 提示
请留意 [GDPR (2018年欧盟数据保护规则改革)](https://ec.europa.eu/commission/priorities/justice-and-fundamental-rights/data-protection/2018-reform-eu-data-protection-rules_en), 在合适或者需要的情况下，考虑将 Google Analytics 设置为[匿名化的 IP](https://support.google.com/analytics/answer/2763052?hl=zh-Hans)。
:::

### locales

- 类型: `{ [path: string]: Object }`
- 默认值: `undefined`

提供多语言支持的语言配置。具体细节请查看 [多语言支持](../guide/i18n.md)。

### shouldPrefetch

- 类型: `Function`
- 默认值: `() => true`

一个函数，用来控制对于哪些文件，是需要生成 `<link rel="prefetch">` 资源提示的。请参考 [shouldPrefetch](https://ssr.vuejs.org/zh/api/#shouldpreload)。

### cache

- 类型: `boolean|string`
- 默认值: `true`

VuePress 默认使用了 [cache-loader](https://github.com/webpack-contrib/cache-loader)  来大大地加快 webpack 的编译速度。

此选项可以用于指定 cache 的路径，同时也可以通过设置为 `false` 来在每次构建之前删除 cache。

::: tip 提示
这个选项也可以通过命令行来使用：
```bash
vuepress dev docs --cache .cache # 设置 cache 路径
vuepress dev docs --no-cache     # 在每次构建前删除 cache
```
:::

## Styling

### palette.styl

如果要对[默认预设](https://github.com/vuejs/vuepress/blob/master/packages/@vuepress/core/lib/app/style/config.styl)的样式应用简单的颜色替换，或者定义一些颜色变量供以后使用，你可以创建一个 `.vuepress/styles/palette.styl` 文件。

你可以调整一些颜色变量:

``` stylus
// 默认值
$accentColor = #3eaf7c
$textColor = #2c3e50
$borderColor = #eaecef
$codeBgColor = #282c34
```

::: danger 注意
你应该**只在**这个文件中写入颜色变量。因为 `palette.styl` 将在根的 stylus 配置文件的末尾引入，作为配置，它将被多个文件使用，所以一旦你在这里写了样式，你的样式就会被多次复制。
:::

### index.styl

VuePress 提供了一种添加额外样式的简便方法。你可以创建一个 `.vuepress/styles/index.styl` 文件。这是一个 [Stylus](http://stylus-lang.com/) 文件，但你也可以使用正常的 CSS 语法。 

```stylus
.content {
  font-size 30px
}
```

## 主题

### theme

- 类型: `string`
- 默认值: `undefined`

当你使用自定义主题的时候，需要指定它。

**参考:**

- [使用主题](../theme/using-a-theme.md).

### themeConfig

- 类型: `Object`
- 默认值: `{}`

为当前的主题提供一些配置，这些选项依赖于你正在使用的主题。

**也可以参考:**

- [默认主题](../theme/default-theme-config.md)。

## Pluggable

### plugins

- 类型: `Object|Array`
- 默认值: `undefined`

请参考 [plugin > Using a plugin](../plugin/using-a-plugin.md) 来使用一个插件。

## Markdown

### markdown.lineNumbers

- 类型: `boolean`
- 默认值: `undefined`

是否在每个代码块的左侧显示行号。

**参考:**

- [行号](../guide/markdown.md#行号)

### markdown.slugify

- 类型: `Function`
- 默认值: [source](https://github.com/vuejs/vuepress/tree/master/packages/@vuepress/shared-utils/src/slugify.ts)

一个将标题文本转换为 slug 的函数。修改它会影响 [标题](../miscellaneous/glossary.md#headers)、[目录](../guide/markdown.md#目录)、以及[侧边栏](../theme/default-theme-config.md#侧边栏)链接的 id 和 链接。

### markdown.anchor

- 类型: `Object`
- 默认值: `{ permalink: true, permalinkBefore: true, permalinkSymbol: '#' }`

[markdown-it-anchor](https://github.com/valeriangalliat/markdown-it-anchor) 的选项。

### markdown.externalLinks

- 类型: `Object`
- 默认值: `{ target: '_blank', rel: 'noopener noreferrer' }`

这个键值对将会作为特性被增加到是外部链接的 `<a>` 标签上，默认的选项将会在新窗口中打开一个该外部链接。

### markdown.toc

- 类型: `Object`

这个值将会控制 `[[TOC]]` 默认行为。它包含下面的选项：

- includeLevel: [number, number]，决定哪些级别的标题会被显示在目录中，默认值为 `[2, 3]`。
- containerClass: string，决定了目录容器的类名，默认值为 `table-of-contents`。
- markerPattern: RegExp，决定了标题匹配的正则表达式，默认值为 `/^\[\[toc\]\]/im`。
- listType: string 或 Array，决定了各级列表的标签，默认值为 `"ul"`。
- containerHeaderHtml: string，在目录开头插入的 HTML 字符串，默认值为 `""`。
- containerFooterHtml: string，在目录结尾插入的 HTML 字符串，默认值为 `""`。

此外，我们还提供了[全局组件 TOC](../guide/using-vue.md#toc)，可以通过直接向 `<TOC>` 传递属性实现更加自由的控制。

### markdown.extendMarkdown

- 类型: `Function`
- 默认值: `undefined`

一个用于修改当前的 [markdown-it](https://github.com/markdown-it/markdown-it) 实例的默认配置，或者应用额外的插件的函数，举例如下：

``` js
module.exports = {
  markdown: {
    extendMarkdown: md => {
      md.set({ breaks: true })
      md.use(require('markdown-it-xxx'))
    }
  }
}
```

::: tip 提示
这个选项也被 [Plugin API](../plugin/option-api.md#extendmarkdown) 所支持。
:::

## 构建流程

### postcss

- 类型: `Object`
- 默认值: `{ plugins: [require('autoprefixer')] }`

[postcss-loader](https://github.com/postcss/postcss-loader) 的选项，请注意，指定这个值，将会覆盖内置的 autoprefixer，所以你需要自己将它加进去。

### stylus

- 类型: `Object`
- 默认值: `{ preferPathResolver: 'webpack' }`

[stylus-loader](https://github.com/shama/stylus-loader) 的选项。

### scss

- 类型: `Object`
- 默认值: `{}`

加载 `*.scss` 文件的 [sass-loader](https://github.com/postcss/postcss-loader) 的选项。

### sass

- 类型: `Object`
- 默认值: `{ indentedSyntax: true }`

加载 `*.sass` 文件的 [sass-loader](https://github.com/postcss/postcss-loader) 的选项。

### less

- 类型: `Object`
- Default: `{}`

[less-loader](https://github.com/webpack-contrib/less-loader) 的选项。

### configureWebpack

- 类型: `Object | Function`
- 默认值: `undefined`

用于修改内部的 Webpack 配置。如果给定一个对象，那么它将会被 [webpack-merge](https://github.com/survivejs/webpack-merge) 合并到最终的配置中，如果给定一个函数，它将会接受 `config` 作为第一个参数，以及 `isServer` 作为第二个参数，你可以直接更改 `config`，也可以返回一个待合并的对象。

``` js
module.exports = {
  configureWebpack: (config, isServer) => {
    if (!isServer) {
      // 修改客户端的 webpack 配置
    }
  }
}
```

### chainWebpack

- 类型: `Function`
- 默认值: `undefined`

通过 [webpack-chain](https://github.com/mozilla-neutrino/webpack-chain) 来修改内部的 Webpack 配置。

``` js
module.exports = {
  chainWebpack: (config, isServer) => {
    // config 是 ChainableConfig 的一个实例
  }
}
```

## 浏览器兼容性

### evergreen

- 类型: `boolean`
- 默认值: `false`

如果你的对象只有那些 “常青树” 浏览器，你可以将其设置成 `true`，这将会禁止 ESNext 到 ES5 的转译以及对 IE 的 polyfills，同时会带来更快的构建速度和更小的文件体积。