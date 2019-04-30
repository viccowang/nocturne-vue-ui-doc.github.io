## CommonTable

---

#### 描述

当你需要整合列表和翻页组件时,可以用该自定义组件. 该自定义组件还可以帮你配置一个自定义缩放列表和最小高度.

> **[warning] 注意内部的使用**
>
> 组件中需要配置两个`template`来完成表格和翻页的整合.**请勿使用**其他标签,因为其他标签会自动生成DOM,影响布局.

#### 演示

```html
<template>
    <common-table size="small" :flex="150" :minHeight="300">
        <template slot="table">
            <el-table></el-table>
        </template>
        <template slot="pagination">
            <el-pagination />
        </template>
    </common-table>
</template>
```

```js
<script>
import commonTable from '@/components/commonTable'
export default {
    name:'DemoComponent',
    components: { commonTable }
}
</script>
```

#### 

#### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| size | 该属性和ElementUI的size不同,设置了该值之后,表格的行高会更窄一些.仅此而已. | String | small | - |
| flex | 设置该值之后,表格会自动缩放高低,缩放的原理是: 表格高度 = 当前页面的高度 - flex值 | Number | - | - |
| minHeight | 表格最小高度,设置该值之后,表格的高度不会小于该值的高度 | Nubmer | - | - |



