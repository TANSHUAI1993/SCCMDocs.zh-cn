---
itle: 'Upgrade clients | Microsoft Docs | Linux UNIX '
description: "在 System Center Configuration Manager 中升級 Linux 或 UNIX 伺服器的用戶端。"
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
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>如何在 System Center Configuration Manager 中升級 Linux 和 UNIX 伺服器的用戶端

*適用於：System Center Configuration Manager (最新分支)*

您可以將電腦上 Linux 和 UNIX 用戶端的版本升級為至較新的用戶端版本，而不需要先解除安裝目前的用戶端。 若要這樣做，請在電腦上安裝新的用戶端安裝封裝，同時使用 **-keepdb** 命令列屬性。 安裝 Linux 和 UNIX 用戶端時，會將現有用戶端資料覆寫為新的用戶端檔案。 不過，**-keepdb** 命令列屬性會指示安裝程序保留用戶端唯一識別項 (GUID)、本機資訊資料庫，以及憑證存放區。 新的用戶端安裝之後會使用這項資訊。  

 例如，您有從 Linux 和 UNIX 之 Configuration Manager 用戶端的原始版本執行用戶端的 RHEL5 x64 電腦。 若要將這個用戶端升級至累計更新 1 中的用戶端版本，請手動搭配執行 **install** 指令碼與 **-keepdb** 命令列參數來安裝累計更新 1 中適用的用戶端套件。 您使用的命令列與下面類似：**./install -mp <主機名稱\> -sitecode <代碼\> -keepdb ccm-Universal-x64.<組建\>.tar**  

## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>如何在 Linux 和 UNIX 伺服器上使用軟體部署來升級用戶端  
 您可以使用軟體部署，將 Linux 和 UNIX 的用戶端升級為新的用戶端版本。 不過，因為新用戶端的安裝必須先解除安裝目前的用戶端，所以 System Center Configuration Manager 用戶端無法直接執行安裝指令碼來安裝新的用戶端。 這會先結束執行安裝指令碼的 Configuration Manager 用戶端程序，再開始安裝新的用戶端。 若要順利使用軟體部署來安裝新的用戶端，您必須排程在未來的時間開始安裝，並透過作業系統的內建排程功能來執行安裝。  

 若要達成此目的，請使用軟體部署先將新用戶端安裝封裝的檔案複製到用戶端電腦，然後部署和執行指令碼來排程用戶端安裝程序。 指令碼會使用作業系統的內建 **at** 命令來延遲其開始時間。 然後，執行指令碼時，其作業是由用戶端作業系統所管理，而非電腦上的 Configuration Manager 用戶端。 這可讓指令碼所呼叫的命令列先解除安裝 Configuration Manager 用戶端，再安裝新的用戶端，以完成 Linux 或 UNIX 電腦上的用戶端升級程序。 完成升級之後，升級的用戶端仍由 Configuration Manager 所管理。  

 使用下列程序可協助您設定軟體部署來升級 Linux 和 UNIX 的用戶端。 下列步驟和範例將執行用戶端初始版本的 RHEL5 x64 電腦升級為累計更新 1 用戶端版本。  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>在 Linux 和 UNIX 伺服器上使用軟體部署來升級用戶端  

1.  將新的用戶端安裝套件檔案複製到執行您想要升級之 Configuration Manager 用戶端的電腦。  

     例如，您可能將累計更新 1 的用戶端安裝封裝和安裝指令碼放在用戶端電腦的下列位置： **/tmp/PATCH**  

2.  建立指令碼來管理 Configuration Manager 用戶端的升級，然後在用戶端電腦上與步驟 1 的用戶端安裝檔案相同的資料夾中放置一份指令碼。  

     指令碼不需要特定的名稱，但所含的命令列必須足以使用用戶端電腦上本機資料夾中的用戶端安裝檔案，以及使用 **-keepdb** 命令列屬性來安裝用戶端安裝套件。 您可以使用 **-keepdb** 命令列屬性維護目前用戶端的唯一識別項，以供將安裝的新用戶端使用。  

     例如，您建立名為 **upgrade.sh** 且包含下列數行的指令碼，然後將它複製至用戶端電腦上的 **/tmp/PATCH** 資料夾：  

    ```  
    #!/bin/sh  
    #  
    /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

    ```  

3.  使用軟體部署，讓每個用戶端先使用電腦內建 **at** 命令來執行具有短暫延遲的 **upgrade.sh** 指令碼，再執行指令碼。  

     例如，使用下列命令列來執行指令碼：**at -f /tmp/upgrade.sh -m now + 5 minutes**  

 用戶端成功排程 **upgrade.sh** 指令碼執行之後，用戶端會提交狀態訊息，指出已順利完成軟體部署。 不過，在延遲之後，實際用戶端安裝之後是由電腦所管理。 完成用戶端升級之後，請檢閱用戶端電腦上的 **/var/opt/microsoft/scxcm.log** 檔案來驗證安裝。 此外，您還可以在 Configuration Manager 主控台之 [資產與相容性] 工作區的 [裝置] 節點中檢視用戶端詳細資料，確認已安裝用戶端，而且用戶端正在與站台通訊。  
