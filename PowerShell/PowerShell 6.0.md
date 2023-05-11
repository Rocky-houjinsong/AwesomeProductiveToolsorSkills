# PowerShell 6.0 

----

[toc]



* 每个cmdlet的作用都很简单，如“get” 仅检索数据，“set” 仅建立或更改数据，“format”t 仅设置数据格式，“out” 仅将输出定向到指定的目标，所以应注意怎么**组合使用**

* 每个 cmdlet 都具有一个**帮助文件**，可以通过键入以下内容访问它：get-help <cmdlet 名称> -detailed，如果只要查看简单的信息，就不要detailed这个参数，如果要查看更全面的技术信息，则需要把detailed更改为full 也可以直接使用help <cmdlet 名称>，或者直接在使用 <cmdlet 名称> -?

```powershell
get-help <cmdlet 名称> -detailed
get-help <cmdlet 名称>
get-help <cmdlet 名称> -full
help <cmdlet 名称>
man <cmdlet 名称>
<cmdlet 名称> -?
```



* 多cmdlet有内置的**别名**，如Get-Service的别名就是gsv
* Get-Command，可以列出所有的cmdlet

```powershell
Get-Command *-Service   #查找 用于查看修改Windows服务的cmdlet 列表
Get-Help Get-Service	# 查看帮助信息  help函数别名 man  故 man  Get-Service也是可以的
man Get-Service
Get-Process  -?
Get-Help -Category Get-Service # 获取所有Get-Service帮助文章的列表  无法使用 ,该参数无效 ? 
Get-Help Get-ChildItem -Detaile  # 显示详细信息
Get-Help Get-ChildItem -Full		#显示帮助文章的所有内容
Get-Help Get-ChileItem -Parameter *	  #获取参数的详细帮助
Get-Help Get-ChileItem -Examples	#显示帮助文章的示例
Get-Service | Get-Member # 返回命令对象的 输出对象信息
PowerShell				# 启动PowerShell 交互式界面 按住Ctrl+Shift + Enter 管理员方式启动
PowerShell_ISE			#启动PowerShell_ISE 集成脚本环境
Stop-Computer			# 关闭计算机
Get-Computer			# 列出网络上所有计算机
Get-Date				# 获取系统日期

Get-Command -Verb Get 	# 使用Verb参数 列出包含特定谓词 Get的所有命令
Get-Command -Noun Service # 使用Noun参数 查看对同一类型的对象产生影响的命令系列
Get-Command *-Service   #查找 用于查看修改Windows服务的cmdlet 列表  作用和上面的好像差不多啊 

Clear-Host #函数 ，清空输出窗口 alias别名—— cls、clear

## 常见命令别名  —————— 输入 Get-Command *   Alias类型的就可以查看
cat 			# 获取文件内容
dir				# 查看当前路径内的文件夹和文件
rm
cd				# 打开文件夹


clear		# clear-Host 清空当前输出窗口

cls          # clear-Host 清空当前输出窗口
history
pushd
tee
copy
kill
pwd			# Get-Loaction 获取当前路径

Get-Alias cls #显示 与别名关联的本机PowerShell命令的真实名称
Get 缩写是 g
Set 缩写是 s
Item 缩写是 i
Location 缩写是l
Command缩写是 cm
Alias 缩写是al
Get-Item 缩写是 gi
Get-Loaction #缩写是 gl   pwd  使用 get-help get-location -full  可以查到 ; 或者 get-alias 查看
Get-Alias 缩写是 gal
Set-Loaction 缩写是sl
Set-Alias-Name gcm -ValueGet-Comman # 创建新别名



Get-Help about_*  #显示 概念文章的列表  Get-Help 的参数 Parameter、Examples等对概念帮助文章的显示无影响
Get-Help about_command_syntax #  显示某一特别的帮助文章


Get-Help registry # 获取有关Registry程序的帮助
Get-Help -Category provider # 获取会话中的所有提供程序帮助文章的列表    失效?
Get-Help Clear-Host -Online # 在线版本的帮助文档

Get-Command 		# 显示在当前会话中可用的命令
Get-Command Get-Help -Syntax 		# 获取Get-Help 的语法

Get-Command *    		#获取会话中的所有命令


Get-Command -CommandType Alias     # 获取命令别名
Get-Command -CommandType  Function	#获取当前会话中的函数
Get-Command -CommandType Script		#显示PowerShell搜索路径中的脚本


$loc	`	#仅创建变量，未分配至

$loc = Get-Location # 变量已存在，无需创建，直接分配值给现有变阿玲

$loc			# 输出
$loc | Get-Member -MemberType Property	#使用Get-Member 显示有关变量内容的信息
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap  #操作变量的命令列表

# Remove-Variable cmdlet 来删除当前会话中所有不受PowerShell 控制的变量。键入以下命令来清除所有变量
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue

Get-Variable # 显示 PowerShell 系统变量
Get-ChildItem Variable:    # 显示 使用变量驱动器的所有PowerShell变量
Get-ChildItem env: # 查看变量=> PowerShell可以使用任何 Windows进程可用的相同环境变量，似乎就是环境变量

$env:SystemRoot # 访问SystemRoot 变量的值
$env:LIB_PATH='/user/local/lib'		#创建新的环境变量 环境变量名称全部大写

# 管道运算符 | ， 连接命令， 每个命令的输出都将用作下一个命令的输入  传递对象，而非文本
Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging
 Get-ChildItem -Path C:\WINDOWS  -Recurse | Out-Host -Paging # 这两个不要 只运行前一半，很费时
 
 # 知道别名 查命令 
 Get-Alias cls
 # 知道命令查别名
 
 Get-Location | Get-Member # 获取 Get-Location返回的对象信息，
 Get-Location		# 仅是文本摘要 返回 PathInfo 对象，其中包含当前路径和其他信息。
 
 

```







## 参考博客文章

* https://www.jb51.net/article/115518.htm Read By 2022年12月8日11:36:25

* https://www.jb51.net/article/196281.htm  Read By 2022年12月8日09:27:59

* https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.management/get-childitem?view=powershell-5.1 Read By 2022年12月8日14:38:01

* https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.utility/get-host?view=powershell-5.1&WT.mc_id=ps-gethelp 

  **Get-Host** ReadBy 2022年12月9日09:03:04



### 2022-12-16 10:35:22

1. https://blog.csdn.net/xoofly/article/details/105720207     一般，也就能看看 里面的几个实例

```powershell
get-service | Where-Object {$_.Status -eq 'running' -and $_.StartType -eq 'manual'}
# 获取正在运行的，且是需要手工启动的服务

$xname = 'kahn','serena','yiwanka' #定义数组变量
# 打印数组第一个值--->$xname[0]
#统计数组count--->$xname.count

Write-Output "kahn hello world" | Where-Object { $_.length -GT 2 } #接受一个字符串，如果字符串大于2就输出到屏幕


# 自定义磁盘容量
Get-WmiObject -class win32_logicaldisk -computername localhost -filter "drivetype=3" | Sort-Object -property DeviceID |`
Format-Table -property DeviceID,@{label='FreeSpace(MB)';expression={$_.FreeSpace / 1MB -as [int]}},`
@{label='Size(GB)';expression={$_.Size / 1GB -as [int]}},`
@{label='%Free';expression={$_.FreeSpace / $_.Size * 100 -as [int]}}


set-ExecutionPolicy RemoteSigned # 开启本机执行powershell脚本权限
```

2. https://learn.microsoft.com/zh-cn/previous-versions/technet-magazine/ff394367(v=msdn.10)#windows-powershell 学习 Select-Object 还可以重命名的作用

---

## 学习方法：

1. 每天学习 60分钟的 PowShell 实战指南第三版的 ，基本每天一个章节 和测试 ，记录和整理到 笔记中

2. 每天看MSDN在线版本的一个命令的具体使用方法，将 学过的链接放到 参考博客文章中 ，添加上时间

3. 2022年12月9日09:42:03，昨晚在B站无意发现 PowerShell作者发布的视频，内容是真的很不错，到时周末有空看看 

   很多内容都是书上没有的，可以作为补充

4. http://PowerShell.org  里面免费电子书、年度现场会议、在线研讨会

5. YouTuBe.com/powershellorg PowerShell + DevOps峰会

6. http://YouTuBe.com/jdhitsolutions  Jeff的频道

7. https://www.dovov.com/cx/shell.html 实际使用开发过程中遇到的问题集合



2022年12月16之后的下周，进入试用 ，写需求，每天的自主学习的时间变少；

转变，基础PowerShell的理论知识，每天学习 **30min** 同时，每天看 2篇 博客文章或者MSDN官方文档

学习吸收就可以；







* 学习一个完整的 命令

```powershell
Get-Help Ge-Command -Online
help  Get-Command -ShowWindow
```

 





### 更改计算机状态

```powershell
 Stop-Computer # 关闭计算机
 Restart-Compute # 重启计算机
 Restart-Computer-Force		#强制重启计算机
```





### 收集 有关计算机的信息



CimCmdlets 模块中的 cmdlet 是对常规系统管理任务最重要的 cmdlet。所有关键子系统设置都通过 WMI 公开。此外，WMI 将数据视为一个或多个项的集合中的对象。由于 Windows PowerShell 也可以使用对象，且具有允许你以相同方式处理单个和多个对象的管道，因此通过泛型 WMI 访问可以非常轻易地执行某些高级任务。



针对任意计算机使用Get-CimInstance收集特定信息

```powershell
Get-CimInstance -ClassName Win32_Destop -ComputerName .  # 收集 ，现在无法使用
```







没有写完 ，后续部分 我是学习 其语法 和 示例 



## 一章 PowerShell 基础知识

### 命令的可发现性 — Get-Command

----



1. **查找**用于查看和更改 Windows 服务的 cmdlet 列表

```powershell
Get-Command *-Service
```

![image-20221206105358687](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/dbca073bcb482387bd1bb979f7175ec3-image-20221206105358687-63a578.png)

2. 发现完成任务的 cmdlet 后，可以运行Get-Help cmdlet 来详细了解此 cmdlet。例如，若要显示Get-Service cmdlet 的**帮助信息**



```powershell
Get-Help Get-Service
Get-Help Get-ChildItem -Detaile  # 显示详细信息
Get-Help Get-ChildItem -Full		#显示帮助文章的所有内容
Get-Help Get-ChileItem -Parameter *	  #获取参数的详细帮助
Get-Help Get-ChileItem -Examples	#显示帮助文章的示例
Get-Command Get-Help -Syntax 		# 获取Get-Help 的语法
```

3. 大多数 cmdlet 会返回对象，这些对象可获得操作，然后再呈现为显示文本。若要全**面了解 cmdlet 的输出**，请将输出通过管道传递给Get-Member cmdlet。例如，下面的命令显示Get-Service cmdlet 的输出对象成员的相关信息

```powershell
Get-Service | Get-Member
```



* 想 操作系统事件日志，不知具体命令是哪个

* 然后发现 Get-EventLog命令 Tab补全

  ```powershell
  Help *log*
  Help *event*
  Help Get-EventLog
  ```

  









### 一致性 Consistency



```powershell
Get-Help Sort-Object
```



PowerShell 结合了交互式 shell 和脚本编写环境。PowerShell 可以访问命令行工具、COM 对象和 .NET 类库。此功能组合可扩展交互用户、脚本编写者和系统管理员的功能



### 面向对象 及 PowerShell的优势

PowerShell **基于对象**而非文本。命令的输出是一个对象。可以将输出对象通过管道发送给另一个命令以作为其输入

有很多不错的工具，但为何要选择学习PowerShell 呢？

UNIX工具（面向文档的操作系统） Windows 面向API的操作系统

双方各有优势，但管理方式完全不同， 在Windows上使用 Bash、AWK、SED、GREP时，

AWK对注册表不起作用、GREP对WMI不起作用、SED对 Active Directory不起作用 

UNIX中，文本处理是管理工具，一切皆文档

Windows中，文本处理工具就仅仅是 文本处理工具 

PowerShell 更多着眼于 VMS DCL 和 AS400 ，有非常好面向生产的环境 

“动词-名词“形式的 命令  和 定义完善的 参数集

 PowerShell  既可以执行UNIX命令、也可以执行Windows命令

自动化管理工具

微软给PowerShell的定位是  通过该Shell管理Windows系统的所有功能

Windows的所有组件采用该Shell

这是一个跨平台的自动化和配置工具/框架，可以很好地与您现有的工具配合使用，并且针对处理结构化数据（即 JSON、CSV、XML 等）、REST API 和对象模型进行了优化。
该软件有 130 多个命令行开关 (cmdlet)，这些专用命令旨在利用特定功能，可以执行多种类型的作业，从服务或进程管理到注册表或对象操作任务。
由于 Windows **PowerShell** 提供对 Windows Management Instrumentation (WMI) 和组件对象模型 (COM) 的访问，因此可以进行本地或远程管理。
此外，由于包中包含托管 API，开发人员可以将运行时集成到他们创建的应用程序中。

### 启动PowerShell

在 Cmd.exe、Windows PowerShell 或 Windows PowerShell ISE(集成脚本环境) 中，若要启动 WindowsPowerShell

我自己使用就是 **Win + R** 输入  Ctrl+Shift + Enter **管理员方式启动**

```powershell
PowerShell
PowerShell_ISE
```

启动 Windows PowerShell 2.0 引擎

> Windows PowerShell 4.0 和 Windows PowerShell 3.0 旨在能够与 Windows PowerShell 2.0 向后兼容。为 Windows PowerShell 2.0 编写的 Cmdlet、提供程序、管理单元、模块以及脚本无需更改，即可在Windows PowerShell 4.0 和 Windows PowerShell 3.0 中运行。但是，由于 Microsoft.NETframework 4 中的运行时激活策略的更改，如果使用 CLR 4.0 编译的 Windows PowerShell 3.0 或Windows PowerShell 4.0 中未进行修改，为 Windows PowerShell 2.0 编写并使用公共语言运行时 (CLR)2.0 编译的 Windows PowerShell 主机程序将无法运行。

```powershell
PowerShell.exe -Version 2
```



使用 Windows PowerShell 2.0 引擎启动后台作业

```powershell
Start-Job{Get-Process}-PSVersion2.0
```

![image-20221229085911539](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/a55e9443227cc6e2fbed544bdad61a41-image-20221229085911539-79f736.png)

**服务和进程是计算机上具有明确定义的生命周期的可管理元素的示例**

大多数命令用于管理操作系统或应用程序中的元素，如服务或进程。



**Cmdlet 使用谓词-名词的名称来减少命令记忆**

* 谓词并不始终是英文谓词，但在 PowerShell 中表达特定的操作
* 名词 描述在系统管理中十分重要的特定类型的对象。



```
Get-Process
Stop-Process
Get-Service
Stop-Service
```

对于包含两个名词和两个谓词的此示例，一致性并未简化太多学习。将该列表扩展为一组标准化的 10 个谓词和 10个名词。现在你只需要了解 20 个词。但是这些词可以组合形成 100 个不同的命令名称。



PowerShell 直接处理参数，并使用参数的这种直接访问权限以及开发人员指南标准化参数名称

标准化参数分隔符。使用 PowerShell 命令，参数名称前面始终带有“-”

在任何 cmdlet 上指定-?参数时，PowerShell 将显示该 cmdlet 的帮助



### 可调参数

---

具备命令 和 数据的情况下，使用 可调参数 ,生成参数 -ComputerName，形成参数化脚本

```powershell
<#
解析引擎忽略其中内容
.Synopsis
This is the  short explanation
.Parameter ComputerName
This is a  ...
.Example
DiskIndo -Computername remote


#>

[CmdletBinding()]    # 启用Parameter属性 允许我们使用该属性 使操作变为强制操作
param{
	[Parameter(Mandatory=$True)]
	[string[]]$ComputerName = 'localhost'
}
Get-WmiObject -ComputerName $ComputerName -Class  win32_Logicaldisk -filter "DeviceID='C:'" | select @{n='freegb';e={$_.FreeSpace /1gb -as [int] } }
```

get-help 就可以查看保存好的脚本的 帮助信息和 语法



在参数化脚本的基础上，设置自己的参数

### 位置参数、通用参数

PowerShell 有几个通用参数。这些参数由 PowerShell 引擎控制。通用参数的行为方式始终相同。通用参数有**WhatIf、Confirm、Verbose、Debug、Warn、ErrorAction、ErrorVariable、OutVariable和OutBuff**

建议的参数名称 

示计算机的参数的建议名称是 ComputerName

其他重要的建议参数名称是 Force、Exclude、Include、PassThru、Path 和 CaseSensitive





![image-20221209111049423](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/43b4df62ed14f97825212fac25983300-image-20221209111049423-4e1e93.png)

![image-20221208142026857](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/3e9297905ec013ffc5b2727ed852a267-image-20221208142026857-bb61cb.png)

![image-20221208142044561](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/b33c17084f0950cf5a447a6b5d529660-image-20221208142044561-85076f.png)





![image-20221208142043633](PowerShell%206.0.assets/image-20221208142043633.png)

![image-20221209111134314](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/1799e3c859d9e3ee2d7f675c720935a9-image-20221209111134314-ed544d.png)

![image-20221208142150656](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/d6aa3dae26ecfeb3d18ca97abbfd1986-image-20221208142150656-5f7adf.png)

![image-20221208142225043](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/0ff925587767872be0f047523b08188c-image-20221208142225043-a21f59.png)



![image-20221208143416031](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/3e10ec62d5f4044e5b6c1c73414707dd-image-20221208143416031-dcacca.png)

![image-20221209111233832](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/715fe298c41f18e494e46a1b18990038-image-20221209111233832-818a29.png)



![image-20221209111252528](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/a2995040c0d178b125bc5010e5f5e23b-image-20221209111252528-7a4417.png)

![image-20221209111308241](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/4ceb5870d29bfe908017e86111dc2bbc-image-20221209111308241-ac04c9.png)



![image-20221209111336826](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/4137f28c33ccf325abc5ba921895df35-image-20221209111336826-d875a0.png)



### 别名

PowerShell 支持别名以通过备用名称引用命令。别名允许具有其他 Shell 经验的用户使用其已知的常见命令名称在 PowerShell 中执行类似操作

别名将新名称与其他命令关联。例如，PowerShell 具有名为Clear-Host的内部函数，该函数清空输出窗口。可以在命令提示符下键入cls或clear别名。PowerShell 解释这些别名并运行Clear-Host函数

* 为何同一个cmdlet有那么多的别名啊 ，例如 Get-Content有三个 ，gc、cat、type

因为 PowerShell 有自己的一套命名系统 简称 gc，同时 包含 cmd、nuix的 ；所以 有时就有不止1个别名

```powershell
get-alias # 获取别名列表
```



Get-Help  cmdlet 也会显示 有关 PowerShell中的概念文章 概念帮助文章 以 about_ 前缀开头 ；

概念文章 的名称 必须英文输入，在非英语版本中的PowerShell中也也是如此



* Get-Command  命令列出 当前会话中的 

1. cmdlet
2. 别名
3. 功能
4. 脚本
5. 外部可执行文件 、已注册的文件类型处理程序的文件



在 PowerShell 中运行 cmdlet 时，可以看到**文本输出**，因为必须在控制台窗口中**以文本形式表示对象**。文本输出可能不会显示输出的对象的所有属性。

**文本输出是信息摘要**，而非Get-Location返回的对象的完整表示形式。



择中自动填充文件名或路径，键入部分名称并按下Tab键。PowerShell 会自动将名称扩展至找到的第一个匹配项。重复按下Tab将循环浏览所有可用选择。

### 快捷键

* Ctrl + C  停止运行命令
* End 跳转到 最新的一行
* Tab 代码辅助  shift+ Tab 也是可以使用的  空格+ 短横杠 显示可用参数
* Ctrl + R 也是查看历史命令 
* 在 | 管道之后按回车，换行书写
* 按住SHIFT点右键就有 PowerShell的快捷菜单

![image-20221229090005298](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/cf3bd3f1118044403199331651950585-image-20221229090005298-5a30fe.png)





### 切换盘符  

```
 F:
 D:
 E:
 .\ 作用是啥？
```

### 参数值 

![image-20221208142931393](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/f77fd32f02c2b22a0addb71f9260a4ef-image-20221208142931393-f8abb8.png)

![image-20221208143058876](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/83e1aab1846fee460f949fe8d013e34e-image-20221208143058876-e40c7a.png)

![image-20221229092854413](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/b5cf4773a147f4321ce3bc19852470cb-image-20221229092854413-33cd35.png)



### 参数集 与 通用参数

---

```powershell
Get-Command  Get-Eventlog -syntax
```

![image-20221229090803095](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/497ea466e848970dda95bb738c80a002-image-20221229090803095-4d1886.png)

![image-20221229090859211](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/f0ed756fc002cc98bc2a0042bdbb6834-image-20221229090859211-0c5670.png)



### 帮助系统-可更新



每一月 更新帮助文档 很重要 

![image-20221208134648192](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/08ca396f7fc809f649b09dca66c5d200-image-20221208134648192-4c9fed.png)





![image-20221208134923296](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/e584ce118789afde1d0e6f363d3331ea-image-20221208134923296-3637cd.png)



![image-20221208135118638](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/ee9767565ae18932a2a47492657b3116-image-20221208135118638-d8c017.png)

![image-20221208135250136](PowerShell%206.0.assets/image-20221208135250136.png)



![image-20221209111005735](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/8061195bb53263f9f6e7da724c69f266-image-20221209111005735-81265f.png)

```cmd
Help Get-EventLog -full
Help Get-EventLog -ShowWindow    # 在非Windows操作系统无法使用
```

![image-20221222104021601](PowerShell%206.0.assets/image-20221222104021601.png)









### 判断命令是否支持 管道输入

学会使用管道后，得学会判断一个命令是否支持管道输入。使用Get-Help命令获取一个命令的使用方法，对于参数，可以看到是否支持管道输入，或者通过MSDN去查询命令帮

对于里面的-InputObject则是支持管道输入，-Is则不支持管道输入

PowerShell Core 里面的-Path则是支持管道输入，-UseTransaction则不支持管道输入



### 常用变量

----

```powershell
$PSHOME				#C:\Windows\System32\WindowsPowerShell\v1.0
$PSVersionTable		#查看PS版本
firmPreference		# 查看Shell设置
```

### 用ISE编写脚本

----

Ctrl + 空格 使用IntelIsence 这个智能提示， 处理名称空间 和查找类

Ctrl + J  直接导入模板

-o  按Tab键 -outVariable  a ，将前面的结果 发送到变量a上面 





![image-20221209103939728](PowerShell%206.0.assets/image-20221209103939728.png)



### 命令运行细节

---

![image-20221213090135212](PowerShell%206.0.assets/image-20221213090135212.png)



![image-20221213090249037](PowerShell%206.0.assets/image-20221213090249037.png)

![image-20221213090435013](PowerShell%206.0.assets/image-20221213090435013.png)

![image-20221213090631402](PowerShell%206.0.assets/image-20221213090631402.png)

### 获取命令参数简称

```powershell
(Get-Command Get-EventLog | select -ExpandProperty parameters).ComputerName.Aliases
```

> 获取 Get-EventLog命令的参数ComputerName的简称 cn



### 位置参数

![image-20221213091227851](PowerShell%206.0.assets/image-20221213091227851.png)



![image-20221213091359436](PowerShell%206.0.assets/image-20221213091359436.png)



![image-20221229091550447](PowerShell%206.0.assets/image-20221229091550447.png)x

### 使用 Show-Command

---

 用图形化方式 进行显式输入，学习PowerShell的最佳方式 

![image-20221229093121235](PowerShell%206.0.assets/image-20221229093121235.png)

## 实际开发学到的技巧集合



### 中文乱码

----



```powershell
chcp 65001
```

### PowerShell 安装 新的模块

---

```powershell
Find-Package pscx | Install-Package -Force -AllowClobber
```



## 五章 使用提供程序

---

> 这部分难以理解 如何使用提供程序
>
> 借助  命令行操作 文件系统的方式  来理解  提供程序 和使用提供程序



### 提供程序是什么？

Powershell 的提供程序PSProvider ，本质上是一个 **适配器**

接受 某些数据存储，这样 介质看起来就像 磁盘驱动器一样。

```powershell
Get-PSProvider   #查看当前Shell中已经存在的提供程序
```

![image-20221214091336383](PowerShell%206.0.assets/image-20221214091336383.png)

### PSProvider有哪些

* Registry 注册表
* Alias  别名
* Environment 环境变量
* Filesystem 文件系统
* Function 函数
* Variable   【不知道】



==**从上面的截图就能知道 每个提供程序 ，有哪些功能，它们映射到 哪些 存储介质上面**==

> 每个 PSProvider 都是不同的，需要了解的是 ：
>
> 1. 每个提供程序 能够实现什么功能
> 2. 即便 Cmdlet知道如何实现某些功能，也不意味着 该提供程序 真正的支持对应的操作 



### **当前PSProviders功能作用** 

![image-20221214091442532](PowerShell%206.0.assets/image-20221214091442532.png)

### 扩展 ：模块 或 管理单元

![image-20221214091524647](PowerShell%206.0.assets/image-20221214091524647.png)

### 提供程序的使用

示例： 创建一个 PSDrive

通过一个特定的提供程序 连接到 某些存储数据的介质。

本质上创建一个 驱动器映射、

除了连接磁盘以外，还能连接更多的数据存储介质。

* 查看当前已连接的驱动器

```powershell
Get-PSDrive
```

![image-20221214092026192](PowerShell%206.0.assets/image-20221214092026192.png)



**PSProvider**

自己会适配 对应的数据存储，通过PSDrive机制 是的数据存储可被访问。然后使用一系列的Cmdlet

去查阅 或者操作 每个PSDrive呈现出来 的数据 ；

**多数情况下，操作PSDrive的cmdlet名词部分都包含 Item**

```powershell
Get-Command -noun *Item*
```



==从上面 的提供程序来看，包含 文件系统、注册表、别名、函数等，借助 文件系统来理解和学习PSProvider==



### 文件系统 FileSystem



![image-20221214092559928](PowerShell%206.0.assets/image-20221214092559928.png)

![image-20221214092618317](PowerShell%206.0.assets/image-20221214092618317.png)

![image-20221214092658952](PowerShell%206.0.assets/image-20221214092658952.png)

![image-20221214092738706](PowerShell%206.0.assets/image-20221214092738706.png)





![image-20221214092918893](PowerShell%206.0.assets/image-20221214092918893.png)



![image-20221214092928344](PowerShell%206.0.assets/image-20221214092928344.png)



![image-20221214093037561](PowerShell%206.0.assets/image-20221214093037561.png)

```powershell
Get-ItemProperty -Path Env:\PSModulePath
```

![image-20221214093431860](PowerShell%206.0.assets/image-20221214093431860.png)

![image-20221214094030790](PowerShell%206.0.assets/image-20221214094030790.png)



### 文件系统 的操作

* 切换路径

![image-20221214094118314](PowerShell%206.0.assets/image-20221214094118314.png)

* 新建项

![image-20221214094214123](PowerShell%206.0.assets/image-20221214094214123.png)

![image-20221214094245432](PowerShell%206.0.assets/image-20221214094245432.png)



![image-20221214094258009](PowerShell%206.0.assets/image-20221214094258009.png)

![image-20221214094604800](PowerShell%206.0.assets/image-20221214094604800.png)

```powershell
New-Item testFolser
```

![image-20221214094744399](PowerShell%206.0.assets/image-20221214094744399.png)

![image-20221214094801124](PowerShell%206.0.assets/image-20221214094801124.png)

![image-20221214094812482](PowerShell%206.0.assets/image-20221214094812482.png)

![image-20221214094848055](PowerShell%206.0.assets/image-20221214094848055.png)

![image-20221214095004051](PowerShell%206.0.assets/image-20221214095004051.png)



![image-20221214095021879](PowerShell%206.0.assets/image-20221214095021879.png)



![image-20221214095051968](PowerShell%206.0.assets/image-20221214095051968.png)



### 尝试 注册表



![image-20221214095126346](PowerShell%206.0.assets/image-20221214095126346.png)

![image-20221214095220629](PowerShell%206.0.assets/image-20221214095220629.png)

![image-20221214095239367](PowerShell%206.0.assets/image-20221214095239367.png)



![image-20221214095259745](PowerShell%206.0.assets/image-20221214095259745.png)



![image-20221214095308517](PowerShell%206.0.assets/image-20221214095308517.png)



## 六章 管道：连接命令

---

![image-20221214095759689](PowerShell%206.0.assets/image-20221214095759689.png)

