## 定义API及使用HTTP服务
---
这里的API定义指在```/service/api/```目录中创建js文件来定义业务中的API模型接口.这里的API将会在业务层中调用.
我们应该遵循以下实践规则:
- API的文件定义与API文档中的模块保持一致,这样的好处是无论是在类似yAPI中查阅调试API时或者查阅API文档时,代码中的API结构始终是和其他部分完全一样.
- API的文件名称应与API文档中定义的模块保持一致.
- API的书写应保持在同一项目中保持统一

> **[info] 关于RESTful **
>
> 如果你的项目使用了REST规范,则请在定义API时遵循其定义规则.

#### API模型示例

```js

export const platformApi = {
  menu: [
    {
      name: 'list',
      method: 'POST',
      path: '/menu/list',
      mockPath: '/menu/list',
      params: {
        role: []
      },
      desc: '获取菜单列表'
    },
    {
      name: 'heatmapstart',
      method: 'POST',
      path: '/temp/heatmap-start',
      mockPath: '/temp/heatmap-start',
      params: {},
      desc: '热力图'
    },
  ]
}

```
#### Vue组件中使用
接着, 我们可以在所有Vue组件中使用以下方式进行调用:

```js
/**
 * 调用一个API接口
 **/
this.$api['menu.list'](params).then(res => { })

```
#### 非Vue组件中使用
如果在非Vue组件中希望调用接口. 则需要先引入API服务

```js
import api from '@/plugins/api'

api['menu.list']({userRoles: roles}).then(res=>{ })

```

#### 使用原生axios组件
如果需要使用原生axios服务, 那么目前只可以在Vue组件中通过以下方式访问,这里直接将axios挂载到了
Vue原型对象上, 因此上下二者使用无任何区别.具体使用方式,请参考axios文档.

```js
// Vue组件中调用框架方法
this.$ajax()

// 调用原生方法
import axios from './axios'
axios.request()
axios.get()
axios.post()
...

```


