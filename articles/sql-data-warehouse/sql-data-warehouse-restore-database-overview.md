---
title: "aaaRestore um depósito de dados do Azure - local e com redundância geográfica | Microsoft Docs"
description: "Visão geral das opções de restauração de banco de dados de saudação para recuperar um banco de dados no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Restauração do SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

O SQL Data Warehouse oferece restaurações locais e geográficas como parte de suas funcionalidades de recuperação de desastre de warehouse. Use o data warehouse backups toorestore sua restauração do data warehouse tooa ponto na região primária hello, ou usar backups com redundância geográfica toorestore tooa região geográfica diferente. Este artigo explica as especificações de saudação da restauração de um data warehouse.

## <a name="what-is-a-data-warehouse-restore"></a>O que é uma restauração do data warehouse?
A restauração de um data warehouse é um novo data warehouse criado por meio de um backup de um data warehouse existente ou excluído. depósito de dados restaurados Olá recria Olá backup do data warehouse em um momento específico. Considerando que o SQL Data Warehouse é um sistema distribuído, uma restauração do data warehouse é criada por meio de muitos arquivos de backup armazenados em blobs do Azure. 

A restauração do banco de dados é uma parte essencial de qualquer estratégia de recuperação de desastre e de continuidade dos negócios, porque ela recria seus dados após uma exclusão ou corrupção acidental.

Para obter mais informações, consulte:

* [Backups do SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Visão geral da continuidade dos negócios](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Pontos de restauração do data warehouse
Uma vantagem de usar o armazenamento Premium do Azure, SQL Data Warehouse usa depósito de dados primário do Blob de armazenamento do Azure instantâneos toobackup hello. Cada instantâneo tem um ponto de restauração que representa o tempo de saudação instantâneo Olá iniciado. toorestore um data warehouse, escolha um ponto de restauração e emitir um comando de restauração.  

SQL Data Warehouse sempre restaura Olá tooa backup novo data warehouse. Você pode manter depósito de dados restaurados hello e Olá atual ou excluir um deles. Se você quiser tooreplace Olá atual do data warehouse com hello restaurado do data warehouse, você pode renomeá-la.

Se você precisar toorestore um depósito de dados excluídos ou pausado, você pode [criar um tíquete de suporte](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Restauração com redundância geográfica
Você pode restaurar sua região de tooany de depósito de dados com suporte do Azure SQL Data Warehouse com o nível de desempenho escolhido. Observe que DWU 9000 e 18000 não têm suporte em todas as regiões durante a visualização de saudação.

> [!NOTE]
> restauração de tooperform uma redundância geográfica que você não deve ter desativado para este recurso.
> 
> 

## <a name="restore-timeline"></a>Restaurar linha do tempo
Você pode restaurar um banco de dados tooany ponto de restauração disponível dentro de saudação últimos sete dias. Instantâneos de iniciar a cada quatro horas tooeight e estão disponíveis por sete dias. Quando um instantâneo possui mais de sete dias, ele expira e seu ponto de restauração fica indisponível.

## <a name="restore-costs"></a>Restaurar custos
custos de armazenamento Olá para depósito de dados restaurados Olá é cobrado na taxa de armazenamento do Azure Premium Olá. 

Se você pausar um depósito de dados restaurado, você é cobrado para armazenamento a taxa de armazenamento do Azure Premium Olá. Olá vantagem pausar é que não seja cobrado por recursos de computação de DWU hello.

Para obter mais informações sobre os preços do SQL Data Warehouse, consulte [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Usos para restauração
Olá principal uso do data warehouse restauração é toorecover dados após a perda acidental de dados ou à corrupção.

Você também pode usar o data warehouse restauração tooretain um backup por mais de sete dias. Depois de saudação backup é restaurado, você data warehouse de saudação online e pode fazer uma pausa nela indefinidamente toosave custos de computação. banco de dados pausada Olá incorre em encargos de armazenamento a taxa de armazenamento do Azure Premium Olá. 

## <a name="related-topics"></a>Tópicos relacionados
### <a name="scenarios"></a>Cenários
* Para obter uma visão geral sobre a continuidade de negócios, veja [Visão geral da continuidade de negócios](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

tooperform um data warehouse de restauração, restaurar usando:

* Azure portal, consulte [restaurar de um data warehouse usando Olá portal do Azure](sql-data-warehouse-restore-database-portal.md)
* Cmdlets do PowerShell, consulte [Restore a data warehouse using PowerShell cmdlets (Restaurar um data warehouse usando cmdlets do PowerShell)](sql-data-warehouse-restore-database-powershell.md)
* APIs REST, consulte [restaurar de um data warehouse usando Olá APIs REST](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
