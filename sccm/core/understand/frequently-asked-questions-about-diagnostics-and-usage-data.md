---
title: 诊断和使用情况数据的常见问题解答
titleSuffix: Configuration Manager
description: 查找有关 System Center Configuration Manager 的诊断和使用情况数据的常见问题。
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38b59e520baf9fddb09f71f459de409f38adad2b
ms.sourcegitcommit: 32a257fafbb29aece8b4f435dd5614fcef305328
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2019
ms.locfileid: "54005443"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>有关 System Center Configuration Manager 的诊断和使用情况数据的常见问题

*适用于：System Center Configuration Manager (Current Branch)*

本文解答有关 Configuration Manager 中的诊断和使用情况数据的常见问题。

## <a name="faqs"></a>常见问题

###  <a name="bkmk_off"></a> 如何关闭遥测？  
无法关闭遥测。 但是，你可以选择所收集的遥测数据的级别。 若要在提交遥测数据后帮助管理，可在脱机模式下使用服务连接点。

需要定期更新 Configuration Manager 的 Current Branch，以支持新版本的 Windows 10 和 Microsoft Intune。 Microsoft 需要至少基本级别的诊断和使用情况数据。 此数据用于使产品保持最新状态、改进更新体检以及提高产品的质量和安全性。

###  <a name="bkmk_retention"></a> 数据保留期为多久？  
 诊断和使用数据的保存期为一年。  

###  <a name="bkmk_update"></a> 安装或更新产品时是否发送了诊断和使用情况数据？  
 否。 仅当安装站点且可对其进行操作之后，才发送诊断和使用情况数据。  

###  <a name="bkmk_frequency"></a> 发送数据的频率是多高？  
 SQL 存储过程每七天（自安装站点之日起）运行一次。 在联机模式下，服务连接点配置为在查询运行后上传数据。 在脱机模式下，管理员使用服务连接工具上传数据。 （安装站点后的七天内，数据不可脱机使用。）  

###  <a name="bkmk_network"></a> 可否将数据用于形成网络映射？  
 如诊断和使用情况数据的级别说明中所示，站点详细信息包括每个站点中的时区信息。 此信息使你能够深入了解层次结构中站点广泛的地理位置和全球分布。 此数据不包括任何网络详细信息，例如 IP 地址或更详细的地理位置信息。 有关详细信息，请参阅[诊断和使用情况数据相关文章](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles)的列表，并找到你正在使用的版本的诊断和使用情况数据集合级别。


###  <a name="bkmk_tables"></a> 可以查看自定义表中的数据吗？  
 否。 Configuration Manager 通过 SQL 存储过程收集诊断和使用情况数据。 这些存储过程针对数据库中的默认产品表运行。 所有这些 SQL 表的前缀都为“TEL_”。 作为 SQL 架构检测查询的一部分，对所有表名称进行了哈希处理，以便与已知默认值进行比较。 此行为确定数据库中存在自定义表。 若存在自定义表，这说明数据库架构已从默认架构扩展。 它不包含这些表中存储的任何数据。  

###  <a name="bkmk_databases"></a>你能看到其他数据库的名称或其他数据库中的数据吗？ 
 否。 用于收集数据的存储过程仅限于站点数据库。  

### <a name="bkmk_gdpr"></a> Configuration Manager 是否遵循一般数据保护条例 (GDPR)？
 否。 Configuration Manager 不受 GDPR 监督。 它是你直接部署、管理和操作的本地产品。 Microsoft 收集的诊断和使用情况数据用于改进未来版本的安装体验、质量和安全性。 此诊断和使用情况数据要受到 GDPR 的监督。 但是，不会收集最终用户标识信息 (EUII) 或最终用户匿名标识符 (EUPI) 并将其传输至 Microsoft。 有关 GDPR 的详细信息，请参阅 [Microsoft 信任中心中关于 GDPR 的内容](https://microsoft.com/gdpr)。 有关 Configuration Manager 数据的详细信息，请参阅[诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)。


## <a name="see-also"></a>另请参阅  
 [诊断和使用情况数据](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
