---
layout: default
---

> 通过在服务器Tomcat中进行简单配置即可在本地debug服务器上的代码。

###1. Tomcat配置
(1) 进入到tomcat目录
(2) 编辑bin/catalina.sh
```
 vim bin/catalina.sh
```
搜索 localhost:8000,如下所示，
```
330   if [ -z "$JPDA_ADDRESS" ]; then
331     JPDA_ADDRESS="localhost:8000"
332   fi
```
将localhost:8000改为自定义的端口号(示例中改为了8081)。
```
330   if [ -z "$JPDA_ADDRESS" ]; then
331     JPDA_ADDRESS="8081"
332   fi
```
(3) 保存退出
(4) 启动tomcat
```
bin/catalina.sh jpda start
```
(5) 使用netstat命令查看是否开启远程调试
```
netstat -npl|grep 8081
```
出现如下结果表示开启成功
```
tcp        0      0 0.0.0.0:8081            0.0.0.0:*               LISTEN
```
###2. Eclipse 配置
(1) 打开调试配置
![](http://upload-images.jianshu.io/upload_images/5151732-9af80a1c62de12dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
(2) 设置运行参数
![](http://upload-images.jianshu.io/upload_images/5151732-7fa0c4447dd7c590.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
(3) 点击**Debug** 按钮
(4) 打上断点，开始调试

### 3. IntelliJ IDEA 配置

(1) 打开运行设置

![](https://upload-images.jianshu.io/upload_images/5151732-feece9b95976aa08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(2) 点击remote

![](https://upload-images.jianshu.io/upload_images/5151732-f63d5d7b5de52fe6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(3) 设置连接参数

1. jvm版本
2. 远程debug ip
3. 远程debug端口号
4. 本地代码

![](https://upload-images.jianshu.io/upload_images/5151732-4aab60faccf79da8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(4) 点击Debug按钮

![](https://upload-images.jianshu.io/upload_images/5151732-4e1e73b7acd8369c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

(5) 打上断点，开始调试
