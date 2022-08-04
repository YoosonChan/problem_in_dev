# Echarts问题

## echarts导入与使用

> 在echarts官方示例中：
>
> 1. **代码编辑**选项下，选择**ts**版本；
> 2. 选择**完整代码**选项；
> 3. **完整代码**选项下，选择**按需导入**选项。

导入代码（地图+散点图）：

```ts
/**
 * 导入
 */
import * as echarts from "echarts/core";
import { GeoComponent, GeoComponentOption } from "echarts/components";
import {
  ScatterChart,
  EffectScatterChart,
  ScatterSeriesOption,
  EffectScatterSeriesOption,
} from "echarts/charts";
import { CanvasRenderer } from "echarts/renderers";

import chinaJson from "./map/china.json";

/**
 * 注册组件
 */
echarts.use([GeoComponent, ScatterChart, EffectScatterChart, CanvasRenderer]);

/**
 * 注册地图
 */
echarts.registerMap("china", JSON.stringify(chinaJson));

/**
 * 声明部分
 */
type EChartsOption = echarts.ComposeOption<
  GeoComponentOption | ScatterSeriesOption | EffectScatterSeriesOption
>;
```

## Vue3(ts)中echarts地图的使用

地图的使用需要在`use`注册完组件之后，使用`echarts`中的[`registerMap`方法](https://echarts.apache.org/zh/api.html#echarts.registerMap)注册地图。第一个参数为地图名称，对应`geo`配置项中的`name`属性。第二个参数需要自己去下载`geoJson`数据。

```ts
import chinaJson from "./map/china.json";
echarts.registerMap("china", JSON.stringify(chinaJson));
```

##