![image-20221214095850917](PowerShell%206.0.assets/image-20221214095850917.png)

![image-20221214104107102](PowerShell%206.0.assets/image-20221214104107102.png)



![image-20221214104119940](PowerShell%206.0.assets/image-20221214104119940.png)

![image-20221214104152069](PowerShell%206.0.assets/image-20221214104152069.png)



![image-20221214104249237](PowerShell%206.0.assets/image-20221214104249237.png)





![image-20221214101850059](PowerShell%206.0.assets/image-20221214101850059.png)

![image-20221214101921053](PowerShell%206.0.assets/image-20221214101921053.png)



![image-20221214102018881](PowerShell%206.0.assets/image-20221214102018881.png)



![image-20221214102122309](PowerShell%206.0.assets/image-20221214102122309.png)



![image-20221214102258436](PowerShell%206.0.assets/image-20221214102258436.png)



![image-20221214102432288](PowerShell%206.0.assets/image-20221214102432288.png)



![image-20221214102612694](PowerShell%206.0.assets/image-20221214102612694.png)



![image-20221214102633660](PowerShell%206.0.assets/image-20221214102633660.png)

![image-20221214102651390](PowerShell%206.0.assets/image-20221214102651390.png)

![image-20221214102728165](PowerShell%206.0.assets/image-20221214102728165.png)



![image-20221214102805803](PowerShell%206.0.assets/image-20221214102805803.png)



![image-20221214102845079](PowerShell%206.0.assets/image-20221214102845079.png)



![image-20221214102950502](PowerShell%206.0.assets/image-20221214102950502.png)



![image-20221214103037906](PowerShell%206.0.assets/image-20221214103037906.png)





![image-20221214103453441](PowerShell%206.0.assets/image-20221214103453441.png)





![image-20221214103632743](PowerShell%206.0.assets/image-20221214103632743.png)



![image-20221214103657028](PowerShell%206.0.assets/image-20221214103657028.png)



![image-20221214103714433](PowerShell%206.0.assets/image-20221214103714433.png)



![image-20221214103737646](PowerShell%206.0.assets/image-20221214103737646.png)

![image-20221214103841449](PowerShell%206.0.assets/image-20221214103841449.png)







## 24章，使用正则表达式解析文本文件

----

![image-20221216101639091](PowerShell%206.0.assets/image-20221216101639091.png)



![image-20221216101819416](PowerShell%206.0.assets/image-20221216101819416.png)

![image-20221216101841781](PowerShell%206.0.assets/image-20221216101841781.png)



### 正则表达式入门 



-----

![image-20221216102906735](PowerShell%206.0.assets/image-20221216102906735.png)

![image-20221216102915863](PowerShell%206.0.assets/image-20221216102915863.png)

![image-20221216102924109](PowerShell%206.0.assets/image-20221216102924109.png)

![image-20221216102932688](PowerShell%206.0.assets/image-20221216102932688.png)

### 通过 —Math 使用正则表达式

---

![image-20221216103001393](PowerShell%206.0.assets/image-20221216103001393.png)



### 使用Select-String 使用正则表达式

---

![image-20221216103024372](PowerShell%206.0.assets/image-20221216103024372.png)

![image-20221216103032649](PowerShell%206.0.assets/image-20221216103032649.png)

![image-20221216103042229](PowerShell%206.0.assets/image-20221216103042229.png)

![image-20221216103049591](PowerShell%206.0.assets/image-20221216103049591.png)









```powershell
$ConfirmPreference
```

## 九章 深入理解管道

----



### 更少的输入，更强大的功能

查看示例，比其他脚本或编程语言来实现同样的目的，使用更加简介

```
Get-Process | Sort VM –desc | Select –first 10
Get-Process | Sort VM -desc | ConvertTo-HTML | Out-File process.html
```

![image-20221216094153033](PowerShell%206.0.assets/image-20221216094153033.png)



### 管道参数绑定

---

![image-20221216094403655](PowerShell%206.0.assets/image-20221216094403655.png)





### ByValue

![image-20221216094516156](PowerShell%206.0.assets/image-20221216094516156.png)

![image-20221216094820064](PowerShell%206.0.assets/image-20221216094820064.png)

![image-20221216094926569](PowerShell%206.0.assets/image-20221216094926569.png)





* 示例 ：

```powershell
 start notepad #启动 一个记事本进程
 Get-Process -Name note* | Get-Member  #搜索以note开头的进程(记事本),并查看其中的成员和属性以及返回类型
```

![image-20221216095642865](PowerShell%206.0.assets/image-20221216095642865.png)



```powershell
Get-Command Stop-Process -ShowCommandInfo
```

![image-20221216100524594](PowerShell%206.0.assets/image-20221216100524594.png)

查看语法信息，知道会匹配到InputObject这个参数 ；



```powershell
 Get-Process -Name note* | Stop-Process  #组合起来就是，找到记事本进程，并杀死
```



> 按照这个思路 ，运行出现 这个问题： 
>
> 引出 备选方案

![image-20221216100907415](PowerShell%206.0.assets/image-20221216100907415.png)



### ByPropertyName

---





## 28 备忘清单

---

### 标点符号 

---

#### 1. `重音符

----

转义字符， ==移除紧跟在重音符之后的字符串中包含的特殊含义

空格是 一个分隔符，· 作用就是将 该字符转义，将空格的作用去除

```powershell
cd C:\Program Files #失败 

cd C:\Program' Files #成功
```





#### 2. ~ 波浪符 

---

路径 一部分 ，表示当前用户的根目录 

```powershell
 cd ~
```



#### 3. （） 括号

---

* 数学中，优先计算 ,从里向外执行 

  ```powershell
  Get-Service -ComputerName (Get-Content C:\ComputerName.txt)
  ```

* 包含一个方法的参数 。即使 该方法  不要求 使用 任何参数 ，也必须带括号 

```powershell
Change-State-Mode('Audomatic')
Delete()
```

#### 4. [] 中括号

---

* 访问 数组或集合 中 某个单独的对象时使用，来指定索引号 

```powershell
$Services[2] #从中获取第三个对象
```

*  需要将 某个数据 转化为特定的类型，将 类型包含在中括号中 。

```powershell
$My Result/3 as [INT] # 除法运算结果转为整数
[XML]$Data = Get-Content Data.xml #读取 Data.XML中内容，尝试将该内容解析为合法的XML文件
```



#### 5. {} 花括号 

----

* 包含可执行代码或者 命令块 —— 脚本段 作为 值传递给那些可以接受脚本段或者筛选块的参数 

```powershell
Get-Service | Where-Object {$_.Status -eq 'Running'}
```

* 用作 构成哈希表的 键值对 ，左括号前面 总是一个 @ 符号， 

```powershell
$HashTable= @{l = 'Label'; e = {experssion}}  
```

*  变量名称中包含 空格 或者其他非法字符，使用 花括号来包含这一部分信息 

```powershell
${My Variable}
cd {C:\Program Files} #错误的，这个 参数指定为脚本块了
```



#### 6. ‘ ’ 单引号 

---

包含字符串， 不会对包含在单引号中的字符串 查找转义字符或者变量

```powershell
cd 'C:\Program Files'
```



#### 7. " " 双引号

----

包含字符串， 但是 ，会针对 包含在双引号中的字符串 数据  ==进行查找转义字符以及$字符==

进行 对转义字符的处理，同时针对$符号后面带有的字符 直到下一个空格位置 进行识别并替换为 值 

```powershell
PS C:\Program Files>
PS C:\Program Files> $One = 'World'
PS C:\Program Files>
PS C:\Program Files> $Two = "Hello $One 'n"
PS C:\Program Files>    
PS C:\Program Files> echo $Two
Hello World 'n
PS C:\Program Files>   # ‘n 代表一个回车键

```



#### 8. $ 美元符号

$后面的字符 为一个变量的名称 有如下的区别

```powershell
PS C:\Users\hp> $One = 'Two'
PS C:\Users\hp>
PS C:\Users\hp> New-Variable -Name $One -Value 'Hello'
PS C:\Users\hp>
PS C:\Users\hp> $Two
Hello
PS C:\Users\hp>
PS C:\Users\hp> New-Variable -Name Onee -Value 'Hello'
PS C:\Users\hp>
PS C:\Users\hp> $Onee
Hello
```



#### % 百分号

---



* ForEach-Object 的别名 
* 模运算符 ，返回除法运算之后的 余数 

#### ？ 问号 

----

* Where-Object 别名



#### 11. > 右尖括号 

---



Out-File 别名 



#### 12. + - * /



#### 13. -破折号

----

* 连接参数名称或者其他运算符 

-ComputerName , -Eq

* 分离 cmdlet 动词和名词  Get-Content
* 算术中的减法

#### 14. @ at符号

---

* 哈希表左花括号前 
* 用在 括号前，构成数组 

```powershell
$Array  = @(1,2,3,4) # @ 和 （）都是可选的，因为PS默认以逗号分割的列表识别为 数组
```

*  表示一个  Here-String指包含在 单引号或者 双引号中的字符串 

​	一个 Here-String字符串以 @开头作为开始和结束标志 ，结束的@ 必须位于另起一行的起始位置

详细信息查看  Help About_Quoting_Rules ，Here-String 也可以通过单引号 来进行定义

```powershell
Help About_Quoting_Rules 
@"
    For help, type "get-help"
    "@
    
    
```



* 传递符 ，构建了哈希表， 在哈希表中， 键名称 能匹配参数名称，并且键值 作为参数的值

  就可以将  该哈希表 传递给一个 cmdlet ；

#### 15. & 与 符号

---



调用运算符 

将 某些字符识别为命令，并运行这些命令 

```powershell
$a = "Dir" 
&$a
```



#### 16. ; 分号

---

* 分隔 PowerShell 中 同一行的两个命令 

```powershell
Dir;Get-Process  #先执行Dir命令，后执行Get-Process命令 他们的执行结果 会发送给一个管道，DIr执行结果不会发送给 Get-Process

```



#### 17. # 井号

----

注释符号 ，跟在 #之后的 文字，直到下个回车之前 

<> 可以被用作定义一个注释块 标签 

```powershell
# 这是单行注释
<# 
注释块1
注释块2
#>
```



#### 17. =等号

---

赋值运算符  $One = 1

==不可用作 相等性比较== ，相等性比较使用 -Eq 

* 该运算符可以和  数学运算符结合使用  $var +=5；

  

#### 18. \ /  正反斜杠

* 除法运算符
* 路径分隔符
* 反斜杠 在WMI筛选场景 以及 正则表达式中做转义字符

#### 19. .句号

---

* 希望访问某个成员，属性或者方法 

$_.Status 表示访问 $_ 占位符对象的Status属性

* 通过.  引用源码 执行一段脚本 

![image-20221222103326550](PowerShell%206.0.assets/image-20221222103326550.png)



#### 20. ,逗号

![image-20221222103637707](PowerShell%206.0.assets/image-20221222103637707.png)



#### 21. :冒号 

![image-20221222103645130](PowerShell%206.0.assets/image-20221222103645130.png)



#### 22 ！ 感叹号

![image-20221222103712900](PowerShell%206.0.assets/image-20221222103712900.png)

#### 23. ^ 脱字符

---

正则表达式运算





### 运算符

![image-20221222104148409](PowerShell%206.0.assets/image-20221222104148409.png)



![image-20221222104158639](PowerShell%206.0.assets/image-20221222104158639.png)



### 自定义属性 /列

![image-20221222104225884](PowerShell%206.0.assets/image-20221222104225884.png)

![image-20221222104302622](PowerShell%206.0.assets/image-20221222104302622.png)



### 管道参数输入

![image-20221222104339240](PowerShell%206.0.assets/image-20221222104339240.png)

![image-20221222104348593](PowerShell%206.0.assets/image-20221222104348593.png)

![image-20221222104355256](PowerShell%206.0.assets/image-20221222104355256.png)



### 使用$_ 

![image-20221222104411752](PowerShell%206.0.assets/image-20221222104411752.png)



![image-20221222104420363](PowerShell%206.0.assets/image-20221222104420363.png)







## PS in Action 1.1 欢迎来到 PS

----

![image-20230103094634739](PowerShell%206.0.assets/image-20230103094634739.png)



```powershell
Get-ChildItem -Path $env:windir\*.log | Select-String -List error | Format-Table Path,LineNumber -AutoSize
echo $env:windir #打印输出 windir目录内容
```



```powershell
([xml] [System.Net.WebClient]::new().
 DownloadString('http://blogs.msdn.com/powershell/rss.aspx')).
 RSS.Channel.Item |
 Format-Table title,link

```

![image-20230103095318218](PowerShell%206.0.assets/image-20230103095318218.png)



**![image-20230103095339636](PowerShell%206.0.assets/image-20230103095339636.png)**

```powershell
using assembly System.Windows.Forms
using namespace System.Windows.Forms
$form = [Form] @{
 Text = 'My First Form'
}
$button = [Button] @{
 Text = 'Push Me!'
 Dock = 'Fill'
}
$button.add_Click{
 $form.Close()
}
$form.Controls.Add($button)
$form.ShowDialog()
# This script uses the Windows Forms library (WinForms) to build a GUI that has a single button displaying the text “Push Me!

```



![image-20230103100138651](PowerShell%206.0.assets/image-20230103100138651.png)



What is PowerShell, and what can you do with it? Ask a group of PowerShell users and you'llget different answers:

什么是PowerShell，你能用它做什么？询问一组PowerShell用户，您将得到不同的答案：

●PowerShell is a command-line shell.Powershell是一个**命令行shell**。
●PowerShell is a scripting environment.Powershell是一个脚本环境。
●PowerShell is an automation engine.Powershell是一个**自动化引擎**。
These are all part of the answer. We prefer to say PowerShell is a tool you can use to manage这些都是答案的一部分。我们更喜欢说PowerShell是一个可以用来管理的工具。
your Microsoft-based machines and applications that programs consistency into your您的基于microsoft的计算机和应用程序可以将一致性应用到您的
management process. The tool is attractive to administrators and developers in that it can span管理过程。该工具对管理员和开发人员很有吸引力，因为它可以跨越
the range of command line, simple and advanced scripts, to real programs.命令行的范围，简单的和高级的脚本，真正的程序。

----

==解释 shell的含义==

![image-20230103101107048](PowerShell%206.0.assets/image-20230103101107048.png)

> 在上一节中，我们将PowerShell称为命令行shell。你可能会问，什么是
> shell?它和命令解释器有什么不同？脚本语言呢？如果
> 您可以使用shell语言编写脚本，难道这不是一种脚本语言吗？在回答这些
> 问题，让我们从shell开始。
> 定义一个shell可能很棘手，因为在微软，几乎所有的东西都有一个叫做
> 一个shell。Windows资源管理器是一个shell。VisualStudio有一个名为shell的组件。见鬼，甚至
> Xbox有一个叫做shell的东西。
> 从历史上看，**shell一词指的是位于操作系统上的软件**
> **核心功能**。这个核心功能被称为**操作系统内核**(shell..。
> 内核..。明白了吗？)。Shell是允许您访问所提供的功能的软件。
> 通过操作系统。为了我们的目的，我们更感兴趣的是传统的基于文本的。
> 环境中，用户键入命令并接收响应。换句话说，一个shell
> 是命令行解释器。这两个术语在很大程度上可以互换使用。

==shell与脚本script的区别和联系==

![image-20230103101648838](PowerShell%206.0.assets/image-20230103101648838.png)





>  如果是这样的话，什么是脚本，为什么脚本语言不是shell？在某种程度上，
> **没什么区别**。许多脚本语言都有一种接收命令的模式。
> 用户，然后执行这些命令返回结果。这种操作模式称为
> **读-评估-打印循环**，或REPL。以何种方式使用REPL而不是shell的脚本语言？
> 不同之处主要在于**用户体验**。正确的命令行shell也是正确的UI。
> 因此，命令行必须提供许多特性才能提供用户体验。
> 愉快和可定制，包括别名(硬到类型命令的快捷方式)、通配符
> 匹配以避免不得不键入全名，并能够轻松启动其他程序。
> 最后，命令行shell提供了检查、编辑和重新执行的机制。
> 以前输入的命令。这些机制被称为命令历史。

如果脚本语言可以是shell，那么shell可以是脚本语言吗？答案是，
显然，是的。随着每一代的发展，UNIXshell语言越来越多
强大。可以用现代shell语言(如Bash)编写大量应用程序
或者Zsh。与shell语言相比，脚本语言具有明显的优势，因为它们
提供机制，**通过让您将脚本分解为**
**组件或模块**。脚本语言通常提供更复杂的特性
调试脚本。接下来，脚本语言运行时的实现方式是
它们的代码执行效率更高，用这些语言编写的脚本执行得更快。
而不是在相应的shell脚本运行时中。最后，脚本语言语法是
更倾向于**编写应用程序**，而不是交互地发出命令。
最后，shell语言和脚本之间没有硬性和快速的区别。
语言。因为**PowerShell的目标是成为一个好的脚本语言和一个好的**
**交互式shell**，平衡用户体验和脚本编写之间的权衡是其中之一。
主要的语言设计挑战。

==因为Windows管理数量的复杂性，需要新的shell模型==

![image-20230103102526931](PowerShell%206.0.assets/image-20230103102526931.png)

另一个促使需要新的shell模型的因素是，随着Windows越来越多地获得
子系统和特性，**用户在管理系统时必须考虑的问题的数量**
**急剧增加。为了帮助用户处理这种复杂性的增加，可管理的**
**元素被分解到结构化数据对象中**。管理对象的集合是
在微软内部被称为==Windows管理界面==。



![image-20230103102735151](PowerShell%206.0.assets/image-20230103102735151.png)



微软并不是唯一一家**因复杂性增加而面临问题**的公司。
这个行业的大部分人也有这个问题。这导致了**分布式管理任务**
(dmtf.org)，一个行业组织，为管理对象创建了一个名为
**公共信息模型(CIM)**。Microsoft最初对此标准的实现是
称为**Windows管理工具(WMI)**。

![image-20230103102923429](PowerShell%206.0.assets/image-20230103102923429.png)

![image-20230103102932007](PowerShell%206.0.assets/image-20230103102932007.png)

虽然这个保理处理解决了总体的复杂性，并且在gui中很好地工作，但是它。
**更难使用传统的基于文本的shell环境**。
Windows是一种API驱动的操作系统，与UNIX及其派生程序相比，
**文档(或文本)驱动。您可以通过更改配置文件来管理UNIX**。在windows里面
，您需要使用api，这意味着**访问属性和使用**
**合适的对象。**
最后，随着PC功能的增强，Windows开始从桌面移动到
公司数据中心。在公司数据中心中，有大量的服务器
管理，和图形点和点击管理方法没有规模。所有这些元素
为了说明这一点，微软**不能再忽略命令行**了。
现在，您已经掌握了导致PowerShell创建的环境力量--需要
在基于分布式对象的操作环境中的命令行自动化--让我们看看
形成了解决方案。



## PS in action 1.2 PS示例代码 

---

三个系统中 ，windows、Linux、macOS ，一个cmdlet有2个不同的别名，一个兼容linux，一个是Cmdlet特有的，别名的使用是方便，简写，但在其他两个系统上可能有冲突，建议使用 cmdlet全名称；

同时 帮助系统自 v3不在有本地，可以使用-online 进行在线查看 具体信息；

![image-20230103104154374](PowerShell%206.0.assets/image-20230103104154374.png)

![image-20230103104236638](PowerShell%206.0.assets/image-20230103104236638.png)

![image-20230103104357474](PowerShell%206.0.assets/image-20230103104357474.png)

对于大多数人来说，用于使用文件系统的PowerShell命令应该非常熟悉。
用户。您可以使用cd(设置位置别名)命令在文件系统周围导航。档案
使用复制或cp(复制项别名)命令复制，并随移动和mv移动。
(移动项的别名)命令，并使用del或rm(移除项的别名)删除。
命令。为什么每个命令都有两个？一组名称是cmd所熟悉的。EXE/DOS用户和
另一个是UNIX用户所熟悉的。实际上，它们是同一个命令的别名，设计为
使人们更容易使用PowerShell。

Using the -Online option is the best way to get help because the online documentation is constantly being updated and corrected, whereas the local copies aren’t.



-----

==基础表达式 和变量==

注意，一旦输入表达式，结果就会被计算和显示。不是
必须使用任何类型的打印语句来显示结果。记住这一点很重要
每当计算表达式时，表达式的结果都是输出，而不是丢弃。
Powershell支持您所期望的大多数基本算术操作，包括浮动运算
重点。
可以使用重定向运算符将表达式的输出保存到文件中：

![image-20230103104847134](PowerShell%206.0.assets/image-20230103104847134.png)

还可以使用变量来存储命令的输出：

![image-20230103104914686](PowerShell%206.0.assets/image-20230103104914686.png)

在本例中，您提取了文件信息对象集合的第二个元素。
由get-child命令返回。您之所以能够这样做是因为您保存了输出。
将get-child Item命令作为$file变量中的对象数组。



![image-20230103105008621](PowerShell%206.0.assets/image-20230103105008621.png)



==Given PowerShell is all about objects, the basic operators need to work on more than numbers==

考虑到PowerShell全部是关于对象的，基本运算符需要处理的不仅仅是数字。

![image-20230103105234219](PowerShell%206.0.assets/image-20230103105234219.png)



正如您所看到的，您可以运行命令获取信息，在
此信息使用PowerShell运算符，然后将结果存储在文件和变量中。
让我们看看处理这些数据的其他方法。首先，您将看到如何排序对象和
如何从这些对象中提取属性。然后我们来看看使用PowerShell流-
控件语句来编写使用条件和循环进行更复杂操作的脚本。
处理。



##  V2EX加群 了解到的内容

---

![image-20230104152302300](PowerShell%206.0.assets/image-20230104152302300.png)



powershell电子书
https://pan.baidu.com/s/1p2zK-BewhursJxDNQnq5PQ

powershell道经-卷1：面向对象简介1
http://tieba.baidu.com/p/5888370884
http://bbs.chinaunix.net/thread-4263988-1-1.html

ps1道经-卷2：常用对象类型
http://bbs.chinaunix.net/thread-4264061-1-1.html
http://tieba.baidu.com/p/5895249893


ps1道经-卷3：面向对象语言有啥优缺点？
http://bbs.chinaunix.net/thread-4264062-1-1.html
http://tieba.baidu.com/p/5913346984


ps1道经-卷4：文件目录对象介绍
http://bbs.chinaunix.net/thread-4264293-1-1.html
http://tieba.baidu.com/p/5918905580


ps1道经-卷5：常用帮助命令
http://bbs.chinaunix.net/thread-4264294-1-1.html    **已看完** **整理完**
http://tieba.baidu.com/p/5929657423


ps1道经-卷6：单个字符对象，讲ps如何处理单个字符,含汉字 
http://bbs.chinaunix.net/thread-4264556-1-3.html
http://tieba.baidu.com/p/5937720169


ps1道经-卷7：powershell到底有何优势，为什么要学？
http://bbs.chinaunix.net/thread-4264776-1-1.html



ps1道经-卷8：用powershell读写文本、二进制文件。
http://bbs.chinaunix.net/thread-4266404-1-1.html
http://tieba.baidu.com/p/5963588220


ps1道经-卷9：powershell数组（静态，动态）
http://bbs.chinaunix.net/thread-4267455-1-1.html



ps1道经-卷10：powershell中有，世界上最好的脚本编码处理技术
http://bbs.chinaunix.net/thread-4291318-1-1.html



ps1道经-卷11：尽解powershell哈希表
http://bbs.chinaunix.net/thread-4296512-1-1.html
http://tieba.baidu.com/p/5981409125


ps1道经-卷12：如何用ps，bash编写远程脚本
http://bbs.chinaunix.net/thread-4298680-1-2.html
http://tieba.baidu.com/p/5988436385


ps1道经-卷13：
单步、断点、在图形界面中执行，鼠标选中脚本行，
在win中远程开发，远程调试linux上的ps脚本。
ps脚本调试性是shell的20倍，ps极大提升了linux脚本生产力
http://bbs.chinaunix.net/thread-4299559-1-2.html
http://tieba.baidu.com/p/6170173448


ps1道经-卷14：变量的作用域
http://bbs.chinaunix.net/thread-4300246-1-1.html


ps1道经-卷15：powershell送你一把，解决日期计算类问题的金钥匙！
http://bbs.chinaunix.net/thread-4301948-1-1.html


ps1道经-卷16：【撸串.ps1】开始学习powershell的tab补全
http://tieba.baidu.com/p/6121726614


ps1道经-卷17：我为啥不建议学python。
http://tieba.baidu.com/p/6191211153


win中通过ssh映射linux的盘符，成为win的z:盘
!http://bbs.chinaunix.net/thread-4302312-1-1.html
http://tieba.baidu.com/p/6060178453


ps1道经-卷18：excel占领linux！不会awk不用愁，powershell带来csv，excel解君忧！
http://bbs.chinaunix.net/thread-4314422-1-1.html


ps1道经-卷19：powershell6，7的新功能，新特性。
https://www.cnblogs.com/piapia/p/11505937.html


ps1道经-卷20：分享powershell脚本：同一个txt文件，300个并发写入
http://bbs.chinaunix.net/thread-4314470-1-1.html


ps1道经-卷21：不用多线程，你对不起powershell
http://bbs.chinaunix.net/thread-4314689-1-1.html
http://tieba.baidu.com/p/6317792752


ps1道经-卷22：powershell中的类sql命令。尽解ps返回对象中，属性的提取。
http://tieba.baidu.com/p/6341691298
http://bbs.chinaunix.net/thread-4315272-1-2.html
系统学过22课后，你的脚本技能将超越linux shell大神！


ps1道经-卷23：powershell的独门秘技之气运丹田（管道两端传对象），你看好不？
https://tieba.baidu.com/p/6728345533
http://bbs.chinaunix.net/thread-4315938-1-2.html

ps1道经-卷23-1：把每层管道结果，存变量里2
http://bbs.chinaunix.net/thread-4319692-1-2.html


ps1道经-卷24：只要能装上powershell，即可丢弃awk，sed，python，ansible
https://tieba.baidu.com/p/6973086756


ps1道经-卷25：【string】对象的方法、属性、详解
https://tieba.baidu.com/p/7070955487
http://bbs.chinaunix.net/thread-4316580-1-1.html

ps1道经-卷31：powershell的nosql真经，之litedb库
http://bbs.chinaunix.net/thread-4320276-1-1.html





问：2021年了，学了powershell后，哪些linux命令【不需要】再学？
答：
shell小部分功能不行，需要借助python。但学了powershell后，基本不需要学python了。
awk，
sed，
grep，用select-string，select-object，where-object
cat/tail/head/wc，用gc支持编码，.count属性代替wc。
grep，where-object不用-v
ls，
find，
tr，
sort，
date，
seq，1..10
stat,get-childitem
mv/rm,

问：哪些linux命令还需要学？
答：
chmod
useradd
userdel
usermod
groups
groupdel
passwd
chown
top
free
kill
netstat
lsof
ps，实际上ps的大部分功能，get-process可以代替。
nohup



## PS传教士编写的入门语法

-----

==**powershell基础语法**==

powershell语法比python简单。对象，库，功能强大。
隐藏的限制，坑，比shell少。
语法一致性，比awk，sed，python等好。学多种语言，多个if语法，多种正则语法，在你脑中打架。
基本上此一种语言，可以解决所有运维，脚本问题。

本人格言：
powershell=【200%的shell功能】+【110%的python功能】
powershell和shell的语法，用法，95%相同。
把shell，换成linux版powershell后，96%以上的问题会消失。

-----【==变量定义==】-----
变量的**定义和引用**，必须用【$】打头【空格】或【运算符】结尾。
任意**数字作为变量名**。如$1 $123 $3顾茅庐，这一点比python强。
支持固定变量类型，即限制+强制转换变量类型，这一点比python强。

```powershell
$1 $123 $3顾茅庐
[string]$a = 'a' #限制变量为字符型。
$a = 3.1  # echo $a  结果是3.1
${a-b}=1 #对于复杂变量，可以用**${}来表示变量名的头尾**
```

[string]$a = 'a' #限制变量为字符型。

$a = 3.1 

支持任意中文，unicode符号作为变量名。如： $张三 = 2

不支持：
对于复杂变量，可以用**${}来表示变量名的头尾**，下同。这一点和shell相同。
变量名不支持【-】，如【$a-b=1】，【-】会被识别为减号。可以写成${a-b}=1
同理，不支持：
+,-,*,/,%,:,|,
**冒号被识别为变量作用域分割符。或驱动器符号**。  

