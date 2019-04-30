## CommonSearch

---

#### 描述

当你的模块需要一个检索条件的区域时,可以使用该组件, 组件支持浮动隐藏与默认显示的方式展现.

> **[info] 隐藏还是固定? **
>
> 一般情况下,如果我们的检索条件很少, 那么应该使用 ```isAbsolute```将检索条件固定在页面上,无需隐藏.用户可以快速进行检索. 反之亦然.

#### 演示

```html
<template>
    <common-search :isShow="showSearch" isAbsolute>
        <el-form></el-form>
    </common-search>
</template>
```

```js
<script>
import commonSearch from '@/components/commonSearch'
export default {
    name:'DemoComponent',
    data () {
        showSearch: false
    },
    components: { commonSearch }
}
</script>
```

#### 

#### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| isShow | 是否显示 | Boolean | - | false |
| isAbsolute | 是否默认展示出来还是浮动隐藏. | Boolean | - | false |




