[Toc]

---

# 学习指导

## 打卡 

> 时间 学习内容  待完成部分

:hourglass_flowing_sand:  2023-1-30 23:04:55  重置以往笔记，以自己总结为中心 

:hourglass: 2023-1-31 15:00:26  重新布局 笔记内容



## 任务清单

:black_square_button:  将常用的全局快捷键 ，输入到里面

:white_check_mark: 已完成的部分

## 学习资源

* 《PowerShell 6.0》
* 《PowerShell应用手册》

## 注意事项

* 在PowerShell特性中展现的 解决方案是直接使用的，但是详细说明要到文档中进行查看
  同时，文档直接查看在线最新版本的内容，不可以按照过往的字母次序，按照使用场景和使用特点来学习

# 预置知识

## 概述

### 什么是PowerShell



一种**跨平台**的任务**自动化解决方案**，

由**命令行 shell**、**脚本语言**和**配置管理框架**组成。 

PowerShell 在 Windows、Linux 和 macOS 上运行。

#### 命令行Shell

PowerShell 接受并返回 .NET 对象

- 可靠的命令行[历史记录](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_history)
- Tab 自动补全和命令预测（请参阅 [about_PSReadLine](https://learn.microsoft.com/zh-cn/powershell/module/psreadline/about/about_psreadline)）
- 支持命令和参数[别名](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_aliases)
- 用于链接命令的[管道](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_pipelines)
- 控制台内[帮助](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/get-help)系统，类似于 Unix `man` 页面

#### 脚本语言

* 通常用于自动执行系统管理
*  CI/CD 环境中生成、测试和部署解决方案

在 .NET 公共语言运行时 (CLR) 上构建的
所有输入和输出都是 .NET 对象。 无需分析文本输出即可从输出中提取信息

- 可通过[函数](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_functions_advanced)、[类](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_classes)、[脚本](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_scripts)和[模块](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_modules)进行扩展
- 便于输出的可扩展[格式系统](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_format.ps1xml)
- 用于创建动态类型的可扩展[类型系统](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.core/about/about_types.ps1xml)
- 对常用数据格式（例如 [CSV](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.utility/convertfrom-csv)、[JSON](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.utility/convertfrom-json) 和 [XML](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.utility/convertto-xml)）的内置支持



#### 配置管理

PowerShell Desired State Configuration ([DSC](https://learn.microsoft.com/zh-cn/powershell/scripting/dsc/overview/dscforengineers)) 是 PowerShell 中的一个管理框架，管理企业基础结构

- 为可重复部署创建声明性[配置](https://learn.microsoft.com/zh-cn/powershell/scripting/dsc/configurations/configurations)和自定义脚本
- 强制执行配置设置并报告配置偏移
- 使用[推送或请求](https://learn.microsoft.com/zh-cn/powershell/scripting/dsc/pull-server/enactingconfigurations)模型部署配置

## 预定义程序/可执行文件

> 直接输入就能启动的程序，一般在 C:\Windows\System32 中
>
> 不懂某程序的作用和用法，可做如下输入`sc /?`



**微软程序**

* calc——计算器
* osk——虚拟键盘
* notepad——空白记事本
* control——控制面板
* mspaint——画图
* charmap 字符映射表
* psr 步骤记录器
* snippingtool 截图工具

**可执行文件**

*  SC 是用来与服务控制管理器和服务进行通信
          的命令行程序。
* write —— 类似C语言中的打印输出print方法 ，eg write hello
* wusa—— 微软独立更新程序
* Windows Performance Recorder (WPR) 和 Windows Performance Analyzer (WPA) ——Windows 性能工具包

* ping——网络连接测试
* ipconfig  —— ip配置工具

**快捷键补充**

https://support.microsoft.com/zh-cn/windows/windows-%E7%9A%84%E9%94%AE%E7%9B%98%E5%BF%AB%E6%8D%B7%E6%96%B9%E5%BC%8F-dcc61a57-8ff0-cffe-9796-cb9706c75eec#keyboard-shortcuts=windows-8&WindowsVersion=Windows_10

* win10 关机快捷键：win+X+U+U

* 关闭程序/窗口 Alt + F4

* 按住“Shift”键，右键点击文件或文件夹，选择“复制为路径

* Win + Home ：移除当前窗口外其他程序最小化，节约系统资源

* 

| Windows 徽标键 + E              | 打开文件资源管理器                                  |
| ------------------------------- | --------------------------------------------------- |
| Windows 徽标键 + D              | 显示和隐藏桌面。                                    |
| Windows 徽标键 + Alt + D        | 显示和隐藏桌面上的日期和时间。                      |
| Windows 徽标键 + M              | 最小化所有窗口                                      |
| Windows 徽标键 + R              | 打开“运行”对话框。                                  |
| Windows 徽标键 + 加号 (+)       | 打开“放大镜”。                                      |
| Windows 徽标键 + Shift + 向上键 | 将桌面窗口拉伸至屏幕顶部和底部。                    |
| Windows 徽标键 + Shift + 向下键 | 在垂直方向上还原/最小化活动桌面窗口，而宽度保持不变 |
| Windows 徽标键 + Tab            | 打开任务视图。                                      |



----

<font color=Red> <b>——————————————————————————</b></font>

```powershell
$n = "bits"
.\sc.exe -- % qc $n
.\sc.exe --% qc bits
```



## PowerShell 使用技巧





## PowerShell 特性

### 别名



#### 查看别名

```powershell
Get-Command -CommandType Alias
```



### 管道



# PowerShell 文档



## Cmdlet







# PS语法

### PS解决方案集合

> 查看PS版本信息

```powershell
$PSVersionTable.PSVersion
###
Major  Minor  Patch  PreReleaseLabel BuildLabel
-----  -----  -----  --------------- ----------
7      3      2
####
```

