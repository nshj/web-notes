# Vue的compiler模式和runtime模式

使用webpack构建工具是引入Vue，在对入口文件进行挂在模板时，报错如下：

```
[Vue warn]: You are using the runtime-only build of Vue where the template compiler is not available. Either pre-compile the templates into render functions, or use the compiler-included build.
```

main.js代码如下：

```javascript
import Vue from 'vue';
new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue'
  }
})
```

## 出错原因

vue有两种代码形式，vue模块的package.json的main字段默认为runtime模式， 指向了"dist/vue.runtime.common.js"位置，而在main.js文件中，初始化vue使用的是compiler模式，所以就会出现上面的错误信息

* runtime-only代码中不可以有任何的template
* runtime-compiler可以有template，因为有compiler可以用于编译template 

## 解决办法

1. webpack配置文件里有个别名配置,也就是说，`import Vue from ‘vue’ `这行代码被解析为` import Vue from ‘vue/dist/vue.esm.js’`，直接指定了文件的位置，没有使用main字段默认的文件位置

   ``` javascript
   resolve: {
       alias: {
           'vue$': 'vue/dist/vue.esm.js' //内部为正则表达式  vue结尾的
       }
   }
   ```

2. 在引用vue时，直接写成如下即可

   ``` javascript
   import Vue from 'vue/dist/vue.esm.js'
   ```



参考：

1. [Vue的compiler模式和runtime模式](https://juejin.im/post/6844903920020488200)
2. [Runtime-Compiler和Runtime-Only的区别](https://juejin.im/post/6844904001788444686)