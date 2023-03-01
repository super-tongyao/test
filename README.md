<div align="center">

![](https://img-blog.csdnimg.cn/1842462da13147fea1c48f8c38fc6125.png)
<h3 align="center"> Wall</h3>

![Vue](https://img.shields.io/badge/Vue-3.2.13-brightgreen.svg)
![Spring Boot 2.2.6](https://img.shields.io/badge/Spring%20Boot-2.2.6-brightgreen.svg)

</div>

Wall是一款快速资源分享应用程序。基于Vue3 + Spring Boot开发的云共享资源应用系统。快速发布分享照片和视频。给爱摄影的人提供了很好的分享平台。

作者的Wall：[https://wall.ityao.cn](https://wall.ityao.cn)



- 演示Demo：[https://wall.demo.ityao.cn](https://wall.demo.ityao.cn)

- Demo后台：[https://wall.demo.ityao.cn/login](https://wall.demo.ityao.cn/login)，账号密码：admin/123456



如果这个项目让你有所收获，记得 Star 关注哦，这对我是非常不错的鼓励与支持。

## 开发者名单

Wall还有很多不足之处，比如Wall暂不支持ios系统调用相册上传图片等。

或许你可以加入Wall团队，我们一起贡献代码。[申请加入](#参与贡献)



下面表格中出现你的头像及Github账号地址，视为Wall团队成员。

| 头像                                                         | 名称    | Github                           |
| ------------------------------------------------------------ | ------- | -------------------------------- |
|| Tongyao | https://github.com/super-tongyao |
| 成员1                                                        | 成员1   | 成员1                            |
| 成员2                                                        | 成员2   | 成员2                            |

## 安装教程

### 前端安装

前端安装推荐、建议使用nginx代理。在此使用nginx做文章配置。

1、把wall文件夹放入nginx/html下，并编辑```config/nginx.conf```配置文件，新增如下配置。

```
server {
	listen       80;
	server_name  你的网站域名或公网IP;
	
	underscores_in_headers on;

	location / {
		# 映射你nginx/html目录下的wall文件夹
		root html/wall;
		try_files $uri $uri/ /index.html;
	}
	
	# 后端服务地址
	location /api{
		rewrite  ^/api/(.*)$ /$1 break;
		proxy_set_header Host $host;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		
		# 转发你Wall的后台地址
		proxy_pass   http://localhost:9999;
	}
	
	error_page   500 502 503 504  /50x.html;
	location = /50x.html {
		root   html;
	}
}
```

2、至此，重启nginx不报错，前端部署完成。

### 后端安装

1、修改config/application.yml配置文件，并修改你本地的MySQL数据库连接端口及账号密码。

```
# project prot
server:
  port: 9999

# database config
mysql:
  database: wall
  port: 3306
  ip: 127.0.0.1
  username: root
  password: root
```

2、后端支持2中环境下快捷启动，自带JDK，无需安装，直接启动。

- Windows下双击```startup.bat```文件启动。

- Linux下执行```startup.sh```文件启动，请先获取执行权限。

3、访问```http://你的网站域名或公网IP:80```正常显示页面及操作数据，至此完成安装。如有问题，请提交Issues。

## 开源代码

> Vue 源码请查看分支：[vue分支](https://github.com/super-tongyao/wall/tree/vue)

> Spring Boot 源码请查看分支：[service分支](https://github.com/super-tongyao/wall/tree/service)

## 更新日志

#### 2023－02－28（v1.0）
> 1、版本1.0上线。

## 共同协作

叙述并提交你的```480x480```个人生活照发送至邮箱：super_tongyao@163.com

让我们一起让Wall变的更好。

## 免责声明

[查看免责声明](/免责声明.md)
