# 操作系统后门
## Windows操作系统后门
## 影子账户
```
影子账户是内部账户和外部账户的形式，主要起备查及处理不方便放在外部账户的费用的功
能。“影子用户”一种指在网络应用中将网卡的MAC，IP地址修改成与别人的一模一样，然后
接在同一个交换机的认证口下的终端用户。另一种指操作系统中影子账户

创建一个隐藏账户 net user test$ （net user看不见，计算机管理界面能看见）
net user admin$ admin /add

注册表 HKEY_LOCAL_MACHINE/SAM/SAM/Domains/Account/Users/

Names文件夹，选中test$，记住十六进制数字，返回上层找到00000(对应的十六进制数字)

找到administrator的十六进制数字，然后找到对应的00000（十六进制）文件夹打开，复
制administrator的000001F4文件夹里面的F值到我们的隐藏账户test$里面的F值中。

导出test$的注册表，删除test$用户、导入注册表。

找到Names里面的test$喝和test$对应的十六进制目录，右键导出到桌面。

然后使用net user test$ /del 删除test$用户。

然后再把导出到桌面的注册表重新导入就ok了

HKEY_LOCAL_MACHINE\SAM\SAM\Domains\Account\Users\Names
```

## 注册表注入后门
1. Run注册表后门
```
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
下的键值为开机启动项,每一次开机都会执行键值对应的程序或bat脚本


新建一个字符串值  自定义名称  
C:\Windows\system32\win32calc.exe 
关机重启
```

2. Logon Scripts后门
```
Logon Scripts 是优先于很多杀毒软件启动的,所有可以通过这种方式达到
一定的免杀效果
计算机\HKEY_CURRENT_USER\Environment
下新建字符串值
新建UserInitMprLogonScript
C:\Windows\system32\cmd.exe
修改后注销重新登录后执行脚本
```

3. Userinit注册表后门
```
Userinit的作用是用户在进行登录初始化设置时,会执行指定的程序,可以修改
计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Winlogon

Userinit
的键值来添加要执行的程序,多个程序用逗号隔开,
注销登陆后执行.
```
4. 计划任务后门
```
Windows实现定时任务主要有schtasks与at两种方式,均可用于计划在某个日期和时间
执行程序和脚本,其中at命令在Win8之后不再支持
```

5. Bitsadmin后门
```
Bitsadmin后台智能传输服务,是一个 Windows组件,从Win7之后操作系统认自带,它可以利用
空闲的带宽在前台或后台异步传输文件,并支持在重新启动计算机或重新建立网络连接之后自动恢复
文件传输,常用于 Windowsupdate的安装更新,从攻击者的角度来看,可以滥用此功能在受控的主
机上执行命令达到持久化控制。
```

6. MSF后门模块

## WMI型后门
```
在日常的使用中,WMI都是用于信息的收集:
wmic startup list full  自启动的程序
wmic process call create "caLc.exe" 在当前机器中执行指定程序
wmic process where(description="rundll32,eXe")  查看 rundll32所加载的dll
wmic cpu get DataWldth  /format:list    查询当前机器的操作系统位数
WMI事件分两类
本地事件:有生命周期,为进程宿主的周期
永久性WMI事件订阅:存储在WM库中,以 SYSTEM权限运行,并且重启后依然存在

Empire是一个后港透框架,可以使用它来创建一个永久性的WMI事件订阅,从而在目标主机上留下
持久化后门。
项目地址:https/github.com/EmpireProject/Empire
```

## Nishang后门
```
Nishang是基于 Powershell的攻击框架,面向红队和渗透测试人员,该框架提供了许多有用的脚本和Payload,适用于渗透测试的各个阶段。
Nishang的使用环境为 Powershell3.0以上
Powershell2.0(Win7)及以下使用可能会有些小问题
Nishang包含多个模块,涵盖渗透测试中的各个阶段
```

# Linux操作系统后门
## alias
```
alias命令可以设置别名
执行 ll 相当于执行  ls  -l
alias  ll=ls -l
```

## ssh 后门设计

## 计划任务
```
反弹shell
```

## TCP_Wrappers

## PAM后门

## SSH后门

## SSH Trapper后门

## Rookit


# 最骚的后门形式 ..  隐藏文件
```

```