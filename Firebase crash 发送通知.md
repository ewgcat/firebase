# 背景

目前firebase目前只支持以下两种缺陷平台的主动推送通知，并不支持飞书消息推送

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8122b930062840d49205e5254999e8b5~tplv-k3u1fbpfcp-zoom-1.image)
## 解决

本文借助飞书的机器人webhook推送能力

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ba3e760050b445f2871da7b0900f3b81~tplv-k3u1fbpfcp-watermark.image?)
### 1.Firebase项目设置，开启提醒

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d3909a81d96045debca3fe6f9948376a~tplv-k3u1fbpfcp-zoom-1.image)

### 2.选择提醒订阅

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/06660e7f89b34e9c9f3800fb17109353~tplv-k3u1fbpfcp-zoom-1.image)

### 3.选择项目，开启Crashlytics的电子邮件提醒

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c15f709a72114a87aff97e3c0a705d7f~tplv-k3u1fbpfcp-zoom-1.image)

### 4.打开Gmail的邮件转发设置，并添加转发地址

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a131a6e678b64b42a7b570f69b725bd5~tplv-k3u1fbpfcp-zoom-1.image)

### 5.创建过滤器，将firebase的邮件转发到qq邮箱（其它国内邮箱也可）

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/51b68628ff8f4296ba34bdd7d2478551~tplv-k3u1fbpfcp-zoom-1.image)

### 6.开启qq邮件IMAP/SMTP服务，需要用到授权码

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/149027766d0442f0b8f2abeda370d2ba~tplv-k3u1fbpfcp-zoom-1.image)

### 7.创建飞书机器人，群添加自定义机器人，获取webhook

[相关文档：飞书消息卡片能力](https://open.feishu.cn/document/ukTMukTMukTM/uEjNwUjLxYDM14SM2ATN#-47bc3dd)

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/945eb9ac2a574b2eb3461ad12f54f828~tplv-k3u1fbpfcp-zoom-1.image)

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d229be0211ea45f0a4ba7a544fc4f745~tplv-k3u1fbpfcp-zoom-1.image)

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0c169d3ecdd845bc9064b234bcd9b00e~tplv-k3u1fbpfcp-zoom-1.image)

###  8.脚本定时任务检测邮箱里面的firebase邮件

相关脚本源码，引用文档

[Python 收邮件、读邮件、标记已读和删除邮件-逍遥峡谷](https://www.icoa.cn/a/891.html)

[Python自动化读取邮件基础代码讲解_早起Python-CSDN博客](https://blog.csdn.net/weixin_41846769/article/details/113864647)

不支持在 Docs 外粘贴 block

### 9.最终效果

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71032c692fba49fa9aaa81a4ac122030~tplv-k3u1fbpfcp-watermark.image?)

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3fe160c6a47943c892626918d18b8ab7~tplv-k3u1fbpfcp-watermark.image?)
