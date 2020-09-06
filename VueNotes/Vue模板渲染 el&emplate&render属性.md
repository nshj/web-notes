# 模板渲染 el、emplate、render属性

Vue有三个属性和模板有关，官网上是这样解释的:

el：提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标

template：一个字符串模板作为 Vue 实例的标识使用。模板将会 替换 挂载的元素。挂载元素的内容都将被忽略，除非模板的内容有分发插槽。

render：字符串模板的代替方案，允许你发挥 JavaScript 最大的编程能力。该渲染函数接收一个 `createElement` 方法作为第一个参数用来创建 `VNode`。