---
title: "HW行动"
subtitle: ""
date: 2022-04-28T18:43:21+08:00
draft: false
author: ""
authorLink: ""
authorEmail: ""
description: ""
keywords: ""
license: ""
comment: false
weight: 0

tags:
- HW
categories:
- 安全

hiddenFromHomePage: false
hiddenFromSearch: false

summary: ""
resources:
- name: featured-image
  src: featured-image.jpg
- name: featured-image-preview
  src: featured-image-preview.jpg

toc:
  enable: true
math:
  enable: false
lightgallery: false
seo:
  images: []


# See details front matter: https://fixit.lruihao.cn/theme-documentation-content/#front-matter
---

<!--more-->
## HW行动的前世今生

### 国外网络安全攻防演习

1. 锁盾（北约）
2. 网络风暴（美国国土安全局）



### HW行动发展

1. 2016试点（无经验、担心出问题）
2. 2017扩展（监管利器，被监管单位认识不足）
3. 2018认可（头部企业认可，部分行业开始组织演练）
4. 2019普及（强信息化机构，普偏尝试实战演练（开始使用0day））
5. 2020推广（扩大演练覆盖面，向常态化转变（更多0day））



### HW行动网络攻防演练

1. 时间2-3周
2. 特点：高度仿真APT



### 记分规则

1. 权限获取
- 账号权限——主机权限——重要系统权限
2. 边界突破
- 逻辑隔离——物理隔离——生产网
3. 靶标系统
- 目标系统——核心业务——核心数据
4. 记分注意事项
- 发现并处置攻击，提交报告可加分，但加分小于扣分
- 溯源攻击者身份可额外加分
- 总结报告分数有一定占比

## HW行动攻击之道

### 哪里信息多就往那儿打

1. 子域名探测（通过banner指纹，发现是国产OA系统，找出历史漏洞Nday）
2. 漏洞挖掘（SQL注入、获取WebShell）
3. 内网信息收集（OA系统邮件、包含VPN账号）
4. 内网扫描、横向扩展（利用永恒之蓝、struts2、weblogic等漏洞）
5. 纵向扩展（多网卡机器、监控摄像头、核心专网）



### 改造内网系统钓鱼，防不胜防

1. 资产收集（获取资产列表）
2. 漏洞挖掘（某系统存在已知漏洞）
3. 内网扫描与横向扩展（利用一直漏洞入侵OA系统）
4. 下载钓鱼（伪造OA系统组件密码，提示用户下载，感染用户主机）
5. 内网信息收集（大量信息获取，比如文档）
6. 纵向扩展（控制单向网闸）



### 稳步前进，步步为营

1. 资产收集（获取资产列表）
2. 漏洞挖掘（利用1day漏洞突破边界，进入DMZ区）
3. 横向扩展（利用未授权、弱口令登录多台内网主机）
4. 内网信息收集（在已控机器上抓取其他账号口令。获取通用账号和域控账号）
5. 内网漫游（用抓取的账号登录多台内网主机和域控）
6. 纵向扩展（利用内网1day漏洞跨入生产网）



### 不能忽略的终端设备

1. 信息收集（获取智能终端固件）
2. 漏洞挖掘（逆向发现溢出漏洞，获取终端root权限）
3. 内部信息收集（终端输出内容从内网主机获取）
4. 内网漫游（获取多台内网服务器）
5. 实现目标（控制诸多用户终端）



### 钓鱼还有用吗？

1. 漏洞挖掘（发现存在邮件伪造漏洞）
2. 鱼叉攻击（尝试对客服、HR等人员进行邮件钓鱼（伪造VPN页面，诱使非技术人员进行登录；给HR发包装过的简历木马；WiFi劫持，大菠萝wifi））
3. 内网漫游（使用获取到的密码，成功进入内网）
4. 钓鱼攻击（使用获取到的人力资源帐号，尝试对运维人员进行攻击）
5. 内网漫游（使用运维人员个人PC收集的信息，在内网进行漫游）



### 攻击者视角

1. 攻击目标选择
- 脆弱资产
  - Weblogic、Spring、Structs2等已经出现问题比较多的组件、框架（引用了不安全的组件、类库等并利用1day）
  - 邮件系统或一些外网被忽略的资产（测试页面、测试系统等）
  - 企业间的通用系统或关键合作方的资产
- 安全意识缺乏
  - 具有弱口令的OA或者VPN
  - 个人手机或主机
  - Github、网盘、文库等引起的信息泄露
