## Auto Layout

RectTransform的布局方式能够适用于大部分的场景，但是，仍然有一些情况下我们需要使用自动布局方式来生成一些页面结构。

Unity UI系统提供了一种方式生成自动扩展布局元素，如水平列表、垂直列表、表格等。也提供了一些方式使得元素的尺寸大小使用内容适配。例如，一个按钮的大小被自动的适配到按钮文本的长度。

### 理解布局元素

自动布局系统是建立在一系列的布局元素和布局控制器上的，一个布局元素是一个包含有RectTransform的GameObject，布局元素知道自己的尺寸大小，但是他们不会直接设置自己的尺寸，而是其他布局控制器组件计算出有gi嗯合理的尺寸大小供使用。

一个布局元素有6个属性：

* Minimum width：最小宽度
* Minimun height：最小高度
* Prefered width：推荐宽度
* Prefered height：推荐高度
* Flexible width：可伸缩宽度
* Flexible height：可伸缩高度

布局元素的这些属性值会被其他控制元素，如**Content Size Filter** 和 列表类组件Group使用。这些属性的使用原则如下：

* 至少会占用Minimum width/height的尺寸大小空间
* 如果有足够的空间使用，Prefered width/height会被使用
* 如果存在多余的额外空间，Flexible width/height会被使用

任一包含RectTransform组件的GameObject，都会有个初始默认的minimum，prefered，flexible size，为零。某些组件附加到GameObject上会修改这些布局元素属性。

**Image** 和 **Text** 是两种这样的组件，他们会将布局元素的Prefered widt/height修改为适配sprite和text的尺寸。

#### 布局元素组件（Layout Element Component)

如果需要复写GameObject的布局元素属性，可以添加Layout Element Component，如下图。

![](http://cdn.zergzerg.cn/2018-12-19layout.png)

### 理解布局元素控制器

布局控制器是一些控制尺寸以及某些布局元素的位置，比如包含RectTransform的GameObject。一个布局控制器能够控制自身的布局，或者控制子元素的布局。

#### Content Size Fitter

Content Size Fitter是一类布局控制器，用于控制资深的布局、尺寸。

#### Aspect Ratio Fitter

这类布局元素用于使元素长宽适配，或者适配父元素。

#### Layout Groups

这类布局控制器不会直接控制自身的尺寸大小，而是可以被子元素控制自身布局。

### 自动布局技术细节

自动布局使用了一些内置的组件，但是也可以通过创建一些自定义组件控制布局，只需要组件实现了一些特定的接口。

#### Layout Interfaces

 一个组件实现了**ILayoutElement** 接口就被自动布局系统看作是一个布局元素。

一个组件实现了**ILayoutGroup** 接口就被看作能具有控制子元素布局的功能。

一个组件实现了**ILayoutSelfController** 接口被看作具有控制自己RectTransform属性的功能。

#### Layout Calculations

自动布局系统计算、执行布局按照如下顺序：

1. 布局元素的minimum,prefered, flexible width通过是爱心了ILayoutElement接口组件的CalculateLayoutInputHorizontal方法计算，这个过程是自底向上进行的，所以父元素能够根据子元素自动调整自己的宽度。
2. 布局元素的有效宽度通过实现了ILayoutController接口的SetLayoutHorizontal方法计算，这个过程是自顶向下的，先生成父元素的宽度，然后是子元素，这样，元素的RectTransform属性值被重新计算出来。
3. 高度类似1
4. 有效高度类似2

由上可知，自动布局系统首先计算width，然后是height，所以height可以根据width计算，但是反之不行。

#### Triggering Layout Rebuild

如果一个组件的属性改变导致了当前的布局不再适合，就需要重新布局，这个能通过下面代码触发

```c#
LayoutRebuilder.MarkLayoutForRebuild (transform as RectTransform);
```

布局重建不会在调用后立即发生，而是在游戏当前帧末尾图形渲染前产生，愿意是布局重建可能会在一帧内发生多次，每次都重新绘制渲染会影响性能。

下面是应该触发布局重建的一些场景：

* 修改会改动布局的一些属性值
* OnEnable
* OnDisable
* OnRectTransformDimensionsChange
* OnValidate
* OnDidApplyAnimationProperties 