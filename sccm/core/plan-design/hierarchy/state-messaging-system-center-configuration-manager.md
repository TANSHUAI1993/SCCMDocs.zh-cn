---
title: 状况消息
titleSuffix: Configuration Manager
description: 受支持版本的 Configuration Manager 中的状况消息说明。
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e3a30211b95e483b30caf1507b74a7737d156bb
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951862"
---
# <a name="state-messages-in-configuration-manager"></a>Configuration Manager 中的状况消息 

适用范围：System Center Configuration Manager (Current Branch)

状况消息包含有关 Configuration Manager 客户端状况的简明信息。 状况消息传递系统由 Configuration Manager 的特定组件（如软件更新和配置设置）使用。

Configuration Manager 客户端向回退状态点或管理点站点系统发送状况消息，报告操作的当前状态。 可以创建报表以查看由 Configuration Manager 客户端发送的状况消息。

使用状况消息的各个 Configuration Manager 功能通过状况消息的主题类型进行标识。 本文中列出的状况消息主题类型可用于定义状况消息相关的 Configuration Manager 功能。

> [!NOTE]  
> 状况消息 ID 的值为零 (0) 通常表示主题类型状态未知。

## <a name="300-statetopictypesumassignmentcompliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|       0   | 符合性状态未知|
|   1   | 合规 | 
|   2   | 不符合 | 

## <a name="301-statetopictypesumassignmentenforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   0    | 强制状态未知 |
|   1    | 正在安装更新        | 
|   2    | 正在等待重新启动              | 
|   3    | 正在等待另一安装过程完成         | 
|   4    | 已成功安装更新 (2)             | 
|   5    | 正在等待系统重启           | 
|   6    | 安装更新失败          | 
|   7    | 正在下载更新   | 
|   8    | 已下载更新    | 
|   9    | 下载更新失败     | 
|   10   | 正在等待安装之前的维护时段         | 
|   11   | 等待业务流程            | 

## <a name="302-statetopictypesumassignmentevaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|      
|0|        评估状态未知|                 
|   1    |评估已激活       |
|   2    |评估成功      |
|   3    |评估失败         |


## <a name="400-statetopictypesumcidetection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
| 0  | 检测状态未知|
|   1|  不需要      |
|   2|  未检测          |
|   3|  已检测      |

## <a name="401-statetopictypesumcicompliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|0| 符合性状态未知|
|   1   |合规         |
|   2   |不符合         |
|   3   |检测到冲突     |
|   4   |错误             |
|   5   |未知           |
|   6   |部分符合   |
|   7   |符合性未配置     |

## <a name="402-statetopictypesumcienforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
| 0 | 强制状态未知|
|   1   |强制执行已启动                   |
|   2   |强制执行正在等待内容               |
|   3   | 正在等待另一安装过程完成         |
|   4   |正在等待安装之前的维护时段              |
|   5   |安装之前要求重新启动            |
|   6   |常规失败           |
|   7   |等待的安装              |
|   8   |正在安装更新                 |
|   9   |正在等待系统重启        |
|   10  |已成功安装更新             |
|   11  |未能安装更新          |
|   12  |正在下载更新        |
|   13  | 已下载更新        |
|   14  |未能下载更新         |

## <a name="500-statetoptctypesumupdatedetection"></a>500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|0 |检测状态未知|
|   1   | 不需要更新     |
|   2   | 需要更新         |
|   3   | 已安装更新    |

## <a name="501-statetopictypesumupdatesourcescan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|0 |扫描状态未知|
|   1   | 扫描正在等待内容        |
|   2   | 扫描正在运行            |
|   3   | 扫描完毕          |
|   4   | 扫描正在等待重试      |
|   5   | 扫描失败        |
|   6   | 扫描已完成，但有错误 |

## <a name="700-statetopictyperesyncstatemsg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

    No State IDs.

## <a name="701-statetopictypesystemheartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

    No State IDs.

## <a name="702-statetopictypeckdupdate"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
    No State IDs.

