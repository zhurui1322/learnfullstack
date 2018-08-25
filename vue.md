# Vue

## 单项绑定

所有数据只有一份

一旦数据变化，就去更新页面\(只有data--&gt;DOM，没有DOM--&gt;data\)

```text
<div id="app">    
    {{ message }}       // 单向绑定</div>

var app = new Vue({     
    el: '#app',        // 指定再什么地方用 div class    
    data: {        
        message: 'Hello Vue!'    
    }
});
```

## 双向绑定

使用v-model指令，实现视图和数据的双向绑定。

所谓双向绑定，指的是vue实例中的data与其渲染的DOM元素的内容保持一致，无论谁被改变，另一方会相应的更新为相同的数据。这是通过设置属性访问器实现的。

v-model主要用在表单的input输入框，完成视图和数据的双向绑定。

v-model只能用在&lt;input&gt;、&lt;select&gt;、&lt;textarea&gt;这些表单元素上。

```javascript
//v-model 实现双向绑定
<div id="app">
    <p>{{ message }}</p>
    <input v-model="message">
</div>
```

### [条件与循环](https://cn.vuejs.org/v2/guide/#%E6%9D%A1%E4%BB%B6%E4%B8%8E%E5%BE%AA%E7%8E%AF) {#条件与循环}

```text
<div id="app">
    <span v-if="seen">Now you see me</span>
</div>

var app = new Vue({
    el: '#app',
    data: {
        seen: true
    }
)};

<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>

var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```

## 处理用户输入

为了让用户和你的应用进行交互，我们可以用 `v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：

```javascript
//v-on 可以addEventListener
//添加click event 会触发reverseMessage function
<div id="app">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">Reverse Message</button>
</div>

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})

```

## 组件化应用构建

```javascript
// Vue component 

<todo-item
    v-for="item in groceryList"
    v-bind:todo="item"
    v-bind:key="item.id">
 </todo-item>

Vue.component('todo-item', {
    props: ['todo'],
    template: '<li>{{ todo.text }}</li>'
})

var app = new Vue({
    el: '#app',
    data: {
      groceryList: [
        { id: 0, text: 'Vegetables' },
        { id: 1, text: 'Cheese' },
        { id: 2, text: 'Whatever else humans are supposed to eat' }
      ]
    }
})

```



## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## 

## Vue vs React 

### 运行时性能

#### 相同点

* 使用 Virtual DOM
* 提供了响应式 \(Reactive\) 和组件化 \(Composable\) 的视图组件。
* 将注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库。

#### 不同点

在 React 应用中，当某个组件的状态发生变化时，它会以该组件为根，重新渲染整个组件子树。如要避免不必要的子组件的重渲染，你需要在所有可能的地方使用 `PureComponent`，或是手动实现 `shouldComponentUpdate` 方法

在 Vue 应用中，组件的依赖是在渲染过程中自动追踪的，所以系统能精确知晓哪个组件确实需要被重渲染。你可以理解为每一个组件都已经自动获得了 `shouldComponentUpdate`，并且没有上述的子树问题限制。

### HTML

使用 JSX 的渲染函数有下面这些优势：

* 你可以使用完整的编程语言 JavaScript 功能来构建你的视图页面。比如你可以使用临时变量、JS 自带的流程控制、以及直接引用当前 JS 作用域中的值等等。
* 开发工具对 JSX 的支持相比于现有可用的其他 Vue 模板还是比较先进的 \(比如，linting、类型检查、编辑器的自动完成\)。

使用VUE模板 HTML

* 对于很多习惯了 HTML 的开发者来说，模板比起 JSX 读写起来更自然。这里当然有主观偏好的成分，但如果这种区别会导致开发效率的提升，那么它就有客观的价值存在。
* 基于 HTML 的模板使得将已有的应用逐步迁移到 Vue 更为容易。
* 这也使得设计师和新人开发者更容易理解和参与到项目中。
* 你甚至可以使用其他模板预处理器，比如 Pug 来书写 Vue 的模板。

### CSS

CSS 作用域在 React 中是通过 CSS-in-JS 的方案实现的 \(比如 [styled-components](https://github.com/styled-components/styled-components)、[glamorous](https://github.com/paypal/glamorous) 和 [emotion](https://github.com/emotion-js/emotion)\)。这引入了一个新的面向组件的样式范例，它和普通的 CSS 撰写过程是有区别的。

 Vue 设置样式的默认方法是[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)里类似 `style` 的标签

```css
<style scoped>
  @media (min-width: 250px) {
    .list-container:hover {
      background: orange;
    }
  }
</style>
```

## VUE vs Angular1.X

 在 API 与设计两方面上 Vue.js 都比 AngularJS 简单得多，因此你可以快速地掌握它的全部特性并投入开发。

 Vue.js 是一个更加灵活开放的解决方案。它允许你以希望的方式组织应用程序，而不是在任何时候都必须遵循 AngularJS 制定的规则，这让 Vue 能适用于各种项目。我们知道把决定权交给你是非常必要的。

 AngularJS 使用双向绑定，Vue 在不同组件间强制使用单向数据流。这使应用中的数据流更加清晰易懂。

Vue 有更好的性能，并且非常非常容易优化，因为它不使用脏检查。

在 AngularJS 中，当 watcher 越来越多时会变得越来越慢，因为作用域内的每一次变化，所有 watcher 都要重新计算。并且，如果一些 watcher 触发另一个更新，脏检查循环 \(digest cycle\) 可能要运行多次。AngularJS 用户常常要使用深奥的技术，以解决脏检查循环的问题。有时没有简单的办法来优化有大量 watcher 的作用域。

Vue 则根本没有这个问题，因为它使用基于依赖追踪的观察系统并且异步队列更新，所有的数据变化都是独立触发，除非它们之间有明确的依赖关系。

有意思的是，Angular 和 Vue 用相似的设计解决了一些 AngularJS 中存在的问题。

