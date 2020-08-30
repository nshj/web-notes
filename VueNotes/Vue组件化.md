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

## 父子组件的访问

* 父子组件的访问方式： $children 是一个数组类型 包含所有子组件对象
* 父子组件的访问方式： $refs 首先通过ref给某一个子组件绑定一个特定的ID通过this.$refs.ID就可以访问到该组件
* 子组件中直接访问父组件，可以通过$parent ，不建议使用，耦合度太高

## slot插槽

```javascript
Vue.component('alert-box', {
  template: `
    <div class="demo-alert-box">
      <strong>Error!</strong>
      <slot></slot>
    </div>
  `
})
```

```html
<alert-box>
	<p>
    组件中的标签会把slot替换掉
  </p>
</alert-box>
```



`<slot></slot>`如果组间内没有指定具名slot，会替换默认不带name属性的slot；

### 具名插槽

`<slot>` 元素有一个特殊的 attribute：`name`，一个不带 `name` 的 `<slot>` 出口会带有隐含的名字“default”；

在向具名插槽提供内容的时候，我们可以在一个 `<template>` 元素上使用 `v-slot` 指令，并以 `v-slot` 的参数的形式提供其名称，`v-slot` 只能添加在 `<template>` 上（一种例外情况：当被提供的内容*只有*默认插槽时，组件的标签才可以被当作插槽的模板来使用）

```html
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>
 </base-layout>
```

```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
</div>
```

### 作用域插槽

子组件模板插槽里的动态数据，作用域在子组件，父组件如果替换了插槽的内容还想用子组件的数据是不行的，作用域不同。

父组件替换子组件的slot，还想拿到子组件的数据，以下方法传出子组件的数据：

* 子组件使用`v-bind : key="子data属性"`动态绑定子组件的data属性
* 父组件通过`v-slot : slotname = "datakeys"`的方式赋值给`datakeys`
* 最后通过`{{ datakeys.key}}`的方式获取数据  

### 具名插槽的缩写

跟 `v-on` 和 `v-bind` 一样，`v-slot` 也有缩写，即把参数之前的所有内容 (`v-slot:`) 替换为字符 `#`。例如 `v-slot:header` 可以被重写为 `#header`