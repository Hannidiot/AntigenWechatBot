## 插件列表

此机器人中核心的对话逻辑都封装在不同的插件当中，从而实现业务上的隔离。

### Conv2Convs 插件

到货提醒机器人能够将消息转发到指定的一个或多个群中，而消息类型包括文本、图片、小程序以及超链接等。以下即为使用方法：

1. 转发文本消息

格式：@AntigenBot # [楼栋号] [楼栋号] [你想说的话], 其中[楼栋号]与[楼栋号]，[楼栋号]与[你想说的话]之间都是以空格分割。

示例：@AntigenBot # 3 第三号楼栋的居民该下来做核算了。

首先，在群里面如果要向指定的群转发消息，就需要艾特机器人才行；其次，# 字符之后必须要携带楼栋号，系统已经根据不同楼栋群配置好其编号，如嘉怡91号楼组群的微信群编号为91；同时不同楼栋号之间以空格为分隔符；[你想说话的话]就是需要转发到微信群中的文本消息内容。

2. 转发图片、小程序、超链接等消息

由于此类消息无法和艾特消息在同一个消息中，故需要处理成两个消息。故如需转发图片消息，通常需要如下两个步骤：

* 艾特机器人并填写楼栋号，格式为：@AntigenBot # 3 8， 此为告诉机器人向三号楼和八号楼准备下一条消息。
* 发送群消息内容，此为志愿者向群内发送的转发内容，可以为图片、小程序以及超链接等不同类型的消息。

疑问：

1. 如果想要同时想群内转发多条消息，如【消息一】、【消息二】。此时就需要重复执行以上过程多次。


### Dyanmic Code

1. 功能介绍：

此插件将生成动态验证码，过期时间和数量都可由调用方自行控制。

2. API 介绍

    * url: server-endpoint:5003/dynamic_code
    * query_string:
        * token: str -> to verify the authentication
        * hours: int -> the expired hours of token
        * count: int -> the number of the generated tokens
    
    * examples:
        curl http://server-endpoint:[port]/dynamic_code?token=...&hours=2&count=2
