> (mqtt java客户端整合Spring的参看[这篇文章](https://www.jianshu.com/p/6b60858b7d44))

Paho Java客户端是一个用Java编写的MQTT客户端库，用于开发在JVM或其他Java兼容平台（如Android）上运行的应用程序。
Paho Java客户端提供了两个API：MqttAsyncClient提供了一个完全异步的API，通过已注册的回调通知完成活动。 MqttClient是MqttAsyncClient的一个同步包装，其中函数与应用程序同步。

### [](https://github.com/eclipse/paho.mqtt.java#downloading)下载

将下面显示的依赖性定义添加到maven pom文件中。

最新版本是`1.2.0`和当前的快照版本`1.2.1-SNAPSHOT`。

```
<dependencies>
    <dependency>
        <groupId>org.eclipse.paho</groupId>
        <artifactId>org.eclipse.paho.client.mqttv3</artifactId>
        <version>1.2.0</version>
    </dependency>
</dependencies>

```

###入门

基类|介绍
-|-
MqttClient|同步调用客户端，使用阻塞方法与MQTT服务器通信。
MqttAsyncClient|异步调用客户端，使用非阻塞方法与MQTT服务器通信，允许操作在后台运行。
MqttClientPersistence|表示持久性数据存储，用于存储正在传输的出站和入站消息，从而实现向指定的[QoS](https://www.jianshu.com/p/73d9c6668dfc)的传递。 可以使用 MqttClient指定此接口的实现，MqttClient将使用该实现来持久保存QoS为1和2消息。
MqttConnectOptions|保存控制客户端连接到服务器的方式的选项集，包括用户名、密码等。
MqttMessage|MQTT消息，保存应用程序有效负载和指定消息如何传递的选项消息。

下面包含的代码是一个非常基本的示例，它连接到服务器并使用**MqttClient同步API**发布/订阅消息。

* 发布端
```
/**
 *发布端
 */
public class PublishSample {
	public static void main(String[] args) {

		String topic = "mqtt/test";
		String content = "hello 哈哈";
		int qos = 1;
		String broker = "tcp://iot.eclipse.org:1883";
		String userName = "test";
		String password = "test";
		String clientId = "pubClient";
		// 内存存储
		MemoryPersistence persistence = new MemoryPersistence();

		try {
			// 创建客户端
			MqttClient sampleClient = new MqttClient(broker, clientId, persistence);
			// 创建链接参数
			MqttConnectOptions connOpts = new MqttConnectOptions();
			// 在重新启动和重新连接时记住状态
			connOpts.setCleanSession(false);
			// 设置连接的用户名
			connOpts.setUserName(userName);
			connOpts.setPassword(password.toCharArray());
			// 建立连接
			sampleClient.connect(connOpts);
			// 创建消息
			MqttMessage message = new MqttMessage(content.getBytes());
			// 设置消息的服务质量
			message.setQos(qos);
			// 发布消息
			sampleClient.publish(topic, message);
			// 断开连接
			sampleClient.disconnect();
			// 关闭客户端
			sampleClient.close();
		} catch (MqttException me) {
			System.out.println("reason " + me.getReasonCode());
			System.out.println("msg " + me.getMessage());
			System.out.println("loc " + me.getLocalizedMessage());
			System.out.println("cause " + me.getCause());
			System.out.println("excep " + me);
			me.printStackTrace();
		}
	}
}
```

* 订阅端
```
/**
 *订阅端
 */
public class SubscribeSample {

	public static void main(String[] args) throws MqttException {	
		String HOST = "tcp://iot.eclipse.org:1883";
		String TOPIC = "mqtt/test";
		int qos = 1;
		String clientid = "subClient";
		String userName = "test";
		String passWord = "test";
		try {
			// host为主机名，test为clientid即连接MQTT的客户端ID，一般以客户端唯一标识符表示，MemoryPersistence设置clientid的保存形式，默认为以内存保存
			MqttClient client = new MqttClient(HOST, clientid, new MemoryPersistence());
			// MQTT的连接设置
			MqttConnectOptions options = new MqttConnectOptions();
			// 设置是否清空session,这里如果设置为false表示服务器会保留客户端的连接记录，这里设置为true表示每次连接到服务器都以新的身份连接
			options.setCleanSession(true);
			// 设置连接的用户名
			options.setUserName(userName);
			// 设置连接的密码
			options.setPassword(passWord.toCharArray());
			// 设置超时时间 单位为秒
			options.setConnectionTimeout(10);
			// 设置会话心跳时间 单位为秒 服务器会每隔1.5*20秒的时间向客户端发送个消息判断客户端是否在线，但这个方法并没有重连的机制
			options.setKeepAliveInterval(20);
			// 设置回调函数
			client.setCallback(new MqttCallback() {

				public void connectionLost(Throwable cause) {
					System.out.println("connectionLost");
				}

				public void messageArrived(String topic, MqttMessage message) throws Exception {
					System.out.println("topic:"+topic);
					System.out.println("Qos:"+message.getQos());
					System.out.println("message content:"+new String(message.getPayload()));
					
				}

				public void deliveryComplete(IMqttDeliveryToken token) {
					System.out.println("deliveryComplete---------"+ token.isComplete());
				}

			});
			client.connect(options);
			//订阅消息
			client.subscribe(TOPIC, qos);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```
#链接

*   项目网站：[https://www.eclipse.org/paho](https://www.eclipse.org/paho)
*   MQTT协议概述：[https://www.jianshu.com/p/73d9c6668dfc](https://www.jianshu.com/p/73d9c6668dfc)
*   Paho Java：[https://eclipse.org/paho/clients/java/](https://eclipse.org/paho/clients/java)
*   GitHub：[https://github.com/eclipse/paho.mqtt.java](https://github.com/eclipse/paho.mqtt.java)
*   Spring支持：[https://www.jianshu.com/p/6b60858b7d44](https://www.jianshu.com/p/6b60858b7d44)
* Mosquitto搭建：[https://www.jianshu.com/p/9e3cb7042a2e](https://www.jianshu.com/p/9e3cb7042a2e)
