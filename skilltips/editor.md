## Editor写插件的一些技巧

> 使用MenuItem生成菜单栏选项，其中，如果path第一项为Assets，则生成右键选项菜单 后面使用 % 代表Ctrl，#代表Shift，&代表Alt

```c#
[MenuItem("MyMenu/Item1")]	// 生成菜单栏菜单
[MenuItem("Assets/SomeAction")]	//生成右键选项
[MenuItem("MyMenu/Item1 &3")]	//生成菜单栏菜单，且使用快捷键 Alt+3
```

