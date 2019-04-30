## NextPage

---

#### 描述

Nextpage是原有产品(公司原有基于AngularJS构建的产品)中重构而来的,适用于公司业务流程的一个全局插件.
- 它可以实现在不改变路由的情况下,在模块中添加多级页面,如下图所示,并支持无限嵌套.
- 它可以在各级Nextpage页面中相互传递数据.
- 它会在新创建的页面自动创建一个面包屑breadCrumb以及一些实例方法.

> **[info] Nextpage 是全局的 **
>
> 这意味着在你所开发的组件中不需要引入任何东西,Nextpage会在每个创建的Vue实例中绑定一个 **vm.$nextPage(options)**方法

![](/assets/np.png)

#### 演示
```js
// FooComponent
<script>
// 导入一个组件
import BarComponent from './BarComponent'
export default {
    name:'FooComponent',
    data () {
    },
    methods: {
        createNp () {
            this.$nextPage({
                title: 'Create New Component',
                props: {
                    name: 'HelloWorld!'
                },
                show() {
                },
                beforeClose(nextpageInstance) {
                },
                component: BarComponent,
                cache: true
            })
        }
    }
}
</script>

// BarComponent
<script>
export default {
    name: 'BarComponent',
    props: ['name'],
    methods: {
        close () {
            // 关闭当前页面
            this.closeNextPage(this)
        }
    }
}
</script>
```
> **[warning] 注意关闭方法中的this **
>
> 通过NextPage打开的业务组件内调用```closeNextPage()```方法时,必须传递当前实例的引用```this```,如上面的例子所示

#### NextPage 属性
| 参数 | 说明 | 类型 | 可选值 | 默认 |
| :--- | :--- | :--- | :--- | :--- |
| title  | 打开页面的标题,会出现在面包屑中  | String  | -  | -  |
| props | 需要向新建页面的组件中传递的数据,和Vue一样,可以传递任何值 | Any | - | - |
| component | 需要打开的业务组件,参考上面的例子,我们要打开的是BarComponent组件页面 | VueComponent | - | - |
| cache| 是否缓存当前组件,缓存方式使用的是Vue的Keep-alive实现,因此可以缓存所有页面状态,传递参数时不能设置为false| Boolean |- | - |

#### NextPage 方法
| 方法名 | 说明 | 参数 |
| :--- | :--- | :--- |
| closeNextPage | 在打开的组件页面中使用该方法可以关闭当前组件页面 | this (必须传入当前组件实例的引用) |

#### NextPage 钩子函数
| 函数名称 | 说明 | 参数 |
| :--- | :--- | :--- |
| show | 在打开Nexpage后调用 | - |
| beforeClose | 在Nexpage关闭前调用 | nextPage实例 |



