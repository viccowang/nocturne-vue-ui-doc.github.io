## Vue Beauti Context

---

## 功能:
- 两种创建方式，即通过当前实例创建， 也可以通过指令的方式创建
- 可自定义鼠标事件，例如click,mouseenter或者contextmenu <指令模式>
- 可自定义窗口内容，包括文本，组件，任意内容均可
- 可自定义窗口内部样式
- 集成了完美的多级右键菜单组件，可静态创建也可动态创建，支持参数传递等

## 使用:
通过 npm 指令安装:
> npm i vue-beauti-context --save

#### 通过CDN直接引用
```javascript
<script src="https://cdn.jsdelivr.net/npm/vue-beauti-context@0.1.6/dist/vue-beauti-context.umd.min.js"></script>
```

#### 在Vue单文件中引用

在需要使用的组件中加载:
```javascript
 import BeautiContext from 'vue-beauti-context'
```

接着注册组件:
```javascript
Vue.use(BeautiContext)
```

---

#### 通过实例模式创建
假设我们在模板中需要通过```click```弹出一个窗口
```html
<button @click="openTip($event)">Click me</button>
```

> 注意，我们需要这个$event

接着，我们可以：
```javascript
openTip ($event) {
  this.$beautiContext({
    event: $event,
    text: 'Hello World!'
  })
}
```
> 为什么需要 $event?
>
> 因为组件在定位弹出位置时需要当前鼠标事件的对象，也就是需要 event.target 来确定窗口展示在什么位置。

#### 通过指令模式创建
实现如实例模式的弹出窗，我们在模板中这样定义：
```html
<!-- 弹出窗 -->
<beauti-context ref="menu"> 
  Hello Wolrd! 
</beauti-context>
<!-- 绑定指令 -->
<button v-beautiContext:menu>Click me</button>
```

#### 通过指令模式创建一个右键菜单
OK，这里我们提供一套制作好的完美的多级右键菜单可供使用，只需要定义几个组件就行：
```html
<!-- 右键菜单 -->
<beauti-context ref="menu" type="contextmenu"> 
  <beauti-contextmenu>
    <beauti-contextmenu-item>New</beauti-contextmenu-item>
    <beauti-contextmenu-item divider></beauti-contextmenu-item>
    <beauti-contextmenu-item>Edit</beauti-contextmenu-item>
    <beauti-contextmenu-item>Remove</beauti-contextmenu-item>
  </beauti-contextmenu>
</beauti-context>
<!-- 绑定指令 -->
<button v-beautiContext:menu>Click me</button>
```
> 为什么实例模式没有提供右键菜单？
>
> 实例模式可以自定义嵌套Vue Component，你可以手工引入一个自己制作的右键菜单，自由度比较大，想怎么做都可以 ：P

---

## 文档:

### 实例模式选项（Options）
| 属性 | 描述 | 必须 | 默认值 |
| -- | -- | -- | -- |
| event | 传递给组件当前鼠标触发对象的event | 必须 | - |
| props | 传递给组件自定义参数数据，如果你传递了，可以配合component来获取 | 非必须 | - |
| text | 如果你只需要弹出一段文字，那就填这里 | 非必须 | - |
| component | 配置弹出窗口需要加载的组件，可以是同步组件，也可以是通过require加载的异步组件 | 非必须 | - |
| useSlot | 配置了以后将可以在组件中使用slot，当设置了该属性后，component和text会失效 | 非必须 | false |
| customStyle | 可以自定义弹出窗口的内部样式，使用对象的方式定义，该样式会直接合并到弹出窗上 | 非必须 | {} |
| show | 菜单展示的回调 | this(当前点击的菜单实例), eventTarget(触发窗口的触发对象), params(通过指令传递的参数) | - | - |
| hide | 菜单关闭的回调 | this(当前点击的菜单实例), eventTarget(触发窗口的触发对象), params(通过指令传递的参数) | - | - |

例子：
```javascript
  this.$beautiContext({
    event: $event,
    props: {
      name: 'Jack'
    },
    component: CustomComponent,
    customStyle: {
      padding: '10px'
    },
    show (instance, event, params) {
      // show hook
    },
    hide ( instance, event, params) {
      // hide hook
    }
  })
```

### 指令模式

### beauti-context 属性
| 属性 | 描述 | 必须 | 默认值 | 可选值 |
| -- | -- | -- | -- | -- |
| type | 表示鼠标触发的事件类型 | 非必须 | click | click, mouseenter, contextmenu |
| debounce | 是否使用延迟执行，如表悬停时候会使用到，是立即展示还是延迟展示 | 非必须 | true | true/false |
| debounceTime | 延迟时间，如果启用了则可以设置，单位ms | 非必须 | 300 | any time |

### beauti-context 事件
| 事件 | 描述 | 参数 |
| -- | -- | -- |
| show | 菜单展示的回调 | this(当前点击的菜单实例), eventTarget(触发窗口的触发对象), params(通过指令传递的参数) |
| hide | 菜单关闭的回调 | this(当前点击的菜单实例), eventTarget(触发窗口的触发对象), params(通过指令传递的参数) |

### beauti-context-submenu 属性
| 属性 | 描述 | 必须 | 默认值 | 可选值 |
| -- | -- | -- | -- | -- |
| label | 当前菜单的名称，设置子菜单时，当前菜单会需要名称，并且自动在右侧生成一个箭头符号 | 非必须 | - | String |


### beauti-contextmenu-item 属性
| 属性 | 描述 | 必须 | 默认值 | 可选值 |
| -- | -- | -- | -- | -- |
| divider | 分隔符 | 非必须 | true | true/false |
| disabled | 是否禁用 | 非必须 | false | true/false |

### beauti-contextmenu-item 事件
| 事件 | 描述 | 参数 |
| -- | -- | -- |
| click | 当前菜单点击事件 | this(当前点击的菜单实例), eventTarget(触发窗口的触发对象), params(通过指令传递的参数) |

例子：
```html
<beauti-context ref="menu" type="contextmenu" @beforeShow="beforeShowHandler"> 
  <beauti-contextmenu>
    <beauti-contextmenu-item @click="clickItemHandler">New</beauti-contextmenu-item>
  </beauti-contextmenu>
</beauti-context>
<button v-beautiContext:menu="item">Click me</button>
```
```javascript
clickItemHandler( menu, eventTarget, params) {
  // params === item
}
```