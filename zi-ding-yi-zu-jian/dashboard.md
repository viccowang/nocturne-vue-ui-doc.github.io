## Dashboard

---

#### 描述

Dashboard是企业平台的门户页面,是首屏页面,我们一般会放置一些个性化定制的内容,例如:列表,图表等等.Dashboard拥有如下功能:

1. 自定义组件且组件相互独立
2. 12列格式的瀑布式布局,与Boostrap类似
3. 自由化拖拽与自定义组件大小,并支持保存布局
4. 自定义风格(后期实现)

该组件与其他通用型组件不同, 这里没有简单的实例,因为我们这里用到的组件和其他使用Vue构建的组件没有任何区别.唯一的区别是你需要把它放在
> ** src/views/ComponentLib/Components ** 

目录下,仅此而已.Dashboard会自动将其列入可被载入在页面的组件.而剩下的则是我们需要使用数据来驱动展示其中的一些组件出来. (当然,你想全部展示也么得问题 :-P )

#### 数据结构
我们的Dashboard是数据驱动.换言之,只要有合适的数据,就可以在页面将希望展示的组件显示出来.
以下是基本的数据结构,以下所列的数据字段都是**必须含有**的,当然,你也可以添加其他数据字段.
```json
[
  {'x': 0, 'y': 0, 'w': 12, 'h': 10, 'i': '0', 'component': 'DashMap'},
  {'x': 0, 'y': 10, 'w': 4, 'h': 8, 'i': '1', 'component': 'DashChart1'},
  {'x': 4, 'y': 10, 'w': 4, 'h': 8, 'i': '2', 'component': 'DashChart2'},
  {'x': 8, 'y': 10, 'w': 4, 'h': 8, 'i': '3', 'component': 'DashChart3'},
  {'x': 0, 'y': 18, 'w': 12, 'h': 7, 'i': '4', 'component': 'DashList'}
]
```

| 字段 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| x  | 组件在页面上的横向位置  | Number  | 0,1,2... etc.  | -  |
| y  | 组件在页面上的纵向位置  | Number| 0,1,2... etc. | - |
| w  | 组件的宽(非像素,而是12列占几列) | Number | 1,2,3... etc. | - |
| h  | 组件的高(默认我们有单行高的像素值,这里可以理解为 单行高*h=组件高 ) | Number | 1,2,3... etc. | - |
| i  | 组件唯一Id,不能重复 | String | any | - |
| component | 组件的名称,对应Vue组件的name | String | any | - |


> 注意: 其中的component即是你需要展示的Vue组件的```name```.名称一定要对应.

#### 基础事件

我们在组件中,可以收到单独组件触发的一些事件, 例如拖拽移动,放大缩小,移除等等,我们经常会需要使用到这些事件. 
例如:当用户在Dashboard上缩放了一个图表组件,我们需要在组件内部来同步重置图表的大小.
类似的需求会很多. 我们这里建议直接使用独立的Store来进行控制:

```js
// dashboard
itemResize (item) {
  this.$store.dispatch('Dashboard/setOperateItem', item)
},

// myComponent
...
watch: {
  '$store.state.Dashboard.operateItem': {
    handler (item) {
      if (item.component === 'myComponent') this.doSomething()
    },
    deep: true
  }
},
...
```

#### 布局更新

自动更新布局很简单,我们只需要在```Dashboard/index.vue```中手工完成```updateLayout```方法即可.
例如:
```javascript
...
   // 当布局更新时,自动保存最新的布局
    updateLayout (newLayout) {
      this.$api['layout.update'](newLayout).then(res => {
        this.$message('布局保存成功.')
      })
    },
...    
```
> 当然,在目前的版本中,保存布局并不会触发任何界面上的展示, 因为我们希望该操作是__静默__操作.

#### 在Dashboard中跨组件通信

注意查看下面的流程图：

![](/assets/组 11.png)

我们通过在父组件放置一个临时的```compData```来接受和发送需要给所有子组件的数据。又或者可以通过```Store```来进行数据传递

