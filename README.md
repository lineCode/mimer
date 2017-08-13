# mimer
<div align=center><img width="80" height="80" src="./icon/mimer.gif" alt="mimier" /></div>
A IM tool that use MQTT protocol

### MIMER 数据包的详细及其修改

1. CONNECT:
	- 固定报头(fixed header):
	    - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水
		         +：1~3 bit 标识部分帐户可以在不同的设备同时登录
	    - (1~4)  S: 剩余长度值: MQTT 长度编码
	
	- 可变报头(variable header):
	    - (1)    D 协议名长度,可能为了方便抓包工具的解析, 不做D处理
	    - (4)    协议名[MQTT]
	    - (1)    协议版本[4]
	    - (1)    连接标志
	    - (2)    保持链接(max: 18h-12m-15s)
	
	- 有效载荷(payload):	
	    - (16)   M: 客户端ID[IPV6]
	    - (*)    SDM: 遗嘱主题[任意数据类型,推荐字符串]
	    - (*)    SDM: 遗嘱消息[任意数据类型,可以是图片]
	    - (*)    SDM: 用户名[任意数据类型,推荐字符串]
	    - (*)    SDM: 密码[任意数据类型,可以是图片,指纹]

2. CONNACK:
    - 固定报头(fixed header):
        - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
        - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
        - (1)    连接确认标志
        - (1)    连接返回码
		
	- 有效载荷(payload):NULL

3. PUBLISH:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1~4)  S: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
	    - (*)    SDM: 主题名[任意数据类型,推荐字符串]
		- (1)    报文标识符
		
	- 有效载荷(payload):
	    - (*)    应用消息
		
4. PUBACK:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
		- (1)    报文标识符
		
	- 有效载荷(payload): NULL
	
5. PUBREC:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
		- (1)    报文标识符
		
	- 有效载荷(payload): NULL

6. PUBREL:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
		- (1)    报文标识符
		
	- 有效载荷(payload): NULL

7. PUBCOMP:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
		- (1)    报文标识符
		
	- 有效载荷(payload): NULL
	
8. SUBSCRIBE:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1~4)  S: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
	    - (*)    SDM: 主题名[任意数据类型,推荐字符串]
		- (1)    报文标识符
		
	- 有效载荷(payload):
	    - (*)    SDM: 主题名1[任意数据类型,推荐字符串]
		- (1)    M: QOS1
		- (*)    SDM: 主题名2[任意数据类型,推荐字符串]
		- (1)    M: QOS2
		- (*)    SDM: 主题名3[任意数据类型,推荐字符串]
		- (1)    M: QOS3
		- ...

9. SUBACK:
    - 固定报头(fixed header):
		- (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1~4)  S: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
	    - (1)    报文标识符
		
	- 有效载荷(payload):
	    - (1)    M: QOS1 返回码
	    - (1)    M: QOS2 返回码
	    - (1)    M: QOS3 返回码
		- ...

10. UNSUBSCRIBE:
    - 固定报头(fixed header):
	    - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1~4)  S: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
	    - (1)    报文标识符
		
	- 有效载荷(payload):
	    - (*)    SDM: 主题名1[任意数据类型,推荐字符串]
	    - (*)    SDM: 主题名2[任意数据类型,推荐字符串]
	    - (*)    SDM: 主题名3[任意数据类型,推荐字符串]
		- ...

11. UNSUBACK:
    - 固定报头(fixed header):
	    - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header):
	    - (1)    报文标识符
		
	- 有效载荷(payload): NULL

12. PINGREQ:
    - 固定报头(fixed header):
	    - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 
		         +: 1~3 bit 用于客户端当前状态类型的标志(正在输入/正在处理紧急问题/... ,目前有8种可选类型)
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header): NULL
		
	- 有效载荷(payload): NULL
	
13. PINGRESP:
    - 固定报头(fixed header):
	    - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 		    
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header): NULL
		
	- 有效载荷(payload): NULL
	
14. DISCONNECT:
    - 固定报头(fixed header):
	    - (1)    +: 0-bit作为脱水标志 [1]:脱水处理(数据包解析按脱水数据包解析);默认是[0]:未脱水	 		    
	    - (1)    D: 剩余长度值: MQTT 长度编码
		
	- 可变报头(variable header): NULL
		
	- 有效载荷(payload): NULL

### 符号说明:

| 符号|        意义|                 描述          |
|:----:|:----------------|:-------------------------|
| +  | 新增语义(ADD)    |新增MQTT协议的原来没有的语义|
| -  | 删除语义(DELEDE) |删除MQTT中原有的语义|
| M   | 修改语义(MODIFED)|修改或扩展了MQTT协议原有语义|
| D   | 脱水语义(DRIED)  |可执行脱水处理的语义部分|
| S   | 度量语义(SIZE)   |必须有度量前缀的语义部分|

### 一些符号组合的说明

