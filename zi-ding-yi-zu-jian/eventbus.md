## EventBus

---

#### 描述

eventBus其实就是一个空白的Vue实例,用于和其他完全不相关的组件进行数据交互时传递数据.
它被注册在全局window对象上.
```js
window.$GLOBAL.$eventbus
```

> **[warning] 手动注销监听事件 **
>
> 一定要在接收参数的组件中手动使用**vm.$off**方式注销掉监听器.因为Vue在注销实例时是不会注销监听器的事件的.(vue 2.x版本遗留问题)

#### 演示

```js
// 在某个组件中传递参数
<script>
export default {
    name:'DemoComponent',
    data () { },
    methods: {
        passValue () {
            const params = { name: 'Hello world!' }
            window.$GLOBAL.$eventbus.$emit('passValue', params)
        }
    }
}
</script>

// 紧接着在另外一个组件中接收参数
<script>
export default {
    name:'AnotherComponent',
    data () { },
    mounted () {
        window.$GLOBAL.$eventbus.$on('passValue', (value) => {
            console.log(value)
        })
    },
    // 必须手动注销监听器事件
    beforeDestroy () {
        window.$GLOBAL.$eventbus.$off('passValue')
    }
}
</script>
```



