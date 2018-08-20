# 前端框架问题

## **单页面应用路由实现原理**

#### 为什么需要路由系统

用户在使用过程中，url 不会发生变化，那么用户在进行多次跳转之后，如果一不小心刷新了页面，又会回到最开始的状态，用户体验极差。 由于缺乏路由，不利于 SEO，搜索引擎进行收录。

#### Hash 软路由 

url 上的 hash 以 \# 开头，原本是为了作为锚点，方便用户在文章导航到相应的位置。因为 hash 值的改变不会引起页面的刷新，程序员就想到用 hash 值来做单页面应用的路由，并且当 url 的 hash 发生变化的时候，可以触发相应 hashchange 回调函数。但是它虽然解决解决单页面应用路由控制的问题，但是在 url 却引入 \# 号，不够美观

#### History 路由

History 路由是基于 HTML5 规范，在 HTML5 规范中提供了 history.pushState \|\| history.replaceState 来进行路由控制。

当你执行 **history.pushState\({}, null, '/about'\)** 时候，页面 url 会从 [http://xxxx/](http://xxxx/) 跳转到 [http://xxxx/about](http://xxxx/about) 可以在改变 url 的同时，并不会刷新页面。

#### angular Route UI-router

原生的angular  routeProvider无法实现深层嵌套

UI-Router提供了一种很好的机制，可以实现深层次嵌套

```markup
<div class="container">
    <div ui-view="topbar"></div>
    <div ui-view="main"></div>
</div>
```

## **AngularJs 理解digest loop**

所有在UI的元素都会绑定到$scope对象中，$watch会绑定到$watch list中，$watch list会在$digest 循环中被循行

只有当UI事件，ajax请求或者 timeout 延迟事件，才会触发脏检查。

 脏检查就是调用一次 $apply\(\) 或者 $digest\(\),将数据中最新的值呈现在界面上  


angular不会直接去call $digest\(\) 而是用 $scope.$apply\(\)去触发$digest\(\)

## AngularJS 改善性能的方法

1. 减少使用Lodash, ES6有很多方法已经实现了lodash提供的方法
2. 减少import 全部libaray 
3. **尽量减少观察者**
4. **ng-if比ng-show更佳**
5. 尽量减少使用{{}}, 使用ng-bind，
6. This ng-bind is a directive and will place a watcher on the passed variable. So the ng-bind will only apply, when the passed value does actually change.

   The brackets on the other hand will be dirty checked and refreshed in every $digest, even if it's not necessary.

## Angular Service和Fatory的差异

Factory还是Service都是单例的。

Service只是一个function，在应用中充当了业务层的角色，注意他仅仅是一个function，当你想将封装的功能暴露给其他模块使用时，就可以使用Service暴露方法作为公共API使用

 实际上Factory的功能包含了Service的功能，即Factory要更加灵活和，**Factory可以返回任何东西**，返回Object字面量只是最通常的情形，对特定需求来说，开发者可以返回函数、函数闭包，甚至只返回字符串这种简单数据类型的数据，具体如何操作，要根据需求而定。

比如再Factory中声明构造函数，之后再 controller中直接调用



