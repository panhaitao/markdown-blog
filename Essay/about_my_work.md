# 关于系统和运维的思考

    从2011年来北京工作至今，历经中标软件，浪潮电子，知道创宇，深度科技，主要从事Linux服务器发行版的制作，维护，以及一小段运维工作的经历，在北京也工作生活了7年多，反观我的职业生涯，对服务器操作系统发行版，运维工作本身的理解也逐渐在改变甚至是重新认知！
    
    在中标软件，浪潮电子 ，深度科技这类公司，服务器产品并不需要太多的研发工作，主要做的是改皮换面，工程支持类的工作，因为LINUX服务器系统本身就是成熟的，而这类公司基本是以党政军机关的项目为主，这类项目特点就是为一群人傻，技术戳，事多的群体服务，这类项目基本是配以采购高性能服务器，光纤存储，IOE等企业级软件套间为主，项目方案很少出现性能瓶颈，出现比较多的raid卡，HBI卡，存储，服务器显卡等硬件适配类的问题，特别是后期在深度科技，我基本一个人就可以支持从debian8，到debian9，从centos6.4，centos6.8 到 centos7.4版本的系统层面的问题，甚至可以说在深度科技工作到两年左右的时候，并无太多实质性工作可用，其中还包括LSB认证，移植DDE桌面等大量不得不做的无用功。

    关于运维的思考，我只在知道创宇有过一年半的运维经历，从部署到上线，到监控到应急相应，运维管理的内容包括，公司内网，线上CDN节点，云平台服务器，编写插件，运维平台建设改进等工作，涉及的服务包括，bind，nagios，Nginx，redis，zabbix，exim等基础服务，saltstack配置库编写，等运维初，中级水平的工作，这段初级运维工作给了我很大压力和挑战，甚至导致出现失眠，脱发，耳鸣的症状，这些直到我离开知道创宇到了深度工作的初期才有所缓解。
  
    随后的几年，我虽然一直在重复做着服务器发行版的工作，但是也在关注的运维的发展方向，但是我依旧对运维这份工作的前景理解有限，总是停留在知道创宇那段痛苦的工作经历，当我最近开始面试换工作的时候，我逐渐体会到运维工作不是我或者到多数人眼里想象的的那么简单和肤浅：
   
    启蒙教育    ：运维团队人数：1-3人，需求，运维开发，整合对接云平台和开源套件
    到家美食会：运维团队人数：8-10人，具体需求不是很明确，没有得到技术负责人的面试
    ADmaster  :   运维团队人数：8-10人,  招聘3-5人的基础架构团队，具有云系统开发经验的人，
    智联招聘   ： 运维团队人数：20人，期望招聘具有丰富调优经验的人才，比如KVM的IO吞出，RPC调用，Docker网络吞吐性能调优等  

    从面试能得知的信息是，运维的初级阶段是简单安装部署等机械劳动，中级阶段是部署自动化，配置自动化，运维系统建设与开发，高级阶段又回到了底层的性能调优，BAT这类大型互联网公司还要应对海量高并发的挑战！

    2018年5月，我入职灵雀云做了一线做实施交付的，2018.5~2019.11, 一年零8个月，从最初对容器领域的浅薄理解，到入门和算是略微熟悉，磕磕碰碰的支持了很多项目，直到最近开始能支撑起光大项目的大部分现场工作，也发现自己走到当下技术成长的尽头，这点可能是灵雀这类创业公司的特点吧，产品架构一直在变，版本一直在发，重复的bug不断，救火不断，说是做的是现场运维工作，其实做的更多的是现场QA，测试，现场修正文档，加班加点忙不完的杂活，感觉是一个魔咒般的死循环，是时候该考虑换个环境看看外面的世界了：
   今日头条：iaas解决方案工程师，这个岗位关注网络，关于对底层技术的深度，和具备较好的开发能力
   慧科教育：资深运维架构，他们想做一个基于阿里云底层技术+ Rancher Paas平台 融合kvm，docker 和 k8s 做一个所谓的超融合云的产品，主要面向教育领域

 
# 关于IaaS PaaS 的思考

## 开源技术

* 开源技术发展期，因为趋势所在，有预期的价值所在，早期参与的商业公司会获得更多的商业机会和利润，一旦某项技术成为事实标准，生存下来的只有垄断市场的公司
 比如： linux 早期存活下来的以客户服务为商业公司RedHat 次之有 Suse ubuntu， 其他公司不会有更多的生存空间
* 在云计算的早期，商业的有vmware，开源的有openstack，随着云计算领域的成熟，单纯的以openstack为基础的第三方公司几乎消失，剩下了硬件捆绑销售云服软件的公司，华为，浪潮，曙光等等
* 在解决了IaaS，随意着业务应用的公共模块，框架，数据库，存储，消息队列，缓存的解耦，下沉形成了操作系统之上，业务应用之下的Paas，也或者叫中台
* 随着DevOps理念的发展，Docker的诞生，K8S的一统天下，形成了各种容器云的paas，或许未来操作系统虚拟化和应用虚拟化会相互融合
* 容器平台不能作为单一存在，需要对接大量基础设施，操作系统虚拟化，应用虚拟化，软件定义存储，软件定义网络，需要一个统一，也就是全栈云概念的诞生，一站式服务，从操作系统，到网络，到存储，到应用架构，从开发到运维


##  关于交付，售前，售后

交付，是在已有的边界，把交付以后的产品，部署，运维，技术支持，至下而上的工作
售前，或者叫售前方案架构，需要站在更高的视角，把控客户的需求，竞品的差异，市场的因数，人的因数来制定客户方案，需要一种趋势判断能力，控盘能力，具备一定的销售能力
解决方案架构师：一个真正解决方案架构师一定不是售前，不是拼命的强推给客户产品和服务，那就成了存粹的销售了，架构师要能捕捉理解客户的痛点，给出切合实际的技术方案，为客户提供所需的产品服务组合，架构师的最大价值在于能够做出正确的技术趋势判断，并促使其落地!

## 一个公有云厂商的困境

A售前: 有次 一个iass研发负责人 还居然和我们说 不要给客户推容器 这样云主机就会卖的少了   。。。
B产品: 哪个 [发呆] 我找他打一架 ==
A售前: 他的只是理解问题，他觉得客户冲虚拟机切换到容器集群，主机总量就会减少，但是他没有看到好多用户本身就是容器化了，
B产品: 只是直接docker运行，还是k8s集群调度的问题，用了容器化，DevOPS 微服务。日志，监控，附带的东西一直都不少，还有最核心的，客户用多少资源是取决于我们能服务什么体量的客户群体，是客户的业务体量决定的，和本身技术无关;反而是我们的paas saas类弱，很多客户想降成本，反而切不到UC，因为被其他友商运的 中间件，日志云监控。。。 这些绑死了 我们无法提供对应服务，比如上周我们见的一个客户 生产环境k8s集群需要用5000核心的计算资源，但是他们重度依赖阿里云的SLS !!!
A: 这个的确是的,一些我们看来可有可无的东西最后都是卡脖子的

