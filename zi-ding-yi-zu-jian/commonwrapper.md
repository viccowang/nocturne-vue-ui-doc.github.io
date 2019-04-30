## CommonWrapper

---

#### 描述

当你的模块需要一个内边距和圆角边框的wrapper,则可以使用该组件进行包裹.

#### 演示

```html
<template>
    <common-wrapper>
        <div>
            Hi, {{ name }}!
        </div>
    </common-wrapper>
</template>
```

```js
<script>
import commonWrapper from '@/components/commonWrapper'
export default {
    name:'DemoComponent',
    data () {
       name: 'Jack' 
    },
    components: { commonWrapper }
}
</script>
```

#### 

#### 属性

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| full | 当你的组件不需要外边距和圆角时,可以配置该属性. | Boolean | - | - |



