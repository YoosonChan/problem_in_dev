# Element Plus问题

## element-plus 图标icon组件的使用

element-plus中使用图标需要先[安装](https://element-plus.gitee.io/zh-CN/component/icon.html)包：

```
# NPM
$ npm install @element-plus/icons-vue
# Yarn
$ yarn add @element-plus/icons-vue
# pnpm
$ pnpm install @element-plus/icons-vue
```

安装之后按需导入：

```ts
import { ArrowDown, Search } from "@element-plus/icons-vue";
```

然后在template中用`<el-icon>`标签包裹起来：

```html
<el-icon class="el-icon--right">
  <arrow-down />
</el-icon>
```

部分组件可以直接成为属性值：

```html
<el-input :suffix-icon="Search" />
```

## 自定义/第三方组件未定义属性警告

> \[Vue warn]: Extraneous non-props attributes (xxx, xxx) were passed to component but could not be automatically inherited because component renders fragment or text root nodes.

在自定义组件上添加了组件本身没有定义的xxx、xxx属性，并且自定义组件内部又没有接收，所以会被警告。

因此，要么在组件内部加上属性接收，要么去掉这个属性。

如果是在第三方库UI库的话，建议直接去掉这些属性。

## element-plus国际化问题

Element Plus 组件 默认 使用英语，如果你希望使用其他语言，你可以参考下面的[方案](https://element-plus.gitee.io/zh-CN/guide/i18n.html)。

### 全局配置

```ts
import ElementPlus from 'element-plus'
import zhCn from 'element-plus/es/locale/lang/zh-cn'

app.use(ElementPlus, {
  locale: zhCn,
})
```

##
