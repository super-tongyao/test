<div align="center">

![](https://img-blog.csdnimg.cn/1842462da13147fea1c48f8c38fc6125.png)
<h3 align="center"> Wall</h3>

![Vue](https://img.shields.io/badge/Vue-3.2.13-brightgreen.svg)
![Spring Boot 2.2.6](https://img.shields.io/badge/Spring%20Boot-2.2.6-brightgreen.svg)

</div>

Wall是一款快速资源分享应用程序。基于Vue3 + Spring Boot开发的云共享资源应用系统。快速发布分享照片和视频。给爱摄影的人提供了很好的分享平台。



演示Demo：[https://wall.demo.ityao.cn](https://wall.demo.ityao.cn)

Demo后台：[https://wall.demo.ityao.cn/login](https://wall.demo.ityao.cn/login)，账号密码：admin/123456

作者的Wall：[https://wall.ityao.cn](https://wall.ityao.cn)



如果这个项目让你有所收获，记得 Star 关注哦，这对我是非常不错的鼓励与支持。

## 开发者名单

Wall还有很多不足之处，比如Wall暂不支持ios系统调用相册上传图片等。

或许你可以加入Wall团队，我们一起贡献代码。[申请加入](#参与贡献)



下面表格中出现你的头像及Github账号地址，视为Wall团队成员。

| 头像                                                         | 名称    | Github                           |
| ------------------------------------------------------------ | ------- | -------------------------------- |
|<img src="https://img-blog.csdnimg.cn/7da53370f8f8449bbc9025cf702e730a.jpeg" style="border-radius:50%;border:1px #eee solid" width="100">| Tongyao | https://github.com/super-tongyao |
| 成员1                                                        | 成员1   | 成员1                            |
| 成员2                                                        | 成员2   | 成员2                            |

## 安装教程

### 源代码地址

> Vue 源码请查看分支：[vue分支](https://github.com/super-tongyao/wall/tree/vue)

> Spring Boot 源码请查看分支：[service分支](https://github.com/super-tongyao/wall/tree/service)

### 前端安装

前端安装建议推荐使用nginx代理。在此使用nginx做文章配置。

1、把wall前端文件放入```nginx.conf```配置文件中，并新增配置。

```
server {
	listen       80;
	server_name  你的网站域名或公网IP;
	
	underscores_in_headers on;

	location / {
		# 映射你nginx/html目录下的wall文件
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

至此，重启nginx不报错，前端部署完成。

### 后端安装

修改config/application.yml配置文件，并修改你本地的MySQL数据库连接端口及账号密码。

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

后端支持2中环境下快捷启动。

- Windows下双击```startup.bat```文件启动。

- Linux下执行```startup.sh```文件启动，请先获取执行权限。

也可以输入命令行启动。

```
java -jar bin/wall.jar -Dspring.config.location="config/application.yml"
```

至此，访问```http://你的网站域名或公网IP:80```正常显示页面及操作数据，完成安装。

如有问题，请提交Issues。

## 更新日志

#### 2023－02－28（v1.0）
> 1、版本（v1.0）上线。

## 参与贡献

发送邮箱：super_tongyao@163.com，内容主题：关于Wall开源参与贡献

让我们一起让Wall变的更好。

## 免责声明

(一)、Wall提供免费开源的程序，不提供网站相关的内容服务，该程序之著作权归Wall及Wall团队所有。

(二)、用户可自由选择是否使用我们的程序，Wall与用户使用我们的程序所建立的网站无任何关联，Wall对用户及其网站不承担任何责任。

(三)、用户下载、安装、使用本程序，即表明用户信任Wall，Wall对任何原因在使用本程序时可能对用户自己或他人造成的任何形式的损失和伤害不承担责任。

(四)、任何单位或个人认为使用本程序建立的网站可能涉嫌侵犯其合法权益的，应该及时向该网站的所有人反映、交涉、或诉诸法律手段。

(五)、使用本程序的用户因为违反本声明的规定而触犯中华人民共和国法律的，一切后果自己负责，Wall和Wall团队不承担任何责任。

(六)、本声明未涉及的问题参见国家有关法律法规，当本声明与国家法律法规冲突时，以国家法律法规为准。
