# Vue 组件化

## 注册组件的基本步骤

``` html
<div id="app">
    <!-- 3、 使用组件 -->
    <my-cpn></my-cpn>
</div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    // 1、 创建组件
    const myComponent = Vue.extend({
      // 注意 模板字符串 的用法 （ ` `里面换行 可以显示）
      template:`
        <div>
          <h3> 我是一个组件</h3>
          <p> 这都是组件里的内容</p>
        </div>`
    })
    // 2、 注册组件 并且定义组件标签的名称
    // Vue.Component()创建的是全局，即多个Vue实例都可以用
    Vue.component('my-cpn', myComponent);

    const app = new Vue({
      el: '#app',
      data : {
        message: 'Hello Vue!'
      }
    })
  </script>
```



1. 创建组件构造器
   * 调用Vue.extend()进行创建一个组件构造器
   * 通常在创建组件构造器时，传入template代表我们自定义组件的模板；注意template属性写HTML时用模板字符串
   * 该模板就是在使用到组件的地方，要显示的HTML代码
   * 此种用法不多见了，更多使用 语法糖
2. 注册组件
   * 调用Vue.component()是将刚才的组件构造器注册为一个组件（注册的为全局组件）
   * 传递两个参数：1、注册组件的标签名 2、组件构造器
3. 使用组件
   * 组件必须使用在 Vue实例里面，如代码中的在`<div id="app">`中

## 全局组件和局部组件

``` javascript
 const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue!'
      },
      components: {
        'my-cpn': myComponent
      }
    })
```

在Vue实例下，使用components属性，{ 定义组件标签名 ：组件构造器名 }，注意的定义标签名要用引号  

## 注册组件的语法糖

``` javascript
 const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue!'
      },
      // 局部组件
      components: {
        'my-cpn': {
          template:`
            <div>
              <h3> 我是一个组件</h3>
              <p> 这是组件注册语法糖</p>
            </div>`
        }
      }
    })
```

主要的省去了写调用Vue.extend()的语法，直接在Vue.component()或者Vue实例components属性里放入一个对象

## 父组件和子组件

Vue.extend()或者语法糖的形式创建组件构造器时，不但有template属性，还有components属性（其实Vue实例有的许多属性它都有），在components属性中引入子组件  

其实可以把Vue实例看作根组件  

🚩 注意：组件的构造，需要提前声明；即Vue实例用到的组件，必须在实例之前就已经声明；父组件（A）里面用到了子组件（B），如果是用Vue.extend()语法构造，那B必须在A之前声明。 如果Vue实例想直接用B组件，必须在自己的components属性里声明，不然无法直接使用。

``` javascript
<div id="app">
    <!-- 3、 使用组件 -->
    <my-cpn></my-cpn>
    <div>
      <p>用组件标签，组件里面用了子组件</p>
      <parent-cpn></parent-cpn>
    </div>
  </div>
//下面是JavaScript
    const childComponent = Vue.extend({
      template:`
        <div>
          <h3> 我是一个子组件</h3>
          <p> 父组件在构建时components属性里面有我，就用我</p>
        </div>`
    })
    const parentComponent = Vue.extend({
      template:`
        <div>
          <h3> 我是一个父组件</h3>
          <p> 这是父组件段落,下面我用子组件定义的标签</p>
          <child-cpn></child-cpn>
        </div>`,
      components: {
        'child-cpn' : childComponent
      }
    })
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue!'
      },
      components: {
        'my-cpn': {
          template:`
            <div>
              <h3> 我是一个组件</h3>
              <p> 这是组件注册语法糖</p>
            </div>`
        },
        'parent-cpn': parentComponent,
      }
    })
```

## 组件模板两种分离写法

1. `<script type="text/x-template" id="aaa"> 模板内容 </script>`  
2. `<template id="bbb"> 模板内容 </template>`

两种标签形式，一定要有id；

``` javascript
<script>
    const app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue!'
      },
      components: {
        'my-cpn': {
          template: '#bbb'
        },
      }
    })
</script>
```

## 组件数据存放

``` javascript
const parentComponent = Vue.extend({
      template:`
        <div>
          <h3> 我是一个父组件</h3>
          <p> 这是父组件段落,下面我用子组件定义的标签</p>
          <p> 这是父组件data：{{ msg }}</p>
          <child-cpn></child-cpn>
        </div>`,
      data(){
        return{
          msg: '这是父组件'
        }
      },
      components: {
        'child-cpn' : childComponent
      }
    })
```

🚩注意：组件的data必须是一个函数，返回对象；并不像Vue实例里面data是个对象，因为组件需要复用，每次返回的都是新对象的地址，如果是对象则复用时共用一个对象

组件的data用在模板里，不是`<parent-cpn> {{ msg }} </parent-cpn>`

🚩注意：Component template should contain exactly one root element.即template里面的HTML必须有一个根标签包裹着

## 父子组件的通信

详细见[Vue官方文档](https://cn.vuejs.org/v2/guide/components.html)

### [通过 Prop 向子组件传递数据](https://cn.vuejs.org/v2/guide/components.html#通过-Prop-向子组件传递数据)

``` javascript
const cpn1 = {
      template:'#cpn1',
      props: ['title'],
      data() {
        return {
          msg: '组件data的msg'
        }
      }
    }
```



子组件 设props属性，传递静态数据`<cpn1 title="abc"></cpn1>`传递动态数据需要v-bind`<cpn1 :title="message"></cpn1>`  

props的值有两种方式：

1. 字符串数组，数组中的字符串就是传递时的名称
2. 对象，对象可以设置传递时的类型，也可以设置默认值等

更多[Prop](https://cn.vuejs.org/v2/guide/components-props.html)看文档，例如html中的atrribute大小写不敏感，props中的驼峰名字在html中使用其等价的 kebab-case (短横线分隔命名) 命名

### [监听子组件事件](https://cn.vuejs.org/v2/guide/components.html#监听子组件事件)

自定义事件流程：

1. 在子组件中，通过$emit()来触发事件
2. 在父组件中，通过v-on来监听子组件事件

$emit()第一个参数为 自定义事件名，第二个可选参数为子组件抛出的值

父组件v-on来监听子组件事件，$event可以访问到这个值`v-on:enlarge-text="postFontSize += $event"`，如果这个事件处理函数是一个方法，那么这个值将会作为第一个参数传入这个方法  

```javascript
<div id="app">
    {{ message }}
    <cpn1 title="abc" @child=" message = $event"></cpn1>

  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <template id="cpn1">
    <div>
      <div>这是组件cpn1</div>
      <div> {{ msg }} <p>静态通过props向子组件传数据title:</p>{{ title }}</div>
      <button @click="$emit('child', '子组件消息')">传数据给父组件</button>
  </div>
  </template>
```



