1、服务器环境：java1.7<BR>
2、建议客户端环境：java1.7<BR>
3、所有jar已经过优化，并未混淆。依然可在一定程度上的反编译<BR>
4、如有侵权代码，请指明，我们将在最短时间内移除侵权代码<BR>
5、软件遵循LGPL原则：可以任意分发以及修改本代码，代码本身不得用于盈利；但可用作商业代码里面的支持部份，而本代码无论修改与否必需开源。<BR>
6、proguard.jar为免费优化java代码工具，保留压缩jar.pro、最大压缩jar.pro为配置文档<BR>
<BR>
框架的目标：去WEB化，打造安全的云计算下游框架。<BR>
先解释云计算上中下游的概念，云计算上游——平台。如阿里云、西部数据。<BR>
云计算中游——为其他服务提供服务。如京东云、天翼云。<BR>
云计算下游——直接为客户服务。各网站可以认为是云计算的下游，直接为客户服务。<BR>
解释完云计算上中下游的概念，再说说与web有哪些区别。<BR>
1、web是现在普遍采用的一种云计算方式，但web有先天的缺点：可匿名访问；这就直接为拒绝服务攻击埋下伏笔。HZS.Durian则只提供有限的匿名访问：索取服务器RSA公钥、向服务器递交AES密钥并获取会晤号，其他任何资源均不可匿名访问，为加强对客户端的限定埋下伏笔，提高了安全性。比如web必需对客户的每一个访问进行无差别提供服务，而HZS.Durian则是多角度的限定恶意访问，从框架本身就有了防范拒绝服务攻击的基因。这就直接造成下面的区别。<BR>
2、web必需穷极速度才能为更多的人提供服务；HZS.Durian则是提高服务的有效率为更多人提供服务。根本宗旨是不同的。好比中国的武术，一味的追求勇猛与狠，发展到宋末明初，就产生了太极拳：原来拳法完全不同的思路。<BR>
3、web由于历史原因，若实现集群就会遇到会晤（session）互通的问题；HZS.Durian则从建立就考虑了这个问题，所以可以轻松搭建集群，而不用考虑如何将会晤进行互通。<BR>
4、由于会晤互通的问题，web的负载就必需有个中央负载；HZS.Durian可以是多个对等的负载服务器。所以负载一旦停机，web就会大面积不可用，HZS.Durian则仅仅一部份不可用，而且可重新进入；无论从影响范围以及影响时间来说，HZS.Durian对用户影响小很多。<BR>
相比web，HZS.Durian有很多优点，但也有个缺点：未形成标准化。面对现在的形式，有两个解决办法：<BR>
1、写浏览器插件，让现在的浏览器可以访问HZS.Durian服务器<BR>
2、写客户端，直接访问HZS.Durian服务器。本人写管理软件，就用的这个方式，只不过是瘦客户端。<BR>
与web比较後，总结一下HZS.Durian的用途：<BR>
1、对安全要求较高的领域，比如各种管理软件、12306的订票、款项的支付等等。可以将这些业务由web分离出来，单独处理。<BR>
2、也有人用于web访问服务的处理，即内部框架。此时假定内网是安全的，没有必要进行安全处理了。<BR>
<BR><BR>
框架特点：<BR>
一、安全。<BR>
1、采用rsa2560握手<BR>
2、aes128数据传输<BR>
<BR>
二、降低恶意访问<BR>
1、单一客户端只能串行访问<BR>
2、限定单一客户端的访问频率<BR>
3、限定单一客户端发文长度<BR>
<BR>
三、无中心集群服务。对外提供负载均衡的服务器可以是多台，而不是一台；坏了一台，不会影响所有用户，只影响一部份用户。受影响客户重新启动程序即可。<BR>
<BR>
四、基于socket的框架，不支持http；不排除有人改造成功。<BR>
<BR>
五、仅有两个非常有限的可匿名访问资源，其他资源不允许匿名访问，所以也就无法作为web服务了。但用来作为安全要求较高的业务服务是没有问题的。<BR>
<BR>
<BR>
框架所处位置：<BR>
框架实现目标：<BR>
框架对客户端要求：<BR>
框架的技术实现：<BR>
握手过程<BR>
会晤过程<BR>
<BR>
<BR>
升级日记：<BR>
2014年05月14日<BR>
　　org.hzs.server　　　　限定客户端上传数据在1M以内<BR>
　　org.hzs.助记文本　　　修复未初始化错误<BR>
2014年05月15日<BR>
　　org.hzs.json　　　　　1、修复序列化时遇到空值的错误；　2、反序列化支持同级引用<BR>
　　org.hzs.Web_Client　　增加缓存资源的功能，进行本地浏览<BR>
2014年06月12日<BR>
　　org.hzs.server　　　　将bio模式改为nio模式，注册session尚未改成nio模式。<BR>
　　org.hzs.Web_Client　　将bio模式改为nio模式<BR>
2014年06月13日<BR>
　　org.hzs.server　　　　修正重复监聽注册session的错误，修正握手过程中的错误<BR>
　　org.hzs.Web_Client　　业务端口改为本地运算<BR>
2014年06月14日<BR>
　　增加示例<BR>
2014年06月19日<BR>
　　org.hzs.server　　　　修正非法申请服务时造成的拒绝服务。<BR>
　　org.hzs.Web_Client　　提高判断网路是否联通的速度<BR>
2014年06月22日<BR>
　　org.hzs.server　　　　修正分配任务时，因节点故障而超时的问题；修正获取负载节点时，未校验访问对象的问题<BR>
　　org.hzs.Web_Client　　修正推出软件，不退出托盘图标的问题<BR>
2014年06月26日<BR>
　　org.hzs.server　　　　在交换权重过程中，加入校验是否为集群内节点的代码<BR>
2014年07月08日<BR>
　　org.hzs.server　　　　1、修正了重复select连接。 2、节点死机时，业务处理可再次分配。<BR>
　　org.hzs.Client　　　　由Web_Client分离出来，专职处理通信<BR>