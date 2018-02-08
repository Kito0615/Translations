# iOS故事板教程:第一部分

[原文](https://www.raywenderlich.com/160521/storyboards-tutorial-ios-11-part-1)

**更新:** 本教程已经由[Nicholas Sakaimbo](https://www.raywenderlich.com/u/lunarboots)更新到Xcode 9, iOS 11, Swift 4。本文原教程由[Matthijs Hollemans](https://www.raywenderlich.com/u/hollance)发布在[这里](https://www.raywenderlich.com/50308/storyboards-tutorial-in-ios-7-part-1)

故事板是在iOS 5中首次引入的一个令人兴奋的特性，它可以为你的应用程序节省构建用户界面的时间。故事板允许你在一个文件中创建或原型设计多个视图控制器的视图。

在使用故事板之前你一定使用过**Xib**文件，而且在一个**XIB**文件中只能创建一个视图（**UITableViewCell**, **UITableView** 或者其他支持的**UIView**类型）。

下面这张图片展示了故事板的样子，它和你将要在本教程中构建的故事板很相似:
![](https://koenig-media.raywenderlich.com/uploads/2017/05/StoryboardComplete.png)

你可能不知道这个App是做什么的，但是你可以看到它的使用场景以及它们是如何相关的。

故事板有以下几个优点:

* 你可以可视化布局你的视图控制器的样子和它们之间的联系。使用故事板你可以对你App的所有场景有一个更新的概念。
* 描述了不同场景之前的转换。这些转换被称为"segue"，通过在故事板中连接视图控制器来创建它们。由于有"segue"。你可以用更少的代码来创建用户界面。
* 使用原型和静态表格单元创建表格视图更容易。你几乎完全可以在故事板编辑器中设计你的表格视图，减少你的代码量。
* 让使用自动布局更容易。自动布局是一种允许你在元素之间定义数学关系来确定它们的位置和大小的特性。这个强大的特性让处理不同屏幕大小和像素的设备更简单。在本教程中，你会很少使用自动布局，它超出了本教程的范围。你可以阅读[自动布局教程](https://www.raywenderlich.com/?p=%2083129)或观看[视频教程](https://videos.raywenderlich.com/courses/62-beginning-auto-layout/lessons/1?_ga=2.183386606.918619933.1517901484-1487628899.1517901484)了解更多。

在本教程中，你要建立一个简单的程序来创建一个列表展示玩家和他们所玩的游戏以及技巧评分。这个过程中，你将学会使用故事板完成一些简单的任务。

#### 准备开始

打开Xcode创建一个新工程。使用**单视图应用程序**模板。如图:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/XcodeProjectOptions.png)

像下面这样填写模板信息，点击"下一步"就创建成功了。

* Product Name(软件名称): **Ratings**
* Organization Name(组织名称): 随便怎么填
* Organization Identifier(组织标识): 给应用程序的标识
* Language(程序语言): **Swift**
* 取消选中Use Core Data(使用Core Data)、Include Unit Tests(包含单元测试)、Include UI Tests(包含界面测试)。

一旦创建成功，Xcode的主窗口会像下面这样:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/RatingsMainWindow-1.png)

新的项目由三个文件组成: **AppDelegate.swift**、**ViewController.swift**和本教程的重点**Main.storyboard**.

在项目常规设置中，点击**Deployment Info** > **Device Orientation**，设置设备为**iPhone**。因为这个程序是一个只支持竖屏状态，所以取消选中**Landscape Left**和**Landscape Right**选项。

项目导航中打开**Main.storyboard**，在**Interface Builder**编辑器中查看。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/MainStoryboard-1-650x397.png)

视图控制器在故事板中的官方术语叫"scene"(场景)，但是你可以交换这些术语。一个场景在故事板中展示一个视图控制器。

这里你可以看到一个包含空视图的单视图控制器。左侧的箭头指向的视图控制器表示它是故事板中显示的初始视图控制器。

在故事板编辑器中设计布局是通过将控件从右下角的Object Library(对象库)中拖拽到视图控制器中完成的。

你会看到默认的场景大小是4.7英寸的屏幕。Xcode的故事板是默认激活自动布局和Size Classes(尺寸分类)的。自动布局和尺寸分类允许你创建灵活的用户界面，可以轻松的调整大小，这对支持不同大小的iPhone和iPad非常有用。要改变场景大小适应其他设备，点击故事板左下角的按钮。你就可以选择所有支持的设备大小，从12.9英寸的iPad Pro到3.5英寸的iPhone 4S，包括横向和纵向都可以选择。
![](https://koenig-media.raywenderlich.com/uploads/2017/05/SizeClasses-2.gif)

在本教程中，我们保持默认的场景大小-iPhone 7不变，如果你点击过其他不同的设备大小，请确保选择回默认。Xcode会自动调整已经存在和新添加的场景大小以适应当前选择的设备大小。

为了了解故事板编辑器如何工作的，从**Object Library**中拖拽一些控件到空白的视图控制器中。
![](https://koenig-media.raywenderlich.com/uploads/2017/05/DragControls.gif)

所有你拖拽进来的控制都可以在左侧的**Document Outline**中看到。
![](https://koenig-media.raywenderlich.com/uploads/2015/08/DocumentOutline.png)

故事板展示所有场景的内容。当前只有一个场景在你的故事板中，但在本教程中你将会再添加几个。

在场景上方有一个小号的**Document Outline**叫做**Dock**
![](https://koenig-media.raywenderlich.com/uploads/2015/08/TheDock.png)

**Dock**展示场景中最上面的对象。每个场景至少有一个**View Controller**(视图控制器)对象，一个**First Responder**(优先响应)对象和一个**Exit**(退出)对象。它也可以包含其他顶层对象。**Dock**可以方便的连接对象和方法。如果你需要连接场景中的某个控件，你只需要拖拽一下**Dock**的图标就可以了。

> 注意:
>   你可能不会经常使用**First Responder**。这是一个代理对象，它指的是在任何特定的时间内，任何对象的优先响应状态。例如，你可以从按钮的Touch Up Inside事件连接到优先响应者的**cut**: 方法。如果在某个时间点，文本框拥有了输入焦点，你可以点击那个按钮让当前的优先响应者-那个文本框，拷贝它的文本到粘贴板。

编译并运行程序，它看起来应该和你在编辑器中设计的一模一样（可能和下面的截图不一样）:
![](https://koenig-media.raywenderlich.com/uploads/2015/08/SimulatorTesting.png)

你定义的单一视图控制器已经设置为**初始视图控制器**，但是程序是如何加载它的？打开**AppDelegate.swift**可以找到答案:
> import UIKit
> @UIApplicationMain
> Class AppDelegate: UIResponder, UIApplicationDelegate {
>	var window: UIWindow?
>	func application(_ application: UIApplication,
>						didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?)
>					-> Bool {
>	*// Override point for customization after application launch.*
>	return true
>	}
> }

文件顶部的**@UIApplicationMain**属性指定了**AppDelegate**类作为模块的入口点。它是继承自**UIResponder**并拥有一个**UIWindow**属性的程序代理使用故事板的必要条件。所有的方法实现都是空的。甚至连**application(_ :didFinishLaunchingWithOptions:)**也只是简单返回真值。

秘密就在**Info.plist**文件中。在**Project Navigator**(项目导航)中打开**Info.plist**你会看到如下内容:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/InfoPlist.png)

故事板程序使用**UIMainStoryboardFile**关键字，也就是"Main storyboard file base name"表示程序启动时加载的故事板的名字。当显示这个设置时，**UIApplication**会加载这个名称的故事板文件，自动实例化"Initial View Controller"并把指定的控制器的视图放到新的**UIWindow**对象中。

你也可以在**Project Settings**(项目设置)中通用标签下的**Deployment Info**(配置信息)区域看到这个选项:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/ProjectSettingsMain.png)

现在开始用几个视图控制器创建真正的评分程序。

#### 把它添加标签控件中

你要开始创建的打分程序有一个标签界面，包含两个场景。使用故事板很容易创建。

打开**Main.storyboard**，然后删除之前编辑过的场景。可以通过点击**View Controller**上的**Document Outline**，然后按下删除键就可以了。

从**Object Library**拖拽一个**Tab Bar Controller**控件到画布中。你首先可能需要最大化Xcode窗口，因为Tab Bar Controller包含两个视图控制器，而且你需要一些操作空间。你可以通过双击画布来放大和缩小，也可以按住ctrl键来选择缩放级别。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/TabBarController.png)

新创建的Tab Bar Controller默认有两个视图控制器-每个标签一个。**UITabBarController**也叫做**container view**(容器视图)控制器因为它包含一个或多个其他视图控制器。另外两个常用的容器是Navigation Controller(导航控制器)和Split View Controller(分离视图控制器)，稍后将介绍导航控制器。

容器**关系**由标签栏和它所包含的视图控制器之间的箭头表示。特定的嵌入**关系**是指在箭头主体的中间看到的图标。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/12_sb_containment.png)

> 注意：如果你要把标签栏控制器和它包含的视图控制器作为一组同时移动或缩放，可以按住**⌘**键选择拖拽多个场景。这让同时移动它们更容易。（选中的场景会有一个蓝色的细边）

拖拽一个文本视图到第一个视图控制器中（当前叫"Item 1"）中，双击它，然后输入**First Tab**。同样拖拽一个文本视图到第二个视图控制器（当前叫"Item 2"）中并取名**Second Tab**。这样在标签之间切换时，你会看到变化。

编译并运行程序。你会在控制台看到类似的信息:
> Ratings[18955:1283100] Failed to instantiate the default view controller for UIMainStoryboardFile 'Main' - perhaps the designated entry point is not set?

幸运的是，错误在这里已经很清楚了——你没有设置过程序入口点，意味着你在删除之前的场景后没有设置初始视图控制器。要解决这个问题，选中Tab Bar Controller，在**Attributes Inspector**(属性检查窗口)选中**Is Initial View Controller**。
![](https://koenig-media.raywenderlich.com/uploads/2017/05/InitialViewController.png)

在画布中，你会看到一个箭头指向Tab Bar Controller：
![](https://koenig-media.raywenderlich.com/uploads/2014/09/13_sb_initialcontroller2.png)

现在运行程序，**UIApplication**将会在屏幕上显示Tab Bar Controller。编译并运行程序。现在你可以看到标签栏并且可以在不同的视图控制器中切换：
![](https://koenig-media.raywenderlich.com/uploads/2015/08/SimulatorAppWithTabs.png)

> 注意：要改变初始视图控制器，你也可以在不同的视图控制器之间拖拽箭头实现。

Xcode也有一个模板可以创建标签栏程序（叫做Tabbed Application template--标签栏程序模板）。你也可以使用，但是知道它的工作原理是很好的，这样当需要的时候，你就可以手动创建一个Tab Bar Controller。

> 注意：如果你连接超过五个场景到Tab Bar Controller，当你运行程序的时候，它会自动显示More...(更多)标签。相当优雅。

#### 添加一个表格视图控制器

当前Tab Bar Controller包含的两个场景都是**UIViewController**的实例。你需要用**UITableViewController**替换第一个标签场景。

在**Document Outline**中点击第一个视图控制器选中并删掉它。拖一个**Table View Controller**到画布中之前那个场景所在的位置：
![](https://koenig-media.raywenderlich.com/uploads/2017/06/AddTableViewController.png)

接下来，你想把这个Table View Controller放到一个导航控制器中。首先，选中表格视图控制器。然后，在Xcode菜单栏依次选择**Editor->Embed In->Navigation Controller**。这样又添加了一个控制器到画布中：
![](https://koenig-media.raywenderlich.com/uploads/2017/06/NavigationController.png)

你也可以从对象库(Object Library)中拖拽一个导航控制器(Navigation Controller)到画布中，然后把表格视图嵌入其中，但是通过嵌入命令是一个很好节约时间的常见操作。

因为导航视图控制器也是一个容器视图控制器（像标签栏视图控制器一样），它也有一个指向表格视图控制器的关系箭头。你可以在**Document Outline**中看到这些关系：
![](https://koenig-media.raywenderlich.com/uploads/2017/06/Relationship.png)

可以看到嵌入的表格视图控制器给了它一个导航栏。Interface Builder自动添加的因为这个场景会显示在导航控制器中。它并不是一个真的**UINavigationBar**对象，只是一个模拟的。当它显示在标签栏控制器中的时候，Simulated Metrics(模拟向量)将会推断场景的上下文(context)显示导航栏。

要把这两个新的场景连接到标签栏控制器中，按住**ctrl**，从标签栏控制器拖拽到导航栏控制器。当松开鼠标的时候，会弹出一个小的菜单。选择**Relationship Segue->view controllers**选项:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/EmbedVC1-2.gif)

这样就在两个场景之间建立了新的联系。就像你看到的标签栏控制器包含的其他控制器一样，这也是一个嵌入关系。

标签栏控制器包含两个嵌入关系，每个标签栏一个。导航控制器它自己也有一个和表格视图控制器的嵌入关系。

当你连接新的联系时，一个新的标签栏添加到标签栏控制器中，命名为"Item"。现在这个程序，你想这个新的场景在第一个标签，只需要拖拽标签调整位置就可以了：
![](https://koenig-media.raywenderlich.com/uploads/2014/09/Drag-tab-items.gif)

编译并运行程序看看。第一个标签现在包含一个有表格视图的导航控制器。
![](https://koenig-media.raywenderlich.com/uploads/2015/08/SimulatorFirstTabWithTableView.png)

在你添加实际功能到这个程序之前，你需要简单整理一下故事板。把第一个标签命名为"Players"，第二个标签命名为"Gestures"。你不需要在标签栏控制器本身改变，只需要改变标签连接的视图控制器。

只要你把视图控制器连接到标签栏控制器，就可以在**Document Outline**或当前场景下边看到一个**Tab Bar Item**对象。用这个标签栏对象来设置标签的标题和在标签栏控制器上看到的图像。

选择导航控制器中的标签栏对象，在**Attributes Inspector**中设置它的标题为**Players**:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/TabBarPlayers.png)

然后，用上面同样的方法给第二个标签栏对象重命名为**Gesture**。

一个好的设计的程序应该在标签栏上放上一些图标。[本教程资源](https://koenig-media.raywenderlich.com/uploads/2015/08/StoryboardResources.zip)包含了一个命名为**Images**的文件夹。把它拖到项目的**Assets.xcassets**目录中。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/DragIntoXCAssets-1.png)

打开**Main.storyboard**，在Players标签栏的**Attributes Inspector**中，选择**Players**图片。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/PlayersImage.png)

接着，给Gestures标签栏添加**Gestures**图片。

嵌入在导航控制器中的视图控制器有一个**Navigation Item**(导航栏菜单)，用来设置导航条。在**Document Outline**中选择表格视图控制器的导航栏菜单，在属性检查器中修改它的标题属性为**Players**:
![](https://koenig-media.raywenderlich.com/uploads/2017/06/NavigationItem.png)

可以在**Document Outline**中看到当前场景的标题已经变成**Players**.

> 注意：同样的，你也可以双击导航条来修改它的标题。你应该双击表格视图控制器中的模拟导航条，而不是导航控制器中实际的导航条对象。

编译并运行程序。现在对你在不写一行代码的情况创建的漂亮的标签栏感到惊讶吧！
![](https://koenig-media.raywenderlich.com/uploads/2015/08/AppWithTabBarImages.png)

#### 单元格原型

单元格原型让你直接在故事板编辑器中为你的表格视图单元格轻松设计自定义布局。

表格视图控制器有一个空白的单元格原型。点击这个单元格选中它并在**Attributes Inspector**中设置**Style**为**Subtitle**。这直接让单元格包含两个文本。

> 注意：如果故事板上有许多重叠的内容，可能导致不能精确的点击到你想点击的控件。遇到这样的问题，有几种方法可以解决。一种是可以在左侧的**Document Outline**中选择对象。第二种是使用快捷键:按住control+shift键点击你想选择的区域，会直接在你鼠标点击的地方弹出一个让你选择元素的菜单。

如果你在以前使用过表格视图并且手动创建过单元格，你应该认识**UITableViewCellStyle.Subtitle**样式。使用单元格原型，你可以像刚才一样选择内置的单元格样式，也可以自定义设计自己的单元格样式(很快就可以完成)。

设置**Accessory**(附件)属性为**Disclosure Indicator**(发现指示器)，并且设置**Identifier**(标识)属性为**PlayerCell**。所有的原型单元格必须有一个复用标识符这样你可以用代码找到它们。另外，设置单元格**Selection**(选择)属性为**None**。

> 注意：设置单元格选择属性为**None**是为了防止用户通过点击**PlayerCell**来编辑已经存在的单元格。尽管在本教程中不会添加这个功能，你将会在第二部分结束的时候充分了解此功能，并在示例项目中实现，以便进一步练习。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/CellSetup-2.png)

编译并运行程序，没有任何变化。并不奇怪：你还需要为表格添加数据源让它知道哪些行应该显示。这是你接下来要做的事。

向工程中添加一个新的文件。在iOS/Source标签下选择**Cocoa Touch Class**模板。将这个类命名为**PlayersViewController**并让它继承自**UITableViewController**。取消选中**Also create XIB file**选项。选择**Swift**作为编程语言然后点击下一步创建 。
![](https://koenig-media.raywenderlich.com/uploads/2015/08/PlayersViewController.png)

打开**Main.storyboard**选中表格视图控制器(确保选中的是视图控制器本身而不是它的一个视图)。在**Identity Inspector**中，设置它的**Class**(类)为**PlayerViewController**。这是将故事板中的场景与自定义视图控制器子类连接起来的必要步骤。不要忘了这一步，否则不会调用你的类。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/PlayersVCClass.png)

现在当你运行程序的时候，故事板中的表格视图控制器就是**PlayersViewController**类的一个实例。

表格视图应该显示一系列的玩家信息，因此现在你将要为程序创建主要数据模型-包含**Player**的一个数组。向工程中添加一个iOS/Source标签下的**Swift File**模板文件，并命名为**Player**。

用下面的代码替换**Player.swift**文件内容：

> import Foundation
> struct Player {
>	*// MARK: -Properties*
>	var name: String?
>	var game: String?
>	var rating: Int
> }

到这里就没有别的什么要做的了。**Player**只是*玩家名字*, *所玩的游戏*和*游戏评分(1-5星)*这三个属性的容器。需要注意的是，你并没有自定义初始化函数，这个结构体会自动接收默认的*memberwise initializer*用来设置它的所有属性。

接着，用**SampleData**命名一个**Swift File**模板。用以下内容替换**SampleData.swift**的内容：
> import Foundation
> final class SampleData {
> 	static func generatePlayersData() -> [Player]{
> 		return [
>			Player(name: "Bill Evans", game: "Tic-Tac-Toe", rating: 4),
>			Player(name: "Oscar Peterson", game: "Spin the Bottle", rating: 5),
>			Player(name: "Dave Brubeck", game: "Texas Hold 'em Poker", rating: 2)
>			]
>	}
> }

现在你在**SampleData**中已经定义了一个静态方法来产生一组硬编码**Player**对象数据了。

然后，打开**PlayersViewController.swift**文件，替换文件为以下内容：
> import UIKit
> class PlayerViewController: UITableViewController{
> 	// MARK: -Properties
> 	var players = SampleData.generatePlayersData()	
> }

你可以在**PlayerViewController**中定义**players**变量时设置好样例数据。但是这个数据可以来自plist文件或其他外部源，因此给视图控制器添加外部数据是很明智选择。

现在你已经有一个组**Player**对象了，继续在**PlayersViewController**中连接数据源。仍然在**PlayersViewController.swift**文件中，在文件最后添加如下扩展:
> //MARK: -UITableViewDataSource
> extension PlayersViewController {
> 	override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int{
> 		return players.count
> 	}
> 	override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
> 		let cell = tableView.dequeueReusableCell(withIdentifier: "PlayerCell", for: indexPath)
> 		let player = players[indexPath.row]
> 		cell.textLabel?.text = player.name
> 		cell.detailTextLabel?.text = player.game
> 		return cell
> 	}
> }

**dequeueReusableCell(withIdentifier: for:)**方法会检查是否存在可以重复使用的单元格。如果没有，它会自动生成一个单元格原型并返回给你。你仅仅需要做的提供一个在你在故事板编辑器设置的复用标识-在本教程中是**PlayerCell**。不要忘了设置这个标识，否则这个规则就不适用了。

编译并运行程序，表格视图可以显示玩家信息了！
![](https://koenig-media.raywenderlich.com/uploads/2015/08/AppWithPlayers.png)

仅仅用几行代码就可以使用单元格原型了。我觉得太棒了！
> 注意：在这个程序中，你只使用了一种单元格原型。如果你的表格需要显示不同的单元格，你可以在故事板添加别的单元格原型。保证每个单元格都有自己的复用标识符。

#### 设计你自己的单元格原型

使用标准的单元格样式对大多数程序来说已经可以了，但是在这个程序中你想要添加图片到单元格右边表示玩家的评分。在标准单元格样式中不支持在那个位置使用图片，所以你必须创建一个自定义的单元格。

打开**Main.storyboard**，在表格视图中选择单元格原型，在**Attributes Inspector**中设置它的**Style**为**Custome**(自定义)。默认的文本消失了。

首先让单元格高一点。在**Size Inspector**(尺寸检查器)中改变**Row Height**(行高)的值或者拖拽单元格下方的手柄调节单元格的高度都可以。设置单元格的高度为60。

从对象库中拖拽两个**Label**(文本标签)对象到单元格中，把它们放在先前标准文本标签所在的位置。在**Attributes Inspector**调整任何你喜欢的字体和颜色。设置上面一个标签名称为**Name**，下面一个标签为**Game**。

在**Document Outline**中按住command键选中Name和Game文本标签，点击**Editor->Embed In->Stack View**。

> 注意：重叠视图是在iOS 9引入的，可以轻松布局视图集合。你可以在[UIStackView教程中](https://www.raywenderlich.com/?p=114552)了解更多。

拖拽一个**Image View**到单元格中并把它放在右侧指示器的旁边。在尺寸检查器中，调整图片大小为宽81个像素点，高35个像素点。设置图片视图的**Content Mode**为**Center**(居中)-在视图的Attributes Inspector选项卡中，这样无论什么样的图片在里面显示的时候都不会被拉伸。

在**Document Outline**中按住command键选中重叠视图和图片视图。点击**Editor->Embed In->Stack View**。Xcode会自动创建一个包含这两个视图的水平重叠视图。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/InitialStackView-1.png)

选中新的水平重叠视图，在**Attributes Inspector**中，修改(Alignment)对齐方式为**Center**(居中)，并将(Distribution)布局设置为**Equal Spacing**(等间距)。

现在简单设置一下这个控件的自动布局。在故事板的右下方，点击Pin(指针)图标：
![](https://koenig-media.raywenderlich.com/uploads/2017/05/PinIcon.png)

设置约束为Top:0,Right:20,Bottom:0和Left:20。确保这四个指针指向的值如图所示。然后点击弹出窗口下方的**Add 4 Constrains**(添加4个约束)按钮。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/StackViewConstraints.png)

如果你的重叠视图有橙色的约束，那它就放置错了。要解决这个问题，选中水平重叠视图然后点击**Editor->Resolve Auto Layout Issues->Update Frames**(在选中视图区的菜单中)

你可能在**Document Outline**中看到一个红色高亮的小箭头，它表示没有解决重叠视图的布局问题。点击这个箭头然后点击红色的小圆圈查看Xcode的自动修正。选择Name文件标签或Game文本标签的**Change Priority**(修改优先级)可以隐藏这个警告。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/FixVerticalHuggingPriority.png)

最终设计的单元格原型应该像这样：
![](https://koenig-media.raywenderlich.com/uploads/2017/06/FinalCell-1.png)

因为这是一个自定义的单元格，你不能再用**UITableViewCell**的**textLabel**和**detailTextLabel**属性设置文字了。这两个文本标签已经不再与这个单元格相关联了；它们在对标准单元格有效。相反，你应该继承自**UITableViewCell**来提供这个功能。

> 注意：在本教程中你可以使用**Tags**，但是标签并不提供编译器在运行时检查的对象类型，因此你必须在运行时使用类型转换和检查，如果可能你应该尽量避免。由于这个原因，在本程序中不再作为谨慎技术。

#### 使用单元格子类

向工程中添加新的**Cocoa Touch Class**模板文件。命名为**PlayerCell**并让它继承自**UITableViewCell**类。取消选中创建XIB选项，因为在故事板已经有了。

然后，把下面的内容添加到**PlayerCell**类的定义中：
> // MARK: - IBOutlets
> @IBOutlet weak var gameLabel: UILabel!
> @IBOutlet weak var nameLabel: UILabel!
> @IBOutlet weak var ratingImageView: UIImageView!

这些**IBOutlets**控件可以连接到你的故事板场景中。

然后，在**IBOutlets**后面添加如下属性：
> *//Mark: -Properties*
> var player: Player? {
> 	didSet{
> 		guard let player = player else { return }	
> 		gameLabel.text = player.game
> 		nameLabel.text = player.name
> 		ratingImageView.image = image(forRating: player.rating)
> 	}	
> }

当设置**玩家**属性的时候，它会验证是否有值，如果有，就更新**IBOutlets**正确信息。
接着，在**player**后面添加以下方法：

> func image(forRating rating: Int) -> UIImage> {
> 	let imageName = "\(rating)Stars"
> 	return UIImage(named: imageName)
> }

这个函数会根据评分参数返回不同的图片。

接下来，打开**Main.storyboard**，选择单元格原型**PlayerCell**并在**Identity Inspector**中修改它的类为**PlayerCell**。现在无论什么时候调用**dequeueReusableCell(withIdentifier: for:)**方法，它都会返回一个**PlayerCell**的实例而不是常规**UItableViewCell**实例。

> 注意：你已经设置了与复用标识一样的类名**PlayerCell**，但那仅仅是因为我喜欢保持一致性。类名和复用标识符并没任何关系，所以你也可以给它们不同的名称，只要你愿意。

最后，关联文本标签和图片视图到类。在故事板中切换到**Connection Inspector**(关联检查器)，选择从**Document Outline**或画布中选择**Player Cell**。把**nameLabel**属性拖到**Document Outline**或画布中关联检查器的**Name**文本标签。**gameLabel**和**ratingImageView**重复上述操作。
![](https://koenig-media.raywenderlich.com/uploads/2017/06/NameLabel-1.gif)

> 注意：你应该关联控件到表格视图单元格，而不是视图控制器！你可以看到，当你的数据源用**dequeueReusableCell**方法向表格视图请求一个新的单元格时，表格视图不会返回一个真实的单元格原型，而是一个副本(或者如果可能则是之前的单元格复用的)。

> 这说明在任何时间点可能会有不止一个**PlayerCell**实例。如果你把文本标签从单元格连接到了视图控制器，几个不同的文本标签会使用同一个outlet。那就会导致出错。（另一方面，把单元格原型连接到视图控制器的方法上没有问题。如果你已经在你的单元格上自定义按钮或其他**UIControls**控件。）

现在你已经连接上了属性，你可以简化一下数据源代码。打开**PlayersViewController.swift**，修改**tableView(_ :cellForRowAt:)**内容如下：
> override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
>	let cell = tableView.dequeueReusableCell(withIdentifier: "PlayerCell", for: indexPath) as ! PlayerCell
> 	let player = players[indexPath.row]
> 	cell.player = player
> 	return cell
> }

这不差不多。你现在将从**dequeueReusableCell**方法得到的对象转换为**PlayerCell**，并将正确的**玩家**传给单元格。在**PlayerCell**中设置player(玩家)变量时会自动赋值给文本标签和图片视图。使用单元格原型让你表格视图变得不那么混乱不是很好吗？

编译并执行程序。
![](https://koenig-media.raywenderlich.com/uploads/2015/08/WrongCellHeight-480x297.png)

看起来有点不对劲--单元格好像被压扁了。你已经改变单元格原型的高度，但是表格视图并没有考虑到。有两种方法可以修改：你可以修改表格视图的**Row Height**属性，或者实现**tableView(_ : heightForRowAt:)**方法。前一种方法对于本例中是可以的，因为我们只有一种单元格类型而且我们已知了它的高度。

> 注意：如果你提前不知道你的单元格高度或者不同的行可能有不同的高度的时候，你应该使用**tableView(_ :heightForRowAt:)**。

打开**Main.storyboard**，在表格视图的**Size Inspector**中设置**Row Height**为60。
![](https://koenig-media.raywenderlich.com/uploads/2017/08/Screen-Shot-2017-08-07-at-9.52.06-PM.png)

编译并运行程序。
![](https://koenig-media.raywenderlich.com/uploads/2015/08/AppProperRowHeight.png)

这就更好了不是吗!

> 注意：如果你是通过拖拽而不是输入值改变的单元格高度，表格视图的**Row Height**属性也会自动改变。因此你第一次运行的时候也可能是运行正确了。