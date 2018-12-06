## 基本布局

在本节内容，我们将了解如何在Canvas上放置UI元素，以及UI元素之间的关系。我们也可以在Unity 编辑器中测试这些功能，如使用 **GameObject -> UI -> Image** 。

![](http://cdn.zergzerg.cn/2018-12-06ui_base.png)

#### 矩形工具

每一个UI元素为了布局方面考虑，都表示为是一个矩形，这个矩形可以通过 **Scene View** 中 **toolbar** 的矩形工具来操作。这个工具可以用于处理 Unity 2D 对象，以及UI元素或者3D 模型。

这个矩形工具能用来控制UI元素的移动，重置大小或者旋转。包括**hand tool、 move tool、 rotate tool、 scale tool、 rect tool和 move-rotate-scale tool**。 前面三个工具的使用基本都很熟悉了，这里的rerect tool（矩形工具）可以用于矩形的移动、重置大小、旋转。点击矩形内部，然后拖拽即可移动，通过边缘拖拽改变UI元素的大小，通过将鼠标放置在略远离顶点处，鼠标会出现一个旋转标记，可以点击拖拽使其旋转。

当使用矩形工具的时候，一般使用当前pivot和local模式。（上图设置的是center模式，具体区别慢慢看吧）

![](http://cdn.zergzerg.cn/2018-12-06ui_transform_full.png)

#### Rect Transform

**Rect Transform** 是在UI元素中的一种用于替换常规的transform元素的新的transform元素。Rect Transform包含有position, rotation, scale这些transfrom已有的元素，另外还有width， height元素用于定义其二维大小。

##### rect tool重置大小

当使用rect tool重置2d sprite或者3d object时，会改变对象的local scale和position，但是当作用于有rect transform的元素时，只会改变当前元素的width，height，保持scale不变，position可能会发生改变(由pivot决定)。这样的重置大小不会影响字体大小，边框等。

##### Pivot(中心点)

当pivot设置为pivot（反之为center），UI对象的移动、重置大小、比例缩放会随着pivot的值不同，展示的修改后结果不同，pivot设置了之后，可以在界面修改pivot具体数值。

##### Anchor（锚点）

Rect Transform包含有一个锚点的布局概念，锚点anchor在编辑器中显示为一个四个小三角形聚集在一起。

如果一个rect transform的父对象也是一个rect transform，那么子对象的位置就能锚定在父对象的某一个位置，如锚定在中心点，或者父对象某一个顶点处。

![](http://cdn.zergzerg.cn/UI_Anchored1.gif)

![](http://cdn.zergzerg.cn/UI_Anchored2.gif)

如上面两图，一个锚点在父对象的中心，一个锚点在父对象的右下顶点，这样在父对象发生改变时，子对象相对于锚点的位置是不变的。

锚点的位置是定义为浮点数的百分数，0.00为最左边，0.50为中间，1.00为最右边。锚点可以设置在父对象的任何位置。每个锚点锁定UI元素矩形的一个顶点。通过点击一个pivot小三角形，可以调整它的位置。如果选择按住shift，那么这个元素也会相应的重置位置。

可以通过使用presets使用编辑器自带的pivot设置，这些基本会是最常用的。

![](http://cdn.zergzerg.cn/2018-12-06ui_pivot.png)

如果选定的是anchor presets里面的一种，那么在transform里面就会展示对应的图标，否则，显示custom图标。

##### Anchor和position

在Anchors设置中，min的xy点坐标对应矩形的左下角的锚点，max对应右上角的锚点坐标。

如果这两个值是相同的，那么UI元素会严格锚定在一个固定的点。

如果在修改anchors时候，按下右边的R按钮，那么会固定position，导致修改pivot时候会充值元素大小。