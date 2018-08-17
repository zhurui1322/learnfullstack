# DOM

## DOM 中 Property 和 Attribute 的区别 

attribute（特性），是我们赋予某个事物的特质或对象。  
property（属性），是早已存在的不需要外界赋予的特质。

* property是DOM中的属性，是JavaScript里的对象；
* attribute是HTML标签上的特性，它的值只能够是字符串；

#### 创建 {#创建}

* DOM对象初始化时会在创建默认的基本property；
* 只有在HTML标签中定义的attribute才会被保存在property的**attributes**属性中；
* attribute会初始化property中的同名属性，但自定义的attribute不会出现在property中；
* attribute的值都是**字符串**；

#### 数据绑定 {#数据绑定}

* attributes的数据会同步到property上，然而property的更改不会改变attribute；
* 对于value，class这样的属性/特性，数据绑定的方向是单向的，**attribute-&gt;property**；
* 对于**id**而言，数据绑定是双向的，**attribute&lt;=&gt;property**；
* 对于disabled而言，property上的disabled为false时，attribute上的disabled必定会并存在，此时数据绑定可以认为是**双向**的；

#### 使用 {#使用}

* 可以使用DOM的setAttribute方法来同时更改attribute；
* 直接访问attributes上的值会得到一个Attr对象，而通过getAttribute方法访问则会直接得到attribute的值；
* 大多数情况（除非有浏览器兼容性问题），jQuery.attr是通过setAttribute实现，而jQuery.prop则会直接访问DOM对象的property；

