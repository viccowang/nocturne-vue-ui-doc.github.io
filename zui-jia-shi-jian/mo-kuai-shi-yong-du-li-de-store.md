## 在模块中使用独立的Store来管理状态
---

在项目开发当中,有时候会涉及很多大型模块, 这些模块中如果所有状态数据都存放在各个独立组件中管理的话,不论是相互传值还是共享数据都会显得非常麻烦,如果组件中的层级多,那更是噩梦,这时我们就需要能动态的在平台的状态管理中注册和卸载store的能力.
这样的好处是:
- 随时用随时创建
- 组件销毁时可以同步销毁状态,不留垃圾
- 如果需要保留组件状态,不销毁即可

#### 第一步,我们首先按照Vuex的规范创建一个store
```js
// 这是一个首页组件的例子
const Dashborad = {
  namespaced: true,
  state: {
    map: {}
  },
  mutations: {
    SET_MAP_STATE (state, mapParams) {
      state.map = Object.assign({}, state.map, mapParams)
    },
    GET_MAP_STATE (state) {
      return state.map
    }
  },

  actions: {
    setMapState ({ commit }, payload) {
      commit('SET_MAP_STATE', payload)
    },
    getMapState ({ commit }, payload) {
      commit('GET_MAP_STATE')
    }
  }
}

export default Dashborad
```

#### 第二步,创建安装store的方法
我们首先创建一个安装和卸载局部store的文件,该文件会导出两个方法```install```用来注册store以及```uninstall```用于卸载store.
```js

import store from '@/plugins/store'
import Dashboard from './store'

export default {
  install () {
    store.registerModule('Dashboard', Dashboard)
  },
  uninstall () {
    store.unregisterModule('Dashboard')
  }
}

```
#### 第三步, 在根组件中注册和卸载store
```js
// Dashboard store
import DashboardStore from './Store'

export default {
  ...
   beforeCreate () {
    // 动态注册 store
    DashboardStore.install()
  },
  beforeDestroy () {
    // 动态销毁 store
    DashboardStore.uninstall()
  },
  ...
}
```

#### 最后, 既可以在组件中使用该store了

```js
...
itemResize (item) {
  this.$store.dispatch('Dashboard/setOperateItem', item)
},
...

```

以上即可在创建```Dashboard```模块时自动创建```store```了.
