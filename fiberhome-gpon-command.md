# 烽火OLT在GPON应用下常用指令

标签（空格分隔）： 烽火OLT常用指令说明文档

[TOC]

---

## Admin

### 查看配置

```show startup-config```

### 查看卡授权状态

```showcard```

-----

## cd card

### 查看PON口光模块参数

```show optic_module_para slot <slotno> pon <ponno>```

```
命令示例
查看18号槽位16号PON口的光模块参数信息。
Admin\card#show optic_module_para slot 18 pon 16
show optic_module_par slot 18 pon 16
----- PON OPTIC MODULE PAR INFO -----
NAME VALUE UNIT
---------------------------------------
TYPE : 20 (KM)
TEMPERATURE : 33.14 ('C)
VOLTAGE : 3.26 (V)
BIAS CURRENT : 6.99 (mA)
SEND POWER : 3.26 (Dbm)
ONU_NO RECV_POWER , ITEM=2
1 -9.06 (Dbm)
3 -19.14 (Dbm)
Admin\card#
```

### 查看GPON盘的CPU和内存利用率

```show cpu-usage slot <slotno>```

```
命令示例
查看16号槽位GPON盘的CPU和内存利用率。
Admin\card#show cpu-usage slot 16
----- OLT CPU & Memory Using -----
CPU : 2.47%
Memory : 41.40%
Admin\card#
```

### 查看PON口关断

```show pon_onoff slot <slotno>```

```
命令示例
查看1号槽位PON接口盘的PON口关断状态。
Admin\card#show pon_onoff slot 1
ITEM(16) STATUS
--------------------------------
1 OFF
2 ON
3 ON
4 ON
```



### 配置PON口关断

```set slot <slotno> pon <ponno> [enable|disable]```

```
命令示例
关闭1号槽位1号PON口。
Admin\card#set slot 1 pon 1 disable
set ok!
Admin\card#
```

### 查看PON口MAC地址

```show pon_mac slot <slotno> pon <ponno> {lookup <mac_address>}*1```

```
命令示例
查看1号槽位1号PON口的MAC地址表。
Admin\card#show pon_mac slot 1 pon 1
----- PON MAC ADDRESS, ITEM=1 -----
001 22:3E:44:55:66:11 Vid:4091 OnuId:1
Admin\card#
结果说明
参数项 参数说明
ITEM PON口MAC地址表条目数。
XX:XX:XX:XX:XX:XX
PON口MAC地址。
Vid PON口MAC地址表的VLAN ID。
OnuId PON口ONU ID。
```

### 查看ONU自动发现配置

``` show onu_auto_discover slot <slotno>```

```
命令示例
查看1号槽位PON接口盘的ONU自动发现配置。
Admin\card#show onu_auto_discover slot 1
FLAG = 1
PERIOD = 120
```

### 配置ONU自动发现

```set onu_auto_discover slot <slotno> status [enable|disable] {aging_period <aging_period>}*1```

```
参数说明
slot <slotno> PON接口盘槽位号。取值范围：1～8，11～18。 必配参数
status [enable|disable]打开或关闭ONU自动发现功能。必配参数
aging_period <aging_period>
自动发现ONU的老化时间，系统根据老化时间定时清除自动发现ONU占用的注册缓存区，防止新上线的ONU因为注册缓存区满而不能正常注册的现象发生。 
取值范围≥120，单位为秒，默认值为120秒。必配参数
```

```
命令示例
打开1号槽位PON接口盘的ONU自动发现功能，自动发现的老化时间为120秒。
Admin\card#set onu_auto_discover slot 1 status enable aging_period 120
set auto upgrade cfg ok!
Admin\card#
```

### 配置端口描述信息

```set port_descp slot <slotno> port <portno> descp_info <descp_info>```

```
命令示例
配置1号槽位PON接口盘1号PON口的端口描述信息为AN5516OLT-SLOT1-PON1。
Admin\card#set port_descp slot 1 port 1 descp_info AN5516OLT-SLOT1-PON1
set port descp info ok!
Admin\card#
```

### 查看端口描述信息

```show port_descp slot <slotno> port <portlist>```

```
命令示例
查看1号槽位PON接口盘1号PON口的端口描述信息。
Admin\card#show port_descp slot 1 port 1
Port 1: AN5516OLT-SLOT1-PON1
Admin\card#
```

### 查看线卡组播地址表

```show igmp_addr_table slot <slotno>```

### 配置PON口认证模式

```set pon_auth slot <slotno> pon <ponno> mode phy_id|phy_id+psw|password|loid+psw|phy_id/loid+psw|no_auth|loid|phy_id/loid|phy_id/psw]```