## <a name="800-statetopictypeclientdeployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   100 |客户端部署已启动             |          
|   101 |正在等待下载                  |          
|   102 |已计划部署                  |          
|   103 | 正在等待部署前的时段 |
|   104 |部署已跳过                |          
|   301 |未知的客户端部署失败 |          
|   302 |创建 ccmsetup 服务失败  |         
|   303 |删除 ccmsetup 服务失败 |          
|   304 |无法在系统驱动器上启用了基于文件的写入筛选器 (FBWF) 的嵌入式操作系统上安装 |          
|   305 |纯安全模式在 Windows 2000 上无效  |         
|   306 |启动 ccmsetup 下载进程失败  |         
|   307 |无效的 ccmsetup 命令行 |        
|   308 |未能通过 WINHTTP 在下列地址下载文件 |        
|   309 |未能通过 BITS 在下列地址下载文件 |       
|   310 |安装 BITS 版本失败 |         
|   311 |无法验证必备文件是否是 MS 签名文件  |          
|   312 |磁盘已满，复制文件失败 |       
|   313 |Client.msi 安装失败，出现 MSI 错误 |          
|   314 |加载 ccmsetup.xml 清单文件失败 |          
|   315 |获取客户端证书失败  |         
|   316 |必备文件不是 MS 签名文件 |         
|   317 |需要重新启动才能继续安装  |          
|   318 |由于 MP 与客户端版本不匹配，无法在 MP 上安装客户端 |        
|   319 |不支持该操作系统或 Service Pack  |        
|   320 |不支持部署                  |          
|   321 |缺少位                      |          
|   322 |源文件夹不可用                  |          
|   323 |不支持 Appv                    |          
|   324 |站点版本不正确                    |          
|   325 |必备的哈希不匹配                |          
|   326 |MDM 取消注册失败             |          
|   327 |检测到 MDM 注册             |          
|   328 |检测到 Intune                   |          
|   329 |不允许使用按流量计费的网络            |          
|   400 |客户端部署成功 |  
|   401 |部署成功，需要重新启动          |          
|   402 |部署成功，重新启动成功         |
|   500 |客户端分配已启动|
|   601 |未知的客户端分配失败|
|   602 |下列站点代码无效|
|   603 |无法分配到 MP|
|   604 |发现默认管理点失败|
|   605 |下载站点签名证书失败|
|   606 |自动发现站点代码失败|
|   607 |站点分配失败；客户端版本高于站点版本|
|   608 |无法从 Active Directory 域服务和 SLP 获取站点版本|
|   609 |无法获取客户端版本|
|   700 |客户端分配成功|

## <a name="801-statetopictypedeviceclientdeployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

    No State IDs.

## <a name="810-statetopictypeclientcomanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   100 | 注册状态         |
|   101 | 已计划注册          |
|   102 | 已取消注册           |
|   105 | 已开始注册            |
|   106 | 注册成功，但未预配   
|   107 | 注册成功且已预配   
|   108 | 注册不活动用户         |
|   110 | 注册失败         |


## <a name="820--statetopictypeclientwufb"></a>820  STATE_TOPICTYPE_CLIENT_WUFB

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   | 适用于企业的 Windows 更新客户端状态| 

## <a name="900-statetopictypebranchdp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   | 磁盘空间      | 

## <a name="901-statetopictyperemotedpmonitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

    No State IDs.

## <a name="902-statetopictypepulldpmonitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

    No State IDs.

## <a name="903-statetopictypedpusage"></a>903 STATE_TOPICTYPE_DP_USAGE

    No State IDs.

## <a name="1000--statetopictypeclientframeworkcomm"></a>1000  STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1      | 客户端与管理点通信成功 |
|   2      | 客户端无法与管理点通信 |

## <a name="1001-statetopictypeclientframeworklocal"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |客户端已成功从本地证书存储检索证书       |
|   2   |客户端未能从本地证书存储检索证书 |

## <a name="1002-statetopictypedeviceclientframeworkcomm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

    No State IDs.

## <a name="1003-statetopictypedeviceclientframeworklocal"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

    No State IDs.

## <a name="1004-statetopictypedeviceclientframeworkcertificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

    No State IDs.

## <a name="1005-statetopictypedeviceclientwipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

    No State IDs.

## <a name="1006-statetopictypedeviceclientretire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

    No State IDs.

## <a name="1007-statetopictypedeviceclientwipeintune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

    No State IDs.

## <a name="1008-statetopictypedeviceclientretireintune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

    No State IDs.

## <a name="1009-statetopictypedeviceclientdevicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

    No State IDs.

