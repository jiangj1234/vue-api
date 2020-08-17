vue api总结

数据相关
Vue.set 向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，而且触发试图更新。
Vue.set(target, propertyName/index, value)
Vue.delete 删除对象的属性，如果对象是响应式的，确保删除能触发更新视图。
Vue.delete(target, propertyName/index)

事件相关
vm.$on 监听当前实例上的自定义事件。事件可以由vm.$emit触发。回调函数会接收所有传入事件触发函数的额外参数。
vm.$on('test', function(msg) {
    console.log(msg)
})
vm.$emit 触发当前实例上的事件。附加参数都会传给监听器回调
vm.$emit('test', 'hi')

事件总线
通过再Vue原型上添加一个Vue实例作为事件总线，实现组件间相互通信，而且不受组件间关系的影响。
Vue.prototype.$bus = new Vue();
这样做可以再任意组件间使用this.$bus访问到该Vue实例

vm.$once
监听一个自定义事件，但是只触发一次。一旦触发之后，监听器就会被移除。
vm.$on('test', function(msg){console.log(msg)})

vm.$off
移除自定义事件监听器
如果没有提供参数，则移除所有的事件监听器
如果只是提供了事件，则移除该事件所有的监听器
如果同时提供了事件和回调，则只移除这个回调的监听器。
vm.$off() // 移除所有的事件监听器
vm.$off('test') // 移除该事件所有的监听器
vm.$off('test', callback) // 只移除这个回调的监听器

组件和元素引用

ref和vm.$refs
ref 被用来给元素或子组件注册引用信息。引用信息将会注册再父组件的$refs对象上。如果在普通的DOM元素上使用，引用指向的是DOM元素；
如果用在子组件上，引用就指向组件。

ref 是作为渲染结果被创建的，在初始渲染时不能访问他们
$refs 不是响应式的，不能试图用它在模板中做数据绑定
当v-for用于元素或组件时，引用信息将是包含DOM节点或组件实例的数组。h'h'h