powershell变量定义支持 $1 、$2 、 $123数字开头 、 $if 等。   

**连等：**
$a,$b,$c = 1,2,3

$数组=1,2,3
$a,$b = $数组

$a
1

$b
2,3

$b[0]
2

$数组 = 1,2,'a',(get-date)

powershell全局变量：不建议多线程同时写。
$global:a=1
支持脚本1结束后，写入全局变量，脚本2继续用，以达到【多脚本公用变量】。
变量存在进程中，可以实现【内存数据库】，【对象池】等场景。



-----【==powershell关键字==】-----

```powershell
Get-Help *Language* #获取到about_Language_Keywords 这个帮助文件
Get-Help about_Language_Keywords -full
https://learn.microsoft.com/zh-cn/powershell/module/Microsoft.PowerShell.Core/About/about_language_keywords?view=powershell-7.2
```

Keyword            Reference

-------            ---------
begin		about_Functions、 about_Functions_Advanced
break		about_Break， about_Trap
catch		about_Try_Catch_Finally
class		about_Classes
continue		about_Continue， about_Trap
data		about_Data_Sections
define		保留以供将来使用
do		about_Do， about_While
dynamicparam		about_Functions_Advanced_Parameters
else		about_If
elseif		about_If
end		about_Functions， about_Functions_Advanced_Methods
enum		about_Enum
exit		本主题中所述
filte		about_Functions
finally		about_Try_Catch_Finally
for		about_For
foreach		about_ForEach
from		保留以供将来使用
function		about_Functions、 about_Functions_Advanced
hidden		about_Hidden
if		about_If
in		about_ForEach
param		about_Functions
process		about_Functions、 about_Functions_Advanced
return		about_Return
static		about_Classes
switch		about_Switch
throw		about_Throw、 about_Functions_Advanced_Methods
trap		about_Trap、 about_Break、 about_Try_Catch_Finally
try		about_Try_Catch_Finally
until		about_Do
using		about_Using， about_Classes
var		保留以供将来使用
while		about_While、 about_Do

-----【==注释==】-----
#单行

<#
多行
#>

-----【==引号==】-----
1 单引号中，可以有双引号。**单引号内变量不能解析**。'       "a"       '
$a不能解析展开=1
Write-Host '       "$a不能解析展开"       '

返回：
"$a不能解析展开"

2 双引号中，可以有单引号。"   'b'       "
$b可以解析展开=2
Write-Host "       '$b可以解析展开'  "
返回：
'2'

3 中文双引号同双引号。
4 **中文单引号同单引号**。

5 
@"
**多行双引号内，变量可展开**。
"@

6 
@'
**多行单引号内，变量不可展开**。
'@



-----【输出】-----
write-host “支持中文单双引号，双引号解析内部变量值。支持不换行 ”   -NoNewline
write-host  ("a" * 10)

-----【类型转换】-----
PS A:\pscode> [int]$a = 3.14
返回
PS A:\pscode> $a
3

**Convert.ToInt64(),Convert.ToDouble()，Convert.ToString()**
**和.net 相同**

-----【if】-----
if ($a -eq $true) #表达式返回真 { }

#单if
if () { }

#if-else
if ( ) { }
else { }



#**多个if条件**
if () { }
elseif () {} 
elseif () {}。。。
else { }

推荐这种写法：简称if空
if (返回真) {}
elseif () {}
else { 非主要脚本代码，作用是报错，退出，一般比较短 }
**脚本主要代码段**
#没有shell的：**if条件then空else不行的问题**。

不推荐这种写法：
if (返回真) {脚本主要代码段}
elseif () {}
else {非主要脚本代码，作用是报错，退出，一般比较短}


这样写脚本的目的：
非主要脚本代码，作用是报错，退出，一般比较短。
快速闭合if，else。
快速看到，报错退出分支。
让【脚本主要代码】不要在多层if，else内。
让很长的【脚本主要代码】，总是【在代码文件】下面，
而不是让【报错，退出，一般比较短。】的代码，在下面。





switch ($a)
{
	1 {命令1 ;命令2;break}
	2 {命令3 ;命令4;break}
	3 {命令5 ;命令6;break}
	default { 命令7 }
}

-----【while】-----
while ()
{}


do
{}
while ()

-----【for-foreach】-----
https://docs.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_for?view=powershell-7.2
for ( 初始化变量; 条件为真;执行完代码块后，改变初始变量)
{
	则执行代码块
}
#**for行，没有shell的【空格】分行问题**。

for ($i=1;$i -lt 100;$i++)
{}

for ($i=200;$i -gt 111;$i--)
{}

foreach ($单个元素 in $数组)
{}



-----【哈希表】-----
请看powershell的哈希表：

$powershell哈希表 = @{
吼 = 'haha1'
哈 = 'haha2'
嘿 = '完全可以使用中文键名，键值哦'
}

$键名数组 = $powershell哈希表.Keys.GetEnumerator()
#$键名数组 返回---> 吼,哈,嘿

$键值数组 = $powershell哈希表.values.GetEnumerator()
#$键值数组
#$powershell哈希表.吼    返回--->   haha1

$键名数组 | Get-Random    #随机返回1个值




---【哈希嵌套】---

$麻将牌 = @{
'万'  = @{w=1}
'饼'  = @{b=2}
'条'  = @{t=3}
'字'  = @{z=4}


}

$麻将牌
$麻将牌.万
$麻将牌.万.w

另一种访问哈希表方法：
$麻将牌['万']
$麻将牌['万']['w']



传教士点评：
哈希的儿子，可以是哈希，（哈希表包含哈希表）
哈希的儿子，可以是数组，
数组的儿子，可以是哈希，
子子孙孙无穷匮也！

-----【foreach-object】-----
问：如何拆分管道元素？
答：
1..10 | foreach-object { 你的命令 $_ }
这类似于xargs


问：如何组合管道元素？
答：
1..10 | sort-object
一般来讲不用手动组合

问：如何手动组合管道元素？
答：
**==用过滤器==**

```powershell
filter a
{
	begin
	{
		"开始执行a"
		$数组 = @()
	}
	process
	{
	$数组 += $_
	}

	end
	{
	"结束执行a，输出组合出的数组"
	$数组 
	}
}
```




## 01 Shell 命令别名Alias

----



> **Get-Command -CommandType Alias** 
>
> 上述命令 显示 Shell 命令 含有别名的 ，与文件系统交互 、运行应用程序的部分 



### 显示别名列表 Get-Alias

Get-Alias 的别名的 gal

```powershell
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           Add-AppPackage                                     2.0.1.0    Appx
Alias           Add-AppPackageVolume                               2.0.1.0    Appx
Alias           Add-AppProvisionedPackage                          3.0        Dism
Alias           Add-ProvisionedAppPackage                          3.0        Dism
Alias           Add-ProvisionedAppxPackage                         3.0        Dism
Alias           Add-ProvisioningPackage                            3.0        Provisioning
Alias           Add-TrustedProvisioningCertificate                 3.0        Provisioning
Alias           algm ->                                            1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           Apply-WindowsUnattend                              3.0        Dism
Alias           asnp -> Add-PSSnapin
Alias           Begin-WebCommitDelay                               1.0.0.0    WebAdministration
Alias           blsmba ->                                          2.0.0.0    SmbShare
Alias           cat -> Get-Content
Alias           cd -> Set-Location			# 进入文件夹内部 ，可前进，可后退
# cd  默认 进入 当前文件件；cd .. 返回上文件夹 
Alias           CFS -> ConvertFrom-String                          3.1.0.0    Microsoft.PowerShell.Utility
Alias           chdir -> Set-Location
Alias           clc -> Clear-Content
Alias           clear -> Clear-Host
Alias           clhy -> Clear-History
Alias           cli -> Clear-Item
Alias           clp -> Clear-ItemProperty
Alias           cls -> Clear-Host
Alias           clv -> Clear-Variable
Alias           cmpcfg ->                                          1.1        PSDesiredStateConfiguration
Alias           cnsn -> Connect-PSSession
Alias           compare -> Compare-Object
Alias           copy -> Copy-Item
Alias           cp -> Copy-Item
Alias           cpi -> Copy-Item
Alias           cpp -> Copy-ItemProperty
Alias           cssmbo ->                                          2.0.0.0    SmbShare
Alias           cssmbse ->                                         2.0.0.0    SmbShare
Alias           curl -> Invoke-WebRequest
Alias           cvpa -> Convert-Path
Alias           dbp -> Disable-PSBreakpoint
Alias           del -> Remove-Item
Alias           diff -> Compare-Object
Alias           dir -> Get-ChildItem		#当前文件夹下的子文件夹和文件信息
Alias           Disable-PhysicalDiskIndication                     2.0.0.0    Storage
Alias           Disable-StorageDiagnosticLog                       2.0.0.0    Storage
Alias           Dismount-AppPackageVolume                          2.0.1.0    Appx
Alias           dlu ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           dnsn -> Disconnect-PSSession
Alias           dsmbd ->                                           2.0.0.0    SmbShare
Alias           ebp -> Enable-PSBreakpoint
Alias           echo -> Write-Output		# 输出 后面的字符串
Alias           elu ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           Enable-PhysicalDiskIndication                      2.0.0.0    Storage
Alias           Enable-StorageDiagnosticLog                        2.0.0.0    Storage
Alias           End-WebCommitDelay                                 1.0.0.0    WebAdministration
Alias           epal -> Export-Alias
Alias           epcsv -> Export-Csv
Alias           epsn -> Export-PSSession
Alias           erase -> Remove-Item
Alias           esmbd ->                                           2.0.0.0    SmbShare
Alias           etsn -> Enter-PSSession
Alias           exsn -> Exit-PSSession
Alias           fc -> Format-Custom
Alias           fhx -> Format-Hex                                  3.1.0.0    Microsoft.PowerShell.Utility
Alias           fimo ->                                            1.0.0.1    PowerShellGet
Alias           fl -> Format-List
Alias           Flush-Volume                                       2.0.0.0    Storage
Alias           foreach -> ForEach-Object
Alias           ft -> Format-Table
Alias           fw -> Format-Wide
Alias           gal -> Get-Alias
Alias           gbp -> Get-PSBreakpoint
Alias           gc -> Get-Content
Alias           gcai ->                                            1.0.0.0    CimCmdlets
Alias           gcb -> Get-Clipboard                               3.1.0.0    Microsoft.PowerShell.Management
Alias           gcfg ->                                            1.1        PSDesiredStateConfiguration
Alias           gcfgs ->                                           1.1        PSDesiredStateConfiguration
Alias           gci -> Get-ChildItem
Alias           gcim ->                                            1.0.0.0    CimCmdlets
Alias           gcls ->                                            1.0.0.0    CimCmdlets
Alias           gcm -> Get-Command
Alias           gcms ->                                            1.0.0.0    CimCmdlets
Alias           gcs -> Get-PSCallStack
Alias           gdr -> Get-PSDrive
Alias           Get-AppPackage                                     2.0.1.0    Appx
Alias           Get-AppPackageDefaultVolume                        2.0.1.0    Appx
Alias           Get-AppPackageLastError                            2.0.1.0    Appx
Alias           Get-AppPackageLog                                  2.0.1.0    Appx
Alias           Get-AppPackageManifest                             2.0.1.0    Appx
Alias           Get-AppPackageVolume                               2.0.1.0    Appx
Alias           Get-AppProvisionedPackage                          3.0        Dism
Alias           Get-DiskSNV                                        2.0.0.0    Storage
Alias           Get-Language                                       1.0        LanguagePackManagement
Alias           Get-PhysicalDiskSNV                                2.0.0.0    Storage
Alias           Get-PreferredLanguage                              1.0        LanguagePackManagement
Alias           Get-ProvisionedAppPackage                          3.0        Dism
Alias           Get-ProvisionedAppxPackage                         3.0        Dism
Alias           Get-StorageEnclosureSNV                            2.0.0.0    Storage
Alias           Get-SystemLanguage                                 1.0        LanguagePackManagement
Alias           ghy -> Get-History
Alias           gi -> Get-Item
Alias           gin -> Get-ComputerInfo                            3.1.0.0    Microsoft.PowerShell.Management
Alias           gip ->                                             1.0.0.0    NetTCPIP
Alias           gjb -> Get-Job
Alias           gl -> Get-Location
Alias           glcm ->                                            1.1        PSDesiredStateConfiguration
Alias           glg ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           glgm ->                                            1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           glu ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           gm -> Get-Member
Alias           gmo -> Get-Module
Alias           gp -> Get-ItemProperty
Alias           gps -> Get-Process
Alias           gpv -> Get-ItemPropertyValue
Alias           group -> Group-Object
Alias           grsmba ->                                          2.0.0.0    SmbShare
Alias           gsmba ->                                           2.0.0.0    SmbShare
Alias           gsmbb ->                                           2.0.0.0    SmbShare
Alias           gsmbc ->                                           2.0.0.0    SmbShare
Alias           gsmbcc ->                                          2.0.0.0    SmbShare
Alias           gsmbcn ->                                          2.0.0.0    SmbShare
Alias           gsmbd ->                                           2.0.0.0    SmbShare
Alias           gsmbgm ->                                          2.0.0.0    SmbShare
Alias           gsmbm ->                                           2.0.0.0    SmbShare
Alias           gsmbmc ->                                          2.0.0.0    SmbShare
Alias           gsmbo ->                                           2.0.0.0    SmbShare
Alias           gsmbs ->                                           2.0.0.0    SmbShare
Alias           gsmbsc ->                                          2.0.0.0    SmbShare
Alias           gsmbscm ->                                         2.0.0.0    SmbShare
Alias           gsmbse ->                                          2.0.0.0    SmbShare
Alias           gsmbsn ->                                          2.0.0.0    SmbShare
Alias           gsmbt ->                                           2.0.0.0    SmbShare
Alias           gsmbw ->                                           2.0.0.0    SmbWitness
Alias           gsn -> Get-PSSession
Alias           gsnp -> Get-PSSnapin
Alias           gsv -> Get-Service
Alias           gtz -> Get-TimeZone                                3.1.0.0    Microsoft.PowerShell.Management
Alias           gu -> Get-Unique
Alias           gv -> Get-Variable
Alias           gwmi -> Get-WmiObject
Alias           h -> Get-History
Alias           history -> Get-History
Alias           icim ->                                            1.0.0.0    CimCmdlets
Alias           icm -> Invoke-Command
Alias           iex -> Invoke-Expression
Alias           ihy -> Invoke-History
Alias           ii -> Invoke-Item
Alias           Initialize-Volume                                  2.0.0.0    Storage
Alias           inmo ->                                            1.0.0.1    PowerShellGet
Alias           ipal -> Import-Alias
Alias           ipcsv -> Import-Csv
Alias           ipmo -> Import-Module
Alias           ipsn -> Import-PSSession
Alias           irm -> Invoke-RestMethod
Alias           iru ->                                             1.0.0.0    AppBackgroundTask
Alias           ise -> powershell_ise.exe
Alias           iwmi -> Invoke-WmiMethod
Alias           iwr -> Invoke-WebRequest
Alias           kill -> Stop-Process
Alias           lp -> Out-Printer
Alias           ls -> Get-ChildItem
Alias           man -> help
Alias           md -> mkdir
Alias           measure -> Measure-Object
Alias           mi -> Move-Item
Alias           mount -> New-PSDrive
Alias           Mount-AppPackageVolume                             2.0.1.0    Appx
Alias           move -> Move-Item
Alias           Move-AppPackage                                    2.0.1.0    Appx
Alias           Move-SmbClient                                     2.0.0.0    SmbWitness
Alias           mp -> Move-ItemProperty
Alias           msmbw ->                                           2.0.0.0    SmbWitness
Alias           mv -> Move-Item
Alias           nal -> New-Alias
Alias           ncim ->                                            1.0.0.0    CimCmdlets
Alias           ncms ->                                            1.0.0.0    CimCmdlets
Alias           ncso ->                                            1.0.0.0    CimCmdlets
Alias           ndr -> New-PSDrive
Alias           ni -> New-Item
Alias           nlg ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           nlu ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           nmo -> New-Module
Alias           npssc -> New-PSSessionConfigurationFile
Alias           nsmbgm ->                                          2.0.0.0    SmbShare
Alias           nsmbm ->                                           2.0.0.0    SmbShare
Alias           nsmbs ->                                           2.0.0.0    SmbShare
Alias           nsmbscm ->                                         2.0.0.0    SmbShare
Alias           nsmbt ->                                           2.0.0.0    SmbShare
Alias           nsn -> New-PSSession
Alias           nv -> New-Variable
Alias           nwsn ->                                            2.0.0.0    PSWorkflow
Alias           ogv -> Out-GridView
Alias           oh -> Out-Host
Alias           Optimize-AppProvisionedPackages                    3.0        Dism
Alias           Optimize-ProvisionedAppPackages                    3.0        Dism
Alias           Optimize-ProvisionedAppxPackages                   3.0        Dism
Alias           pbcfg ->                                           1.1        PSDesiredStateConfiguration
Alias           pfn ->                                             1.0.0.0    AppBackgroundTask
Alias           popd -> Pop-Location
Alias           ps -> Get-Process
Alias           pumo ->                                            1.0.0.1    PowerShellGet
Alias           pushd -> Push-Location
Alias           pwd -> Get-Location
Alias           r -> Invoke-History
Alias           rbp -> Remove-PSBreakpoint
Alias           rcie ->                                            1.0.0.0    CimCmdlets
Alias           rcim ->                                            1.0.0.0    CimCmdlets
Alias           rcjb -> Receive-Job
Alias           rcms ->                                            1.0.0.0    CimCmdlets
Alias           rcsn -> Receive-PSSession
Alias           rd -> Remove-Item
Alias           rdr -> Remove-PSDrive
Alias           Remove-AppPackage                                  2.0.1.0    Appx
Alias           Remove-AppPackageVolume                            2.0.1.0    Appx
Alias           Remove-AppProvisionedPackage                       3.0        Dism
Alias           Remove-EtwTraceSession                             1.0.0.0    EventTracingManagement
Alias           Remove-ProvisionedAppPackage                       3.0        Dism
Alias           Remove-ProvisionedAppxPackage                      3.0        Dism
Alias           Remove-ProvisioningPackage                         3.0        Provisioning
Alias           Remove-TrustedProvisioningCertificate              3.0        Provisioning
Alias           ren -> Rename-Item
Alias           ri -> Remove-Item
Alias           rjb -> Remove-Job
Alias           rksmba ->                                          2.0.0.0    SmbShare
Alias           rlg ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           rlgm ->                                            1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           rlu ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           rm -> Remove-Item
Alias           rmdir -> Remove-Item
Alias           rmo -> Remove-Module
Alias           rni -> Rename-Item
Alias           rnlg ->                                            1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           rnlu ->                                            1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           rnp -> Rename-ItemProperty
Alias           rp -> Remove-ItemProperty
Alias           rsmbb ->                                           2.0.0.0    SmbShare
Alias           rsmbc ->                                           2.0.0.0    SmbShare
Alias           rsmbgm ->                                          2.0.0.0    SmbShare
Alias           rsmbm ->                                           2.0.0.0    SmbShare
Alias           rsmbs ->                                           2.0.0.0    SmbShare
Alias           rsmbscm ->                                         2.0.0.0    SmbShare
Alias           rsmbt ->                                           2.0.0.0    SmbShare
Alias           rsn -> Remove-PSSession
Alias           rsnp -> Remove-PSSnapin
Alias           rtcfg ->                                           1.1        PSDesiredStateConfiguration
Alias           rujb -> Resume-Job
Alias           rv -> Remove-Variable
Alias           rvpa -> Resolve-Path
Alias           rwmi -> Remove-WmiObject
Alias           sacfg ->                                           1.1        PSDesiredStateConfiguration
Alias           sajb -> Start-Job
Alias           sal -> Set-Alias
Alias           saps -> Start-Process
Alias           sasv -> Start-Service
Alias           sbp -> Set-PSBreakpoint
Alias           sc -> Set-Content
Alias           scb -> Set-Clipboard                               3.1.0.0    Microsoft.PowerShell.Management
Alias           scim ->                                            1.0.0.0    CimCmdlets
Alias           select -> Select-Object
Alias           set -> Set-Variable
Alias           Set-AppPackageDefaultVolume                        2.0.1.0    Appx
Alias           Set-AppPackageProvisionedDataFile                  3.0        Dism
Alias           Set-AutologgerConfig                               1.0.0.0    EventTracingManagement
Alias           Set-EtwTraceSession                                1.0.0.0    EventTracingManagement
Alias           Set-PreferredLanguage                              1.0        LanguagePackManagement
Alias           Set-ProvisionedAppPackageDataFile                  3.0        Dism
Alias           Set-ProvisionedAppXDataFile                        3.0        Dism
Alias           Set-SystemLanguage                                 1.0        LanguagePackManagement
Alias           shcm -> Show-Command
Alias           si -> Set-Item
Alias           sl -> Set-Location
Alias           slcm ->                                            1.1        PSDesiredStateConfiguration
Alias           sleep -> Start-Sleep
Alias           slg ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           sls -> Select-String
Alias           slu ->                                             1.0.0.0    Microsoft.PowerShell.LocalAccounts
Alias           sort -> Sort-Object
Alias           sp -> Set-ItemProperty
Alias           spjb -> Stop-Job
Alias           spps -> Stop-Process
Alias           spsv -> Stop-Service
Alias           ssmbb ->                                           2.0.0.0    SmbShare
Alias           ssmbcc ->                                          2.0.0.0    SmbShare
Alias           ssmbp ->                                           2.0.0.0    SmbShare
Alias           ssmbs ->                                           2.0.0.0    SmbShare
Alias           ssmbsc ->                                          2.0.0.0    SmbShare
Alias           start -> Start-Process
Alias           stz -> Set-TimeZone                                3.1.0.0    Microsoft.PowerShell.Management
Alias           sujb -> Suspend-Job
Alias           sv -> Set-Variable
Alias           swmi -> Set-WmiInstance
Alias           tcfg ->                                            1.1        PSDesiredStateConfiguration
Alias           tee -> Tee-Object
Alias           tid ->                                             1.0.0.0    AppBackgroundTask
Alias           TNC ->                                             1.0.0.0    NetTCPIP
Alias           trcm -> Trace-Command
Alias           type -> Get-Content
Alias           udsmbmc ->                                         2.0.0.0    SmbShare
Alias           ulsmba ->                                          2.0.0.0    SmbShare
Alias           upcfg ->                                           1.1        PSDesiredStateConfiguration
Alias           upmo ->                                            1.0.0.1    PowerShellGet
Alias           wget -> Invoke-WebRequest
Alias           where -> Where-Object
Alias           wjb -> Wait-Job
Alias           write -> Write-Output
Alias           Write-FileSystemCache                              2.0.0.0    Storage
```

### 查看某个命令的别名

```powershell
Get-Alias -Definition Get-Process
```

就可以查看 ps、gps都是它的别名

 ### cd  => Set-Location

```powershell
dir -> Get-ChildItem
cd C:\ # 切换到 C:\
cd		#进入下一文件夹内部
cd ..	#返回上一级文件夹
cd ~ # 返回到根目录
```

### cls => Clear-Host

----

清屏操作





### cat、type => Get-Content

----

查看文件内容



### copy、cp => Copy-Item

----



### dir、ls => Get-ChildItem

都是对Get-ChildItem的别名

获取当前文件夹下的目录

### fl => Format-List

----

显示对象的属性值 

这里要重点区分  format-list  和 get-member的区别 



### Format-List、Format-Table、Format-Wide

----

![image-20221208105910122](PowerShell%206.0.assets/image-20221208105910122.png)



![image-20221208110000054](PowerShell%206.0.assets/image-20221208110000054.png)

![image-20221208110042840](PowerShell%206.0.assets/image-20221208110042840.png)



![image-20221208110121078](PowerShell%206.0.assets/image-20221208110121078.png)

### foreach、% => ForEach-Object

----

**处理列表 或者  命令输出的每一个项目**

处理列表中每一项还可以用for、foreach、do和while等

![image-20221208095509102](PowerShell%206.0.assets/image-20221208095509102.png)



### start

```powerShell
start chrome -WindowStyle Maximized 		#启动Chrome浏览器，以最大化窗口启动
```

Get-Command -CommandType  Function	#获取当前会话中的函数
Get-Command -CommandType Script		#显示PowerShell搜索路径中的脚本



### help 、man=>Get-Help

----

```powershell
Help Get-EventLog -full
Help Get-EventLog -ShowWindow    # 在非Windows操作系统无法使用
Help Get-EventLog -example # 查看示例
Help Get-EventLog -Online # 每天 输入一个 命令 ，跳转到 MSDN在线查看和学习
```



### gc =>Get-Content

```powershell
# 查看文件保存的内容
```

### gcm => Get-Command

----

> help 命令搜索的是 帮助主题 
>
> 每个cmdlet都有一个帮助文件，
>
> gcm 搜索cmdlet命令  和help一样，都接受通配符*  ，
>
> 使用技巧 ： 使用-动词，-名词 canshu  ,返回结果限制为cmdlet命令（因为cmdlet名称有名词和动词）

```powershell
Get-Command -noun *event*   # 返回关于事件命令的列表
Get-Command -Verb Get		# 返回具有检索能力的列表 
Get-Command *log* -type Cmdlet # 返回所有命令包含log 的命令列表，且 不会包含任何其他扩展应用程序或扩展命令
Get-Command Get-EventLog -ShowCommandInfo 		#强烈推荐使用，查看 一个命令最核心的 部分 
```



### gps =>Get-Process

---

```powershell
Start-Process "$PSHOME\powershell.exe" -Verb runas  #以管理员方式打开Posershell程序
```



### group => Group-Object 

----

对列表项 或输出结果进行分组 

指定的属性包含相同值的组对象。Group-Object 返回一个表，其中每个属性值对应一行，同时一个列显示具有该值的项目数

![image-20221208113036340](PowerShell%206.0.assets/image-20221208113036340.png)



可以让返回的对象是个HashTable——key-value的键值对数组，指定-AsHashTable参数：

![image-20221208113417299](PowerShell%206.0.assets/image-20221208113417299.png)



![image-20221208113533221](PowerShell%206.0.assets/image-20221208113533221.png)





###  ipmo -> Import-Module

```powershell
import-Module .\DiskInfo.psm1
import-Module .\DiskInfo.psm1 -Force -Verbose
```

不想每次都导入 

查看 路径 

```powershell
cat Env:\PSModulePath
$env:PSModulePath -split ";"
```

![image-20221209104707182](PowerShell%206.0.assets/image-20221209104707182.png)

后面2个 是微软专用的文件夹，不可以将自己编写的放到里面；

第一个文件夹不存在，需要自己建立，建立PSM1文件夹，里面存放文件PSM1



### md mkdir =>

---

创建文件夹 ·





### measure => Measure-Object 

---

对列表项或者输出结果进行计算

使用Measure-Object（measure）计算对象的数字属性以及字符串对象（如文本文件）中的字符数、单词数和行数。它计算某些类型对象的属性值。Measure-Object 执行三种类型测量，具体取决于命令中的参数。可以对对象计数并计算数字值的最小值、最大值、总和及平均值。对于文本对象，它可以计数并计算行数、单词数和字符数

![image-20221208111902300](PowerShell%206.0.assets/image-20221208111902300.png)

![image-20221208112126648](PowerShell%206.0.assets/image-20221208112126648.png)



![image-20221208112152310](PowerShell%206.0.assets/image-20221208112152310.png)

![image-20221208112727433](PowerShell%206.0.assets/image-20221208112727433.png)







### where、？ => Where-Object

----

**过滤列表项或命令输出结果**



列表或者命令输出结果中过滤选择你需要的项目

对于输入的每一项，Where-Object都会根据{}中定义的**脚本块对输入进行计算**，**如果返回True，则输出**，否则不输出

![image-20221208094603293](PowerShell%206.0.assets/image-20221208094603293.png)

{}表示一个脚本块，可以输入一系列PowerShell命令，其中**$_代表当前输入对象**，在这个例子中，$_就代表一个文件项目。-gt是比较操作符，意思是大于，关于比较操作符的介绍如下

![image-20221208094258417](PowerShell%206.0.assets/image-20221208094258417.png)

PowerShell中比较操作符是用于对表达式进行比较的。默认情况比较操作符**不区分大小写**，如果想要**区分，需要使用-C前缀**，不需要区分的，使用-I前缀



