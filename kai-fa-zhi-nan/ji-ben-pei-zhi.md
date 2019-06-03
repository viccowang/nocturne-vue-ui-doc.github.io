## 基本配置
---

框架的基本配置项基本都在```config/```目录下,这里可以配置常量,以及平台基础参数.

#### 配置项目名称常量前缀
该前缀用于保存session或者cookie,以及store中可能会涉及到的临时存贮的键值.配置的位置在```config/settings.js```中，我们一般取项目英文名称加下划线即可
```js
/**
  * 全局项目名称
  */
export const PLATFORM_PERFIX_NAME = 'YOUR_PROJECT_NAME'
```

---

#### 配置开发访问地址和生产环境地址

访问目录为```config/settings.js```下面。```devBaseUrl```是指开发模式，框架会使用该地址调用接口，我们通常用一套在线模拟API接口的服务来配合使用，这样后端的开发顺序就不必和前端同步了，我们只需要使前后端相互沟通协调好API接口即可。当然，如果你是全栈，自己同时兼顾前后端也是可以的。```prodBaseUrl```是打包完成后用于生产环境的地址。

```js
/**
  * API接口默认参数配置
  */
export const API_DEFAULT_CONFIG = {
  // 开发环境对应的API访问路径
  devBaseUrl: 'http://localhost:3000',
  // 生产环境对应的API访问路径
  prodBaseUrl: 'http://100.10.10.10:8888',
  // 此处一般不必修改
  isDevMode: process.env.NODE_ENV !== 'production',
  // 开启后会打印接口访问info
  isDebug: true,
  // 接口连缀，一般情况下我们不需要修改默认情况下我们调用接口使用类似 this.$api['user.info']()，如果你修改了
  // 连接符，比如修改为/，则接口调用会变为 this.$api['user/info']()。这只是使用习惯问题。
  // user.info or user/info
  sep: '.'
}
```

> 系统在```/server/```目录集成了一个简单的mockServer，可以通过```npm run mockServer```指令来启动, 默认的端口即为3000

---

#### 配置静态或动态路由
框架提供了静态路由和动态路由两种方式。

开启静态路由后,页面路由将通过```router/```目录下定义的路由表访问页面，其中我们将框架级，即和业务没有关系的或者公用的路由放在```staticRoutes.js```中，业务模块页面的路由放在```asyncRoutes.js```中。

```js
/**
  * 路由表默认参数配置
  */
export const ROUTER_DEFAULT_CONFIG = {
  // true表示开启静态路由表
  isUseStaticeRouter: true
}
```

配置动态路由后则系统会通过内建接口来获取数据并自动生成路由表。需要将上面的值修改为```false```,并且在```service/api/platform.js```中配置```menu.list```API接口。该接口返回的数据会被框架解析为可识别的路由数据。

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
    ...
  ]
}

```
---

#### 全局主题颜色
目前全局配色定义的位置在```config/const/platform.js```中, 我们可以根据不同的喜好定义任意的主颜色（默认我们给了一组彩虹色，一般情况下足够使用，不需要再额外配色）。系统会根据所定义的颜色动态生成相关的辅助色彩.定义的方式既是参考已定义的格式（K,V）




