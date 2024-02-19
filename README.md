# Starting-minecraft-in-the-VPS-host
适用于有特殊用途且没有GPU渲染功能的主机, 不过它对于大部分人都没有用

<br>
<br>

## 主要使用"llvmpipe-loader"并利用CPU进行渲染

- 首先从这里下载得到"llvmpipe-loader-1.0.jar", 将它放到某个路径中, 并确保不要再移动它.

- 然后需要添加一个环境变量"_JAVA_OPTIONS", 它的作用是会为每个jvm虚拟机添加特定的启动参数, 内容为`-javaagent:路径\\llvmpipe-loader-1.0.jar=llvmpipe`, 记得每个`\`后需要再加一个`\`
( 例如:`-javaagent:C:\\myApp\\llvmpipe-loader-1.0.jar=llvmpipe` ).

> 我推荐你编写两个bat来方便对这个环境变量进行修改

> `setx _JAVA_OPTIONS -javaagent:路径\\llvmpipe-loader-1.0.jar=llvmpipe /m` 用于添加这个环境变量

> `setx _JAVA_OPTIONS "" /m` 用于删除这个环境变量

<br>

**这里值得注意的是任何应用/进程运行时是会读取这一时刻的环境变量, 当你运行某个进程后再去修改环境变量的话, 进程缓存的环境变量不会改变, 想要应用改变后的环境变量就需要重启那个进程.**


当你添加好这个环境变量时, 记得关闭你要启动minecraft的父进程(例如minecraft启动器), 等待一分钟左右, 再启动父进程, 这时你就可以启动minecraft了!!(若未成功那么就重启主机)

<br>
<br>





