

# Charles抓包\(iOS的http/https请求\)

---

* Charles安装
* HTTP抓包
* HTTPS抓包

#### 1. Charles安装

官网下载安装Charles:  
[https://www.charlesproxy.com/download/](https://www.charlesproxy.com/download/)

#### 2. HTTP抓包

###### （1）查看电脑IP地址

![](http://upload-images.jianshu.io/upload_images/2469183-ff851ce2abe6cfe8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



###### （2）设置手机HTTP代理

手机连上电脑，点击“设置-&gt;无线局域网-&gt;连接的WiFi”，设置HTTP代理：  
服务器为电脑IP地址：如192.168.1.169  
端口：8888

![](http://upload-images.jianshu.io/upload_images/2469183-ad19fa10a1815cbc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


设置代理后，需要在电脑上打开Charles才能上网

###### （3）电脑上打开Charles进行HTTP抓包

手机上打开某个App或者浏览器什么的，如果不能上网，检查前面步骤是否正确

![](http://upload-images.jianshu.io/upload_images/2469183-8630cf0087d20187.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


点击“Allow”允许，出现手机的HTTP请求列表

![](http://upload-images.jianshu.io/upload_images/2469183-874a256420dcae1f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


HTTP抓包

#### 3. HTTPS抓包

HTTPS的抓包需要在HTTP抓包基础上再进行设置

设置前抓包HTTPS是这样的  


![](http://upload-images.jianshu.io/upload_images/2469183-81c9d7cd686f86eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


设置后抓包HTTPS长这样  


![](http://upload-images.jianshu.io/upload_images/2469183-3b9210f6ea4c6403.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


![](http://upload-images.jianshu.io/upload_images/2469183-c83e45626a1cb35e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


> **以下为在HTTP抓包基础上进行HTTP抓包的进一步设置步骤:**

###### （1）安装SSL证书到手机设备

点击 Help -&gt; SSL Proxying -&gt; Install Charles Root Certificate on a Mobile Device

![](http://upload-images.jianshu.io/upload_images/2469183-8f47a1b1c1540ef7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


出现弹窗得到地址[chls.pro/ssl](http://www.jianshu.com/p/chls.pro/ssl)

![](http://upload-images.jianshu.io/upload_images/2469183-c7f6ad4a204b0bd4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


手机安装SSL证书的地址

在手机Safari浏览器输入地址[chls.pro/ssl](http://www.jianshu.com/p/chls.pro/ssl)，出现证书安装页面，点击安装  
手机设置有密码的输入密码进行安装

![](http://upload-images.jianshu.io/upload_images/2469183-7ed4a5c8c2a36217.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


安装证书

* _注意1：_
  有兄弟姐妹说Safari浏览器输入这个网址
  [chls.pro/ssl](http://www.jianshu.com/p/chls.pro/ssl)
  安装不了证书的情况,
 
  亲测要\(1\)设置好手机HTTP代理 \(2\)电脑上Charles要开着
* _注意2：_
  iOS 10.3系统，需要在
  _设置→通用→关于本机→证书信任设置_
  里面启用完全信任Charles证书
 
  （这里感谢
  [@13002171223](http://www.jianshu.com/users/d4b6b76e81da)
  的提出这点 ，之前没升级10.3哈）

###### （2）Charles设置Proxy

Proxy -&gt; SSL Proxying Settings...

![](http://upload-images.jianshu.io/upload_images/2469183-2c460b4652797ccf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


勾选Enable SSL Proxying,点击Add

![](http://upload-images.jianshu.io/upload_images/2469183-11eb2be75eae13fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


Host设置要抓取的https接口，比如想抓这个  


![](http://upload-images.jianshu.io/upload_images/2469183-b39831342a11daca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


  
Host填写：[https://api.weibo.cn](https://api.weibo.cn/)  
Port填写：443

![](http://upload-images.jianshu.io/upload_images/2469183-ca37de9cdb920511.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


###### （3）进行HTTPS抓包

让手机重新发送https请求，可看到抓包

![](http://upload-images.jianshu.io/upload_images/2469183-5f1b21912781d466.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  


HTTPS抓包

注意：不抓包请关闭手机HTTP代理，否则断开与电脑连接后会连不上网  
_----愿您有所收获~ end_

---

郑重提醒， iOS10.3的真机抓包https， 在手机设置，关于本机，最下边有一个证书信任，必须打开charles的证书信任，才能抓包，而且，挂证书的api貌似抓不到包，只显示❌， 只有不挂证书的才能抓到



[AceSheep](http://www.jianshu.com/u/5771c9457880)：挂证书的API 会显示证书错误 有中间人之类的不发送任何数据



[xinyiheng518](http://www.jianshu.com/u/8f6ad2a186d7)：[@13002171223](http://www.jianshu.com/users/d4b6b76e81da)挂证书？是指服务器端有证书给客户端认证？



[半块](http://www.jianshu.com/u/6a16bd6f1d06)：10.3 确实是这样 之前的系统OK 不用信任证书



[Roy\_Liang](http://www.jianshu.com/u/7ebfb6ae1f6b)：[@jia611](http://www.jianshu.com/users/2da1e516025c)图文所示就是抓APP的。要注意设置手机HTTP代理，HTTPS的话要另设置证书，Proxy，接口名（见图）。就算是加密了，如微信、QQ，起码网络请求接口能看见，weixin...什么什么的



[Roy\_Liang](http://www.jianshu.com/u/7ebfb6ae1f6b)：[@男儿心](http://www.jianshu.com/users/1b366104ddc7)并没有，有的只能看到接口名，而内容是被另外加密处理过的，看到的是一堆乱码，如某Q、某信





[Roy\_Liang](http://www.jianshu.com/u/7ebfb6ae1f6b)：[@李白不读书](http://www.jianshu.com/users/8e8e3494aad5)有一些进行了内容加密，比如某心、某Q。请求request跟response都被加密成一堆乱码了。  
不知道你说的“抓了之后还是抓不出来”，是返回内容没出来，还是请求没出来，还是出来了一堆乱码





HTTPS抓微博的是成功了，但是别的都不成功，话说端口443是怎么来的，发现端口是非常重要的一环哦

[Roy\_Liang](http://www.jianshu.com/u/7ebfb6ae1f6b)：查了下，HTTPS的SSL一般使用443端口，默认的，当然也是可以修改的

[扇子飞舞](http://www.jianshu.com/u/69974eb4c586)：[@Roy\_Liang](http://www.jianshu.com/users/7ebfb6ae1f6b)谢谢回复，我也发现了，确实大部分的是443端口，不知道有些不是443端口的可有解决办法呢？

[Roy\_Liang](http://www.jianshu.com/u/7ebfb6ae1f6b)：[@扇子飞舞](http://www.jianshu.com/users/69974eb4c586)试了下，把端口名去掉也可以抓到微博的。但是随便填其它的就不行了。



如果是私有证书，能抓到么？

[Roy\_Liang](http://www.jianshu.com/u/7ebfb6ae1f6b)：测试了自己弄的自签名证书HTTPS，也可以抓到  
需要在Proxy -&gt; SSL Proxying Settings...添加抓包ip地址，如我自己电脑的服务器的是192.168.1.112



