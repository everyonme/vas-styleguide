# Vasteam style guide -v0.1.0

编码:  `utf-8`

缩进:  `2空格`

首选HTML引擎 ： [jade](http://jade-lang.com)

首选CSS预处理器： [compass with prepros](http://alphapixels.com/prepros/)

> 之所以用 compass 是因为目前stylus还没有对sprite支持比较好的插件；

> 后续可以考虑为 stylus 开发一个sprite插件；
	
    
##工程结构

注意： 都以文件类型命名文件夹
```
project/

	#开发目录
	src/ 
    	img
        sass
        jade
        
    #发布目录
	dist/
    	img
        css
        html
        
    #离线包
	offline
    	offline.zip
        
    #工程配置
	project.js 
    
```

