## Visual Components(可见组件)

在使用UI系统的过程中，新的组件会不断的出现，用于帮助构建特定的GUI功能，本节将讲述这些基本的组件。

#### Text

![](http://cdn.zergzerg.cn/2018-12-06ui_text.png)

Text组件，或者成为Label（标签），是有一个文本区域，用于输入、展示文本，可以设置文本的字体、字体风格、字体大小和是否使用富文本功能。

可以通过选项设置文本的对齐方式，设置水平和竖直方向溢出的处理方式，用于处理文本超过text元素范围的处理方式。还有一个best fit用于在固定空间动态调整文本大小以适配空间。

#### Image:

![](http://cdn.zergzerg.cn/2018-12-07ui_image.png)

如上图，是image组件的inspector界面。image包含的image type类型为：

* Simple：普通类型，直接原尺寸放入
* Sliced：将图片分为3x3等分，四角的图像保持不变，其余部分适配整体长宽比做拉伸。
* Tiled：类似Sliced，但是中心部分不是拉伸，而是使用重复，如果图片sprite没有border边界，那么整个图片会重复填充整个rect transform
* Filed：可以控制图片的显示方式，显示方向，和显示总量比。

unity的image组件接受sprite(2D/UI)类型的texture type, unity editor提供一个图片编辑器，用于确定图片三等分各自的比例，如下图，通过调整上下左右边界的值，确定中间值和四周值

![](http://cdn.zergzerg.cn/2018-12-11ui_image.png)

#### Raw Image

image组件使用sprite，而raw image使用材质，不需要边界，一般情况下，除非特定情况下，使用raw image，否则一般使用image。

#### mask

mask不是一个可见的UI组件，它主要是用于控制其子元素的显示，在添加了mask组件的元素下，子元素的可见范围不可以超过父元素。mask组件需要配合image组件使用。

#### Effects

unity提供一些制作特效的组件，比如说阴影（shadow），轮廓（outline）。使用这个，需要元素同时包含image或者text组件。