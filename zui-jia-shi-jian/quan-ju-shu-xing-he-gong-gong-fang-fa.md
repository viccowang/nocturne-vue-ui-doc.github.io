## 全局属性和公共函数
---

为了日后开发方便，在访问一些通用的属性变量和函数时候，我们设置了全局的通用访问方式。即将公共部分绑定到了Vue原型对象上，这样我们在任何Vue组件实例中均可以访问。


#### $config

通过该属性可以访问到```config/settings.js```中的全部配置项：
```js
// 例如获取websocket配置项
...
const { WS_CONFIG } = this.$config
```

#### $const

通过该属性访问```config/const/platform.js```中的全部常量配置
```js
// 例如获取侧边栏的常量
const { shortcut } = this.$const
```

#### $api

通过该方法来调用任何定义好的接口
```js
// 例如调用menuList接口
const res = await this.$api['menu.list']()
```

#### $to

该方法是一个Promise的包装器，从而避免套用try...catch语句，使代码更简洁，阅读更容易
```js
// 例如
const [err, res] = await this.$to(this.$api['menu.list']())
if(err) throw new Error('...')
if(res) {
    // do sth.
}
```
#### $ajax

该方法是axios的另一个词法替换。 $ajax === axios 。 我们只是为了平时看上去比较熟悉罢了。使用方法请参考[axios on github](https://github.com/axios/axios)
```js
// 例如
this.$ajax({
    url: '',
    method: '',
    ...
})
```

#### $ws
该方法适用于公司关于websocket封装的业务.默认是关闭状态，如果需要使用则可以前往```config/settings.js```中进行配置

