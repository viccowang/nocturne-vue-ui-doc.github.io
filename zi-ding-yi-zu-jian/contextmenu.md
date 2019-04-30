## Contextmenu

---

#### 描述
 
顾名思义,这是一个展示右键菜单的组件.该组件是[XBT:v-contextmenu](https://github.com/XBT1/v-contextmenu)的扩展版本,本着```DRY```原则,仅仅在此基础上进行了适合公司业务平台的扩展开发.
该右键菜单具有如下特点:
- 完全模板驱动型
- 支持全局引入或单独引入
- 支持多级菜单
- 支持自定义触发方式(click, rightClick etc.)
- 支持动态菜单
- 支持自定义主题
- 丰富的钩子函数

#### 演示
```html
<template>
  <div class="context-menu">
    <v-contextmenu ref="menu1">
        <v-contextmenu-item>New Item</v-contextmenu-item>
        <v-contextmenu-item>Edit Item</v-contextmenu-item>
        <v-contextmenu-item @click="showParam">click to get Param</v-contextmenu-item>
    </v-contextmenu>
    
    <el-button v-contextmenu:menu1="menuParams">show contextmenu</el-button>
  </div>
</template>  
```
```js
export default {
  name: 'Contextmenu',
   data () {
    return {
      menuParams: { name: 'Vicco.W.', message: 'Hello World!' }
    }
  },
  methods: {
    // 菜单的方法接到三个参数
    // menuItem: 菜单行本身(Vue Component)
    // event: 事件
    // params  菜单回传接收到的参数,该参数由v-contextmenu指令传入(如上传入了menuParams)
    showParam (menuItem, event, {name, message}) {
     // elementUI Message component
      this.$message({
        message: `name: ${name}, text: ${message}`,
        type: 'success'
      })
    }
  }
```
> 以上例子是一个典型演示

---

### Contextmenu 
#### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| eventType |触发方式 | String | window.eventType | contextmenu  |
| theme |自定义主题 | String | - | default  |
| autoPlacement |是否自动检测边框距离,不会让菜单溢出屏幕 | Boolean | true / false | true  |
#### 事件
| 参数 | 说明 | 回调函数参数 | 
| :--- | :--- | :--- | :--- | :--- |
| beforeShow | 展示菜单前触发 | ( vm, event, params ) | 
| contextmenu | 展示菜单前触发 | ( vode ) | 
| show | 展示菜单后触发 | ( vm ) |
| hide | 隐藏菜单后触发 | ( vm ) |
| beforeDestroy | 销毁菜单前触发 | ( vm ) |

---

### ContextmenuItem 
#### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| divider |分割线 | Boolean | true / false | false  |
| disabled |是否呈现为禁用 | Boolean | true / false | false  |
| autoHide |点击后是否自动关闭contextmenu | Boolean | true / false | true  |
#### 事件
| 参数 | 说明 | 回调函数参数 | 
| :--- | :--- | :--- | :--- | :--- |
| click | 点击事件 | ( vm, event, params ) | 
| mouseenter | 滑鼠划入事件 | ( vm, event, params ) | 
| mouseleave | 滑鼠划出事件 | ( vm, event, params ) | 

---

### ContextmenuSubmenu 
#### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| title | 子菜单标题 | String | - | - |
| disabled |是否呈现为禁用 | Boolean | true / false | false  |
 #### 事件
| 参数 | 说明 | 回调函数参数 | 
| :--- | :--- | :--- | :--- | :--- |
| mouseenter | 滑鼠划入事件 | ( vm, event ) | 
| mouseleave | 滑鼠划出事件 | ( vm, event ) | 
#### Slot
| 参数 | 说明 | 回调函数参数 | 
| :--- | :--- | :--- | :--- | :--- |
| title | 菜单名称, **和上面的title属性二选一** | - | 


--

### ContextmenuGroup 
#### 属性
| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| maxWidth | 最大宽度 | String / Number | - | -  |









