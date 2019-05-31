## 组件的定义
---
我们在定义组件时,为了保证统一性与良好的可阅读性,势必需要遵循一定的定义顺序. 虽然Vue在组件的定义上没有任何强制要求.但我们为了所有前端团队中成员在相互阅读代码时的便利性上考虑,还是需要定义些规则.

> **[warning] 关于name与props **
>
> 组件的名称首字母必须为**大写**开头.
>
> 我们应该在定义Props时**强制使用类型验证**模式,以避免出现运行时的错误.
> 



#### 普通Vue组件

```js
import BarComponent from './BarComponent'
export default {
    name: 'FooComponent',
    props: {
        name: {
            type: String,
            required: true
        },
        age: {
            type: Number,
            default: false
        }
    },
    data () {
        tableList: []
    },
    mounted () {},
    watch () {
        age (newVal) {
            console.log(newVal)
        }
    }
    methods: {
         create (){
             
         }   
    },
    components : { BarComponent }
}
```

#### 函数式组件

我们在某些情况下需要使用类似```容器组件（包装组件）```的组件，即不做任何```DOM```渲染，只是需要在真正渲染组件之前做数据处理，那这类组件```Vue```建议我们使用函数式组件来减小开销。

```js
// FooWrapperComponent不会被渲染至DOM中，也不会出现在devtool调试窗口的组件树内
export default {
    name: 'FooWrapperComponent',
    functional: true,
    render (h, context) {
        //process some data before child component rendered
        const ctxData = context.props.ctxData.filter(d => d.hasSomeProps)
        return (
            <barComponent data={ctxData}></barComponent>
        )
    }
}

```


