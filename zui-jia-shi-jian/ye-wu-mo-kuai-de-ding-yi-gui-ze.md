## 业务模块的定义规则
---

#### 普通模块定义

我们通常将业务模块定义在 ```views```目录下。通常有如下最佳实践的规则：

- 一般模块都会包含大于1个的组件，因此在模块下需要定义文件夹而不是文件；
- 文件夹一般需要包含```components```子文件夹，作为该模块的子组件存放区域；
- 一般主文件都为```index.vue```或```index.js```，这样的好处是```webpack```在解析载入路径时默认会查询该名称，因此我们在```import```时可以忽略该文件名称，使写法更简单。例如 ``` import BaseComp from './views/components/BaseComp'```;
- 子组件名称定义时，即文件名称和组件的```name```都为大写开头；
 
我们以用户管理组件为例子，首先，其目录结构应该如下：

![](/assets/组 1.png)

组件中如下定义：

```javascript
import Search from './Components/Search'
import List from './Component/List

export default {
  // 组件名称与文件名称保持一致
  name: 'UserManagement',
  components: {
    Search,
    List
  }
  ...
}
```

通过以上定义，我们就完成一个业务模块的基本定义了。

---
