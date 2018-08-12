# SCSS

## 变量 

SASS允许使用变量，所有变量以$开头。 如果变量需要镶嵌在字符串之中，就必须需要写在\#{}之中

```css
$blue : #1875e7;　

div {
    color : $blue;
}

$side : left;

.rounded {
    border-#{$side}-radius: 5px;
}
```

##  **计算功能**

```css
body {
    margin: (14px/2);
    top: 50px + 100px;
    right: $var * 10%;
}
```

## 嵌套

```css
div h1 {
    color: red;
}

did {
    h1 {
        color: red;
       }
}

/*border-color 可以携程*/

p{
    border: {
        color: red;
    }
}
/* a:hover*/
a {
    &:hover { 
        color: red;
    }
}
```

## 继承

```css
.class2 {
    @extend .class1;
    font-size: 120%;
} 
```

## Mixin

 Mixin有点像C语言的宏（macro），是可以重用的代码块。

 使用@mixin命令，定义一个代码块。

```css
@mixin left {
　　float: left;
　　margin-left: 10px;
}
```

 使用@include命令，调用这个mixin。

```css
div {
　　@include left;
}
```

 mixin的强大之处，在于可以指定参数和缺省值。

```css
@mixin left($value: 10px) {
　　　　float: left;
　　　　margin-right: $value;
}

div {
　　　@include left(20px);
}
```

##  **条件语句**

```css
@if lightness($color) > 30% {
　　　background-color: #000;
} @else {
　　　background-color: #fff;
}
```

##  **循环语句**

```css
@for $i from 1 to 10 {
　　　　.border-#{$i} {
　　　　　　border: #{$i}px solid blue;
　　　　}
}

$i: 6;

@while $i > 0 {
　　.item-#{$i} { width: 2em * $i; }
　　$i: $i - 2;
}
```

##  **自定义函数**

```css
@function double($n) {
　　　@return $n * 2;
}

#sidebar {
　　　width: double(5px);
}
```

