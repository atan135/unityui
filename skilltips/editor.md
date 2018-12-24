## Editor写插件的一些技巧

#### 一. MenuItem

**1. 常规使用：**

```c#
[MenuItem("MyMenu/Do Something")]
static void DoSomething()
{
    Debug.Log("Doing Something...");
}
```

产生一个按钮，如果MyMenu替换为Assets，那么会在Project窗口点击对象右键也会产生这个选项。如果替换为GameObject，则会在Hierarchy下的create中，以及选中对象中都生成对应的选项。

Do Something可以使用一个热键，规则如下

1. 使用%代替ctrl，#代替shift，&代替alt
2. 常规使用 `Do Something &g` ， 如果只是单一键，使用`Do Something _g` 这样方式
3. 支持一些特殊键，如LEFT, RIGHT, UP, DOWN, F1, HOME, END, PGUP, PGDN

**2. 选项是否激活**

```c#
[MenuItem("MyMenu/Log Selected Transform Name")]
static void LogSelectedTransformName()
{
    Debug.Log("Selected Transform is on " + Selection.activeTransform.gameObject.name + ".");
}
[MenuItem("MyMenu/Log Selected Transform Name", true)]
static void ValidateLogSelectedTransformName()
{
    return Selection.activeTransform != null;
}
```

使用这样的方式，确定该选项是否当前处于激活状态。自己通过代码写出激活逻辑。

**3. Inspector界面的component组件界面添加右键选项**

```c#
[MenuItem("CONTEXT/Rigidbody/Double Mass")]
static void DoubleMass(MenuCommand command)
{
    Rigidbody rb = (Rigidbody)command.context;
    body.mass = body.mass * 2;
    Debug.Log("Rigidbody mass has multiple to " + body.mass + " from script");
}
```

此时，在GameObject的rigidbody组件右键，可以看到**Double Mass** 选项。选择后，会把组件的mass属性乘2.

**4. 生成一个GameObject**

```c#
[MenuItem("GameObject/MyCategory/Custom GameObject")]
static void CreateCustomGameObject(MenuCommand menuCommand)
{
    GameObject go = new GameObject("Custom GameObject");
    GameObjectUtility.SetParentAndAlign(go, menuCommand.context as GameObject);
    Undo.RegisterCreatedObjectUndo(go, "Create " + go.name);
    Selection.activeObject = go;
}
```

这里，**SetParentAndAlign** 可以将对象生成为选定对象的子对象，**RegisterCreatedObjectUndo** 注册这个新创建对象的记录，可以在之后使用ctrl+z撤回，**Selection.activeObject** 使当前选中的为新对象。