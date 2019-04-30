## Breadcrumb

---

该组件可以在页面上展示一个当前路由状态下的面包屑.为了保证不与```ElementUI```的组件命名冲突, 这里加了前缀```header-```.
该组件使用非常简单.

> **[warning] 注意 **
>
> 目前Breadcrumb组件与NextPage内部使用的组件有冲突.


#### 使用方法

** 全局引入 **
```js
// main.js

// breadcrumb
import breadcrumb from './components/breadcrumb'
Vue.use(breadcrumb)

```

** 局部引入 **
```js
// Foo component
import { HeaderBreadcrumb } from '@/components/breadcrumb'
export default {
    ...
    components: { HeaderBreadcrumb  }
    ...
}
```

**模板定义**
```html
// Foo component
...
<template>
    ...
    <header-breadcrumb :breadData="$route.matched" />
    ...
</template>    
```

#### 属性配置

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| breadData | 为面包屑提供当前路由的数据 | Array | - | $route.matched |

> ** [warning] 传参注意**
> 
>  默认的面包屑请务必传递 ** $route.matched ** 作为参数, 如果你希望传递其他的参数,请参考该组件源文件.