# 快速实践，第二节：搭建 WordPress 应用

> 本教程基于 DataFoundry 经典界面编写，考虑到产品的快速演进，部分步骤和图示可能已经改变。

为了更好地向你介绍 DataFoundry 各种功能，我们编写了这个系列教程，共包含四个章节：
- 第一节，（XXX），你将学习如何通过代码构建和服务部署来部署一个简单应用；
- 第二节，搭建 WordPress 应用，你将学习如何使用 DataFoundry 后端服务来部署应用；
- 第三节，（XXX），你将学习如何使用 DataFoundry 的 DevOps 功能进行 CICD；
- 第四节，（XXX），你将学习如何进行 User Provided Service 实例的创建、部署，并于后端服务绑定。

## 1 第二节所覆盖的知识点

在第二节，我们将学会如何进行：
- 代码构建
- 后端服务申请
- 服务部署
- 将应用与后端服务绑定

## 2 关于 WordPress 应用

WordPress 是一种使用 PHP 语言开发的博客平台，用户可以在支持 PHP 和 MySQL 数据库的服务器上架设属于自己的网站。也可以把 WordPress 当作一个内容管理系统（CMS）来使用。

在本节，我们将演示如何通过 DataFoundry 平台提供的 MySQL 后端服务来部署 WordPress 应用。

![](img/Part_2_WordPress.png)

## 3 开始前的准备工作

在你开始之前，你需要在 DataFoundry 注册一个帐号。

对于图形界面操作，你还需要以下浏览器之一：
- Firefox 15 或以上
- Chrome 21 或以上
- Internet Explorer 10 或以上
- Safari 7 或以上

