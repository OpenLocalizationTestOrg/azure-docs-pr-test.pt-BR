---
title: Como dimensionar o Cache Redis do Azure | Microsoft Docs
description: "Saiba como dimensionar suas instâncias do Cache Redis do Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 91b3580491a1e3504a3891b66606a9bd18c0638f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="16224-103">Como dimensionar o Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="16224-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="16224-104">O Cache Redis do Azure tem diferentes ofertas de cache que fornecem flexibilidade na escolha do tamanho e dos recursos de cache.</span><span class="sxs-lookup"><span data-stu-id="16224-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="16224-105">Se os requisitos de seu aplicativo se alterarem depois que um cache for criado, você poderá dimensionar o tamanho e o tipo de preço desse cache.</span><span class="sxs-lookup"><span data-stu-id="16224-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="16224-106">Este artigo mostra como dimensionar seu cache no Portal do Azure e usando ferramentas como o Azure PowerShell e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="16224-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="16224-107">Quando dimensionar</span><span class="sxs-lookup"><span data-stu-id="16224-107">When to scale</span></span>
<span data-ttu-id="16224-108">Você pode usar os recursos de [monitoramento](cache-how-to-monitor.md) do Cache Redis do Azure para monitorar a integridade e o desempenho do seu cache e para ajudar a determinar se é necessário dimensionar o cache.</span><span class="sxs-lookup"><span data-stu-id="16224-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="16224-109">Você pode monitorar as métricas a seguir para ajudá-lo a determinar se é preciso dimensionar.</span><span class="sxs-lookup"><span data-stu-id="16224-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="16224-110">Carga do Servidor Redis</span><span class="sxs-lookup"><span data-stu-id="16224-110">Redis Server Load</span></span>
* <span data-ttu-id="16224-111">Uso de Memória</span><span class="sxs-lookup"><span data-stu-id="16224-111">Memory Usage</span></span>
* <span data-ttu-id="16224-112">Largura de Banda de Rede</span><span class="sxs-lookup"><span data-stu-id="16224-112">Network Bandwidth</span></span>
* <span data-ttu-id="16224-113">Uso da CPU</span><span class="sxs-lookup"><span data-stu-id="16224-113">CPU Usage</span></span>

