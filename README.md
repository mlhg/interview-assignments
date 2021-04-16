<<<<<<< HEAD <<<<<<<<
## u - 短网址平台 
以打造一个高性能，可快速部署的短网址服务平台<br>

短链接我们或多或少都使用过，所谓短链接就是根据较长的原链接url生成一段较短的链接，
访问短链接可以跳转到对应的原链接，这样做好处在于：
1. url更加美观，访问头更短，更快更安全；
2. 便于保存和传播；
3. 某些网站内容发布有字数限制，短链接可以节约字数。
<br>
我只为缩短你的超链接url，让你变得短短的，不。。。是你的url变得短短的。


对于把长网址生成的短网址等信息放在内存中，
我用了一个HashMap来储存，并加了一个队例，为了防止内存溢出，
我这边是1、定时清理HashMap中过期的对像。
2、同时HashMap设定了一个最大值，如果超过最大的值，则把最先加入的值移出并销毁。

gitee地址： <br>


## 系统说明：
- 基于 Spring Boot Redis实现的一个短网址平台
### 目前
- 支持web方式和api方式创建短网址
- 支持api解析短网址
### 后续
- 将支持web控制台进行动态配置进行管控
- 增加监控功能
- 支持更丰富的api操作

### 程序在本地正常跑起来之后，  api 文档地址：
http://localhost:8080/swagger-ui.html#
- ...


### 单体测试结果图
![效果图1](dockertest\jacocotest\one.png)
![效果图2](dockertest\jacocotest\two.png)
  
  

### Web方式运行效果图
![效果图1](dockertest\shorturlimages\用短地址查询长地址.png)
![效果图2](dockertest\shorturlimages\长地址生成短地址.png)
  
### API方式使用


- 接口使用样例1 (生成短网址)


post http://127.0.0.1:8080/url/generate

type application/json

body {
    "url":"https://www.baidu.com",
    "valid":14400
 }
参数说明：url 传入的长网址
        valid 有效时间（秒），默认6个小时，

{
  "code": 1,
  "success": true,
  "msg": "ok",
  "data": {
    "orgUrl": "www.baidu.com",
    "shortUrl": "http://127.0.0.1:8080/u/M7RJFj",
    "shortTarget": "M7RJFj",
    "validTime": 2160000,
    "createTime": 1618532639712
  }
}


- 接口使用样例2 (查询长网址)


post http://127.0.0.1:8080/url/queryLongUrl

type application/json

body {
    "shortUrl":"http://127.0.0.1:8080/u/M7RJFj"
 }
参数说明：shortUrl 传入的短网址
        默认6个小时

{
  "code": 1,
  "success": true,
  "msg": "ok",
  "data": {
    "orgUrl": "www.baidu.com",
    "shortUrl": "http://127.0.0.1:8080/u/M7RJFj",
    "shortTarget": "M7RJFj",
    "validTime": 2160000,
    "createTime": 1618532639712
  }
}
  
### 核心依赖
  
  | 依赖                   | 版本          |
  | ---------------------- | ------------- |
  | Spring Boot            | 2.3.6.RELEASE |
  | Spring Boot Redis      | 2.3.6.RELEASE  |
  | layui                  | 2.5.7        |

###  环境需要
- Java 1.8.0_211
- Maven 3.6.3
- Redis  3.x 不用redis方式可以不要。

### application.yml修改


spring:
  redis:
    database: 1
    host: 119.45.199.171 #这个是用redis做为存储方式时引用的redis信息。
    port: 6379
#    password:
short_url:
  valid: 2160000
  server: http://127.0.0.1:8080 #这里是短网址服务器地址

server:
  port: 8080

## 其他说明
1. 有更多的功能想法欢迎提出
2. 联系作者QQ：1140336945
3. ### 高级的API使用方式，是要加加密认证字符串。
 **`Access Key Id（AK）用于标示用户，Secret Access Key（SK）是用户用于加密认证字符串和云厂商用来验证认证字符串的密钥`**<br>
