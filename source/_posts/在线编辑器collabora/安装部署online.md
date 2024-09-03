---
title: 记录一次collabora online安装部署
urlname: install-collabora-online
cover: https://cdn.nlark.com/yuque/0/2024/png/28846352/1714094796085-23a3a180-6572-49d1-97bd-e4fe10ec4e8b.png
description: 记录一次collabora online安装部署
date: 2024-09-02 12:01:51
tags:
    - collabora
comments: false
top_img: false
---

> 环境：centos-7，docker-26.0.2

<a name="lVYiy"></a>
# 一：安装部署online
安装docker```
1. 更新系统
sudo yum update
2. 安装依赖
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
3. 添加 Docker CE 仓库
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
4. 安装 Docker CE软件包
sudo yum install docker-ce docker-ce-cli containerd.io
5. 启动 Docker 服务
sudo systemctl start docker
6. 设置 Docker 开机启动
sudo systemctl enable docker
7. 验证安装
sudo docker --version
8. 拉取nginx测试
sudo docker pull nginx
sudo docker run --name nginx -p 80:80 -d nginx
```
安装配置docker collabora online> 拉取启动collabora/code镜像

```
docker run -t -d \
--name collabora \
-p 9980:9980 \
-e username=admin \
-e password=admin \
--restart always \
--cap-add MKNOD \
-v /home/docker/coolwsd.xml:/etc/coolwsd/coolwsd.xml \
-v /home/fonts:/opt/cool/systemplate/usr/share/fonts/truetype \
-v /home/fonts:/usr/share/fonts/truetype \
collabora/code
```
> 运行后使用docker ps查看是否运行成功：

![image.png](https://cdn.nlark.com/yuque/0/2024/png/28846352/1714094796085-23a3a180-6572-49d1-97bd-e4fe10ec4e8b.png#averageHue=%232a4a5f&clientId=u308c2fc1-99ff-4&from=paste&height=108&id=u6352cb75&originHeight=121&originWidth=1270&originalType=binary&ratio=1.125&rotation=0&showTitle=false&size=183001&status=done&style=none&taskId=ud6db562c-4cdb-45e1-8fcc-313cda5924b&title=&width=1128.888888888889)
> Online默认使用SSH，进入进入挂载的配置文件修改禁用SSH已经运行访问的主机名及端口
> 这里的<clientHost>：为客户端的ipv4地址，3000为SDK启动端口，根据实际修改
> <group></group>可配置多个<host>标签

```
挂载卷：-v /home/docker/coolwsd.xml:/etc/coolwsd/coolwsd.xml \
1. 禁用SSL
<ssl desc="SSL settings">
    <enable type="bool" desc="xxx." default="true">false</enable>
</ssl>
2. 配置域名允许访问
<group>
    <host desc="hostname to allow or deny." allow="true">http://<clientHost>:3000</host>
</group>
```
> 配置好以后保存重启docker Online服务，同上查看是否启动服务端口

```
1. 重启collabora
docker restart collabora
2. 查看是否启动
docker ps
3. 输出日志信息
docker logs -f collabora
```
> 在浏览器输入http://<serverHost>:9980，返回ok表示部署Online成功：

![image.png](/安装部署online/image%20(1).png)
> 浏览器输入：http://<serverHost>:9980/browser/dist/admin/admin.html，输入docker run时配置的账号密码，访问online控制台，可显示连接的wopi主机和打开的文档，和查看在线用户

![image.png](安装部署online/image%20(2).png)<br />![image.png](安装部署online/image%20(3).png)
<a name="Cd68k"></a>
# 二：连接online
<a name="cCzwU"></a>
## 一：下载SDK，连接Online
下载CollaboraOnlineSDK，这里使用NodeJs框架<br />[GitHub - CollaboraOnline/collabora-online-sdk-examples: Various minor pieces of code to be used in Collabora Online and related software](https://github.com/CollaboraOnline/collabora-online-sdk-examples)
打开node.js 框架```
1. 安装依赖
npm intall
2. 启动客户端
npm start
```
![image.png](https://img-blog.csdn/Users/liangquan/Downloads/image (3).png /Users/liangquan/Downloads/image (2).png /Users/liangquan/Downloads/image (1).pngimg.cn/img_convert/9fed88617a6556f47f4adcc4b0e1b4d7.png)
> 这里的localhost改为客户端服务器的ipv4地址：

![image.png](https://img-blog.csdnimg.cn/img_convert/f574fee5d7c322e1a4e2a538b4902686.png)
> 浏览器访问客户端服务：http://<clientHost>:3000

![image.png](https://img-blog.csdnimg.cn/img_convert/725f5b3f9504505218ac5dc982d04f6e.png)
> 在**Collabora Online Server**框中输入Online地址http://<serverHost>:9980，点击**Load Collabora Online**即可在下方ifram标签中查看到默认的HelloWorld	 	 	 

![image.png](https://img-blog.csdnimg.cn/img_convert/2ca32f99ceddebd7c9ce68148e5dcacc.png)
<a name="JpGfI"></a>
# 二：整合

1. 获取discovery.xml
> 访问：https://<serverHost>:<port>/hosting/discovery

![image.png](https://img-blog.csdnimg.cn/img_convert/22bf8ab027e611caa7aae59a9efd37c4.png)
> 返回的discovery.xml，其中包含各种文件格式的_urlsrc_ 。 urlsrc指定为文档编辑而创建的 iframe 需要使用的地址

![image.png](https://img-blog.csdnimg.cn/img_convert/87d7385c2607f435eb29c9014a3f4601.png)
> 获取到discovery.xml以后在客户端找到需要的文件格式，返回url和token(为给定文件和用户生成令牌（可将其存储在数据库中，可以选择过期))

2. Online客户端提供GetFile/PutFile/CheckFileInfo
   1. **CheckFileInfo**，当调用时以 json 形式返回文件的 BaseFileName 和 Size

![image.png](https://img-blog.csdnimg.cn/img_convert/c4d966ed48972ab6db10ce44ab13ebb2.png)

   2. **GetFile**，当调用时发送回文件的内容

![image.png](https://img-blog.csdnimg.cn/img_convert/977af55cf5619116a46882455235cdd1.png)

   3. **PutFile**

![image.png](https://img-blog.csdnimg.cn/img_convert/7365b7eecea51c94e647088a69d2d688.png)

3. 设置页面中文
> docker服务默认安装了中文字体，可在ifream的url上加参数：&lang=zh-cn，但是汉化不是很完善

http://<serverHost>:<port>/browser/baa6eef/cool.html?WOPISrc=http://<clientHost>:<port>/wopi/files/<id>&lang=zh-cn<br />![image.png](https://img-blog.csdnimg.cn/img_convert/592449efcdbff06fd1384877f1099980.png)
<a name="NlWiU"></a>
# 三：增加字体
增加字体> 挂载卷：

```
-v /home/fonts:/opt/cool/systemplate/usr/share/fonts/truetype \
-v /home/fonts:/usr/share/fonts/truetype \
```
![image.png](https://img-blog.csdnimg.cn/img_convert/7e1573ac3db1a80a04051a5b10e67318.png)
> docker restart collabora，重启容器
> docker exec -it collabora bash，进入容器
> fc-cache -fv   ，重建字体缓存
> coolconfig update-system-template   ，更新系统配置

![image.png](https://img-blog.csdnimg.cn/img_convert/d53aadd620dc00ba46c799a5a5439870.png)