## Interaction Components(可交互组件)

本节主要讲 UI 系统中控制交互的组件，包括鼠标、触屏事件，以及使用键盘、控制器等的交互。

#### Common Functionality

大多数交互组件有一些共性，他们能够被选中，也就可以有一些内置的可视化状态转变（普通、高亮、按压、失效），以及使用键盘、控制器导航到其他可选中的组件。

这些交互组件至少有一个事件，用于当用户与这个组件交互时产生特定的消息事件。UI系统会捕获、记录所有传播异常的事件。

#### Button

一个button有一个OnClick事件，用于定义它被点击时候的处理。

#### Toggle

一个toggle有一个**Is On** 选择框，用于触发这个toggle是开启还是关闭。它绑定了一个**OnValueChanged** 事件，用于触发值改变的情况。

#### Toggle Group

一个toggle group用于设置一组toggle，使其只能选中一个，选中一个会自动的取消选中其他所有的。

#### Slider

一个Slider是一个滑动条，通过设置Value值，调整滑动条的滑动量，滑动条的方向和里面滑动方向都可以设置，他也有一个OnValueChanged的事件。