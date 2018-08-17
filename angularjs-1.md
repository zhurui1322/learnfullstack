# AngularJs 1

## 理解digest loop 

所有在UI的元素都会绑定到$scope对象中，$watch会绑定到$watch list中，$watch list会在$digest 循环中被循行

只有当UI事件，ajax请求或者 timeout 延迟事件，才会触发脏检查。

 脏检查就是调用一次 $apply\(\) 或者 $digest\(\),将数据中最新的值呈现在界面上  


angular不会直接去call $digest\(\) 而是用 $scope.$apply\(\)去触发$digest\(\)

## 改善 AngularJS 性能的方法

1. 减少使用Lodash, ES6有很多方法已经实现了lodash提供的方法
2. 减少import 全部libaray 
3. **尽量减少观察者**
4. **ng-if比ng-show更佳**
5. 尽量减少使用{{}}, 使用ng-bind，This ng-bind is a directive and will place a watcher on the passed variable. So the ng-bind will only apply, when the passed value does actually change.

   The brackets on the other hand will be dirty checked and refreshed in every $digest, even if it's not necessary.