对于命令行操作，你还需要下载 OpenShift 客户端：
- [Windows](https://s3.cn-north-1.amazonaws.com.cn/complier/oc-control.zip)
- [Mac](https://s3.cn-north-1.amazonaws.com.cn/complier/openshift-origin-client-tools-v1.1.0.1-bf56e23-mac.zip)
- [Linux](https://s3.cn-north-1.amazonaws.com.cn/complier/openshift-origin-client-tools-v1.1.0.1-bf56e23-linux)

## 4 Step by Step 详细操作

下面分别对图形界面和命令行两种方式进行介绍。

### 4.1 图形界面操作

#### Step 1：代码构建

1）登录平台：

![](img/Screenshot from 2016-05-12 18-14-31.png)

2）在左侧菜单中点击“代码构建”：
![](img/Screenshot from 2016-05-17 12-10-38.png)

3）点击“新建构建”：
![](img/Screenshot from 2016-05-12 18-16-17.png)

4）在“构建名称”中输入“wordpress”、在“代码 URL”中输入 “https://github.com/datafoundry/wordpress.git” 后，点击“开始构建” ：
![](img/Screenshot from 2016-05-17 12-11-09.png)

注意：
- 为了能够让 WordPress 自动适配后端服务提供的环境变量，我们对 DockerHub 官方 WordPress 镜像进行了微调；
- 在状态页中可以查看构建状态，构建完成后可以镜像仓库中查看本次构建的镜像。

#### Step 2：后端服务申请
1）点击“后端服务” 可以看到目前 DataFoundry 所能提供的各类后端服务：
![](img/Screenshot from 2016-05-16 18-27-54.png)

2）点击“申请实例”，填入“服务名称”，在选择“服务套餐”后点击“创建” ：
![](img/Screenshot from 2016-05-12 18-41-15.png)

3）后端服务创建完成后，可以显示创建后端服务详细信息：
![](img/Screenshot from 2016-05-12 18-41-36.png)

4）回到“后端服务”，点击“我的后端服务实例”Tab 页，在这里可以看到所有已创建的后端服务实例：
![](img/Screenshot from 2016-05-16 18-37-04.png)
 
#### Step 3：服务部署
1）在左侧菜单栏点击“镜像仓库”，鼠标移动到镜像仓库上后，可以点击“部署最新版本”来部署该镜像： 
![](img/Screenshot from 2016-05-17 12-21-24.png)

2）在部署容器镜像时，可填写“服务名称”、“容器名称”、容器启动时占用的端口和对应服务的端口，点击“创建服务”：
![](img/Screenshot from 2016-05-17 12-23-18.png)

3）容器默认是“自动运行”，若未勾选，你也可以进入“服务详情”页，点击”启动“来触发容器启动：
![](img/Screenshot from 2016-05-17 12-24-07.png)

4）在“服务详情”页的“高级配置”区域，可以看到“路由设置”开关，在这里可以为服务配置 route 信息：
![](img/Screenshot from 2016-05-17 12-25-11.png)

#### Step 4：后端服务绑定
1）最后，在“高级配置”区域，进行“后端服务绑定”与“环境变量设置”：
![](img/Bind_Backing_Service.png)

2）配置完成后，点击“创建服务”，数十秒内即可完成绑定了后端服务的服务部署。部署完成后，点击“路由 URL”下方的 URL，即可访问你所部署的服务：
![](img/Route_URL.jpg)

注意：
- 对于“Step 2：后端服务申请”和“Step 3：服务部署”，你也可以选择先进行“Step 3：服务部署”，再进行“Step 2 & 4：后端服务的申请和绑定”。不过，由于“服务部署”时没有提供后端服务，WordPress 会一直重启；
- 待后端服务创建完成后，在“后端服务”-“我的后端服务实例”Tab 页，选择相应后端服务，点击“服务绑定”按钮，在窗口中点击“新增绑定”，在弹出窗口中选择需要绑定后端服务的应用，后端服务与应用即绑定完成：
![](img/Screenshot from 2016-05-16 18-38-15.png)


### 4.2 命令行操作

命令行操作时，必须先部署服务，再将后端服务与应用绑定，于是我们将操作步骤的顺序略作调整为 1、3、2、4。

#### Step 1 & 3：代码构建+服务部署

1）命令行操作时，“代码构建”和“服务部署”可以通过一个命令 `oc new-app` 完成：

```
$ oc new-app https://github.com/datafoundry/wordpress.git
--> Found Docker image 10e778c (12 days old) from Docker Hub for "library/php:5.6-apache"
    * An image stream will be created as "php:5.6-apache" that will track the source image
    * A Docker build using source code from https://github.com/datafoundry/wordpress.git will be created
      * The resulting image will be pushed to image stream "wordpress:latest"
      * Every time "php:5.6-apache" changes a new build will be triggered
    * This image will be deployed in deployment config "wordpress"
    * Port 80/tcp will be load balanced by service "wordpress"
      * Other containers can access this service through the hostname "wordpress"
    * WARNING: Image "wordpress" runs as the 'root' user which may not be permitted by your cluster administrator
--> Creating resources with label app=wordpress ...
    imagestream "php" created
    imagestream "wordpress" created
    buildconfig "wordpress" created
    deploymentconfig "wordpress" created
    service "wordpress" created
--> Success
    Build scheduled, use 'oc logs -f bc/wordpress' to track its progress.
    Run 'oc status' to view your app.
```  

2）查看部署结果：  

```
$ oc get pods
  NAME                 READY     STATUS             RESTARTS   AGE
  wordpress-1-build    0/1       Completed          0          3m
  wordpress-1-deploy   1/1       Running            0          1m
  wordpress-1-hfzhs    0/1       CrashLoopBackOff   3          1m
``` 

因为没有提供 MySQL 后端服务，WordPress 一直在重启，我们现在来创建 MySQL Backing Service。
     
##### Step 2：后端服务申请

1）在通过 DataFoundry 生成一个 MySQL 的后端服务之前，我们可以先查看一下目前 DataFoundry 已经集成的后端服务。

```   
$ oc get bs -n openshift  
```

注意：   
- 后端服务是 DataFoundry 的特有功能，所以必须要使用 DataFoundry 客户端连接服务端查看；   
- 在查看 DataFoundry 已集成的后端时，要添加后端服务默认的集成命名空间 OpenShift。

以上命令输出结果为：  

```   
  NAME         LABELS                           BINDABLE   STATUS
  Cassandra    asiainfo.io/servicebroker=etcd   true       Active
  ETCD         asiainfo.io/servicebroker=etcd   true       Active
  Greenplum    asiainfo.io/servicebroker=rdb    true       Active
  Kafka        asiainfo.io/servicebroker=etcd   true       Active
  MongoDB      asiainfo.io/servicebroker=rdb    true       Active
  Mysql        asiainfo.io/servicebroker=rdb    true       Active
  PostgreSQL   asiainfo.io/servicebroker=rdb    true       Active
  RabbitMQ     asiainfo.io/servicebroker=etcd   true       Active
  Redis        asiainfo.io/servicebroker=etcd   true       Active
  Spark        asiainfo.io/servicebroker=etcd   true       Active
  Storm        asiainfo.io/servicebroker=etcd   true       Active
  ZooKeeper    asiainfo.io/servicebroker=etcd   true       Active
```   

可以看到 DataFoundry 已集成了非常丰富的后端服务组件，下面我们创建一个 MySQL 后端服务实例。  
  
2）在创建实例之前，我们要先通过 `oc describe bs <backingservcie-name> ` 获取应用所需的后端服务计划（Plan），例如我们获取 MySQL 后端服务的服务计划为：

```   
$ oc describe bs Mysql -n openshift
  Name:			Mysql
  Created:		21 hours ago
  Labels:			asiainfo.io/servicebroker=rdb
  Annotations:		<none>
  Description:		A MYSQL DataBase
  Status:			Active
  Bindable:		true
  Updateable:		false
  documentationUrl:	http://docs.mysql.com
  longDescription:	OpenSoure RDMBS Mysql
  providerDisplayName:	asiainfoLDP
  supportUrl:		http://www.mysql.com
  displayName:		Mysql
────────────────────
  Plan:		Experimental
  PlanID:		56660431-6032-43D0-A114-FFA3BF521B66
  PlanDesc:	share a mysql database in one instance
  PlanFree:	true
  Bullets:
  20 GB of Disk
  20 connections
  PlanCosts:
  CostUnit:	MONTHLY
  Amount:
    eur: 49
    usd: 99
  CostUnit:	1GB of messages over 20GB
  Amount:
    eur: 0.49
    usd: 0.99
```

3）我们选取 Experimental 计划创建 MySQL 后端服务实例：

```   
$ oc new-backingserviceinstance mysql-inst1 \
  --backingservice_name=Mysql \
  --planid=56660431-6032-43D0-A114-FFA3BF521B66
  Backing Service Instance has been created.
```

4）查看后端服务列表：

```   
$ oc get bsi
  NAME          SERVICE   PLAN           BOUND     STATUS
  mysql-inst1   Mysql     Experimental   0         Unbound 
```

5）查看后端服务详细信息：

```
$ oc describe bsi mysql-inst1
  Name:			mysql-inst1
  Created:		5 minutes ago
  Labels:			<none>
  Annotations:		<none>
  Status:			Unbound
  DashboardUrl:		http://e412377c9b5f3db:1394e5f077d1519@phpmyadmin-service-broker-db.app.dataos.io?db=8c60f229ef4dac0
  BackingServiceName:	Mysql
  BackingServicePlanName:	Experimental
  BackingServicePlanGuid:	56660431-6032-43D0-A114-FFA3BF521B66
  Parameters:
  instance_id:	340082e4-1734-11e6-a653-fa163edcfb45
  Bound:		0
  Events:
  FirstSeen	LastSeen	Count	From	SubobjectPath	Type		Reason		Message
  ---------	--------	-----	----	-------------	--------	------		-------
  5m		5m		1	{bsi }			Normal		Provisioning	bsi provisioning done, instanceid: 340082e4-1734-11e6-a653-fa163edcfb45
```

##### Step 4：后端服务绑定

1）以上服务实例创建完成，我们继续把 MySQL Backing Service 绑定到 WordPress 应用中：

```
$ oc bind mysql-inst1 wordpress
$ oc env dc/wordpress MYSQLBSI=MYSQLINST1 BSITYPE=MYSQL
```  

2）查看部署结果：

```
$ oc get pods
  NAME                READY     STATUS      RESTARTS   AGE
  wordpress-1-build   0/1       Completed   0          7m 
  wordpress-2-55q5a   1/1       Running     0          41s
```  

3）Pod 已正常启动，给 WordPress 生成一个 route 地址后就可以访问了：

```
$ oc expose dc wordpress  --port=80 --name=wordpress
$ oc expose svc wordpress --hostname=wordpress.demo.app.dataos.io --name=wordpress
```

### 5 下一步

1）本节，我们分别使用了图形界面与命令行两种方式，搭建了 WordPress 应用。打开浏览器，访问 http://wordpress.demo.app.dataos.io 看到如下界面，说明 WordPress 应用已经成功运行。
![](img/WordPress.png)

2）下一节，我们将学习如何使用 DataFoundry 的 DevOps 功能进行 CICD。

# 快速实践，第三节：使用DataFoundry进行CI/CD

## 1 第三节所覆盖的知识点

在第三节，我们将学会：
- 如何对部署的应用进行CI/CD的配置


## 2 对部署的应用进行CI/CD配置

### 2.1 图形界面操作

新建服务-高级配置页面配置CI/CD选项配置，如下图所示：

![](img/cicd页面配置.jpg)

勾选“镜像变化触发自动部署”后，当容器所基于的镜像发生改变时，就会触发服务基于新的镜像重新部署。

### 2.2 命令行操作

我们可以通过命令对dc,bc和rc的triggers进行操作。这里我们需要介绍triggers的概念：triggers就是指一些能够触发CI/CD的条件。datafoundry中包括两种triggers，分别为配置文件发生改变时触发自动部署和镜像发生改变时触发自动部署。


#### 2.2.1 列出资源中所有的triggers条件

```
$ oc set triggers dc/wordpress
```

会得到以下结果：

	NAME                         TYPE    VALUE                         AUTO
	deploymentconfigs/wordpress  config                                true
	deploymentconfigs/wordpress  image   wordpress:master (wordpress)  true

我们可以看到以上结果中列出了两个trigger条件，分别为dc配置文件发生改变时触发自动部署和WordPress:master这个镜像发生改变时触发自动部署。

#### 2.2.2 删除所有的triggers

```
$ oc set triggers dc/wordpress --remove-all
```

再次查看dc/wordpress的triggers时，我们会发现没有任何trigger条件了。

也可以删除单独的trigger，使用以下命令：

```
$ oc set triggers dc/wordpress --from-config --remove
```

执行完这条命令后，当dc的配置文件发生改变时，就不会触发自动部署了。

下面我们来逐步为它增加triggers，以此来熟悉增加trigger的命令。


#### 2.2.3 增加trigger

```
$ oc set triggers  dc/wordpress --from-image=wordpress:master --containers=wordpress
```

这条命令中，需要指定--containers，否则会报错。--containers内容为pod配置文件中Containers字段下的容器名字。也可以通过以下命令增加dc配置文件发生改变时触发部署的trigger：

```
$ oc set triggers  dc/wordpress --from-config=true
```
