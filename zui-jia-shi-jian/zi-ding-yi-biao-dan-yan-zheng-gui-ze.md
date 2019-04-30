## 自定义表单验证规则
---

- 目前项目框使用ElementUI, 表单验证依赖于[Async-validator](https://github.com/yiminghe/async-validator)验证框架. 该验证框架支持一些通用的验证,例如Number, String, Date,, email 等等.详细可以参考他的[GitHub](https://github.com/yiminghe/async-validator)页面.
- 这里的自定义验证规则则是对其进行的规则扩展,并不对其他方面,比如方法,属性进行扩展.
- 自定义规则扩展一般在框架的 ```@/service/expands/extendValidate```目录下.
---

#### 第一步,定义正则验证规则

- 在```pattern.js```文件中,我们可以根据需要自定义规则,并导出该规则.例如:

```js
...
// 验证手机号
const cellPhone = /^1[34578]\d{9}$/

export default {
    ...
    cellPhone
}
```

#### 第二步,完成验证规则

- 在```extendVlidate.js```文件中,我们导入上面的验证规则, 然后为该规则匹配具体的验证方法,最后再导出该验证方法.

```js
/**
 * Validate cellPhone
 * @param {*} rule
 * @param {*} value
 * @param {*} callback
 */
const cellPhone = (rule, value, callback) => {
  if (value) {
    const errors = []
    if (!regPattern.cellPhone.test(value)) {
      errors.push(new Error('手机号填写有误'))
      callback(errors)
    } else {
      callback()
    }
  } else {
    callback()
  }
}

export default {
  ...
  cellPhone
}

```

#### 接着,我们即可以在ElementUI框架中使用该自定义验证规则

```js
// validate
import Validator from '@/service/expands/extendValidate/'

export deafult {
    data() {
      return {
        formRules: {
          ...
          userMobile: [
            { validator: Validator.cellPhone, trigger:'blur' }
          ]
        }
      }
    } 
}
```
- 这样, 该字段在输入不符合```cellPhone```验证规则的时候就会触发第二步定义的验证方法了.

> 更多的验证规则请参考Async-Validator, ElementUI即是在此之上进行的封装.


