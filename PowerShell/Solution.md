1. 返回对象列表中，我查看某一属性列，查看某一对象的某一具体属性 

应该是 使用 Select-Object的用法 

```powershell
 [System.Reflection.Assembly]::LoadWithPartialName("System.Web") | Select-Object -Property Location
```

2. 警告所说， 加载完整dll名称的方法实例

3. PS F:\CODE> "kaixin" | out-File kaixin.txt
   out-File : 对路径“F:\CODE\kaixin.txt”的访问被拒绝。
   所在位置 行:1 字符: 12

   + "kaixin" | out-File kaixin.txt
   + ~~~~~~~~~~~~~~~~~~~
     是因为这个2.txt是一个只读文件。



Get-Command Get-Process -syntax  

差语法，是差的是输入 

输出哪些对象和属性呢？

* 查看  某个属性的的值 

* ```
  $startInfo = New-Object System.Diagnostics.ProcessStartInfo
  ```

  :horse
  
  

