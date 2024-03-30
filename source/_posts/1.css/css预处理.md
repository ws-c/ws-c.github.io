---
title: css-预处理
tags: [css]
categories: [css]
---
# less

**Less(CSS预处理器)**:扩充CSS语言，使CSS具备一定的逻辑性和计算能力

 	表达式存在多种计算单位以第一个单位为准

​		less计算除法正确方式： **(10 / 37.5rem)**

## 导入

~~~less
@import 'xxx.less';//放在第一行
~~~

## 导出

~~~less
// out: ../css/

// out: false 
//禁止导出
~~~



## **less允许嵌套**

~~~less
.box{
	a{
		&:hover {
            //& = 当前选择器 a
		}
	}
}
~~~



## less声明变量

适用于页面出现次数比较多的适合使用

~~~less
@color:red;
.box{
    color:@color;
}
~~~





# scss

sass和scss是一个东西，sass是老版本

1. 后缀名：SASS（**S**yntactically **A**wesome **S**tyle**S**heets）版本3.0之前的后缀名为.sass，而版本3.0之后的后缀名.scss

2. 语法规范：

   ​	sass没有`{}`和`;`, 有严格的缩进规范 ; 

   ​    scss和css的缩进规范是一致的

我们在实际开发过程中，scss是常用写法



## 定义变量

$标识变量

~~~scss
$primary-color: #f90;
div {
    color: $primary-color;
}
~~~

同样支持嵌套语法



## &父选择器

假如你想针对某个特定子元素 进行设置

~~~scss
$highlight-color: #f90;
$basic-border: 1px solid black;

#app{
  background-color:  $highlight-color;
  border:$basic-border;
  .container{
    font-size:30px;
  }
  a{
    color:blue;
    &:hover{
      color: red;
    }
  }
}
~~~



## 模块

 `@import './xxxx.scss';`



## 混合指令

声明：@mixin ，引入：@include

~~~scss
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
} 
~~~

~~~scss
.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
} 
~~~



