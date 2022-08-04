# Vue3问题

## 在Vue3的SFC中使用[`<script setup>`的`defineProps`](https://v3.cn.vuejs.org/api/sfc-script-setup.html#defineprops-%E5%92%8C-defineemits)

在 `<script setup>` 中必须使用 `defineProps` 和 `defineEmits` API 来声明 `props` 和 `emits` ，它们具备完整的类型推断并且在 `<script setup>` 中是直接可用的。

如果使用了 Typescript，[使用纯类型声明来声明 prop 和 emits](https://v3.cn.vuejs.org/api/sfc-script-setup.html#%E4%BB%85%E9%99%90-typescript-%E7%9A%84%E5%8A%9F%E8%83%BD) 也是可以的。

```ts
const props = defineProps<{
  foo: string
  bar?: number
}>()
```

原本的`defineProps`定义时，属性的类型`type`只能使用原本的类型声明，如果需要使用自定义声明，需要强制转换类型。

自定义类型`interface MapData`:

```ts
const props = defineProps({
  citys: {
    type: MapData[]
  }
})
```

以上不支持，**强制转换**解决方式：

```js
const props = defineProps({
  citys: {
    type: Array as () => Array<MapData>
  }
})
```

> 强制转换`as`关键字

## 在Vue3的SFC中使用`<script setup>`的`defineEmits`

Vue `<script setup>` compiler macro for declaring a component's emitted events. The expected argument is the same as the component emits option.

Example runtime declaration:

```ts
const emit = defineEmits(['change', 'update'])
Example type-based declaration:

const emit = defineEmits<{
  (event: 'change'): void
  (event: 'update', id: number): void
}>()

emit('change')
emit('update', 1)
```

This is only usable inside `<script setup>`, is compiled away in the output and should not be actually called at runtime.

## Vue3组件同步参数值功能变化[`.sync` -> `v-model:`](https://v3.cn.vuejs.org/guide/migration/v-model.html#%E6%A6%82%E8%A7%88)

> 非兼容：`v-bind` 的 `.sync` 修饰符和组件的 `model` 选项已移除，可在 `v-model` 上加一个**参数**代替；

```html
<component :propName.sync="propValue"></component>
```

> 提示：`[vue/no-deprecated-v-bind-sync] '.sync' modifier on 'v-bind' directive is deprecated. Use 'v-model:propName' instead.eslint-plugin-vue`

```html
<component v-model:propName="propValue"></component>
```

> 在 `3.x` 中，自定义组件上的 `v-model` 相当于传递了 `modelValue` prop 并接收抛出的 `update:modelValue`

```html
<ChildComponent v-model:title="pageTitle" />
<!-- 是以下的简写: -->
<ChildComponent :title="pageTitle" @update:title="pageTitle = $event" />
```

## 异步组件传值问题

若父子组件中，子组件参数双向绑定时，若父组件传参的值是在异步方法中赋值或者改变值。那么子组件不能正常更新，需要`watch`方法侦听`props`中参数值的变化。

```ts
/**
 * 监听参数变化
 */
watch(
  () => props.citys,
  (value) => {
    console.log("watch-> ", value);
    // ...一些操作
  }
);
```

**注意**：下面的写法不会被触发：

```ts
watch(props.value, (value, prevValue) => {
  /* ... */
})
```

## Vue3中获取`route`

Vue3中的Vue-router需要导入router，然后使用`getRoutes`方法获取route信息。

但是，获取到的是一个`to`和`from`的route信息数组，要是需要当前路由需要选择第一个`to`。

```ts
import router from "../../router";
const route = router.getRoutes()[0];
```

获取URL中的query params时，可以使用`router`里面的`currentRoute`：

```ts
router.currentRoute.value.query
```

## Vue中相同路由名时，组件不更新问题

引用相同组件的时候，会导致该组件无法更新。

解决方案：

给`<router-view :key="key"></router-view>`增加一个不同`:key`值，这样vue就会识别这是不同的`<router-view>`

##