![image-20221208094822014](PowerShell%206.0.assets/image-20221208094822014.png)













### select => Select-Object

---

> 选择列表项 或者 输出结果 只输出想要的结果

使用Select-Object（别名是select）对象可以**选择一个对象**或者**一组对象的指定属性**。还可以从对象的数组中选择唯一的对象，也可以从对象数组的开头或末尾选择指定个数的对象。

如果使用 Select-Object 来**选择指定属性**，则它会从输入对象中**复制**这些属性的值，并创建具有指定的属性和复制的值的新对象。使用 **Property** 参数指定您要选择的属性。或者，使用 First、Last、Unique、Skip 和 Index **参数**从输入对象数组中**选择特定对象**

![image-20221208100135274](PowerShell%206.0.assets/image-20221208100135274.png)

![image-20221208100252858](PowerShell%206.0.assets/image-20221208100252858.png)



![image-20221208100712432](PowerShell%206.0.assets/image-20221208100712432.png)

![image-20221208100901885](PowerShell%206.0.assets/image-20221208100901885.png)

![image-20221208101122594](PowerShell%206.0.assets/image-20221208101122594.png)

![image-20221208101220979](PowerShell%206.0.assets/image-20221208101220979.png)





![image-20221208101347983](PowerShell%206.0.assets/image-20221208101347983.png)





### shcm =>Show-Command

----

![image-20221213092637422](PowerShell%206.0.assets/image-20221213092637422.png)



![image-20221213092730854](PowerShell%206.0.assets/image-20221213092730854.png)







### sort => Sort-Object

---

 对列表项或者输出结果进行排序

可以按照特定属性值对对象进行排序。您可以指定一个属性或多个属性（用于多键排序），也可以选择区分大小写或不区分大小写的排序。您还可以指示 Sort-Object 只显示对于特定属性具有唯一值的对象。

如果某个对象不具有所指定的属性之一，则 cmdlet 会将该对象的属性值解释为 NULL，并将其放置在排序顺序的末尾。

![image-20221208101731224](PowerShell%206.0.assets/image-20221208101731224.png)



![image-20221208101900294](PowerShell%206.0.assets/image-20221208101900294.png)

![image-20221208102012391](PowerShell%206.0.assets/image-20221208102012391.png)

















### tee => Tee-Object

---

保存并输出列表项 或者输出结果

将 命令输出结果保存在文件或者变量中， 同时将其显示在控制台中 

![image-20221208102426805](PowerShell%206.0.assets/image-20221208102426805.png)

![image-20221208102511003](PowerShell%206.0.assets/image-20221208102511003.png)

![image-20221208102633193](PowerShell%206.0.assets/image-20221208102633193.png)



![image-20221208102934359](PowerShell%206.0.assets/image-20221208102934359.png)

![image-20221208102948479](PowerShell%206.0.assets/image-20221208102948479.png)



### Out-File

![image-20221208104536141](PowerShell%206.0.assets/image-20221208104536141.png)



### epcsv => Export-Csv 

---

 将对象转化为 CSV字符串存储到文件中 

用Export-Csv（别名是epcsv）将 Microsoft .NET Framework 对象转换为一系列以逗号分隔的、长度可变的 (CSV) 字符串，并将这些字符串保存到一个 CSV 文件中

![image-20221208105412772](PowerShell%206.0.assets/image-20221208105412772.png)



### ConvertTo-Html 

---

 将对象转化为HTML

用ConvertTo-Html可以将Microsoft.Net Framework对象转换为可在Web浏览器中显示的HTML

![image-20221208110320001](PowerShell%206.0.assets/image-20221208110320001.png)







### gm =>Get-Member

----

用法：查找存储在对象属性中的对象的类型![image-20221208103903446](PowerShell%206.0.assets/image-20221208103903446.png)





![image-20221208103936577](PowerShell%206.0.assets/image-20221208103936577.png)





### gu=> Get-Unique

---

 获取 输出结果的唯一值

![image-20221208104826324](PowerShell%206.0.assets/image-20221208104826324.png)



### compare 、diff => Compare-Object

用Compare-Object（别名是compare和diff）可以将两组对象进行比较，一组对象为Reference组，而另一组为Difference组。比较的结果将指示属性值是只出现在 Reference 组中的对象中（由 <= 符号指示），或是只出现在 Difference 组中的对象中（由 => 符号指示），抑或（在指定了 IncludeEqual 参数的情况下）同时出现在这两个对象中（由 == 符号指示）



![image-20221208111532479](PowerShell%206.0.assets/image-20221208111532479.png)

## 02Shell函数 Function

> Get-Command -CommandType  Function	#获取当前会话中的函数
>
> 函数 基本上就是见名知意



