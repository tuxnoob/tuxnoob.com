---
title: Linux Commands - Important 10 Linux Ps Command With Examples
date: '2016-07-02T05:51:00.000+07:00'
author: Arief JR
tags: [Linux Commands, 10 Important Linux Process]
categories: [Linux]
---

![](https://4.bp.blogspot.com/-xFFG276mI84/V3MKs_F1YsI/AAAAAAAADew/1uew6pPXmYYGUqjmvNAOscB15MKqzBvGwCLcB/s1600/image4195.png)

**Why i love linux???** the answer, i use **linux** because like with the **commands** of **CLI**. This post i will discuss **10 Ps Command In Linux**, yep linux was built-in tool to capture current process in the system since this operating system inspired from **Unix**.

#### What Is PS Command???

Ps is acronym **Process Status**, used to provide information about the currently running processes, including their _process identification numbers_ (PIDs). (_source: [http://www.linfo.org/ps.html](http://www.linfo.org/ps.html)_)  

From its manual page, PS gives a snapshots of the current process. It will “capture” the system condition at a single time. If you want to have a repetitive updates in a real time, we can use top command.  

PS support three (3) type of usage syntax style.  

1. UNIX style, which may be grouped and must be preceded by a dash  
2. BSD style, which may be grouped and must not be used with a dash  
3. GNU long options, which are preceded by two dash  

We can mix those style, but conflicts can appear. In this article, will use UNIX style. Here’s are some examples of PS command in a daily use.

#### 1. Show All Current Process

Here i use simple ps command with options _ax_, this option _a_ is acronym **all** and _x_ will show all process even the current process is not associated with any TTY (terminal).  

Here this command:  

```
# ps ax
```

This result might be long result. To make it more easier to read, combine it with less command.  

```
# ps ax | less
```

![](https://3.bp.blogspot.com/-Ka6cnxQRXtQ/V3MQzXXW6mI/AAAAAAAADfA/BAtCY0BBEaA4qRw-KqG5R5yhOp60AVmtQCLcB/s1600/Screenshot_20160629_070431.png)

#### 2. Filter Process By User

The ps command will show process which run by user, for show processing by user use option _-u_. Here i will see for you process with **user gunzip**.  

```
# ps -u gunzip 
```

![](https://1.bp.blogspot.com/-lmtZ4JKfpBo/V3MR0J_Dq_I/AAAAAAAADfM/tC08KlKpGnwiwivXy3kG7-UOB9v_Juy1ACLcB/s1600/Screenshot_20160629_070823.png)

#### 3. Filter Processes By Memory Usage Or CPU

If you want see result memory usage or CPU, type **ps** command with **aux** options and you'll see:

```
# ps -aux | less 
```

![](https://3.bp.blogspot.com/-BmDcQFpGOOk/V3P633xEv3I/AAAAAAAADfc/zPyTCGyA-1Ivgyq9fHyHgwV9654ndJllgCLcB/s1600/Screenshot_20160629_234058.png)

Since the result can be in a long list, we can **pipe** less command into ps command.  
By default, the result will be in unsorted form. If we want to sort by particular column, we can add --sort option into **ps command**.  

Sort by the highest **CPU utilization** in ascending order and sort by the highest **Memory utilization** in ascending order  

```
# ps -aux --sort -pcpu | less

# ps -aux --sort -pmem | less 
```

![](https://3.bp.blogspot.com/-71HsIvQ4n6w/V3SbzSIEeqI/AAAAAAAADf0/uC7XGDPR_9cM2mWCs1vkSSWGApfGNUpdgCLcB/s1600/Screenshot_20160630_055459.png)

This example i will combine a command, will display like below image.  

```
# ps -aux --sort -pcpu,+pmem | head -n 10
```

![](https://2.bp.blogspot.com/-pnmN2JthLSk/V3SbyGs4sGI/AAAAAAAADfs/hh3UYQI9jA83cy1ly1ghBCcbzyDoe7b3QCLcB/s1600/Screenshot_20160630_055544.png)

#### 4. Filter Process By Name Process ID

This i will use options **-C** for filter process, and i will filtering amarok process with following command:  

```
$ ps -C amarok
```

![](https://3.bp.blogspot.com/-rAz3lrl3cWk/V3bo80fS9rI/AAAAAAAADhc/_onY5xiSzbIm98xnrq0Et_2qAV7sMFEbgCLcB/s1600/Screenshot_20160702_050327.png)

If you want see more result, you can add **-f** options for show full listing. See this following command:  

```
$ ps -f -C amarok
```

![](https://4.bp.blogspot.com/-7dCYoMkCuVM/V3bpvfEOCsI/AAAAAAAADhk/sm3RQUroSlMPjUacqrdn97xbHtX9XvoPACLcB/s1600/Screenshot_20160702_050708.png)

#### 5. Filter Processes By Thread Of Process

This ps command will show process by thread fit PID (_Process ID_). For running this command add **-L** options, like this command:  

```
$ ps -L 16014
```

![](https://4.bp.blogspot.com/-y1BFvsqlG_Y/V3brZr83PfI/AAAAAAAADhw/oAIrc-B3BYgTj0ZEFARQ-WQKwULGse_oACLcB/s1600/Screenshot_20160702_051337.png)

The above screenshot was tell, the PID remain same value but LWP which shows rows different values of thread.

#### 6. Show Process In Hierarchy

For show processes by hierarchical form, use options **-axjf** like this:  

```
$ ps -axjf
```

![](https://1.bp.blogspot.com/-7_QYz2O7NGo/V3bslO6rviI/AAAAAAAADh8/hWbP2ofV6gwtr6OyPy5Lgf-xbkuE3vpfACLcB/s1600/Screenshot_20160702_051909.png)

Or other command you can use **pstree**

```
$ pstree
```

![](https://4.bp.blogspot.com/-IuuStiVCb0w/V3btKkPsdJI/AAAAAAAADiE/yxc0eIPVCrcP6RusnukyHFbdoB_TzsigACLcB/s1600/Screenshot_20160702_052146.png)

#### 7. Show Security Information

If want see information about security using ps command, you can use command:  

```
$ ps -eo pid,user,args
```

Option **-e** will show you all processes while **-o** option will control the output. **Pid**, **User** and **Args** will show you the **Process ID**, **the User who run the application** and **the running application**.

![](https://2.bp.blogspot.com/-aRmbCrZegpQ/V3bud37WrFI/AAAAAAAADiQ/_SW2jfvEMp0MAIXlNHE7J6W7PovMFatTQCLcB/s1600/Screenshot_20160702_052608.png)

The keyword / user-defined format that can be used with **-e option** are **args, cmd, comm, command, fname, ucmd, ucomm, lstart, bsdstart and start**.

#### 8. Show Every Process As Root (real & effecitve ID) in user format
ß
System admin may want to see what processes are being run by root and other information related to it. Using ps command, we can do by this simple command :  

```
$ ps -U root -u root u
```

The **-U parameter** will select by **real user ID (RUID)**. It selects the processes whose real user name or ID is in the userlist list. The real User ID identifies the user who created the process.  
While the **-u paramater** will select by effective user ID (EUID)  
The last **u** paramater, will display the output in user-oriented format which contains **User, PID, %CPU, %MEM, VSZ, RSS, TTY, STAT, START, TIME and COMMAND** columns.  
Here’s the output of the above command.

![](https://1.bp.blogspot.com/-OJ85ov1sdyQ/V3bvTxrxHnI/AAAAAAAADic/viDXP9Q50q4m9mafJQxLIFaRrMAj1LacACLcB/s1600/Screenshot_20160702_053054.png)

#### 9. Ps Command For See A Realtime Process Viewer

ps will display a report of what happens in your system. The result will be a static report.  
Let say, we want to filter processes by PID, User, Detail Command, CPU and Memory usage. And we want the report is updated every 1 second. We can do it by **combining ps command with watch command** on Linux.  
Here’s the command :  

```
$ watch -n 1 'ps -e -o pid,uname,cmd,pmem,pcpu --sort=-pmem,-pcpu | head -15'
```

![](https://1.bp.blogspot.com/-9PLS7jxBT4g/V3bxukeif-I/AAAAAAAADio/ibSEJ7nTcxI0vpc5XY5Ny2bZuOZO9-0GQCLcB/s1600/Screenshot_20160702_053847.png)

#### 10. Displayed Elapsed Time Of Process

This command options almost same with point 7 in above, but **user** and **args** not used. See this command:  

```
$ ps -eo pid,comm,etime
```

![](https://4.bp.blogspot.com/-XaXOGfhQKME/V3by5fJGrbI/AAAAAAAADiw/slW24sJFYaUBdn84Tnte7HCSprkjR6FzgCLcB/s1600/Screenshot_20160702_054549.png)

#### Conclusion

This **ps command** you can use for monitor usage daily activity about what happen in your linux systems. You can generate variant options with **ps**, i think **ps** it's better for system administrator which work without GUI.  

Don't forget for see documentation of **ps** with command **man ps**.  

Thanks.