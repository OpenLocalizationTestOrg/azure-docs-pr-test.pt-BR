---
title: bancos de dados do SQL Azure fragmentados aaaQuery | Microsoft Docs
description: "Execute consultas entre fragmentos usando a biblioteca de cliente do banco de dados Elástico hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Consulta de vários fragmentos
## <a name="overview"></a>Visão geral
Com hello [ferramentas de banco de dados Elástico](sql-database-elastic-scale-introduction.md), você pode criar soluções de banco de dados fragmentado. **Consulta de vários fragmentos** é usada para tarefas, como coleta/relatórios de dados que exigem a execução de uma consulta que se estende por vários fragmentos. (Compare muito[roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md), que executa todo o trabalho em um único fragmento.) 

1. Obter um [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) usando Olá [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), Olá [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) método. Consulte [**Construindo um ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) e [**Obter um RangeShardMap ou ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Crie um objeto **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**.
3. Crie um **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Saudação de conjunto  **[propriedade CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa comando T-SQL.
5. Executar o comando Olá por chamada hello  **[método ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Exibir resultados de saudação usando Olá  **[MultiShardDataReader classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Exemplo
Olá, código a seguir ilustra Olá uso de vários fragmentos consultas usando um determinado **ShardMap** chamado *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
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


Uma diferença importante é a construção de saudação de conexões de vários fragmentos. Onde **SqlConnection** opera em um único banco de dados, hello **MultiShardConnection** leva um ***conjunto de fragmentos*** como sua entrada. Preencha a coleção de saudação de fragmentos de um mapa de fragmento. consulta de Hello, em seguida, é executada na coleção de saudação de fragmentos usando **UNION ALL** semântica tooassemble um único resultado geral. Opcionalmente, nome de saudação do fragmento Olá qual linha hello origina pode ser adicionado toohello saída usando Olá **ExecutionOptions** propriedade no comando. 

Observe a chamada de saudação muito**myShardMap.GetShards()**. Esse método recupera todos os fragmentos de mapa do fragmento hello e fornece uma maneira fácil de toorun uma consulta em todos os bancos de dados relevantes. Olá coleção de fragmentos para uma consulta de vários fragmento pode ser refinada executando um LINQ consultar mais coleção Olá retornado da chamada de saudação muito**myShardMap.GetShards()**. Em combinação com a política de resultados parciais hello, a funcionalidade atual Olá em vários fragmentos uma consulta tiver sido projetado toowork bem para dezenas backup toohundreds de fragmentos.

Uma limitação com vários fragmentos de consulta no momento é falta de saudação de validação para fragmentos e shardlets são consultados. Enquanto o roteamento dependente de dados verifica que um fragmento especificado faz parte do mapa do fragmento Olá no tempo de saudação da consulta, consultas de vários fragmentos não executar essa verificação. Isso pode levar a consultas de fragmento toomulti executando em bancos de dados que foram removidos do mapa do fragmento hello.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Consultas de vários fragmentos e operações de divisão/mesclagem
Vários fragmentos consultas não verifica se shardlets no banco de dados consultado Olá participam de operações de divisão de mesclagem em andamento. (Consulte [dimensionamento usando a ferramenta Olá direta de divisão de banco de dados Elástico](sql-database-elastic-scale-overview-split-and-merge.md).) Isso pode levar tooinconsistencies onde linhas de Olá mesma apresentação de shardlet para vários bancos de dados Olá mesma consulta vários fragmento. Esteja atento essas limitações e considere drenagem contínuo divisão mesclagem operações e alterações toohello mapa do fragmento ao executar consultas de vários fragmentos.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Consulte também
Classes e métodos **[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**.

Gerenciar fragmentos usando Olá [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md). Inclui um namespace chamado [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) que fornece Olá capacidade tooquery vários fragmentos usando uma única consulta e resultado. Ele fornece uma abstração de consulta em uma coleção de fragmentos. Ele também fornece as políticas de execução alternativo, resultados parciais em particular, toodeal com falhas ao consultar em vários fragmentos.  

