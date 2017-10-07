---
title: "Azure SQL Database usando exibições de gerenciamento dinâmico de aaaMonitoring | Microsoft Docs"
description: "Saiba como toodetect e diagnosticar problemas de desempenho comuns usando exibições de gerenciamento dinâmico toomonitor banco de dados SQL do Microsoft Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a>Monitoramento de Banco de Dados SQL usando exibições de gerenciamento dinâmico
Banco de dados SQL do Microsoft Azure habilita um subconjunto de gerenciamento dinâmico exibe toodiagnose problemas de desempenho, que podem ser causados por consultas bloqueadas ou demoradas, afunilamentos de recursos, planos de consulta ruins e assim por diante. Este tópico fornece informações sobre como toodetect problemas comuns de desempenho por meio de exibições de gerenciamento dinâmico.

O Banco de Dados SQL oferece suporte parcial para três categorias de exibições de gerenciamento dinâmico:

* Exibições de gerenciamento dinâmico relacionadas ao banco de dados.
* Exibições de gerenciamento dinâmico relacionadas à execução.
* Exibições de gerenciamento dinâmico relacionadas à transação.

Para obter informações detalhadas sobre exibições de gerenciamento dinâmico, consulte [Funções e exibições (Transact-SQL) de gerenciamento dinâmico](https://msdn.microsoft.com/library/ms188754.aspx) nos Manuais Online do SQL Server.

## <a name="permissions"></a>Permissões
No Banco de Dados SQL, consultar uma visualização de gerenciamento dinâmico requer permissões **VIEW DATABASE STATE** . Olá **VIEW DATABASE STATE** permissão retorna informações sobre todos os objetos de banco de dados atual hello.
Olá toogrant **VIEW DATABASE STATE** usuário de banco de dados específico tooa permissão, execute Olá consulta a seguir:

```GRANT VIEW DATABASE STATE toodatabase_user; ```

Em uma instância do SQL Server local, as exibições de gerenciamento dinâmico retornam informações de estado do servidor. Em um Banco de Dados SQL, elas retornam informações relacionadas apenas ao seu banco de dados lógico atual.

## <a name="calculating-database-size"></a>Calculando o tamanho do banco de dados
Olá consulta a seguir retorna o tamanho de saudação do banco de dados (em megabytes):

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

Olá consulta a seguir retorna Olá tamanho dos objetos individuais (em megabytes) no banco de dados:

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a>Monitoramento de conexões
Você pode usar o hello [sys.DM exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) exibir tooretrieve informações sobre o servidor de banco de dados SQL específico do hello conexões estabelecidas tooa e detalhes de saudação de cada conexão. Além disso, Olá [sys.DM exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) exibição é útil ao recuperar as informações sobre todas as conexões de usuário ativas e tarefas internas.
Olá consulta a seguir recupera informações sobre a conexão atual hello:

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> Ao executar Olá **exec_requests** e **modos de exibição de sys.DM exec_sessions**, se você tiver **VIEW DATABASE STATE** permissão no banco de dados hello, consulte executando todas as sessões no banco de dados Olá; Caso contrário, você vê apenas Olá sessão atual.
> 
> 

## <a name="monitoring-query-performance"></a>Monitoramento de desempenho da consulta
Consultas de execução lenta ou longa podem consumir recursos significativos do sistema. Esta seção demonstra como toouse exibições de gerenciamento dinâmico toodetect alguns problemas comuns de desempenho de consulta. Uma referência mais antiga, mas ainda é útil para solução de problemas, é hello [Solucionando problemas de desempenho no SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artigo no Microsoft TechNet.

### <a name="finding-top-n-queries"></a>Localizando as principais consultas N
Olá, exemplo a seguir retorna informações sobre Olá cinco principais consultas classificadas por tempo médio de CPU. Este exemplo agrega as consultas de saudação de acordo com tootheir hash de consulta, para que as consultas logicamente equivalentes sejam agrupadas pelo respectivo consumo de recursos cumulativo.

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a>Monitoramento de consultas bloqueadas
Consultas de execução longa ou lenta podem contribuir tooexcessive o consumo de recursos e ser consequência de saudação de consultas bloqueadas. causa Olá Olá bloqueio pode ser o design de aplicativo insatisfatório, ruim planos de consulta, Olá falta de índices úteis e assim por diante. Você pode usar o hello tran_locks exibir tooget informações sobre a atividade de bloqueio atual Olá no banco de dados SQL do Azure. Para ver um exemplo de código, veja [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) nos Manuais Online do SQL Server.

### <a name="monitoring-query-plans"></a>Monitoramento de planos de consulta
Um plano de consulta ineficiente também pode aumentar o consumo de CPU. Olá, exemplo a seguir usa Olá [sys.DM exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) exibir toodetermine qual consulta usa a CPU mais cumulativa hello.

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a>Consulte também
[Introdução tooSQL banco de dados](sql-database-technical-overview.md)

