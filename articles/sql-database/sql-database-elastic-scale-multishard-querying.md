---
title: Consultar bancos de dados fragmentados do SQL do Azure | Microsoft Docs
description: "Execute consultas entre fragmentos usando a biblioteca de cliente de banco de dados elástico."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: torsteng
ms.openlocfilehash: 33128357bd5b2bd744c5c1c3032f658ebe865d49
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="multi-shard-querying"></a>Consulta de vários fragmentos
## <a name="overview"></a>Visão geral
Com as [ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-introduction.md), você pode criar soluções de banco de dados fragmentado. **Consulta de vários fragmentos** é usada para tarefas, como coleta/relatórios de dados que exigem a execução de uma consulta que se estende por vários fragmentos. (Compare-a com o [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md), que executa todo o trabalho em um único fragmento). 

1. Obtenha um **RangeShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807318.aspx)) ou **ListShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807370.aspx)) usando o método **TryGetRangeShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetrangeshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)), **TryGetListShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetlistshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)) ou **GetShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.getshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)). Consulte **[Construindo um ShardMapManager](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager)** e **[Obter um RangeShardMap ou ListShardMap](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap)**.
2. Criar um **MultiShardConnection** (objeto [Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_connection), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)).
3. Criar um **MultiShardStatement ou MultiShardCommand** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_statement), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)). 
4. Defina a **propriedade CommandText** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_statement), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)) para um comando T-SQL.
5. Execute o comando chamando o método **ExecuteQueryAsync ou ExecuteReader** ([Java](), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)).
6. Veja os resultados usando a classe **MultiShardResultSet ou MultiShardDataReader** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_result_set), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)). 

## <a name="example"></a>Exemplo
O código a seguir ilustra o uso da consulta de vários fragmentos usando um determinado **ShardMap** chamado *myShardMap*. 

```csharp
using (MultiShardConnection conn = new MultiShardConnection(myShardMap.GetShards(), myShardConnectionString)) 
{ 
    using (MultiShardCommand cmd = conn.CreateCommand())
    { 
        cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
        cmd.CommandType = CommandType.Text; 
        cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
        cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

        using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
        { 
            while (sdr.Read())
            { 
                var c1Field = sdr.GetString(0); 
                var c2Field = sdr.GetFieldValue<int>(1); 
                var c3Field = sdr.GetFieldValue<Int64>(2);
            } 
        } 
    } 
} 
```

Uma diferença importante é a construção de fragmentos várias conexões. Enquanto a **SqlConnection** opera em um banco de dados individual, a **MultiShardConnection** usa um ***conjunto de fragmentos*** como sua entrada. Popule a coleção de fragmentos por meio de um mapa do fragmento. Em seguida, a consulta é executada na coleção de fragmentos usando a semântica **UNION ALL** para montar um único resultado geral. Como alternativa, o nome do fragmento que origina a linha pode ser adicionado à saída usando a propriedade **ExecutionOptions** no comando. 

Observe a chamada para **myShardMap.GetShards()**. Esse método recupera todos os fragmentos do mapa de fragmentos e fornece uma maneira fácil de executar uma consulta em todos os bancos de dados relevantes. A coleção de fragmentos para uma consulta de vários fragmento pode ser refinada ainda mais executando uma consulta LINQ sobre a coleção retornada da chamada para **myShardMap.GetShards()**. Em combinação com a política de resultados parciais, a funcionalidade atual de consultas do fragmento vários foi projetado para funcionar bem para dezenas, centenas de fragmentos.

Uma limitação com as consultas de vários fragmentos no momento é a ausência de validação de fragmentos e shardlets são consultados. Enquanto o roteamento dependentes de dados verifica que um determinado fragmento faz parte do mapa do fragmento no momento da consulta, consultas de vários fragmentos não executam essa verificação. Isso pode levar à execução de consultas em vários fragmentos em bancos de dados que já foram removidos do mapa de fragmentos.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Consultas de vários fragmentos e operações de divisão/mesclagem
Consultas de vários fragmentos não verificam se shardlets do banco de dados consultado estão participando de operações de divisão/mesclagem em andamento. (Veja [Escalando com a ferramenta de divisão e mesclagem de Banco de Dados Elástico](sql-database-elastic-scale-overview-split-and-merge.md).) Isso pode levar a inconsistências em que as linhas do mesmo shardlet são mostradas para vários bancos de dados na mesma consulta de vários fragmento. Lembre-se dessas limitações e considere drenar as operações de divisão/mesclagem em execução e alterações no mapa de fragmentos ao executar consultas de vários fragmentos.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]


