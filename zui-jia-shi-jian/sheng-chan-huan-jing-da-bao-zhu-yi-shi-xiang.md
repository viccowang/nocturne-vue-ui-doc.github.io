## 生产环境的注意事项

> 通过目前项目在生产环境中的应用.总结除了一些特殊的注意点和技巧:

---

### ~~生成环境与开发环境目录结构不同:~~

#### 产生原因
~~因为Vue在自动构建目录时会使用绝对路径,但有时候我们生产环境部署的目录并非根目录,有时层级会比较深.这时,由于绝对路径的问题,会导致首页所有文件无法加载到而产生404问题.~~

#### 解决办法
修改配置文件``` config / index.js ```中的```assetsPublicPath```修改为空,去掉反斜杠 :
```javascript
module.export = {
    admin: {
        dev: {
            ...
        },
        build: {
            ...
             // 修改这里
             assetsPublicPath: '',
        }
}
```
---

### 静态资源(图片,字体)路径错误导致引入失败的问题:

#### 产生原因
Vue项目有两个地方可以存放静态资源, 一个是```src```目录下的```assets```,另一个是根目录的```static```.
二者的最重要区别是:
- assets内的资源会被当成组件引入而转换,比如图片,会被转为BASE64.
- static内的资源仅仅会在打包的时候原封不动的复制进生成环境的static目录下.不做任何操作.

我们一般会在两个地方使用静态资源, 一个是```template```模板中, 好似这样:
```html
    ...
    <img src="@/assets/someImg.jpg" />
    ...
```
这样是没有问题的.因为其会转换为BASE64直接插入进HTML中.而在```style```中引入的则不会进行转换
```css
    .foo {
        background: url('@/assets/someImg.png') 100% no-repeat;
    }
```
遇到这样的情况,我们的图片路径在打包完成后会出现招不到图片的问题.

#### 解决办法:
因为Vue打包完成的目录结构中,```js/css```文件与```static```目录的层级差了2级,因此我们可以修改配置文件:```build / utils ```:
```javascript
...
 return ExtractTextPlugin.extract({
    use: loaders,
    fallback: 'vue-style-loader',
    // 添加该路径
    publicPath: '../../'
  })
...  
```
这样,我们在打包后,所有的样式表中的静态资源都会自动加上这两级**相对路径**.