## <a name="1010-statetopictypedeviceclientdevicelockintune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

    No State IDs.

## <a name="1011-statetopictypedeviceclientdevicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

    No State IDs.

## <a name="1012-statetopictypedeviceclientdevicepinresetintune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

    No State IDs.

## <a name="1013-statetopictypedeviceclientdevicepinresetonprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

    No State IDs.

## <a name="1014-statetopictypedeviceclientdevicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

    No State IDs.

## <a name="1015-statetopictypedeviceclientdevicealbypassintune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

    No State IDs.

## <a name="1100-statetopictypeclientframeworkmodereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |客户端尚未就绪，无法进入纯模式  |
|   2   |客户端已就绪，可以进入纯模式       |


## <a name="1300-statetopictypeclienthealth"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |   成功|    
|   2   |   未成功 |    

## <a name="1401-statetopictypestatereport"></a>1401 STATE_TOPICTYPE_STATE_REPORT

    No State IDs.

## <a name="1500-statetopictypecaltrackut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

    No State IDs.

## <a name="1502-statetopictypecaltrackmt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

    No State IDs.

## <a name="1503-statetopictypecaltrackml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

    No State IDs.   

## <a name="1600-statetopictypeuseraffinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |用户关联已设置        |
|   2   |用户关联已删除        |

## <a name="1700-statetopictypeappciscan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

    No State IDs.

## <a name="1701-statetopictypeappcicompliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

    No State IDs.

## <a name="1702-statetopictypeappcienforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1000    |配置项目成功                      |
|   1001    |配置项目成功并已安装            |
|   1002    |配置项目成功并预检                |
|   1003    |配置项目快速状态成功                  |
|   2000    |正在配置项目                    |
|   2001    |正在配置项目，正在等待内容            |
|   2002    |正在配置项目，正在安装                 |
|   2003    |正在配置项目，正在等待重新启动             |
|   2004    |正在配置项目，正在等待维护时段         |
|   2005    |正在配置项目，正在等待计划               |
|   2006    |正在配置项目，正在下载从属内容     |
|   2007    |正在配置项目，正在安装依赖项        |
|   2008    |正在配置项目，正在等待重新启动             |
|   2009    |正在配置项目，内容已下载             |
|   2010    |正在配置项目，正在等待更新             |
|   2011    |正在配置项目，正在等待用户重新连接         |
|   2012    |正在配置项目，正在等待用户注销              |
|   2013    |正在配置项目，正在等待用户登录               |
|   2014    |正在配置项目，正在等待安装            |
|   2015    |正在配置项目，正在等待重试              |
|   2016    |正在配置项目，正在等待 presmode               |
|   2017    |正在配置项目，正在等待业务流程          |
|   2018    |正在配置项目，正在等待网络            |
|   2019    |正在配置项目，正在等待更新 VE              |
|   2020    |正在配置项目，正在更新 VE            |
|   3000    |配置项目不符合要求                       |
|   3001    |配置项目不符合要求，主机不适用           |
|   4000    |配置项目未知                    |
|   5000    |配置项目出错                          |
|   5001    |配置项目出错，正在评估                   |
|   5002    |配置项目出错，正在安装                   |
|   5003    |配置项目出错，正在检索内容               |
|   5004    |配置项目出错，正在安装依赖项            |
|   5005    |配置项目出错，正在检索内容依赖项        |
|   5006    |配置项目出错，规则冲突                   |
|   5007    |配置项目出错，正在等待重试                |
|   5008    |配置项目出错，正在卸载取代        |
|   5009    |配置项目出错，正在下载取代               |
|   5010    |配置项目出错，正在更新 VE                  |
|   5011    |配置项目出错，正在安装许可证               |
|   5012    |配置项目出错，正在检索允许的所有受信任的应用       |
|   5013    |配置项目出错，没有可用的许可证            |
|   5014    |配置项目出错，不支持该 OS                 |
|   6000    |配置项目启动成功                           |
|   6010    |配置项目启动出错                           |
|   6020    |配置项目启动状态未知|

## <a name="1703-statetopictypeappciassignmentevaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

    No State IDs.

## <a name="1704-statetopictypeappcilaunch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

    No State IDs.

## <a name="1800-statetopictypeeventintrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

    No State IDs.

## <a name="1801-statetopictypeeventextrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

    No State IDs.