2. 攻击流程
- 信息收集
- 初始入侵
- 站稳脚跟
- 提升权限
- 内部信息收集——>横向移动——>维持现状——>提升权限
- 完成目标
3. 粮草先行
- 人：个人基础信息、员工通讯录、社交账号（邮箱、手机、账号）、社交关系、互联网泄露信息、角色关系（客户、员工、供应商、合作方）
- 信息资产：域名/IP、内外网拓扑结构、端口、使用软件、使用网络设备、关键系统（邮箱、OA、VPN、域控）、关联合作方资产
4. 攻击武器
- 工作人员安全意识：弱口令、撞库、泄露账号、钓鱼、物理入侵
- 内网中已知漏洞利用：积累漏洞利用库
- 0day漏洞攻击：方程式小组武器库
- 钓鱼攻击
  - 口令钓鱼
  - WiFi钓鱼
  - Drive-by-download
  - 利用漏洞：文档、压缩包、恶意网页
- 远程入侵与本地权限提升
  - Web应用漏洞
  - 通用组件与框架漏洞
  - 网络设备漏洞
  - 供应链漏洞
  - 内核漏洞
  - 不安全的服务提权
5. 攻击强化
- 维持与后门
  - 远控功能
  - 敏感信息收集功能
  - 漏洞利用能力
  - 蠕虫特性
  - 目标业务实现
  - 免杀与流量加密

## HW行动的防守之道

### HW安全防护体系

1. 安全流程控制（40%）
- 网络安全保障方案：事前筹备、事中保障、事后总结
2. 安全技术保障（与工具支撑一起40%）
- 应急保障：应急响应，预案之类
- 安全基线检测：最基础的安全检测，把初级、最基础的漏洞弱口令等进行完善
- 人员意识检测：弱口令、安全意识培训、防守团队安全意识培训
- 安全测试：常规的渗透，HW前进行攻防演练，1day和Nday进行检测
- 安全加固：业务系统无法根本解决，则可通过技术手段、安全设备进行防范
- 安全运维：业务迭代更新中也要进行安全规划
3. 安全工具支撑
- IPS、WAF、IDS、防火墙、蜜罐、全流量检测、APT、HIDS、SIEM等
4. 安全能力提升（20%）
- 安全意识培训、安全工具培训、应急流程培训、配置核查培训



### HW防守中的安全技术手段

1. 信息收集：资产梳理、敏感信息泄露排查
2. 工具检查：极限检查/配置核查、漏洞扫描
3. 渗透测试：外网渗透、内网渗透、安全意识测试
4. 攻防演练：找出可能被攻击的切入点
5. 专项检查：重要系统、重要漏洞/端口、重要网络区域、WiFi、弱口令、历史账号清理、违规外联检测
7. 应急响应：攻击研判、应急处置、溯源分析
8. 安全加固：漏洞修补、防护设备策略调优



###	安全设备布放思路：点线面立体防护（各个安全设备为点，安全设备连起来为线，收集汇总设备信息日志构成面）

1. 边界防护：IDS/IPS/WAF
- 明确内外边界、在内网边界上部署监测和阻断攻击的设备
- 对内部网络进行层层细分隔离，也在内网边界部署检测和阻断攻击的设备
2. 流量监控：全流量审计、APT检测
- 从网络流量角度，对流经内外网流量、以及内网之间的流量做记录和监测，弥补边界防护在内网横向流量检测方面的不足
3. 攻击诱捕：蜜罐
- 各内网区域部署陷阱，诱敌深入，及早发现并处置
4. 主机防护：HIDS
- 在主机上识别和检测入侵痕迹
5. 联防联控：SIEM
- 收集安全设备日志，联动监测并自动阻断



###	项目组织架构与职责分工

1. 领导层
- 信息安全工作领导小组——>管理协调小组
2. 执行层
- 后勤保障小组
- 风险监测小组：（汇报反应给研判处置小组）
  - 安全设备告警观测、初筛
- 研判处置小组：（汇报反应给管理协调小组）
  - 告警处置、策略完善、效果确认
  - 异常分析、攻击溯源
  - 防护报告编写、工作上报

## 攻防思路、工具-攻击思路与手段


###	需要收集哪些信息

1. 人：个人基础信息（姓名、出生日期、住址）、员工通讯录、社交账号（邮箱、手机、QQ、微信）、社交关系、互联网泄露信息、角色关系（客户、员工、供应商、合作方）
2. 信息资产：域名/IP、内外网拓扑结构、端口、使用软件、使用网络设备、关键系统（邮箱、OA、VPN、域控）、关联合作方资产



