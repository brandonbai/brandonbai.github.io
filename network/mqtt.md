---
layout:default
---

## MQTT 概述
-----------
MQTT是IBM开发的一个即时通讯协议，有可能成为物联网的重要组成部分。该协议支持所有平台，几乎可以把所有联网物品和外部连接起来，被用来当做传感器和制动器之间通信的桥梁。

MQTT协议是为大量计算能力有限，且工作在低带宽、不可靠的网络的远程传感器和控制设备通讯而设计的协议。有以下特点：
* 使用发布/订阅消息模式，提供一对多的消息发布
* 使用TCP/IP提供网络连接
* 小型传输，开销很小（固定长度的头部是 2 字节），协议交换最小化，以降低网络流量，传输的内容最大为256MB。
* 使用 Last Will 和 Testament 特性通知有关各方客户端异常中断的机制。
 

### 1.MQTT协议实现方式
-----------
MQTT系统由与服务器通信的客户端组成，通常称服务器为“代理Broker”。客户可以是信息发布者Publish或订阅者Subscribe。每个客户端都可以连接到代理。

信息按主题层次结构组织。当发布者具有要分发的新数据时，它会将包含数据的控制消息发送到连接的代理。然后，代理将信息分发给已订阅该主题的任何客户端。发布者不需要有关于订阅者数量或位置的任何数据，而订阅者又不必配置有关发布者的任何数据。

MQTT传输的消息分为：主题（Topic）和负载（payload）两部分：
（1）Topic，可以理解为消息的类型，订阅者订阅（Subscribe）后，就会收到该主题的消息内容（payload）；
（2）payload，可以理解为消息的内容，是指订阅者具体要使用的内容。

### 2.	MQTT协议中的订阅、主题、会话
-----------
##### 2.1订阅（Subscription）
订阅包含主题筛选器（Topic Filter）和最大服务质量（QoS）。订阅会与一个会话（Session）关联。一个会话可以包含多个订阅。每一个会话中的每个订阅都有一个不同的主题筛选器。
##### 2.2会话（Session）
每个客户端与服务器建立连接后就是一个会话，客户端和服务器之间有状态交互。会话存在于一个网络之间，也可能在客户端和服务器之间跨越多个连续的网络连接。
##### 2.3主题名（Topic Name）
连接到一个应用程序消息的标签，该标签与服务器的订阅相匹配。服务器会将消息发送给订阅所匹配标签的每个客户端。
系统主题：通过定义$SYS开头的主题可以查看一些系统信息，如客户端连接数量等，
详细介绍：https://github.com/mqtt/mqtt.github.io/wiki/SYS-Topics
##### 2.4主题筛选器（Topic Filter）
一个对主题名通配符筛选器，在订阅表达式中使用，表示订阅所匹配到的多个主题。
多级匹配符 #
单级匹配符 +
更多主题讨论，请移步github wiki https://github.com/mqtt/mqtt.github.io/wiki/topic_format
##### 2.5负载（Payload）
消息订阅者所具体接收的内容。

### 3.保留消息和最后遗嘱
-----------
##### 保留消息 Retained Messages
MQTT中，无论是发布还是订阅都不会有任何触发事件。
1个Topic只有唯一的retain消息，Broker会保存每个Topic的最后一条retain消息。 
发布消息时把retain设置为true，即为保留信息。每个Client订阅Topic后会立即读取到retain消息。如果需要删除retain消息，可以发布一个空的retain消息，因为每个新的retain消息都会覆盖最后一个retain消息。 
##### 最后遗嘱 Last Will & Testament
MQTT本身就是为信号不稳定的网络设计的，所以难免一些客户端会无故的和Broker断开连接。 当客户端连接到Broker时，可以指定LWT，Broker会定期检测客户端是否有异常。 
当客户端异常掉线时，Broker就往连接时指定的topic里推送当时指定的LWT消息。

### 4.消息服务质量
-----------
 有三种消息发布服务质量qos(Quality of Service)：

#### 4.1“至多一次”

