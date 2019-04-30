## 配置路由表与访问权限
---

- 如果我们的项目结构很简单, 我们可以使用静态路由表,也就是手工将路由配置到```.js```文件中,并配合静态的```role```字段实现简单的权限管理.
- 如果我们的项目需要复杂的权限与更多的功能配合,那么我们则可以使用动态路由表.
  动态路由表的配置将会需要在前端生成一套配置功能,并将路由表存入数据库中.届时我们即可通过访问用户来动态生成路由数据,并交由前端生成相对应的路由表.
  
是否开启静态或动态路由表需要在```config/settings.js```中配置如下选项:
```js
export const ROUTER_DEFAULT_CONFIG = {
  isUseStaticeRouter: true
}
```  
---
#### 静态路由表的使用

当我们开启静态路由后,我们就可以配置我们的静态路由了.
静态路由文件配置在```router/asyncRouters.js```中, 我们只需要按照```vue-router```给出的正确的配置项配置路由即可.

举个栗子:
```js
  ...
  
  {
    path: '/charts',
    component: Layout,
    meta: { title: 'Charts', icon: 'zvpfont icon-chart2', role: ['user'] },
    children: [
      {
        path: 'echart',
        name: 'Charts',
        component: _import_('Charts/index'),
        meta: { title: 'Chart', icon: 'zvpfont icon-chart2' }
      }
    ]
  }
  
  ...
```
这样,该路由表内的内容会根据```role```的配置项自动合并至总路由表中.页面上我们就可以访问了.

---
    
#### 动态路由表的使用  

当我们配置动态路由表, 我们首先需要检查我们是否配置了正确的路由```API```接口,接口定义在```service/api/platform.js```中. 定义```menu.list```接口即可.
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
    }
}

```
这样,我们就可以通过该```API```来获取正确的路由表数据了.

#### 路由表数据字段
接下来,我们可以通过后端来过滤出前端需要的路由表信息.路由的数据结构如下:

##### Routers Config

| 属性| 类型 |说明 |
| :--- | :--- |:--- |
| path | String |访问路径,会展现在url中,例如```/table-list```,如果是子路由(children),**请勿**加```/``` |
| name | String |该字段**必须**与模块属性```name```相对应, 否则将影响功能模块的缓存功能|
| component | String |模块主文件加在路径,相对于```views```目录. 例如```/table/tabe-list/index```,表示需要加载的模块是```views/table/table-list/index.vue```文件|
| meta | Object |路由信息, 配置项请见下表 | 
| children | Array |子路由字段,内容配置项与父保持一致 | 

> **[warning] 注意事项 **:
> 1. 如果路由为最顶级的父节点,则不需要```name```和```component```字段, 父节点路由会被系统自动配置为父路由节点来加在```Layout```布局.配置该两项也是无效的配置.前端不会做任何处理.
> 2. 如果有且仅有1个子路由,则```path```可以为```''```(空)

##### meta Config

| 属性| 类型 |说明 |
| :--- | :--- |:--- |
| title | String | 模块名称,会显示在菜单中 |
| icon  | String | 模块前的图标展示,对应iconfont中的图标,例如: ```zvpfont icon-menu-list``` |
| noCache | Boolean | 设置改模块是否开启缓存功能. 关闭后则在用户切换标签页时,每次都会重新读取该页面. 默认为缓存模式, **注意,该属性请设置在子路由(children)上**|

下面,这里列举一个数据库返回的模拟路由表数据:

```js

{
  "head": {
    "success": "true"
  },
  "data": [
    {
      "path": "/form",
      "meta": {
        "title": "Table List",
        "icon": "zvpfont icon-menu-list"
      },
      "children": [
        {
          "path": "",
          "name": "TableList",
          "component": "Form/List/index",
          "meta": {
            "title": "Table List",
            "icon": "zvpfont icon-menu-list"
          }
        }
      ]
    },
    {
      "path": "/map",
      "meta": {
        "title": "Map",
        "icon": "zvpfont icon-map"
      },
      "children": [
        {
          "path": "bmap",
          "name": "BaiduMapCom",
          "component": "Map/BaiduMap/index",
          "meta": {
            "title": "Baidu Map",
            "icon": "zvpfont icon-dizhi1"
            "noCache": true
          }
        },
        {
          "path": "heat-map",
          "name": "HeatMap",
          "component": "Map/HeatMap/index",
          "meta": {
            "title": "Heat Map",
            "icon": "zvpfont icon-icheatmap",
            "noCache": true
          }
        }
      ]
    },
    {
      "path": "/utils",
      "meta": {
        "title": "Utils",
        "icon": "zvpfont icon-tools"
      },
      "children": [
        {
          "path": "nextpage",
          "name": "NextPage",
          "component": "Utils/NextPage/index",
          "meta": {
            "title": "NextPage",
            "icon": "zvpfont icon-page"
          }
        },
        {
          "path": "contextmenu",
          "name": "Contextmenu",
          "component": "Utils/Contextmenu/index",
          "meta": {
            "title": "Contextmenu",
            "icon": "zvpfont icon-menu3caidan3"
          }
        }
      ]
    }
  ]
}

```
如果需要配置角色和权限, 我们可以在访问路由接口的时候将用户id或者用户所在的角色传回后端,后端过滤出可供访问的路由数据返回给前端即可. 前端会根据数据(例如上面的栗子)来重构成```vue-router```可访问的路由表信息.

