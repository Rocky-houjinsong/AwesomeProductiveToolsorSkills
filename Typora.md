### 介绍

> Typora是一款 Markdown 格式的文本编辑器软件;
> 桌面端(Windows即PC,和Mac) 
>
> 本地,无云端;  非常好用 ;
>
> 本地需要上传到 云端(云盘,git仓库等)

> 整理进度

:one:  :hourglass_flowing_sand:  2023年4月28日11:21:40  目前将最常用的核心功能整理出来,还有很多的细节 没有填充和讲解 ,有空再说;
先做一个 待办,以免遗忘 ; 注:五一要是能够提前搞定毕设,那么就可以接着整理技能和 工具

















## 内容元素

> 首先说明  ,Typora 本质上是 浏览器,  
>
> 除了内置的快捷将将 操作封装提供用户使用,还可以 使用 `HTML/CSS` 进行优化,
> 故,下文的讲解,涉及到 该部分, 同一功能  ,会有不同的实现方式

### 文本 Text

#### 样式

##### 基础操作

* 加粗    `Ctrl + B` 

* 下划线 `Ctrl + U`

* 删除线 `Alt + Shift + 5` 

* 斜体 `Ctrl + i`

* 高亮

  * (默认的高亮) `==高亮内容==`     :pushpin:  勾选 `高亮设置 `
  * (自定义高亮 ,颜色,大小)
    <span style="font-size:3rem; background:blue;">**内容填充**</span>