###	如何寻找突破口

1. 工作人员的安全意识薄弱
- 弱口令、撞库、泄露账号、钓鱼、物理入侵
2. 已知漏洞未修补，内网重灾
- 积累漏洞利用库
3. 以小见大，主站无洞可以从旁站入手
- XSS、CSRF、SQL注入、越权->获取管理员账号->上传、备份->后台getshell
4. 发现源码->审计漏洞
- 文件扫描、Github
5. 未公开0day漏洞



###	钓鱼攻击

1. 口令钓鱼：引导用户到URL与界面外观与真正网站几无二致的假冒网站输入个人数据（域名仿冒、中奖邮件）
2. 鱼叉式网络钓鱼：私人化定制，伪装成目标的同事或亲友等身份，诱导目标点击链接或者下载附件（word、vpn）。或伪装成领导，要求员工进行xx操作
3. 偷渡式下载（Drive-by download）
- 授权但不了解后果的下载（eg：安装未知或者伪造的可执行程序，ActiveX组件或者Java applet）
- 不知情的情况下进行的任何下载，通常是计算机病毒，间谍软件，恶意软件或犯罪软件
4. 热点钓鱼（WiFi钓鱼）
- 切断目标的网络，设置一个假的公开WiFi，目标一旦连入网络，所有的数据和操作都会被掌控
- 通过WiFi共享连入目标网络，发送泛红攻击
5. 搜索引擎钓鱼：付费广告（购买近似域名，提升权重）
6. 桌面钓鱼：修改hosts并制作成解压文件，捆绑其他软件，通过任意途径诱导用户安装



###	其他突破口

1. 社会工程学
- 伪造猎头身份，诱导目标员工下载work木马。根据个人信息，生成字典
2. DNS欺骗
- 破坏DNS记录，将目标网站的访客引至实现布好的欺诈网站（入侵路由器）
3. 水坑攻击
- 得知目标经常访问的网站后，攻击该网站，放置登录控件马
4. 物理攻击
- 水、电、网、空调维修人员冒充，提供U盘进行打印等



###	后门隐藏

1. webshell：回调后门、代码混淆和加密、不死马、无文件webshell
2. 计划任务、启动项、注册表
3. 增加UID为0、权限为Administrator的账户
4. ssh key

5. alias后门（.bashrc、/etc/profile）（先执行反弹shell再执行原命令）
6. suid后门
7. ssh后门：软连接后门、ssh server wrapper
8. pam后门
9. mafix后门
10. Kbeast_rootkit后门

###	内网渗透-选择攻击目标

1. 优先攻击高权限账号，如管理员，目标系统负责人账号
2. 优先攻击运维安全人员账号和终端，这些人往往有服务器root账号，安全设备管理员账号，可以进一步深入控制
3. 优先攻击集中管控设施，如域控，集中身份认证系统，终端管理系统，攻陷单系统即可获得公司呢大部分系统的权限
4. 优先攻击基础设施，如DNS、DHCP、邮件系统、知识分享平台、OA系统、工单系统；这些系统有内置高权限账号，或可以帮助攻击者隐蔽痕迹。或Git/SVN等开发源代码管理服务器，通过代码审计发现应用0day漏洞

## 攻防思路、工具-攻击常用工具

###	信息收集工具

1. 公司信息收集：天眼查、Github、各大搜索引擎
2. 个人信息收集：Telegram、QQ、微信、钉钉、支付宝、脉脉、Linkedin、贴吧
3. 端口扫描工具：nmap、zmap、masscan
4. 目录扫描工具：dirb、dirsearch、御剑、SourceLeakHacker、wwwscan、weakfilescan
5. whois/备案查询：站长之家、阿里云、备案查询
6. 历史域名解析记录：ViewDNSinfo、DomainTools、dnsdumpster、WhoISRequesr
7. C段收集工具：必应
8. 子域名收集工具：Layer子域名挖掘机、subDomainsBrute、Sublist3r、DNSDumper、IP反查域名、谷歌语法：site:baidu.com
9. 指纹识别：bugscaner、云悉、whatweb
10. 多地ping工具（CDN）：站长之家、爱站网、dnsenum、just-ping



###	绕过CDN查找真实IP

