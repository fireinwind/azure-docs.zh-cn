---
title: 在 Azure Database for MariaDB 中进行监视
description: 本文介绍了用于对 Azure Database for MariaDB 进行监视并发出警报的指标，包括 CPU、存储和连接统计信息。
services: mariadb
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: mariadb
ms.topic: article
ms.date: 11/10/2018
ms.openlocfilehash: 3daa4eb07e626e53d9106abf978174f505e785ab
ms.sourcegitcommit: 5a1d601f01444be7d9f405df18c57be0316a1c79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2018
ms.locfileid: "51516402"
---
# <a name="monitoring-in-azure-database-for-mariadb"></a>在 Azure Database for MariaDB 中进行监视
监视服务器的相关数据有助于排查工作负荷故障及优化工作负荷。 Azure Database for MariaDB 提供了各种指标来帮助用户深入了解服务器的行为。

## <a name="metrics"></a>度量值
所有 Azure 指标的频率都是一分钟，每个指标提供 30 天的历史记录。 可针对指标配置警报。 其他任务包括设置自动操作、执行高级分析和存档历史记录。 有关详细信息，请参阅 [Azure 指标概述] (../monitoring-and-diagnostics/monitoring-overview-metrics.md)。

<!--For step by step guidance, see [How to set up alerts](howto-alert-on-metric.md). -->

### <a name="list-of-metrics"></a>指标列表
以下指标适用于 Azure Database for MariaDB：

|指标|指标显示名称|单位|Description|
|---|---|---|---|---|
|cpu_percent|CPU 百分比|百分比|使用的 CPU 百分比。|
|memory_percent|内存百分比|百分比|使用的内存百分比。|
|io_consumption_percent|IO 百分比|百分比|使用的 IO 百分比。|
|storage_percent|存储百分比|百分比|所用存储占服务器最大存储的百分比。|
|storage_used|已用的存储量|字节|使用的存储量。 服务使用的存储可能包括数据库文件、事务日志和服务器日志。|
|serverlog_storage_percent|服务器日志存储空间百分比|百分比|所用的服务器日志存储占服务器的服务器日志最大存储的百分比。|
|serverlog_storage_usage|服务器日志已用的存储量|字节|使用的服务器日志存储量。|
|serverlog_storage_limit|服务器存储空间上限|字节|此服务器的最大服务器日志存储。|
|storage_limit|存储限制|字节|此服务器的最大存储。|
|active_connections|活动连接数|Count|服务器的活动连接数。|
|connections_failed|失败的连接数|Count|服务器的失败连接数。|
|network_bytes_egress|网络传出|字节|跨活动连接数的网络传出。|
|network_bytes_ingress|网络传入|字节|跨活动连接数的网络传入。|

## <a name="server-logs"></a>服务器日志
可以在服务器上启用慢查询日志。 若要了解有关日志记录的详细信息，请访问 [服务器日志](concepts-server-logs.md)页。

## <a name="next-steps"></a>后续步骤
- 若要深入了解如何使用 Azure 门户、REST API 或 CLI 访问和导出指标，请参阅 [Azure 指标概述](../monitoring-and-diagnostics/monitoring-overview-metrics.md)。

<!-- - See [How to set up alerts](howto-alert-on-metric.md) for guidance on creating an alert on a metric.-->