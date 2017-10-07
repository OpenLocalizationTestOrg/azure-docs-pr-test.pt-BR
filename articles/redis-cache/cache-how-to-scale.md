---
title: aaaHow tooScale Cache Redis do Azure | Microsoft Docs
description: "Saiba como tooscale do Azure Redis Cache instâncias"
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
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a><span data-ttu-id="e318c-103">Como tooScale Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="e318c-103">How tooScale Azure Redis Cache</span></span>
<span data-ttu-id="e318c-104">Cache Redis do Azure tem diferentes ofertas de cache, que fornecem flexibilidade na escolha de saudação do tamanho do cache e recursos.</span><span class="sxs-lookup"><span data-stu-id="e318c-104">Azure Redis Cache has different cache offerings, which provide flexibility in hello choice of cache size and features.</span></span> <span data-ttu-id="e318c-105">Depois que um cache é criado, você pode dimensionar tamanho hello e hello preço do cache de saudação se alterarem de requisitos de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e318c-105">After a cache is created, you can scale hello size and hello pricing tier of hello cache if hello requirements of your application change.</span></span> <span data-ttu-id="e318c-106">Este artigo mostra como tooscale seu cache Olá portal do Azure e o uso de ferramentas como o PowerShell do Azure e a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-106">This article shows you how tooscale your cache in both hello Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-tooscale"></a><span data-ttu-id="e318c-107">Quando tooscale</span><span class="sxs-lookup"><span data-stu-id="e318c-107">When tooscale</span></span>
<span data-ttu-id="e318c-108">Você pode usar o hello [monitoramento](cache-how-to-monitor.md) recursos do Cache Redis do Azure toomonitor Olá integridade e desempenho do cache e ajudar a determinar quando tooscale Olá cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-108">You can use hello [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache toomonitor hello health and performance of your cache and help determine when tooscale hello cache.</span></span> 

<span data-ttu-id="e318c-109">Você pode monitorar a seguir Olá métricas toohelp determinar se é necessário tooscale.</span><span class="sxs-lookup"><span data-stu-id="e318c-109">You can monitor hello following metrics toohelp determine if you need tooscale.</span></span>

* <span data-ttu-id="e318c-110">Carga do Servidor Redis</span><span class="sxs-lookup"><span data-stu-id="e318c-110">Redis Server Load</span></span>
* <span data-ttu-id="e318c-111">Uso de Memória</span><span class="sxs-lookup"><span data-stu-id="e318c-111">Memory Usage</span></span>
* <span data-ttu-id="e318c-112">Largura de Banda de Rede</span><span class="sxs-lookup"><span data-stu-id="e318c-112">Network Bandwidth</span></span>
* <span data-ttu-id="e318c-113">Uso da CPU</span><span class="sxs-lookup"><span data-stu-id="e318c-113">CPU Usage</span></span>

