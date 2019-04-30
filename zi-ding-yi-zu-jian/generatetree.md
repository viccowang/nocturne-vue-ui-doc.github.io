## GenerateTree

---

#### 描述

这其实不是一个独立组件,而是一个符合目前通用结构的树形数据转换工具.将我们一般后端返回的树形的JSON数据转换为符合ElementUI的数据格式.,工具位置放置在: ```utils/generateTree.js```


#### 使用方法

我们原始返回的数据格式一般是这样:

```js
data: [
    {
        pId: '',
        id: '1',
        title: 'tree node',
        icon: '',
    },
    {
        pId: '1',
        id: '2',
        title: 'tree node 2',
        icon: ''
    },
    {
        pId:'2',
        id:'3',
        title: 'tree node 3',
        icon: ''
    }
]

```
以上是原始数据, 通过该工具将能转化为带层级结构的树形数据对象:

```js
data: [
    {
        pId: '',
        id: '1',
        title: 'tree node',
        icon: '',
        children: [
            {
                pId: '1',
                id: '2',
                title: 'tree node 2',
                icon: '',
                children: [
                    {
                        pId:'2',
                        id:'3',
                        title: 'tree node 3',
                        icon: ''
                    }
                ]
            }
        ]
    }
]

```

__这样我们就可以将1维数据对象转化为带层级结构的数据对象了.可以直接在ElementUI中使用Tree组件__

