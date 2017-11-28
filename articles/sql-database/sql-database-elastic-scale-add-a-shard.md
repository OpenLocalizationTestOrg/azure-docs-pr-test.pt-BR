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
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="7dc75-103">Adicionando um fragmento usando ferramentas do Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="7dc75-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="7dc75-104">tooadd um fragmento para um novo intervalo ou uma chave</span><span class="sxs-lookup"><span data-stu-id="7dc75-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="7dc75-105">Aplicativos geralmente precisa toosimply adicionar novos fragmentos toohandle dados que são esperados de novas chaves ou intervalos de chaves para um mapa do fragmento que já existe.</span><span class="sxs-lookup"><span data-stu-id="7dc75-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="7dc75-106">Por exemplo, um aplicativo fragmentado por ID de locatário pode ser necessário tooprovision um novo fragmento para um novo locatário ou mensal de dados fragmentados talvez seja necessário um novo fragmento provisionado antes do início da saudação de cada novo mês.</span><span class="sxs-lookup"><span data-stu-id="7dc75-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="7dc75-107">Se o novo intervalo de valores de chave de Olá não ainda faz parte de um mapeamento existente, é tooadd muito simples Olá novo fragmento e associar Olá nova chave ou intervalo toothat fragmento.</span><span class="sxs-lookup"><span data-stu-id="7dc75-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="7dc75-108">Exemplo: adicionando um fragmento e seu mapa de fragmento intervalo tooan existente</span><span class="sxs-lookup"><span data-stu-id="7dc75-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="7dc75-109">Este exemplo usa Olá [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) Olá [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) métodos e cria uma instância de saudação [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe.</span><span class="sxs-lookup"><span data-stu-id="7dc75-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="7dc75-110">No exemplo hello abaixo, um banco de dados denominado **sample_shard_2** e todos os objetos de esquema necessárias dentro dele tem sido criados toohold intervalo [300, 400).</span><span class="sxs-lookup"><span data-stu-id="7dc75-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

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


<span data-ttu-id="7dc75-111">Como alternativa, você pode usar o Powershell toocreate um novo Gerenciador de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="7dc75-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="7dc75-112">Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="7dc75-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="7dc75-113">tooadd um fragmento para uma parte vazia de um intervalo existente</span><span class="sxs-lookup"><span data-stu-id="7dc75-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="7dc75-114">Em algumas circunstâncias, já mapeado a um fragmento de tooa de intervalo e parcialmente preenchido com dados, mas agora deseja fragmento de diferentes dados futuros toobe tooa direcionado.</span><span class="sxs-lookup"><span data-stu-id="7dc75-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="7dc75-115">Por exemplo, você fragmento por dia de intervalo e já ter alocado fragmento de tooa 50 dias, mas no dia 24, deseja que os dados futuros tooland em um fragmento diferente.</span><span class="sxs-lookup"><span data-stu-id="7dc75-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="7dc75-116">banco de dados Elástico Olá [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md) podem executar esta operação, mas se a movimentação de dados não é necessária (por exemplo, dados de intervalo de saudação de dias [25, 50), ou seja, too50 inclusivo do dia 25 exclusivo, ainda não existir) você pode executar Este inteiramente usando Olá diretamente APIs de gerenciamento de mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="7dc75-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="7dc75-117">Exemplo: dividindo um intervalo e atribuindo Olá vazia fragmento recentemente adicionado do parte tooa</span><span class="sxs-lookup"><span data-stu-id="7dc75-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="7dc75-118">Um banco de dados chamado "sample_shard_2" e todos os objetos de esquema necessários dentro dele foram criados.</span><span class="sxs-lookup"><span data-stu-id="7dc75-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

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

<span data-ttu-id="7dc75-119">**Importante**: Use essa técnica somente se tiver certeza de que Olá intervalo para mapeamento de saudação atualizado está vazio.</span><span class="sxs-lookup"><span data-stu-id="7dc75-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="7dc75-120">métodos de saudação acima não verificam dados para o intervalo de saudação que está sendo movido, portanto, é melhor tooinclude verifica no seu código.</span><span class="sxs-lookup"><span data-stu-id="7dc75-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="7dc75-121">Se existirem linhas no intervalo de saudação que está sendo movido, distribuição de dados reais de saudação não corresponderão mapa do fragmento atualizado de saudação.</span><span class="sxs-lookup"><span data-stu-id="7dc75-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="7dc75-122">Saudação de uso [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md) tooperform Olá operação em vez disso, nesses casos.</span><span class="sxs-lookup"><span data-stu-id="7dc75-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