```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        A:
Function        Add-BitLockerKeyProtector                          1.0.0.0    BitLocker
Function        Add-DnsClientNrptRule                              1.0.0.0    DnsClient
Function        Add-DtcClusterTMMapping                            1.0.0.0    MsDtc
Function        Add-EtwTraceProvider                               1.0.0.0    EventTracingManagement
Function        Add-InitiatorIdToMaskingSet                        2.0.0.0    Storage
Function        Add-MpPreference                                   1.0        ConfigDefender
Function        Add-MpPreference                                   1.0        Defender
Function        Add-NetEventNetworkAdapter                         1.0.0.0    NetEventPacketCapture
Function        Add-NetEventPacketCaptureProvider                  1.0.0.0    NetEventPacketCapture
Function        Add-NetEventProvider                               1.0.0.0    NetEventPacketCapture
Function        Add-NetEventVFPProvider                            1.0.0.0    NetEventPacketCapture
Function        Add-NetEventVmNetworkAdapter                       1.0.0.0    NetEventPacketCapture
Function        Add-NetEventVmSwitch                               1.0.0.0    NetEventPacketCapture
Function        Add-NetEventVmSwitchProvider                       1.0.0.0    NetEventPacketCapture
Function        Add-NetEventWFPCaptureProvider                     1.0.0.0    NetEventPacketCapture
Function        Add-NetIPHttpsCertBinding                          1.0.0.0    NetworkTransition
Function        Add-NetLbfoTeamMember                              2.0.0.0    NetLbfo
Function        Add-NetLbfoTeamNic                                 2.0.0.0    NetLbfo
Function        Add-NetNatExternalAddress                          1.0.0.0    NetNat
Function        Add-NetNatStaticMapping                            1.0.0.0    NetNat
Function        Add-NetSwitchTeamMember                            1.0.0.0    NetSwitchTeam
Function        Add-OdbcDsn                                        1.0.0.0    Wdac
Function        Add-PartitionAccessPath                            2.0.0.0    Storage
Function        Add-PhysicalDisk                                   2.0.0.0    Storage
Function        Add-Printer                                        1.1        PrintManagement
Function        Add-PrinterDriver                                  1.1        PrintManagement
Function        Add-PrinterPort                                    1.1        PrintManagement
Function        Add-StorageFaultDomain                             2.0.0.0    Storage
Function        Add-TargetPortToMaskingSet                         2.0.0.0    Storage
Function        Add-VirtualDiskToMaskingSet                        2.0.0.0    Storage
Function        Add-VpnConnection                                  2.0.0.0    VpnClient
Function        Add-VpnConnectionRoute                             2.0.0.0    VpnClient
Function        Add-VpnConnectionTriggerApplication                2.0.0.0    VpnClient
Function        Add-VpnConnectionTriggerDnsConfiguration           2.0.0.0    VpnClient
Function        Add-VpnConnectionTriggerTrustedNetwork             2.0.0.0    VpnClient
Function        AfterAll                                           3.4.0      Pester
Function        AfterEach                                          3.4.0      Pester
Function        Assert-MockCalled                                  3.4.0      Pester
Function        Assert-VerifiableMocks                             3.4.0      Pester
Function        B:
Function        Backup-BitLockerKeyProtector                       1.0.0.0    BitLocker
Function        BackupToAAD-BitLockerKeyProtector                  1.0.0.0    BitLocker
Function        BeforeAll                                          3.4.0      Pester
Function        BeforeEach                                         3.4.0      Pester
Function        Block-FileShareAccess                              2.0.0.0    Storage
Function        Block-SmbShareAccess                               2.0.0.0    SmbShare
Function        C:
Function        cd..
Function        cd\
Function        Clear-BitLockerAutoUnlock                          1.0.0.0    BitLocker
Function        Clear-Disk                                         2.0.0.0    Storage
Function        Clear-DnsClientCache                               1.0.0.0    DnsClient
Function        Clear-FileStorageTier                              2.0.0.0    Storage
Function        Clear-Host
Function        Clear-PcsvDeviceLog                                1.0.0.0    PcsvDevice
Function        Clear-StorageBusDisk                               1.0.0.0    StorageBusCache
Function        Clear-StorageDiagnosticInfo                        2.0.0.0    Storage
Function        Close-SmbOpenFile                                  2.0.0.0    SmbShare
Function        Close-SmbSession                                   2.0.0.0    SmbShare
Function        Compress-Archive                                   1.0.1.0    Microsoft.PowerShell.Archive
Function        Configuration                                      1.1        PSDesiredStateConfiguration
Function        Connect-IscsiTarget                                1.0.0.0    iSCSI
Function        Connect-VirtualDisk                                2.0.0.0    Storage
Function        Context                                            3.4.0      Pester
Function        ConvertFrom-SddlString                             3.1.0.0    Microsoft.PowerShell.Utility
Function        Copy-NetFirewallRule                               2.0.0.0    NetSecurity
Function        Copy-NetIPsecMainModeCryptoSet                     2.0.0.0    NetSecurity
Function        Copy-NetIPsecMainModeRule                          2.0.0.0    NetSecurity
Function        Copy-NetIPsecPhase1AuthSet                         2.0.0.0    NetSecurity
Function        Copy-NetIPsecPhase2AuthSet                         2.0.0.0    NetSecurity
Function        Copy-NetIPsecQuickModeCryptoSet                    2.0.0.0    NetSecurity
Function        Copy-NetIPsecRule                                  2.0.0.0    NetSecurity
Function        D:
Function        Debug-FileShare                                    2.0.0.0    Storage
Function        Debug-MMAppPrelaunch                               1.0        MMAgent
Function        Debug-StorageSubSystem                             2.0.0.0    Storage
Function        Debug-Volume                                       2.0.0.0    Storage
Function        Describe                                           3.4.0      Pester
Function        Disable-BitLocker                                  1.0.0.0    BitLocker
Function        Disable-BitLockerAutoUnlock                        1.0.0.0    BitLocker
Function        Disable-DAManualEntryPointSelection                1.0.0.0    DirectAccessClientComponents
Function        Disable-DeliveryOptimizationVerboseLogs            1.0.2.0    DeliveryOptimization
Function        Disable-DscDebug                                   1.1        PSDesiredStateConfiguration
Function        Disable-MMAgent                                    1.0        MMAgent
Function        Disable-NetAdapter                                 2.0.0.0    NetAdapter
Function        Disable-NetAdapterBinding                          2.0.0.0    NetAdapter
Function        Disable-NetAdapterChecksumOffload                  2.0.0.0    NetAdapter
Function        Disable-NetAdapterEncapsulatedPacketTaskOffload    2.0.0.0    NetAdapter
Function        Disable-NetAdapterIPsecOffload                     2.0.0.0    NetAdapter
Function        Disable-NetAdapterLso                              2.0.0.0    NetAdapter
Function        Disable-NetAdapterPacketDirect                     2.0.0.0    NetAdapter
Function        Disable-NetAdapterPowerManagement                  2.0.0.0    NetAdapter
Function        Disable-NetAdapterQos                              2.0.0.0    NetAdapter
Function        Disable-NetAdapterRdma                             2.0.0.0    NetAdapter
Function        Disable-NetAdapterRsc                              2.0.0.0    NetAdapter
Function        Disable-NetAdapterRss                              2.0.0.0    NetAdapter
Function        Disable-NetAdapterSriov                            2.0.0.0    NetAdapter
Function        Disable-NetAdapterUso                              2.0.0.0    NetAdapter
Function        Disable-NetAdapterVmq                              2.0.0.0    NetAdapter
Function        Disable-NetDnsTransitionConfiguration              1.0.0.0    NetworkTransition
Function        Disable-NetFirewallRule                            2.0.0.0    NetSecurity
Function        Disable-NetIPHttpsProfile                          1.0.0.0    NetworkTransition
Function        Disable-NetIPsecMainModeRule                       2.0.0.0    NetSecurity
Function        Disable-NetIPsecRule                               2.0.0.0    NetSecurity
Function        Disable-NetNatTransitionConfiguration              1.0.0.0    NetworkTransition
Function        Disable-NetworkSwitchEthernetPort                  1.0.0.0    NetworkSwitchManager
Function        Disable-NetworkSwitchFeature                       1.0.0.0    NetworkSwitchManager
Function        Disable-NetworkSwitchVlan                          1.0.0.0    NetworkSwitchManager
Function        Disable-OdbcPerfCounter                            1.0.0.0    Wdac
Function        Disable-PhysicalDiskIdentification                 2.0.0.0    Storage
Function        Disable-PnpDevice                                  1.0.0.0    PnpDevice
Function        Disable-PSTrace                                    1.0.0.0    PSDiagnostics
Function        Disable-PSWSManCombinedTrace                       1.0.0.0    PSDiagnostics
Function        Disable-ScheduledTask                              1.0.0.0    ScheduledTasks
Function        Disable-SmbDelegation                              2.0.0.0    SmbShare
Function        Disable-StorageBusCache                            1.0.0.0    StorageBusCache
Function        Disable-StorageBusDisk                             1.0.0.0    StorageBusCache
Function        Disable-StorageEnclosureIdentification             2.0.0.0    Storage
Function        Disable-StorageEnclosurePower                      2.0.0.0    Storage
Function        Disable-StorageHighAvailability                    2.0.0.0    Storage
Function        Disable-StorageMaintenanceMode                     2.0.0.0    Storage
Function        Disable-WdacBidTrace                               1.0.0.0    Wdac
Function        Disable-WSManTrace                                 1.0.0.0    PSDiagnostics
Function        Disconnect-IscsiTarget                             1.0.0.0    iSCSI
Function        Disconnect-VirtualDisk                             2.0.0.0    Storage
Function        Dismount-DiskImage                                 2.0.0.0    Storage
Function        E:
Function        Enable-BitLocker                                   1.0.0.0    BitLocker
Function        Enable-BitLockerAutoUnlock                         1.0.0.0    BitLocker
Function        Enable-DAManualEntryPointSelection                 1.0.0.0    DirectAccessClientComponents
Function        Enable-DeliveryOptimizationVerboseLogs             1.0.2.0    DeliveryOptimization
Function        Enable-DscDebug                                    1.1        PSDesiredStateConfiguration
Function        Enable-MMAgent                                     1.0        MMAgent
Function        Enable-NetAdapter                                  2.0.0.0    NetAdapter
Function        Enable-NetAdapterBinding                           2.0.0.0    NetAdapter
Function        Enable-NetAdapterChecksumOffload                   2.0.0.0    NetAdapter
Function        Enable-NetAdapterEncapsulatedPacketTaskOffload     2.0.0.0    NetAdapter
Function        Enable-NetAdapterIPsecOffload                      2.0.0.0    NetAdapter
Function        Enable-NetAdapterLso                               2.0.0.0    NetAdapter
Function        Enable-NetAdapterPacketDirect                      2.0.0.0    NetAdapter
Function        Enable-NetAdapterPowerManagement                   2.0.0.0    NetAdapter
Function        Enable-NetAdapterQos                               2.0.0.0    NetAdapter
Function        Enable-NetAdapterRdma                              2.0.0.0    NetAdapter
Function        Enable-NetAdapterRsc                               2.0.0.0    NetAdapter
Function        Enable-NetAdapterRss                               2.0.0.0    NetAdapter
Function        Enable-NetAdapterSriov                             2.0.0.0    NetAdapter
Function        Enable-NetAdapterUso                               2.0.0.0    NetAdapter
Function        Enable-NetAdapterVmq                               2.0.0.0    NetAdapter
Function        Enable-NetDnsTransitionConfiguration               1.0.0.0    NetworkTransition
Function        Enable-NetFirewallRule                             2.0.0.0    NetSecurity
Function        Enable-NetIPHttpsProfile                           1.0.0.0    NetworkTransition
Function        Enable-NetIPsecMainModeRule                        2.0.0.0    NetSecurity
Function        Enable-NetIPsecRule                                2.0.0.0    NetSecurity
Function        Enable-NetNatTransitionConfiguration               1.0.0.0    NetworkTransition
Function        Enable-NetworkSwitchEthernetPort                   1.0.0.0    NetworkSwitchManager
Function        Enable-NetworkSwitchFeature                        1.0.0.0    NetworkSwitchManager
Function        Enable-NetworkSwitchVlan                           1.0.0.0    NetworkSwitchManager
Function        Enable-OdbcPerfCounter                             1.0.0.0    Wdac
Function        Enable-PhysicalDiskIdentification                  2.0.0.0    Storage
Function        Enable-PnpDevice                                   1.0.0.0    PnpDevice
Function        Enable-PSTrace                                     1.0.0.0    PSDiagnostics
Function        Enable-PSWSManCombinedTrace                        1.0.0.0    PSDiagnostics
Function        Enable-ScheduledTask                               1.0.0.0    ScheduledTasks
Function        Enable-SmbDelegation                               2.0.0.0    SmbShare
Function        Enable-StorageBusCache                             1.0.0.0    StorageBusCache
Function        Enable-StorageBusDisk                              1.0.0.0    StorageBusCache
Function        Enable-StorageEnclosureIdentification              2.0.0.0    Storage
Function        Enable-StorageEnclosurePower                       2.0.0.0    Storage
Function        Enable-StorageHighAvailability                     2.0.0.0    Storage
Function        Enable-StorageMaintenanceMode                      2.0.0.0    Storage
Function        Enable-WdacBidTrace                                1.0.0.0    Wdac
Function        Enable-WSManTrace                                  1.0.0.0    PSDiagnostics
Function        Expand-Archive                                     1.0.1.0    Microsoft.PowerShell.Archive
Function        Export-ODataEndpointProxy                          1.0        Microsoft.PowerShell.ODataUtils
Function        Export-ScheduledTask                               1.0.0.0    ScheduledTasks
Function        F:
Function        Find-Command                                       1.0.0.1    PowerShellGet
Function        Find-DscResource                                   1.0.0.1    PowerShellGet
Function        Find-Module                                        1.0.0.1    PowerShellGet
Function        Find-NetIPsecRule                                  2.0.0.0    NetSecurity
Function        Find-NetRoute                                      1.0.0.0    NetTCPIP
Function        Find-RoleCapability                                1.0.0.1    PowerShellGet
Function        Find-Script                                        1.0.0.1    PowerShellGet
Function        Flush-EtwTraceSession                              1.0.0.0    EventTracingManagement
Function        Format-Hex                                         3.1.0.0    Microsoft.PowerShell.Utility
Function        Format-Volume                                      2.0.0.0    Storage
Function        G:
Function        Get-AppBackgroundTask                              1.0.0.0    AppBackgroundTask
Function        Get-AppxLastError                                  2.0.1.0    Appx
Function        Get-AppxLog                                        2.0.1.0    Appx
Function        Get-AutologgerConfig                               1.0.0.0    EventTracingManagement
Function        Get-BitLockerVolume                                1.0.0.0    BitLocker
Function        Get-ClusteredScheduledTask                         1.0.0.0    ScheduledTasks
Function        Get-DAClientExperienceConfiguration                1.0.0.0    DirectAccessClientComponents
Function        Get-DAConnectionStatus                             1.0.0.0    NetworkConnectivityStatus
Function        Get-DAEntryPointTableItem                          1.0.0.0    DirectAccessClientComponents
Function        Get-DedupProperties                                2.0.0.0    Storage
Function        Get-DeliveryOptimizationPerfSnap                   1.0.2.0    DeliveryOptimization
Function        Get-DeliveryOptimizationPerfSnapThisMonth          1.0.2.0    DeliveryOptimization
Function        Get-DeliveryOptimizationStatus                     1.0.2.0    DeliveryOptimization
Function        Get-Disk                                           2.0.0.0    Storage
Function        Get-DiskImage                                      2.0.0.0    Storage
Function        Get-DiskStorageNodeView                            2.0.0.0    Storage
Function        Get-DnsClient                                      1.0.0.0    DnsClient
Function        Get-DnsClientCache                                 1.0.0.0    DnsClient
Function        Get-DnsClientGlobalSetting                         1.0.0.0    DnsClient
Function        Get-DnsClientNrptGlobal                            1.0.0.0    DnsClient
Function        Get-DnsClientNrptPolicy                            1.0.0.0    DnsClient
Function        Get-DnsClientNrptRule                              1.0.0.0    DnsClient
Function        Get-DnsClientServerAddress                         1.0.0.0    DnsClient
Function        Get-DOConfig                                       1.0.2.0    DeliveryOptimization
Function        Get-DODownloadMode                                 1.0.2.0    DeliveryOptimization
Function        Get-DOPercentageMaxBackgroundBandwidth             1.0.2.0    DeliveryOptimization
Function        Get-DOPercentageMaxForegroundBandwidth             1.0.2.0    DeliveryOptimization
Function        Get-DscConfiguration                               1.1        PSDesiredStateConfiguration
Function        Get-DscConfigurationStatus                         1.1        PSDesiredStateConfiguration
Function        Get-DscLocalConfigurationManager                   1.1        PSDesiredStateConfiguration
Function        Get-DscResource                                    1.1        PSDesiredStateConfiguration
Function        Get-Dtc                                            1.0.0.0    MsDtc
Function        Get-DtcAdvancedHostSetting                         1.0.0.0    MsDtc
Function        Get-DtcAdvancedSetting                             1.0.0.0    MsDtc
Function        Get-DtcClusterDefault                              1.0.0.0    MsDtc
Function        Get-DtcClusterTMMapping                            1.0.0.0    MsDtc
Function        Get-DtcDefault                                     1.0.0.0    MsDtc
Function        Get-DtcLog                                         1.0.0.0    MsDtc
Function        Get-DtcNetworkSetting                              1.0.0.0    MsDtc
Function        Get-DtcTransaction                                 1.0.0.0    MsDtc
Function        Get-DtcTransactionsStatistics                      1.0.0.0    MsDtc
Function        Get-DtcTransactionsTraceSession                    1.0.0.0    MsDtc
Function        Get-DtcTransactionsTraceSetting                    1.0.0.0    MsDtc
Function        Get-EtwTraceProvider                               1.0.0.0    EventTracingManagement
Function        Get-EtwTraceSession                                1.0.0.0    EventTracingManagement
Function        Get-FileHash                                       3.1.0.0    Microsoft.PowerShell.Utility
Function        Get-FileIntegrity                                  2.0.0.0    Storage
Function        Get-FileShare                                      2.0.0.0    Storage
Function        Get-FileShareAccessControlEntry                    2.0.0.0    Storage
Function        Get-FileStorageTier                                2.0.0.0    Storage
Function        Get-InitiatorId                                    2.0.0.0    Storage
Function        Get-InitiatorPort                                  2.0.0.0    Storage
Function        Get-InstalledModule                                1.0.0.1    PowerShellGet
Function        Get-InstalledScript                                1.0.0.1    PowerShellGet
Function        Get-IscsiConnection                                1.0.0.0    iSCSI
Function        Get-IscsiSession                                   1.0.0.0    iSCSI
Function        Get-IscsiTarget                                    1.0.0.0    iSCSI
Function        Get-IscsiTargetPortal                              1.0.0.0    iSCSI
Function        Get-IseSnippet                                     1.0.0.0    ISE
Function        Get-LogProperties                                  1.0.0.0    PSDiagnostics
Function        Get-MaskingSet                                     2.0.0.0    Storage
Function        Get-MMAgent                                        1.0        MMAgent
Function        Get-MockDynamicParameters                          3.4.0      Pester
Function        Get-MpComputerStatus                               1.0        ConfigDefender
Function        Get-MpComputerStatus                               1.0        Defender
Function        Get-MpPreference                                   1.0        ConfigDefender
Function        Get-MpPreference                                   1.0        Defender
Function        Get-MpThreat                                       1.0        ConfigDefender
Function        Get-MpThreat                                       1.0        Defender
Function        Get-MpThreatCatalog                                1.0        ConfigDefender
Function        Get-MpThreatCatalog                                1.0        Defender
Function        Get-MpThreatDetection                              1.0        ConfigDefender
Function        Get-MpThreatDetection                              1.0        Defender
Function        Get-NCSIPolicyConfiguration                        1.0.0.0    NetworkConnectivityStatus
Function        Get-Net6to4Configuration                           1.0.0.0    NetworkTransition
Function        Get-NetAdapter                                     2.0.0.0    NetAdapter
Function        Get-NetAdapterAdvancedProperty                     2.0.0.0    NetAdapter
Function        Get-NetAdapterBinding                              2.0.0.0    NetAdapter
Function        Get-NetAdapterChecksumOffload                      2.0.0.0    NetAdapter
Function        Get-NetAdapterEncapsulatedPacketTaskOffload        2.0.0.0    NetAdapter
Function        Get-NetAdapterHardwareInfo                         2.0.0.0    NetAdapter
Function        Get-NetAdapterIPsecOffload                         2.0.0.0    NetAdapter
Function        Get-NetAdapterLso                                  2.0.0.0    NetAdapter
Function        Get-NetAdapterPacketDirect                         2.0.0.0    NetAdapter
Function        Get-NetAdapterPowerManagement                      2.0.0.0    NetAdapter
Function        Get-NetAdapterQos                                  2.0.0.0    NetAdapter
Function        Get-NetAdapterRdma                                 2.0.0.0    NetAdapter
Function        Get-NetAdapterRsc                                  2.0.0.0    NetAdapter
Function        Get-NetAdapterRss                                  2.0.0.0    NetAdapter
Function        Get-NetAdapterSriov                                2.0.0.0    NetAdapter
Function        Get-NetAdapterSriovVf                              2.0.0.0    NetAdapter
Function        Get-NetAdapterStatistics                           2.0.0.0    NetAdapter
Function        Get-NetAdapterUso                                  2.0.0.0    NetAdapter
Function        Get-NetAdapterVmq                                  2.0.0.0    NetAdapter
Function        Get-NetAdapterVMQQueue                             2.0.0.0    NetAdapter
Function        Get-NetAdapterVPort                                2.0.0.0    NetAdapter
Function        Get-NetCompartment                                 1.0.0.0    NetTCPIP
Function        Get-NetConnectionProfile                           1.0.0.0    NetConnection
Function        Get-NetDnsTransitionConfiguration                  1.0.0.0    NetworkTransition
Function        Get-NetDnsTransitionMonitoring                     1.0.0.0    NetworkTransition
Function        Get-NetEventNetworkAdapter                         1.0.0.0    NetEventPacketCapture
Function        Get-NetEventPacketCaptureProvider                  1.0.0.0    NetEventPacketCapture
Function        Get-NetEventProvider                               1.0.0.0    NetEventPacketCapture
Function        Get-NetEventSession                                1.0.0.0    NetEventPacketCapture
Function        Get-NetEventVFPProvider                            1.0.0.0    NetEventPacketCapture
Function        Get-NetEventVmNetworkAdapter                       1.0.0.0    NetEventPacketCapture
Function        Get-NetEventVmSwitch                               1.0.0.0    NetEventPacketCapture
Function        Get-NetEventVmSwitchProvider                       1.0.0.0    NetEventPacketCapture
Function        Get-NetEventWFPCaptureProvider                     1.0.0.0    NetEventPacketCapture
Function        Get-NetFirewallAddressFilter                       2.0.0.0    NetSecurity
Function        Get-NetFirewallApplicationFilter                   2.0.0.0    NetSecurity
Function        Get-NetFirewallDynamicKeywordAddress               2.0.0.0    NetSecurity
Function        Get-NetFirewallInterfaceFilter                     2.0.0.0    NetSecurity
Function        Get-NetFirewallInterfaceTypeFilter                 2.0.0.0    NetSecurity
Function        Get-NetFirewallPortFilter                          2.0.0.0    NetSecurity
Function        Get-NetFirewallProfile                             2.0.0.0    NetSecurity
Function        Get-NetFirewallRule                                2.0.0.0    NetSecurity
Function        Get-NetFirewallSecurityFilter                      2.0.0.0    NetSecurity
Function        Get-NetFirewallServiceFilter                       2.0.0.0    NetSecurity
Function        Get-NetFirewallSetting                             2.0.0.0    NetSecurity
Function        Get-NetIPAddress                                   1.0.0.0    NetTCPIP
Function        Get-NetIPConfiguration                             1.0.0.0    NetTCPIP
Function        Get-NetIPHttpsConfiguration                        1.0.0.0    NetworkTransition
Function        Get-NetIPHttpsState                                1.0.0.0    NetworkTransition
Function        Get-NetIPInterface                                 1.0.0.0    NetTCPIP
Function        Get-NetIPsecDospSetting                            2.0.0.0    NetSecurity
Function        Get-NetIPsecMainModeCryptoSet                      2.0.0.0    NetSecurity
Function        Get-NetIPsecMainModeRule                           2.0.0.0    NetSecurity
Function        Get-NetIPsecMainModeSA                             2.0.0.0    NetSecurity
Function        Get-NetIPsecPhase1AuthSet                          2.0.0.0    NetSecurity
Function        Get-NetIPsecPhase2AuthSet                          2.0.0.0    NetSecurity
Function        Get-NetIPsecQuickModeCryptoSet                     2.0.0.0    NetSecurity
Function        Get-NetIPsecQuickModeSA                            2.0.0.0    NetSecurity
Function        Get-NetIPsecRule                                   2.0.0.0    NetSecurity
Function        Get-NetIPv4Protocol                                1.0.0.0    NetTCPIP
Function        Get-NetIPv6Protocol                                1.0.0.0    NetTCPIP
Function        Get-NetIsatapConfiguration                         1.0.0.0    NetworkTransition
Function        Get-NetLbfoTeam                                    2.0.0.0    NetLbfo
Function        Get-NetLbfoTeamMember                              2.0.0.0    NetLbfo
Function        Get-NetLbfoTeamNic                                 2.0.0.0    NetLbfo
Function        Get-NetNat                                         1.0.0.0    NetNat
Function        Get-NetNatExternalAddress                          1.0.0.0    NetNat
Function        Get-NetNatGlobal                                   1.0.0.0    NetNat
Function        Get-NetNatSession                                  1.0.0.0    NetNat
Function        Get-NetNatStaticMapping                            1.0.0.0    NetNat
Function        Get-NetNatTransitionConfiguration                  1.0.0.0    NetworkTransition
Function        Get-NetNatTransitionMonitoring                     1.0.0.0    NetworkTransition
Function        Get-NetNeighbor                                    1.0.0.0    NetTCPIP
Function        Get-NetOffloadGlobalSetting                        1.0.0.0    NetTCPIP
Function        Get-NetPrefixPolicy                                1.0.0.0    NetTCPIP
Function        Get-NetQosPolicy                                   2.0.0.0    NetQos
Function        Get-NetRoute                                       1.0.0.0    NetTCPIP
Function        Get-NetSwitchTeam                                  1.0.0.0    NetSwitchTeam
Function        Get-NetSwitchTeamMember                            1.0.0.0    NetSwitchTeam
Function        Get-NetTCPConnection                               1.0.0.0    NetTCPIP
Function        Get-NetTCPSetting                                  1.0.0.0    NetTCPIP
Function        Get-NetTeredoConfiguration                         1.0.0.0    NetworkTransition
Function        Get-NetTeredoState                                 1.0.0.0    NetworkTransition
Function        Get-NetTransportFilter                             1.0.0.0    NetTCPIP
Function        Get-NetUDPEndpoint                                 1.0.0.0    NetTCPIP
Function        Get-NetUDPSetting                                  1.0.0.0    NetTCPIP
Function        Get-NetworkSwitchEthernetPort                      1.0.0.0    NetworkSwitchManager
Function        Get-NetworkSwitchFeature                           1.0.0.0    NetworkSwitchManager
Function        Get-NetworkSwitchGlobalData                        1.0.0.0    NetworkSwitchManager
Function        Get-NetworkSwitchVlan                              1.0.0.0    NetworkSwitchManager
Function        Get-OdbcDriver                                     1.0.0.0    Wdac
Function        Get-OdbcDsn                                        1.0.0.0    Wdac
Function        Get-OdbcPerfCounter                                1.0.0.0    Wdac
Function        Get-OffloadDataTransferSetting                     2.0.0.0    Storage
Function        Get-OperationValidation                            1.0.1      Microsoft.PowerShell.Operation.Validation
Function        Get-Partition                                      2.0.0.0    Storage
Function        Get-PartitionSupportedSize                         2.0.0.0    Storage
Function        Get-PcsvDevice                                     1.0.0.0    PcsvDevice
Function        Get-PcsvDeviceLog                                  1.0.0.0    PcsvDevice
Function        Get-PhysicalDisk                                   2.0.0.0    Storage
Function        Get-PhysicalDiskStorageNodeView                    2.0.0.0    Storage
Function        Get-PhysicalExtent                                 2.0.0.0    Storage
Function        Get-PhysicalExtentAssociation                      2.0.0.0    Storage
Function        Get-PnpDevice                                      1.0.0.0    PnpDevice
Function        Get-PnpDeviceProperty                              1.0.0.0    PnpDevice
Function        Get-PrintConfiguration                             1.1        PrintManagement
Function        Get-Printer                                        1.1        PrintManagement
Function        Get-PrinterDriver                                  1.1        PrintManagement
Function        Get-PrinterPort                                    1.1        PrintManagement
Function        Get-PrinterProperty                                1.1        PrintManagement
Function        Get-PrintJob                                       1.1        PrintManagement
Function        Get-PSRepository                                   1.0.0.1    PowerShellGet
Function        Get-ResiliencySetting                              2.0.0.0    Storage
Function        Get-ScheduledTask                                  1.0.0.0    ScheduledTasks
Function        Get-ScheduledTaskInfo                              1.0.0.0    ScheduledTasks
Function        Get-SmbBandWidthLimit                              2.0.0.0    SmbShare
Function        Get-SmbClientConfiguration                         2.0.0.0    SmbShare
Function        Get-SmbClientNetworkInterface                      2.0.0.0    SmbShare
Function        Get-SmbConnection                                  2.0.0.0    SmbShare
Function        Get-SmbDelegation                                  2.0.0.0    SmbShare
Function        Get-SmbGlobalMapping                               2.0.0.0    SmbShare
Function        Get-SmbMapping                                     2.0.0.0    SmbShare
Function        Get-SmbMultichannelConnection                      2.0.0.0    SmbShare
Function        Get-SmbMultichannelConstraint                      2.0.0.0    SmbShare
Function        Get-SmbOpenFile                                    2.0.0.0    SmbShare
Function        Get-SmbServerCertificateMapping                    2.0.0.0    SmbShare
Function        Get-SmbServerConfiguration                         2.0.0.0    SmbShare
Function        Get-SmbServerNetworkInterface                      2.0.0.0    SmbShare
Function        Get-SmbSession                                     2.0.0.0    SmbShare
Function        Get-SmbShare                                       2.0.0.0    SmbShare
Function        Get-SmbShareAccess                                 2.0.0.0    SmbShare
Function        Get-SmbWitnessClient                               2.0.0.0    SmbWitness
Function        Get-StartApps                                      1.0.0.2    StartLayout
Function        Get-StorageAdvancedProperty                        2.0.0.0    Storage
Function        Get-StorageBusBinding                              1.0.0.0    StorageBusCache
Function        Get-StorageBusDisk                                 1.0.0.0    StorageBusCache
Function        Get-StorageChassis                                 2.0.0.0    Storage
Function        Get-StorageDiagnosticInfo                          2.0.0.0    Storage
Function        Get-StorageEnclosure                               2.0.0.0    Storage
Function        Get-StorageEnclosureStorageNodeView                2.0.0.0    Storage
Function        Get-StorageEnclosureVendorData                     2.0.0.0    Storage
Function        Get-StorageExtendedStatus                          2.0.0.0    Storage
Function        Get-StorageFaultDomain                             2.0.0.0    Storage
Function        Get-StorageFileServer                              2.0.0.0    Storage
Function        Get-StorageFirmwareInformation                     2.0.0.0    Storage
Function        Get-StorageHealthAction                            2.0.0.0    Storage
Function        Get-StorageHealthReport                            2.0.0.0    Storage
Function        Get-StorageHealthSetting                           2.0.0.0    Storage
Function        Get-StorageHistory                                 2.0.0.0    Storage
Function        Get-StorageJob                                     2.0.0.0    Storage
Function        Get-StorageNode                                    2.0.0.0    Storage
Function        Get-StoragePool                                    2.0.0.0    Storage
Function        Get-StorageProvider                                2.0.0.0    Storage
Function        Get-StorageRack                                    2.0.0.0    Storage
Function        Get-StorageReliabilityCounter                      2.0.0.0    Storage
Function        Get-StorageScaleUnit                               2.0.0.0    Storage
Function        Get-StorageSetting                                 2.0.0.0    Storage
Function        Get-StorageSite                                    2.0.0.0    Storage
Function        Get-StorageSubSystem                               2.0.0.0    Storage
Function        Get-StorageTier                                    2.0.0.0    Storage
Function        Get-StorageTierSupportedSize                       2.0.0.0    Storage
Function        Get-SupportedClusterSizes                          2.0.0.0    Storage
Function        Get-SupportedFileSystems                           2.0.0.0    Storage
Function        Get-TargetPort                                     2.0.0.0    Storage
Function        Get-TargetPortal                                   2.0.0.0    Storage
Function        Get-TestDriveItem                                  3.4.0      Pester
Function        Get-Verb
Function        Get-VirtualDisk                                    2.0.0.0    Storage
Function        Get-VirtualDiskSupportedSize                       2.0.0.0    Storage
Function        Get-Volume                                         2.0.0.0    Storage
Function        Get-VolumeCorruptionCount                          2.0.0.0    Storage
Function        Get-VolumeScrubPolicy                              2.0.0.0    Storage
Function        Get-VpnConnection                                  2.0.0.0    VpnClient
Function        Get-VpnConnectionTrigger                           2.0.0.0    VpnClient
Function        Get-WdacBidTrace                                   1.0.0.0    Wdac
Function        Get-WindowsUpdateLog                               1.0.0.0    WindowsUpdate
Function        Get-WUAVersion                                     1.0.0.2    WindowsUpdateProvider
Function        Get-WUIsPendingReboot                              1.0.0.2    WindowsUpdateProvider
Function        Get-WULastInstallationDate                         1.0.0.2    WindowsUpdateProvider
Function        Get-WULastScanSuccessDate                          1.0.0.2    WindowsUpdateProvider
Function        Grant-FileShareAccess                              2.0.0.0    Storage
Function        Grant-SmbShareAccess                               2.0.0.0    SmbShare
Function        H:
Function        help
Function        Hide-VirtualDisk                                   2.0.0.0    Storage
Function        I:
Function        Import-IseSnippet                                  1.0.0.0    ISE
Function        Import-PowerShellDataFile                          3.1.0.0    Microsoft.PowerShell.Utility
Function        ImportSystemModules
Function        In                                                 3.4.0      Pester
Function        Initialize-Disk                                    2.0.0.0    Storage
Function        InModuleScope                                      3.4.0      Pester
Function        Install-Dtc                                        1.0.0.0    MsDtc
Function        Install-Module                                     1.0.0.1    PowerShellGet
Function        Install-Script                                     1.0.0.1    PowerShellGet
Function        Install-WUUpdates                                  1.0.0.2    WindowsUpdateProvider
Function        Invoke-AsWorkflow                                  1.0.0.0    PSWorkflowUtility
Function        Invoke-Mock                                        3.4.0      Pester
Function        Invoke-OperationValidation                         1.0.1      Microsoft.PowerShell.Operation.Validation
Function        Invoke-Pester                                      3.4.0      Pester
Function        It                                                 3.4.0      Pester
Function        J:
Function        K:
Function        L:
Function        Lock-BitLocker                                     1.0.0.0    BitLocker
Function        M:
Function        mkdir
Function        Mock                                               3.4.0      Pester
Function        more
Function        Mount-DiskImage                                    2.0.0.0    Storage
Function        Move-SmbWitnessClient                              2.0.0.0    SmbWitness
Function        N:
Function        New-AutologgerConfig                               1.0.0.0    EventTracingManagement
Function        New-DAEntryPointTableItem                          1.0.0.0    DirectAccessClientComponents
Function        New-DscChecksum                                    1.1        PSDesiredStateConfiguration
Function        New-EapConfiguration                               2.0.0.0    VpnClient
Function        New-EtwTraceSession                                1.0.0.0    EventTracingManagement
Function        New-FileShare                                      2.0.0.0    Storage
Function        New-Fixture                                        3.4.0      Pester
Function        New-Guid                                           3.1.0.0    Microsoft.PowerShell.Utility
Function        New-IscsiTargetPortal                              1.0.0.0    iSCSI
Function        New-IseSnippet                                     1.0.0.0    ISE
Function        New-MaskingSet                                     2.0.0.0    Storage
Function        New-NetAdapterAdvancedProperty                     2.0.0.0    NetAdapter
Function        New-NetEventSession                                1.0.0.0    NetEventPacketCapture
Function        New-NetFirewallDynamicKeywordAddress               2.0.0.0    NetSecurity
Function        New-NetFirewallRule                                2.0.0.0    NetSecurity
Function        New-NetIPAddress                                   1.0.0.0    NetTCPIP
Function        New-NetIPHttpsConfiguration                        1.0.0.0    NetworkTransition
Function        New-NetIPsecDospSetting                            2.0.0.0    NetSecurity
Function        New-NetIPsecMainModeCryptoSet                      2.0.0.0    NetSecurity
Function        New-NetIPsecMainModeRule                           2.0.0.0    NetSecurity
Function        New-NetIPsecPhase1AuthSet                          2.0.0.0    NetSecurity
Function        New-NetIPsecPhase2AuthSet                          2.0.0.0    NetSecurity
Function        New-NetIPsecQuickModeCryptoSet                     2.0.0.0    NetSecurity
Function        New-NetIPsecRule                                   2.0.0.0    NetSecurity
Function        New-NetLbfoTeam                                    2.0.0.0    NetLbfo
Function        New-NetNat                                         1.0.0.0    NetNat
Function        New-NetNatTransitionConfiguration                  1.0.0.0    NetworkTransition
Function        New-NetNeighbor                                    1.0.0.0    NetTCPIP
Function        New-NetQosPolicy                                   2.0.0.0    NetQos
Function        New-NetRoute                                       1.0.0.0    NetTCPIP
Function        New-NetSwitchTeam                                  1.0.0.0    NetSwitchTeam
Function        New-NetTransportFilter                             1.0.0.0    NetTCPIP
Function        New-NetworkSwitchVlan                              1.0.0.0    NetworkSwitchManager
Function        New-Partition                                      2.0.0.0    Storage
Function        New-PesterOption                                   3.4.0      Pester
Function        New-PSWorkflowSession                              2.0.0.0    PSWorkflow
Function        New-ScheduledTask                                  1.0.0.0    ScheduledTasks
Function        New-ScheduledTaskAction                            1.0.0.0    ScheduledTasks
Function        New-ScheduledTaskPrincipal                         1.0.0.0    ScheduledTasks
Function        New-ScheduledTaskSettingsSet                       1.0.0.0    ScheduledTasks
Function        New-ScheduledTaskTrigger                           1.0.0.0    ScheduledTasks
Function        New-ScriptFileInfo                                 1.0.0.1    PowerShellGet
Function        New-SmbGlobalMapping                               2.0.0.0    SmbShare
Function        New-SmbMapping                                     2.0.0.0    SmbShare
Function        New-SmbMultichannelConstraint                      2.0.0.0    SmbShare
Function        New-SmbServerCertificateMapping                    2.0.0.0    SmbShare
Function        New-SmbShare                                       2.0.0.0    SmbShare
Function        New-StorageBusBinding                              1.0.0.0    StorageBusCache
Function        New-StorageBusCacheStore                           1.0.0.0    StorageBusCache
Function        New-StorageFileServer                              2.0.0.0    Storage
Function        New-StoragePool                                    2.0.0.0    Storage
Function        New-StorageSubsystemVirtualDisk                    2.0.0.0    Storage
Function        New-StorageTier                                    2.0.0.0    Storage
Function        New-TemporaryFile                                  3.1.0.0    Microsoft.PowerShell.Utility
Function        New-VirtualDisk                                    2.0.0.0    Storage
Function        New-VirtualDiskClone                               2.0.0.0    Storage
Function        New-VirtualDiskSnapshot                            2.0.0.0    Storage
Function        New-Volume                                         2.0.0.0    Storage
Function        New-VpnServerAddress                               2.0.0.0    VpnClient
Function        O:
Function        Open-NetGPO                                        2.0.0.0    NetSecurity
Function        Optimize-StoragePool                               2.0.0.0    Storage
Function        Optimize-Volume                                    2.0.0.0    Storage
Function        oss
Function        P:
Function        Pause
Function        prompt
Function        PSConsoleHostReadLine                              2.0.0      PSReadline
Function        Publish-Module                                     1.0.0.1    PowerShellGet
Function        Publish-Script                                     1.0.0.1    PowerShellGet
Function        Q:
Function        R:
Function        Read-PrinterNfcTag                                 1.1        PrintManagement
Function        Register-ClusteredScheduledTask                    1.0.0.0    ScheduledTasks
Function        Register-DnsClient                                 1.0.0.0    DnsClient
Function        Register-IscsiSession                              1.0.0.0    iSCSI
Function        Register-PSRepository                              1.0.0.1    PowerShellGet
Function        Register-ScheduledTask                             1.0.0.0    ScheduledTasks
Function        Register-StorageSubsystem                          2.0.0.0    Storage
Function        Remove-AutologgerConfig                            1.0.0.0    EventTracingManagement
Function        Remove-BitLockerKeyProtector                       1.0.0.0    BitLocker
Function        Remove-DAEntryPointTableItem                       1.0.0.0    DirectAccessClientComponents
Function        Remove-DnsClientNrptRule                           1.0.0.0    DnsClient
Function        Remove-DscConfigurationDocument                    1.1        PSDesiredStateConfiguration
Function        Remove-DtcClusterTMMapping                         1.0.0.0    MsDtc
Function        Remove-EtwTraceProvider                            1.0.0.0    EventTracingManagement
Function        Remove-FileShare                                   2.0.0.0    Storage
Function        Remove-InitiatorId                                 2.0.0.0    Storage
Function        Remove-InitiatorIdFromMaskingSet                   2.0.0.0    Storage
Function        Remove-IscsiTargetPortal                           1.0.0.0    iSCSI
Function        Remove-MaskingSet                                  2.0.0.0    Storage
Function        Remove-MpPreference                                1.0        ConfigDefender
Function        Remove-MpPreference                                1.0        Defender
Function        Remove-MpThreat                                    1.0        ConfigDefender
Function        Remove-MpThreat                                    1.0        Defender
Function        Remove-NetAdapterAdvancedProperty                  2.0.0.0    NetAdapter
Function        Remove-NetEventNetworkAdapter                      1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventPacketCaptureProvider               1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventProvider                            1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventSession                             1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventVFPProvider                         1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventVmNetworkAdapter                    1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventVmSwitch                            1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventVmSwitchProvider                    1.0.0.0    NetEventPacketCapture
Function        Remove-NetEventWFPCaptureProvider                  1.0.0.0    NetEventPacketCapture
Function        Remove-NetFirewallDynamicKeywordAddress            2.0.0.0    NetSecurity
Function        Remove-NetFirewallRule                             2.0.0.0    NetSecurity
Function        Remove-NetIPAddress                                1.0.0.0    NetTCPIP
Function        Remove-NetIPHttpsCertBinding                       1.0.0.0    NetworkTransition
Function        Remove-NetIPHttpsConfiguration                     1.0.0.0    NetworkTransition
Function        Remove-NetIPsecDospSetting                         2.0.0.0    NetSecurity
Function        Remove-NetIPsecMainModeCryptoSet                   2.0.0.0    NetSecurity
Function        Remove-NetIPsecMainModeRule                        2.0.0.0    NetSecurity
Function        Remove-NetIPsecMainModeSA                          2.0.0.0    NetSecurity
Function        Remove-NetIPsecPhase1AuthSet                       2.0.0.0    NetSecurity
Function        Remove-NetIPsecPhase2AuthSet                       2.0.0.0    NetSecurity
Function        Remove-NetIPsecQuickModeCryptoSet                  2.0.0.0    NetSecurity
Function        Remove-NetIPsecQuickModeSA                         2.0.0.0    NetSecurity
Function        Remove-NetIPsecRule                                2.0.0.0    NetSecurity
Function        Remove-NetLbfoTeam                                 2.0.0.0    NetLbfo
Function        Remove-NetLbfoTeamMember                           2.0.0.0    NetLbfo
Function        Remove-NetLbfoTeamNic                              2.0.0.0    NetLbfo
Function        Remove-NetNat                                      1.0.0.0    NetNat
Function        Remove-NetNatExternalAddress                       1.0.0.0    NetNat
Function        Remove-NetNatStaticMapping                         1.0.0.0    NetNat
Function        Remove-NetNatTransitionConfiguration               1.0.0.0    NetworkTransition
Function        Remove-NetNeighbor                                 1.0.0.0    NetTCPIP
Function        Remove-NetQosPolicy                                2.0.0.0    NetQos
Function        Remove-NetRoute                                    1.0.0.0    NetTCPIP
Function        Remove-NetSwitchTeam                               1.0.0.0    NetSwitchTeam
Function        Remove-NetSwitchTeamMember                         1.0.0.0    NetSwitchTeam
Function        Remove-NetTransportFilter                          1.0.0.0    NetTCPIP
Function        Remove-NetworkSwitchEthernetPortIPAddress          1.0.0.0    NetworkSwitchManager
Function        Remove-NetworkSwitchVlan                           1.0.0.0    NetworkSwitchManager
Function        Remove-OdbcDsn                                     1.0.0.0    Wdac
Function        Remove-Partition                                   2.0.0.0    Storage
Function        Remove-PartitionAccessPath                         2.0.0.0    Storage
Function        Remove-PhysicalDisk                                2.0.0.0    Storage
Function        Remove-Printer                                     1.1        PrintManagement
Function        Remove-PrinterDriver                               1.1        PrintManagement
Function        Remove-PrinterPort                                 1.1        PrintManagement
Function        Remove-PrintJob                                    1.1        PrintManagement
Function        Remove-SmbBandwidthLimit                           2.0.0.0    SmbShare
Function        Remove-SMBComponent                                2.0.0.0    SmbShare
Function        Remove-SmbGlobalMapping                            2.0.0.0    SmbShare
Function        Remove-SmbMapping                                  2.0.0.0    SmbShare
Function        Remove-SmbMultichannelConstraint                   2.0.0.0    SmbShare
Function        Remove-SmbServerCertificateMapping                 2.0.0.0    SmbShare
Function        Remove-SmbShare                                    2.0.0.0    SmbShare
Function        Remove-StorageBusBinding                           1.0.0.0    StorageBusCache
Function        Remove-StorageFaultDomain                          2.0.0.0    Storage
Function        Remove-StorageFileServer                           2.0.0.0    Storage
Function        Remove-StorageHealthIntent                         2.0.0.0    Storage
Function        Remove-StorageHealthSetting                        2.0.0.0    Storage
Function        Remove-StoragePool                                 2.0.0.0    Storage
Function        Remove-StorageTier                                 2.0.0.0    Storage
Function        Remove-TargetPortFromMaskingSet                    2.0.0.0    Storage
Function        Remove-VirtualDisk                                 2.0.0.0    Storage
Function        Remove-VirtualDiskFromMaskingSet                   2.0.0.0    Storage
Function        Remove-VpnConnection                               2.0.0.0    VpnClient
Function        Remove-VpnConnectionRoute                          2.0.0.0    VpnClient
Function        Remove-VpnConnectionTriggerApplication             2.0.0.0    VpnClient
Function        Remove-VpnConnectionTriggerDnsConfiguration        2.0.0.0    VpnClient
Function        Remove-VpnConnectionTriggerTrustedNetwork          2.0.0.0    VpnClient
Function        Rename-DAEntryPointTableItem                       1.0.0.0    DirectAccessClientComponents
Function        Rename-MaskingSet                                  2.0.0.0    Storage
Function        Rename-NetAdapter                                  2.0.0.0    NetAdapter
Function        Rename-NetFirewallRule                             2.0.0.0    NetSecurity
Function        Rename-NetIPHttpsConfiguration                     1.0.0.0    NetworkTransition
Function        Rename-NetIPsecMainModeCryptoSet                   2.0.0.0    NetSecurity
Function        Rename-NetIPsecMainModeRule                        2.0.0.0    NetSecurity
Function        Rename-NetIPsecPhase1AuthSet                       2.0.0.0    NetSecurity
Function        Rename-NetIPsecPhase2AuthSet                       2.0.0.0    NetSecurity
Function        Rename-NetIPsecQuickModeCryptoSet                  2.0.0.0    NetSecurity
Function        Rename-NetIPsecRule                                2.0.0.0    NetSecurity
Function        Rename-NetLbfoTeam                                 2.0.0.0    NetLbfo
Function        Rename-NetSwitchTeam                               1.0.0.0    NetSwitchTeam
Function        Rename-Printer                                     1.1        PrintManagement
Function        Repair-FileIntegrity                               2.0.0.0    Storage
Function        Repair-VirtualDisk                                 2.0.0.0    Storage
Function        Repair-Volume                                      2.0.0.0    Storage
Function        Reset-DAClientExperienceConfiguration              1.0.0.0    DirectAccessClientComponents
Function        Reset-DAEntryPointTableItem                        1.0.0.0    DirectAccessClientComponents
Function        Reset-DtcLog                                       1.0.0.0    MsDtc
Function        Reset-NCSIPolicyConfiguration                      1.0.0.0    NetworkConnectivityStatus
Function        Reset-Net6to4Configuration                         1.0.0.0    NetworkTransition
Function        Reset-NetAdapterAdvancedProperty                   2.0.0.0    NetAdapter
Function        Reset-NetDnsTransitionConfiguration                1.0.0.0    NetworkTransition
Function        Reset-NetIPHttpsConfiguration                      1.0.0.0    NetworkTransition
Function        Reset-NetIsatapConfiguration                       1.0.0.0    NetworkTransition
Function        Reset-NetTeredoConfiguration                       1.0.0.0    NetworkTransition
Function        Reset-PhysicalDisk                                 2.0.0.0    Storage
Function        Reset-StorageReliabilityCounter                    2.0.0.0    Storage
Function        Resize-Partition                                   2.0.0.0    Storage
Function        Resize-StorageTier                                 2.0.0.0    Storage
Function        Resize-VirtualDisk                                 2.0.0.0    Storage
Function        Restart-NetAdapter                                 2.0.0.0    NetAdapter
Function        Restart-PcsvDevice                                 1.0.0.0    PcsvDevice
Function        Restart-PrintJob                                   1.1        PrintManagement
Function        Restore-DscConfiguration                           1.1        PSDesiredStateConfiguration
Function        Restore-NetworkSwitchConfiguration                 1.0.0.0    NetworkSwitchManager
Function        Resume-BitLocker                                   1.0.0.0    BitLocker
Function        Resume-PrintJob                                    1.1        PrintManagement
Function        Resume-StorageBusDisk                              1.0.0.0    StorageBusCache
Function        Revoke-FileShareAccess                             2.0.0.0    Storage
Function        Revoke-SmbShareAccess                              2.0.0.0    SmbShare
Function        S:
Function        SafeGetCommand                                     3.4.0      Pester
Function        Save-EtwTraceSession                               1.0.0.0    EventTracingManagement
Function        Save-Module                                        1.0.0.1    PowerShellGet
Function        Save-NetGPO                                        2.0.0.0    NetSecurity
Function        Save-NetworkSwitchConfiguration                    1.0.0.0    NetworkSwitchManager
Function        Save-Script                                        1.0.0.1    PowerShellGet
Function        Send-EtwTraceSession                               1.0.0.0    EventTracingManagement
Function        Set-ClusteredScheduledTask                         1.0.0.0    ScheduledTasks
Function        Set-DAClientExperienceConfiguration                1.0.0.0    DirectAccessClientComponents
Function        Set-DAEntryPointTableItem                          1.0.0.0    DirectAccessClientComponents
Function        Set-Disk                                           2.0.0.0    Storage
Function        Set-DnsClient                                      1.0.0.0    DnsClient
Function        Set-DnsClientGlobalSetting                         1.0.0.0    DnsClient
Function        Set-DnsClientNrptGlobal                            1.0.0.0    DnsClient
Function        Set-DnsClientNrptRule                              1.0.0.0    DnsClient
Function        Set-DnsClientServerAddress                         1.0.0.0    DnsClient
Function        Set-DtcAdvancedHostSetting                         1.0.0.0    MsDtc
Function        Set-DtcAdvancedSetting                             1.0.0.0    MsDtc
Function        Set-DtcClusterDefault                              1.0.0.0    MsDtc
Function        Set-DtcClusterTMMapping                            1.0.0.0    MsDtc
Function        Set-DtcDefault                                     1.0.0.0    MsDtc
Function        Set-DtcLog                                         1.0.0.0    MsDtc
Function        Set-DtcNetworkSetting                              1.0.0.0    MsDtc
Function        Set-DtcTransaction                                 1.0.0.0    MsDtc
Function        Set-DtcTransactionsTraceSession                    1.0.0.0    MsDtc
Function        Set-DtcTransactionsTraceSetting                    1.0.0.0    MsDtc
Function        Set-DynamicParameterVariables                      3.4.0      Pester
Function        Set-EtwTraceProvider                               1.0.0.0    EventTracingManagement
Function        Set-FileIntegrity                                  2.0.0.0    Storage
Function        Set-FileShare                                      2.0.0.0    Storage
Function        Set-FileStorageTier                                2.0.0.0    Storage
Function        Set-InitiatorPort                                  2.0.0.0    Storage
Function        Set-IscsiChapSecret                                1.0.0.0    iSCSI
Function        Set-LogProperties                                  1.0.0.0    PSDiagnostics
Function        Set-MMAgent                                        1.0        MMAgent
Function        Set-MpPreference                                   1.0        ConfigDefender
Function        Set-MpPreference                                   1.0        Defender
Function        Set-NCSIPolicyConfiguration                        1.0.0.0    NetworkConnectivityStatus
Function        Set-Net6to4Configuration                           1.0.0.0    NetworkTransition
Function        Set-NetAdapter                                     2.0.0.0    NetAdapter
Function        Set-NetAdapterAdvancedProperty                     2.0.0.0    NetAdapter
Function        Set-NetAdapterBinding                              2.0.0.0    NetAdapter
Function        Set-NetAdapterChecksumOffload                      2.0.0.0    NetAdapter
Function        Set-NetAdapterEncapsulatedPacketTaskOffload        2.0.0.0    NetAdapter
Function        Set-NetAdapterIPsecOffload                         2.0.0.0    NetAdapter
Function        Set-NetAdapterLso                                  2.0.0.0    NetAdapter
Function        Set-NetAdapterPacketDirect                         2.0.0.0    NetAdapter
Function        Set-NetAdapterPowerManagement                      2.0.0.0    NetAdapter
Function        Set-NetAdapterQos                                  2.0.0.0    NetAdapter
Function        Set-NetAdapterRdma                                 2.0.0.0    NetAdapter
Function        Set-NetAdapterRsc                                  2.0.0.0    NetAdapter
Function        Set-NetAdapterRss                                  2.0.0.0    NetAdapter
Function        Set-NetAdapterSriov                                2.0.0.0    NetAdapter
Function        Set-NetAdapterUso                                  2.0.0.0    NetAdapter
Function        Set-NetAdapterVmq                                  2.0.0.0    NetAdapter
Function        Set-NetConnectionProfile                           1.0.0.0    NetConnection
Function        Set-NetDnsTransitionConfiguration                  1.0.0.0    NetworkTransition
Function        Set-NetEventPacketCaptureProvider                  1.0.0.0    NetEventPacketCapture
Function        Set-NetEventProvider                               1.0.0.0    NetEventPacketCapture
Function        Set-NetEventSession                                1.0.0.0    NetEventPacketCapture
Function        Set-NetEventVFPProvider                            1.0.0.0    NetEventPacketCapture
Function        Set-NetEventVmSwitchProvider                       1.0.0.0    NetEventPacketCapture
Function        Set-NetEventWFPCaptureProvider                     1.0.0.0    NetEventPacketCapture
Function        Set-NetFirewallAddressFilter                       2.0.0.0    NetSecurity
Function        Set-NetFirewallApplicationFilter                   2.0.0.0    NetSecurity
Function        Set-NetFirewallInterfaceFilter                     2.0.0.0    NetSecurity
Function        Set-NetFirewallInterfaceTypeFilter                 2.0.0.0    NetSecurity
Function        Set-NetFirewallPortFilter                          2.0.0.0    NetSecurity
Function        Set-NetFirewallProfile                             2.0.0.0    NetSecurity
Function        Set-NetFirewallRule                                2.0.0.0    NetSecurity
Function        Set-NetFirewallSecurityFilter                      2.0.0.0    NetSecurity
Function        Set-NetFirewallServiceFilter                       2.0.0.0    NetSecurity
Function        Set-NetFirewallSetting                             2.0.0.0    NetSecurity
Function        Set-NetIPAddress                                   1.0.0.0    NetTCPIP
Function        Set-NetIPHttpsConfiguration                        1.0.0.0    NetworkTransition
Function        Set-NetIPInterface                                 1.0.0.0    NetTCPIP
Function        Set-NetIPsecDospSetting                            2.0.0.0    NetSecurity
Function        Set-NetIPsecMainModeCryptoSet                      2.0.0.0    NetSecurity
Function        Set-NetIPsecMainModeRule                           2.0.0.0    NetSecurity
Function        Set-NetIPsecPhase1AuthSet                          2.0.0.0    NetSecurity
Function        Set-NetIPsecPhase2AuthSet                          2.0.0.0    NetSecurity
Function        Set-NetIPsecQuickModeCryptoSet                     2.0.0.0    NetSecurity
Function        Set-NetIPsecRule                                   2.0.0.0    NetSecurity
Function        Set-NetIPv4Protocol                                1.0.0.0    NetTCPIP
Function        Set-NetIPv6Protocol                                1.0.0.0    NetTCPIP
Function        Set-NetIsatapConfiguration                         1.0.0.0    NetworkTransition
Function        Set-NetLbfoTeam                                    2.0.0.0    NetLbfo
Function        Set-NetLbfoTeamMember                              2.0.0.0    NetLbfo
Function        Set-NetLbfoTeamNic                                 2.0.0.0    NetLbfo
Function        Set-NetNat                                         1.0.0.0    NetNat
Function        Set-NetNatGlobal                                   1.0.0.0    NetNat
Function        Set-NetNatTransitionConfiguration                  1.0.0.0    NetworkTransition
Function        Set-NetNeighbor                                    1.0.0.0    NetTCPIP
Function        Set-NetOffloadGlobalSetting                        1.0.0.0    NetTCPIP
Function        Set-NetQosPolicy                                   2.0.0.0    NetQos
Function        Set-NetRoute                                       1.0.0.0    NetTCPIP
Function        Set-NetTCPSetting                                  1.0.0.0    NetTCPIP
Function        Set-NetTeredoConfiguration                         1.0.0.0    NetworkTransition
Function        Set-NetUDPSetting                                  1.0.0.0    NetTCPIP
Function        Set-NetworkSwitchEthernetPortIPAddress             1.0.0.0    NetworkSwitchManager
Function        Set-NetworkSwitchPortMode                          1.0.0.0    NetworkSwitchManager
Function        Set-NetworkSwitchPortProperty                      1.0.0.0    NetworkSwitchManager
Function        Set-NetworkSwitchVlanProperty                      1.0.0.0    NetworkSwitchManager
Function        Set-OdbcDriver                                     1.0.0.0    Wdac
Function        Set-OdbcDsn                                        1.0.0.0    Wdac
Function        Set-Partition                                      2.0.0.0    Storage
Function        Set-PcsvDeviceBootConfiguration                    1.0.0.0    PcsvDevice
Function        Set-PcsvDeviceNetworkConfiguration                 1.0.0.0    PcsvDevice
Function        Set-PcsvDeviceUserPassword                         1.0.0.0    PcsvDevice
Function        Set-PhysicalDisk                                   2.0.0.0    Storage
Function        Set-PrintConfiguration                             1.1        PrintManagement
Function        Set-Printer                                        1.1        PrintManagement
Function        Set-PrinterProperty                                1.1        PrintManagement
Function        Set-PSRepository                                   1.0.0.1    PowerShellGet
Function        Set-ResiliencySetting                              2.0.0.0    Storage
Function        Set-ScheduledTask                                  1.0.0.0    ScheduledTasks
Function        Set-SmbBandwidthLimit                              2.0.0.0    SmbShare
Function        Set-SmbClientConfiguration                         2.0.0.0    SmbShare
Function        Set-SmbPathAcl                                     2.0.0.0    SmbShare
Function        Set-SmbServerConfiguration                         2.0.0.0    SmbShare
Function        Set-SmbShare                                       2.0.0.0    SmbShare
Function        Set-StorageBusProfile                              1.0.0.0    StorageBusCache
Function        Set-StorageFileServer                              2.0.0.0    Storage
Function        Set-StorageHealthSetting                           2.0.0.0    Storage
Function        Set-StoragePool                                    2.0.0.0    Storage
Function        Set-StorageProvider                                2.0.0.0    Storage
Function        Set-StorageSetting                                 2.0.0.0    Storage
Function        Set-StorageSubSystem                               2.0.0.0    Storage
Function        Set-StorageTier                                    2.0.0.0    Storage
Function        Set-TestInconclusive                               3.4.0      Pester
Function        Setup                                              3.4.0      Pester
Function        Set-VirtualDisk                                    2.0.0.0    Storage
Function        Set-Volume                                         2.0.0.0    Storage
Function        Set-VolumeScrubPolicy                              2.0.0.0    Storage
Function        Set-VpnConnection                                  2.0.0.0    VpnClient
Function        Set-VpnConnectionIPsecConfiguration                2.0.0.0    VpnClient
Function        Set-VpnConnectionProxy                             2.0.0.0    VpnClient
Function        Set-VpnConnectionTriggerDnsConfiguration           2.0.0.0    VpnClient
Function        Set-VpnConnectionTriggerTrustedNetwork             2.0.0.0    VpnClient
Function        Should                                             3.4.0      Pester
Function        Show-NetFirewallRule                               2.0.0.0    NetSecurity
Function        Show-NetIPsecRule                                  2.0.0.0    NetSecurity
Function        Show-StorageHistory                                2.0.0.0    Storage
Function        Show-VirtualDisk                                   2.0.0.0    Storage
Function        Start-AppBackgroundTask                            1.0.0.0    AppBackgroundTask
Function        Start-AutologgerConfig                             1.0.0.0    EventTracingManagement
Function        Start-Dtc                                          1.0.0.0    MsDtc
Function        Start-DtcTransactionsTraceSession                  1.0.0.0    MsDtc
Function        Start-EtwTraceSession                              1.0.0.0    EventTracingManagement
Function        Start-MpScan                                       1.0        ConfigDefender
Function        Start-MpScan                                       1.0        Defender
Function        Start-MpWDOScan                                    1.0        ConfigDefender
Function        Start-MpWDOScan                                    1.0        Defender
Function        Start-NetEventSession                              1.0.0.0    NetEventPacketCapture
Function        Start-PcsvDevice                                   1.0.0.0    PcsvDevice
Function        Start-ScheduledTask                                1.0.0.0    ScheduledTasks
Function        Start-StorageDiagnosticLog                         2.0.0.0    Storage
Function        Start-Trace                                        1.0.0.0    PSDiagnostics
Function        Start-WUScan                                       1.0.0.2    WindowsUpdateProvider
Function        Stop-DscConfiguration                              1.1        PSDesiredStateConfiguration
Function        Stop-Dtc                                           1.0.0.0    MsDtc
Function        Stop-DtcTransactionsTraceSession                   1.0.0.0    MsDtc
Function        Stop-EtwTraceSession                               1.0.0.0    EventTracingManagement
Function        Stop-NetEventSession                               1.0.0.0    NetEventPacketCapture
Function        Stop-PcsvDevice                                    1.0.0.0    PcsvDevice
Function        Stop-ScheduledTask                                 1.0.0.0    ScheduledTasks
Function        Stop-StorageDiagnosticLog                          2.0.0.0    Storage
Function        Stop-StorageJob                                    2.0.0.0    Storage
Function        Stop-Trace                                         1.0.0.0    PSDiagnostics
Function        Suspend-BitLocker                                  1.0.0.0    BitLocker
Function        Suspend-PrintJob                                   1.1        PrintManagement
Function        Suspend-StorageBusDisk                             1.0.0.0    StorageBusCache
Function        Sync-NetIPsecRule                                  2.0.0.0    NetSecurity
Function        T:
Function        TabExpansion2
Function        Test-Dtc                                           1.0.0.0    MsDtc
Function        Test-NetConnection                                 1.0.0.0    NetTCPIP
Function        Test-ScriptFileInfo                                1.0.0.1    PowerShellGet
Function        U:
Function        Unblock-FileShareAccess                            2.0.0.0    Storage
Function        Unblock-SmbShareAccess                             2.0.0.0    SmbShare
Function        Uninstall-Dtc                                      1.0.0.0    MsDtc
Function        Uninstall-Module                                   1.0.0.1    PowerShellGet
Function        Uninstall-Script                                   1.0.0.1    PowerShellGet
Function        Unlock-BitLocker                                   1.0.0.0    BitLocker
Function        Unregister-AppBackgroundTask                       1.0.0.0    AppBackgroundTask
Function        Unregister-ClusteredScheduledTask                  1.0.0.0    ScheduledTasks
Function        Unregister-IscsiSession                            1.0.0.0    iSCSI
Function        Unregister-PSRepository                            1.0.0.1    PowerShellGet
Function        Unregister-ScheduledTask                           1.0.0.0    ScheduledTasks
Function        Unregister-StorageSubsystem                        2.0.0.0    Storage
Function        Update-AutologgerConfig                            1.0.0.0    EventTracingManagement
Function        Update-Disk                                        2.0.0.0    Storage
Function        Update-DscConfiguration                            1.1        PSDesiredStateConfiguration
Function        Update-EtwTraceSession                             1.0.0.0    EventTracingManagement
Function        Update-HostStorageCache                            2.0.0.0    Storage
Function        Update-IscsiTarget                                 1.0.0.0    iSCSI
Function        Update-IscsiTargetPortal                           1.0.0.0    iSCSI
Function        Update-Module                                      1.0.0.1    PowerShellGet
Function        Update-ModuleManifest                              1.0.0.1    PowerShellGet
Function        Update-MpSignature                                 1.0        ConfigDefender
Function        Update-MpSignature                                 1.0        Defender
Function        Update-NetFirewallDynamicKeywordAddress            2.0.0.0    NetSecurity
Function        Update-NetIPsecRule                                2.0.0.0    NetSecurity
Function        Update-Script                                      1.0.0.1    PowerShellGet
Function        Update-ScriptFileInfo                              1.0.0.1    PowerShellGet
Function        Update-SmbMultichannelConnection                   2.0.0.0    SmbShare
Function        Update-StorageFirmware                             2.0.0.0    Storage
Function        Update-StoragePool                                 2.0.0.0    Storage
Function        Update-StorageProviderCache                        2.0.0.0    Storage
Function        V:
Function        W:
Function        Write-DtcTransactionsTraceSession                  1.0.0.0    MsDtc
Function        Write-PrinterNfcTag                                1.1        PrintManagement
Function        Write-VolumeCache                                  2.0.0.0    Storage
Function        X:
Function        Y:
Function        Z:
```





