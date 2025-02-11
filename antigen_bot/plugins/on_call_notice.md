# 核心功能

按关键词触发预设回复，回复支持文本（必须）、图片（表情图）或视频（可选），并且可设定等待时间（秒为单位）

同一个群里发送"查询"，可以获得上一轮发送结果记录

# 特点

1、最低限度对触发指令的格式要求，只需要包含关键词和指定楼栋群组的数字就行，以上元素排列顺序不限制，中间用空格隔开即可；

2、支持连号指定，任意两个数字之间加-、——、：即可，例如3-27，代表3到27（包含3和27）

3、支持与现有MessageForwarder以及WatchRoomTopic两个插件的同时部署

# 效果

![img](/asset/Collage_20220424_201527.jpg)

![img](/asset/Collage_20220424_201634.jpg)

# 具体使用

1、侦测"工作群"中或指定联系人的特定格式消息（key_words和楼号数字的任意组合），进行预设通知内容的触发

2、应用于"[团购送达](https://github.com/ShanghaiITVolunteer/AntigenWechatBot/issues/25#issuecomment-1104817261)"、
"[核酸提醒](https://github.com/ShanghaiITVolunteer/AntigenWechatBot/issues/25#issuecomment-1104823018)"等需求场景

3、配置文件：.wechaty/on_call_notice.json(存储keyword已经对应的回复文本（必须）、群聊名称pre_fix(必须）、回复媒体（存贮在media/）以及延迟时间）

# 注意：

1、注意规避与其他插件（如MessageForwarder）的配置干扰，比如指定同一个人的对话适用于MessageForwarder和OnCallNotice，那么就可能产生误发（各个插件在业务逻辑上是独立的）；

2、OnCallNotice优先判定群。即某个有权限触发通知的人如果在有权限触发通知的群内发消息，实际触发以群内设定为准；

3、对发送目标群（一般来说是居民群）的群名有一定要求：同一小区的各群名称必须包含固定元素，该元素需要存储在config文件中的"pre_fix"字段下， 且pre_fix与用于标识具体楼栋的关键字之间要至少间隔一个
非数字字符，同时标识关键字之后也必须跟至少一个非数字字符。

比如：

**ok**：xx小区25号群、共克时艰xx小区别墅群、xx【业主】8号（其中xx为标识该小区的统一名称，即pre_fix)；

**Nok**：25号群xxx小区（标识关键词前缺乏非数字字符），别墅群（没有小区标识）、xx【业主】8（标识关键词后缺乏非数字字符）；

我们已经最大化降低对群聊命名格式的要求了，上述例子中Nok部分即便是人类也容易搞错。

**on_call_notice.json的参考示例：**

{"19310048281@chatroom": 
{"pre_fix":"test", 
"送达":{"reply": "团购物资已到，错峰下楼取货喔~", "media": "notice_xiaodu.jpeg"}, 
"准备":{"reply": "还有两栋楼就轮到我们做核酸了，请合理安排时间", "hold": 15}}}
