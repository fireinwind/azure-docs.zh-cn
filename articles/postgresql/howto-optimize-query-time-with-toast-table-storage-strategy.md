---
title: 使用 toast 表存储策略优化 Azure Database for PostgreSQL 服务器中的查询时间
description: 本文介绍如何使用 toast 表存储策略优化 Azure Database for PostgreSQL 服务器中的查询时间。
author: dianaputnam
ms.author: dianas
editor: jasonwhowell
ms.service: postgresql
ms.topic: conceptual
ms.date: 10/22/2018
ms.openlocfilehash: dee8aaaef4b1998a7234a88d07ad5efbc79d050b
ms.sourcegitcommit: 1f9e1c563245f2a6dcc40ff398d20510dd88fd92
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51628332"
---
# <a name="optimizing-query-time-with-toast-table-storage-strategy"></a>使用 TOAST 表存储策略优化查询时间 
本文介绍如何使用 TOAST 表存储策略优化查询时间。

## <a name="toast-table-storage-strategies"></a>TOAST 表存储策略
有四个不同的策略可在磁盘中存储 toast 列，这些列表示压缩与行外存储之间的各种组合。 可在数据类型级别和列级别设置策略。
- “普通”策略可防止压缩或行外存储；此外，它会禁用 varlena 类型的单字节标头。 “普通”策略是非 toast 数据类型的列的唯一可行策略。
- “扩展”策略允许压缩和行外存储。 “扩展”策略是大多数 toast 数据类型的默认策略。 首先尝试压缩；如果行仍然过大，则尝试行外存储。
- “外部”策略允许行外存储，但不允许压缩。 使用“外部”策略可以加速针对宽文本和 bytea 列执行的子字符串操作，并且会大幅增加存储空间，因为这些操作经过优化，只会提取未压缩的行外值的所需部分。
- “主要”策略允许压缩，但不允许行外存储。 仍会针对此类列执行行外存储，但仅当没有其他任何方法可将行变得足够小，使之可以适合页面时，才使用这种最终手段。

## <a name="using-toast-table-storage-strategies"></a>使用 TOAST 表存储策略
如果查询访问 toast 数据类型，请考虑使用“主要”策略而不是默认的“扩展”策略选项，以减少查询时间。 “主要”策略不防碍行外存储。 但是，如果查询不访问 toast 数据类型，则保留“扩展”选项可能有利。 这样，主表中的大部分行将会装入共享的缓冲区缓存中，从而有助于提高性能。

如果某个工作负荷使用的架构包含宽表和较多的字符，请考虑使用 PostgreSQL TOAST 表。 例如，某个客户表包含 350 个以上的列，其中多个列包含的字符数超过 255 个。 转换“主要”TOAST 策略后，基准查询时间从 4203 秒减少至 467 秒，性能改善了 89%。

## <a name="next-steps"></a>后续步骤
查看工作负荷的上述特征。 

查看以下 PostgreSQL 文档：[第 68 章：数据库物理存储](https://www.postgresql.org/docs/current/storage-toast.html) 