### more

---

`more`不用于*限制*输出，它用于对输出进行*分页*

* 空格 展开一页
* 回车展开 一行



![image-20221214100400501](PowerShell%206.0.assets/image-20221214100400501.png)

### less -？不知道如何使用

---

less函数 ，需要先安装 ，在管理员权限下安装

```powershell
 Find-Package pscx | Install-Package -Force
```

Powershell社区扩展具有一个名为“less”的方便函数，它使用less.exe的移植副本来实际处理分页，从而提供更完整的Unix样式function集。

![image-20221214101447682](PowerShell%206.0.assets/image-20221214101447682.png)

![image-20221214101506815](PowerShell%206.0.assets/image-20221214101506815.png)



慎重，不知道怎么使用 



## 03 Shell 命令 Cmdlet





```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Add-AppxPackage                                    2.0.1.0    Appx
Cmdlet          Add-AppxProvisionedPackage                         3.0        Dism
Cmdlet          Add-AppxVolume                                     2.0.1.0    Appx
Cmdlet          Add-BitsFile                                       2.0.0.0    BitsTransfer
Cmdlet          Add-CertificateEnrollmentPolicyServer              1.0.0.0    PKI
Cmdlet          Add-Computer                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-Content                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Add-History                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-JobTrigger                                     1.1.0.0    PSScheduledJob
Cmdlet          Add-KdsRootKey                                     1.0.0.0    Kds
Cmdlet          Add-LocalGroupMember                               1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Add-Member                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Add-PSSnapin                                       3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Add-Type                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Add-WebConfiguration                               1.0.0.0    WebAdministration
Cmdlet          Add-WebConfigurationLock                           1.0.0.0    WebAdministration
Cmdlet          Add-WebConfigurationProperty                       1.0.0.0    WebAdministration
Cmdlet          Add-WindowsCapability                              3.0        Dism
Cmdlet          Add-WindowsDriver                                  3.0        Dism
Cmdlet          Add-WindowsImage                                   3.0        Dism
Cmdlet          Add-WindowsPackage                                 3.0        Dism
Cmdlet          Backup-WebConfiguration                            1.0.0.0    WebAdministration
Cmdlet          Checkpoint-Computer                                3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Clear-Content                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Clear-EventLog                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Clear-History                                      3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Clear-IISCentralCertProvider                       1.1.0.0    IISAdministration
Cmdlet          Clear-IISConfigCollection                          1.1.0.0    IISAdministration
Cmdlet          Clear-Item                                         3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Clear-ItemProperty                                 3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Clear-KdsCache                                     1.0.0.0    Kds
Cmdlet          Clear-RecycleBin                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Clear-Tpm                                          2.0.0.0    TrustedPlatformModule
Cmdlet          Clear-Variable                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Clear-WebCentralCertProvider                       1.0.0.0    WebAdministration
Cmdlet          Clear-WebConfiguration                             1.0.0.0    WebAdministration
Cmdlet          Clear-WebRequestTracingSetting                     1.0.0.0    WebAdministration
Cmdlet          Clear-WebRequestTracingSettings                    1.0.0.0    WebAdministration
Cmdlet          Clear-WindowsCorruptMountPoint                     3.0        Dism
Cmdlet          Compare-Object                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Complete-BitsTransfer                              2.0.0.0    BitsTransfer
Cmdlet          Complete-DtcDiagnosticTransaction                  1.0.0.0    MsDtc
Cmdlet          Complete-Transaction                               3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Confirm-SecureBootUEFI                             2.0.0.0    SecureBoot
Cmdlet          Connect-PSSession                                  3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Connect-WSMan                                      3.0.0.0    Microsoft.WSMan.Management
Cmdlet          ConvertFrom-Csv                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertFrom-Json                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertFrom-SecureString                           3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          ConvertFrom-String                                 3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertFrom-StringData                             3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Convert-Path                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Convert-String                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertTo-Csv                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertTo-Html                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertTo-Json                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          ConvertTo-ProcessMitigationPolicy                  1.0.12     ProcessMitigations
Cmdlet          ConvertTo-SecureString                             3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          ConvertTo-TpmOwnerAuth                             2.0.0.0    TrustedPlatformModule
Cmdlet          ConvertTo-WebApplication                           1.0.0.0    WebAdministration
Cmdlet          ConvertTo-Xml                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Copy-Item                                          3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Copy-ItemProperty                                  3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Debug-Job                                          3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Debug-Process                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Debug-Runspace                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Delete-DeliveryOptimizationCache                   1.0.2.0    DeliveryOptimization
Cmdlet          Disable-AppBackgroundTaskDiagnosticLog             1.0.0.0    AppBackgroundTask
Cmdlet          Disable-ComputerRestore                            3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Disable-IISCentralCertProvider                     1.1.0.0    IISAdministration
Cmdlet          Disable-IISSharedConfig                            1.1.0.0    IISAdministration
Cmdlet          Disable-JobTrigger                                 1.1.0.0    PSScheduledJob
Cmdlet          Disable-LocalUser                                  1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Disable-PSBreakpoint                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Disable-PSRemoting                                 3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Disable-PSSessionConfiguration                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Disable-RunspaceDebug                              3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Disable-ScheduledJob                               1.1.0.0    PSScheduledJob
Cmdlet          Disable-TlsCipherSuite                             2.0.0.0    TLS
Cmdlet          Disable-TlsEccCurve                                2.0.0.0    TLS
Cmdlet          Disable-TlsSessionTicketKey                        2.0.0.0    TLS
Cmdlet          Disable-TpmAutoProvisioning                        2.0.0.0    TrustedPlatformModule
Cmdlet          Disable-WebCentralCertProvider                     1.0.0.0    WebAdministration
Cmdlet          Disable-WebGlobalModule                            1.0.0.0    WebAdministration
Cmdlet          Disable-WebRequestTracing                          1.0.0.0    WebAdministration
Cmdlet          Disable-WindowsErrorReporting                      1.0        WindowsErrorReporting
Cmdlet          Disable-WindowsOptionalFeature                     3.0        Dism
Cmdlet          Disable-WSManCredSSP                               3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Disconnect-PSSession                               3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Disconnect-WSMan                                   3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Dismount-AppxVolume                                2.0.1.0    Appx
Cmdlet          Dismount-WindowsImage                              3.0        Dism
Cmdlet          Enable-AppBackgroundTaskDiagnosticLog              1.0.0.0    AppBackgroundTask
Cmdlet          Enable-ComputerRestore                             3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Enable-IISCentralCertProvider                      1.1.0.0    IISAdministration
Cmdlet          Enable-IISSharedConfig                             1.1.0.0    IISAdministration
Cmdlet          Enable-JobTrigger                                  1.1.0.0    PSScheduledJob
Cmdlet          Enable-LocalUser                                   1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Enable-PSBreakpoint                                3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Enable-PSRemoting                                  3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Enable-PSSessionConfiguration                      3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Enable-RunspaceDebug                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Enable-ScheduledJob                                1.1.0.0    PSScheduledJob
Cmdlet          Enable-TlsCipherSuite                              2.0.0.0    TLS
Cmdlet          Enable-TlsEccCurve                                 2.0.0.0    TLS
Cmdlet          Enable-TlsSessionTicketKey                         2.0.0.0    TLS
Cmdlet          Enable-TpmAutoProvisioning                         2.0.0.0    TrustedPlatformModule
Cmdlet          Enable-WebCentralCertProvider                      1.0.0.0    WebAdministration
Cmdlet          Enable-WebGlobalModule                             1.0.0.0    WebAdministration
Cmdlet          Enable-WebRequestTracing                           1.0.0.0    WebAdministration
Cmdlet          Enable-WindowsErrorReporting                       1.0        WindowsErrorReporting
Cmdlet          Enable-WindowsOptionalFeature                      3.0        Dism
Cmdlet          Enable-WSManCredSSP                                3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Enter-PSHostProcess                                3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Enter-PSSession                                    3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Exit-PSHostProcess                                 3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Exit-PSSession                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Expand-WindowsCustomDataImage                      3.0        Dism
Cmdlet          Expand-WindowsImage                                3.0        Dism
Cmdlet          Export-Alias                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Export-BinaryMiLog                                 1.0.0.0    CimCmdlets
Cmdlet          Export-Certificate                                 1.0.0.0    PKI
Cmdlet          Export-Clixml                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Export-Console                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Export-Counter                                     3.0.0.0    Microsoft.PowerShell.Diagnostics
Cmdlet          Export-Csv                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Export-FormatData                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Export-IISConfiguration                            1.1.0.0    IISAdministration
Cmdlet          Export-ModuleMember                                3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Export-PfxCertificate                              1.0.0.0    PKI
Cmdlet          Export-ProvisioningPackage                         3.0        Provisioning
Cmdlet          Export-PSSession                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Export-StartLayout                                 1.0.0.2    StartLayout
Cmdlet          Export-StartLayoutEdgeAssets                       1.0.0.2    StartLayout
Cmdlet          Export-TlsSessionTicketKey                         2.0.0.0    TLS
Cmdlet          Export-Trace                                       3.0        Provisioning
Cmdlet          Export-WindowsCapabilitySource                     3.0        Dism
Cmdlet          Export-WindowsDriver                               3.0        Dism
Cmdlet          Export-WindowsImage                                3.0        Dism
Cmdlet          Find-Package                                       1.0.0.1    PackageManagement
Cmdlet          Find-PackageProvider                               1.0.0.1    PackageManagement
Cmdlet          ForEach-Object                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Format-Custom                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Format-List                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Format-SecureBootUEFI                              2.0.0.0    SecureBoot
Cmdlet          Format-Table                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Format-Wide                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Acl                                            3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Get-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-AppxDefaultVolume                              2.0.1.0    Appx
Cmdlet          Get-AppxPackage                                    2.0.1.0    Appx
Cmdlet          Get-AppxPackageManifest                            2.0.1.0    Appx
Cmdlet          Get-AppxProvisionedPackage                         3.0        Dism
Cmdlet          Get-AppxVolume                                     2.0.1.0    Appx
Cmdlet          Get-AuthenticodeSignature                          3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Get-BitsTransfer                                   2.0.0.0    BitsTransfer
Cmdlet          Get-Certificate                                    1.0.0.0    PKI
Cmdlet          Get-CertificateAutoEnrollmentPolicy                1.0.0.0    PKI
Cmdlet          Get-CertificateEnrollmentPolicyServer              1.0.0.0    PKI
Cmdlet          Get-CertificateNotificationTask                    1.0.0.0    PKI
Cmdlet          Get-ChildItem                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-CimAssociatedInstance                          1.0.0.0    CimCmdlets
Cmdlet          Get-CimClass                                       1.0.0.0    CimCmdlets
Cmdlet          Get-CimInstance                                    1.0.0.0    CimCmdlets
Cmdlet          Get-CimSession                                     1.0.0.0    CimCmdlets
Cmdlet          Get-Clipboard                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-CmsMessage                                     3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Get-Command                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-ComputerInfo                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-ComputerRestorePoint                           3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-Content                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-ControlPanelItem                               3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-Counter                                        3.0.0.0    Microsoft.PowerShell.Diagnostics
Cmdlet          Get-Credential                                     3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Get-Culture                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-DAPolicyChange                                 2.0.0.0    NetSecurity
Cmdlet          Get-Date                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-DeliveryOptimizationLog                        1.0.2.0    DeliveryOptimization
Cmdlet          Get-DeliveryOptimizationLogAnalysis                1.0.2.0    DeliveryOptimization
Cmdlet          Get-Event                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-EventLog                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-EventSubscriber                                3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-ExecutionPolicy                                3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Get-FormatData                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Help                                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-History                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-Host                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-HotFix                                         3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-IISAppPool                                     1.1.0.0    IISAdministration
Cmdlet          Get-IISCentralCertProvider                         1.1.0.0    IISAdministration
Cmdlet          Get-IISConfigAttributeValue                        1.1.0.0    IISAdministration
Cmdlet          Get-IISConfigCollection                            1.1.0.0    IISAdministration
Cmdlet          Get-IISConfigCollectionElement                     1.1.0.0    IISAdministration
Cmdlet          Get-IISConfigElement                               1.1.0.0    IISAdministration
Cmdlet          Get-IISConfigSection                               1.1.0.0    IISAdministration
Cmdlet          Get-IISServerManager                               1.1.0.0    IISAdministration
Cmdlet          Get-IISSharedConfig                                1.1.0.0    IISAdministration
Cmdlet          Get-IISSite                                        1.1.0.0    IISAdministration
Cmdlet          Get-IISSiteBinding                                 1.1.0.0    IISAdministration
Cmdlet          Get-InstalledLanguage                              1.0        LanguagePackManagement
Cmdlet          Get-Item                                           3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-ItemProperty                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-ItemPropertyValue                              3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-Job                                            3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-JobTrigger                                     1.1.0.0    PSScheduledJob
Cmdlet          Get-KdsConfiguration                               1.0.0.0    Kds
Cmdlet          Get-KdsRootKey                                     1.0.0.0    Kds
Cmdlet          Get-LocalGroup                                     1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Get-LocalGroupMember                               1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Get-LocalUser                                      1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Get-Location                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-Member                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Module                                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-NonRemovableAppsPolicy                         3.0        Dism
Cmdlet          Get-Package                                        1.0.0.1    PackageManagement
Cmdlet          Get-PackageProvider                                1.0.0.1    PackageManagement
Cmdlet          Get-PackageSource                                  1.0.0.1    PackageManagement
Cmdlet          Get-PfxCertificate                                 3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Get-PfxData                                        1.0.0.0    PKI
Cmdlet          Get-PmemDisk                                       1.0.0.0    PersistentMemory
Cmdlet          Get-PmemPhysicalDevice                             1.0.0.0    PersistentMemory
Cmdlet          Get-PmemUnusedRegion                               1.0.0.0    PersistentMemory
Cmdlet          Get-Process                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-ProcessMitigation                              1.0.12     ProcessMitigations
Cmdlet          Get-ProvisioningPackage                            3.0        Provisioning
Cmdlet          Get-PSBreakpoint                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-PSCallStack                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-PSDrive                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-PSHostProcessInfo                              3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-PSProvider                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-PSReadLineKeyHandler                           2.0.0      PSReadline
Cmdlet          Get-PSReadLineOption                               2.0.0      PSReadline
Cmdlet          Get-PSSession                                      3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-PSSessionCapability                            3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-PSSessionConfiguration                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-PSSnapin                                       3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Get-Random                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Runspace                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-RunspaceDebug                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-ScheduledJob                                   1.1.0.0    PSScheduledJob
Cmdlet          Get-ScheduledJobOption                             1.1.0.0    PSScheduledJob
Cmdlet          Get-SecureBootPolicy                               2.0.0.0    SecureBoot
Cmdlet          Get-SecureBootUEFI                                 2.0.0.0    SecureBoot
Cmdlet          Get-Service                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-SystemPreferredUILanguage                      1.0        LanguagePackManagement
Cmdlet          Get-TimeZone                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-TlsCipherSuite                                 2.0.0.0    TLS
Cmdlet          Get-TlsEccCurve                                    2.0.0.0    TLS
Cmdlet          Get-Tpm                                            2.0.0.0    TrustedPlatformModule
Cmdlet          Get-TpmEndorsementKeyInfo                          2.0.0.0    TrustedPlatformModule
Cmdlet          Get-TpmSupportedFeature                            2.0.0.0    TrustedPlatformModule
Cmdlet          Get-TraceSource                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Transaction                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-TroubleshootingPack                            1.0.0.0    TroubleshootingPack
Cmdlet          Get-TrustedProvisioningCertificate                 3.0        Provisioning
Cmdlet          Get-TypeData                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-UICulture                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Unique                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-Variable                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Get-WebAppDomain                                   1.0.0.0    WebAdministration
Cmdlet          Get-WebApplication                                 1.0.0.0    WebAdministration
Cmdlet          Get-WebAppPoolState                                1.0.0.0    WebAdministration
Cmdlet          Get-WebBinding                                     1.0.0.0    WebAdministration
Cmdlet          Get-WebCentralCertProvider                         1.0.0.0    WebAdministration
Cmdlet          Get-WebConfigFile                                  1.0.0.0    WebAdministration
Cmdlet          Get-WebConfiguration                               1.0.0.0    WebAdministration
Cmdlet          Get-WebConfigurationBackup                         1.0.0.0    WebAdministration
Cmdlet          Get-WebConfigurationLocation                       1.0.0.0    WebAdministration
Cmdlet          Get-WebConfigurationLock                           1.0.0.0    WebAdministration
Cmdlet          Get-WebConfigurationProperty                       1.0.0.0    WebAdministration
Cmdlet          Get-WebFilePath                                    1.0.0.0    WebAdministration
Cmdlet          Get-WebGlobalModule                                1.0.0.0    WebAdministration
Cmdlet          Get-WebHandler                                     1.0.0.0    WebAdministration
Cmdlet          Get-WebItemState                                   1.0.0.0    WebAdministration
Cmdlet          Get-WebManagedModule                               1.0.0.0    WebAdministration
Cmdlet          Get-WebRequest                                     1.0.0.0    WebAdministration
Cmdlet          Get-Website                                        1.0.0.0    WebAdministration
Cmdlet          Get-WebsiteState                                   1.0.0.0    WebAdministration
Cmdlet          Get-WebURL                                         1.0.0.0    WebAdministration
Cmdlet          Get-WebVirtualDirectory                            1.0.0.0    WebAdministration
Cmdlet          Get-WheaMemoryPolicy                               2.0.0.0    Whea
Cmdlet          Get-WIMBootEntry                                   3.0        Dism
Cmdlet          Get-WinAcceptLanguageFromLanguageListOptOut        2.0.0.0    International
Cmdlet          Get-WinCultureFromLanguageListOptOut               2.0.0.0    International
Cmdlet          Get-WinDefaultInputMethodOverride                  2.0.0.0    International
Cmdlet          Get-WindowsCapability                              3.0        Dism
Cmdlet          Get-WindowsDeveloperLicense                        1.0.0.0    WindowsDeveloperLicense
Cmdlet          Get-WindowsDriver                                  3.0        Dism
Cmdlet          Get-WindowsEdition                                 3.0        Dism
Cmdlet          Get-WindowsErrorReporting                          1.0        WindowsErrorReporting
Cmdlet          Get-WindowsImage                                   3.0        Dism
Cmdlet          Get-WindowsImageContent                            3.0        Dism
Cmdlet          Get-WindowsOptionalFeature                         3.0        Dism
Cmdlet          Get-WindowsPackage                                 3.0        Dism
Cmdlet          Get-WindowsReservedStorageState                    3.0        Dism
Cmdlet          Get-WindowsSearchSetting                           1.0.0.0    WindowsSearch
Cmdlet          Get-WinEvent                                       3.0.0.0    Microsoft.PowerShell.Diagnostics
Cmdlet          Get-WinHomeLocation                                2.0.0.0    International
Cmdlet          Get-WinLanguageBarOption                           2.0.0.0    International
Cmdlet          Get-WinSystemLocale                                2.0.0.0    International
Cmdlet          Get-WinUILanguageOverride                          2.0.0.0    International
Cmdlet          Get-WinUserLanguageList                            2.0.0.0    International
Cmdlet          Get-WmiObject                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Get-WSManCredSSP                                   3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Get-WSManInstance                                  3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Group-Object                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Alias                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-BinaryMiLog                                 1.0.0.0    CimCmdlets
Cmdlet          Import-Certificate                                 1.0.0.0    PKI
Cmdlet          Import-Clixml                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Counter                                     3.0.0.0    Microsoft.PowerShell.Diagnostics
Cmdlet          Import-Csv                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-LocalizedData                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-Module                                      3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Import-PackageProvider                             1.0.0.1    PackageManagement
Cmdlet          Import-PfxCertificate                              1.0.0.0    PKI
Cmdlet          Import-PSSession                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Import-StartLayout                                 1.0.0.2    StartLayout
Cmdlet          Import-TpmOwnerAuth                                2.0.0.0    TrustedPlatformModule
Cmdlet          Initialize-PmemPhysicalDevice                      1.0.0.0    PersistentMemory
Cmdlet          Initialize-Tpm                                     2.0.0.0    TrustedPlatformModule
Cmdlet          Install-Language                                   1.0        LanguagePackManagement
Cmdlet          Install-Package                                    1.0.0.1    PackageManagement
Cmdlet          Install-PackageProvider                            1.0.0.1    PackageManagement
Cmdlet          Install-ProvisioningPackage                        3.0        Provisioning
Cmdlet          Install-TrustedProvisioningCertificate             3.0        Provisioning
Cmdlet          Invoke-CimMethod                                   1.0.0.0    CimCmdlets
Cmdlet          Invoke-Command                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Invoke-CommandInDesktopPackage                     2.0.1.0    Appx
Cmdlet          Invoke-DscResource                                 1.1        PSDesiredStateConfiguration
Cmdlet          Invoke-Expression                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Invoke-History                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Invoke-Item                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Invoke-RestMethod                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Invoke-TroubleshootingPack                         1.0.0.0    TroubleshootingPack
Cmdlet          Invoke-WebRequest                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Invoke-WmiMethod                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Invoke-WSManAction                                 3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Join-DtcDiagnosticResourceManager                  1.0.0.0    MsDtc
Cmdlet          Join-Path                                          3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Limit-EventLog                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Measure-Command                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Measure-Object                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Mount-AppxVolume                                   2.0.1.0    Appx
Cmdlet          Mount-WindowsImage                                 3.0        Dism
Cmdlet          Move-AppxPackage                                   2.0.1.0    Appx
Cmdlet          Move-Item                                          3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Move-ItemProperty                                  3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-CertificateNotificationTask                    1.0.0.0    PKI
Cmdlet          New-CimInstance                                    1.0.0.0    CimCmdlets
Cmdlet          New-CimSession                                     1.0.0.0    CimCmdlets
Cmdlet          New-CimSessionOption                               1.0.0.0    CimCmdlets
Cmdlet          New-DtcDiagnosticTransaction                       1.0.0.0    MsDtc
Cmdlet          New-Event                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-EventLog                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-FileCatalog                                    3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          New-IISConfigCollectionElement                     1.1.0.0    IISAdministration
Cmdlet          New-IISSite                                        1.1.0.0    IISAdministration
Cmdlet          New-IISSiteBinding                                 1.1.0.0    IISAdministration
Cmdlet          New-Item                                           3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-ItemProperty                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-JobTrigger                                     1.1.0.0    PSScheduledJob
Cmdlet          New-LocalGroup                                     1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          New-LocalUser                                      1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          New-Module                                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-ModuleManifest                                 3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-NetIPsecAuthProposal                           2.0.0.0    NetSecurity
Cmdlet          New-NetIPsecMainModeCryptoProposal                 2.0.0.0    NetSecurity
Cmdlet          New-NetIPsecQuickModeCryptoProposal                2.0.0.0    NetSecurity
Cmdlet          New-Object                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-PmemDisk                                       1.0.0.0    PersistentMemory
Cmdlet          New-ProvisioningRepro                              3.0        Provisioning
Cmdlet          New-PSDrive                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-PSRoleCapabilityFile                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-PSSession                                      3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-PSSessionConfigurationFile                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-PSSessionOption                                3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-PSTransportOption                              3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          New-PSWorkflowExecutionOption                      2.0.0.0    PSWorkflow
Cmdlet          New-ScheduledJobOption                             1.1.0.0    PSScheduledJob
Cmdlet          New-SelfSignedCertificate                          1.0.0.0    PKI
Cmdlet          New-Service                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-TimeSpan                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-TlsSessionTicketKey                            2.0.0.0    TLS
Cmdlet          New-Variable                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          New-WebApplication                                 1.0.0.0    WebAdministration
Cmdlet          New-WebAppPool                                     1.0.0.0    WebAdministration
Cmdlet          New-WebBinding                                     1.0.0.0    WebAdministration
Cmdlet          New-WebFtpSite                                     1.0.0.0    WebAdministration
Cmdlet          New-WebGlobalModule                                1.0.0.0    WebAdministration
Cmdlet          New-WebHandler                                     1.0.0.0    WebAdministration
Cmdlet          New-WebManagedModule                               1.0.0.0    WebAdministration
Cmdlet          New-WebServiceProxy                                3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          New-Website                                        1.0.0.0    WebAdministration
Cmdlet          New-WebVirtualDirectory                            1.0.0.0    WebAdministration
Cmdlet          New-WindowsCustomImage                             3.0        Dism
Cmdlet          New-WindowsImage                                   3.0        Dism
Cmdlet          New-WinEvent                                       3.0.0.0    Microsoft.PowerShell.Diagnostics
Cmdlet          New-WinUserLanguageList                            2.0.0.0    International
Cmdlet          New-WSManInstance                                  3.0.0.0    Microsoft.WSMan.Management
Cmdlet          New-WSManSessionOption                             3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Optimize-AppxProvisionedPackages                   3.0        Dism
Cmdlet          Optimize-WindowsImage                              3.0        Dism
Cmdlet          Out-Default                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Out-File                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-GridView                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-Host                                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Out-Null                                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Out-Printer                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Out-String                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Pop-Location                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Protect-CmsMessage                                 3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Publish-DscConfiguration                           1.1        PSDesiredStateConfiguration
Cmdlet          Push-Location                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Read-Host                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Receive-DtcDiagnosticTransaction                   1.0.0.0    MsDtc
Cmdlet          Receive-Job                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Receive-PSSession                                  3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Register-ArgumentCompleter                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Register-CimIndicationEvent                        1.0.0.0    CimCmdlets
Cmdlet          Register-EngineEvent                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Register-ObjectEvent                               3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Register-PackageSource                             1.0.0.1    PackageManagement
Cmdlet          Register-PSSessionConfiguration                    3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Register-ScheduledJob                              1.1.0.0    PSScheduledJob
Cmdlet          Register-WmiEvent                                  3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-AppxPackage                                 2.0.1.0    Appx
Cmdlet          Remove-AppxProvisionedPackage                      3.0        Dism
Cmdlet          Remove-AppxVolume                                  2.0.1.0    Appx
Cmdlet          Remove-BitsTransfer                                2.0.0.0    BitsTransfer
Cmdlet          Remove-CertificateEnrollmentPolicyServer           1.0.0.0    PKI
Cmdlet          Remove-CertificateNotificationTask                 1.0.0.0    PKI
Cmdlet          Remove-CimInstance                                 1.0.0.0    CimCmdlets
Cmdlet          Remove-CimSession                                  1.0.0.0    CimCmdlets
Cmdlet          Remove-Computer                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-Event                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-EventLog                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-IISConfigAttribute                          1.1.0.0    IISAdministration
Cmdlet          Remove-IISConfigCollectionElement                  1.1.0.0    IISAdministration
Cmdlet          Remove-IISConfigElement                            1.1.0.0    IISAdministration
Cmdlet          Remove-IISSite                                     1.1.0.0    IISAdministration
Cmdlet          Remove-IISSiteBinding                              1.1.0.0    IISAdministration
Cmdlet          Remove-Item                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-ItemProperty                                3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-Job                                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Remove-JobTrigger                                  1.1.0.0    PSScheduledJob
Cmdlet          Remove-LocalGroup                                  1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Remove-LocalGroupMember                            1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Remove-LocalUser                                   1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Remove-Module                                      3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Remove-PmemDisk                                    1.0.0.0    PersistentMemory
Cmdlet          Remove-PSBreakpoint                                3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-PSDrive                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-PSReadLineKeyHandler                        2.0.0      PSReadline
Cmdlet          Remove-PSSession                                   3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Remove-PSSnapin                                    3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Remove-TypeData                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-Variable                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Remove-WebApplication                              1.0.0.0    WebAdministration
Cmdlet          Remove-WebAppPool                                  1.0.0.0    WebAdministration
Cmdlet          Remove-WebBinding                                  1.0.0.0    WebAdministration
Cmdlet          Remove-WebConfigurationBackup                      1.0.0.0    WebAdministration
Cmdlet          Remove-WebConfigurationLocation                    1.0.0.0    WebAdministration
Cmdlet          Remove-WebConfigurationLock                        1.0.0.0    WebAdministration
Cmdlet          Remove-WebConfigurationProperty                    1.0.0.0    WebAdministration
Cmdlet          Remove-WebGlobalModule                             1.0.0.0    WebAdministration
Cmdlet          Remove-WebHandler                                  1.0.0.0    WebAdministration
Cmdlet          Remove-WebManagedModule                            1.0.0.0    WebAdministration
Cmdlet          Remove-Website                                     1.0.0.0    WebAdministration
Cmdlet          Remove-WebVirtualDirectory                         1.0.0.0    WebAdministration
Cmdlet          Remove-WindowsCapability                           3.0        Dism
Cmdlet          Remove-WindowsDriver                               3.0        Dism
Cmdlet          Remove-WindowsImage                                3.0        Dism
Cmdlet          Remove-WindowsPackage                              3.0        Dism
Cmdlet          Remove-WmiObject                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Remove-WSManInstance                               3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Rename-Computer                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Rename-Item                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Rename-ItemProperty                                3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Rename-LocalGroup                                  1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Rename-LocalUser                                   1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Rename-WebConfigurationLocation                    1.0.0.0    WebAdministration
Cmdlet          Repair-WindowsImage                                3.0        Dism
Cmdlet          Reset-ComputerMachinePassword                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Reset-IISServerManager                             1.1.0.0    IISAdministration
Cmdlet          Resolve-DnsName                                    1.0.0.0    DnsClient
Cmdlet          Resolve-Path                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Restart-Computer                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Restart-Service                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Restart-WebAppPool                                 1.0.0.0    WebAdministration
Cmdlet          Restart-WebItem                                    1.0.0.0    WebAdministration
Cmdlet          Restore-Computer                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Restore-WebConfiguration                           1.0.0.0    WebAdministration
Cmdlet          Resume-BitsTransfer                                2.0.0.0    BitsTransfer
Cmdlet          Resume-Job                                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Resume-ProvisioningSession                         3.0        Provisioning
Cmdlet          Resume-Service                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Save-Help                                          3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Save-Package                                       1.0.0.1    PackageManagement
Cmdlet          Save-WindowsImage                                  3.0        Dism
Cmdlet          Select-Object                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-String                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Select-WebConfiguration                            1.0.0.0    WebAdministration
Cmdlet          Select-Xml                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Send-DtcDiagnosticTransaction                      1.0.0.0    MsDtc
Cmdlet          Send-MailMessage                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-Acl                                            3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Set-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-AppBackgroundTaskResourcePolicy                1.0.0.0    AppBackgroundTask
Cmdlet          Set-AppxDefaultVolume                              2.0.1.0    Appx
Cmdlet          Set-AppXProvisionedDataFile                        3.0        Dism
Cmdlet          Set-AuthenticodeSignature                          3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Set-BitsTransfer                                   2.0.0.0    BitsTransfer
Cmdlet          Set-CertificateAutoEnrollmentPolicy                1.0.0.0    PKI
Cmdlet          Set-CimInstance                                    1.0.0.0    CimCmdlets
Cmdlet          Set-Clipboard                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-Content                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-Culture                                        2.0.0.0    International
Cmdlet          Set-Date                                           3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-DeliveryOptimizationStatus                     1.0.2.0    DeliveryOptimization
Cmdlet          Set-DODownloadMode                                 1.0.2.0    DeliveryOptimization
Cmdlet          Set-DOPercentageMaxBackgroundBandwidth             1.0.2.0    DeliveryOptimization
Cmdlet          Set-DOPercentageMaxForegroundBandwidth             1.0.2.0    DeliveryOptimization
Cmdlet          Set-DscLocalConfigurationManager                   1.1        PSDesiredStateConfiguration
Cmdlet          Set-ExecutionPolicy                                3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Set-IISCentralCertProvider                         1.1.0.0    IISAdministration
Cmdlet          Set-IISCentralCertProviderCredential               1.1.0.0    IISAdministration
Cmdlet          Set-IISConfigAttributeValue                        1.1.0.0    IISAdministration
Cmdlet          Set-Item                                           3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-ItemProperty                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-JobTrigger                                     1.1.0.0    PSScheduledJob
Cmdlet          Set-KdsConfiguration                               1.0.0.0    Kds
Cmdlet          Set-LocalGroup                                     1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Set-LocalUser                                      1.0.0.0    Microsoft.PowerShell.LocalAccounts
Cmdlet          Set-Location                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-NonRemovableAppsPolicy                         3.0        Dism
Cmdlet          Set-PackageSource                                  1.0.0.1    PackageManagement
Cmdlet          Set-ProcessMitigation                              1.0.12     ProcessMitigations
Cmdlet          Set-PSBreakpoint                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-PSDebug                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Set-PSReadLineKeyHandler                           2.0.0      PSReadline
Cmdlet          Set-PSReadLineOption                               2.0.0      PSReadline
Cmdlet          Set-PSSessionConfiguration                         3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Set-ScheduledJob                                   1.1.0.0    PSScheduledJob
Cmdlet          Set-ScheduledJobOption                             1.1.0.0    PSScheduledJob
Cmdlet          Set-SecureBootUEFI                                 2.0.0.0    SecureBoot
Cmdlet          Set-Service                                        3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-StrictMode                                     3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Set-SystemPreferredUILanguage                      1.0        LanguagePackManagement
Cmdlet          Set-TimeZone                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-TpmOwnerAuth                                   2.0.0.0    TrustedPlatformModule
Cmdlet          Set-TraceSource                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-Variable                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Set-WebBinding                                     1.0.0.0    WebAdministration
Cmdlet          Set-WebCentralCertProvider                         1.0.0.0    WebAdministration
Cmdlet          Set-WebCentralCertProviderCredential               1.0.0.0    WebAdministration
Cmdlet          Set-WebConfiguration                               1.0.0.0    WebAdministration
Cmdlet          Set-WebConfigurationProperty                       1.0.0.0    WebAdministration
Cmdlet          Set-WebGlobalModule                                1.0.0.0    WebAdministration
Cmdlet          Set-WebHandler                                     1.0.0.0    WebAdministration
Cmdlet          Set-WebManagedModule                               1.0.0.0    WebAdministration
Cmdlet          Set-WheaMemoryPolicy                               2.0.0.0    Whea
Cmdlet          Set-WinAcceptLanguageFromLanguageListOptOut        2.0.0.0    International
Cmdlet          Set-WinCultureFromLanguageListOptOut               2.0.0.0    International
Cmdlet          Set-WinDefaultInputMethodOverride                  2.0.0.0    International
Cmdlet          Set-WindowsEdition                                 3.0        Dism
Cmdlet          Set-WindowsProductKey                              3.0        Dism
Cmdlet          Set-WindowsReservedStorageState                    3.0        Dism
Cmdlet          Set-WindowsSearchSetting                           1.0.0.0    WindowsSearch
Cmdlet          Set-WinHomeLocation                                2.0.0.0    International
Cmdlet          Set-WinLanguageBarOption                           2.0.0.0    International
Cmdlet          Set-WinSystemLocale                                2.0.0.0    International
Cmdlet          Set-WinUILanguageOverride                          2.0.0.0    International
Cmdlet          Set-WinUserLanguageList                            2.0.0.0    International
Cmdlet          Set-WmiInstance                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Set-WSManInstance                                  3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Set-WSManQuickConfig                               3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Show-Command                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Show-ControlPanelItem                              3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Show-EventLog                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Show-WindowsDeveloperLicenseRegistration           1.0.0.0    WindowsDeveloperLicense
Cmdlet          Sort-Object                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Split-Path                                         3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Split-WindowsImage                                 3.0        Dism
Cmdlet          Start-BitsTransfer                                 2.0.0.0    BitsTransfer
Cmdlet          Start-DscConfiguration                             1.1        PSDesiredStateConfiguration
Cmdlet          Start-DtcDiagnosticResourceManager                 1.0.0.0    MsDtc
Cmdlet          Start-IISCommitDelay                               1.1.0.0    IISAdministration
Cmdlet          Start-IISSite                                      1.1.0.0    IISAdministration
Cmdlet          Start-Job                                          3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Start-OSUninstall                                  3.0        Dism
Cmdlet          Start-Process                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Start-Service                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Start-Sleep                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Start-Transaction                                  3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Start-Transcript                                   3.0.0.0    Microsoft.PowerShell.Host
Cmdlet          Start-WebAppPool                                   1.0.0.0    WebAdministration
Cmdlet          Start-WebCommitDelay                               1.0.0.0    WebAdministration
Cmdlet          Start-WebItem                                      1.0.0.0    WebAdministration
Cmdlet          Start-Website                                      1.0.0.0    WebAdministration
Cmdlet          Stop-Computer                                      3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Stop-DtcDiagnosticResourceManager                  1.0.0.0    MsDtc
Cmdlet          Stop-IISCommitDelay                                1.1.0.0    IISAdministration
Cmdlet          Stop-IISSite                                       1.1.0.0    IISAdministration
Cmdlet          Stop-Job                                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Stop-Process                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Stop-Service                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Stop-Transcript                                    3.0.0.0    Microsoft.PowerShell.Host
Cmdlet          Stop-WebAppPool                                    1.0.0.0    WebAdministration
Cmdlet          Stop-WebCommitDelay                                1.0.0.0    WebAdministration
Cmdlet          Stop-WebItem                                       1.0.0.0    WebAdministration
Cmdlet          Stop-Website                                       1.0.0.0    WebAdministration
Cmdlet          Suspend-BitsTransfer                               2.0.0.0    BitsTransfer
Cmdlet          Suspend-Job                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Suspend-Service                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Switch-Certificate                                 1.0.0.0    PKI
Cmdlet          Tee-Object                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Test-Certificate                                   1.0.0.0    PKI
Cmdlet          Test-ComputerSecureChannel                         3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Test-Connection                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Test-DscConfiguration                              1.1        PSDesiredStateConfiguration
Cmdlet          Test-FileCatalog                                   3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Test-KdsRootKey                                    1.0.0.0    Kds
Cmdlet          Test-ModuleManifest                                3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Test-Path                                          3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Test-PSSessionConfigurationFile                    3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Test-WSMan                                         3.0.0.0    Microsoft.WSMan.Management
Cmdlet          Trace-Command                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Unblock-File                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Unblock-Tpm                                        2.0.0.0    TrustedPlatformModule
Cmdlet          Undo-DtcDiagnosticTransaction                      1.0.0.0    MsDtc
Cmdlet          Undo-Transaction                                   3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Uninstall-Language                                 1.0        LanguagePackManagement
Cmdlet          Uninstall-Package                                  1.0.0.1    PackageManagement
Cmdlet          Uninstall-ProvisioningPackage                      3.0        Provisioning
Cmdlet          Uninstall-TrustedProvisioningCertificate           3.0        Provisioning
Cmdlet          Unprotect-CmsMessage                               3.0.0.0    Microsoft.PowerShell.Security
Cmdlet          Unregister-Event                                   3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Unregister-PackageSource                           1.0.0.1    PackageManagement
Cmdlet          Unregister-PSSessionConfiguration                  3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Unregister-ScheduledJob                            1.1.0.0    PSScheduledJob
Cmdlet          Unregister-WindowsDeveloperLicense                 1.0.0.0    WindowsDeveloperLicense
Cmdlet          Update-FormatData                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Update-Help                                        3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Update-List                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Update-TypeData                                    3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Update-WIMBootEntry                                3.0        Dism
Cmdlet          Use-Transaction                                    3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Use-WindowsUnattend                                3.0        Dism
Cmdlet          Wait-Debugger                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Wait-Event                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Wait-Job                                           3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Wait-Process                                       3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Where-Object                                       3.0.0.0    Microsoft.PowerShell.Core
Cmdlet          Write-Debug                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Error                                        3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-EventLog                                     3.1.0.0    Microsoft.PowerShell.Management
Cmdlet          Write-Host                                         3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Information                                  3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Output                                       3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Progress                                     3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Verbose                                      3.1.0.0    Microsoft.PowerShell.Utility
Cmdlet          Write-Warning                                      3.1.0.0    Microsoft.PowerShell.Utility
```







