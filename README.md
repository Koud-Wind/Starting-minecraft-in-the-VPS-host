# Starting-minecraft-in-the-VPS-host
适用于有特殊用途且没有GPU渲染功能的主机, 不过它对于大部分人都没有用


主要使用"llvmpipe-loader"并利用CPU进行渲染

首先从这里下载得到"llvmpipe-loader-1.0.jar", 将它放到某个路径中, 并确保不要再移动它.

然后需要添加一个环境变量"_JAVA_OPTIONS", 它的作用是会为每个jvm虚拟机添加特定的启动参数, 内容为"-javaagent:路径\\llvmpipe-loader-1.0.jar=llvmpipe", 记得每个\后需要再加一个\

例如:"-javaagent:C:\\myApp\\llvmpipe-loader-1.0.jar=llvmpipe".

我推荐你编写两个bat来方便对这个环境变量进行修改

setx _JAVA_OPTIONS -javaagent:路径\\llvmpipe-loader-1.0.jar=llvmpipe /m

用于添加这个环境变量

REG delete "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /F /V _JAVA_OPTIONS

用于删除这个环境变量


这里值得注意的是任何应用/进程运行时是会读取这一时刻的环境变量, 当你运行某个进程后再去修改环境变量的话, 进程缓存的环境变量不会改变, 想要应用改变后的环境变量就需要重启那个进程.


当你添加好这个环境变量时, 记得关闭你要启动minecraft的父进程(例如minecraft启动器), 等待一分钟左右, 再启动父进程, 这时你就可以启动minecraft了!!(若未成功那么就重启主机)


以下是适用于在主机进行网易局域网对接减少占用资源的操作

进入网易启动器设置, 尽可能少分配运行内存(最低512MB), 编写一个或者更改你的用来删除网易模组的bat, 用于删除客户端启动时所加载的模组,
只保留模组"4620273834451558259@3@0.jar"(Network网易前置模组), "4657086570888223593@3@38.jar"(Operator1.13+网易对接用模组)以及你在"V_版本"中加入的对接模组(若是1.13+以上版本则保留名称末尾为@0的模组),

![image](https://github.com/Koud-Wind/Starting-minecraft-in-the-VPS-host/assets/123817318/5c1fdd7f-ed55-413f-9dee-403d35d13cce)

保留上述模组并删除占用多余性能的模组后, 就可以开始启动房间了


在你启动服务端之前, 运行ProcessHacker.exe(如果你的资源够用可以先启动服务端)
选择到网易启动的javaw.exe进程并右键, 点击"亲和性", 只选用任意一个CPU(默认全选), 点击确定, 这样能减少客户端占用的CPU核心.

![image](https://github.com/Koud-Wind/Starting-minecraft-in-the-VPS-host/assets/123817318/647b237f-14a6-4a68-b32c-a50460fdfb9b)


右键进程并将鼠标浮到"优先级", 选择"空闲"或"低于正常".

![image](https://github.com/Koud-Wind/Starting-minecraft-in-the-VPS-host/assets/123817318/ee03a590-5780-4bf2-b95f-cc22b86cf0c9)

右键进程并将鼠标浮到"I/O优先级", 选择"非常低", 最小化客户端窗口.

![image](https://github.com/Koud-Wind/Starting-minecraft-in-the-VPS-host/assets/123817318/54dc2ca7-fd27-4c62-b206-393d5d2172c1)

等待一会之后, javaw.exe的占用会减少很多(有时会占满1个CPU核心).

注意: 不要长时间暂停javaw.exe进程, 尽管已进入的玩家能够正常游戏, 但新玩家会无法进入.












