# Repository和Mirror

## 1、Repository（仓库）

### 1.1、概要

​ repository里存放的都是各种jar包和maven插件。当向仓库请求插件或依赖的时候，会先检查local repository，如果local repository有则直接返回，否则会向remote repository请求，并缓存到local repository。也可以把做的东西放到本地仓库，仅供本地使用；或上传到远程仓库，供大家使用。

![](http://opzv089nq.bkt.clouddn.com/17-7-2/70113161.jpg)

### 1.2、 Maven仓库分类

1. remote repository：相当于公共的仓库，大家都能访问到，一般可以用URL的形式访问

2. local repository：存放在本地磁盘的一个文件夹，例如，windows上默认是C:\Users\｛用户名｝.m2\repository目录

### 1.3、远程仓库分类：

1. 中央仓库：[http://repo1.maven.org/maven2/](http://repo1.maven.org/maven2/)

2. 私服：内网自建的maven repository，其URL是一个内部网址

3. 其他公共仓库：其他可以互联网公共访问maven repository，例如 jboss repository ,jcenter repository,ali repository等

## 2、 Mirror

### 2.1、 概要

​        mirror相当于一个拦截器，它会拦截maven对remote repository的相关请求，把请求里的remote repository地址，重定向到mirror里配置的地址。

### 2.2、定义

mirror表示的是两个Repository之间的关系，在maven配置文件（setting.xml\)里配置了

&lt;mirrors&gt;

&lt;mirror&gt;



..........

&lt;

/mirror

&gt;

&lt;

/mirrors

&gt;

，即定义了两个Repository之间的镜像关系

### 2.3、目的

​ 配置两个Repository之间的镜像关系，一般是出于访问速度和下载速度考虑。

### 2.4、 注意

​ 需要注意的是，由于镜像仓库完全屏蔽了被镜像仓库，当镜像仓库不稳定或者停止服务的时候，Maven仍将无法访问被镜像仓库，因而将无法下载构件。

## 3、私服

### 3.1、 概要

私服是一种特殊的远程Maven仓库，它是架设在局域网内的仓库服务，私服一般被配置为互联网远程仓库的镜像，供局域网内的Maven用户使用。当Maven需要下载构件的时候，先向私服请求，如果私服上不存在该构件，则从外部的远程仓库下载，同时缓存在私服之上，然后为Maven下载请求提供下载服务，另外，对于自定义或第三方的jar可以从本地上传到私服，供局域网内其他maven用户使用。

### 3.2、优点

1. 节省外网宽带

2. 加速Maven构建

3. 部署第三方构件

4. 提高稳定性、增强控制：原因是外网不稳定

5. 降低中央仓库的负荷：原因是中央仓库访问量太大