1. 查找二级域名（一般二级域名不会放CDN）
2. nslookup法（大部分CDN只针对国内市场），nslookup http://xxx.cn 国外dns
3. ping法，ping xxx.cn（有些CDN厂商基本只把www.xxx.cn cname到cdn主服务器上去。www.xxx.cn和xxx.cn是两条独立的解析记录，一般只会吧www.xxx.cn拿去做CDN）
4. 查找历史域名解析记录（使用CDN前是真实IP）
5. 内部邮箱源（必须是目标自己的mailserver）
6. 网站测试文件，phpinfo等
7. APP抓包



###	EXP、POC、漏洞扫描框架

1. exploit-db、乌云镜像库、vulhub
2. CMS-Hunter、AngelSword、onlinetools、Some-Poc-oR-Exp、exphub
3. struts-scan、wpscan、kunpeng、AWVS、appscan、nessus、xray



###	漏洞利用工具

1. SQLMap、BrupSuite、NoSQLMap
2. webshell：*webshell、webshell-sample、WebShell、php-webshells*
3. webshell管理工具：菜刀（后门）、蚁剑（RCE：1、2）、冰蝎
4. 内网渗透神器：Metasploit-Framework、Cobalt Strike（可克隆网站、制作word宏病毒、发送邮件）
5. Proxy：*ReGeorg*、EarthWorm、Termite、ProxyChains-ng、Proxifier、*Venom*、openvpn
6. 提权：*windows-kernel-exploits、linux-kernel-exploits、LinEnum*
7. 端口转发：Windows、Linux
8. 手机短信接收平台：*云端、materialtools、z-sms、receive-sms-online*
9. 在线临时匿名邮箱：*yopmail*
10. 在线邮件伪造：*EMKEI、小幻邮箱系统*
11. 在线短链生成：*站长之家、短网址工具*
12. 在线md5解密：*cmd5、zuwuwang、somd5、pmd5、chamd5、xmd5、ttmd5*



###	清理痕迹

1. 攻击过程做记录，拿到shell后清理日志
2. history -c

###	隐藏IP

1. 免费代理服务器

## 案例分析与总结

###	邮件安全

1. 邮件伪造漏洞、伪造脚本
2. 容易获得，有规律可行，并且是直接公开的，非安全非技术岗位更容易钓鱼
3. 邮件攻击手段
- 账号钓鱼：伪造一个和正常系统看起来很像的登录界，吸引受害人输入账号密码
- 鱼叉攻击：利用木马程序作为电子邮件附件，结合时事或者受害感兴趣方面的内容，诱导点击打开附件木马
- 结合浏览器、文档软件漏洞的高级鱼叉攻击：点击连接或者打开附件文档也可能中招
- 邮件社工：伪装成同事、领导给受害者发生邮件（发件人伪造技术或已入侵相关账号），索取敏感信息或下达特权操作
- 历史邮件信息获取：从已入侵的邮箱账号中查阅历史邮件信息，从中获取到员工通讯录、企业组织架构、账号密码、重要资产等信息
4. 邮件安全防范措施
- 重点警惕钓鱼邮件和木马
- 不要轻信发件人地址中显示的“显示名”
- 不要轻易点开陌生邮件中的链接或附件
- 不要放松对“熟人”邮件的警惕
- 对于附件，及时使用杀毒软件查杀，若是可执行文件，要通过其他方式确保邮件来源可靠，非执行文件也需谨慎，防止未知软件漏洞
- 若邮件索要敏感信息或要求进行敏感操作，直接询问相关人员确认最为保险
- 定期归档和清理历史邮件，尤其主义其中的敏感信息
- 发现中招异常后及时向安全人员报告，及时进行应急处置

###	数据安全：企业敏感信息泄露

1. 常见泄露源
- 网盘、微盘
- 代码托管平台（github）
- 文库平台
- 微博、论坛等社交网站
2. 常见泄露内容
- 企业组织架构
- 员工通讯录
- 供应商或合作方
- 源码文件
- 账号密码
- 技术方案
- 招投标文件
- 项目合同
- 网络拓扑
- 内部系统手册
3. 防范措施
- 禁止在互联网上发布公司内部信息

###	密码安全

1. 弱口令——小问题，大隐患

2. 什么是弱口令

- 字符种类不够，长度不够
- 系统/设备默认出厂口令
- 使用和个人或公司有关信息，例如生日、年份、公司名称等
- 键盘上连续按键（qwert、1qaz@wsx、！@#）
- 包含特殊含义字符串（520、1324、iloveyou）
- 其他常用字符串（root、abc123！、@123）

