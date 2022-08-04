# 基础问题

## [newDate()苹果手机日期格式显示NaN](https://blog.csdn.net/chelen\_jak/article/details/98215109) <a href="#articlecontentid" id="articlecontentid"></a>

```javascript
new Date("1990-01-01 08:00:00")
```

以`-`形式组成的时间字符串创建的时间在安卓手机上显示是正常的，在苹果手机上显示为`NaN`。

解决方案是通过替换字符串的方法，讲字符串中的 `-` 替换为 `/` ，这样就能正常显示了。

```javascript
new Date("1990-01-01 08:00:00".replace(/\-/g, "/"))
// => 结果：1990/01/01 08:00:00
```

## 在函数的默认传参之外额外传入自定义参数 <a href="#articlecontentid" id="articlecontentid"></a>

当一个组件的属性或者事件的方法含有默认的参数值的时候，如果我们在编写方法的时候，还需要额外传入自己需要的自定义参数时，我们需要写一个闭包来实现它。

```
<template>
    <components
        @event="(param1: any, param2: any) => handle(param1, param2, param)"
        :attribute="(param1: any, param2: any) => handle(param1, param2, param)"
    >
    </components>
</template>

<script setup lang="ts">
const handle = (param1: any, param2: any, param: any) => {
  // ...handle
};
</script>
```

> `<components>`：组件；
>
> `@even`：组件事件；
>
> `:attribute`：组件属性；
>
> `handle`：处理事件/属性的方法；
>
> `(param1: any, param2: any)`：组件原本方法中含有的默认参数`param1` 和 `param2`；
>
> `param`：方法中需要的自定义参数。

## Axios的上传文件注意事项 <a href="#articlecontentid" id="articlecontentid"></a>

当通过 `input` 的方式上传文件时，获取到的 `file` 文件，如果通过 `post` 请求发送是，需要将 `file` 转换为 `FormData` 的形式再上传。

```javascript
var data = new FormData();
// file为上传的文件
data.append("file", file);
```

## &#x20;<a href="#articlecontentid" id="articlecontentid"></a>
