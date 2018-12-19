## 富文本表现

使用标记语言，允许使用嵌套形式，例如

We are <b\>absolutely <i\>definitely not </i\></b\>

展示为：

We are <b>absolutely <i>definitely not</i></b>

### Unity支持的标记Tag

| Tag       | 描述                           | 用例                                        |
| --------- | ------------------------------ | ------------------------------------------- |
| **b**     | 粗体                           |                                             |
| **i**     | 斜体                           |                                             |
| **size**  | 字体大小设置                   | We are <size=50\>largely</size\> unaffected |
| **color** | 设置字体颜色，格式为##rrggbbaa | <color=#00ffffff\>.....</color\>            |

#### Editor GUI

在editor Gui系统中，富文本显示是默认disabled，通过显示设置该属性为true可以使用富文本，如

```c#
GUIStyle style = new GUIStyle();
style.righText = true;
GUILayout.Label("<size=30>Some <color=yellow> Rich</color> Text</size>", style);
```