3. 什么是拖库

- 利用系统漏洞或者社工等手段直接获取被攻击目标的整个数据库，其中通常含有口令等大量敏感信息
- 大量数据库在暗网进行交易

4. 什么是撞库

- 由于大量人员在不同网站上使用相同的密码，使用已拖库或泄露的A网站数据库中的口令登录B网站

5. 通用密码

- 同一个密码可以登录多个机器/账号

6. ssh免密登录

- 若密钥所在机器被渗透，通过查看known_hosts则可直接登录开启免密登录的服务器

7. 密码安全防御措施

- 默认密码一定要修改
- 不要使用关联信息或通用信息（个人信息、公司信息、常见字符串）
- 加大密码强度，增加密码长度和字符种类（数字+大小写字母+特殊字符）
- 对系统重要性有清晰认识，对重要系统使用更强的密码
- 定期修改密码
- 不要将密码存放在任何地方（记录在邮件、在线笔记、或者写在便利贴并粘贴在办公区域）
- 二次认证能开则开
- 个人和工作密码完全分开

###	无线安全

1. WiFi钓鱼案例分析
- 在某攻防演练中，攻击者通过爬虫方式爬取完整的WiFi用户登录页面，通过伪造该页面，当该单位员工使用WiFi过程中，配置重定向为伪造的钓鱼页面，诱使输入自己使用的账户密码，从而窃取用户登录信息。攻击者在获取账号密码后，可以访问该公司内网中的生成网段和办公网段，造成的后果特别严重
2. WiFi渗透案例分析
- 渗透测试过程中，发现该公司的WiFi未设置密码，可以直接连接，但是连接后需要认证才可以上网，可以根据网络配置界面，判断出无线网络设备，使用网络嗅探工具进行密码嗅探，获取数百条网络认证的账号与口令。使用获取到的逐个测试，利用高权限账号进入网络，探测网络内其他重要资产，进行一系列后渗透工作，最终获取到很多重要系统权限
3. 无线安全防范措施
- 强化WiFi连接认证方式，防止出现无须认证即可连接的情况
- 实现WiFi无线网络与内网的物理隔离，防止攻击者通过WiFi对内网进行攻击
- 限制网络访问，采取MAC地址过滤方式，预防未知设备连接网络
- WiFi连接认证口令不使用弱口令，防止WiFi连接认证被破解
- 严格禁止在公司内部私设WiFi
- 严格禁止在公司内部使用WiFi共享软件

###	物理安全

1. 假冒电信维修人员
2. 复制工牌进入机房
3. 物理安全防范措施

###	U盘安全

1. Bad USB攻击：在控制器固件中写入恶意代码，该部分不可见，唯一对用户可见的是其大容量存储
2. U盘安全防范

###	软件安全

1. 漏洞军火商软件漏洞贩卖
2. 高价值0day漏洞
3. 老旧软件攻击（升级系统，及时打补丁，不适用老旧不再维护的系统）
- WannaCry
- Shiro反序列化（组件有漏洞）

###	通信安全

1. 电话、短信、微信诈骗工具

###	上网安全

1. 互联网钓鱼攻击案例
- 某次攻防演练活动期间，攻击对假冒防守方在微信公众号发布了一篇演练总结的文字，文章中呼吁各防守单位下载文末的漏洞审计补丁工具进行加固，其实此工具为木马，上百人中招，涉及十几个参演单位（也可以使用邮箱分享该文档，同时把木马程序伪装成文档文件）
2. 防范措施
- 不允许来源不明的程序和软件
- 重大保障期间不轻信网上信息，对互联网信息保持谨慎

###	外包安全

###	防守方十要十不要

1. 要注意邮件安全，不要点击、回复可疑的、陌生邮件
2. 要注意数据安全，不要私自在互联网上发布个人或者与单位有关的内容
3. 要注意通信安全，不要回复、相信可疑电话、短信
4. 要注意外包安全，不要将内部敏感信息提供给外包商
5. 要注意U盘安全，不要将重要数据拷贝到U盘或者使用来历不明的U盘
6. 要加强无线安全，不要连接陌生的无线热点，关闭单位内部无线
7. 要加强物理安全，不要让陌生人随意进出
8. 要加强密码安全，不适用弱密码，同一密码
9. 要加强上网安全，不要点击可疑网站，不要下载可疑的程序
10. 要加强系统软件安全，不要使用老旧版本的系统与软件