## <a name="1900-statetopictypeepaminfection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

    No State IDs.

## <a name="1901-statetopictypeepamhealth"></a>1901 State_Topictype_Ep_Am_Health

    No State IDs.

## <a name="1902-statetopictypeepmalware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

    No State IDs.

## <a name="1950-statetopictypeatphealthstatus"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

    No State IDs.

## <a name="2001-statetopictypeepclientdeployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |Endpoint Protection 未托管       |
|   2   |Endpoint Protection 正在等待安装  |
|   3   |Endpoint Protection 已托管         |
|   4   |Endpoint Protection 安装失败     |
|   5   |Endpoint Protection 重新启动挂起  |
|   6   |不支持 Endpoint Protection       |
|   7   |Endpoint Protection 已共同管理      |

## <a name="2002-statetopictypeepclientpolicyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   0   |Endpoint Protection 策略应用程序状态未知        |
|   1   |Endpoint Protection 策略应用程序已成功         |
|   2   |Endpoint Protection 策略应用程序失败        |

## <a name="2003-statetopictypeclientaction"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   0   |  未知           |
|   1   |  Active            |
|   2   |  Inactive          |

## <a name="2100-statetopictypewpclientdeployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   | 唤醒代理未安装          |
|   2   | 唤醒代理正在等待安装       |
|   3   | 唤醒代理已安装          |
|   4   | 唤醒代理安装失败       |
|   5   | 唤醒代理正在等待重新启动         |
|   6   | 此 OS 上不支持唤醒代理   |
|   7   | 唤醒代理服务器选择退出        |
|   8   | 唤醒代理卸载失败      |
|   9   | 不支持唤醒代理运行时         |

## <a name="2200-statetopictypefdm"></a>2200 STATE_TOPICTYPE_FDM

    No State IDs.

## <a name="2201-statetopictypeccmcertbinding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

    No State IDs.

## <a name="2202-statetopictypeserverstatistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

    No State IDs.

## <a name="3000-statetopictypedmwnschannel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|0  | Windows 推送通知服务通道已设置|

## <a name="4000-statetopictypemdmdeviceproperty"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

    No State IDs.

## <a name="4002-statetopictypemdmclientidenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

    No State IDs.

## <a name="4003-statetopictypemdmapplicationrequest"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

    No State IDs.

## <a name="4004-statetopictypemdmapplicationstate"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

    No State IDs.

## <a name="4005-statetopictypemdmlicensedevicerelation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

    No State IDs.

## <a name="4006-statetopictypemdmlicensekeys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

    No State IDs.

## <a name="4007-statetopictypemdmpolicyassignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

    No State IDs.

## <a name="4008-statetopictypemdmandroidcount"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

    No State IDs.

## <a name="4009-statetopictypemdmslkstatus"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

    No State IDs.

## <a name="4010-statetopictypemdmusercompanytermacceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="4022-statetopictypemdmdepsyncnowstatus"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

    No State IDs.

## <a name="4023-statetopictypemdmmamstoreappsync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

    No State IDs.

## <a name="5000-statetopictypecertificateenrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |已发出质询                    |
|   2   |质询发出失败              |
|   3   |请求创建失败                 |
|   4   |请求提交失败               |
|   5   |质询验证成功          |
|   6   |质询验证失败             |
|   7   |发出失败                    |
|   8   |问题挂起                   |
|   9   |已发出                      |
|   10  |响应处理失败          |
|   11  |响应挂起                    |
|   12  |注册成功                    |
|   13  |无需注册                   |
|   14  |已吊销                         |
|   15  |已从集合中删除                 |
|   16  |已验证续订                  |
|   17  |安装失败              |
|   18  |已安装                   |
|   19  |删除失败                   |
|   20  |已删除                     |
|   21  |已请求续订               |


## <a name="5001-statetopictypecertificatecrp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |已发出质询                       |
|   2   |质询发出失败                 |
|   3   |请求创建失败                    |
|   4   |请求提交失败                  |
|   5   |质询验证成功             |
|   6   |质询验证失败                |
|   7   |发出失败                       |
|   8   |问题挂起                      |
|   9   |已发出                         |
|   10  |响应处理失败             |
|   11  |响应挂起                       |
|   12  |注册成功                       |
|   13  |无需注册                      |
|   14  |已吊销                            |
|   15  |已从集合中删除                    |
|   16  |已验证续订                     |
|   17  |安装失败                 |
|   18  |已安装                      |
|   19  |删除失败                      |
|   20  |已删除                        |
|   21  |已请求续订                  |

