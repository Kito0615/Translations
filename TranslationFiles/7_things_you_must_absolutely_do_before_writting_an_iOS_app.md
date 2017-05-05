# 7件开发iOS程序之前必须要做的事

##### 作者:[Nlkant and](https://medium.com/@nikantvohra)
##### 翻译:[Mr_龙0615](http://weibo.com/409498119)
##### 原文:[7 Things you must absolutely do before writing an iOS app](https://medium.com/ios-os-x-development/7-things-you-must-absolutely-do-before-writing-an-ios-app-a8bacf710c57#.mb53mbct4)

我已经开发高质量的iOS程序产品已经两年了。我知道绝大多数开发者有一种倾向，就是直接进入程序的核心逻辑的编码，这就是乐趣的所在。按流程进行很无聊。

我最近学到的是，如果你在前期花一些时间正确设置你的项目，你将会在以后节省大把时间。如果你是个人开发者，你可能还没有意识到我以下提到的步骤的重要性。大多数好的应用程序都是团队开发的，而以下步骤绝对会减少你和团队的挫折(障碍)并提高应用程序的质量。

####1.为你的项目建立编码风格规范

编码风格规范是指在使用某种特定编程语言前参考的风格和约定。它包括诸如应该用tab键还是空格，如何给变量命名，或者一种语言的一些惯例(如在Swift中应该使用类还结构体)	编码风格没有对错。你可以在开始你的项目之前决定你自己的风格，但是要记住整个团队都需要遵守这个规范。这些规范将帮你们使用你们的代码更统一并方便阅读。

一些公司已经开源了他们关于Swift和objective-C的编码规范

