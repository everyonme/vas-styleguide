# Vasteam style guide -v0.1.0

编码:  `utf-8`

缩进:  `2空格`

首选HTML引擎 ： [jade](http://jade-lang.com)

首选CSS预处理器： [compass with prepros](http://alphapixels.com/prepros/)

> 之所以用 compass 是因为目前[stylus](http://learnboost.github.io/stylus/) 还没有对sprite支持比较好的插件；

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


##基础流程

1、配置开发环境

环境依赖：  
安装 [nodejs](http://nodejs.org/) 

安装 [prepros](http://alphapixels.com/prepros/)

安装  [vastl](https://github.com/everyonme/vastl) (vasteam 定制工具包）
命令行
	npm i -g vastl
	

2、开始生产

进入开发目录，根据[工程结构](#工程结构)建好目录
命令行
	vastl init --usecompass

然后会发现工程目录里多了 ， project.js 和 config.rb 两个配置文件。

打开 project.js 好好配置一下，非常简单。

常用就几个命令
```
	#生成离线包 -> ./offline/offline.zip
	vastl zip
	
	#CSS 根据配置自动加前缀 如:  transform ->  -webkit-transform
	vastl prefix
	
	#copy，根据配置复制文件  src/ -> dist/
	vastl copy
	
	#clean，清洁工作，删除一些临时文件
	vastl clean
	
	
```
