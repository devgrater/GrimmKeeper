## 目前已经可以用的
**跳到@开头的对应tag上**

```/jumpto [tag]```

**修改变量的值**

```/setflag [key] [value]```

例如：```/setflag smartphone_1 1```
会把名叫smartphone_1的变量设置为1。

**调用项目里的函数**

```/call [function name]```

函数的内容目前还是需要我们负责。写的时候写个placeholder名字就行，到时候我们在代码这边接上

**等待条件满足**

```/await [condition]```

条件满足后运行下一行。

例如：```/await smartphone_1 == 1```。等```smartphone_1```的数值变为1时，停止等待，运行下一行的内容。

其他的运算符号包括```> >= == <= < != 以及 "= (用于比较两个字符串变量)```

**条件分支**

```[[condition]](when success)(when failure)```

condition可以像上面一样，写比较句，例如

```[smartphone_1 == 1](/jumpto success)(/jumpto failure)```

也可以当做switch来使用，例如

```[#choice](/jumpto choice0)(/jumpto choice1)(/jumpto choice2)```

此时，会根据#choice的值决定运行哪一段内容。```#choice```是保留变量，用来保存玩家上一次做出选择时的选项。选择第一个选项即为0，第二个为1，以此类推。

有多个条件，但是分支数量不足时，例如```[#choice](/jumpto choice0)(/jumpto choice1)```但#choice为2，或```[smartphone_1 == 1](/jumpto success)```得出结果为false，此时会默认执行下一行内容。

**给玩家提供选项**

```?(Choice 1)(Choice 2)(Choice 3)....```

会在屏幕上显示多个选项，选项内容为括号里面的内容。

例如```?(Yes)(No)```

玩家做出的选择会被保存在```#choice```这个保留关键字里。第一个选项为0，第二个为1，以此类推。

一个常用的办法是将选项和分支结合

```
?(Yes)(No)
[#choice](/jumpto yes)(/jumpto no)
```


**调整对话窗口的显示**

```/showui [true/false]```

**载入新文件**

```/load [file]```


载入指定位置的剧本，剧本的名称不需要包括扩展名，用相对于```/Resource/```的路径即可
例如：```/load 2_get_to_meowwer```会载入```Resource```文件夹下的```2_get_to_meowwer.txt```

**禁止玩家关闭手机**

```/alwaysshowphone [true/false]```

设置为```true```时，玩家不可关闭手机。设置后需要手动设置回```false```

**存档/读档**

```/savegame /loadgame```

```/savegame```会将当前的状态保存下来，```/loadgame```会载入最后一次保存的存档。

由于可能形成死循环，尽量将```loadgame```作为选择分支后的动作，只有玩家确认了才能载入。

## 你不一定知道的

**修改角色表情**

```alice,happy: lorem ipsum```

在角色名称后面加上逗号和表情，可以改变角色表情。
当然，前提是有角色和相关表情的数据存在。

**终止对话**

在文件末尾加上一个```@End```的标签
然后在想要强制终止的地方直接```/jumpto End```即可


执行之后，不管剩下什么内容，一律不会执行。
可能会用到的地方：

```
[#choice](/jumpto choice0)(/jumpto choice1)
@choice0
Alice: you have landed in choice 0
/jumpto @End
@choice1
Alice: you have landed in choice 1
/jumpto @End
```

跳到其中一个分支，Alice说话之后终止。

**玩家在看哪一个APP？**

```
#phone_app_opened -> 可能的值："meowwer", "meowgle", "homescreen"
#phone_view_opened -> 可能的值：依app决定
```

## 还没做的

可以提前写在脚本里，不会影响运行。
你用到了我就开始做相关的功能

**屏幕抖动**

```/shake [magnitude] [frequency]```

**淡入淡出**

```/fade [in/out] [time] [color]```

用指定的颜色淡入淡出。```time```单位为秒。```color```为16进制颜色，不写默认为黑色

**随机变量**

```#random```

暂定每一帧更新一次，变量为```Mathf.Random()```的值（0~1之间）
