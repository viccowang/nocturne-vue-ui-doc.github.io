## 组件的定义
---
我们在定义组件时,为了保证统一性与良好的可阅读性,势必需要遵循一定的定义顺序. 虽然Vue在组件的定义上没有任何强制要求.但我们为了所有前端团队中成员在相互阅读代码时的便利性上考虑,还是需要定义些规则.

> **[warning] 关于name与props **
>
> 我们为了保证日后兼容Class模式的定义,组件的名称首字母必须为**大写**.
>
> 我们应该在定义Props时**强制使用类型验证**模式,以避免出现运行时的错误.

```js
import BarComponent from './BarComponent'
export default {
    name: 'FooComponent',
    props: {
        name: {
            type: String,
            required: true
        },
        isStudent: {
            type: Boolean,
            default: false
        }
    },
    data () {
        tableList: []
    },
    mixins: [],
    beforeCreate () {},
    created () {},
    beforeMount () {},
    mounted () {},
    beforeUpdate () {},
    updated () {},
    activated () {},
    deactivated () {},
    beforeDestroy () {},
    destroyed () {},
    watch () {
        isStudent (newVal) {
            console.log(newVal)
        }
    }
    methods: {
         create (){
             
         }   
    },
    directives: {},
    filters: {},
    components : { BarComponent }
}
```