- 首先需要ak和sk的授权才可以访问api接口，当然你可以在你系统中取消此项认证<br>
在com.kk.docker.config.WebConfig中中注释掉如下代码即可取消认证<br>
```
//添加api权限拦截器拦截所有api
=======
## 如果你还没听说过「红杉」...

如果果你还没听说过「红杉」
身为工程师的你一定听说过这些公司:Apple, Google, GitHub... 
作为「创业者背后的创业者」，红杉中国投资了阿里巴巴、京东、头条、美团点评等互联网头部企业。

## 开放岗位

岗位非特别注明签约实体均为第三方 (外包)

北京：
- [Java](java/)
- [TypeScript Fullstack](fullstack/)
- [TypeScript Frontend](frontend/)
- [Swift](swift/)
- [QA](qa/)
- [DevOps](dev-ops/) (全职)
- [UI 设计师](design/)

上海/深圳/香港：
- [IT Support Engineer](it-support-engineer/) (全职)

链接中有更为具体的 JD。

# interview-assignments

The monorepo for interview take home assignments.

Please find your assignment in subfolder accordingly.

## 这样一家投资公司为什么要招工程师 / 设计师？

为红杉中国各团队提供数字化支持，持续整合业务，提升能效，创造新机会。投资了这么多高新互联网企业，我们自身的脚步也不想停下。

虽然不是面向公众的产品但有很多有意思的地方，具体的我们面试聊。

## 在投资公司做技术 / 设计是不是属于边缘业务？

对于其他投资公司，我们不太清楚。但在红杉中国，我可以肯定地告诉你，工程师所做的不会是写几个简单的展示型页面，设计师也不会只是画图。你将会：

1. 接触到真实业务场景与核心需求，参与制定世界顶级 PE / VC 的日常业务流程
2. 从用户的角度出发思考产品逻辑与方向
3. 近距接触投资人们的喜怒哀乐 (接 bug)
4. 独立地负责整块功能，跟随产品一起迭代整体技术架构

## 技术栈是？

设计：Figma

前端: TypeScript + React

后端: TypeScript + Express

移动端: SwiftUI

如此激进的选择得益于完善的设备管理以及项目所处的阶段，你不用花大量时间处理不同设备的兼容问题或陈旧的代码，只需要关注技术本身。

## 实力如何？

团队成员来自 AWS、Airbnb 等企业，深知做好技术的重要性。所以我们在尽可能的范围内将流程做到最规范：CI / CD / Code Review 一样都没落下。再厚脸皮举两个例子：

1. 有工程师在入职后感叹：没想到对产品和 Code Review 的要求如此严格，不过同时也能学到很多新东西
2. 设计师说：不再只是 “画图的”，而是能真正地思考并把握一个产品的设计与体验

## 说了这么多优点，难道没有缺点吗？

肯定不是。如果你想发展的是高并发 / 高可用等基础架构方向，诚实地说我们短期内没有合适的岗位。

但如果你想在保持开发技术的同时，去探索一块新的领域，去深度理解用户需求与产品间的联系，去从更高层的角度看待你所在的行业，这将是一个不错的机会。

## 团队氛围呢？

两个词：高效与平等。

1. 我们不愿意大家的时间花在无意义的事情上。大家曾不经意抱怨写周报需要占用时间，于是我们马上取消了周报，并改为每周计划会的形式来规划产品与同步进度
2. 在这里没有谁比谁的职级高，只有事实与道理。只要言之有理，每一个人都可以发出自己的声音。我们的设计师经常说：“这是开发与设计相处得最融洽的团队”
3. 出现了问题我们的方案是先解决，随后建立相关的机制避免重蹈覆辙，而不是去一味地责怪某一个人
4. 不鼓励加班，更看重效率

## 有些什么福利？

我们不打算靠福利来吸引优秀的你，不过该有的都不会缺：

1. 最新 MacBook Pro
2. 外设（键鼠，升降桌，高清显示器…）
3. 星巴克提供品牌，雀巢提供服务的免费咖啡服务
4. 无限冷热饮/小吃供应

至于薪水，我们想要找到合适的人而不是想一味地压缩成本。给出的 package 不输互联网大厂，相信能让你满意。

## 会不会存在类似互联网企业的的一些坑？

工作时间：双休，结果导向，倡导提升效率而不是加班

年龄限制：没有。团队成员 70 后到 90 后都有分布

学历要求：不限。面试通过都好说

## 你们的技术太新了，我没有用过...

没关系。我们并不需要你的经历 100% 匹配上文提到的技术栈，如果你有三年以上（可以有例外）技术相关的工作经历，并愿意：

1. 花一些时间学习并做一份简单的作业
2. 面试来进一步确认我们的岗位符合你的预期

我们随时欢迎你的到来。

## 作业在哪？如何提交？

### 设计师

发送你的作业和简历/作品集至以下地址：

```
cmVjcnVpdGluZy5kZXNpZ25Ac2VxdW9pYWNhcC5jb20=
```

（防止爬虫进行了 base64 编码，可以通过[这个链接](https://tool.oschina.net/encrypt?type=3)进行解析）


### 其他岗位

Fork 当前仓库并在相关文件夹下找到你的作业。完成作业后提交一个 Pull Request 即可。如果方便，可以在 PR 描述中留下你的简历。

## 还有其他要补充的吗？

1. 面试不会问茴字有几种写法，甚至不会限制语言。我们看重的是解决问题的能力
2. 办公地点在北京国贸 / 望京，交通便利，离地铁和环线都特别近
3. IT Support Engineer 在 上海 / 香港 都有名额，其余岗位仅限北京
>>>>>>> a74557c679e2ecf379f1f7a493b1406cb0aec498
