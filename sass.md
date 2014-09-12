#  global style  全局样式维护指南（sass） 编辑中..


## name space

约定一下几个字母为公用命名空间， 私有类名一律不准以单字母作为前缀。


 前缀 | 含义   
-----|-------
 .i_ | 图标   
 .b_ | 按钮   
 .m_ | 模块
 .m_modal | 对话框
 .m_popover | 提示浮层
 .m_tootip | 工具提示


模块定义 Module

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