SDM: 表示该部分的语义有前缀SIZE段(此处的脱水方案可以参考MQTT 长度编码方式), 该字段可作脱水处理, 且修改了原MQTT协议的原始语义
(?): 每个字段前面的()及数字表示该字段占用的byte, *表示不确定
关于剩余长度的脱水处理
- 长度固定为2的去掉该字段
- 长度为1~4byte的无法做脱水处理

### 一个关于长度编码在其他部分应用的讨论

&emsp;&emsp;对于不同的数据包, 其中的数据的每一个字段的长度总有一个前缀来度量它的的大小(SIZE), 所以为了尽量减小不必要的字节, 可
以在某些数据包中这种度量值使用可变形式的编码方式来表示长度, 但有些数据包用固定的两个字节反而更加有利。因此可以灵活的设置fixed header
的0号bit为来标定这种度量方式, 所以为了保证这种语义的一致性, 一种数据包中如果采用脱水方式编码, 则该数据包任何部分都必须采用脱水处理,
否则只要有一处无法脱水, 则该数据包不采用脱水处理！对于不同的数据包：考虑到每种数据包的使用频率和重要程度以及数据包的可能性大小, 选择
不同的编码方式和有必要

- CONNECT     : 只在登录或注册的时候会使用此类数据包, 而且涉及到的字段(clientID,willTopic,willMsg,userName,passwd)的长度一般不会过长, 建议使用可变编码以减少不必要的度量数据, 但是其中的password字段的长度可能会扩展到2个字节，故固定为2个字节度量

>|     字段  |        意义    |        度量处理方式          |  官方度量处理方式  |
>|:---------:|:--------------|:------------------------------|--------------------|
>| clientID  | 客户端ID(唯一) | 固定长度，无需度量            |      2 个字节     |
>| willMsg   | 遗嘱消息       | 1 个字节(所以长度不能超过256) |      2 个字节     |
>| willTopic | 遗嘱主题       | 1 个字节(所以长度不能超过256) |      2 个字节     |
>| userName  | 用户名         | 1 个字节(所以长度不能超过256)|       2 个字节     |
>| password  | 密码           | 2 个字节(所以长度不能超过65535)|     2 个字节     |

- CONNACK     : 只在登录或注册的时候会使用此类数据包, 使用可变编码

>|     字段  |        意义    |        度量处理方式          |  官方度量处理方式  |
>|:---------:|:---------------|:-----------------------------|--------------------|
>| rc        | 连接返回码     | 固定长度，无需度量           |         无         |
>| clientID  | 客户端ID(注册时) | 固定长度，无需度量         |         无         |

- PUBLISH     : 通讯的最主要的数据包形式, 使用频率最高, 涉及到的字段(topic, payload),其中topic可以采用可变编码, payload不建议使用可变编码, 暂时建议使用固定长度编码2个字节表示payload大小

>|     字段  |        意义    |        度量处理方式          |  官方度量处理方式  |
>|:---------:|:---------------|:-----------------------------|--------------------|
>| topic     | 发布主题       | 1 个字节(所以长度不能超过256)|       2 个字节     |
>| payload   | 发布数据内容   | 同官方处理          | 可用剩余长度计算出来，无需度量|

- PUBACK      : 和PUBLISH配合, 但数据包本身不大, 使用频率较高
- PUBREC      : 和PUBLISH配合, 但数据包本身不大, 使用频率较高
- PUBREL      : 和PUBLISH配合, 但数据包本身不大, 使用频率较高
- PUBCOMP     : 和PUBLISH配合, 但数据包本身不大, 使用频率较高
- SUBSCRIBE   : 该类数据包只在查找关系中使用, 使用频率相对稳定,考虑到topic字段的可读性建议使用可变编码

>|     字段  |        意义    |        度量处理方式          |  官方度量处理方式  |
>|:---------:|:---------------|:-----------------------------|--------------------|
>| topic     | 订阅主题       | 1 个字节(所以长度不能超过256)|       2 个字节     |

- SUBACK      : 和SUBSCRIBE配合, 但数据包本身不大, 使用频率相对稳定

>|     字段  |        意义    |        度量处理方式          |  官方度量处理方式  |
>|:---------:|:---------------|:-----------------------------|--------------------|
>| topicRC   | 订阅主题返回码 |           1 个字节           |       1 个字节     |

- UNSUBSCRIBE : 该类数据包只在取消关系中使用, 数据包小, 使用频率相对稳定
- UNSUBACK    : 该类数据包只在取消关系中使用, 数据包小, 使用频率相对稳定
- PINGREQ     : 该数据包功能固定, 小数据包, 使用频繁但不影响, 建议使用完全脱水处理, 去除不必要的度量值
- PINGRESP    : 和PINGREQ搭配, 作为保活操作, 建议使用完全脱水处理, 去除不必要的度量值
- DISCONNECT  : 和CONNECT相对, 使用次数只在每次离线时使用, 建议使用可变编码
