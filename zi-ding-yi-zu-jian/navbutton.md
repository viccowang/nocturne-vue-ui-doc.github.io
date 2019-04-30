## NavButton

---

#### 描述

当你的组件需要使用顶部的按钮,例如新建,修改,导入导出时,亦或是需要使用权限配置按钮时,可以使用该组件.该组件会有一个非依赖关系的子组件(**NavPremissionButton**)配合使用以实现权限按钮.
> **[warning] 权限按钮的重要配置项 **
>
> 在使用权限按钮组件**NavPremissionButton**时,**务必要传递当前组件的引用this**.

#### 演示
```html
<template>
    <nav-button>
        <nav-premission-button :buttonData="premissionButtonData" :comp="comp" />
        <el-button-group>
            <el-button>New</el-button>
            <el-button>Export</el-button>
        </el-button-group>
    <nav-button>
</template>
```
```js
<script>
import NavButton from '@/components/navButton'
import NavPremissionButton from '@/components/navButton/navPremissionButton'
export default {
    name:'DemoComponent',
    data () {
        comp: this,
        premissionButtonData: []
    },
    components: { NavButton, NavPremissionButton }
}
</script>
```

#### NavButton属性

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| - |-  |- | - |-  |


#### NavPremissionButton属性

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| comp| 当前组件的实例引用,通常会通过```data()```传递```this```进来  | Object  | -  | - |
| buttonData| 权限按钮数据对象,数据对象参数见下表  | Array  | -  | - |

#### ButtonData属性

| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| name | 按钮的名称,会显示当前是什么按钮,例如:新建 | String | - | - |
| click | 按钮的点击事件Function名 | String | - | - |
| name | 按钮的名称,会显示当前是什么按钮,例如:新建 | String | - | - |
| size | 参数同el-button的size  | String  | small/mini  etc. | -  |
| icon | 按钮的前缀图标 | String  | -   | -  |













