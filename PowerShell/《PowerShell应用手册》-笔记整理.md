# 手册知识点整理 

[toc]

## 提要

----

### 打卡

* :timer_clock: 2023-1-5 09:32:11  从 今日开始 学习 这本手册，因为发现这本手册   从 实际 使用出发，学完就能使用

同时 自己 在 学完之后 ，在学习 PowerShell理论部分就更快了

* :timer_clock: 2023-1-6 11:39:01  整理 博客 
* :timer_clock: 2023-1-9 09:48:13  周一，今天开始进入  第一次学习 ，复现和理解为主，简单 摘抄 笔记的学习，尽快学会 应用手册的知识点   先 复习之前学习的，后面再学习新的 



###  学习重点 

>  不是 全盘将 手册内容 摘录 到笔记里面，而是将 每个内容 自己复现 出来
>
> 第一次 复现 ，自己的思考 ， 之后学完理论再 整理一遍   

## 博客搬运

----

 [ps第5课：常用帮助命令](http://bbs.chinaunix.net/thread-4264294-1-1.html)

```powershell

问：如何知道powershell版本？
答：
$PSVersionTable



问：如何列出本地模块？
答：
get-module -ListAvailable


问：只知道命令的一部分，如何查找命令？
答：
get-command  *service*



问：知道命令，但不知道命令中都有啥参数，如何列出参数？
答：
get-help write-host -Parameter *   # 很好用迅速查看参数，以及参数的具体使用方法
Get-Command Get-Help -Syntax	# 有一个 是语法 

show-command write-host				#配套使用，图形化完整输出命令语句
Get-Help Get-ChildItem -Parameter * | Format-List # 参数列表的详细信息
Get-Help Get-ChildItem -Parameter * | Select-Object name  # 只获得 参数列表 
Get-ChildItem | Get-Member -MemberType Property #获取 Get-ChildItem返回的对象的属性列表
先学 语法，语法包含参数， Get-Command，Get-Help 输入部分学完 ，学的是正确的输入；还要学习命令输出对象的属性和方法 ，那就是Get-Member


问：知道参数，但不知道哪个命令有此参数，如何查找命令？
答：
例子：想知道哪个命令有encoding参数，就用
get-command -ParameterName encoding  # 深层学习 cmdlet之间的关联可以使用，管道传输使用 



问：如何从命令行获取某命令帮助？
答：
get-help get-date
get-date -?   #快速查看帮助
get-help get-date  -Examples # 命令例子
get-help get-date  -online    #在线手册
Get-Command Get-Help -Syntax	# 有一个 是语法 



问：不知道命令（不知道对象）的属性方法，如何查找？
答：
"abc"  | get-member
get-date | get-member
```



## 第一章 Windows PowerShell 交互界面

----

Windows PowerShell 在设计的时候将它的高效率和强大的交互性放在首位

本章将从交互性的角度来介绍PowerShell。



### 1. 运行程序、脚本和已有的工具

****

**问题描述：**

你依赖着那些已经花费你很多精力来学习使用的工具。

在日常工作中，你可能已经有一些**可执行文件**、Perl脚本、VBScript等，或者遗留的错综复杂的用于编译的**批处理文件**。你想使用PowerShell，但又不想放弃已经有的工具。



**解决方案：**

* 在系统路径下运行程序、脚本、批处理文件或其他可执行文件，可以键入其文件名。

* 对 于可执行类型的文件，可以不用输人扩展名

```powershell
Program.exe arguments 
ScriptName.psl arguments 
BatchFile.cmd arguments 
```



==运行那些在**命令名**中**包含空格**的命令，需要用**单引号**（＇）将命令括起来，同时在前面加上符号（＆），这在PowerShell中称作调用操作（Invoke operator）==，如：

```powershell
& 'C:\Program Files\Program\Program.exe' arguments 
```

运行**当前目录下**的命令，在文件名前添加，如

```powershell
.\Program.exe arguments 
```

在当前目录下运行那些命令名中包含空格的命令，同时加上符号（＆）和.＼，如：

```powershell
&'.\Program With Spaces.exe' arguments 
```



**讨论：**

PowerShell与大多数Unixshell一样，**要求你明确地指出你要在当前目录下运行程序**。这样做，你需要使用像前面提到的.＼Program.exe这样的语法。这样做的目的是，当你访问某一目录的时候，可以有效地防止一些用户在你的硬盘上非法散布一些与你要运行的程序名称相近（或相同）的恶意程序。

许多用户将经常用到的工具和PowerShell脚本放到系统目录的“tools”目录下，这样就不用在每次运行程序的时候键入路径了。**如果PowerShell能够在系统路径下找到你键入的命令**，你可以不用刻意地输入路径。

```powershell
1.  chrome 这个应用程序，我如何获取 它的 参数列表呢？
```



### 2. （查找PowerShell命令）命令语法查询

**问题：**

运行 PowerShell命令 ，但是 需要找到 **正确的 Cmdlet命令**  和  **会使用该命令** 

**解决方案：**

```powershell
Get-Command *Language*   # 查找命令

Get-Help Get-Language  # 了解命令的详细使用方法
Get-Language-？ # 可以这样使用

若要查看示例，请键入: "get-help Get-InstalledLanguage -examples".
有关详细信息，请键入: "get-help Get-InstalledLanguage -detailed".
若要获取技术信息，请键入: "get-help Get-InstalledLanguage -full".
有关在线帮助，请键入: "get-help Get-InstalledLanguage -online"
```





**讨论**

Get-Process命令是一个内置的PowerShell命令，我们称之为**cmdlet**。它与传统命令 的区别在于，cmdlet为管理员和开发人员提供了重要的功能：

1. 采用统一的**命令语法**。

2. 支持丰富的**管道功能**（将一个命令的输出作为另外一个命令的输入）。**输出易于管理的对象**，而不是容易出错的文本。

由于Get—Process命令生成了丰富的基于对象的输出，所以你可以利用这个输出来执行一些与进程相关的任务。

Get-Process命令仅仅是PowerShell支持的命令之一。

要学习**如何查找PowerShell命 令**的技术，请参见1.4节。

要获得**如何使用.NET框架提供的类的更多信息**，请参见3.4节



### 3. 自定义Shell、配置文件 与 提示符

---

通过引用＄profile变量你可以定义你要引用的配置文件，PowerShell实际上最多支持4个配置脚本文件。关于如何使用这些配置脚本的说明（包括其他配置项），可以查阅附录A。

P48 ，略



----

### 4. 查找实现指定任务的 命令 及语法

---

**问题**

不知道 使用什么命令来执行 ，前置 可结合 1.1 运行PowerShell命令 进行查看

**解决方案**

```powershell
Get-Command  #检索命令
Get-Command CommandName # 获得指定命令的概要信息  eg:Get-Command get-help
Get-Command Set-Location | Format-List  # 输出结果重定向
Get-Command *text* # 搜索 包含text的所有命令 
Get-Command -Verb  Get  # 搜索使用Get动词 的命令 
Get-Command -Noun Service # 搜索 与 服务 Service有关的 命令 
```

**讨论**

```powershell
Get-Command *language*  # 返回CommandType类型是 别名、Cmdlet和应用 
Get-Command *language* -CommandType Application  # 单独查找 应用
Get-Command **  -CommandType Application #查找可以直接输入执行的应用 
Get-Command *chrome*  -CommandType Application # 单独输入chrome 可以启动，但是 通过这个查找不到
Get-Command *win*  -CommandType Application # 总结： 发现这些应用 是 在注册表登记的； 在注册表一定可执行，可执行，不止在注册表中
Get-Help *language* # 返回Cmdlet，HelpFile
Get-Help *language* | Select-Object -Property Category



切记：深入学习PowerShell时，最常使用的是 Get-Command、Get-Help、Get-Member 这三个命令，辅助的是 show-command 
```

### 5. 获得命令帮助

---

 略，内容 看看就行



---

### 6. 编程：搜索帮助

---

 略，了解即可

---

### 7. 在PS之外， 调用PS脚本

----

**问题：**

从批处理工具、登录脚本、定时任务 等 调用PS脚本；

略，

explorer 、psr

## 第二章 管道

---



### 简介

Shell  有基本的 概念 ： 管道 pipeline ； 

形成表格的最重要功能之一  

一组命令中， 前一个命令的输出 成为下一个命令的输入

```powershell
Get-Process | Where-Object {$_.WorkoingSet -gt 50kb} | Sort-Object -Descending Name
```

在PowerShell中，使用管道符号 {} 来划分管道中的每个命令。

在例中，Get-Process命令返回系统中存在的进程，这些进程对象包含进程的基本信息，如进程名、内存使用情况、进程的ID及其他信息。

紧接着，Where-Object命令直接对这些进程对象进行处理，简单处理那些占用内存大于500kb的进程对象，

然后将结果往后传递，Sort-Object对这些进程对象按名称进行降序排列。

这个简略的例子说明了管道的强大功能，**powerShell在管道中传递的是高保真的对象**，不仅仅是文本表述。与之形成对比的是，**所有其他Shell在管道中传递的是纯文本的数据**。它们从纯文本的输出中提取有用的信息并转换成管道中传递的信息。在cmd.exe中，以传统的基于UNIX的Shell来实现上面的例子是十分困难的，而且几乎是不可能的。

**传统的基于文本的Shell使得管道功能变得十分复杂**，因为要对在管道中的每个命令的输出格式十分清楚才行，

```cmd
ps -F | awk '{if($5 > 500) print}' | sort -r -k 64,70 # cmd版本的 不习惯使用 组号5是内存范围，awk工具 语言来过滤数据，最后 了解 进程名的列的范围 
```



### 1. 过滤列表项 或  命令输出项

----



**问题**

 过滤 一个 列表 或者  命令输出的 项 



**解决方案**



使用 Where-Object (标准别名是 where 和  ?) 从列表或命令的输出  中 来选择 你要输出的项

* 列出 所有 正在运行进程名称中包含search的进程 ，对进程名字属性使用 -like 操作符 进行比较 进程Name属性

```powershell
Get-Process | Where-Object {$_.Name -like "*Search*" } 
Get-Process | Where-Object {$_.Name -like "*Shell*" } # 运行PowerShell 后便可以查到
Get-Process | Where-Object {$_.Name -like "*NVIDIA*" }

```

*  列出 当前位置的子目录 使用PsIsContainer属性

```powershell
Get-ChildItem  | Where-Object {$_.PsIsContainer}
```

* 列出 所有已经停止的服务  ，对服务的属性 使用操作符 -eq

```powershell
Get-Service | Where-Object {$_.Status -eq "Stopped" }
```



对于输入的每一项（前一个命令的输出），Where-object会根据你定义的脚本块对输入进行估算。

**如果脚本块返回真，Where-Object会把结果输出；否则，不输出。**

在PowerShell中，一个**脚本块**是指用 {} 括起来的一系列PowerShell命令。在脚本块中可以输入任意的PowerShell命令。

在脚本块中，**＄＿变量代表当前输入的对象**。对于输入对象中的每一个项，PowerShell将它指派给＄＿变量，然后运行脚本块。

在上面的例子中，**输入的对象代表前一个命令生成的进程、文件或服务**。

如果需要，**在脚本块中可以包含大量的函数**，可以进行**组合测试、比较或其他工作**。

关从于脚本块的更多信息，参见10.3节；

关于有效的比较类型，参见附录A中的“比较操作符”。

对于**简单的过滤**，Where-Object的语法看起来有点繁琐。

在2.2节中，通过一个脚本可以使简单的过滤（如上面的例子）更容易实现。

对于**复杂的过滤**（比如，在Explorer窗口中用鼠标对文件进行操作），编写脚本块表达你的愿望是困难的，甚至是不可能的。2.3节展示了一个使手工过滤更容易完成的脚本。





### 2.编程：简化多数Where-Object 过滤

Where-Object命令是如此的强大，以至于允许你**基于任意的表达式来过滤你的输出**。

对于简单的过滤（如**只基于一个简单属性的比较操作**），语法看起来可能有些难看：Get-Process | Where-Object ($_.Handles -gt 1000)

对于这种情况，一个简单的方法是**编写一个脚本文件**（如例2-3所示），把脚本块中的表达式直接写在脚本中：

Get-Process | Compare-Property Handles gt 1000

Get-ChildItem | Compare-Property PsIsContainer 

通过简短的**别名**，可以**简化书写**：

PS >Set-Alias wheres Compare-Property

PS>Get-ChildItem | wheres Length gt 100

例2-3 实现了这个“简单位置”功能。注意，如果输入了不存在的操作符作为＄符号参数，会生成一个错误信息。

```powershell
  & 'F:\ShouCangPin\Typora文档保存处\DotNet学习笔记\PowerShell\PowerShell应用手册\PowerShell随书源码\Compare-Property.ps1'
```



### 3. 编程：交互式过滤对象

有些时候，对我们来说Where-Object提供了太强大的功能，在这种情况下，2.2节中的Compare-Property脚本文件提供了更简单的方法。有些时候，Where-Object又太 简单了，如表达你的选择逻辑的代码十分麻烦，不如手工选择，在这种情况下，**交互式的过滤**变得更有效率。

例子2—4实现了交互式过滤。使用了一些本书没有提到的概念，你可以认为这是个灵巧的脚本。为了了解脚本中你还不能理解的内容，看看脚本中的注释。

```
 & "F:\ShouCangPin\Typora文档保存处\DotNet学习笔记\PowerShell\PowerShell应用手册\PowerShell随书源码\Select-FilteredObject.ps1"
```





### 4. 处理列表或 命令输出的每一项





### 5. 自动化数据密集型任务





https://zhuanlan.zhihu.com/p/351686861 利用 Powershell 编写简单的浏览器脚本

https://www.zhihu.com/question/46435308/answer/1590621039 使用PowerShell可以做那些有趣的事情?

https://www.zhihu.com/market/pub/119960136/manuscript/1289513048127352832

https://zhuanlan.zhihu.com/p/429002760 自定义供日常使用的PowerShell脚本模块

https://zhuanlan.zhihu.com/p/555519648



## 第四章 循环与流程控制

---

**简介**

当你开始编写脚本或命令来操作未知的数据的时候，对**数据的循环与流程控制**变得日益重要。

PowerShell的循环语句和命令可以允许你执行一个操作，而不用重复命令本身。比如说，执行某项任务特定次数，处理集合中的每一项，或者一直执行某一任务直到满足某一条件。

PowerShell的流程控制和比较的语句可以让你的脚本或命令更适合操作未知类型的数据，可以**基于数据的值**来执行命令或跳过命令。

总而言之，循环和流程控制语句使PowerShell 工具链的功能更加强大。



### 1. 通过比较和逻辑操作做出决定

**问题**

你想对两个数据进行比较，根据比较的结果做出决定。

**解决方案**

使用PowerShell逻辑运算符对数据进行比较，然后根据结果做出决定。

详细使用，参看 附录A 比较运算符

```powershell
常用比较运算符：
-eq, 
-ne,
-ge, 
-gt, 
-lt, 
-le, 
-like, 
-notlike, 
-match,
-notmatch, 
-contains,
-notcontains, 
-is, 
-isnot
常用逻辑符
-and 且
-or 或
-xor 异或
-not 否/非
```

==待补充==



### 2. 使用条件语句控制脚本流程

----

**问题**

控制流程



**解决方案**

使用if 、elseif、else条件语句 来控制

```powershell
$temperature = 90
if($temperature -le 0)
{
	"Balmy Canadian Summer"
}
elseif($temperature -le 32)
{
	"Freezinig"
}
else
{
	"Hot"
}
# 输出 Hot
```

**讨论**

![image-20230109105629935](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/17cc6084a4f83c271e67f898c1460ddc-image-20230109105629935-8970b2.png)

### 3. 使用Switch管理条件语句

**问题**

控制大量的if else 

**解决方案**

使用switch来控制

```powershell
$temperature = 20
switch($temprature)
{
	{$_ -lt 32} { "Below Freezing"; break }
	32 			{ "Exactly Freezing"; break }
	{$_ -le 50} { "Cold"; break }
	{$_ -le 70} { "Warm"; break }
	default { "Hot"; break }
}
#返回 Below Freezing
```



**讨论**

![image-20230109110346830](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/27f91ffd44a2a10f2de67f7be593afcb-image-20230109110346830-88ffd0.png)

![image-20230109110357363](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/eb32ff75d711f15eb07387d4e7b02f59-image-20230109110357363-eb0ca6.png)

:timer_clock:

```powershell
就暂时学到这，2023-1-9 11:05:18 ，明天接着学习 循环 
```







## 附录A PowerShell 语言和环境 

----







### 比较操作符

**重点提要**

* ==不区分大小写==
* 对于需要严格区分的地方 
  * 区分`-i` 前缀 
  * 不区分`-c` 前缀

* 相等运算符

* 匹配运算符

* 容量运算符

* 替代运算符

* 类型运算符

| 操作符         | 含义                                                         |
| -------------- | ------------------------------------------------------------ |
| `-eq` 等于     | 如果值相等，则此运算符返回布尔值`TRUE`，否则返回`False`。    |
| `-ne`不等于    | 如果值不相等，则此运算符返回布尔值`TRUE`，否则返回`False`。  |
| `-ge` 大于等于 | 如果运算符左侧的变量值大于或等于运算符右侧的变量值，则此运算符返回布尔值`TRUE`，否则返回 |
| `-gt` 大于     | 如果运算符左侧的变量值大于运算符右侧的变量值，则此运算符返回布尔值`TRUE`，否则返回`False` |
| `-lt` 小于     | 如果运算符左侧的变量值小于运算符右侧的变量值，则此运算符返回布尔值`TRUE`，否则返回`False` |
| `-le`不小于    | 如果运算符左侧的变量值小于或等于运算符右侧的变量值，则此运算符返回布尔值`TRUE`，否则返回 |
| `-like`        | 使用通配符匹配字符串，则`-like`运算符将返回布尔值`TRUE`      |
| `-notlike`     | 字符串与通配符不匹配，则`-notlike`运算符将返回布尔值`TRUE`   |
| `-match`       | 使用通配符匹配字符串，则`-match`运算符将返回布尔值`TRUE`。 如果输入是列表，则`-match`运算符返回列表的匹配数据成员 |
| `-notmatch`    | 字符串与通配符不匹配时，`-notmatch`运算符将返回布尔值`True`  |
| `-contains`    | 运算符右侧的值存在于运算符左侧的值集中时，此运算符将返回布尔值`TRUE` |
| `-notcontains` | 运算符右侧的值在运算符左侧的值集中不存在时，此运算符返回布尔值`TRUE` |
| `-is`          | 运算符左侧的值指定为Microsoft .NET类型时，此运算符将返回`True` |
| `-isnot`       | 未将运算符左侧的值指定为Microsoft .NET类型时，`-isnot`运算符将返回布尔值`True` |
| `-in`          | 运算符左侧的值存在于运算符右侧的值集中时，此运算符将返回布尔值`TRUE` |
| `-notin`       | 运算符左侧的值在运算符右侧的值集中不存在时，此运算符返回布尔值`TRUE` |




CodeWars2023Rocky

**讨论**

1. 默认情况下，所有比较运算符均区分大小写。 这些运算符可帮助我们查找，测试，比较，修改和替换数据和信息。 

哪个对？



### 逻辑操作符

---

**提要**

比较布尔类型值



















# 自己摸索的 

1. 三个常用命令、 command、help、member
2. variable  可以查看所有的 变量
