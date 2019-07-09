## SSPanel DOCKER版

特点：

- 镜像模式类似wordpress、typoehco、nextcloud等，抛弃臃肿的LNMP，镜像极简。
- 更轻量、更快、也更安全。
- 完整镜像体积仅仅275MB，源码可挂载本地

## 部署方法

### 一键脚本（推荐）

集成docker环境和docker-compose环境检测及安装，适配Centos、Debian、Ubuntu等系统。
提供两种版本：

- 稳定版每月同步master分支
- 开发版每月同步dev分支

```
bash <(curl -L -s https://raw.githubusercontent.com/Baiyuetribe/ss-panel-v3-mod_Uim/dev/sspanel.sh)
```

脚本结束后会提示如下内容：

- sspanel主程序：http://ip:666
- kodexplore文件管理器：http://ip:999
- 默认源码路径：`/opt/sspanel/code`
- 默认数据库路径：`/opt/sspanel/mysql`

修改宿主机源码，可实时同步容器内文件。

![]（https://img.baiyue.one/upload/2019/07/5d21bb61ae931.png）

### 手动部署

稳定版（master分支）：

```
wget https://raw.githubusercontent.com/Baiyuetribe/ss-panel-v3-mod_Uim/dev/Docker/master/docker-compose.yml
docker-compose up -d
```

开发版（dev分支）：

```
wget https://raw.githubusercontent.com/Baiyuetribe/ss-panel-v3-mod_Uim/dev/Docker/docker-compose.yml
docker-compose up -d
```

部署完成后，主要内容如下：

- sspanel主程序：http://ip:666
- kodexplore文件管理器：http://ip:999
- 默认源码路径：`/opt/sspanel/code`
- 默认数据库路径：`/opt/sspanel/mysql`

之后执行剩下的相关命令：

```
docker exec -it sspanel sh		#进入sspanel容器
php xcat createAdmin		#创建管理员账户
php xcat syncusers		#同步用户
php xcat initQQWry		#下载ip解析库
php xcat resetTraffic		#重置流量
php xcat initdownload		#下载客户端安装包
exit		#退出
```

执行 `crontab -e` 命令, 添加以下四条（定时任务配置）：

```
30 22 * * * docker exec -t sspanel php xcat sendDiaryMail
0 0 * * * docker exec -t sspanel php -n xcat dailyjob
*/1 * * * * docker exec -t sspanel php xcat checkjob
*/1 * * * * docker exec -t sspanel php xcat syncnode
```

## 备注：

稳定版与开发版不可共存。

- 卸载命令：`docker-compose down`
- 删除本地缓存源码：`rm -rf /opt/sspanel`

脚本作者：azure 更多优质web资源，请参考：[佰阅部落](https://baiyue.one)




**ss-panel-v3-mod**是一款专为shadowsocks设计的web前端面板，再次感谢ss-panel-v3-mod 的制作者，修改后的功能简介：

- **支付系统集成**：集成 支付宝当面付  易付通 码支付 TrimePay 等多种支付系统，使用方法见项目[wiki](https://github.com/NimaQu/ss-panel-v3-mod_Uim/wiki/)
- **UI** ：修改为 ~~援交~~ 圆角、并自定义了几个图标的显示，节点列表等級0可见等級1节点但无法看见节点详情，增加了国家图标显示
- **商店**：商品增加同时连接设备数，用户限速属性
- 从肥羊那里**抄**来的：新用户注册现金奖励|高等级节点体验|设备数量限制
- **优化**：css和js等置入本地提升加载速度
- 增加**v2Ray** 功能，详情请看 wiki: [Indexyz 版](https://github.com/Anankke/ss-panel-v3-mod_Uim/wiki/v2ray---indexyz-%E7%89%88%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B)  |  [Rico 版](https://github.com/Anankke/ss-panel-v3-mod_Uim/wiki/v2ray---Rico-%E7%89%88%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B)

Telegram 频道 ：https://t.me/sspanel_Uim

Telegram 非官方水群 ：https://t.me/SSUnion

演示站: [sspanel.host](https://sspanel.host) 账号和密码都是 admin  对接节点的 mukey=NimaQu

**原作者** [galaxychuck](https://github.com/galaxychuck)

[支持开发者请点我](https://github.com/NimaQu/ss-panel-v3-mod_UIM#%E5%85%B3%E4%BA%8E%E6%8D%90%E8%B5%A0)

## 搭建教程

GitHub Wiki : https://github.com/NimaQu/ss-panel-v3-mod_Uim/wiki/%E5%89%8D%E7%AB%AF%E5%AE%89%E8%A3%85

Wiki已经启用，欢迎为此面板维护wiki

#### 鸣谢

##### [galaxychuck](https://github.com/galaxychuck)

- 面板**原作者**

##### [hkserversolution](https://www.hkserversolution.com/cart.php)
- Demo 演示站服务器赞助

##### [dumplin](https://github.com/dumplin233) 

- 码支付对接 + 码支付当面付二合一
- 为面板加入 AFF 链接功能
- 商品增加限速和限制 ip 属性
- 多端口订阅
- 解决用户列表加载缓慢历史遗留问题

##### [RinSAMA](https://github.com/mxihan)

- 整理分类 config.php
- 美观性调整
- 客服系统优化

##### [miku](https://github.com/xcxnig)

- 美观和性能优化

##### [Tony Zou](https://github.com/ZJY2003)

- 为公告增加群发邮件功能
- 节点负载情况显示&用户账户过期在首页弹窗提醒
- 增加返利列表

[**Indexyz**](https://github.com/Indexyz)

- 为面板增加 v2Ray 功能

[**NeverBehave**](https://github.com/NeverBehave)

- 添加 Telegram OAuth

[**CGDF**](https://github.com/CGDF-GitHub)

- xcat一键update
- 适配SSD
- 用户列表分页加载

[**CHEN**](https://github.com/ChenSee)

- 免签约支付宝与微信，自带监听，不需第三方软件，直接到个人账户

[**laurieryayoi**](https://github.com/laurieryayoi)

- 重做美化UI（~~援交~~圆角化）

- 重写节点列表，支持分级显示所有级别节点

##### 还有所有被引用过代码的同学，以及所有提交过issue的同学。

#### 关于捐赠

您对我们的帮助将是支持我们做下去的动力，只需您在购买部分产品或向他人推荐产品时从我们的返利链接购买，这就是对我们很大的支持了。~~没有钱了，肯定要做啊，不做没有钱用啊，打工是不可能打工的，这辈子不可能打工的~~


##### dumplin

- [码支付-微信收款功能开通](https://codepay.fateqq.com/i/39756)

##### galaxychuck

- [黛米付-支付接入](https://www.daimiyun.cn/register.php?aff=624)
- [冲上云霄云主机](http://console.soar-clouds.com/aff.php?aff=94)
- [Vultr](https://www.vultr.com/?ref=7205737)

[laurieryayoi 的前端课程报名](https://t.me/kinokonominoco)



## 免责声明

本程序由 MIT License 授权。**不提供任何担保**。使用本程序即表明，您知情并同意：程序开发者不对此程序导致的任何服务中断、数据损失或任何少见未列出的事故负责。
