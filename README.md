# prometheus-webhook

---
用于prometheus webwook接口报警。该服务主要是云片网的接口短信报警和邮件报警。必须要添加告警组，将用户添加到告警组中即可。报警的时候是以组为单位。db用的是sqllite. 简单易用。其他的报警抑制 沉默就靠prometheus了。

---
### Install：
 ```
 git clone https://github.com/prometheus-zh/prometheus-webhook.git
 cd prometheus-webhook 
 pip install Pillow
 python manage.py migrate
 python manager.py syncdb # 设置登录admin的账号密码 
 python runserver 0.0.0.0:8080 启动服务
```


### 配置项

* 云片网短信密钥: 配置云片网api的key。（如果在云片网中开启了白名单，还需要配置允许本机的公网Ip能访问）

* 邮件账号配置:配置一个可以发送邮件的邮箱账户

* 微信公众号配置：corpid是企业ID,corpsecret是应用的凭证密钥,详情参见https://work.weixin.qq.com/api/doc

* ip白名单:需要在Ip中配置允许哪些Ip地址访问告警接口

* 告警用户:添加需要被告知的用户，需要配置邮箱和手机号码，微信号并且配置到所属的告警组中

* 告警组:配置告警组（告警的发送都是基于组形式，所以必须配置好组，将用户添加到组中即可）

* 日志:分别记录了短信，微信和邮件的发送状态日志和时间

### 调用告警接口



* 首先需要配置ip白名单，允许调用。
* 接下来按照格式发送到接口,prometheus alertmanager 传送给webhook也是这些json，这个web服务只是对json做了解析
post json方式按照下列格式传入 
```
{"receiver":"receiver_name",\
alerts:{"annotations":{"description":"game over one"},"annotations": {"description":"game over two"}}
```

* 短信和邮件接口地址：http://XXXXX.com:8080/sendmessage/ 
* 微信接口地址：http://XXXXX.com:8080/sendmessage/wechat
* 该服务的db是用sqllite，所以如果单独出去跑的话，需要把sqllite数据文件挂载出来
---
# 对了 我这里卖新疆阿克苏冰糖心苹果,感兴趣加微信 18612615725 请注明买苹果 否则不加哈
---