## <a name="5200-statetopictyperesourceaccessstatus"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   | 状态 PIN 设置成功                   |
|   2   | 状态 PIN 设置失败                  |
|   3   | 不支持状态 PIN 设置               |
|   4   | 正在进行状态 PIN 设置             |

## <a name="6000-statetopictyperemoteappsubscriptionstatus"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

    No State IDs.

## <a name="6001-statetopictyperemoteappsubscriptionsyncstatus"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

    No State IDs.

## <a name="6002-statetopictyperemoteappauthcookiessyncstatus"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

    No State IDs.

## <a name="6003-statetopictyperemoteapplicationssyncstatus"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

    No State IDs.

## <a name="6004-statetopictyperemoteapplockresult"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

    No State IDs.

## <a name="7000-statetopictypeusercompanytermacceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="7001-statetopictypepfxcertificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |已发出质询               |
|   2   |质询发出失败         |
|   3   |请求创建失败            |
|   4   |请求提交失败          |
|   5   |质询验证成功     |
|   6   |质询验证失败        |
|   7   |发出失败               |
|   8   |问题挂起              |
|   9   |已发出                 |
|   10  |响应处理失败     |
|   11  |响应挂起               |
|   12  |注册成功               |
|   13  |无需注册              |
|   14  |已吊销                    |
|   15  |已从集合中删除            |
|   16  |已验证续订             |
|   17  |安装失败         |
|   18  |已安装              |
|   19  |删除失败              |
|   20  |已删除                |
|   21  |已请求续订          |

## <a name="7010-statetopictypeconditionalaccesscompliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
||  1   | 符合性成功             |
|   2   | MP 符合性失败      |
|   3   | 客户端符合性失败      |
|   4   | Intune 符合性失败      |
|   5   | AAD 符合性失败         |
|   6   | 符合性 comgmt Intune       |

## <a name="7200-statetopictypesuperpeerupdatecachemap"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |已添加对等缓存源                |
|   2   |已删除对等缓存源          |

## <a name="7201-statetopictypesuperpeerupdateconfig"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |已停用对等缓存源              |
|   2   |已启用对等缓存源                |

## <a name="7202-statetopictypedownloadaggregatedata"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |下载聚合数据上传       |

## <a name="7203-statetopictypepeersourcereqrejectionstats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |对等源拒绝数据上传     |

## <a name="7300-statetopictypeproxytraffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

    No State IDs.

## <a name="7301-statetopictypeproxyconnection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

    No State IDs.

## <a name="7302-statetopictypesrsusagedata"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

    No State IDs.

## <a name="7303-statetopictypeproxytrafficidentity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

    No State IDs.

## <a name="8001-statetopictypehasreport"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     状况消息 ID     |  状况消息描述 |
|:-------------|:------|
|   1   |支持运行状况证明         |
|   2   |不支持运行状况证明         |

## <a name="statetopictypedeviceclientedplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

    No State IDs.

## <a name="8003-statetopictypeenablelostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

    No State IDs.

## <a name="8004-statetopictypedisablelostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

    No State IDs.

## <a name="8005-statetopictypelocatedevice"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

    No State IDs.

## <a name="8006-statetopictyperebootdevice"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

    No State IDs.

## <a name="8007-statetopictypelogoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

    No State IDs.

## <a name="8008-statetopictypeuserslist"></a>8008 STATE_TOPICTYPE_USERSLIST

    No State IDs.

## <a name="8009-statetopictypedeleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

    No State IDs.

## <a name="8010-statetopictypecleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

    No State IDs.

## <a name="8011-statetopictypecleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

    No State IDs.

## <a name="8012-statetopictypesetdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

    No State IDs.

## <a name="9000-statetopictypebookcicompliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

    No State IDs.

## <a name="9001-statetopictypebookcienforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

    No State IDs.

## <a name="next-steps"></a>后续步骤

- [Configuration Manager 中的状况消息传递说明](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Configuration Manager 的软件更新管理白皮书](https://www.microsoft.com/download/details.aspx?id=44578)
