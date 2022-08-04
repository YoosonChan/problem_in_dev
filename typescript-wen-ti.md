# TypeScript问题

## [ts中`!`和`?`的用法](https://www.jianshu.com/p/dd304d5cb3dc)

!用法 用在变量前表示取反 用在赋值的内容后时，使null和undefined类型可以赋值给其他类型并通过编译

```ts
let y:number

y = null        // 无法通过编译
y = undefined   // 无法通过编译

y = null!
y = undefined!
```

## 使用interface中某属性类型

interface:

```ts
interface EffectScatterSeriesOption {
    // ...
    data?: (EffectScatterDataItemOption | ScatterDataValue)[];
    // ...
}
```

使用`data`属性的类型

```ts
EffectScatterSeriesOption["data"]
```

多处使用时，也可以直接声明

```ts
type typeName = EffectScatterSeriesOption["data"]
```

## TypeScript中使用方括号`[]`访问对象属性值问题

在TypeScript中，直接使用`object[key]`会产生错误。

> 元素隐式具有 "any" 类型，因为类型为 "any" 的表达式不能用于索引类型

因为对象的`keys`是any类型，我们需要使用`keyof`关键字处理：

### `keyof`使用

```ts
// 获取类key的类型
class A {
    a: number;
    b: number;
}
 
keyof A;
// 'a' | 'b'

// 获取对象key的类型
const a = {
    a: 1,
    b: 2,
};
keyof typeof a;
// 'a' | 'b'
```

因此在使用`object[key]`的时候需要使用`as`关键字对类型进行强制转换：

```ts
object[key as keyof typeof object]

for (k in obj) {
  console.log(obj[k as keyof typeof obj]);
}
```

## ts忽略类型检查

添加`// @ts-nocheck`注释来跳过对某些文件的检查；

添加`// @ts-check`注释只检查一些.js文件而不需要设置`--checkJs`编译选项；

添加`// @ts-ignore`到特定行的一行前来忽略这一行的错误。

##
