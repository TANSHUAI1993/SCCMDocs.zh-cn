---
title: "预声明具有 IMEI 或 iOS 序列号的设备"
description: "预声明具有 IMEI 或 iOS 序列号的公司拥有的设备。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6cd640085e90b2945326e3fa942ae9bd7b8f7e24
ms.openlocfilehash: 2550fef062b5ef508e4c0492a5a9c63ffcb9084a

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>预声明具有 IMEI 或 iOS 序列号的设备

*适用范围：System Center Configuration Manager (Current Branch)*

可通过导入公司拥有设备的国际移动设备识别 (IMEI) 码或 iOS 序列号对此类设备进行识别。 可上传包含设备 IMEI 码的逗号分隔值 (.csv) 文件，或者手动输入设备信息。  导入的信息将设置在设备列表中作为“公司”注册的设备的“所有权”。 访问该服务的每位用户仍需要 Intune 许可证。  

## <a name="predeclare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>预声明具有 IMEI 或 iOS 序列号的公司拥有的设备

1.  在 Configuration Manager 控制台中，导航到“资产和符合性”>“概述”>“公司拥有的所有设备”>“预声明设备”，然后单击“添加预声明设备”。 将打开“预声明设备”向导。
2.  指定添加设备信息的方式：
     -  上传包含 IMEI 号码和详细信息的 .csv 文件
     -  手动添加 IMEI 号码和详细信息。 若要手动输入信息，请键入 IMEI 号码或 iOS 序列号和设备的详细信息。

      对于已上传的文件，浏览到包含信息的 .csv 文件，以预声明公司拥有的设备。 该文件必须具有以下格式，仅提供指导的顶行除外。 每一行必须包含 IMEI 号码或 iOS 序列号。 只能预声明 iOS 设备的序列号；IMEI 号码用于其他设备平台。 此表格包含示例数据：
      | IMEI #  | iOS 序列 #  | 操作系统 | 详细信息 |
      | :------------ |:---------------|:-----|:-----|
      | 123456789012345    |   | WINDOWS | 公司拥有的 Windows 设备|
      |       | A1B2C3D4E5C6 |   iOS |  公司拥有的 iOS 设备|
      | 223456789012345 | E6D5C4B3A210 |   iOS |    另一台 iOS 设备|
      | 323456789012345 |        |   iOS |  第三台 iOS 设备|
      | 123456789012346 |         |   Android |     公司拥有的 Android 设备|

    .Csv 文件中不能包含标题行。 上例中仅包括用于阐述的标题。

    **列支持以下值：**    
      - 第 1 列：不含空格的 IMEI 号码
      - 第 2 列：iOS 序列号
      - 第 3 列：设备的操作系统：
         - IOS - 所有 iOS 设备
         - WINDOWS - 包括 Windows Phone、Windows 10 Mobile 和 Windows 电脑
         - ANDROID - 所有 Android 设备
      - 第 4 列 - 详细信息（可选）- Configuration Manager 控制台中显示的其他设备信息。 1024 个字符限制。

    单击“下一步” 。

3. 查看文件导入的结果。 如果之前已导入设备编号，Configuration Manager 将显示这些设备和替换**详细信息**。 选择希望重写其详细信息的设备。 设备详细信息只能通过重新导入设备标识或序列号来修改。 单击“下一步”继续，或单击“返回”保存更新后的详细信息，然后完成向导。

4. 如果导入中包括 iOS 序列号，则必须为这些设备分配注册配置文件。 从提供的配置文件列表中选择“待分配的注册配置文件”，然后单击“下一步”。

5. 单击“下一步”查看摘要，然后完成向导。



<!--HONumber=Nov16_HO1-->


