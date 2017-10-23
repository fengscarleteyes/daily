# xshell.help

标签（空格分隔）： Xshell说明文档

---

```vbscript
Sub main  
    xsh.Screen.Synchronous = True    ' 使窗口显示与当前输出同步  
    xsh.Screen.WaitForString "Reboot now? (y/n)"    ' 等待目标设备发回 "Reboot now? (y/n)" 字符串  
    xsh.Screen.Send "y" & VbCr    ' 输入字符 y 并回车  
End Sub  
```

| **Functions** |                                          |                                          |                   |
| ------------- | ---------------------------------------- | ---------------------------------------- | ----------------- |
| **返回值**       | **函数**                                   | **参数**                                   | **说明**            |
| void          | **Clear**()                              |                                          | 清除终端屏幕。           |
| void          | **Send**(LPCTSTR lpszStrToSend)          | lpszStrToSend用户拟要发送的字符串                  | 向终端发送消息。          |
| BSTR          | **Get**(long nBegRow, long nBegCol, long nEndRow, long nEndCol) | nBegRow终端的行起始位置nBegCol终端的列起始位置nEndRow终端的行末端位置nEndCol终端的列末端位置 | 读入终端规定区域的字符串后返回值。 |
| void          | **WaitForString**(LPCTSTR lpszString)    | lpszString终端中出现的字符串                      | 等待消息。             |
| Long          | **WaitForStrings**(VARIANT FAR* strArray, long nTimeout) | strArray终端中出现的字符串nTimeout等候时间的毫秒值*返回值*发现的字符数 | 等待消息直至到时。         |
| void          | **Synchronous**(BOOL bSync)              | bSync1(True): 使用画面同步化0(False) : 禁用画面同步化  | 定义画面的同步化。         |

| **参数**        |        |                |
| ------------- | ------ | -------------- |
| **名称**        | **类型** | **说明**         |
| CurrentColumn | long   | 返回当前值。         |
| CurrentRow    | long   | 返回当前行。         |
| Columns       | long   | 返回与终端的列宽相同的列数。 |
| Rows          | long   | 返回与终端的行高相同的行数。 |

| **Functions** |                                          |                                          |                                          |
| ------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| **返回值**       | **函数**                                   | **参数**                                   | **说明**                                   |
| Void          | **OpenSession**(LPCTSTR lpszSession)     | lpszSession是字符串，指Xshell会话路径或Xshell使用的URL类型。 | 打开新会话或URL。为打开会话把 /s选项置于字符串的前端。例)在打开A.xsh 会话时使用‘/s $PATH/A.xsh’。 |
| Void          | **CloseSession**()                       |                                          | 退出当前连接的会话。                               |
| Void          | **Sleep**(long timeout)                  | Timeout毫秒单位的时间值                          | Xshell按照指定时间进行待机。                        |
| Void          | **LogFilePath**(LPCTSTR lpszNewFilePath) | lpszNewFilePath包括路径在内的文件名                | 指定日志文件。                                  |
| void          | **StartLog**()                           |                                          | 开始会话的日志记录。日志将被保存到LogFilePath()指定的路径。如未指定日志文件路径则使用默认路径。 |
| void          | **StopLog**()                            |                                          | 停止日志记录。                                  |

| **参数**        |        |               |
| ------------- | ------ | ------------- |
| **名称**        | **类型** | **说明**        |
| Connected     | BOOL   | 是否连接当前会话。     |
| LocalAddress  | BSTR   | 导入本地地址。       |
| Path          | BSTR   | 导入当前会话文件的路径。  |
| RemoteAddress | BSTR   | 导入远程地址。       |
| RemotePort    | long   | 导入远程端口号。      |
| Logging       | BOOL   | 确认当前会话是否记录日志。 |