[raywenderlich/swift-style-guide](https://github.com/Artwalk/swift-style-guide/blob/master/README_CN.md)![](https://avatars1.githubusercontent.com/u/4722515?v=3&s=20)

[github/swift-style-guide](https://github.com/github/swift-style-guide)![](https://avatars3.githubusercontent.com/u/9919?v=3&s=20)

[NYTimes/objective-c-style-guide](https://github.com/NYTimes/objective-c-style-guide)![](https://avatars3.githubusercontent.com/u/221409?v=3&s=20)

#### 2.开始编码前确定程序的结构

在开始写代码之前确定程序的结构是非常重要的。良好的结构会使得你的程序经得起考验，容易理解，降低维护成本。你可以遵循传统的MVC(Model-View-Controller)结构，或者尝试更优秀的MVVM或VIPER结构。网络上现在有超多的资料介绍这些结构。

[iOS Architecture Patterns](https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52#.3suf3q36w) --[中文版](https://blog.coding.net/blog/ios-architecture-patterns)

[Issue 13:Architecture-objc.io](https://www.objc.io/issues/13-architecture/)

[Modern application architectures (Reactive programming, MVVM beyond)](https://slack-files.com/T051G5Y6D-F0HABHKDK-8e9141e191)

#### 3.规范程序目录结构
为了保证你大量的源代码在同一个目录中存储，根据你的结构决定你可以设定对应的目录结构。例如，你可以这样:

```
|-- Models
|-- Views
|-- Controllers(or ViewModels, if your architecture is MVV)
|-- Stores
|-- Helpers
```

首先，在Xcode的项目导航栏创建以上分组(小的黄色的"文件夹")。然后，把每组与项目路径中实际的目录对应，通过右侧的文件检查器，点击小的灰色的文件夹图标创建与你工程目录中名字相同的子文件夹。

这好像是个次要的事，但是绝对会让你的应用程序更加结构化而且更容易理解。

想了解更多，查看这个资源。

[futurice/ios-good-practices](https://github.com/futurice/ios-good-practices)![](https://avatars3.githubusercontent.com/u/852157?v=3&s=20)

#### 4.依赖库管理
在你程序中，你肯定会用到某些第三方库。以下是三种重要的管理项目中依赖库的方式。

**CocoaPods**

[CocoaPods.org](https://cocoapods.org/)

CocoaPods是针对Swift和Objective-C语言cocoa项目的依赖库管理工具。它大概有上万个库可以帮助你使你的项目更优秀。它是管理依赖库最有效的方式，在过程上和Ruby Gems相似。

<iframe height = 320 width = 560 src="https://youtu.be/iEAjvNRdZa0?list=PLOU2XLYxmsIKGQekfmV0Qk52qLG5LU2jO" frameborder=0 allowfullscreen></iframe>

**Github Submodules**

你也可以使用git子模块来组织你程序中的依赖库。相比于CocoaPods，子模块的优势在于**子模块就是子仓库**——不仅意味着git和git的GUI都可以隐式识别它们，和越来越多的支持使它们更方便使用，也意味着你的项目依赖的库与它们的仓库，保持着关联，CocoaPods并不，它保留在你的项目中。

使用git子模块的问题在于:你的项目并不包含你依赖的源代码，它只是引用了子模块的仓库。而且大多数时候你甚至不能控制那个仓库。

[注]仓库指的程序托管的代码库。

**Carthage**

[Carthage/Carthage](https://github.com/Carthage/Carthage)![](https://avatars0.githubusercontent.com/u/9146792?v=3&s=20)

Carthage的初衷是成为向Cocoa程序添加框架最简单的方式。Carthage使用xcodebuild创建框架，但是把整合的责任交给了用户。CocoaPods的使用方法更简单，而Carthage的方式则更灵活。

不幸的是，Carthage有一个大的缺点——就是**只支持iOS8以后的版本**

以上就是最常用的三种管理依赖库的方式，而我个人最喜欢的是CocoaPods，因为它设置超级方便而且可以获取到成千上万的第三方库。

#### 5.为你的程序设置恰当的Schemes

Schemes告诉Xcode当你点击"执行"、"设置"、"配置"、"分析"或者"打包"的时候，应该干什么。基本上，Schemes标明了这些操作对应的目标和编译配置。你也可以通过传入启动参数，如程序应该运行的语言(手动测试本地化！)或者设置一些调度诊断标志。

以下是**MyApp(\<Language\>)[Environment]**的Schemes命名规范:

`MyApp (Enligsh) [Development]`

`MyApp (Germen) [Development]`

`MyApp [Testing]`

`MyApp [Staging]`

`MyApp [App Store]`

你可以用不同的目标(Targets)像下面描述的那样，为你的程序生成不同的产品(Production),测试(Test)和开发(Development)版本。

[How to Use Xcode Targets to Manage Development and Production Builds](https://www.appcoda.com/using-xcode-targets/)

#### 6.为你的程序设置恰当的证书及配置文件

这一步是测试和发布iOS程序最痛苦也是最重要的步骤之一。代码签名需要证书，这样你的程序才能在真机上运行。

证书有两种:

* **开发证书**:每个开发者所在团队都有他们自己的开发证书，它是基于请求生成的。Xcode可以为你做，但是最好不要点击 神奇的"修复"按钮，并且不要去理解到底实际发生了什么。这种证书在部署开发版程序到设备上的时候才需要。
* **生产证书**:生产证书可以有多个，但是最好是保证一个公司只有一个，然后通过内部渠道共享它的关联的密钥。在上传到App Store或者你的公司内部的"企业app store"的时候需要这种证书。

**配置文件**——可能是这个系统中最令人疑惑的文件了。一个配置文件表示应用程序对于哪些设备是签名正确的。如果你访问开发者网站首页，你会注意到你可以创建两种(也叫*开发配置文件*和*生产配置文件*)配置文件。配置文件作用是*使用这个**标识(Identifier)**的应用程序是用**证书(Certificate)**的私有密钥(Key)签名的，可以在这类设备上运行。*


参考[What are the differences between certificates provisioning profiles and identifiers](https://www.quora.com/What-are-the-differences-between-certificates-provisioning-profiles-and-identifiers)

你可以在下面的链接中了解更多:

[Maintaining Your Signing Identifiers and Certificates](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)

[What is a Provisioning Profile> (Pt. 2) by Jay Graves of Double Encore](https://possiblemobile.com/2013/04/what-is-a-provisioning-profile-part-2/)

#### 7.设置持续集成和交付进度

设置持续集成和交付进度在今天看来有点挑剔了，但是它可以帮助你在开发周期中早点发现问题(bugs)并且节省大量开发时间。

**持续集成(CI)**是一种开发实践需要开发者们每天**集成**代码到共享库几次。每次先检查，然后通过自动编译验证，可以使团队早点发现问题。

现在有很多工具可以帮助你持续集成iOS程序可以使用，像Xcode Server, Jenkins 和 Travis CI。

[About Continuous Integration in Xcode](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/xcode_guide-continuous_integration/)

[Travis CI - Test and Deploy Your Code with Confidence](https://travis-ci.org/)

[iOS CI with Jenkins | Pivotal P.O.V](https://blog.pivotal.io/labs/labs/ios-ci-jenkins)

**持续交付(Continuous Delivery(CD))**是[软件工程](https://en.wikipedia.org/wiki/Software_engineering)方法，这种方法要求开发团队短期编译生成软件，用来确保软件可以随时发布的可靠性。[1](https://en.wikipedia.org/wiki/Continuous_delivery#cite_note-CD_LC-1)。它的目标是在于使软件编译、测试和发布更快和更频繁。

***为什么要使用持续交付？***

1. 节省准备提交、上传截图和发布程序的几天时间。

2. 同事在度假而一个紧急问题修复(bugfix)需要发布？不要指望一个人发布升级。

3. 更频繁和更小体积的发布可以提升软件质量和反应时间。

尽管有许多持续交付的工具可以使用，但是我个人最喜欢的还是Fastlane. 它的设置真的是超级方便，而且功能非常强大。这可以实现整个编译和发布流程自动化。

[fastlane - iOS and Android Automation for Continuous Delivery](https://fastlane.tools/)

如果你喜欢这篇文章，建议你分享出去，可以让其他人也能看到并喜欢它。订阅我的[网站](http://www.nikant.me/newsletter/)获取更多文章。

---
**关键字**: `iOS`  `持续集成`  `Swift`

---
**写在后面:**

由于译者的翻译水平有限，如有不足之处，希望大家指出。

**关于译者:**

微博:[Mr_龙0615](http://weibo.com/409498119)

邮箱:[anar0615@sina.com](mailto:anar0615@sina.com)

GitHub:[Anar](https://github.com/Kito0615)