### Get-Host ——获取表示当前主机程序的对象。

-----

#### 说明

> 获取一个对象，该对象表示承载Windows PowerShell的程序

默认显示内容包括 

1. Windows PowerShell 版本号以及

2. 主机使用的当前区域和语言设置，但是主**机对象包含大量信息**

   其中包括有关当前正在运行的 Windows PowerShell 版本以及 Windows PowerShell 的当前区域性和 UI 区域性的详细信息。 还可以使用此 cmdlet **自定义主机程序用户界面的功能**，例如文本和背景色。



#### 获取有关 PowerShell 控制台主机的信息

```powershell
Get-Host			#显示有关 PowerShell 控制台的信息
```

包括主机的名称、主机中运行的 PowerShell 版本以及当前区域性和 UI 区域性。

**Version**、**UI**、**CurrentCulture、CurrentUICulture**、**PrivateData** 和 **Runspace** 属性分别包含具有其他有用属性的对象



![image-20221209091019809](PowerShell%206.0.assets/image-20221209091019809.png)

#### 调整 PowerShell 窗口的大小

```powershell
$H = Get-Host
$Win = $H.UI.RawUI.WindowSize
$Win.Height = 10
$Win.Width  = 10
$H.UI.RawUI.Set_WindowSize($Win)    # 将Windows PowerShell窗口的大小调整为 10 行（10 个字符）
```

![image-20221209091354746](PowerShell%206.0.assets/image-20221209091354746.png)![image-20221209091416246](PowerShell%206.0.assets/image-20221209091416246.png)



#### 获取主机的 PowerShell 版本

```powershell
(Get-Host).Version | Format-List -Property *  #获取有关主机中运行的 Windows PowerShell 版本的详细信息  只能查看，不能修改
```

