#  global style  全局样式维护指南（sass） 编辑中..

指南的目的在于尽可能消除维护过程中模糊的部分。
让开发变得舒适。

先从模块的构成开始

## 模块构成
以 icon 模块为例

``` scss
// icon

// 模块中用到的变量
$_i_sp:sprite-map("sp_ico/*.png");

//  模块中用到的函数
@mixin _i_resize($fileName){
  background:sprite-url($_i_sp) no-repeat 0 round(nth(sprite-position($_i_sp, $fileName), 2))/2;
  background-size:image-width(sprite-path($_i_sp))/2 auto;
  width:image-width(sprite-file($_i_sp, $fileName))/2;
  height:image-height(sprite-file($_i_sp, $fileName))/2;
}


// 原型类
// 它包含此类模块的基础结构与属性信息
// 它的作用是被
._i {
  display: inline-block;
}

//扩展类
.i-new{
  @extend ._i;
  @include _i_resize(new);
  position: absolute;
  top:0;
  left:0;
}

```





## 命名空间

命名空间包含：

-类
-函数&变量&keyframes

### 1、命名空间
以单字母前缀作为类的命名空间。

 前缀| 含义 | 备注  
-----|--------------
 .i- | 图标 | `.i-vip`
 .b- | 按钮 | `.b-primary` 
 .m- | 模块 | 模块是指 图标、按钮以外的所有模块
 
 
 模块举例

 模块名     | 含义   
------------|---------
 .m-modal   | 对话框
 .m-popover | 提示浮层
 .m-tootip  | 工具提示


### 2、函数&变量&keyframes

统一以`_`+`模块名`作为命名空间

例子：
```
// icon 模块

// _i_ 为 icon模块变量的命名空间
$_i_sp:sprite-map("sp_ico/*.png");


// _ 为命名空间
@mixin _icon($fileName){
  background:sprite-url($_i_sp) no-repeat 0 round(nth(sprite-position($_i_sp, $fileName), 2))/2;
  background-size:image-width(sprite-path($_i_sp))/2 auto;
  width:image-width(sprite-file($_i_sp, $fileName))/2;
  height:image-height(sprite-file($_i_sp, $fileName))/2;
}
```







## 模块定义 Module

### 下划线代表私有、中间件

全局mixin定义

```
  @mixin _icon(){
  }
```

模块原型

以图标icon为例
```
  ._i {
    display: inline-block;
  }
```