```
参数说明

slot <slotno> PON接口盘槽位号。取值范围：1～8，11～18。 
pon <ponno>PON口号。取值范围：1～16。 
mode[phy_id|phy_id+psw|password|loid+psw|phy_id/loid+psw|no_auth|loid|phy_id/loid|phy_id/psw]

认证模式。
u phy_id：物理标识认证。
u phy_id+psw：物理标识+密码认证。
u password：密码认证。
u loid+psw：逻辑标识+密码认证。
u no_auth：不认证。
u loid：逻辑标识（不含密码）认证。
u phy_id/loid：物理标识/逻辑标识（不含密码）混合认证。
u phy_id/psw：物理标识/密码混合认证。
```

### 查看PON口认证模式

```show pon_auth [select|all] {slot <slotno> pon <ponno>}*1```

```
命令示例
查看1号槽位PON接口盘1号PON口的认证模式。
Admin\card#show pon_auth select slot 1 pon 1
slot 1 pon 1 ,auth mode is physical id.
Admin\card#
```

## cd device

### 查看指定上联端口的信息

```show uplink slot <slotno> port <portno>```

```
参数项 参数说明
Port info 上联端口号。
Link state 上联端口连接状态。
Port state 上联端口使能状态。
AutoNegotiation 上联端口自动协商状态。
Speed 上联端口速率。
Duplex 上联端口双工模式。
Learning 上联端口地址学习功能。
FlowControl 上联端口流量控制功能。
Port VLAN ID 上联端口VLAN ID。
PriEn 上联端口优先级使能状态。
PriValue 上联端口优先级值。
interface mode 上联端口模式，包括：SerDes和SGMⅡ。
Jumbo Frame 上联端口最大帧长度。
```

### 查看所有上联端口的信息

```show uplink port all```

### 查看机盘温度

```show card temperature```

-----

## cd service

### 配置/查看/删除 静态路由

```add static route destination <A.B.C.D> gateway <A.B.C.D> mask <A.B.C.D>```

`show static_route`

```no static route destination <A.B.C.D> mask <A.B.C.D>```

### 配置管理VLAN

```set manage vlan name <name> vid <1-4085> inputport <portlist> [untagged|tagged]```

```
参数说明
name <name> 管理VLAN的名称。 
vid <1-4085> 管理VLAN ID。取值范围为1～4085。
inputport<portlist>管理VLAN的端口号。 
[untagged|tagged]管理VLAN的Tag属性。
untagged：剥离VLAN ID。tagged：不剥离VLAN ID。

```

```
命令示例
配置管理VLAN名称为test，VLAN ID为1000，端口为19:1，Tag属性为Untagged。
Admin\service#set manage vlan name test vid 1000 inputport 19:1 untagged
Admin\service#
```
### 配置管理VLAN的IP

```set manage vlan name <name> ip <A.B.C.D/M> {<A.B.C.D>}*1```

```set manage vlan name <name> ipv6 <ipaddr> mask <masklen>```

### 删除管理VLAN

```no manage_vlan <name>```

### 查看管理VLAN

```show manage_vlan [<1-4085>|all]```

### 配置/查看命令行终端长度

```terminal length [<10-512>|0]```

```show terminal length```

-----

## cd onu

### 查看ONU光模块参数信息

```show optic_module slot <slotno> pon <ponno> onu <onuno>```

### 查看ONU的最后一次离线时间和上线时间

```show onu_last_on_and_off_time slot <slotno> pon [<ponno>|null] onu[<onuno>|null]```

### 查看在线ONU信息

```show online slot <slotno> pon <ponno>```

### 查看GPON ONU端口的MAC地址表

```show mac_list slot <slotno> pon <ponno> onu <onuno> port <portno> {lookup <mac_address>}*1```

### 复位ONU PON口

```set pon_onoff slot <slotno> pon <ponno> onu <onuno> status [on|off] {interval<off_time>}*1```

```
参数说明
slot <slotno> PON接口盘槽位号。取值范围：1～8，11～18。 
pon <ponno>PON端口号。取值范围：1～16。 
onu <onuno> ONU授权号。 
status [on|off]ONU PON口复位开关。
u on：复位。
u off：不复位。
{interval <off_time>}*1
PON口关断时间。取值范围：1～65535，单位为秒。 可选参数
```

### 配置ONU认证方式

```set auth_type slot <slotno> pon <ponno> onulist <onulist> type [mac|loid|loidonceon|psw|pswonceon]```

### 查看ONU认证方式

```show onu_authtype slot <slotno> pon <ponno> onu <onulist>```

### 授权ONU

```set authorization slot <slotno> pon <ponno> type <typestr> onuid <onuno>phy_id <phy_id_str> {[password] [<password>|null]}*1 {[logic_sn]<logic_sn_str> password[<password>|null]}*1```

