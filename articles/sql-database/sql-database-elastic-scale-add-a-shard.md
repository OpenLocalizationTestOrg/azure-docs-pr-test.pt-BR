---
title: "aaaAdding um fragmento usando as ferramentas de banco de dados Elástico | Microsoft Docs"
description: "Como configurar toouse APIs de dimensionamento Elástico tooadd novo fragmentos tooa fragmento."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Adicionando um fragmento usando ferramentas do Banco de Dados Elástico
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd um fragmento para um novo intervalo ou uma chave
Aplicativos geralmente precisa toosimply adicionar novos fragmentos toohandle dados que são esperados de novas chaves ou intervalos de chaves para um mapa do fragmento que já existe. Por exemplo, um aplicativo fragmentado por ID de locatário pode ser necessário tooprovision um novo fragmento para um novo locatário ou mensal de dados fragmentados talvez seja necessário um novo fragmento provisionado antes do início da saudação de cada novo mês. 

Se o novo intervalo de valores de chave de Olá não ainda faz parte de um mapeamento existente, é tooadd muito simples Olá novo fragmento e associar Olá nova chave ou intervalo toothat fragmento. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Exemplo: adicionando um fragmento e seu mapa de fragmento intervalo tooan existente
Este exemplo usa Olá [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) Olá [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) métodos e cria uma instância de saudação [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe. No exemplo hello abaixo, um banco de dados denominado **sample_shard_2** e todos os objetos de esquema necessárias dentro dele tem sido criados toohold intervalo [300, 400).  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


Como alternativa, você pode usar o Powershell toocreate um novo Gerenciador de mapa do fragmento. Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd um fragmento para uma parte vazia de um intervalo existente
Em algumas circunstâncias, já mapeado a um fragmento de tooa de intervalo e parcialmente preenchido com dados, mas agora deseja fragmento de diferentes dados futuros toobe tooa direcionado. Por exemplo, você fragmento por dia de intervalo e já ter alocado fragmento de tooa 50 dias, mas no dia 24, deseja que os dados futuros tooland em um fragmento diferente. banco de dados Elástico Olá [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md) podem executar esta operação, mas se a movimentação de dados não é necessária (por exemplo, dados de intervalo de saudação de dias [25, 50), ou seja, too50 inclusivo do dia 25 exclusivo, ainda não existir) você pode executar Este inteiramente usando Olá diretamente APIs de gerenciamento de mapa do fragmento.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Exemplo: dividindo um intervalo e atribuindo Olá vazia fragmento recentemente adicionado do parte tooa
Um banco de dados chamado "sample_shard_2" e todos os objetos de esquema necessários dentro dele foram criados.  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**Importante**: Use essa técnica somente se tiver certeza de que Olá intervalo para mapeamento de saudação atualizado está vazio.  métodos de saudação acima não verificam dados para o intervalo de saudação que está sendo movido, portanto, é melhor tooinclude verifica no seu código.  Se existirem linhas no intervalo de saudação que está sendo movido, distribuição de dados reais de saudação não corresponderão mapa do fragmento atualizado de saudação. Saudação de uso [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Olá operação em vez disso, nesses casos.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

