## 使用async/await处理Promise异步函数
---
我们的目的是为了使代码更加容易阅读调试，并且更加健壮。在Promise中，我们通常会使用```.then()```来处理异步，在这里，我们推荐使用```async/await```配合框架的promise公共包装函数来处理。

例子：
```javascript

// 我们之前处理时会因为回调引起更多的嵌套，导致非常难以阅读，也不容易维护。
function getMenuList () {
    this.$api['menu.list'](param).then(res => {
        //处理异步
        if(res) {
            // 调用另一个方法
            this.$api['menu.subList']().then(res => {
                //处理得到结果
                if(res) {
                    this.subList = res.list
                }
            }).catch(err) { }
        }
    }).catch (error) {
       console.log(error)
    }
}


// 我们使用async/await来处理异步, 因为await不处理异常情况，所以我们需要通过try...catch方式来处理异常。
// 但是这样的话，感觉仍然非常凌乱。
async function getMenuList () {
    try {
        const list = await this.$api['menu.list'](param)
        if(list){
            try {
                const subList = await this.$api['menu.subList']()
                if(subList) {
                    this.subList = subList.list
                }
            } catch (err) {
            
            }
        }
    } catch (err) {
    }
}


// 配合Promise公共包装函数$to，使得代码不需要嵌套很多层，看上去更加简洁，也更加容易阅读。
async function getMenuList () {
    const [err, list] = await this.$to( this.$api['menu.list'](param) )
    if(err) { }
    if(list) {
        const [err, subList] = await this.$to( this.$api['menu.subList']() )
        if(err) { }
        if(subList) {
            this.subList = subList.list
        }
    }
}

```

> 通过以上方式我们可以看到，通过ES7的语法加上包装函数，我们可以得到简单明了的代码格式。处理异步逻辑时更加像同步的方式。