## HW安全设备布防-安全设备介绍及部署

###	安全设备介绍

1. IDS：入侵检测系统
- 设备特点：常通过旁路部署，属于审计类产品，对威胁不具备拦截性
- 部署特点：IDS产品采用的是旁路部署方式，镜像端口，一般直接通过交换机的监听口进行网络报文采样或者在需要监听的网络线路上放置监听探针
2. IPS：入侵防御系统
- 设备特点：分析传输层和网络层的数据，通过制定不同的规则和响应方式主动防御已知攻击，实施阻断各种黑客攻击，如缓冲区溢出、SQL注入、暴力猜解、拒绝服务、扫描探测、非授权访问、蠕虫病毒、木马后门、间谍软件等
- 部署特点：一般部署在区域和区域的连接处，部署方式多以串联为主
3. WAF：Web防火墙
- 设备特点：分析Web应用层数据，能够完整地解析HTTP，包括报文头部、参数及载荷。能够检测常见的Web漏洞，具备拦截告警功能
- 部署特点：通常采用串行接入，一般部署在Web服务器的前面的网络边界，用来隔离内外网
- *WAF 和 IPS的区别*
  - WAF部署在比较靠近应用服务器的位置，而IPS部署的比较靠前
4. 流量监控（APT、全流量监控、科来、360...）
- 设备特点：基于网络全流量分析技术，旁路采集、分析和存储所有的网络流量。通过回溯分析数据包特征、异常网络行为，对网络安全时间进行精准的定性分析
- 部署特点：通过探针的方式部署流量采集节点，然后再管理中心进行汇聚
5. 蜜罐
- 设备特点：通过部署一些作为诱饵的主机、网络服务或者信息，诱使攻击方对它们实施攻击，从而可以对攻击行为进行捕获和分析，了解攻击方所使用的工具与方法，推测攻击意图和动机
- 部署特点：部署在不同域之间，DMZ区、办公区、内网核心区是主要的布防位置，另外在分支机构、合作机构，域与域之间也应当部署相应数量的诱捕节点



###	自动化应急处置平台

1. 搭建原则
- 具备灵活的策略调整功能，能够根据预设的规则进行自动决策
- 具备丰富的告警日志收集能力，保证可以做更多维度的关联分析
- 根据收集到的日志，搭建具备实时动态展示功能大屏展示系统（态势感知）

## HW安全设备布防-防守单位风险现状分析

###	网络现状与风险分析

1. 边界互联网区
- 运营商接入主要指电信、联通专线接入；内联网接入主要指数据中心分支结构、下属分行单位、第三方合作机构专线接入；外联网接入主要指人行、银联、社保、资金清算中心等相关机构的接入
- 风险分析
  - 供应链攻击，直接通过运营商专线发起攻击
  - 第三方机构沦陷，通过专线打入边界外联区
  - 下属机构，各行沦陷，通过专线打入内联区

2. 外网业务区（DMZ区）
- 又称为互联网去，主要对外提供数据中心的业务服务，如该单位的招聘系统、客服系统、网上手机银行等
- 风险分析
  - 业务网站Web漏洞
  - 第三方开源及组件漏洞
  - 信息泄露、站点运维不当风险

3. 内网业务区
- 主要为整个数据中心提供基础服务工作，其他区域的大部分业务员服务器及核心数据均部署在此，根据数据的重要程度，该区域由分为核心内网区甚至核心专网
- 风险分析

4. 终端办公区
- 该区域主要为单位员工日常工作提供网络支持服务，用于访问连通OA、Mail、WiKi、内部论坛等
- 风险分析
  - 员工浏览钓鱼网站，办公电脑被攻击
  - 员工被水坑攻击，办公电脑被攻击
  - 攻击者物理攻击，获取办公电脑权限

5. 运维管理区
- 该区域主要为单位IT运维人员使用，部署有堡垒机、运维监控系统、IT资产管理系统等，方便运维人员进行日常的办公和业务切割
- 风险分析
  - 运维人员信息泄露，导致账号被窃取，直接获取大量系统权限
  - DMZ区被攻击，导致可以直接连接进入运维管理区
  - 运维不当导致网络把部分系统配置到互联网或办公网等区域
  - 区域内存在大量的弱口令、低版本组件、默认配置



###	整体安全需求分析

1. 重点防护
- 外网到DMZ区（互联网边界，打穿就进内网）
- DMZ区到核心内网区

#### 