```
参数说明
slot <slotno> PON接口盘槽位号。取值范围：1～8，11～18。
pon <ponno>PON端口号。取值范围：1～16。
type <typestr>ONU类型。 
onuid <onuno> ONU授权号。取值范围：1～128。 
phy_id <phy_id_str>物理标识。取值为12字节字符串。 
{[password][<password>|null]}*1物理密码。取值为不超过10字节的字符串或NULL。 
[logic_sn]<logic_sn_str>逻辑标识。取值为不超过24字节的字符串。 
password[<password>|null]逻辑密码。取值为不超过12字节的字符串或NULL。
```

```
命令示例
授权1号槽位PON接口盘1号PON口类型为AN5506-04-b2g的ONU，授权号为1，其
物理地址为FHTT00030405，物理密码为空。

Admin\onu#set authorization slot 1 pon 1 type 5506-04-b2g onuid 1 phy_id FHTT00030405
password null
set onu authcated cmd ok!
```

### 去授权ONU

```set unauthorization slot <slotno> pon <ponno> onu <onulist>```

### 查看ONU授权表

```show [authorization|discovery] slot [<slotno>|all] pon [<ponno>|all]```

### 查看ONU发现表

```show [authorization|discovery] slot [<slotno>|all] pon [<ponno>|all]```

### 查看ONU在线表

```show online slot <slotno> pon <ponno>```

### 配置ONU授权状态

```set authstatus slot <slotno> pon <ponno> onulist <onulist> status [auth|preauth|reserved]```

```
status [auth|preauth|reserved]ONU授权状态。
auth：已授权。preauth：预授权。reserved：预留。
```

### 配置ONU白名单

```
set whitelist {[phy_addr] address <address> password [<pwd_str>|null]}*1{[password] password <pwd_str>}*1 {[logic_sn] sn <sn_str> password[<pswd_str>|null]}*1 action[add|delete|lock|unlock] {slot <slotno> pon<ponno> onu <onuno> type <onutype>}*1
```

```
参数说明
[phy_addr]address <address>物理标识。取值为12字节字符串。 可选参数
password [<pwd_str>|null]物理密码。取值为不超过10字节的字符串或NULL。 可选参数
{[password]password <pwd_str>}*1密码。取值为不超过10字节的字符串。 可选参数
[logic_sn] sn <sn_str>逻辑标识。取值为不超过24字节的字符串。 可选参数
password [<pswd_str>|null]逻辑密码。取值为不超过12字节的字符串或NULL。 可选参数
action [add|delete|lock|unlock]动作。
u add：添加白名单。
u delete：删除白名单。
u lock：锁定白名单。
u unlock：解锁白名单。
slot <slotno> PON接口盘槽位号。取值范围：1～8，11～18。 必配参数
pon <ponno>PON端口号。取值范围：1～16。 必配参数
onu <onuno> ONU授权号。取值范围：1～128。 必配参数
type <onutype>ONU类型。 必配参数
```

```
命令示例
将物理地址为FHTT00030405、物理密码为空的ONU AN5506-04-b2g添加至1号槽
位PON接口盘1号PON口的白名单。

Admin\onu#set whitelist phy_addr address FHTT00030405 password null action add slot 1
pon 1 onu 1 type 5506-04-b2g
set onu whitelist ok!
```

### 查看ONU白名单

```show whitelist [physn|password|logicsn] {slot <slotno> pon <ponno>}*1```

### 配置GPON ONU业务带宽

```
set service_bandwidth slot <slotno> pon <ponno> onu <onuno> type <typestr>
fix <fixbw> assure <asrbw> max <maxbw>
```

```
slot <slotno> PON接口盘槽位号。取值范围：1～8，11～18。 必配参数
pon <ponno>PON端口号。取值范围：1～16。 必配参数
onu <onuno> ONU授权号。取值范围：1～128。 必配参数
type <typestr>业务类型。
取值范围：
1：IPTV业务。
2：宽带上网业务。
3：语音业务。
4：TDM（仅适用于AN5506-06）业务。
5：综合业务。
6：宽带上网2业务。
7：宽带上网3业务。
8：宽带上网4业务。
9：串口业务。
fix <fixbw> 固定带宽。取值范围：0～256000，单位为KByte/s。 必配参数
assure <asrbw> 保证带宽。取值范围：0～256000，单位为KByte/s。 必配参数
max <maxbw> 最大带宽。取值范围：64～256000，单位为KByte/s。 必配参数
```

```
命令示例
配置1号槽位PON接口盘1号PON口1号ONU的业务带宽
业务类型为带宽上网，固定带宽为100KByte/s。
保证带宽为200KByte/s，最大带宽为500KByte/s。

Admin\onu#set service_bandwidth slot 1 pon l onu 1 type data fix 100 assure 200 max 500
set onu service (data) bandwidth ok!
Admin\onu#
```

-----

## admin\onu\ngn

