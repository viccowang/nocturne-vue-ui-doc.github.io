## VSCode的配置指南
---
如果你使用了VSCode作为IDE,那么可以尝试将一下内容负值到你的```用户设置```中.以保证我们所有人开发出的代码格式相同.

> **[warning] 安装必要的依赖 **
>
> 使用以下配置请先安装 **ESLint**, **jshint**

```json
// VScode 用户设置

{
    "jshint.options": {
        "esversion": 6,
        "asi": true     //允许省略分号
    },

    "eslint.validate": [
        "javascript",
        "javascriptreact",
        {
            "language": "html",
            "autoFix": true
        },
        {
            "language": "vue",
            "autoFix": true
        }
    ],
    "eslint.autoFixOnSave": true,
}
```