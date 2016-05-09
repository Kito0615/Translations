#如何创建自定义控件

---
本文翻译自:[How to Make a Custom Control Tutorial: A Reusable Slider](https://www.raywenderlich.com/76433/how-to-make-a-custom-control-swift)

**2014年12月8日更新**:更新到Xcode 6.1.1

**更新日志**这篇教程被Mikael Konutgan更新支持到iOS8，使用Swift，用Xcode 6 beta 7运行过。[原文章](https://www.raywenderlich.com/36288/how-to-make-a-custom-control)由团队成员[Colin Eberhardt](http://www.raywenderlich.com/u/ColinEberhardt)执笔。

*通过这篇文章，你将学会实现一个带有两个滑块的滑动条。*

![](http://www.raywenderlich.com/wp-content/uploads/2014/07/iOS-Simulator-Screen-Shot-12-Jul-2014-11.54.42-e1405158991678.png)

---
控件是任何一个应用程序中最重要的模块之一。它们作为图形元件允许你的用户看到，并且可以和他们的应用程序数据进行交互。本篇教程将向你展示如何自定义一个可以重复使用的控件。苹果提供了大概20种控件，如:*UITextFiled*, *UIButton*和*UISwitch*。使用预置工具栏(Toolbox)里的控件，就可以创建多种多样的界面。

但是，有时候你需要做点不一样的事；有些事其他的控件不能**恰好**完成你想要的功能。

自定义控件只不过是你自己创建的控件，即不是继承自UIKit 框架的控件。自定义控件，就像标准控件一样，应该普通而功能多样。结果是，你会发现，有一个活跃的社区，那里的开发者都乐于分享他们自定义的控件。

在这篇教程中，你将会实现完全你自定义的滑杆控件。这个控件像一个双端滑杆，通过它你可以选择最大值和最小值。你会接触在已经存在的控件上扩展的概念，设计并实现你控件的API(Application Programming Interface:应用编程接口，简称“接口”)，甚至你可以分享你的新控件到开发者社区。

开始自定义之旅吧！

>注意：在编程这篇教程的过程中，我们理解的是我们不能发布iOS 8的截图，因为它还在测试当中。文中所有的截图都是来自iOS预览版，但是你们的结果看起来这个非常相似。

**准备阶段**

假设你正在开发一个搜索房屋出售列表的应用程序。这个假设的程序允许用户用一个确定的价格范围过滤搜索结果。

你*可以*用一对`UISlider`控件提供给用户这个界面，一个Slider设置价格的最大值，另一个设置价格的最小值。然而，这个界面并不能真正帮助用户直观的感受到价格范围。使用一个两个滑块的Slider表示用户搜索的高的价格和低的价格范围显示更好。

你*可以*继承自`UIView`来创建这个带范围的Slider，也可以定制一个视图表示价格范围。这可能对你程序环境有好处——但是可能对你导入其他程序中有点困难。

更好的办法是创建一个新的尽量普通控件，这样你可以在任何适当的时候重复利用它。这就是自定义控件的本质。

打开Xcode。点击`File->New File`，选择`iOS/Application/Single View Application`模板，点击`Next`。在下一个页面，输入`CustomSliderExample`作为工程名称，选择你希望的`组织名称(Organization Name and Organization Identifier)`，然后确保你选择的是`Swift`作为你的开发语言，`iPhone`作为你的`目标设备`，请不要选择`Use Core Data`。

最后，选择你保存工程的位置，点击`Create`。

要创建你新的控件，当你创建一个自定义控件的时候，你需要你明确你创建的控件是哪个类的子类或扩展。

为了让你的控件在程序中可以展示，你的类必须是`UIView`的子类。

如果你查看过苹果`UIKit`的参考资料，你会看到许多框架控件如:`UILabel`和`UIWebView`都是直接继承自`UIView`的。然而，也有许多的控件，如:`UIButton`和`UISwitch`是继承自`UIControl`的，继承关系如下图:

![](https://cdn2.raywenderlich.com/wp-content/uploads/2013/03/RangeSliderClassStructure-480x260.png)

>注意：
想要了解UI控件的继承关系，请查看[UIKit Framework Reference](http://developer.apple.com/library/ios/#documentation/uikit/reference/UIKit_Framework/Introduction/Introduction.html)

`UIControl`的实现，是[`目标-行为模式`](https://en.wikipedia.org/wiki/Target%E2%80%93action)，它是通知订阅者改变的机械操作。`UIControl`还有几个与控制状态相关的属性。你会在你的自定义控件中用到`目标-行为模式`，因此`UIControl`将作为一个好的起点。

在项目导航栏中右键点击`CustomSliderExample`分组，选择`New File...`，然后选择`iOS/Source/Cocoa Touch Class`模板，点击`Next`。取名叫做`RangeSlider`，输入`UIControl`到`Subclass of`一栏。确保选择的语言是`Swift`。点击`Next`，然后，点击`Create`选择保存这个文件默认存储路径。

尽管写代码非常酷，你也可能想看看你的控件在屏幕上渲染的效果，好检查你的进度。在你开始为你的控件写任何代码之前，你应该添加你的控件到视图控制器中，好让你可以看到控件的'进化`(改变)。

打开的你的`ViewController.swfit`文件，输入以下内容:

```
import UIKit

class ViewController:UIViewController{
	let rangeSlider = RangeSlider(frame:CGrectZero)
	
	override func viewDidLoad(){
		super.viewDidLoad()
		
		rangeSlider.backgroundColor = UIColor.redColor()
		view.addSubview(rangeSlider)
	}
	
	override func viewDidLayoutSubviews(){
		let margin:CGFloat = 20
		let width = view.bounds.width - 20 * margin
		rangeSlider.frame = CGRect(x: margin, y: margin + topLayoutGuide.length, width: width, height: 31.0)
	}
}
```

以上代码用一个指定的frame创建了一个你的全新的控件的实例并添加到了视图上。控件的背景颜色被设置成了红色，这样可以与应用程序的背景颜色区别开来。如果你不设置控件的背景颜色为红色，控件的颜色将是透明的，这样你就会想知道你的控件去哪儿了。

编译并运行你的程序，你将会看到如下效果:

![](https://cdn1.raywenderlich.com/wp-content/uploads/2013/03/StepOne-170x320.png)

在你添加可视元素到你的控件之前，你先需要几个属性用来记录几个信息并存储在你的控件中的属性。这将形成你控件的应用程序接口或简称API的开始。

>注意:
你的控件的API定义了方法和属性，这些定义由你决定暴露给其他将要使用你的控件的开发者。你将会在文章的后面阅读到关于设计的一些内容——至于现在，跟上就好!

**添加默认控属性**

打开`RangeSlider.swift`文件，用如下代码替换:

```
import UIKit

class RangeSlider:UIControl
{
	var minimumValue = 0.0
	var maximumValue = 1.0
	var lowerValue = 0.2
	var upperValue = 0.8
}
```
这四个属性是所有你需要的描述这个控件的属性，提供了范围的最大值和最小值，同时提供了供用户设置的较大值和较小值。

一个好的设计的控件，应该定义一些属性的默认值，否则当你的控件渲染到屏幕上是将会看起来很奇怪。你上面那样做就很好。

现在，该是添加为你的控件添加交互元素的时候了，即代表较大和较小值的滑块，和记录两个滑块之间的轨道。

**图片 VS. 图形上下文**

有两种主要途径可以渲染你的控件到屏幕上:

1. 图片——创建图片代表控件的多种元素
2. 图形上下文——使用图形上下文的层的组合渲染你的控件

下面列表每种方法的优缺点:

*图片:*在程序员这方面看来，使用图片构建你的控件可能是一个简单的选项——只要你知道如何**画**。如果你想其他程序员也能改变你的控件的外观，你应该只暴露这些图片作为你为`UIImage`属性。

使用图片为使用你控件的开发者们提供了最强的适应性。开发者可以改变你控件的外观的每一个像素甚至每个细节，但是这需要好的图形设计技能——而这从代码去调整很难。

*图形上下文:*使用图形上下文去构建你的控件，也就意味着你必须自己去写渲染代码，这可能需要更多一点的努力。然后，这个技术允许你创建一个更合理的API。

使用图形上下文，你可以参数化你控件的每个特点，如颜色，边框宽度和弯曲度——画的每个可视的元素都在你的掌控之中。这个方法允许使用你控件的开发者完全定制它去适应他们的需求。

>注意:
有趣的是，苹果公司倾向于在他们的控件中使用图片。这有很可能是因为他们知道每个控件的大小而不倾向于希望允许太多的自定义。毕竟，他们希望所有的应用程序最终都有一个相似有外观感受。

打开`RangeSlider.swift`文件，在文件的最上方，`import UIKit`下面，添加如下引用:

`import QuartzCore`

然后，在上面我们定义的下方，为`RangeSlider`添加如下属性。

```
let trackLayer = CALayer()
let lowerThumbLayer = CALayer()
let upperThumbLayer = CALayer()

var thumbWidth:CGFloat {
	return CGFloat(bounds.height)
}
```

上面三个层——`trackLayer`,`lowerThumbLayer`,`upperThumbLayer`——将会用于渲染你的控件的不同元件。`thumbWidth`将是用于布局目的。

下一步是控件的一些默认的图形属性的设置。

在`RangeSlider`类中，添加如下初始化函数和帮助函数:

```
override init(frame:CGRect) {
	spuer.init(frame:frame)
	
	trackLayer.backgroundColor = UIColor.blueColor().CGColor
	layer.addSublayer(tracklayer)
	
	lowerThumbLayer.backgroundColor = UIColor.GreenColor().CGColor
	layer.addSublayer(lowerThumbLayer)
	
	upperThumbLayer.backgroundColor = UIColor.GreenColor().CGColor
	layer.addSublayer(upperThumbLayer)
	
	updateLayerFrames()
}

required init(coder:NSCoder)
{
	super.init(coder:coder)
}

func updateLayerFrames(){
	trackLayer.frame = bounds.rectByInsetting(dx:0.0, dy:bounds.height/3)
	trackLayer.setNeedsDisplay()
	
	let lowerThumbCenter = CGFloat(positionForValue(lowerValue))
	
	lowerThumbLayer.frame = CGRect(x:lowerThumbCenter - thumbWidth / 2.0, y:0.0, width:thumbWidth, height:thumbWidth)
	lowerThumbLayer.setNeedsDisplay()
	
	let upperThumbCenter = CGFloat(positionForValue(upperValue))
	
	upperThumbLayer.frame = CGRect(x:upperThumbCenter - thumbWidth / 2.0, y:0.0, width:thumbWidth, height:thumbWidth)
	upperThumbLayer.setNeedsDisplay()
}

func positionForValue(value:Double)->Double{
	return Double(bounds.width - thumbWidth) * (value - minimumValue) / (maximumValue - minimumValue) + Double(thumbWidth / 2,0)
}
```

初始化函数仅仅只是创建了三个层，并将它们添加到控件的根层作为子层，然后`updateLayerFrames`函数更新它们的边框以适应。

最后，`positionForValue`用简单的比例换算计算出控件在屏幕上最大值和最小值之间的位置。

接下来，重写了`frame`方法，然后在`RangeSlider.swift`中添加以下代码实现观察者属性。

```
override var frame:CGRect {
	didSet{
		updateLayerFrames()
	}
}
```

当大小改变的时候，观察者属性更新层大小。这是很必要的，当控件在使用一个大小初始化的时候。而`RangeSlider.swift`中的大小并不是它的最终大小。

编译并运行你的程序，你的控件开始有点样子了！它看起来应该和下面图片相似:

![](https://cdn2.raywenderlich.com/wp-content/uploads/2013/03/SliderTwo-170x320.png)

记住，红色的是整个控件的背景。蓝色的是"进度条"的背景，绿色是较大值和较小值两个滑块的位置。

你的控件开始从视觉上有一定样子了，但是大多数控件提供了供用户交互的方式。

对于你的控件，用户必须能够拖拽每个滑块来设置他们期望的范围控制。你将要处理这些交互，并且更新包括UI(界面)和控件暴露出来的属性。

**添加交互逻辑**

交互逻辑需要保存哪一个滑块被拖动过，并且在UI上表现出来。控件的层是放置这些逻辑最好的地方。

在开始之前，在Xcode中创建一个新的`Cocoa Touch Class`继承自`CALayer`并命名为`RangeSliderLayer`。

在`RangeSliderThumbLayer.swift`用下面的内容替换其中的内容:

```
import UIKit
import QuartzCore

class RangeSliderThumbLayer:CALayer{
	var highlighted = false
	weak var rangeSlider:RangeSlider?
}
```

这里只添加了两个属性:一个是表示滑块是否是高亮(即按住)状态，另一个反向引用到Slider。因为RangeSlider包含两个滑块层，所以这个反向引用是`weak`修饰，这样避免了循环强引用。

打开`RangeSlider.swift`把`lowerThumbLayer`和`upperThumbLayer`属性，修改它们的定义为如下:

```
let lowerThumbLayer = RangeSliderLayer()
let upperThumbLayer = RangeSliderLayer()
```

还是在`RangeSlider.swfit`中，找到`init`方法，添加下面两行:

```
lowerThumbLayer.rangeSlider = self
upperThumbLayer.rangeSlider = self
```

上面两行只设置了layer的反向引用`rangeSlider`属性到`self`。

编译并执行你的程序，检查显示是否和刚才一样。

既然你的控件有使用了`RangeSliderLayer`的滑块层，你需要在那里添加用户拖拽的功能。

**添加控制处理**

打开`RangeSlider.swift`在属性中添加下面一行

`var previousLocation = CGPoint()`

这个属性将会用来记录点击的位置。

你准备怎样为你的控件记录不同的点击和释放事件呢？

`UIControl`提供了一些追踪点击事件的方法。继承自`UIControl`的类可以重写这些方法来满足自己的交互逻辑。

在你自定义的控件中，你将会重写三个`UIControl`的关键方法: `beginTrackingWithTouch`, `continueTrackingWithTouch`和`endTrackingWithTouch`。

在`RangeSlider.swift`中添加如下内容:

```
override func beginTrackingWithTouch(touch:UITouch, withEvent event:UIEvent) -> Bool {
	previousLocation = touch.locationInView(self)
	
	// Hit test the thumb layers
	if lowerThumbLayer.frame.contains(previousLocation) {
		lowerThumbLayer.highlighted = true
	} else if upperThumbLayer.frame.contains(previousLocation) {
		upperThumbLayer.highlighted = true
	}
	
	return lowerThumbLayer.highlighted || upperThumbLayer.highlighted
}
```

上面的方法将在用户点击控件的时候调用。

首先，它将点击事件转换为控件坐标空间。接着，检查每个滑块层是否包含点击事件坐标。然后上面函数的返回值表示的父类`UIControl`是否继续追踪点击事件。

持续追踪点击事件判断滑块是否是高亮状态。

既然你已经初始化了点击事件，当用户滑动在屏幕上移动手指的时候，你将需要处理这些点击事件。

在`RangeSlider.swift`中添加如下代码:

```
func boundValue(value:Double, toLowerValue lowerValue:Double, upperValue:Double) -> Double {
	return min(max(value, lowerValue), upperValue)
}

override func continueTrackingWithTouch(touch:UITouch, withEvent event:UIEvent) -> Bool {
	let location = touch.locationInView(self)
	
	// 1.Determine by how much the user has dragged
	let deltaLocation = Double(location.x - previousLocation.x)
		let deltaValue = (maximumValue - minimumValue) * deltaLocation / Double(bounds.width - thumbWidth)
	previousLocation = location
	
	// 2. Update the values
	if lowerThumbLayer.highlighted {
		lowerValue += deltaValue;
		lowerValue = boundValue(lowerValue, toLowerValue:minimumValue, upperValue:upperValue)
	} else if upperThumbLayer.highlighted {
		upperValue += deltaValue
		upperValue = boundValue(upperValue, toLowerValue:lowerValue, upperValue:maximumValue)
	}
	
	// 3. Update the UI
	CATransaction.begin()
	CATransaction.setDisableActions(true)
	
	updateLayerFrames()
	
	CATransaction.commit()
	
	return true
}
```

`boundValue`会限制传入的值，这样才可以指定范围。使用这个辅助函数比调用`min / max`更容易理解。

这里的`continueTrackingWithTouch`会崩溃，通过注释说明:

1. 首先，你计算了改变的位置，这决定了用户手指移动了多少像素。然后把它转换成基于控件的最小值和最大值缩放后的值。
2. 在这里，你是根据用户拖拽滑块来调整范围的。
3. 在`CATransaction`中，这段代码设置`disableActions`标志。确保滑块位置、大小的改变可以即时响应，而不使用动画。最后，调用`updateLayerFrames`方法使滑块移动到恰当的位置。

你已经写好了拖拽滑块的代码了——但是你还需要处理点击结束的事件。

在`RangeSlider.swift`中添加如下代码:

```
override func endTrackingWithTouch(touch:UITouch, withEvent event:UIEvent) {
	lowerThumbLayer.highlighted = false
	upperThumbLayer.highlighted = false
}
```

上面的代码只是重置了滑块的高亮状态。

编译并运行你的工程，试一下你闪亮的新滑杆！你应该可以拖拽绿色的滑块了。

你会注意到当滑杆追踪触摸事件的时候，你可以在控件范围内外随意拖拽，而控件还是可以追踪触摸事件。这对于低精确点的小屏幕设备来说是一个非常重要且有用的功能——或者更熟知的手指。

**通知**
现在，你已经有一个可以交互的控件，用户可以用它控制范围的上下边界。但是你要怎样让通知到程序知道这个控件有了一个新的值了？

其实有很多不同的设计模式让你可以实现提供通知: `NSNotification(通知), Key-Value-Observing(KVO:键-值-观察者)`和`delegate(代理),Target-Action(目标-方法)`设计模式等。有太多选择了。

那怎么办呢？

如果查看`UIKit`控件，你会发现苹果并没有使用通知或者鼓励使用KVO，所以为了UIKit的统一性，你可以有两种方法执行。另外两种模式——`代理模式`和`目标-方法模式`——UIKit中常见的两种。

下面是代理模式和目标-方法模式的详细分析:

`代理模式`:使用代理模式，你需要提供一个协议，这个协议包含一系列方法，这些方法用于通知范围的改变。控件有一个属性，通常叫做`delegate`，它可以是任意实现了这个协议的类的实例。典型的例子是`UITableView`提供了一个`UITableViewDelegate`的协议，注意，控件只接受一个代理实例。一个代理方法可以有多个参数，所以你可以给方法传入你想传入的信息。

`目标-方法模式`:目标-方法模式是由`UIControl`基于类提供的。当控件的状态发生改变时，目标会由行为通知，这个行为是由`UIControlEvents`枚举值描述的。你可以提供多个目标去控制行为，而且你可以自定义事件(参考`UIControlEventApplicationReserved`)，自定义事件限制最多只有4个。控件方法并没有通过事件发送任何信息的能力。因此，当事件触发的时候，它们可以被用来传递额外信息。

两种模式之间的关键差异在于:

* 多点传输——目标-方法模式是多点传输改变的通知，而代理模式是绑定到一个指定的代理实例。
* 灵活性——在代理模式中你自定义协议，意味着你可以准确控制你需要传递多少信息。当事件触发的时候，目标-方法模式没有提供传递额外信息的方法。

你的滑杆并没有一个表示状态改变或交互的大的数字，所以你需要提供一个这样的通知。真正会改变的是控件的较大值和较小值。

这种情况下，目标-方法模式完美适合。这就是教程开头为什么要求你继承自`UIControl`的原因。

现在说得过去了。😀

滑杆的值在`continueTrackingWithTouch:withEvent:`中更新，所以你需要在里面添加通知代码。

打开`RangeSlider.swift`，找到`continueTrackingWithTouch`方法，在`return ture`之前添加如下代码:

`sendActionsForControlEvents(.ValueChanged)`

上面就是通知所有订阅(监听)目标的值改变了你所需要做的。

既然你已经在恰当的地方处理通知，你应该把它加到你的程序中。

打开`ViewController.swift`，在`viewDidLoad:`的最后添加如下代码:

`rangeSlider.addTarget(self, action:"rangeSliderValueChanged:", forControlEvents:.ValueChanged)`

上面代码每次控件发送`UIControlEventValueChanged`通知时就调用`rangeSliderValueChanged`方法。

现在在`ViewController.swift`中添加以下方法:

```
func rangeSliderValueChanged(rangeSlider:RangeSlider){
	println("Range slider value changed:(\(rangeSlider.lowerValue) \ (rangeSlider.upperValue))")
}
```

这个方法只是打印控件的值到控制台，证明你的控件按设想的发送通知。

编译并执行你的程序，来回拖拽滑块。你应该看到控件的值打印到了控制台，像下面这样:

```
Range slider value changed: (0.117670682730924 0.390361445783134)
Range slider value changed: (0.117670682730924 0.38835341365462)
Range slider value changed: (0.117670682730924 0.382329317269078)
Range slider value changed: (0.117670682730924 0.380321285140564)
Range slider value changed: (0.119678714859438 0.380321285140564)
Range slider value changed: (0.121686746987952 0.380321285140564)
```

你现在可能对看到多彩的控件感到恶心。看起来有点像疯狂的水果沙拉。

是时候更新控件的外观了。

**使用Core Graphics修改控件**

首先，你需要随着滑块的移动更新图形的“轨道”。

像之前一样，添加另一个`CALayer`的子类到你的工程中，这次叫它`RangeSliderTrackLayer`。

打开新创建的`RangeSliderTrackLayer.swift`文件，使用下面的内容替换它:

```
#import UIKit
#import QuartzCore

class RangeSliderTrackLayer:CALayer{
	weak var rangeSlider:RangeSlider?
}
```

上面的代码添加了一个滑杆的反向引用，像之前的滑块层一样。

打开`RangeSlider.swift`，定位到`trackLayer`属性，修改它成为一个新的类的实例，像这样:

`let trackLayer = RangeSliderTrackLayer()`

现在，找到`init`方法，用下面的内容替换:

```
init(frame:CGRect){
	super.init(frame)
	
	trackLayer.rangeSlider = self
	trackLayer.contentsScale = UIScreen.mainScreen().scale
	layer.addSublayer(trackLayer)
	
	lowerThumbLayer.rangeSlider = self
	lowerThumbLayer.contentScale = UIScreen.mainScreen().scale
	layer.addSublayer(lowerThumbLayer)
	
	upperThumbLayer.rangeSlider = self
	upperThumbLayer.contentScale = UIScreen.mainScreen().scale
	layer.addSublayer(upperThumbLayer)
}
```

上面的代码确保新添加的层有一个滑杆——并且那令人厌恶的背景色不会被应用。设置`ContentScale`参数匹配设备的屏幕将保证在视网膜屏幕上的清晰显示。

还有一步——移除控件的红色背景。

打开`ViewController.swift`，定位到下面这一行并把它删掉:

`rangeSlider.backgroundColor = UIColor.redColor()`

编译并执行…现在，你看到了什么？

![](https://cdn1.raywenderlich.com/wp-content/uploads/2013/05/Screenshot-3-170x320.png)

是不是什么都看不到？那就对了。

对了？这有什么对的？所以的努力——都白费了？！？！

别着急——你只是移除了我们应用到轨道层花哨的颜色。你的控件仍然还在——但是你现在只有一个空白的画布去装饰你的控件了。

因为大多数开发者在编程的时候喜欢它，当控件可以被配置来为特定的程序模拟不同的界面外观，你会添加一些属性到滑杆上允许自定义控件的外观。

打开`RangeSlider.swift`添加下面属性到你之前添加的属性下方:

```
var trackTintColor = UIColor(white:0.9, alpha:1.0)
var trackHighlightTintColor = UIColor(red:0.0, green:0.45, blue:0.94, alpha:1.0)
var thumbTintColor = UIColor.whiteColor()

var curvaceousness : CGFloat = 1.0
```

多种颜色属性的目的相当简单。那`curvaceousness`呢？这是为了一点乐趣——你很快就会发现。

下一步，打开`RangeSliderTrackLayer.swift`。

这层渲染的是两个滑块之间的轨道。它现在是继承自`CALayer`,它只能渲染一种固定的颜色。

为了要渲染这个路径，你需要实现`drawInContext:`方法，并且使用Core Graphics API来实现渲染。

>注意:
要学习深入Core Graphics，强烈推荐你阅读这篇博客[Core Graphics 101 教程系列](https://www.raywenderlich.com/?p=2033)，因为Core Graphics的学习已经超出了本篇教程的范围了。

添加以下方法到`RangeSliderTrackLayer:`

```
override func drawInContext(ctx: CGContex!){
	if let slider = rangeSlider {
		// Clip
		let cornerRadius = bounds.height * slider.curvaceousness / 2.0
		let path = UIBezierPath(roundedRect: bounds, cornerRadius: cornerRadius)
		CGContextAddPath(ctx, path.CGPath)
		
		// Fill the track
		CGContextSetFillColorWithColor(ctx, slider.trackTintColor.CGColor)
		CGContextAddPath(ctx, path.CGPath)
		CGContextFillPath(ctx)
		
		// Fill the highlighted range
		CGContextSetFillColorWithColor(ctx, slider.trackHighlightTintColor.CGColor)
		let lowerValuePosition = CGFloat(slider.positionForValue(slider.lowerValue))
		let upperValuePosition = CGFloat(slider.positionForValue(slider.upperValue))
		let rect = CGRect(x:lowerValuePosition, y:0.0, width:upperValuePosition - lowerValuePosition, height: bounds.height)
	}
	CGContextFillRect(ctx, rect)
}
```

一旦轨道形状固定，背景就被填充了。之后，高亮的范围被填充了。

编译并运行，查看新的轨道层渲染，相当漂亮！它看起来应该像这样:

![](https://cdn4.raywenderlich.com/wp-content/uploads/2013/05/Screenshot-4-170x320.png)

改变暴露的属性值，观察它们是如何影响控件的渲染的。

如果你还在想知道`curvaceousness`是干什么的，尝试改变它看看！

接着，使用相似的方法绘制滑块层。

打开`RangeSliderThumbLayer.swift`，在声明属性的下方添加如下方法:

```
override func drawInContex(ctx: CGContext!) {
	if let slider = rangeSlider {
		let thumbFrame = bounds.rectByInsetting(dx: 2.0, dy: 2.0)
		let cornerRadius = thumbFrame.height * slider.curvaceousness / 2.0
		let thumbPath = UIBezierPath(roundRect: thumbFrame, cornerRadius: cornerRadius)
		
		//Fill - with a subtle shadow
		let shadowColor = UIColor.grayColor()
		CGContextSetShadowWithColor(ctx, CGSize(width: 0.0, height: 1.0), 1.0, shadowColor.CGColor)
		CGContextSetFillColorWithColor(ctx, slider.thumbTintColor.CGColor)
		CGContextAddPath(ctx, thumbPath.CGPath)
		CGContextFillPath(ctx)
		
		// outline
		CGContextSetStrokeColorWithColo(ctx, shadowColor.CGColor)
		CGContextSetLineWidth(ctx, 0.5)
		CGContextAddPath(ctx, thumbPath.CGPath)
		CGContextStrokePath(ctx)
		
		if highlighted {
			CGContextSetFillColorWithColor(ctx, UIColor(white: 0.0, alpha: 0.1).CGColor)
			CGContextAddPath(ctx, thumbPath.CGPath)
			CGContextFillPath(ctx)
		}
	}
}
```

一旦滑块形状的路径被定义，形状就填充了。注意阴影，它给人以浮动在轨道上方的感觉。然后渲染的是边框。最后，如果滑块是高亮状态——是的，如果它被滑动了——就变成了灰白色。

在编译运行之前，有一件事需要完成。修改`highlighted`属性的定义，像这样:

```
var highlighted: Bol = false {
	didSet {
		setNeedsDisplay()
	}
}
```

定义了一个属性观察者，这样，每次高亮属性改变的时候，这层会被重新绘制。

再一次编译并执行；它应该看起来像下面这样好看:

![](https://cdn3.raywenderlich.com/wp-content/uploads/2013/05/Screenshot-5-170x320.png)

你可以清楚地看到，使用Core Graphics来渲染控件的额外努力是值得的。使用Core Graphics的结果比使用仅仅图片渲染的控件更多用途。

**处理控件属性的改变**

那还剩下什么？控件现在看起来相当时髦，视觉样式很多样，而且它支持目标-行为通知。

看起来好像已经完成了——真的吗？

想一下，如果控件在渲染之后修改了它的某个属性的值。例如:你可能想要修改滑杆的预设范围，或者修改高亮的轨道表示合法的范围。

当前没有任何观察者监听设置方法。你需要将那些功能添加到你的控件中。你需要实现属性观察者更新重绘控件的位置、大小。打开`RangeSlider.swift`像下面这样修改属性声明:

```
var minimumValue:Double = 0.0{
	didSet {
		updateLayerFrames()
	}
}

var maximumValue:Double = 1.0{
	didSet {
		updateLayerFrames()
	}
}

var lowerValue:Double = 0.2{
	didSet {
		updateLayerFrames()
	}
}

var upperValue:Double = 0.8{
	didSet {
		updateLayerFrames()
	}
}

var trackTintColor:UIColor = UIColor(white: 0.9, alpha: 1.0){
	didSet {
 		trackLayer.setNeedsDisplay()
	}
}

var trackHighlightTintColor:UIColor = UIColor(red: 0.0, green:0.45, blue: 0.94, alpha:1.0){
	didSet {
 		trackLayer.setNeedsDisplay()
	}
}

var thumbTintColor:UIColor = UIColor.whiteColor(){
	didSet {
		lowerThumbLayer.setNeedsDisplay()
 		upperThumbLayer.setNeedsDisplay()
	}
}

var curvaceousness:CGFloat = 1.0{
	didSet {
		trackLayer.setNeedsDisplay()
 		lowerThumbLayer.setNeedsDisplay()
 		upperThumbLayer.setNeedsDisplay()
	}
}
```

基本上，那些各个层依赖的属性发生了改变，你就需要调用`setNeedsDsiplay`方法。在影响控件布局属性发生改变的时候，就需要调用`setLayerFrames`方法。

现在，找到`updateLayerFrames`方法，在首行添加下面方法:

```
CATransaction.begin()
CATransaction.setDisableActions(true)
```

在方法的最后添加下面方法:

`CATransaction.commit()`

这个代码将整个大小、位置的更新包括到一个处理片断中，从而使重新流动更流畅。它还禁止了层上的冲突动画，像我们之前做的一样，这样层的大小、位置可以立即更新。

因为现在每次较大值和较小值改变的时候，是自动更新大小、位置，所以，找到`continueTrackingWithTouch`方法，把下面的内容删掉:

```
// 3.Update the UI
CATransaction.begin()
CATransaction.setDisableActions(true)
updateLayerFrames()
CATransaction.commit()
```

为了确保滑杆对属性改变做出正确的反应，以上就是你需要做的全部内容。

然后，现在你需要写一点代码，来测试你新的宏指令并且保证所有都已经正确设置且能正常工作。

打开`ViewController.swift`在`viewDidLoad`中添加下面的代码:

```
let time = dispatch_time(DISPATCH_TIME_NOW, Int64(NSEC_PER_SEC))
dispatch_after(time, dispatch_get_main_queue()) {
	self.rangeSlider.trackHighlightTintColor = UIColor.redColor()
	self.rangeSlider.curvaceousness = 0.0
}
```

上面的代码会在一暂停1s后更新控件的某些属性。把轨道的高亮颜色设置为红色，控件和滑块的形状都修改了。

编译并且运行你的工程，1秒之后，你应该看到你的控件由这样:

![](https://cdn5.raywenderlich.com/wp-content/uploads/2013/03/BlueSlider-480x94.png)

变成这样:

![](https://cdn3.raywenderlich.com/wp-content/uploads/2013/03/RedSlider-480x82.png)

是不是很简单？

你刚刚添加到视图控制器的代码说明了最有趣的一点，而且是开发自定义控件常常被疏忽的点——测试。当你在编写一个自定义控件的时候，你就责任去测试控件的所有属性并通过视觉来判断结果。一个达到这种目的的好的途径是创建一个可见的测试，用不同的按钮和滑杆来测试，每一个控件与自定义控件的不同属性相关联。这样就可以实时调整自定义控件的属性了——也能实时的看到结果。

**接下来该干什么了？**

你的范围滑杆已经功能其全了，也可以在你自己的工程中使用了！你可以在这里下载整个工程的代码.[点击下载](http://www.raywenderlich.com/wp-content/uploads/2014/08/CustomSliderExample-Swift-7.zip)

然而，创建普通的自定义控件最关键的好处是，你可以在整个工程中分享它——也可以分享给其他开发者。

你的控件准备好时机了吗？

并没有。在分享你的自定义控件之前，请考虑以下几点:

* 文档——每个开发者最喜欢的工作！尽管你可能认为你的代码是完美的作品，自带文档，而且其他开发都都不会怀疑反对的。但是，一个好的实践是提供一个公共的API文档，最起码为了分享代码。这意味着记录所有公共类和属性。

例如：对于`RangeSlider`需要一个文档来解释它是什么——一个由四个属性`minimumValue, maximumValue, lowerValue`和`upperValue`的滑杆——它是干什么用的——允许用户可视化确定数值范围。

* 健壮性——如果你设置`upperValue`的值大于`maximumValue`会怎么样？当然，你自己肯定不会这么做——那多傻啊，不是吗？但是最终你能保证别人不会吗？你需要确保控件状态一直保持合法性——除非某个傻子尝试那样做。
* API设计——前面一点指出了关于健壮性，这一点关于更广泛的话题——API设计。创建一个灵活的、直观的健壮的API，将能保证你的控件能被广泛使用，并且广泛传播。

API设计是一个深度话题，已经超出了本篇教程的范围。如果你感兴趣，推荐查看Matt Gemmell的[25 Rules of API Design](http://mattgemmell.com/2012/05/24/api-design/)

可以分享你的控件的地方有很多，这里只是一些建议:

* [GitHUb](https://github.com/)——GitHub已经成为了分享开源项目最流行的地方之一。上面已经有了大量iOS自定义控件。GitHub不错的地方在于允许用户轻松访问你的代码，其他人可以通过fork你的代码潜在地与你合作，或者在你已有的控件上提出建议。
* [CocoaPods](http://cocoapods.org/)——允许用户轻松地添加你的控件到他们的项目中，你可以通过CocoaPods分享你的控件，它是一个针对iOS和OSX项目的依赖库管理器。
* [Cocoa Controls](http://www.cocoacontrols.com/)——这个网站提供包括商业项目和开源项目的路径。许多开源项目控件由GitHub拥有，Cocoa Control封闭，是一个推广你的控件的好方法。

希望你从编写这个分段滑杆控件中感到愉快，或许已经激发你想创建你自己控件了。如果是这样，请在评论区中分享——我们很期望能看到你的作品。

---

写在后面：

由于译者水平有限，翻译不足之处，请指正。

如需转载，请注明出处。
	
**关于译者:**

微博:[Mr_龙0615](http://weibo.com/409498119)

GitHub:[Kito0615](https://github.com/Kito0615/)