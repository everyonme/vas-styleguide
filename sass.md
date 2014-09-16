#  global style  全局样式维护指南（sass）

指南的目的在于开发舒适度与规则取得平衡

## 命名空间

有几种对象需要命名空间：

- 类 class
- 变量
- 函数 mixin
- 动画 animation

### 1、类 class
以单字母前缀作为类的命名空间。
目前规定如下：

 前缀| 含义 | 备注  
-----|------|-------
 .i- | 图标 | `.i-vip`
 .b- | 按钮 | `.b-primary`
 .a- | 动画 | `.a-bounce` 
 .m- | 模块 | 模块是指 图标、按钮以外的所有模块
 
 
 模块举例

 模块名     | 含义   
------------|---------
 .m-modal   | 对话框
 .m-popover | 提示浮层
 .m-tootip  | 工具提示


### 2、变量

统一以`_模块名` 作为命名空间,结合驼峰使用 如 `_iconSprite`

例子：
```
$_iconSprite:sprite-map("sp_ico/*.png");
```
### 3、Mixin 函数

统一以`_模块名` 作为命名空间,结合驼峰使用 如 `_iconSprite(){}`

例子：
```sass
@mixin _iconSprite($fileName){
  background:sprite-url($_iconSprite) no-repeat 0 round(nth(sprite-position($_iconSprite, $fileName), 2))/2;
  background-size:image-width(sprite-path($_iconSprite))/2 auto;
  width:image-width(sprite-file($_iconSprite, $fileName))/2;
  height:image-height(sprite-file($_iconSprite, $fileName))/2;
}
```


### 4、动画 keyframes

统一以`_动画名` 作为命名空间,结合驼峰使用 如 `_bounceIn()`

例子：
```sass
@keyframes _bounce {
  0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
  40% {transform: translateY(-30px);}
  60% {transform: translateY(-15px);}
}
```



## 模块构成
这里模块分为两种类型：实体模块、动画模块；


###实体模块

通常一个模块包含：
- 模块变
- 模块函数`mixin`
- 原型
- 实例

以 icon 模块为例

``` sass
// 模块中用到的变量
$_iconSp:sprite-map("sp_ico/*.png");
```

// 模块中用到的mixin
@mixin _iconSp($fileName){
  background:sprite-url($_iconSp) no-repeat 0 round(nth(sprite-position($_iconSp, $fileName), 2))/2;
  background-size:image-width(sprite-path($_iconSp))/2 auto;
  width:image-width(sprite-file($_iconSp, $fileName))/2;
  height:image-height(sprite-file($_iconSp, $fileName))/2;
}

// 原型类 (下划线前缀表明这是一个“原型类”)
// 它包含此类模块的基础结构与属性信息
// 它的作用是用来生成实例
._i {
  display: inline-block;
}

// 图标实例
.i-new{
  // 继承 ._i
  @extend ._i; 
  @include _iconSp(new);
  position: absolute;
  top:0;
  left:0;
}


###动画模块

####一个动画模块应该包含
- @keframes
- @mixin
- 调用类

- 默认参数值（也可以是全局公用）

@keframes
```sass
@keyframes _bounce {
  0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
  40% {transform: translateY(-30px);}
  60% {transform: translateY(-15px);}
}
```

@mixin
```sass
@mixin _bounce($duration, $delay, $function, $fill, $visibility) {
  animation-name:bounce;
  duration:$duration;
  delay:$delay;
  function:$function;
  fill-mode:$fill;
  visibility:$visibility;
}
```

@调用类
```sass
.a-bounce {
  @include _bounce($duration, $delay, $function, $fill, $visibility);
}
```

@默认参数值
```sass
$duration: 1s;
$delay: .2s;
$function: ease;
$fill: both;
$visibility: hidden;
```
