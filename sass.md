#  global style  全局样式维护指南（sass）

指南的目的在于开发舒适度与规则取得平衡

包含以下内容：
- 文件结构
- 命名空间
- 模块构成


## 文件结构

```
_global
  ├─src
      ├─ img
      ├─ sass
          ├─ _reset.scss
          ├─ _mixins.scss           
          ├─ _icons.scss
          ├─ _buttons.scss         
          ├─ _modals.scss          
          ├─ _animation             
          │    ├─ _animation.scss
          │    ├─ _bounce.scss
          │    └─ ... 
          ├─ ...         
          └─global.scss 
```

## 命名空间

有几种对象需要命名空间：

- 类 className
- 变量
- 函数 mixin
- 动画关键帧 keyframes

### 1、类 class
以单字母前缀作为类的命名空间。

目前已使用命名空间：

 前缀| 含义 | 备注  
-----|------|-----------
 _   | 原型 | `._i` 
 .i- | 图标 | `.i-vip` 
 .b- | 按钮 | `.b-primary`
 .m- | 模块 | 指代除图标/按钮以外的所有模块 如 `.m-modal`
 .a- | 动画 | `.a-bounce` 
 
 
模块命名参考主流命名方式，比如目前为止影响最广的 bootstrap

 模块名     | 含义   
------------|---------
 .m-modal   | 对话框
 .m-popover | 提示浮层
 .m-tootip  | 工具提示


### 2、变量

统一以`$_模块名` 作为命名空间,结合驼峰使用 如 `$_iconSprite`

例子：
```
$_iconSprite:sprite-map("sp_ico/*.png");
```


### 3、Mixin 函数

统一以`_模块名` 作为命名空间，结合驼峰使用 如 `_iconSprite(){}`

例子：
```scss
//图标mixin
@mixin _iconSprite($fileName){
  background:sprite-url($_iconSprite) no-repeat 0 round(nth(sprite-position($_iconSprite, $fileName), 2))/2;
  background-size:image-width(sprite-path($_iconSprite))/2 auto;
  width:image-width(sprite-file($_iconSprite, $fileName))/2;
  height:image-height(sprite-file($_iconSprite, $fileName))/2;
}

//动画mixin
@mixin _bounce($duration, $delay, $function, $fill, $visibility) {
  animation-name:bounce;
  duration:$duration;
  delay:$delay;
  function:$function;
  fill-mode:$fill;
  visibility:$visibility;
}
```


### 4、动画 keyframes

统一以 `_动画名` 作为命名空间，结合驼峰使用 如 `_bounceIn{}`

例子：
```scss
@keyframes _bounceIn {
  0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
  40% {transform: translateY(-30px);}
  60% {transform: translateY(-15px);}
}
```



## 模块构成
这里模块分为两种类型：
- 实体模块
- 动画模块；


###实体模块

通常一个模块包含：
- 模块变量
- 模块函数`mixin`
- 模块原型
- 模块实例

以 icon 模块为例

模块中用到的变量
``` scss
$_iconSp:sprite-map("sp_ico/*.png");
```


模块中用到的mixin
``` scss
@mixin _iconSp($fileName){
  background:sprite-url($_iconSp) no-repeat 0 round(nth(sprite-position($_iconSp, $fileName), 2))/2;
  background-size:image-width(sprite-path($_iconSp))/2 auto;
  width:image-width(sprite-file($_iconSp, $fileName))/2;
  height:image-height(sprite-file($_iconSp, $fileName))/2;
}
```


模块的原型

它包含此类模块的基础结构与属性信息
``` scss
._i {
  display: inline-block;
}
```

// 通过继承原型得到一个实例
``` scss
.i-new{
  @extend ._i; 
  @include _iconSp(new);
  position: absolute;
  top:0;
  left:0;
}
```


###动画模块

####动画模块包含：
- @keyframes
- @mixin
- 调用类
- 默认参数值（也可以是全局公用）


@keyframes
```scss
@keyframes _bounce {
  0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
  40% {transform: translateY(-30px);}
  60% {transform: translateY(-15px);}
}
```

@mixin
```scss
@mixin _bounce($duration, $delay, $function, $fill, $visibility) {
  animation-name:bounce;
  duration:$duration;
  delay:$delay;
  function:$function;
  fill-mode:$fill;
  visibility:$visibility;
}
```


调用类
```scss
.a-bounce {
  @include _bounce($duration, $delay, $function, $fill, $visibility);
}
```

默认参数值
```scss
$_duration: 1s;
$_delay: .2s;
$_function: ease;
$_fill: both;
$_visibility: hidden;
```
