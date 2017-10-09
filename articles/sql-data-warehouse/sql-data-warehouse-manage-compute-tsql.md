---
title: aaaPause, retomar, dimensionar com T-SQL no Azure SQL Data Warehouse | Microsoft Docs
description: "Transact-SQL (T-SQL) tarefas tooscale desempenho ajustando DWUs. Reduzir custos por meio da redução durante horários que não sejam de pico."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Gerenciar poder de computação no SQL Data Warehouse do Azure (T-SQL)
> [!div class="op_single_selector"]
> * [Visão geral](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Exibir configurações atuais de DWU
tooview Olá DWU configurações para seus bancos de dados:

1. Abra o Pesquisador de Objetos do SQL Server no Visual Studio.
2. Conecte o banco de dados mestre toohello associado ao servidor de banco de dados SQL lógico hello.
3. Selecione na exibição de gerenciamento dinâmico Olá sys.database_service_objectives. Aqui está um exemplo: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Computação de escala
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

Olá toochange DWUs:

1. Conecte o banco de dados mestre toohello associado a seu servidor lógico do banco de dados SQL.
2. Saudação de uso [ALTER DATABASE] [ ALTER DATABASE] instrução TSQL. Olá, exemplo a seguir define serviço Olá nível tooDW1000 objetivo para o banco de dados Olá MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Verificar estado do banco de dados e o progresso da operação

1. Conecte o banco de dados mestre toohello associado a seu servidor lógico do banco de dados SQL.
2. Enviar o estado do banco de dados de toocheck de consulta

```sql
SELECT *
FROM
sys.databases
```

3. Enviar toocheck consultar o status da operação

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Essa DMV retornará informações sobre várias operações de gerenciamento no Data Warehouse do SQL, como o estado de operação e Olá Olá da operação de saudação, que será IN_PROGRESS ou concluída.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Próximas etapas
Para outras tarefas de gerenciamento, consulte [Visão geral de gerenciamento][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