<span data-ttu-id="e318c-114">Se você determinar que o cache não está atendendo aos requisitos do aplicativo, você pode dimensionar tooa cache maior ou menor preço é adequada para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e318c-114">If you determine that your cache is no longer meeting your application's requirements, you can scale tooa larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="e318c-115">Para obter mais informações sobre como determinar qual cache toouse de camada de preços, consulte [qual oferta de Cache do Redis e tamanho devo usar](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="e318c-115">For more information on determining which cache pricing tier toouse, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="e318c-116">Dimensionar um cache</span><span class="sxs-lookup"><span data-stu-id="e318c-116">Scale a cache</span></span>
<span data-ttu-id="e318c-117">tooscale seu cache, [procurar cache toohello](cache-configure.md#configure-redis-cache-settings) em Olá [portal do Azure](https://portal.azure.com) e clique em **escala** de saudação **menu recursos**.</span><span class="sxs-lookup"><span data-stu-id="e318c-117">tooscale your cache, [browse toohello cache](cache-configure.md#configure-redis-cache-settings) in hello [Azure portal](https://portal.azure.com) and click **Scale** from hello **Resource menu**.</span></span>

![Escala](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="e318c-119">Selecione Olá desejado de preços de saudação **selecione preço** folha e clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="e318c-119">Select hello desired pricing tier from hello **Select pricing tier** blade and click **Select**.</span></span>

![Tipo de preço ][redis-cache-pricing-tier-blade]


<span data-ttu-id="e318c-121">Você pode dimensionar tooa diferente preços com hello restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="e318c-121">You can scale tooa different pricing tier with hello following restrictions:</span></span>

* <span data-ttu-id="e318c-122">Não é possível redimensionar de um maior preço camada tooa menor preço.</span><span class="sxs-lookup"><span data-stu-id="e318c-122">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="e318c-123">Você não pode ser dimensionada de um **Premium** cache para baixo tooa **padrão** ou um **básica** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-123">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="e318c-124">Você não pode ser dimensionada de um **padrão** cache para baixo tooa **básica** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-124">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="e318c-125">Pode ser dimensionada de um **básica** cache tooa **padrão** cache, mas você não pode alterar o tamanho de saudação em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e318c-125">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="e318c-126">Se você precisar de um tamanho diferente, você pode fazer um tamanho de toohello desejado escala operação subsequente.</span><span class="sxs-lookup"><span data-stu-id="e318c-126">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="e318c-127">Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-127">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="e318c-128">Deve ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em uma escala subsequentes operação.</span><span class="sxs-lookup"><span data-stu-id="e318c-128">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="e318c-129">Não é possível redimensionar de um tamanho maior para baixo toohello **C0 (250 MB)** tamanho.</span><span class="sxs-lookup"><span data-stu-id="e318c-129">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="e318c-130">Enquanto está dimensionamento do cache de saudação toohello novo preço, uma **Scaling** status é exibido no hello **Redis Cache** folha.</span><span class="sxs-lookup"><span data-stu-id="e318c-130">While hello cache is scaling toohello new pricing tier, a **Scaling** status is displayed in hello **Redis Cache** blade.</span></span>

![Dimensionamento][redis-cache-scaling]

<span data-ttu-id="e318c-132">Quando o dimensionamento for concluído, o status de Olá muda de **Scaling** muito**executando**.</span><span class="sxs-lookup"><span data-stu-id="e318c-132">When scaling is complete, hello status changes from **Scaling** too**Running**.</span></span>

## <a name="how-tooautomate-a-scaling-operation"></a><span data-ttu-id="e318c-133">Como tooautomate uma operação de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="e318c-133">How tooautomate a scaling operation</span></span>
<span data-ttu-id="e318c-134">Em adição tooscaling suas instâncias de cache em Olá portal do Azure, você pode dimensionar usando cmdlets do PowerShell, CLI do Azure e usando Olá Microsoft Azure Management bibliotecas (MAML).</span><span class="sxs-lookup"><span data-stu-id="e318c-134">In addition tooscaling your cache instances in hello Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using hello Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="e318c-135">Dimensionar usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e318c-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="e318c-136">Dimensionar usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e318c-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="e318c-137">Dimensionar usando MAML</span><span class="sxs-lookup"><span data-stu-id="e318c-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="e318c-138">Dimensionar usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e318c-138">Scale using PowerShell</span></span>
<span data-ttu-id="e318c-139">Você pode dimensionar suas instâncias de Cache Redis do Azure com o PowerShell usando Olá [conjunto AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet quando hello `Size`, `Sku`, ou `ShardCount` propriedades são modificadas.</span><span class="sxs-lookup"><span data-stu-id="e318c-139">You can scale your Azure Redis Cache instances with PowerShell by using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="e318c-140">Olá exemplo a seguir mostra como tooscale um cache nomeado `myCache` tooa 2,5 GB cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-140">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="e318c-141">Para obter mais informações sobre a expansão com o PowerShell, consulte [tooscale um Redis cache usando o Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="e318c-141">For more information on scaling with PowerShell, see [tooscale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="e318c-142">Dimensionar usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e318c-142">Scale using Azure CLI</span></span>
<span data-ttu-id="e318c-143">tooscale suas instâncias de Cache Redis do Azure usando a CLI do Azure, chame Olá `azure rediscache set` comando e passe as alterações de configuração de saudação desejada que incluem um novo tamanho, o sku ou o tamanho do cluster, dependendo da saudação desejado a operação de escala.</span><span class="sxs-lookup"><span data-stu-id="e318c-143">tooscale your Azure Redis Cache instances using Azure CLI, call hello `azure rediscache set` command and pass in hello desired configuration changes that include a new size, sku, or cluster size, depending on hello desired scaling operation.</span></span>

<span data-ttu-id="e318c-144">Para obter mais informações sobre o dimensionamento com CLI do Azure, confira [Alterar as configurações de um Cache Redis existente](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="e318c-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="e318c-145">Dimensionar usando MAML</span><span class="sxs-lookup"><span data-stu-id="e318c-145">Scale using MAML</span></span>
<span data-ttu-id="e318c-146">tooscale suas instâncias de Cache Redis do Azure usando Olá [Microsoft Azure Management bibliotecas (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), chamada hello `IRedisOperations.CreateOrUpdate` método e passar no novo tamanho Olá Olá `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="e318c-146">tooscale your Azure Redis Cache instances using hello [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call hello `IRedisOperations.CreateOrUpdate` method and pass in hello new size for hello `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="e318c-147">Para obter mais informações, consulte Olá [gerenciar Redis Cache usando MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) exemplo.</span><span class="sxs-lookup"><span data-stu-id="e318c-147">For more information, see hello [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="e318c-148">Perguntas frequentes sobre dimensionamento</span><span class="sxs-lookup"><span data-stu-id="e318c-148">Scaling FAQ</span></span>
<span data-ttu-id="e318c-149">Olá lista a seguir contém as respostas toocommonly perguntas frequentes sobre o dimensionamento do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="e318c-149">hello following list contains answers toocommonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="e318c-150">Posso escalonar para um cache Premium, por meio dele ou nele?</span><span class="sxs-lookup"><span data-stu-id="e318c-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="e318c-151">Depois de escalar, é necessário toochange minhas chaves de acesso ou o nome do cache?</span><span class="sxs-lookup"><span data-stu-id="e318c-151">After scaling, do I have toochange my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="e318c-152">Como funciona o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="e318c-153">Perderei dados de meu cache durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="e318c-154">A configuração dos meus bancos de dados personalizados foi afetada durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="e318c-155">O cache estará disponível durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="e318c-156">Operações que não têm suporte</span><span class="sxs-lookup"><span data-stu-id="e318c-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="e318c-157">Quanto tempo o dimensionamento leva?</span><span class="sxs-lookup"><span data-stu-id="e318c-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="e318c-158">Como saber quando o dimensionamento é concluído?</span><span class="sxs-lookup"><span data-stu-id="e318c-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="e318c-159">Posso escalonar para um cache Premium, por meio dele ou nele?</span><span class="sxs-lookup"><span data-stu-id="e318c-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="e318c-160">Você não pode ser dimensionada de um **Premium** cache para baixo tooa **básica** ou **padrão** preço.</span><span class="sxs-lookup"><span data-stu-id="e318c-160">You can't scale from a **Premium** cache down tooa **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="e318c-161">Você pode dimensionar uma **Premium** tooanother da camada de preço do cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-161">You can scale from one **Premium** cache pricing tier tooanother.</span></span>
* <span data-ttu-id="e318c-162">Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-162">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="e318c-163">Você deve primeiro ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em um subsequente a operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e318c-163">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="e318c-164">Se você habilitou o cluster quando criou sua **Premium** cache, você pode [alterar o tamanho do cluster Olá](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="e318c-164">If you enabled clustering when you created your **Premium** cache, you can [change hello cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="e318c-165">Se o cache foi criado sem clustering habilitado, não é possível configurar o clustering em um momento posterior.</span><span class="sxs-lookup"><span data-stu-id="e318c-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="e318c-166">Para obter mais informações, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="e318c-166">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a><span data-ttu-id="e318c-167">Depois de escalar, é necessário toochange minhas chaves de acesso ou o nome do cache?</span><span class="sxs-lookup"><span data-stu-id="e318c-167">After scaling, do I have toochange my cache name or access keys?</span></span>
<span data-ttu-id="e318c-168">Não, o nome do cache e as chaves permanecem inalterados durante uma operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e318c-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="e318c-169">Como funciona o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-169">How does scaling work?</span></span>
* <span data-ttu-id="e318c-170">Quando um **básica** cache for dimensionado tooa de tamanho diferente, ele é desligado e um novo cache é configurado usando o novo tamanho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e318c-170">When a **Basic** cache is scaled tooa different size, it is shut down and a new cache is provisioned using hello new size.</span></span> <span data-ttu-id="e318c-171">Durante esse tempo, cache Olá não está disponível e todos os dados no cache de saudação serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="e318c-171">During this time, hello cache is unavailable and all data in hello cache is lost.</span></span>
* <span data-ttu-id="e318c-172">Quando um **básica** cache for dimensionado tooa **padrão** cache, um cache de réplica é provisionado e Olá dados são copiados do cache de réplica de toohello Olá cache primário.</span><span class="sxs-lookup"><span data-stu-id="e318c-172">When a **Basic** cache is scaled tooa **Standard** cache, a replica cache is provisioned and hello data is copied from hello primary cache toohello replica cache.</span></span> <span data-ttu-id="e318c-173">cache Olá permanece disponível durante a saudação dimensionamento de processo.</span><span class="sxs-lookup"><span data-stu-id="e318c-173">hello cache remains available during hello scaling process.</span></span>
* <span data-ttu-id="e318c-174">Quando um **padrão** cache for dimensionado tooa um tamanho diferente ou tooa **Premium** cache, uma das réplicas de saudação é desligada e provisionado novamente toohello novo tamanho e hello dados transferidos por e, em seguida, Olá outros réplica executará um failover antes que ele seja provisionado novamente, o processo toohello semelhante que ocorre durante uma falha de um de nós de cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e318c-174">When a **Standard** cache is scaled tooa different size or tooa **Premium** cache, one of hello replicas is shut down and re-provisioned toohello new size and hello data transferred over, and then hello other replica performs a failover before it is re-provisioned, similar toohello process that occurs during a failure of one of hello cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="e318c-175">Perderei dados de meu cache durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="e318c-176">Quando um **básica** cache é dimensionado tooa novo tamanho, todos os dados é perdido e cache Olá fica indisponível durante a operação de dimensionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e318c-176">When a **Basic** cache is scaled tooa new size, all data is lost and hello cache is unavailable during hello scaling operation.</span></span>
* <span data-ttu-id="e318c-177">Quando um **básica** cache for dimensionado tooa **padrão** do cache, hello dados no cache de saudação normalmente sejam preservados.</span><span class="sxs-lookup"><span data-stu-id="e318c-177">When a **Basic** cache is scaled tooa **Standard** cache, hello data in hello cache is typically preserved.</span></span>
* <span data-ttu-id="e318c-178">Quando um **padrão** cache for dimensionado tooa maior tamanho ou camada, ou um **Premium** cache for dimensionado tooa maior tamanho, todos os dados normalmente é preservado.</span><span class="sxs-lookup"><span data-stu-id="e318c-178">When a **Standard** cache is scaled tooa larger size or tier, or a **Premium** cache is scaled tooa larger size, all data is typically preserved.</span></span> <span data-ttu-id="e318c-179">Ao dimensionar um **padrão** ou **Premium** cache inativo tooa menores, dados pode ser perdida dependendo de quantos dados estão no cache de saudação relacionadas toohello novo tamanho quando ela é dimensionada.</span><span class="sxs-lookup"><span data-stu-id="e318c-179">When scaling a **Standard** or **Premium** cache down tooa smaller size, data may be lost depending on how much data is in hello cache related toohello new size when it is scaled.</span></span> <span data-ttu-id="e318c-180">Se os dados são perdidos na redução, as chaves são removidas usando Olá [allkeys lru](http://redis.io/topics/lru-cache) política de remoção.</span><span class="sxs-lookup"><span data-stu-id="e318c-180">If data is lost when scaling down, keys are evicted using hello [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="e318c-181">A configuração dos meus bancos de dados personalizados foi afetada durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="e318c-182">Alguns tipos de preço têm diferentes [limites de bancos de dados](cache-configure.md#databases), portanto, há algumas considerações ao dimensionamento se configurado um valor personalizado para Olá `databases` configuração durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="e318c-183">Dimensionamento quando tooa preço com baixo `databases` limite da camada atual de saudação de:</span><span class="sxs-lookup"><span data-stu-id="e318c-183">When scaling tooa pricing tier with a lower `databases` limit than hello current tier:</span></span>
  * <span data-ttu-id="e318c-184">Se você estiver usando o número padrão de saudação do `databases` que é 16 para todas as camadas de preços, nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="e318c-184">If you are using hello default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="e318c-185">Se você estiver usando um número de `databases` que se enquadra dentro dos limites Olá para Olá camada toowhich dimensionará, isso `databases` configuração é mantida e nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="e318c-185">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="e318c-186">Se você estiver usando um número de `databases` que excede os limites de saudação do novo nível de hello, hello `databases` configuração é reduzido toohello limites de nova camada de saudação e todos os dados em bancos de dados Olá removido é perdida.</span><span class="sxs-lookup"><span data-stu-id="e318c-186">If you are using a custom number of `databases` that exceeds hello limits of hello new tier, hello `databases` setting is lowered toohello limits of hello new tier and all data in hello removed databases is lost.</span></span>
* <span data-ttu-id="e318c-187">Dimensionamento quando tooa preço com hello igual ou superior `databases` limite da camada atual de saudação de seu `databases` configuração é mantida e nenhum dado será perdido.</span><span class="sxs-lookup"><span data-stu-id="e318c-187">When scaling tooa pricing tier with hello same or higher `databases` limit than hello current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="e318c-188">Observe que, embora os caches Standard e Premium tenham um SLA de 99,9% de disponibilidade, não há SLA para perda de dados.</span><span class="sxs-lookup"><span data-stu-id="e318c-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="e318c-189">O cache estará disponível durante o dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="e318c-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="e318c-190">**Padrão** e **Premium** caches permanecem disponíveis durante a operação de dimensionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e318c-190">**Standard** and **Premium** caches remain available during hello scaling operation.</span></span>
* <span data-ttu-id="e318c-191">**Básico** caches estão offline durante a escala de tamanho diferente de tooa de operações, mas permanecem disponíveis quando o dimensionamento de **básica** muito**padrão**.</span><span class="sxs-lookup"><span data-stu-id="e318c-191">**Basic** caches are offline during scaling operations tooa different size, but remain available when scaling from **Basic** too**Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="e318c-192">Operações que não têm suporte</span><span class="sxs-lookup"><span data-stu-id="e318c-192">Operations that are not supported</span></span>
* <span data-ttu-id="e318c-193">Não é possível redimensionar de um maior preço camada tooa menor preço.</span><span class="sxs-lookup"><span data-stu-id="e318c-193">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
  * <span data-ttu-id="e318c-194">Você não pode ser dimensionada de um **Premium** cache para baixo tooa **padrão** ou um **básica** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-194">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="e318c-195">Você não pode ser dimensionada de um **padrão** cache para baixo tooa **básica** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-195">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
* <span data-ttu-id="e318c-196">Pode ser dimensionada de um **básica** cache tooa **padrão** cache, mas você não pode alterar o tamanho de saudação em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e318c-196">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="e318c-197">Se você precisar de um tamanho diferente, você pode fazer um tamanho de toohello desejado escala operação subsequente.</span><span class="sxs-lookup"><span data-stu-id="e318c-197">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
* <span data-ttu-id="e318c-198">Você não pode ser dimensionada de um **básica** diretamente do cache tooa **Premium** cache.</span><span class="sxs-lookup"><span data-stu-id="e318c-198">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="e318c-199">Você deve primeiro ser dimensionada de **básica** muito**padrão** em uma operação de escala e de **padrão** muito**Premium** em um subsequente a operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e318c-199">You must first scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="e318c-200">Não é possível redimensionar de um tamanho maior para baixo toohello **C0 (250 MB)** tamanho.</span><span class="sxs-lookup"><span data-stu-id="e318c-200">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>

<span data-ttu-id="e318c-201">Se uma operação de dimensionamento falhar, serviço Olá tentará operação de saudação do toorevert e cache Olá reverterá tamanho original toohello.</span><span class="sxs-lookup"><span data-stu-id="e318c-201">If a scaling operation fails, hello service will try toorevert hello operation and hello cache will revert toohello original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="e318c-202">Quanto tempo o dimensionamento leva?</span><span class="sxs-lookup"><span data-stu-id="e318c-202">How long does scaling take?</span></span>
<span data-ttu-id="e318c-203">Dimensionamento leva aproximadamente 20 minutos, dependendo de quantos dados estão no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="e318c-203">Scaling takes approximately 20 minutes, depending on how much data is in hello cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="e318c-204">Como saber quando o dimensionamento é concluído?</span><span class="sxs-lookup"><span data-stu-id="e318c-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="e318c-205">Olá portal do Azure, você verá Olá a operação de dimensionamento em andamento.</span><span class="sxs-lookup"><span data-stu-id="e318c-205">In hello Azure portal you can see hello scaling operation in progress.</span></span> <span data-ttu-id="e318c-206">Quando o dimensionamento for concluído, Olá status das alterações de cache Olá muito**executando**.</span><span class="sxs-lookup"><span data-stu-id="e318c-206">When scaling is complete, hello status of hello cache changes too**Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



