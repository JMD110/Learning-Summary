

### MongoDB基础

#### 一、MongoDB在Linux环境下的安装

​MongoDB[官网](https://www.mongodb.com/ "官网"):找到对应版本下载地址

`wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz`

文件解压缩/解归档:

`tar -zxvf mongodb-linux-x86_64-rhel70-3.6.5.tgz `

#### 二、配置MongoDB

我们要启动mongo的服务需要启动mongod。先编写配置文件。

`mkdir mongoConfig & cd mongoConfig`

`mkdir -p data/db`
`vim mongod.conf`



	yaml
	systemLog:  # 系统日志
	  destination: file  # 以文件形式存储
	  path: "./mongod.log"  # 文件路径和名称
	  logAppend: true  # 日志添加
	storage:  # 存储
	  dbPath: "./data/db"  # 数据存储的地方
	  journal:
	    enabled: true
	processManagement:
	  fork: true  # 是否后台运行
	net:
	  bindIp: 127.0.0.1  # 绑定IP地址
	  port: 27017  # 端口
	setParameter:
	  enableLocalhostAuthBypass: false  # 本地登录不需要密码
	

设置环境变量

`vim .bash_profile`  配置当前用户的环境
`source .bash_profile`  加载环境变量


#### 三、启动和关闭mongod服务

启动

`mongod -f mongod.conf `


关闭

`mongod -f mongod.conf --shutdown`


#### 四、数据库安全配置

进入mongo客户端设置全局用户

	javascript
	use admin
	db.createUser(
	  {
	    user: "username",
	    pwd: "password",
	    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
	  }
	)


mongo[官方文档](https://docs.mongodb.com/manual/reference/built-in-roles/index.html)

重新启动服务

`mongod -f mongod.conf --auth`
