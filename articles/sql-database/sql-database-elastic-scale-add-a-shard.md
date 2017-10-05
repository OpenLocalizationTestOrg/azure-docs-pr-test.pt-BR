---
title: "Adicionando um fragmento usando ferramentas de banco de dados elástico | Microsoft Docs"
description: "Como usar APIs de Escala Elástica para adicionar novos fragmentos para um fragmento de conjunto."
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
ms.openlocfilehash: 6a91ea2251ea3b748faba5c97765bfded9c00234
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="a57ec-103">Adicionando um fragmento usando ferramentas do Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="a57ec-103">Adding a shard using Elastic Database tools</span></span>
## <a name="to-add-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="a57ec-104">Para adicionar um fragmento a um novo intervalo ou uma chave</span><span class="sxs-lookup"><span data-stu-id="a57ec-104">To add a shard for a new range or key</span></span>
<span data-ttu-id="a57ec-105">Geralmente, os aplicativos precisam simplesmente adicionar novos fragmentos para lidar com dados que são esperados de novas chaves ou intervalos de chaves para um mapa do fragmento que já existe.</span><span class="sxs-lookup"><span data-stu-id="a57ec-105">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="a57ec-106">Por exemplo, um aplicativo fragmentado por ID de locatário talvez tenha provisionar um novo fragmento para um novo locatário ou dados mensalmente fragmentados talvez precisem de um novo fragmento provisionado antes do início de cada novo mês.</span><span class="sxs-lookup"><span data-stu-id="a57ec-106">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="a57ec-107">Se o novo intervalo de valores de chave já não é parte de um mapeamento existente, é muito simples adicionar o novo fragmento e associar a nova chave ou o intervalo para esse fragmento.</span><span class="sxs-lookup"><span data-stu-id="a57ec-107">If the new range of key values is not already part of an existing mapping, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-to-an-existing-shard-map"></a><span data-ttu-id="a57ec-108">Exemplo: adicionar um fragmento e seu intervalo a um mapa de fragmentos existente</span><span class="sxs-lookup"><span data-stu-id="a57ec-108">Example:  adding a shard and its range to an existing shard map</span></span>
<span data-ttu-id="a57ec-109">Este exemplo usa os métodos [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx), [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx) e [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) e cria uma instância da classe [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.).</span><span class="sxs-lookup"><span data-stu-id="a57ec-109">This sample uses the [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) the [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of the [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="a57ec-110">No exemplo a seguir, um banco de dados denominado **sample_shard_2** e todos os objetos de esquema necessários dentro dele foram criados para conter o intervalo [300, 400).</span><span class="sxs-lookup"><span data-stu-id="a57ec-110">In the sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created to hold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create the mapping and associate it with the new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="a57ec-111">Como alternativa, é possível usar o Powershell para criar um novo Gerenciador de Mapa de Fragmentos.</span><span class="sxs-lookup"><span data-stu-id="a57ec-111">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="a57ec-112">Um exemplo está disponível [aqui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="a57ec-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="to-add-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="a57ec-113">Para adicionar um fragmento de uma parte vazia de um intervalo existente</span><span class="sxs-lookup"><span data-stu-id="a57ec-113">To add a shard for an empty part of an existing range</span></span>
<span data-ttu-id="a57ec-114">Em algumas circunstâncias, você já mapeou um intervalo para um fragmento e parcialmente preencheu-o com dados, mas agora deseja que os dados futuros sejam direcionados para um fragmento diferente.</span><span class="sxs-lookup"><span data-stu-id="a57ec-114">In some circumstances, you may have already mapped a range to a shard and partially filled it with data, but you now want upcoming data to be directed to a different shard.</span></span> <span data-ttu-id="a57ec-115">Por exemplo, você fragmentou o intervalo por dia e já tem 50 dias alocados para um fragmento, mas no dia 24, você deseja que os dados futuros encaixem em um fragmento diferente.</span><span class="sxs-lookup"><span data-stu-id="a57ec-115">For example, you shard by day range and have already allocated 50 days to a shard, but on day 24, you want future data to land in a different shard.</span></span> <span data-ttu-id="a57ec-116">A [ferramenta de divisão/mesclagem](sql-database-elastic-scale-overview-split-and-merge.md) do banco de dados elástico pode executar essa operação, mas se a movimentação de dados não for necessária (por exemplo, dados para o intervalo de dias [25, 50), por exemplo, o dia 25, inclusive, até o 50, inclusive, ainda não existe), você pode executar tudo isso usando as APIs de Gerenciamento de Mapa de Fragmentos diretamente.</span><span class="sxs-lookup"><span data-stu-id="a57ec-116">The elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for the range of days [25, 50), i.e., day 25 inclusive to 50 exclusive, does not yet exist) you can perform this entirely using the Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-the-empty-portion-to-a-newly-added-shard"></a><span data-ttu-id="a57ec-117">Exemplo: dividir um intervalo e atribuir a parte vazia a um fragmento adicionado recentemente</span><span class="sxs-lookup"><span data-stu-id="a57ec-117">Example: splitting a range and assigning the empty portion to a newly-added shard</span></span>
<span data-ttu-id="a57ec-118">Um banco de dados chamado "sample_shard_2" e todos os objetos de esquema necessários dentro dele foram criados.</span><span class="sxs-lookup"><span data-stu-id="a57ec-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard to hold the range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split the Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) to different shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline to a different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="a57ec-119">**Importante**: use essa técnica apenas se tiver certeza de que o intervalo para o mapeamento atualizado está vazio.</span><span class="sxs-lookup"><span data-stu-id="a57ec-119">**Important**:  Use this technique only if you are certain that the range for the updated mapping is empty.</span></span>  <span data-ttu-id="a57ec-120">Os métodos acima não verificam os dados para o intervalo que está sendo movido, portanto, é melhor incluir verificações em seu código.</span><span class="sxs-lookup"><span data-stu-id="a57ec-120">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>  <span data-ttu-id="a57ec-121">Se existirem linhas no intervalo que está sendo movido, a distribuição de dados real não corresponderá ao mapa do fragmento atualizado.</span><span class="sxs-lookup"><span data-stu-id="a57ec-121">If rows exist in the range being moved, the actual data distribution will not match the updated shard map.</span></span> <span data-ttu-id="a57ec-122">Use a [ferramenta de divisão/mesclagem](sql-database-elastic-scale-overview-split-and-merge.md) para executar a operação nesses casos.</span><span class="sxs-lookup"><span data-stu-id="a57ec-122">Use the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) to perform the operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

