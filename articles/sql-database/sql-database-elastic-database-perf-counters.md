---
title: contadores de aaaPerformance do Gerenciador do mapa de fragmentos
description: Classe do ShardMapManager e contadores de desempenho de roteamento dependente de dados
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Contadores de desempenho do gerenciador de mapa de fragmentos
Você pode capturar o desempenho de saudação de um [Gerenciador do mapa de fragmentos](sql-database-elastic-scale-shard-map-management.md), especialmente ao usar [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md). Contadores são criados com métodos de saudação Microsoft.Azure.SqlDatabase.ElasticScale.Client classe.  

Contadores são usados tootrack Olá desempenho de [roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md) operações. Esses contadores são acessíveis no hello Monitor de desempenho, na categoria de "Gerenciamento de fragmento de: de banco de dados que Elástico" hello.

**Para a versão mais recente do hello:** ir muito[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Consulte também [atualizar uma aplicativo toouse hello mais recente Elástico de banco de dados biblioteca de cliente](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Pré-requisitos
* categoria de desempenho de saudação toocreate e contadores, Olá usuário deve ser uma parte da saudação local **administradores** grupo máquina Olá hospedando o aplicativo hello.  
* toocreate um desempenho de instância do contador e atualizar contadores hello, Olá usuário deve ser um membro de qualquer hello **administradores** ou **usuários de Monitor de desempenho** grupo. 

## <a name="create-performance-category-and-counters"></a>Criar categoria e contadores de desempenho
contadores de saudação toocreate, chamar o método de CreatePeformanceCategoryAndCounters de saudação de Olá [ShardMapManagmentFactory classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Somente um administrador pode executar o método hello: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

Você também pode usar [isso](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) método de saudação do tooexecute de script do PowerShell. método Hello cria Olá contadores de desempenho a seguir:  

* **Armazenado em cache mapeamentos**: número de mapeamentos armazenados em cache para o mapa do fragmento hello.
* **Operações/s DDR**: taxa de operações de roteamento dependente de dados para o mapa do fragmento hello. Esse contador é atualizado quando uma chamada muito[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) resulta em um fragmento de destino toohello conexão bem-sucedida. 
* **Mapeamento de pesquisa de acertos de cache/s**: taxa de operações de pesquisa de cache bem-sucedida para mapeamentos no mapa do fragmento hello. 
* **Mapeamento de pesquisa de erros de cache/s**: taxa de operações de pesquisa de cache com falha para mapeamentos no mapa do fragmento hello.
* **Mapeamentos adicionados ou atualizados no cache/s**: taxa na qual mapeamentos estão sendo adicionados ou atualizados no cache para o mapa do fragmento hello. 
* **Os mapeamentos são removidos do cache/s**: taxa em que os mapeamentos estão sendo removidos do cache para o mapa do fragmento Olá. 

Contadores de desempenho são criados para cada mapa de fragmentos em cache por processo.  

## <a name="notes"></a>Observações
Olá seguintes eventos disparam criação Olá Olá de contadores de desempenho:  

* Inicialização de saudação [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) com [carregamento adiantado](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), se Olá ShardMapManager contém qualquer mapas de fragmento. Esses incluem hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) e hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) métodos.
* Pesquisa bem-sucedida de um mapa de fragmentos (usando [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) ou [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Criação bem-sucedida do mapa de fragmentos usando CreateShardMap().

contadores de desempenho de saudação serão atualizados por todas as operações de cache executadas em mapeamentos e o mapa do fragmento hello. Remoção bem-sucedida do mapa do fragmento hello usando DeleteShardMap () reults na exclusão da instância de contadores de desempenho de saudação.  

## <a name="best-practices"></a>Práticas recomendadas
* Criação de categoria de saudação de desempenho e contadores deve ser executada somente uma vez antes da criação de saudação do objeto ShardMapManager. Cada execução do comando Olá CreatePerformanceCategoryAndCounters() limpa contadores anterior de saudação (perda de dados reportados por todas as instâncias) e cria novas.  
* Instâncias de contador de desempenho são criadas por processo. Qualquer falha do aplicativo ou a remoção de um mapa do fragmento do cache de saudação resultará na exclusão de instâncias de contadores de desempenho de saudação.  

### <a name="see-also"></a>Consulte também
[Visão geral dos recursos do Banco de Dados Elástico](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