![至多一次](https://upload-images.jianshu.io/upload_images/5151732-514c317ca16128d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
 
消息发布完全依赖底层TCP/IP网络。会发生消息丢失或重复。这一级别可用于如下情况，环境传感器数据，丢失一次读记录无所谓，因为不久后还会有第二次发送。

#### 4.2“至少一次”

![至少一次](https://upload-images.jianshu.io/upload_images/5151732-f5c83240efced9b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

PUBACK消息是对QoS级别为1的PUBLISH消息的响应.PUBACK消息由服务器发送以响应来自发布端的PUBLISH消息，订阅端也会响应来自服务器的PUBLISH消息。当发布端收到PUBACK消息时，它会丢弃原始消息，因为它也被服务器接收（并记录）。

如果一定时间内，发布端或服务器没有收到PUBACK消息，则会进行重发。这种方式虽然确保了消息到达，但消息重复可能会发生。

#### 4.3“只有一次”

![只有一次](https://upload-images.jianshu.io/upload_images/5151732-e6d4a518c8932b6d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

PUBREC消息是对QoS级别为2的PUBLISH消息的响应。它是QoS级别2协议流的第二个消息。 PUBREC消息由服务器响应来自发布端的PUBLISH消息，或订阅端响应来自服务器的PUBLISH消息。发布端或服务器收到PUBREC消息时，会响应PUBREL消息。

PUBREL消息是从发布端对PUBREC的响应，或从服务器对订阅端PUBREC消息的响应。 这是QoS 2协议流中第三个消息。当服务器从发布者收到PUBREL消息时，服务器会将PUBLISH消息发送到订阅端，并发送PUBCOMP消息到发布端。 当订阅端收到来自服务器的消息PUBREL时，使得消息可用于应用程序并将PUBCOMP消息发送到服务器。

PUBCOMP消息是服务器对来自发布端的PUBREL消息的响应，或订阅者对来自服务器的PUBREL消息的响应。 它是QoS 2协议流程中的第四个也是最后一个消息。当发布端收到PUBCOMP消息时，它会丢弃原始消息，因为它已经将消息发给了服务器。

在一些要求比较严格的计费系统中，可以使用此级别。在计费系统中，消息重复或丢失会导致不正确的结果。这种最高质量的消息发布服务还可以用于即时通讯类的APP的推送，确保用户收到且只会收到一次。

-----
### 附录：各编程语言对MQTT客户端/服务器的实现
| Name | Developed by | Language | Type | First release date | Last release | Last release date | License |
-|-|-|-|-|-|-|-
| Adafruit IO | [Adafruit](https://en.wikipedia.org/wiki/Adafruit_Industries "Adafruit Industries") | [Ruby on Rails](https://en.wikipedia.org/wiki/Ruby_on_Rails "Ruby on Rails"), [Node.js](https://en.wikipedia.org/wiki/Node.js "Node.js")<sup>[[31]](https://en.wikipedia.org/wiki/MQTT#cite_note-31)</sup> | Client | ***?*** | 2.0.0<sup>[[32]](https://en.wikipedia.org/wiki/MQTT#cite_note-32)</sup> | ***?*** | ***?*** |
| flespi | [Gurtam](https://en.wikipedia.org/wiki/Gurtam "Gurtam") | [C](https://en.wikipedia.org/wiki/The_C_Programming_Language "The C Programming Language") | Broker | 2017-12-15 | ***?*** | 2018-07-26 | Proprietary License |
| M2Mqtt | [eclipse](https://en.wikipedia.org/wiki/Eclipse_Foundation "Eclipse Foundation") | [C#](https://en.wikipedia.org/wiki/C_Sharp_(programming_language) "C Sharp (programming language)") | Client | 2017-05-20 | 4.3.0.0<sup>[[33]](https://en.wikipedia.org/wiki/MQTT#cite_note-33)</sup> | 2017-05-20 | [Eclipse Public License 1.0](https://en.wikipedia.org/wiki/Eclipse_Public_License "Eclipse Public License") |
| Machine Head | ClojureWerkz Team | [Clojure](https://en.wikipedia.org/wiki/Clojure "Clojure") | Client | 2013-11-03 | 1.0.0<sup>[[34]](https://en.wikipedia.org/wiki/MQTT#cite_note-34)</sup> | 2017-03-05 | Creative Commons Attribution 3.0 Unported License |
| moquette | Selva, Andrea | [Java](https://en.wikipedia.org/wiki/Java_(programming_language) "Java (programming language)") | Broker | 2015-07-08 | 0.10<sup>[[35]](https://en.wikipedia.org/wiki/MQTT#cite_note-35)</sup> | 2017-06-30 | [Apache License 2.0](https://en.wikipedia.org/wiki/Apache_License "Apache License") |
| Mosquitto | [eclipse](https://en.wikipedia.org/wiki/Eclipse_Foundation "Eclipse Foundation") | [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)"), [Python](https://en.wikipedia.org/wiki/Python_(programming_language) "Python (programming language)") | Broker and client | 2009-12-03 | 1.4.15<sup>[[36]](https://en.wikipedia.org/wiki/MQTT#cite_note-36)</sup> | 2018-02-27 | [Eclipse Public License 1.0](https://en.wikipedia.org/wiki/Eclipse_Public_License "Eclipse Public License"), Eclipse Distribution License 1.0 (BSD) |
| [Paho MQTT](https://en.wikipedia.org/wiki/Eclipse_Paho "Eclipse Paho") | [eclipse](https://en.wikipedia.org/wiki/Eclipse_Foundation "Eclipse Foundation") | [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)"), [C++](https://en.wikipedia.org/wiki/C%2B%2B "C++"), [Java](https://en.wikipedia.org/wiki/Java_(programming_language) "Java (programming language)"), [Javascript](https://en.wikipedia.org/wiki/Javascript "Javascript"), [Python](https://en.wikipedia.org/wiki/Python_(programming_language) "Python (programming language)"), [Go](https://en.wikipedia.org/wiki/Go_(programming_language) "Go (programming language)") | Client | 2014-05-02 | 1.3.0<sup>[[37]](https://en.wikipedia.org/wiki/MQTT#cite_note-37)</sup> | 2017-06-28 | [Eclipse Public License 1.0](https://en.wikipedia.org/wiki/Eclipse_Public_License "Eclipse Public License"), Eclipse Distribution License 1.0 (BSD)<sup>[[38]](https://en.wikipedia.org/wiki/MQTT#cite_note-38)</sup> |
| SharkMQTT | Real Time Logic | [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)") | Client | 2015-11-06 | 1.5<sup>[[39]](https://en.wikipedia.org/wiki/MQTT#cite_note-39)</sup> | 2017-10-08 | Proprietary License |
| [VerneMQ](https://vernemq.com/) | [Octavo Labs](https://octavolabs.com/) | [Erlang/OTP](https://en.wikipedia.org/wiki/Erlang/OTP "Erlang/OTP") | Broker | 2015-05-28 | 1.4.1<sup>[[40]](https://en.wikipedia.org/wiki/MQTT#cite_note-40)</sup> | 2018-06-05 | [Apache License 2.0](https://en.wikipedia.org/wiki/Apache_License "Apache License") |
| wolfMQTT | wolfSSL | [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)") | Client | 2015-11-06 | 0.14<sup>[[41]](https://en.wikipedia.org/wiki/MQTT#cite_note-41)</sup> | 2017-11-22 | [GNU Public License, version 2](https://en.wikipedia.org/wiki/GPL "GPL") |
| MQTTRoute | Bevywise Networks | [C](https://en.wikipedia.org/wiki/C_(programming_language) "C (programming language)"), [Python](https://en.wikipedia.org/wiki/Python_(programming_language) "Python (programming language)") | Broker | 2017-04-25 | 1.0<sup>[[42]](https://en.wikipedia.org/wiki/MQTT#cite_note-42)</sup> | 2017-12-19 | Proprietary License<sup>[[43]](https://en.wikipedia.org/wiki/MQTT#cite_note-43)</sup> |
| HiveMQ | dc-square GmbH | [Java](https://en.wikipedia.org/wiki/Java_(programming_language) "Java (programming language)") | Broker | 2013-03-26 | 3.4.0<sup>[[44]](https://en.wikipedia.org/wiki/MQTT#cite_note-44)</sup> | 2017-05-09 | Proprietary License |
| SwiftMQ | IIT Software GmbH | [Java](https://en.wikipedia.org/wiki/Java_(programming_language) "Java (programming language)") | Broker | 2000-07-01 | 11.1.0<sup>[[45]](https://en.wikipedia.org/wiki/MQTT#cite_note-45)</sup> | 2018-06-06 | Proprietary License |
| JoramMQ | ScalAgent D.T. | [Java](https://en.wikipedia.org/wiki/Java_(programming_language) "Java (programming language)") | Broker | 2000-05-01 | 11.1.0<sup>[[46]](https://en.wikipedia.org/wiki/MQTT#cite_note-46)</sup> | 2018-04-13 | Proprietary License |
