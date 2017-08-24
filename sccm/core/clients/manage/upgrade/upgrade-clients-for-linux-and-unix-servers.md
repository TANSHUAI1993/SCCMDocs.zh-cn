---
itle: 'Upgrade clients | Microsoft Docs | Linux UNIX '
description: "在 System Center Configuration Manager 中升级 Linux 或 UNIX 服务器上的客户端。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 394ba7c236c05cc90a3d7f99eb6146b15d620f11
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中升级 Linux 和 UNIX 服务器的客户端

*适用范围：System Center Configuration Manager (Current Branch)*

可以将计算机上的适用于 Linux 和 UNIX 的客户端版本升级到较新的客户端版本，而不用先卸载当前的客户端。 要实现此操作，请使用 **-keepdb** 命令行属性在计算机上安装新的客户端安装包。 安装适用于 Linux 和 UNIX 的客户端时，它将用新的客户端文件覆盖现有的客户端数据。 但是，**keepdb** 命令行属性将指示安装过程保留客户端唯一标识符 (GUID)、本地信息数据库和证书存储。 然后，新的客户端安装将使用这些信息。  

 例如，你具有一台 RHEL5 x64 计算机，该计算机运行来自适用于 Linux 和 UNIX 的原始版 Configuration Manager 客户端的客户端。 若要将此客户端升级到累计更新 1 中的客户端版本，请手动运行 **install** 脚本以从累积更新 1 中安装适用的客户端包，并增加 **keepdb** 命令行开关。 使用的命令行类似于：**./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar**  

## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>如何使用软件部署来升级 Linux 和 UNIX 服务器上的客户端  
 你可以使用软件部署来将适用于 Linux 和 UNIX 的客户端升级到新的客户端版本。 但是，System Center Configuration Manager 客户端不能通过直接运行安装脚本来安装新客户端，因为必须先卸载当前客户端才能安装新的客户端。 这将在安装新客户端开始之前，结束运行安装脚本的 Configuration Manager 客户端进程。 若要成功使用软件部署来安装新客户端，必须计划此安装，使其在将来某一时间点由操作系统内置计划功能启动并运行。  

 若要实现此目的，请使用软件部署先将新的客户端安装包的文件复制到客户端计算机，然后部署并运行一个脚本来计划客户端安装过程。 该脚本使用操作系统的内置 **at** 命令来延迟其启动。 然后，当脚本运行时，由客户端操作系统而不是计算机上的 Configuration Manager 客户端对其进行管理。 这允许脚本调用的命令行先卸载 Configuration Manager 客户端，然后安装新客户端，完成 Linux 或 UNIX 计算机上的客户端升级过程。 升级完成后，升级后的客户端依旧由 Configuration Manager 进行管理。  

 使用以下过程来帮助你配置软件部署以升级适用于 Linux 和 UNIX 的客户端。 下面的步骤和示例将运行初始版客户端的 RHEL5 x64 计算机升级到累积更新 1 客户端版本。  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>若要使用软件部署来升级 Linux 和 UNIX 服务器上的客户端  

1.  将新的客户端安装包文件复制到运行计划升级的 Configuration Manager 客户端的计算机上。  

     例如，你可能会将客户端安装包和累积更新 1 的安装脚本放置于客户端计算机上的以下位置： **/tmp/PATCH**  

2.  创建一个脚本来管理 Configuration Manager 客户端的升级，然后将脚本的副本放置到客户端计算机上与步骤 1 中的客户端安装文件相同的文件夹中。  

     此脚本不需要特定名称，但必须包含能够使用客户端计算机上本地文件夹中的客户端安装文件的命令行，并能够通过使用 **keepdb** 命令行属性来安装客户端安装包。 使用 **-keepdb** 命令行属性来维护当前客户端的唯一标识符，以供正在安装的新客户端使用。  

     例如，创建名为 **upgrade.sh** 且包含以下行的脚本，然后将其复制到客户端计算机上的 **/tmp/PATCH** 文件夹：  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  使用软件部署让每个客户端都使用计算机内置的 **at** 命令来运行 **upgrade.sh** 脚本，且运行脚本前具有短暂延迟。  

     例如，使用以下命令行来运行脚本：**at -f /tmp/upgrade.sh -m now + 5 minutes**  

 客户端成功计划要运行的 **upgrade.sh** 脚本后，客户端将提交一条状态消息，指示软件部署已成功完成。 但是在延迟后，实际客户端安装随后由计算机进行管理。 客户端升级完成后，通过检查客户端计算机上的 **/var/opt/microsoft/scxcm.log** 文件来验证安装。 此外，可以通过在 Configuration Manager 控制台中“资产和符合性”工作区的“设备”节点中查看客户端的详细信息，确认客户端是否已安装并与站点通信。  
