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
* Filed：