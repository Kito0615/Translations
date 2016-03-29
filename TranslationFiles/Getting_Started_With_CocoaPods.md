#Getting Started with CocoaPods
#CocoaPods指南
--
###CocoaPods安装
以下内容来自[CocoaPods.org](https://guides.cocoapods.org/using/getting-started.html)
#####0. 什么是CocoaPods?

CocoaPods帮助管理你的Xcode项目依赖库。

你的项目依赖库在一个叫Podfile的文本文件中声明。CocoaPods会解决这些库之间的依赖关系，获取生成的源代码，然后将这些库连接到一个Xcode工作空间来创建你的项目。

最终目标是要通过创建一个更集中的生态来提高可发现性，可参与性的第三方开源库。

####1. 现在开始吧！
#####1.1 安装CocoaPods

CocoaPods是用Ruby创建的，所有CocoaPods需要在Ruby环境下才能安装，而Ruby是OS X系统自带的。你可以使用Ruby版本管理器。除非你知道自己在干什么，不然，我们还是建议你在OS X上使用标准Ruby。

在安装gems时，使用默认Ruby安装需要你使用`sudo`命令。(尽管这是在安装gem过程中唯一会出现的问题)。

`$ sudo gem install cocoapods`

如何你在安装过程中，遇到任何问题，请访问[疑难解答](https://guides.cocoapods.org/using/troubleshooting#installing-cocoapods).
#####1.2 非超级管理员安装

如果你在这个过程中不想授予RubyGems管理员特权，你可以通过设置`gem install`的`--user-install`标识指向用户路径告诉RubyGems将RubyGems安装到指定的用户目录下，也可以通过设置RubyGems环境变量来实现。后者是我们认为最好的解决办法。如果这样做，需要在用户主目录下创建并修改`.podfile`文件，添加或修改的内容如下:

`export GEM_HOME=$HOME/.gem`

`export PATH=$GEM_HOME/bin:/$PATH`
>注意，如果你使用了`--user-install`选项，你还需要设置在`.podfile`设置`PATH`参数或在使用这个命令前注入路径。你可以通过`gem which cocoapods`查看gem的安装位置。
使用实例:

>`$ gem install cocoapods --user-install`
>`$ gem which cocoapods`
>`/Users/eloy/.gem/ruby/2.0.0/gems/cocoapods-0.29.0/lib/cocoapods.rb`
>`$ /Users/eloy/.gem/ruby/2.0.0/bin/pod install`

#####1.3 升级CocoaPods

要升级CocoaPods，你只需要重新安装一下gem就可以了。

>`$ [sudo] gem install cocoapods`

或者，安装预览版

>`$ [sudo] gem install cocoapods --pre`

如果你第一次就使用全了超级管理员权限`sudo`安装CocoaPods gem，那么你需要再次使用`sudo`命令来升级。

然后，当你经常使用CocoaPods来安装pods时，当有新版的CocoaPods可以使用时，你会收到诸如_CocoaPods X.X.X is now available, please update_这样的信息提示。

#####1.4 使用CocoaPods命令

有两种方式可以使用CocoaPods命令，一种是使用[Gemfile](https://guides.cocoapods.org/using/a-gemfile.html)(推荐)，一种是在讨论或实际阶段使用[开发版](https://guides.cocoapods.org/using/unreleased-features)。

####其他资源

[CocoaPods at Treehouse](https://teamtreehouse.com/library/ios-tools/cocoapods/cocoapods)
--
###使用CocoaPods
####向Xcode项目中添加Pods

**写在前面**

1. 检查[Specs](https://github.com/CocoaPods/Specs/)仓库或检查网站[cocoapods.org](https://cocoapods.org/)确保你想使用的库是可用的。

2. 在你的电脑上[安装CocoaPods](https://guides.cocoapods.org/using/getting-started.html)

#####安装

* 创建[Podfile](https://guides.cocoapods.org/using/the-podfile.html)，添加你的依赖库:
>`target 'MyApp' do`
>`	pod 'AFNetworking', '~>3.0'`
>`	pod 'FBSDKCoreKit', '~>4.9'`
>`end`

* 在你的工程目录执行`$ pod install`命令。
* 打开`App.xcworkspace`并开始工作。

#####使用CocoaPods创建一个新Xcode项目
要使用CocoaPods创建一个新项目，只需要以下几个简单的步骤:

* 正常使用Xcode创建一个新工程。
* 打开终端窗口，使用`$ cd`命令进入到工程所有目录。
* 创建Podfile. 可以通过`$ pod init`命令完成。
* 打开Podfile.第一行需要指明支持的系统及版本.

>`platform: ios, '9.0'`

* 要使用CocoaPods，你需要定义Xcode目标并连接它们。例如，如果你准备写一个iOS程序，那Xcode目标就是你的app。通过在`target '$TARGET_NAME' do`和`end`之间使用几行代码创建目标
* 通过使用`pod '$PODNAME'`在目标块之间添加一个CocoaPods

>`target 'MyApp' do`
>`	pod 'ObjectiveSugar'`
>`end`

* 保存Podfile
* 执行`$ pod install`命令
* 打开创建的`MyApp.xcworkspace`项目。以后就使用这个文件作为你创建app的每天要使用文件。

#####集成已经存在的工作空间

使用CocoaPods集成已经存在的工作空间需要在Podfile中增加一行。在目标块外面简单声明`.xcworkspace`文件的文件名。

>`workspace 'MyWorkspace'`

####什么时候使用__pod install__,使用时候使用__pod update__?

许多人都比较疑惑，什么时候应该用`pod install`, 什么时候应该用`pod update`。特别是在他们应该使用`pod install`的时候却经常使用`pod update`.

你可以在[pod install vs pod update](https://github.com/Kito0615/Translations/blob/master/TranslationFiles/Getting_Started_With_CocoaPods.md#pod-install-vs-pod-update)这篇这文章中找到关于什么时候该使用哪个命令以及每个命令的目的是什么的更详细的解释。

#####我应该将Pods路径加入到代码控制当中吗？

是否将Pods文件夹添加到代码控制中完全取决于你自己，因为工作流在项目之间不断变化。我们建议你将Pods目录添加到代码管理当中，而不是添加到`.gitignore`文件当中。但是最终的决定权在于你:

#####添加Pods目录到代码管理的好处

* 在复制项目(仓库)之后，立即编译和执行工程，甚至都没有在机器上安装CocoaPods。就没有必要执行`pod install`了，而且不能连接网络。
* 即使Pod源(如:GitHub)失效了，Pod文件(代码/库)常常也是可用的。
* Pod文件可以在复制项目(仓库)之后，保证是和原来安装的是一样的。

#####忽略Pod目录的好处

* 代码管理项目(仓库)会更小，占用更少的空间。
* 只要源(如:GitHub)的所有Pods可用，CocoaPods会能够自动重新创建安装。(严格来说，当没有使用提交Podfile的哈希值时，无法保证执行`pod install`命令将会获取并重新创建特定的文件。尤其是在Podfile中使用zip压缩文件时)
* 否要将Pod目录添加到代码控制中，`Podfile`和`Podfile.lock`都应该在版本控制中。

####什么是`Podfile.lock`？

这个文件是在执行`pod install`命令之后自动生成的，它记录了每个Pod的版本是什么时候安装的。比如:在Podfile中声明以下依赖库

>`pod ‘RestKit`

执行`pod install`将会安装当前版本的RestKit，造成`Podfile.lock`文件被创建，表示安装的具体版本(如:RestKit 0.10.3).由于`Podfile.lock`文件，在这个假定的项目中以后的某个时间，在一台不同的机器上执行`pod install`命令，将会仍然安装RestKit0.10.3，即使有更新的版本可用。CocoaPods将会首先使用`Podfile.lock`中记录的Pod版本，除非依赖库更新或使用了`pod update`(这会使一个更新的`Podfile.lock`文件生成)命令。这样使用CocoaPods可以避免因为依赖库引发的各种令人头痛的问题。

关于这是怎样工作的，有一个来自Google的不错的视频:[CocoaPods and Lockfiles](https://www.youtube.com/watch?v=H-zK1mEwTe0)

####这些事件背后发生了什么？

在Xcode中，直接引用[ruby source](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator.rb#L61-L65),进行了以下操作:

	1.创建或更新了[工作空间](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator.rb#L82)
	2.如果需要，[将你的工程添加到工作空间](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator.rb#L88-L94)
	3.如果需要，[向工作空间中添加CocoaPods静态库](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/target_installer.rb#L40-L61)
	4.添加libPods.a到:[目标=>编译选项=>链接库](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer.rb#L385-L393)
	5.向你的app工程中添加CocoaPods[Xcode配置文件](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator/target_integrator.rb#L112)
	6.根据CocoaPods的目标配置更改你app的[目标配置](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/generator/xcconfig/aggregate_xcconfig.rb#L46-L73)
	7.根据安装绑定到你app的pods[复制源](https://github.com/CocoaPods/CocoaPods/blob/master/lib/cocoapods/installer/user_project_integrator/target_integrator.rb#L145)即在添加其他编译选项后添加如下内容到`Script build phase`(脚本编译选项):

>* Shell:/bin/sh
>* Script:${SRCROOT}/Pods/PodsResources.sh

注意，如果CocoaPods静态库已经添加到你的项目中，将跳过第三步。这是基于Jonah Williams的利用[静态库](http://blog.carbonfive.com/2011/04/04/using-open-source-static-libraries-in-xcode-4/)

####Pods和子模块

CocoaPods和git子模块是尝试用来解决非常相似的问题的。都致力于简化包含添加第三方代码到你的项目的过程。子模块是连接到项目的特定提交(提交时间)，而CocoaPods是绑定到开发者发布的版本。

#####更改子模块为CocoaPods

在你决定要全部更改到CocoaPods之前，你要确保你目前使用的库都是可用的。记录下你正在使用的库的版本也是一个不错的想法，然后，你就可以设置CocoaPods为同样版本。逐渐地、一步一步地而不一次性完成这项工作也是一个不错的想法。

步骤如下:
	1.如果你还没有安装CocoaPods的话，请先安装CocoaPods
	2.创建[Podfile](https://guides.cocoapods.org/using/the-podfile.html)
	3.[移除子模块引用](http://davidwalsh.name/git-remove-submodule)
	4.向Podfile中添加你移除掉的引用
	5.执行`pod install`
--
###pod install vs. pod update
####简介

许多刚刚开始使用CocoaPods的人认为好像只有在第一次用CocoaPods设置项目的时候使用`pod install`，以后都使用`pod update`.**但实际并不是这样的。**

这篇指南的目的就是向你们解释什么时候使用`pod install`，什么时候使用`pod update`的。

TL;DR:(too long, don't read)简单说来:

>* 在安装新的Pod到你的项目里时使用`pod install`。**即使你已经有了`Podfile`也已经执行过`pod install`了**，当你向一个已经使用过CocoaPods的项目里添加/删除pods时。
>* 只有当你想要**更新pods到更新的版本**时才使用`pod update [PODNAME]`

####详细说明这两个命令

> 注意:CocoaPods中的`install`和`update`并不准确。它的灵感来自于许多其他依赖库管理器如:[bundler](http://bundler.io/), [RubyGems](https://rubygems.org/)或者[composer](https://getcomposer.org/),这些都有相似的命令，这些命令都与这篇指南中的描述功能一样。

#####pod install

这不仅是在第一次向项目中获取pods(第三方库)时使用的命令，而且每次你编辑Podfile，添加/更新/删除pod的时候也要使用它。

* 每次运行/下载/安装新的pods时使用`pod install`命令，它都会将每个已经安装的每个pods的版本写到Podfile.lock文件中。这个文件记录并且锁定每个pod的安装的版本。
* 当你执行`pod install`命令时，它只解析**不在**`Podfile.lock`列表中依赖库。
	* 对于已经在`Podfile.lock`列表中的pods，`pod install`命令只会下载`Podfile.lock`列表中指定的版本而不会检查是否有更新的版本可用。
	* 对于不在`Podfile.lock`列表中的pods，`pod install`命令会搜索`Podfile`中描述的版本(如:`pod 'MyPod', '~>1.2'`)

####pod outdated

当你执行`pod outdate`命令时，CocoaPods将会列出`Podfile.lock`列表中(即当前已经安装的版本)有更新版本可用的pods。也就是说如果你对在上述列表中的pods执行`pod update PODNAME`命令，这些pod将会被更新-同样也会更新在`Podfile`文件中的规则为匹配更新版本,如:`pod 'MyPod', '~>x.y'`

#####pod update

当你执行`pod update PODNAME`命令时，CocoaPods将会查找PODNAME的更新版本，而不会考虑`Podfile.lock`文件里列举的版本。它将会更新pod到最新版本(只要满足你在`Podfile`文件中的版本规则)

如果你不带pod name执行`pod update`命令，CocoaPods将会更新`Podfile`里每个可能的pod为最新版本。

####高级用法

使用`pod update PODNAME`,你将只可以**更新**指定的pod(根据检查是否有新的版本存在而更新pod)。相反，`pod install`不会尝试更新已经安装版本。

当你向`Podfile`里添加pod时，你应该执行`pod install`命令，而不是`pod update`--想要没有更新已经存在的pod的风险而安装新pod也是同样的操作。

当你想要更新指定(或者所有)pod版本的时候，你才会用到`pod update`.

####提交你的Podfile.lock文件

提醒一下，即使**你的原则是不提交`Pods`目录到你的共享仓库**，**你也应该提交并且确认你的Podfile.lock文件**

否则，就可以破坏上面关于`pod install`能锁定你的pod的安装版本的整个逻辑。

####场景实例:

以下有几种场景实例来模拟在项目周期中可能出现多种状况。

#####场景1:*用户1*创建项目

*用户1*创建一个项目并且希望使用pod`A`,`B`,`C`。它们用这些pod创建一个`Podfile`,并且执行`pod install`

这样将会安装`A`,`B`,`C`三个pod，每个的版本都`1.0.0`

`Podfile.lock`文件将会记录`A`,`B`,`C`三个pod的版本都是`1.0.0`

>顺带说一下，因为那是第一次执行`pod install`并且`Pods.xcodeproj`还不存在，这个命令也会创建`Pods.xcodeprj`和`.xcworkspace`文件，但是那只是这个命令的侧面影响，不是它的主要作用。

#####场景2:*用户1*添加新pod

然后，*用户1*想要添加`D`到`Podfile`中。

然后**它们应该执行`pod install`**，这样即使维护`B`的人在上一次执行`pod install`之后发布版本`1.1.0`，这个项目会继续使用`1.0.0`版本，因为用户1只希望添加`D`，而不希望更新`B`。

>这就是为什么有些人会得到错误结果，因为他们使用了`pod update`命令——他们可能在想"我想要用新的pod更新我的项目"？——而不是使用`pod install`，来安装为项目安装新的pod。

#####场景3:*用户2*加入项目

然后，从来没有在这个项目工作的*用户2*加入到这个团队。他复制了这个项目，并执行了`pod install`。

`Podfile.lock`(应该被提交到git仓库)将能保证他能得到和*用户1*一样版本的pod。

即使`C`的`1.2.0`版本也已经可用了，*用户2*也将能得到`C`的`1.0.0`版本。因为那是`Podfile.lock`文件记录的版本。`C`已经被`Podfile.lock`(从名称就可以看出有锁定的意思)文件*锁定*为`1.0.0`版本。

#####场景4:查找新版本

然后，*用户1*希望检查pod是否有可用的新版本。他执行`pod update`命令，将会得到`B`有新版本`1.1.0`发布，`C`有新版本`1.2.0`发布。

*用户1*决定升级`B`，而不升级`C`；所以他将**执行`pod update B`**来升级`B`到`1.1.0`版本(相应地更改`Podfile.lock`)**但是**保持`C`的版本为`1.0.0`(*不会*升级到`1.2.0`)。

####在`Podfile`中，精确的版本不够用？
有时可能会觉得在`Podfile`中指定精确的pod版本，像`pod 'A', '1.0.0'`可能不能每个人都有与的团队里其他人都有相同的版本。

即使仅仅只想添加一个新pod时，他们有时甚至会用`pod update`命令，认为不会有升级其他pod的风险，因为他们已经在`Podfile`里固定了版本。

但是，**那样并不足以保证上述场景中的*用户1*和*用户2*所有pod总是能得到完全一样的版本。**

一个典型的例子，如果`A`依赖于`A2`，在`A.podspec`中有如下声明`dependency 'A2', '~>3.0'`。这样，在你的`Podfile`中使用使用`pod 'A', '1.0.0'`声明的确能强制使*用户1*和*用户2*都使用`A`的`1.0.0`版本。但是:

	* *用户1*可能以`A2`的`3.4`版本结束(因为那是`A2`的当时的最新版本)
	* 然而当*用户2*加入项目后运行`pod install`时，他可能得到`A2`的`3.5`版本(因为`A2`的维护人员同时发布了一个新的版本)

这就是什么只有使用`Podfile.lock`文件以及恰当地使用`pod install`和`pod update`命令可以保证每个成员在自己的电脑上都能使用相同版本的pod
