<span data-ttu-id="16224-114">Se você determinar que o cache não atende mais aos requisitos de seu aplicativo, você poderá mudar para um tipo de preço de cache maior ou menor, que seja adequado ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16224-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="16224-115">Para obter mais informações sobre como determinar qual camada de preços de cache usar, consulte [Qual oferta e tamanho do Cache Redis devo usar](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="16224-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="16224-116">Dimensionar um cache</span><span class="sxs-lookup"><span data-stu-id="16224-116">Scale a cache</span></span>
<span data-ttu-id="16224-117">Para dimensionar o cache, [navegue até ele](cache-configure.md#configure-redis-cache-settings) no [Portal do Azure](https://portal.azure.com) e clique em **Dimensionar** no **menu Recurso**.</span><span class="sxs-lookup"><span data-stu-id="16224-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![Escala](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="16224-119">Selecione o tipo de preço desejado na folha **Selecionar tipo de preço** e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="16224-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![Tipo de preço][redis-cache-pricing-tier-blade]


<span data-ttu-id="16224-121">Você pode dimensionar para um tipo de preço diferente com as restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="16224-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="16224-122">Você não pode dimensionar de uma camada de preços mais alta para uma camada de preços mais baixa.</span><span class="sxs-lookup"><span data-stu-id="16224-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="16224-123">Você não pode dimensionar de um cache **Premium** para um cache **Standard** ou **Básico**.</span><span class="sxs-lookup"><span data-stu-id="16224-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="16224-124">Você não pode dimensionar de um cache **Standard** para um cache **Básico**.</span><span class="sxs-lookup"><span data-stu-id="16224-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="16224-125">É possível dimensionar de um cache **Básico** para um cache **Standard**, mas não é possível alterar o tamanho simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="16224-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="16224-126">Se precisar de um tamanho diferente, você pode fazer uma operação de dimensionamento subsequente para o tamanho desejado.</span><span class="sxs-lookup"><span data-stu-id="16224-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="16224-127">Você não pode dimensionar de um cache **Básico** diretamente para um cache **Premium**.</span><span class="sxs-lookup"><span data-stu-id="16224-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="16224-128">Você deve dimensionar do **Básico** para o **Standard** em uma única operação de dimensionamento e do **Standard** para o **Premium** em uma operação de dimensionamento subsequente.</span><span class="sxs-lookup"><span data-stu-id="16224-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="16224-129">Não é possível dimensionar de um tamanho maior para o tamanho **C0 (250 MB)** .</span><span class="sxs-lookup"><span data-stu-id="16224-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="16224-130">Enquanto o cache é dimensionado para o novo tipo de preços, um status **Dimensionando** é exibido na folha do **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="16224-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![Dimensionamento][redis-cache-scaling]

<span data-ttu-id="16224-132">Quando o dimensionamento for concluído, o status será alterado de **Dimensionando** para **Executando**.</span><span class="sxs-lookup"><span data-stu-id="16224-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="16224-133">Como automatizar uma operação de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="16224-133">How to automate a scaling operation</span></span>
<span data-ttu-id="16224-134">Além de dimensionar as instâncias do cache no Portal do Azure, você pode dimensionar usando cmdlets do PowerShell, a CLI do Azure e a MAML (Bibliotecas de Gerenciamento do Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="16224-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="16224-135">Dimensionar usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="16224-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="16224-136">Dimensionar usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="16224-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="16224-137">Dimensionar usando MAML</span><span class="sxs-lookup"><span data-stu-id="16224-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="16224-138">Dimensionar usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="16224-138">Scale using PowerShell</span></span>
<span data-ttu-id="16224-139">É possível dimensionar as instâncias do Cache Redis do Azure com o PowerShell usando o cmdlet [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) quando as propriedades `Size`, `Sku` ou `ShardCount` forem modificadas.</span><span class="sxs-lookup"><span data-stu-id="16224-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="16224-140">O exemplo a seguir mostra como dimensionar um cache denominado `myCache` para um cache de 2,5 GB.</span><span class="sxs-lookup"><span data-stu-id="16224-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="16224-141">Para obter mais informações sobre o dimensionamento com o PowerShell, confira [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="16224-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="16224-142">Dimensionar usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="16224-142">Scale using Azure CLI</span></span>
<span data-ttu-id="16224-143">Para dimensionar instâncias do Cache Redis do Azure usando a CLI do Azure, chame o comando `azure rediscache set` e transmita as mudanças de configuração desejadas que incluam novo tamanho, SKU ou tamanho de cluster, de acordo com a operação de dimensionamento desejada.</span><span class="sxs-lookup"><span data-stu-id="16224-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="16224-144">Para obter mais informações sobre o dimensionamento com CLI do Azure, confira [Alterar as configurações de um Cache Redis existente](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="16224-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="16224-145">Dimensionar usando MAML</span><span class="sxs-lookup"><span data-stu-id="16224-145">Scale using MAML</span></span>
<span data-ttu-id="16224-146">Para dimensionar as instâncias do Cache Redis do Azure usando a [MAML (Bibliotecas de Gerenciamento do Microsoft Azure)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), chame o método `IRedisOperations.CreateOrUpdate` e transmita o novo tamanho para `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="16224-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="16224-147">Para obter mais informações, consulte o exemplo [Gerenciar o Cache Redis usando MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) .</span><span class="sxs-lookup"><span data-stu-id="16224-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="16224-148">Perguntas frequentes sobre dimensionamento</span><span class="sxs-lookup"><span data-stu-id="16224-148">Scaling FAQ</span></span>
<span data-ttu-id="16224-149">A lista a seguir contém as respostas a perguntas frequentes sobre o dimensionamento do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="16224-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="16224-150">Posso escalonar para um cache Premium, por meio dele ou nele?</span><span class="sxs-lookup"><span data-stu-id="16224-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="16224-151">Depois do dimensionamento, é necessário alterar minhas chaves de acesso ou o nome do cache?</span><span class="sxs-lookup"><span data-stu-id="16224-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="16224-152">Como funciona o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="16224-153">Perderei dados de meu cache durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="16224-154">A configuração dos meus bancos de dados personalizados foi afetada durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="16224-155">O cache estará disponível durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="16224-156">Operações que não têm suporte</span><span class="sxs-lookup"><span data-stu-id="16224-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="16224-157">Quanto tempo o dimensionamento leva?</span><span class="sxs-lookup"><span data-stu-id="16224-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="16224-158">Como saber quando o dimensionamento é concluído?</span><span class="sxs-lookup"><span data-stu-id="16224-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="16224-159">Posso escalonar para um cache Premium, por meio dele ou nele?</span><span class="sxs-lookup"><span data-stu-id="16224-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="16224-160">Você não pode dimensionar de um cache **Premium** para um tipo de preço **Básico** ou **Standard**.</span><span class="sxs-lookup"><span data-stu-id="16224-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="16224-161">Você pode dimensionar de um tipo de preço de cache **Premium** para outro.</span><span class="sxs-lookup"><span data-stu-id="16224-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="16224-162">Você não pode dimensionar de um cache **Básico** diretamente para um cache **Premium**.</span><span class="sxs-lookup"><span data-stu-id="16224-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="16224-163">Primeiro, você deve dimensionar do **Básico** para o **Standard** em uma única operação de dimensionamento e do **Standard** para o **Premium** em uma operação de dimensionamento subsequente.</span><span class="sxs-lookup"><span data-stu-id="16224-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="16224-164">Se você habilitou o clustering quando criou o cache **Premium** , será possível [alterar o tamanho do cluster](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="16224-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="16224-165">Se o cache foi criado sem clustering habilitado, não é possível configurar o clustering em um momento posterior.</span><span class="sxs-lookup"><span data-stu-id="16224-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="16224-166">Para saber mais, consulte [Como configurar um cluster para um Cache Redis do Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="16224-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="16224-167">Depois do dimensionamento, é necessário alterar minhas chaves de acesso ou o nome do cache?</span><span class="sxs-lookup"><span data-stu-id="16224-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="16224-168">Não, o nome do cache e as chaves permanecem inalterados durante uma operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="16224-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="16224-169">Como funciona o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-169">How does scaling work?</span></span>
* <span data-ttu-id="16224-170">Quando um cache **Básico** é escalonado para um tamanho diferente, ele é desligado e um novo cache é provisionado usando o novo tamanho.</span><span class="sxs-lookup"><span data-stu-id="16224-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="16224-171">Durante esse tempo, o cache não está disponível e todos os dados em cache são perdidos.</span><span class="sxs-lookup"><span data-stu-id="16224-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="16224-172">Quando um cache **Básico** é escalonado para um cache **Standard**, um cache de réplica é provisionado e os dados são copiados do cache primário no cache de réplica.</span><span class="sxs-lookup"><span data-stu-id="16224-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="16224-173">O cache permanece disponível durante o processo de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="16224-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="16224-174">Quando um cache **Standard** é dimensionado para um tamanho diferente ou para um cache **Premium**, uma das réplicas é desligada e provisionada novamente para o novo tamanho, os dados são transferidos e a outra réplica executa um failover antes de ser provisionada novamente, de forma semelhante ao processo que ocorre durante uma falha em um dos nós de cache.</span><span class="sxs-lookup"><span data-stu-id="16224-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="16224-175">Perderei dados de meu cache durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="16224-176">Quando um cache **Básico** é escalonado para um novo tamanho, todos os dados são perdidos, e o cache fica indisponível durante a operação de colocação em escala.</span><span class="sxs-lookup"><span data-stu-id="16224-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="16224-177">Quando um cache **Básico** é dimensionado para um cache **Standard**, os dados no cache geralmente são preservados.</span><span class="sxs-lookup"><span data-stu-id="16224-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="16224-178">Quando um cache **Standard** é dimensionado para uma camada ou tamanho maior, ou quando um cache **Premium** é dimensionado para um tamanho maior, todos os dados normalmente são preservados.</span><span class="sxs-lookup"><span data-stu-id="16224-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="16224-179">Ao se dimensionar um cache **Standard** ou **Premium** para um tamanho menor, dados podem ser perdidos, dependendo da quantidade de dados estão no cache em relação ao novo tamanho quando ele for dimensionado.</span><span class="sxs-lookup"><span data-stu-id="16224-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="16224-180">Se dados forem perdidos ao se reduzir, as chaves serão removidas usando a política de remoção [allkeys-lru](http://redis.io/topics/lru-cache) .</span><span class="sxs-lookup"><span data-stu-id="16224-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="16224-181">A configuração dos meus bancos de dados personalizados foi afetada durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="16224-182">Alguns tipos de preço têm diferentes [limites de bancos de dados`databases`, portanto, há algumas considerações a fazer ao reduzir verticalmente um valor personalizado para a configuração ](cache-configure.md#databases) durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="16224-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="16224-183">Ao escalar para um tipo de preço com menos `databases` limite do que a camada atual:</span><span class="sxs-lookup"><span data-stu-id="16224-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="16224-184">Se você estiver usando o número padrão de `databases`, que é 16 para todos os tipos de preço, nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="16224-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="16224-185">Se você estiver usando um número personalizado de `databases`, que se encaixa dentro dos limites do tipo para o qual você está dimensionando, essa configuração `databases` será mantida e nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="16224-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="16224-186">Se você estiver usando um número personalizado de `databases`, que excede os limites do novo tipo, a configuração `databases` será reduzida para os limites do novo tipo e todos os dados nos bancos de dados removidos são perdidos.</span><span class="sxs-lookup"><span data-stu-id="16224-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="16224-187">Ao escalonar para um tipo de preço com o mesmo limite ou limite superior `databases` do que o tipo atual, sua configuração `databases` é mantida e nenhum dado é perdido.</span><span class="sxs-lookup"><span data-stu-id="16224-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="16224-188">Observe que, embora os caches Standard e Premium tenham um SLA de 99,9% de disponibilidade, não há SLA para perda de dados.</span><span class="sxs-lookup"><span data-stu-id="16224-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="16224-189">O cache estará disponível durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="16224-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="16224-190">Os caches **Standard** e **Premium** permanecem disponíveis durante a operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="16224-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="16224-191">Os caches **Básicos** ficam offline durante as operações de dimensionamento para um tamanho diferente, mas permanecem disponíveis durante o dimensionamento do **Básico** para **Standard**.</span><span class="sxs-lookup"><span data-stu-id="16224-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="16224-192">Operações que não têm suporte</span><span class="sxs-lookup"><span data-stu-id="16224-192">Operations that are not supported</span></span>
* <span data-ttu-id="16224-193">Você não pode dimensionar de uma camada de preços mais alta para uma camada de preços mais baixa.</span><span class="sxs-lookup"><span data-stu-id="16224-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="16224-194">Você não pode dimensionar de um cache **Premium** para um cache **Standard** ou **Básico**.</span><span class="sxs-lookup"><span data-stu-id="16224-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="16224-195">Você não pode dimensionar de um cache **Standard** para um cache **Básico**.</span><span class="sxs-lookup"><span data-stu-id="16224-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="16224-196">É possível dimensionar de um cache **Básico** para um cache **Standard**, mas não é possível alterar o tamanho simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="16224-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="16224-197">Se precisar de um tamanho diferente, você pode fazer uma operação de dimensionamento subsequente para o tamanho desejado.</span><span class="sxs-lookup"><span data-stu-id="16224-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="16224-198">Você não pode dimensionar de um cache **Básico** diretamente para um cache **Premium**.</span><span class="sxs-lookup"><span data-stu-id="16224-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="16224-199">Primeiro, você deve dimensionar do **Básico** para o **Standard** em uma única operação de dimensionamento e do **Standard** para o **Premium** em uma operação de dimensionamento subsequente.</span><span class="sxs-lookup"><span data-stu-id="16224-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="16224-200">Não é possível dimensionar de um tamanho maior para o tamanho **C0 (250 MB)** .</span><span class="sxs-lookup"><span data-stu-id="16224-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="16224-201">Se uma operação de dimensionamento falhar, o serviço tentará reverter a operação, e o cache será revertido para o tamanho original.</span><span class="sxs-lookup"><span data-stu-id="16224-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="16224-202">Quanto tempo o dimensionamento leva?</span><span class="sxs-lookup"><span data-stu-id="16224-202">How long does scaling take?</span></span>
<span data-ttu-id="16224-203">O dimensionamento leva aproximadamente 20 minutos, dependendo da quantidade de dados no cache.</span><span class="sxs-lookup"><span data-stu-id="16224-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="16224-204">Como saber quando o dimensionamento é concluído?</span><span class="sxs-lookup"><span data-stu-id="16224-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="16224-205">No portal do Azure, você pode ver a operação de dimensionamento em andamento.</span><span class="sxs-lookup"><span data-stu-id="16224-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="16224-206">Quando o dimensionamento for concluído, o status do cache será alterado para **Executando**.</span><span class="sxs-lookup"><span data-stu-id="16224-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