![image-20221209091642150](PowerShell%206.0.assets/image-20221209091642150.png)

Get-Host  的属性 Version对象，发送到 Format-List ，使用参数 Property 将版本对象的所有属性和属性值显示出来

#### 获取主机的当前区域性

```powershell
(Get-Host).CurrentCulture | Format-List -Property * # 获取有关主机中运行的 Windows PowerShell 的当前区域性设置的详细信息
```

![image-20221209092056755](PowerShell%206.0.assets/image-20221209092056755.png)

#### 获取当前区域性的 DateTimeFormat

```powershell
(Get-Host).CurrentCulture.DateTimeFormat | Format-List -Property *    #返回有关 Windows PowerShell 使用的当前区域性的 DateTimeFormat 的详细信息
```

主机对象的 **CurrentCulture** 属性包含 **CultureInfo 对象，而 CultureInfo** 对象又包含许多有用的属性。 其中， **DateTimeFormat** 属性包含具有许多有用属性的 **DateTimeFormatInfo** 对象









![image-20221209092301139](PowerShell%206.0.assets/image-20221209092301139.png)



#### 获取主机的 RawUI 属性

```powershell
(Get-Host).UI.RawUI | Format-List -Property *  # 显示主机对象的 RawUI 属性的属性。 通过更改这些值，可以更改主机程序的外观

# 在当前会话中有效。 若要更改所有会话控制台的背景色，请将该命令添加到 PowerShell 配置文件。
(Get-Host).UI.RawUI.BackgroundColor = "Black"  #设置 PowerShell 控制台的背景色
cls					# 清除屏幕并将整个屏幕更改为新颜色
```



#### 设置错误消息的背景色

此命令使用 `$Host` 自动变量，其中包含**当前主机程序的主机对象**。

 `Get-Host` 返回包含 `$Host` 的相同对象，因此可以**互换使用它们**。

此命令使用 **PrivateData** 属性 `$Host` 作为其 ErrorBackgroundColor 属性。 若要查看对象的所有属性，请参阅该对象 `$Host`中的所有属性

```powershell
$Host.PrivateData.ErrorBackgroundColor = "white"
```



#### 输入：管道 =>None

不能通过管道将输入传递给此 cmdlet。



#### 输出



`Get-Host` 返回 **System.Management.Automation.Internal.Host.InternalHost** 对象。



#### 补充

自动 `$Host` 变量包含返回的同一对象 `Get-Host` ，并且可以以相同的方式使用它。 

同样， `$PSCulture` 和 `$PSUICulture` 自动变量包含主机对象的 CurrentCulture 和 CurrentUICulture 属性包含的相同对象。 你可以交替使用这些功能

![image-20221209093424228](PowerShell%206.0.assets/image-20221209093424228.png)





#### 示例操作



* 编写一个脚本，设定以管理员的方式启动 PowerShell，并将该脚本导入到 PowerShell的配置文件中 
  1. 编写并保存脚本到桌面 

```powershell
Start-Process "$PSHOME\powershell.exe" -Verb runas # 以管理员的方式启动 
```

        2. 

```powershell
$a= (Get-Host).UI.RawUI
$a.WindowTitle="MCShadow"
$a.ForegroundColor="Green"
$b=$a.WindowSize
$b.Width="120"
$b.Height="57"
$a.WindowSize=$b
Import-Module D:\ShadowMod.psm1
Start-Shadow
Write-Host "Imported Module ShadowMod.psm1"
Write-Host "Ready to use Start or Stop Shadow”
```

3 . Save as Profile.ps1 under this path “C:\Users\userName\Documents\WindowsPowerShell”, if you can’t find this folder, please create it by manual.







### Out-File

----

* 简写 > 



### Out-GridView

```powershell
Get-Service | out-GridView
```

### Out-Host

----



### Out-Null



### Out-String







## 04 Shell 脚本 Script

> Get-Command -CommandType Script		#显示PowerShell搜索路径中的脚本 

https://blog.51cto.com/u_15127576/3271530



### 创建脚本

以下 切换到 F：进行演练 

```powershell
# 打印输出 Hello
$a = echo "Hello" 
$a
echo $a > a.ps1
# 这里面 a.ps1 记事本打开里面只有 Hello这个输出，而不是 echo "Hello" 的代码
```

这里可以这样 ：

手动修改 a.txt文件 ，里面写入  echo “Hello" 然后 改为a.ps1 ，运行

```powershell
. \a.ps1
```



```powershell
# 输出第一个脚本
@'
Get-Date
$Env:CommonProgramFiles
#Script End
"files count"
(ls).count
#script Really End
'@ >MyScript.ps1

.\MyScript.ps1
```

![image-20221207100057252](PowerShell%206.0.assets/image-20221207100057252.png)







### 基础知识



* 代码必须放在闭合的引号中。这样的书写方式一旦在脚本内部也有引号时，是一件很痛苦的事
* 以 @‘开头，以’@结束.任何文本都可以存放在里面，哪怕是一些特殊字符，空号，白空格。但是如果您不小心将**单引号**写成了双引号，Powershell将会把里面的变量进行解析

*  最快捷的就是通过 PowerShell ISE 编辑器进行创建脚本



### 运行脚本

运行PowerShell脚本 **使用相对路径，或者绝对路径**

```powershell
dir

.\MyScript.ps1
```





### 执行策略限制
Powershell一般初始化情况下都会禁止脚本执行。脚本能否执行取决于Powershell的执行策略。

只有管理员才有权限更改这个策略。非管理员会报错。
查看脚本执行策略，可以通过 Get-ExecutionPolicy
更改脚本执行策略，可以通过 Set-ExecutionPolicy UnRestricted


脚本执行策略类型为：Microsoft.PowerShell.ExecutionPolicy


Unrestricted:权限最高，可以不受限制执行任何脚本。
Default:为Powershell默认的策略：Restricted，不允许任何脚本执行。
AllSigned：所有脚本都必须经过签名才能在运行。
RemoteSigned：本地脚本无限制，但是对来自网络的脚本必须经过签名



### 给脚本传递参数

怎样将一个脚本稍作润色，让它能够根据用户的输入，处理并输出相应的结果，而不是只产生一成不变的输出。怎样将参数传递给脚本



**$args** 返回所有的参数

传递 给一个函数或者一个脚本的参数 都保存在 $args变量中

打开记事本，输入  

```powershell
Write-Host "Hello,$args"
```

保存后 通过控制台 执行脚本

![image-20221207101343108](PowerShell%206.0.assets/image-20221207101343108.png)

默认情况下，传递给一个Powershell脚本的参数类型为数组



![image-20221207101557434](PowerShell%206.0.assets/image-20221207101557434.png)

上面的文本中包含多个连续的空格，可是当脚本把参数输出时却不存在连续的空格了。那是因为脚本会把文本根据白空格截断并转换成数组。如果不想文本被当成数组那就把它放在引号中。

![image-20221207101740044](PowerShell%206.0.assets/image-20221207101740044.png)

![image-20221207101807486](PowerShell%206.0.assets/image-20221207101807486.png)

在$args中逐个访问参数
因为$args是一个数组，自然可以通过索引访问数组的每一个元素。可以将MyScript.sp1的内容改为

把上面的使用$args的语句进行注释掉

```powershell
For ($i = 0; $i -lt $args.Count; $i++)
{
	Write-Host "parameter $i : $($args[$i])"
}
```

![image-20221207102226983](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/e245b27ebaff55d1714f7f2c0956a24e-image-20221207102226983-340404.png)

![image-20221207102606511](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/de67c13a9d68dc28e4f07d207e238693-image-20221207102606511-9ca65e.png)

### 参数顺序的重要性 

![image-20221207103130534](PowerShell%206.0.assets/image-20221207103130534.png)

* 解决办法： 给参数指定名称 



![image-20221207103826174](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/298823529ef3d9068772b98c845082b6-image-20221207103826174-8f49a9.png)



==查看脚本内部需要传入的变量==？

### 验证参数



给脚本的参数绑定数据类型，绑定帮助信息。一旦脚本缺少参数，或者输入的参数类型不正确，就提醒用户

![image-20221207104526635](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/7f58016007e9267a7ca2d7ab1ae52f4c-image-20221207104526635-3ac9e4.png)



### 变量作用域

Powershell默认使用**全局作用域global:** ，但是在函数和脚本中分别使用**函数作用域function:**和**脚本作用域script:** 。
一旦脚本执行结束，存在于脚本作用域的变量也会消失。但是有一点，如果一个变量在**脚本外定义**，在脚本内没有定义，在脚本内使用时会把**外面的变量引渡过来**

但是脚本内的变量不会影响脚本外的变量

做个示例:脚本内部和外部同时设定$Temp 修改内外部 赋值，看彼此是否会改变，发现不会改变





### 可读性： 拆分 函数和 类库



1. 函数：把实现一些小功能的代码写成一个函数，不仅可以增强代码的可读性，还可以很方便的重用。一旦你创建了一个实现特定功能的函数，也可以下次在其它脚本中使用。
   类库：把需要的函数嵌入进类库中，就不用每次在执行脚本时拷贝函数，并且还可以在需要时扩充它。另外以函数的方式构建类库，还可以让你更专注特定功能的具体实现，降低脚本开发的复杂度。

Powershell中的函数必须先定义后使用

```powershell
# 脚本接收一个正整数参数，然后通过Factorial函数求阶乘
```

![image-20221207105809895](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/5410e5a1c54e3020969abce34058fb9b-image-20221207105809895-9b148e.png)

2、将脚本分为工作脚本和类库
真正的脚本开发需要处理的问题可能包含许多函数。如果在一个脚本的开头定义许多函数，脚本会显得很凌乱。把函数和工作脚本分开，可以隔离函数，使它不容易被修改。



将Factorial函数保存在a.ps1

```powershell
Function Factorial([int]$n)
{
    $total=1
    for($i=1;$i -le $n;$i++)
    {
        $total*=$i
    }
    return $total
}
```

将工作脚本设为 b.ps1

```powershell
param([int]$n=$(throw "请输入一个正整数"))
. .\PSLib.ps1 # 两个脚本放在同级目录下面 
Factorial $n
```

![image-20221207110607304](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/7d3bf47712b40c3fa4a4311460862854-image-20221207110607304-c94e5f.png) 



3. 类库脚本集中存放
   在开始使用类库脚本工作之前，最好先制定出一个存储脚本类库的策略。一种方法是和工作脚本存放在一起，可以使用相对路径；另一种方法是分开存放，加载时就得使用绝对路径了。最好在当前用户的私人目录中存放脚本，相对来说比较安全



### 创建管道脚本



采用低速顺序模式，还是高速流模式，这取决于具体的编程实现。



1. 低速顺序模式



在脚本中使用管道，脚本收集上一个语句的执行结果，默认保存在$input自动变量中。但是直到**上一条语句完全执行彻底**，管道脚本才会执行



执行脚本：
ls $env:windir | .pipeline.ps1
如果这样执行：
ls $env:windir -Recurse | .pipeline.ps1
控制台会被冻结，因为存储的中间结果在玩命的吃内存。这个也是低速顺序模式的**缺点**

![image-20221207111731715](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/f957da4b4b0191a251f45589f7c64e97-image-20221207111731715-ded616.png)



2. 高速流模式

   在Powershell脚本的处理中，绝大多数情况下遇到的都是集合，一旦上一条命令产生一个中间结果，下一条命令就对这个中间结果及时处理，及时释放资源。这样可以节省内存，也减少了用户的等待时间。在处理大量数据时，尤其值得推荐。高速流模式的管道定义包括三部分：begin,process,end。上面的描述中提到了中间结果，中间结果保存在$_自动化变量中



![image-20221207112701469](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/79afbe55a5dedd9800ed7a928823e8f0-image-20221207112701469-423bbc.png)









### 自动执行脚本之profile
在Powershell控制台的许多更改只会在当前会话有效。一旦关闭当前控制台，你自定义地所有别名、函数、和其它改变将会消失，除非将更改保存在windows环境变量中。这也就是为什么我们需要profile来保存一些基本的初始化工作。

四种不同的profile脚本
Powershell支持四种可以用来初始化任务的profile脚本。应用之前要弄清楚你的初始化是当前用户个人使用，还是所有用户。如果是个人使用，可以使用”当前用户profile“，但是如果你的初始化任务是针对所有用户，可是使用“所有用户profile”。
![image-20221207105353303](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/ec330f4f638aa9aff33c1b65440ef7ef-image-20221207105353303-876a0f.png)
我们注意到上面的四种profile有两个private。一旦声明为private，只有个microsoft的Powershell自身才会去调用，不会对其它引用powershell的组件有效。

创建自己的profile
Profile脚本并不是强制性的，换言之，profile可有可无。下面会很方便的创建自己的profile。 在控制台执行： notepad $profile 如果不存在profile默认会创建，在打开的记事本中输入： Set-Alias edit notepad.exe
也就是给notepad添加edit别名，保存关闭，之后重启控制台，输入： edit
控制台会打开记事本打开，可见edit别名已经生效。

创建全局profile
创建全局的profile也是很容易的，如上，只是文件的位置稍有改变； 需要注意的是，创建全局profile需要管理员权限，没有管理员权限，该文件或者文件夹拒绝访问。还有一点也须注意：在vista系统中，即使你拥有管理员权限，但是没有通过administrator登录，并且系统没有禁用UAC，也是拒绝更改的。除非你鼠标右键单击Powershell快捷方式，以管理员权限运行。







## 05CMD原生命令-Windows使用技巧

-----

![image-20221213093703572](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/0fe09aee2ba9033db066d26a095f9885-image-20221213093703572-8e426a.png)

![image-20221213094525958](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/9471ba7d8e6c8deff2aa67591b8cc367-image-20221213094525958-77f76b.png)



![image-20221213094553341](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/6466b9ee07aaaa73f02f970a6f9112bf-image-20221213094553341-ee25e8.png)



![image-20221213094652479](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/ee28af30593b354a244e4085244141b4-image-20221213094652479-d754c5.png)



![image-20221213094714610](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/f0916130c32ec22f8487be4e94e26d3c-image-20221213094714610-1efe39.png)



----

















### chrome

-----

这个不是内置的 ，但是可以设置

未设置前，可以通过  start chrome启动

## 业务/事务处理 

---

 ### 第三章 使用帮助系统 问题

----

![image-20221208144918911](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/e2755f396cec267e75a4f978e4a4be3f-image-20221208144918911-13d401.png)

![image-20221208144931626](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/4641e24be9f898ae5d4667df42938013-image-20221208144931626-b8a244.png)





![image-20221208144942540](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/0f6f4786bcf5ab4587f2ec6f09bbd464-image-20221208144942540-091477.png)



### 第四章 运行命令

![image-20221213095146554](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/0a57295d70e5d149ca681436d27fdd8d-image-20221213095146554-d2c08d.png)

### 第五章 使用提供程序

![image-20221214095340799](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/ded652e3906711ea8289d42f7aa83fbf-image-20221214095340799-09567a.png)

![image-20221214095501184](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/1cf22543278e14a189ebe6cf562055e4-image-20221214095501184-cc3413.png)



![image-20221214095550361](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/5abd5646afaa548c950445778a92e22f-image-20221214095550361-ae5c03.png)

![image-20221214095559264](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/8833966e766e8ba3ef43c87a077342cf-image-20221214095559264-f6c39e.png)



### 第六章 管道：连接命令

---

![image-20221214104322212](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/b97dc42415b2c4cff087ea1fcd3ba133-image-20221214104322212-e8610e.png)

![image-20221214104329161](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/5bdccdfec30a1b698df8f7945e7520fd-image-20221214104329161-c4b818.png)



![image-20221214104344588](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/e66217036ee7e8f349c00042fddfdf74-image-20221214104344588-2e8554.png)

![image-20221214104354411](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/c475f5181f5cc20463b5e9501c31f6fb-image-20221214104354411-b1f91e.png)



### 24章 正则表达式解析文本

![image-20221216103136267](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/8da27f3980be21a6c639359356926dab-image-20221216103136267-0f49fb.png)![image-20221216103147338](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/c992031b9809bc0189d87ef470e28773-image-20221216103147338-c6c65c.png)

![image-20221216103201479](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/96efa2deb95c28e269a92bd72e6df97b-image-20221216103201479-74e175.png)











### 自动化处理 数据密集任务

如果要对大量的数据进行处理简单的任务，可以把数据保存在一个CSV文件里面，使用Import-Csv来导入数据，导入后为每一行自动创建对象，并将列的名字作为对象的属性，之后用foreach对数据的每一项进行操作



![image-20221208114557354](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/c224f21b23e81f2af642fc1625879487-image-20221208114557354-57a334.png)



### 显示C盘 和可用空间大小



```powershell
 Get-WmiObject win32_logicaldisk -filter "DeviceID='C:'"
```

![image-20221209102218210](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/192286a66f39499d96830c38088ffb6b-image-20221209102218210-f78b6d.png)

![image-20221209102728504](https://raw.githubusercontent.com/Rocky-houjinsong/PictureBed/main/img/2023/05/09/2227e9d8c26b964835d9e9e1792458b8-image-20221209102728504-2edf2e.png)



https://blog.51cto.com/u_15127576/3271530



Add By SongHouJin 2022年12月7日11:40:14 HangZhou 

### 删除



### 查看笔记本内存条所有信息

---

```powershell
 Get-CimInstance Win32_PhysicalMemory  # PowerShell
 wmic 
 memorychip
```



### 窗体制作

----

```powershell
##使用.NET
[void] [System.Reflection.Assembly]::LoadWithPartialName("System.Windows.Forms")
[void] [System.Reflection.Assembly]::LoadWithPartialName("System.Drawing")

### Add Forms ###
$MainForm = New-Object System.Windows.Forms.Form
$MainForm.Text = "First Form"
$MainForm.Size = New-Object System.Drawing.Size(400,200)
$MainForm.KeyPreview = $True
$MainForm.FormBorderStyle = "1"
$MainForm.MaximizeBox = $false
$MainForm.StartPosition = "CenterScreen"
$MainForm.TopMost =$true
### Add Buttons ###
$Close = New-Object System.Windows.Forms.Button
$Close.Size = New-Object System.Drawing.Size(75,25)
$Close.Location = New-Object System.Drawing.Size(165,110)
$Close.Text = "Close"
$MainForm.Controls.Add($Close)
$Close.add_click({[void] $MainForm.Close()})

### Add Lables ###
$Text = New-Object System.Windows.Forms.Label
$Text.Size = New-Object System.Drawing.Size(300,50)
$Text.Location = New-Object System.Drawing.Size(70,50)
$Text.Text = "Press the button to close this window"
$MainForm.Controls.Add($Text)

### Activate Form
$MainForm.Add_Shown({$MainForm.Activate()})
[void] $MainForm.ShowDialog()
```



### 实现输入选择

----

在bat中，如果我要实现这样的功能

当用户输入1的时候，执行显示abcd；当用户输入2的时候，执行显示efgh

```powershell
$UserInput = Read-Host
Switch($UserInput) {"1" {Write-Host "abcd" } ; "2" { Write-Host "efgh" } }
```



### 周五乐趣：使用 ChatGPT 编写 PowerShell 脚本 发表于

### [2022 年 12 月 16 日](https://jdhitsolutions.com/blog/powershell/9187/friday-fun-powershell-scripting-with-chatgpt/)

----

“编写一个 PowerShell 函数，在屏幕中央以交替颜色显示“Hello, World”。包含一个参数以使消息闪烁

```powershell
function Show-HelloWorld {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [ValidateSet("On", "Off")]
        [string]$Blink
    )

    # Clear the screen
    Clear-Host

    # Set the text colors to alternate between red and green
    $colors = @("Red", "Green")
    $colorIndex = 0

    # Set the cursor position to the center of the screen
    $x = (Get-Host).UI.RawUI.WindowSize.Width / 2
    $y = (Get-Host).UI.RawUI.WindowSize.Height / 2

    # Set the cursor position and display the message
    Write-Host "Hello, World" -ForegroundColor $colors[$colorIndex] -NoNewline
    $host.UI.RawUI.CursorPosition = New-Object System.Management.Automation.Host.Coordinates $x, $y

    # Toggle the text color and blink the message if the Blink parameter is set to "On"
    while ($Blink -eq "On") {
        Start-Sleep -Milliseconds 500
        $colorIndex = ($colorIndex + 1) % 2
        Write-Host "`b" -NoNewline
        Write-Host "Hello, World" -ForegroundColor $colors[$colorIndex] -NoNewline
    }
}
```

一个函数创建一个 Julia 集



```powershell
function Show-JuliaSet {
    [cmdletbinding()]
    param (
      [double]$cReal = -0.8,
      [double]$cImag = 0.156,
      [int]$width = 80,
      [int]$height = 24,
      [int]$maxIterations = 256
    )

    # Create the Julia set function
    function julia {
      param (
        [double]$cReal,
        [double]$cImag,
        [int]$width,
        [int]$height,
        [int]$maxIterations
      )

      # Calculate the pixel values for the Julia set
      $pixels = for ($y = 0; $y -lt $height; $y++) {
        for ($x = 0; $x -lt $width; $x++) {
          # Map the pixel coordinates to the complex plane
          $zReal = [math]::Round((($x / $width) * 3.5) - 2.5, 2)
          $zImag = [math]::Round((($y / $height) * 2) - 1, 2)

          # Iterate the Julia set equation
          $iteration = 0
          while (($zReal * $zReal + $zImag * $zImag) -lt 4) {
            $tempReal = $zReal * $zReal - $zImag * $zImag + $cReal
            $zImag = 2 * $zReal * $zImag + $cImag
            $zReal = $tempReal
            $iteration++
            if ($iteration -ge $maxIterations) {
              break
            }
          }

          # Return the number of iterations as a pixel value
          $iteration
        }
      }

      # Print the Julia set to the console
      for ($y = 0; $y -lt $height; $y++) {
        for ($x = 0; $x -lt $width; $x++) {
          $pixel = $pixels[$y * $width + $x]
          if ($pixel -eq $maxIterations) {
            Write-Host "." -NoNewline
          } else {
            Write-Host " " -NoNewline
          }
        }
        Write-Host ""
      }
    }

   # Call the Julia set function
  julia -cReal $cReal -cImag $cImag -width $width -height $height -maxIterations $maxIterations
}

### 输入运行 
Show-MandelbrotSet -width 88 -heigh 20 -maxIterations 32
```





### 一个 WPF 倒数计时器

### 发表于[2022 年 10 月 19 日](https://jdhitsolutions.com/blog/powershell/9154/a-wpf-countdown-timer/)



https://jdhitsolutions.com/blog/powershell/9154/a-wpf-countdown-timer/haun 



### 问：在powershell中，如何打开【win10---》设置---》选项】图形界面？

----

于 QQ群中 搜罗下来



```powershell
答：Start-Process -FilePath 'ms-settings:batterysaver'

ms-settings打开设置
ms-settings:batterysaver节电模式
ms-settings:batterysaver-settings节电模式设置
ms-settings:batterysaver-usagedetails电池用量
ms-settings:personalization个性化
ms-settings:colors个性化-颜色
ms-settings:personalization-colors个性化-颜色
ms-settings:personalization-background个性化-背景
ms-settings:lockscreen个性化-锁屏
ms-settings:personalization-start个性化-开始
ms-settings:taskbar个性化-任务栏
ms-settings:themes个性化-主题
ms-settings:network 网络和Internet
ms-settings:datausage数据使用量
ms-settings:network-mobilehotspot 移动热点
ms-settings:mobilehotspot移动热点
ms-settings:network-proxy代理
ms-settings:network-vpnVPN
ms-settings:network-airplanemode飞行模式
ms-settings:airplanemode 飞行模式
ms-settings:network-dialup拨号
ms-settings:network-ethernet以太网
ms-settings:network-status状态
ms-settings:network-wifi WiFi
ms-settings:wifiWiFi
ms-settings:network-wifisettings管理已知网络
ms-settings:dateandtime时间和语言-日期和时间
ms-settings:speech语音
ms-settings:regionlanguage区域和语言
ms-settings:easeofaccess-closedcaptioning轻松使用-隐藏式字幕
ms-settings:easeofaccess-highcontrast高对比度
ms-settings:easeofaccess-magnifier放大镜
ms-settings:easeofaccess-narrator讲述人
ms-settings:easeofaccess-otheroptions其他选项
ms-settings:easeofaccess-keyboard键盘
ms-settings:easeofaccess-mouse鼠标
ms-settings:emailandaccounts 账户-电子邮件和应用账户
ms-settings:yourinfo 你的信息
ms-settings:sync同步你的设置
ms-settings:otherusers家庭和其他人员
ms-settings:signinoptions 登录选项
ms-settings:workplace访问工作单位或学校
ms-settings:privacy隐私
ms-settings:privacy-accountinfo账户信息
ms-settings:privacy-backgroundapps后台应用
ms-settings:privacy-calendar日历
ms-settings:privacy-callhistory通话记录
ms-settings:privacy-contacts联系人
ms-settings:privacy-customdevices其他设备
ms-settings:privacy-email 电子邮件
ms-settings:privacy-feedback反馈
ms-settings:privacy-location位置
ms-settings:privacy-messaging 消息传送
ms-settings:privacy-microphone麦克风
ms-settings:privacy-radios 无线电收发器
ms-settings:privacy-speechtyping语音、墨迹书写和键入
ms-settings:privacy-webcam相机
ms-settings:windowsinsider更新和安全-获取Insider Preview版本
ms-settings:windowsupdateWindows更新
ms-settings:windowsupdate-history 更新历史
ms-settings:windowsupdate-options 高级设置
ms-settings:windowsupdate-restartoptions重启选项
ms-settings:windowsupdate-action 检查更新
ms-settings:backup 备份
ms-settings:activation激活
ms-settings:developers针对开发人员
ms-settings:recovery 恢复
ms-settings:windowsdefender Windows Defender
ms-settings:appsfeatures 系统-应用和功能
ms-settings:notifications通知和操作
ms-settings:powersleep电源和睡眠
ms-settings:defaultapps默认应用
ms-settings:phone-defaultapps 默认应用(Win10 Mobile)
ms-settings:deviceencryption关于
ms-settings:about关于
ms-settings:display显示
ms-settings:screenrotation显示
ms-settings:multitasking多任务
ms-settings:maps离线地图
ms-settings:maps-downloadmaps下载地图
ms-settings:storagesense存储
ms-settings:optionalfeatures管理可选功能
ms-settings:project投影到这台电脑
ms-settings:tabletmode平板模式
ms-settings:autoplay 自动播放
ms-settings:bluetooth蓝牙
ms-settings:connecteddevices已连接设备
ms-settings:mousetouchpad鼠标和触摸板
ms-settings:usb USB
ms-settings:pen笔
ms-settings:printers打印机和扫描仪
ms-settings:typing输入
ms-settings:wheel滚轮
```



### 问：python是shell的救星吗？ linux版powershell ≈ bash + python”？

答：
python对于运维来讲，有3个癌症：1**用命令前**需要import库。2没有shell级别命令行。3管道用起来太麻烦。
可以简单把ps理解为没有这三个癌症的python。
1powershell的自动import太好用，99.9%不用手动import。即便命令函数重名，也可以用库名/命令名（函数名）来解决。如：Microsoft.PowerShell.Management\Get-ChildItem
3写py【管道】脚本，需要import，open，read，close。而powershell，bash，使用管道数据，不需要这些步骤。
假如py消掉了这三个癌症，shell就没啥存在必要了。这就是powershell比py，比shell的优势。



### PS读取文件的几种方法.txt

下面的消耗时间是基于一个大小为14M的文件来测试。

1. 一般 Get-Content ``` Get-Content a.txt | ForEach-Object { ... } ``` [消耗时间(MS)] 7494.0185 流模式（省内存），用了管道（慢）

2. Get-Content 加 -ReadCount 0 

   ` $lines = Get-Content a.txt -ReadCount 0 foreach ($line in $lines) { ... } ` [消耗时间(MS)] 521.4067 一次性读入（耗内存），不用管道（快）

3. Net平台的[System.IO.File]::ReadLines ``` $lineStream = [System.IO.File]::ReadLines("$pwd\a.txt") foreach ($line in $lineStream) { ... } ``` [消耗时间(MS)] 500.289 流模式（省内存），不用管道（快）

4. Get-Content 加 -Raw ``` $allText = Get-Content a.txt -Raw ``` [消耗时间(MS)] 152.0455 一次性读入（耗内存），不用管道（快） 但是，这里的 $allText 是一个string，而不是string数组，所以无法做行迭代处理

