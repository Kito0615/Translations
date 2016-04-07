#27个iOS开源库助力你的开发
__*你绝对不想错过*__

* 作者:[Pawel Bialecki](https://medium.com/@pawel_bialecki)
* 翻译:[Mr_龙](http://weibo.com/409498119)
* 原文:[27 iOS Open source libraries to skyrocket your development.](https://medium.com/app-coder-io/27-ios-open-source-libraries-to-skyrocket-your-development-301b67d3124c#)

---

__*我喜欢开源！*__

而且我也喜欢那些花费宝贵时间来创造好玩的东西并不求回报地与他人分享这些东西的开发者。**所有为开源做贡献的人们，你们都太棒了！**感谢你们的努力！
	
---

下面，从我日常工作中我自己的[APP](https://www.eclerstudios.com/)里，从我非常喜欢的iOS开源库里选出一些开源库，列举在这里。以下排名不分先后，因为它们都很不错。

这里面绝大部分开源库都支持[CocoaPods](https://cocoapods.org/)，所以，将它们添加到你的Xcode项目里是轻而易举的事。

在文章的最后，你会找到TL;DR(Too long; didn't read.)版本——只有标题和项目超链接。如果你觉得这篇文章有用，__请和你的iOS小伙伴分享。好的东西需要传播。__

###__1.DZNEmptyDataSet__

这个库应该内置于iOS SDK中成为标准的处理空表视图(TableView)和集合视图(CollectionView)的方法。使用默认的表视图，如果你的视图是空的，那么屏幕就是空的。你并不能获得最好的用户体验。

使用这个库，你只需要实现几个协议，iOS就可以完美恰当地展示给你一个对用户友好的集合视图。对每个iOS项目来说都很简单。

![](https://cdn-images-1.medium.com/max/800/1*-GPQJ5GrZGlo560Vjn6ueQ.png)

####CocoaPods:

`pod 'DZNEmptyDataSet'`

###__2.PDTSimpleCalendar__

想要为你的App添加一个简单、好看而且有效的日历组件吗？从现在起，你拥有了可能是iOS上最好的日历组件——PDTSimpleCalendar。

![](https://cdn-images-1.medium.com/max/800/1*py6WgEruAWaYGGG0xxgRwg.png)

####CocoaPods:

`pod 'PDTSimpleCalendar'`

###__3.MagicalRecord__

有人说，*Core Data很简单*。也有人说，*它很好用也很简单*。呵呵，说的是苹果产品吗？成千上万的范例代码添加到哪个项目都不是优雅且简单的。还别说添加、删除、更新一大堆的实例、保存上下文、创建为不同的环境不同的Core Data堆栈等等。我当然非常喜欢Core Data，但是苹果*真的*可以用一种稍微好一点的方式——__MagicalRecord的方式__——简化它。

MagicalRecord的工作方式像将Core Data封装起来，将所有与开发者不相关的东西隐藏掉。如果你在你的App中使用了Core Data，真诚地推荐你使用这个库。

#####CocoaPods:

`pod 'MagicalRecord'`

###__4.Chameleon__

如果你正在阅读这篇文章，你可能是一个比设计师更出色的工程师。这个库合适你。

![](https://cdn-images-1.medium.com/max/800/1*bjdhJDlCZJtya6bAI5938g.png)

Chameleon是一个iOS色彩框架.它在UIColor的基础上，扩展出漂亮的、现代的、扁平化的颜色。它也可以根据我们自定义的颜色创建出选色板。它还可以做很多事情，从Readme中去发现吧。如果你想使你的App变漂亮，绝对要将这个库添加到你的项目中。

![](https://cdn-images-1.medium.com/max/800/1*sMgYah4wuGhN3IQsWtG_7A.png)

####CocoaPods:

`pod 'ChameleonFramework'`

###__5.Alamofire__

Alamofire是一个用Swift写的出色的网络连接库。你应该一直都在使用AFNetworking吧？Alamofire是它的亲兄弟。年轻但是更时髦，当然(AFNetworking是用Objective-C写的)。

![](https://cdn-images-1.medium.com/max/800/1*qkOCEhp5g9ixArBdLDwPyw.png)

你需要完成网络任务如：下载、上传、获取JSON数据等？Alamofire适合你。GitHub8000人的选择不会错。

####CocoaPods:

`pod 'Alamofilre'`

###__6.TextFiledEffects__

你有没有觉得标准的UITextField有一点枯燥？我也是这样认为的，那么，来认识一下__TextFiledEffects__吧！我不会写太多，只给你们展示一下这个库能完成的例子:

![](https://cdn-images-1.medium.com/max/800/1*Nws8VPi9br54Ae-tCwLXGA.gif)

当然，__只要拖拽进控制器就行__。你甚至可以在storyboard中当作IBDesignables使用。

####CocoaPods:

`pod 'TextFiledEffects'`

####Carthage:

`github "raulriera/TextFiledEffects"`

###__7.GPUImage__

你有开发过相机应用吗？如果没有，__在见识这个库之后你一定会尝试的__。

![](https://cdn-images-1.medium.com/max/800/1*s7tpFPCnKV8YZ7qdCVZyqg.png)

GPUImage提供给我们一个GPU(图形处理单元)加速的相机效果(图片和视频都可以)，速度超快！App Store里有几百个app使用了这个库——我的其中一个也使用了:

在GitHub上有8869颗星，而且还在增加。

####CocoaPods:

`pod 'GPUImage'`

###__8.iRate__

在App Store中获得更多评论的最好方法是什么？我并没有足够的数据能回答这个问题，但是如果要我说，我可能会说*问问用户就好啦*。这可能是有点老派的方式了——现在很多开发者在App中创建自定义提示——但是如果你没有时间或者不想从取消实现任何方法，那最好是使用iRate。iRate具体可以是——一个小型的，你把它添加到你的项目中并且你忘了要求用户评价时——iRate可以帮你在合适的时机提示用户评价的库。

####CocoaPods:

`pod 'iRate'`

###__9.GameCenterManager__

你喜欢或者讨厌单例，但是这种情况下，在我们最熟悉的反模式的帮助下管理Game Center是很__简单__的(在你的游戏中*只有一个Game Center*吧？)。

![](https://cdn-images-1.medium.com/max/800/1*t1Sy5Jt2fAaeU1VaAeEjbQ.png)

老实说，*vanilla-managing*在iOS中管理游戏中心并不难，__但是使用这个库只会更方便快捷__。而且更好是好的对立面。

![](https://cdn-images-1.medium.com/max/800/1*P3bj6yW7GnnT0yTt0RdboQ.png)

我在我的一个游戏中正在使用它，而且很好用。

####CocoaPods:

`pod 'GameCenterManager'`

###__10.PKRevealController2__

这是一块宝石，__我最喜欢的iOS控制模块之一__。PKRevealController2可以滑动的侧边菜单(左右都可以)，往哪边滑取决你的手指(或者通过点击按钮，但是那样并没有滑动操作那样酷)

![](https://cdn-images-1.medium.com/max/800/1*uM5nPOq0tbieJBYMC0f1jg.png)

我尝试过其他提供类似功能的库，PKRevealController是最好的。设置非常简单，高度自定义，手势识别非常好。我觉得可以作为iOS SDK的标准库，真的！

####CocoaPods:

`pod 'PKRevealController'`

###__11.SlackTextViewController__

你使用Slack iOS应用吗？如果你在一家大一点软件公司，你可能用过。对于还没有在自己的app中使用过的人来说——Slack很难。而Slack的iOS程序也很难，特别是对于很棒的、自定义的文本输入控制…，这种情况下，准备好在你的程序中使用这些代码吧！

__自动增加文本区域？可以。手势识别，自动填充，多媒体复制？可以。简单的拖拽方案？可以__你还需要什么功能呢？

####CocoaPods:

`pod 'SlackTextViewController'`

###__12.RETableViewManager__

RETableViewManager可以帮助你用代码动态创建和管理表格视图。它已经帮我们定义了一些表格(bool值、文本、日期等，看下图)，但你也可以自定义视图与默认的一起使用。

![左边是iOS6以前，右边是iOS7以后](https://cdn-images-1.medium.com/max/800/1*Tq-kGojYO7NjWWa2R7pKcQ.png)

如果没有这个库，你可以在storyboard上也能完成，但是有时候代码比可视操作更好。

####CocoaPods:

`pod 'RETableViewManager'`

###__13.PermissionScope__

这是一个好用的库，它通过在需要系统权限__之前__提示征求用户允许提升用户体验。更高的授受度->用户更高的使用率->更好的保留度->更好的统计->更多的下载量。高度推荐的库。

![](https://cdn-images-1.medium.com/max/800/1*lCNOzpkOzDj-WUFbUITtQA.png)

####CocoaPods:

`pod 'PermissionScope'`

###__14.SVProgressHUD__

这个图片出现很合适，不用等太久也不要刷新页面。__这就是SVProgressHUD在你的App中的样子__。如果你需要自定义指示器，你可以用它(可能是最好的)。

![](https://cdn-images-1.medium.com/max/800/1*nUWClDbqfsNzRqFx6jhA3g.gif)

####CocoaPods:

`pod 'SVProgressHUD'`

###__15.FontAwesomeKit__

__Font Awesome 真的很棒！__用这个库，你可以非常方便的在你的项目中添加字体而且在很多方面都可以用它。

![](https://cdn-images-1.medium.com/max/800/1*QYbVsOA96NsUxSCrQ_CIUw.jpeg)

###CocoaPods:

`pod 'FontAwesomeKit'`

###__16.SanpKit__

你喜欢自动布局？应该喜欢！

*至少在storyboard中喜欢*

如果没有一些辅助使用代码构造一个好的布局是非常痛苦的，但幸运的是，SnapKit可以让代码布局变得简单，易懂。

![](https://cdn-images-1.medium.com/max/800/1*PVelVchmwY6kHZ9FMGuJiQ.png)

####CocoaPods:

`pod 'SnapKit'`

###__MGSwipeTableCell__

另一个用户界面组件，在许多应用程序中都很常见，苹果应该可以考虑把一些相似的东西添加到标准iOS SDK中。

![](https://cdn-images-1.medium.com/max/800/1*g9U2AX7pYXm5QY0_rBKOUQ.gif)

这里只有三种动画类型，实际还有更多。在Readme中去发现吧。

####CocoaPods:

`pod 'MGSwipeTableCell'`

###__18.Quick__

Swift中的单元测试(对Objective-C也可以)，集成了Xcode。如果你是Objective-C的粉丝，我会向你推荐[Specta](https://github.com/specta/specta)，但是，对于Swift来说，Quick是最好的选择。

![](https://cdn-images-1.medium.com/max/800/1*slKaci9ZuZRTUjDzgi3-SA.png)

![](https://cdn-images-1.medium.com/max/800/1*ZMm8Jgzv9VTPi3v7cxc4KA.png)

####CocoaPods:

`pod 'Quick'`

###__19.IAPHelper__

App内购给我们带来了很多示例代码，这个库都不没有使用，而是给我们一个简单常用的与用户与你(你的公司)交易相关任务封装。

####CocoaPods:

`pod 'IAPHelper'`

###__20.ReactiveCocoa__

好吧，我们遇到一个大家伙。

![](https://cdn-images-1.medium.com/max/800/1*ZGn-IDtnbbN7ryiXwpNQTg.png)

ReactiveCocoa并不一个小型的，拖拽项目，不像列表中的其他项目。__ReactiveCocoa给我们带来了一种完全不同的基于信号值与流值的编程方式/结构__它会让你的大脑爆炸，一开始，你需要忘掉你已经学过的来理解它是怎样工作的。这并不轻松，但回报颇丰。

这里不适合开始学习ReactiveCocoa，但是如果你感兴趣，以下资源你可以参考:

* [Getting Started with ReactiveCocoa](http://www.teehanlax.com/blog/getting-started-with-reactivecocoa/)
* [ReactiveCocoa](http://nshipster.com/reactivecocoa/)
* [ReactiveCocoa Tutorial - The Definitive Introduction: Part 1/2](https://www.raywenderlich.com/62699/reactivecocoa-tutorial-pt1)

####CocoaPods:

`pod 'ReactiveCocoa'`

###__21.SwiftyJSON__

Swift中JSON格式化，从未如此简单。

####CocoaPods:

`pod 'SwiftyJSON'`

###__22.Spring__

动画从未如此简单，可链接而且直接。

![](https://cdn-images-1.medium.com/max/800/1*J0QzPXBCDAs6d5MS9DPMpg.jpeg)

####CocoaPods:

`pod 'Spring'`

###__23.FontBlaster__

轻轻松松向你的程序中添加自定义字体。

####CocoaPods:

`pod 'FontBlaster'`

###__24.TAPromotee__

交叉推广你的应用程序是最好的市场策略之一，现在你可以免费实现它们了。使用这个库很简单，你再也不用证明不这样做——添加TAPromotee到你的Podfile,设置好免费等着更多的下载量吧。

![](https://cdn-images-1.medium.com/max/800/1*FF4dr7V617RSqlrUhuvr7Q.png)

####CocoaPods:

`pod 'TAPromotee'`

###__25.Concorde__

你有在你的应用程序中显示过很多JPEG图片吗？使用ConCorde库，你可以用更好看的方式完成。带进度的方式。

![](https://cdn-images-1.medium.com/max/800/1*2UdNaQS15wesjGjjiHAvaQ.gif)

####CocoaPods:

`pod 'Concorde'`

###__26.KeychainAccess__

管理Keychain访问的小帮手。

![](https://cdn-images-1.medium.com/max/400/1*uLid5pu3_m0YQIptfim5jg.png)
![](https://cdn-images-1.medium.com/max/400/1*lfVh0XU6GaSr-irD8xeb8A.png)
![](https://cdn-images-1.medium.com/max/400/1*tEIFKi-dRQW7FkohYgELAw.png)

####CocoaPods:

`pod 'KeychainAccess'`

###__27.iOS-charts__

最后一个，也是最重要的一个——iOS图表库！非常实用而且好看，我不会写太多——__向下翻查看可以用这个库在你的App里做什么吧！__

![](https://cdn-images-1.medium.com/max/800/1*VbtAD_1hxOldYxjJx6vASA.png)

![](https://cdn-images-1.medium.com/max/400/1*WaQkU2dRwNzqMEZunyqNAQ.png)
![](https://cdn-images-1.medium.com/max/400/1*OeGTvNnJUqBIehn1wjIbpg.png)
![](https://cdn-images-1.medium.com/max/600/1*sDI562oJKyDVGq49BjMeYA.png)
![](https://cdn-images-1.medium.com/max/400/1*3Nn3WU5YSg26_8vPQZ2rDQ.png)
![](https://cdn-images-1.medium.com/max/400/1*pOqvE_3UQPfkepplZA2zqA.png)
![](https://cdn-images-1.medium.com/max/400/1*RSiBbr-v5YXod6MQNDXz2g.png)
![](https://cdn-images-1.medium.com/max/400/1*BCtAfcEAjrU1KW-IfG7jmA.png)
![](https://cdn-images-1.medium.com/max/600/1*IPF0dEGyvDLsw4pzASPxaA.png)
![](https://cdn-images-1.medium.com/max/200/1*vHUAaOByjBHfLfo2x1Z6yw.png)
![](https://cdn-images-1.medium.com/max/600/1*JMvTfSBPIFj-ganbyCPTzg.png)
![](https://cdn-images-1.medium.com/max/600/1*bC4jLpWVEqhxGRXbdv_2xw.png)
![](https://cdn-images-1.medium.com/max/1000/1*AAcJvh9nb4BETcE4f6g9lw.png)
![](https://cdn-images-1.medium.com/max/400/1*YfdosQop9CLvd1cMV7JsXw.png)

是的，所有图表者是可以拖拽(或者“写代码”)的组件。

不幸的是，这个库现在还不支持CocoaPods，因此，你需要手动将这个项目拖拽到你的Xcode项目中去。

---

TL;DR，快速访问以上所有库的列表：

1.[DZNEmptyDataSet](https://github.com/dzenbot/DZNEmptyDataSet)[用户界面，空表格视图解决方案]
2.[PDTSimpleCalendar]()[用户界面，拖拽日历控件]
3.[MagicalRecord]()[Core Data实现活跃记录模式帮手]
4.[Chameleon]()[用户界面，色彩框架]
5.[Alamofire]()[Swift网络框架]
6.[TextFieldEffects]()[用户界面，自定义文本框外观]
7.[GPUImage]()[快速图形处理]
8.[iRate]()[获得用户评论]
9.[GameCenterManager]()[方便管理GameCenter]
10.[PKRevealController]()[用户界面，侧滑菜单]
11.[SlackTextViewController]()[用户界面，高度自定义文本框]
12.[RETableViewManager]()[代码动态创建列表视图]
13.[PermissionScope]()[用户界面，友好的系统权限获取请求]
14.[SVProgressHUD]()[用户界面，自定义等待指示器]
15.[FontAwesomeKit]()[添加字体到你的项目更简单]
16.[SnapKit]()[代码布局更方法]
17.[MGSwipeTableCell]()[用户界面，可以滑动的表格行]
18.[Quick]()[Swift单元测试框架]
19.[IAPHelper]()[应用程序内购封装]
20.[ReactiveCocoa]()[FRP框架]
21.[SwfityJSON]()[Swift JSON库]
22.[Spring]()[动画框架]
23.[FontBlaster]()[在程序中快速添加自定义字体]
24.[TAPromotee]()[使用拖拽视图交叉推广你的程序]
25.[Concorde]()[图片下载解码进度条]
26.[KeychainAccess]()[管理Keychain更简单]
27.[iOS-charts]()[好看的图表库]

---

感谢您阅读这一份长长的列表！如果你觉得这篇文章有价值，**请点击文章下面的*分享*按钮将文章分享出去。**——将会有更多的人受益。——这将会激励我写更多的关于iOS开发的文章。

我平日都在写[Ecler Studios](https://www.eclerstudios.com/)的程序——随时来查看[我的App](https://www.eclerstudios.com/)

![](https://cdn-images-1.medium.com/max/800/1*PTn3QofhA4_ihRulOwXg-g.png)

我通常把iOS开发相关的发到Twitter上，你也可以[关注我](https://twitter.com/pawel_bialecki)

__推荐阅读:__

[27 places to learn iOS Development. Bets ones.](https://medium.com/app-coder-io/27-places-to-learn-ios-development-best-ones-b1bcfb48efab)

[52 people every iOS developer shold follow on Twitter.](https://medium.com/app-coder-io/52-people-every-ios-developer-should-follow-on-twitter-25ca8915369a)

__关键字:__  `iOS 开发`  `iOS` `苹果`

---

感谢大家看我的翻译，如果有翻译不正确的地方，希望大家可以指出来。
邮件:[anar0615@sina.com](mailto:anar0615@sina.com)
微博:[Mr_龙0615](http://weibo.com/409498119)