* 颜色

  * (自定义颜色) `$\textcolor{颜色}{文本内容}$`    :pushpin: 勾选 `内联公式设置`  不能 同步修改 `字体大小 `

      :one:   $\textcolor{yellow}{文本}$   :pushpin:  英语单词要用熟练, .NET正好也是如此 ==操作==

        :two:  $\textcolor{#00fcfc}{文本}$

        :three: $\textcolor{rgb(255,0,0)}{文本}$

        ```html
        $\textcolor{yellow}{文本}$      黄色 yellow,
        $\textcolor{#00fcfc}{文本}$
        $\textcolor{rgb(255,0,0)}{文本}$
        ```
    
        
    
    * (颜色 + 大小 同时修改 )
    
      <font color= blue>我是蓝色</font>
      <font color= red size = 4>我是红色</font>
      <font color= green size =5 ><b>我是蓝色</b></font>
    
      <span style='color:red'>This is red</span>
      
      :pushpin:  建议使用 span  style 标签,不适用 font标签,,在Html5中已经移除 
      
      ```html
       <span style="color:red;background-color:yellow;font-size:20px;font-size:3em;margin:0;display:none;text-align:center;border-bottom：1px solid green"> `应用程序Application`</span>
      ```
      
      
    
    <ruby> 漢 <rt> ㄏㄢˋ </rt> </ruby>
    
  
  Ctrl</kbd>+<kbd>F9</kbd>
  
  <span style="font-size:2rem; background:yellow;">**Bigger**</span>
  
  

```html
<font color= green size =5 ><b>我是蓝色</b></font>
 <span style='color:red'>This is red</span>
  <span style="font-size:2rem; background:yellow;">**Bigger**</span>
```

在HTML块中，不允许有任何空行，否则它将被渲染为两个HTML块。

- 在Typora中，只有普通/普通HTML标签将作为HTML内容呈现，自定义标签（如`<application>`）`<my-custom-component>`将被忽略（它们将在导出/打印时包括在内）。
- 并非所有属性都受支持。`id`，`class`，`data-*`和渲染时HTML未知属性将不包括（他们将被列入当出口/打印）。
- 基本上不允许使用脚本。`<style>`并且`<meta>`也不会应用（它们将在导出/打印时包括在内）。
- 并非所有HTML标签/样式都可以导出为其他格式。导出为PDF，HTML或与HTML兼容的格式（例如EPub）将保留这些HTML内容，但是导出为其他格式（例如Word或LaTeX），这些HTML内容可能会变成纯文本。

  



### 图片Image



> 图片居中显示

<div align=center>![logo](https://www.baidu.com/img/flexible/logo/pc/result.png)

#### 表格

> 创建 
>
> `Ctrl + T` 

### :rofl: 表情Emoji

> 代码查看  

* 系统内置表情   `Win + .`
* 在线Emoji查看
  * https://www.emojiall.com/zh-hans
* Utools插件  Emoji

> 使用  `:英语单词:`  
>
> ​	Typora支持  `:hourglass:`  显示的是  :hourglass:

> 功能 作用

:one:  **图形化 标记**
			丰富单一乏味的 文本文档 ; 直观的图片 比文字更容易 理解 和学习 , 比如  :question:  就是比 `疑问:` 更形象 

:two: 精简内容,优化布局   
			http://typora.io :star:此处隐藏 我重点强调的内容       

点击查看 `网页链接` 之后 ,就能弹出 :star: 中 要强调的内容    <br>

:pushpin: 只有`网页链接` 才可以这样操作



   

> 常用表情速记 

| 表情                      | 代码        | 含义                                                         |
| ------------------------- | ----------- | ------------------------------------------------------------ |
| :warning:                 | warning     | 警告,此处是易错点,重点阐述                                   |
| :inbox_tray:              | inbox       | 收件箱,多在 待办待整理中使用                                 |
| :question:                | question    | 疑问, 此处有疑惑,未解决                                      |
| :interrobang:             | interrobang | 未搞懂,一知半解,未解决 ,但比 :question: 有些许理解           |
| :bulb:                    | bulb        | 解决该疑惑,对知识点的解决                                    |
| :key:                     | key         | 解决方案,是对 一个重大问题,提出完整的解决方法                |
| :star:                    | star        | 重点标记 ,                                                   |
| :pushpin:                 | pushpin     | 重点标记,建议理解 并记忆                                     |
| :triangular_flag_on_post: | triangular  | 此处做个标记,                                                |
| :heavy_check_mark:        | check       | :one:该待办,勾选这个待办 多数要 关联到 待办清单中 , 与 文本中的 任务列表做区分 ; :two: 正确的例子 |
| :x:                       | x           | 错误, 是错误的例子                                           |
| :one:                     | one         | 序号                                                         |
| :hourglass:               | hourglass   | 时间开始:hour                                                |
| :hourglass_flowing_sand:  | hourglass   | 时间进行中 ,一般会有中途休息或者其他耽误                     |
|                           |             |                                                              |
|                           |             |                                                              |
|                           |             |                                                              |
|                           |             |                                                              |
|                           |             |                                                              |



####  :white_check_mark: 任务列表ToDo

> 使用 

* 快捷键  `Ctrl + Shift + X`
* 语法  `- [ ] `

样式如下  

- [x] 
- [ ] 



#### 图表





#### 代码Code

> 快捷键  `Ctrl + Shift + K`





> 

### 链接Link



#### 网页链接



<http://typora.io>   

http://typora.io  :star:自动网址：Typora可以自动检测markdown中的网址链接，并将其呈现为URL链接，但是请注意，其他markdown引擎可能不支持此功能。

#### 本地资源-文件级

 **链接到本地文件**

您可以使用写入相对路径或绝对路径作为指向本地文件的链接地址，例如（*.md*）的扩展名可以省略，例如：

```
[Readme1](Readme1.md)

[Readme2](../Docs/Readme2.markdown)

[Readme3](Readme3)

[Readme4](/User/root/Docs/Readme1.md)

[Readme4](C:/Develop/Docs/Readme1.md)

[Readme4](file:///User/root/Docs/Readme1.md)
```

:warning:  对于相对链接地址，根据Markdown的规范导出为HTML时，它不会转换为真正的绝对文件路径。



####  **文档内部-标题级**



```
# This is a title

...
...
...


A [link](#this-is-a-title) to jump towards target header
```

您可以在Typora中的链接上使用`command+click`（macOS）或`ctrl+click`（Linux / Windows）跳转到目标标题，或在Typora中打开它们，或在相关应用程序中打开 

例如 本文中  

[点我跳转查看代码Code介绍](#代码Code) 

## 其他



### 目录

`[toc]`  产生菜单 自动更新

### 标题

开头#的个数表示，空格+文字。标题有1~6个级别，#表示开始，按换行键结束 

快捷键 Ctrl + 对应标题级别的数

### 换行  

* 按换行键`Enter`建立新的一行
* 按`Shift`+`Enter`可以创建一个比段落间距更小的行间距。
* 可在行尾插入打断线，禁止向后插入 `<br/>`

## 嵌入



### 视频

```html
< video src=”xxx.mp4” />
```



### 音频

```html
<audio src="xxx.mp3" />
```



### 网页嵌入

> 直接复制过来就可以
>
> :x: 不可再放到 代码Code中

<iframe height='265' scrolling='no' title='Fancy Animated SVG Menu' src='//codepen.io/jeangontijo/embed/OxVywj/?height=265&theme-id=0&default-tab=css,result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/jeangontijo/pen/OxVywj/'>Fancy Animated SVG Menu</a> by Jean Gontijo (<a href='https://codepen.io/jeangontijo'>@jeangontijo</a>) on <a href='https://codepen.io'>CodePen</a>. </iframe>



## 图床

使用Utools-图床插件来自定义上传到 Gitee中来使用其中的文件