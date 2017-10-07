---
title: aaaHow tooconfigure Cache Redis do Azure | Microsoft Docs
description: "Entender a configuração de Redis saudação padrão para o Cache Redis do Azure e aprenda como tooconfigure do Azure Redis Cache instâncias"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="d1331-103">Como tooconfigure Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="d1331-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="d1331-104">Este tópico descreve como tooreview e atualização Olá configuração para suas instâncias de Cache Redis do Azure e configuração do servidor abrange saudação padrão Redis para instâncias de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="d1331-105">Para obter mais informações sobre como configurar e usar os recursos de cache premium, consulte [como persistência tooconfigure](cache-how-to-premium-persistence.md), [como tooconfigure clustering](cache-how-to-premium-clustering.md), e [como o suporte a tooconfigure rede Virtual ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="d1331-106">Definir configurações de cache Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="d1331-107">Configurações de Cache Redis do Azure são exibidas e configuradas em Olá **Cache Redis** folha usando Olá **Menu recursos**.</span><span class="sxs-lookup"><span data-stu-id="d1331-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Configurações de Cache Redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="d1331-109">Você pode exibir e configurar Olá seguindo as configurações usando Olá **Menu recursos**.</span><span class="sxs-lookup"><span data-stu-id="d1331-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="d1331-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d1331-110">Overview</span></span>](#overview)
* [<span data-ttu-id="d1331-111">Log de atividade</span><span class="sxs-lookup"><span data-stu-id="d1331-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="d1331-112">Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="d1331-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="d1331-113">Marcas</span><span class="sxs-lookup"><span data-stu-id="d1331-113">Tags</span></span>](#tags)
* [<span data-ttu-id="d1331-114">Diagnosticar e resolver problemas</span><span class="sxs-lookup"><span data-stu-id="d1331-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="d1331-115">Configurações</span><span class="sxs-lookup"><span data-stu-id="d1331-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="d1331-116">Chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="d1331-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="d1331-117">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="d1331-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="d1331-118">Supervisor do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="d1331-119">Escala</span><span class="sxs-lookup"><span data-stu-id="d1331-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="d1331-120">Tamanho do cluster Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="d1331-121">Persistência de dados do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="d1331-122">Agendar atualizações</span><span class="sxs-lookup"><span data-stu-id="d1331-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="d1331-123">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="d1331-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="d1331-124">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="d1331-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="d1331-125">Firewall</span><span class="sxs-lookup"><span data-stu-id="d1331-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="d1331-126">Propriedades</span><span class="sxs-lookup"><span data-stu-id="d1331-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="d1331-127">Bloqueios</span><span class="sxs-lookup"><span data-stu-id="d1331-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="d1331-128">Script de automação</span><span class="sxs-lookup"><span data-stu-id="d1331-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="d1331-129">Administração</span><span class="sxs-lookup"><span data-stu-id="d1331-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="d1331-130">Importar dados</span><span class="sxs-lookup"><span data-stu-id="d1331-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="d1331-131">Exportar Dados</span><span class="sxs-lookup"><span data-stu-id="d1331-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="d1331-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="d1331-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="d1331-133">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="d1331-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="d1331-134">Métricas do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="d1331-135">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="d1331-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="d1331-136">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d1331-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="d1331-137">Configurações de suporte e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="d1331-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="d1331-138">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="d1331-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="d1331-139">Nova solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="d1331-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="d1331-140">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d1331-140">Overview</span></span>

<span data-ttu-id="d1331-141">**A visão geral** fornece informações básicas sobre o cache como: nome, portas, tipo de preço e métricas de cache selecionadas.</span><span class="sxs-lookup"><span data-stu-id="d1331-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="d1331-142">Log de atividades</span><span class="sxs-lookup"><span data-stu-id="d1331-142">Activity log</span></span>

<span data-ttu-id="d1331-143">Clique em **log de atividades** tooview ações executadas em seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="d1331-144">Você também pode usar filtragem tooexpand tooinclude essa exibição outros recursos.</span><span class="sxs-lookup"><span data-stu-id="d1331-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="d1331-145">Para obter mais informações sobre como trabalhar com logs de auditoria, confira [Operações de auditoria com o Resource Manager](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="d1331-146">Para saber mais sobre como monitorar eventos do Cache Redis do Azure, confira [Operações e alertas](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="d1331-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="d1331-147">Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="d1331-147">Access control (IAM)</span></span>

<span data-ttu-id="d1331-148">Olá **(IAM) do controle de acesso** seção fornece suporte para controle de acesso baseado em função (RBAC) em Olá toohelp portal do Azure organizações atender seus requisitos de gerenciamento de acesso simples e precisa.</span><span class="sxs-lookup"><span data-stu-id="d1331-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="d1331-149">Para obter mais informações, consulte [controle de acesso baseado em função no portal do Azure de saudação](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="d1331-150">Marcas</span><span class="sxs-lookup"><span data-stu-id="d1331-150">Tags</span></span>

<span data-ttu-id="d1331-151">Olá **marcas** seção ajuda você a organizar os recursos.</span><span class="sxs-lookup"><span data-stu-id="d1331-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="d1331-152">Para obter mais informações, consulte [usando marcas tooorganize seus recursos do Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="d1331-153">Diagnosticar e resolver problemas</span><span class="sxs-lookup"><span data-stu-id="d1331-153">Diagnose and solve problems</span></span>

<span data-ttu-id="d1331-154">Clique em **diagnosticar e resolver problemas** toobe fornecido com problemas comuns e estratégias para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="d1331-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="d1331-155">Configurações</span><span class="sxs-lookup"><span data-stu-id="d1331-155">Settings</span></span>
<span data-ttu-id="d1331-156">Olá **configurações** seção permite que você tooaccess e configurar Olá seguindo as configurações para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="d1331-157">Chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="d1331-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="d1331-158">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="d1331-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="d1331-159">Supervisor do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="d1331-160">Escala</span><span class="sxs-lookup"><span data-stu-id="d1331-160">Scale</span></span>](#scale)
* [<span data-ttu-id="d1331-161">Tamanho do cluster Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="d1331-162">Persistência de dados do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="d1331-163">Agendar atualizações</span><span class="sxs-lookup"><span data-stu-id="d1331-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="d1331-164">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="d1331-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="d1331-165">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="d1331-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="d1331-166">Firewall</span><span class="sxs-lookup"><span data-stu-id="d1331-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="d1331-167">Propriedades</span><span class="sxs-lookup"><span data-stu-id="d1331-167">Properties</span></span>](#properties)
* [<span data-ttu-id="d1331-168">Bloqueios</span><span class="sxs-lookup"><span data-stu-id="d1331-168">Locks</span></span>](#locks)
* [<span data-ttu-id="d1331-169">Script de automação</span><span class="sxs-lookup"><span data-stu-id="d1331-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="d1331-170">Chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="d1331-170">Access keys</span></span>
<span data-ttu-id="d1331-171">Clique em **chaves de acesso** chaves de acesso de saudação tooview ou gere novamente para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="d1331-172">Essas chaves são usadas pelos clientes Olá tooyour cache de conexão.</span><span class="sxs-lookup"><span data-stu-id="d1331-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Chaves de acesso de Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="d1331-174">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="d1331-174">Advanced settings</span></span>
<span data-ttu-id="d1331-175">Olá configurações a seguir são configuradas no hello **configurações avançadas** folha.</span><span class="sxs-lookup"><span data-stu-id="d1331-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="d1331-176">Portas de acesso</span><span class="sxs-lookup"><span data-stu-id="d1331-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="d1331-177">Políticas de memória</span><span class="sxs-lookup"><span data-stu-id="d1331-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="d1331-178">Notificações de Keyspace (configurações avançadas)</span><span class="sxs-lookup"><span data-stu-id="d1331-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="d1331-179">Portas de acesso</span><span class="sxs-lookup"><span data-stu-id="d1331-179">Access Ports</span></span>
<span data-ttu-id="d1331-180">Por padrão, o acesso não SSL está desabilitado para novos caches.</span><span class="sxs-lookup"><span data-stu-id="d1331-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="d1331-181">tooenable Olá não SSL da porta, clique em **não** para **permitir acesso somente via SSL** em Olá **configurações avançadas** folha e depois clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="d1331-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Portas de acesso de Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="d1331-183">Políticas de memória</span><span class="sxs-lookup"><span data-stu-id="d1331-183">Memory policies</span></span>
<span data-ttu-id="d1331-184">Olá **política Maxmemory**, **reservado maxmemory**, e **reservado maxfragmentationmemory** configurações Olá **configuraçõesavançadas**folha configurar políticas de saudação de memória para cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Política Maxmemory de Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="d1331-186">**Política MaxMemory** configura a política de remoção de saudação de cache hello e permite que você toochoose de saudação políticas de remoção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1331-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="d1331-187">`volatile-lru`-Este é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="d1331-188">Para saber mais sobre políticas `maxmemory`, consulte [Políticas de remoção](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="d1331-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="d1331-189">Olá **reservado maxmemory** configuração define a quantidade de saudação de memória em MB é reservado para operações de cache não como replicação durante o failover.</span><span class="sxs-lookup"><span data-stu-id="d1331-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="d1331-190">Definir esse valor permite que você toohave uma experiência mais consistente do servidor Redis quando sua carga varia.</span><span class="sxs-lookup"><span data-stu-id="d1331-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="d1331-191">Esse valor deve ser definido como maior para cargas de trabalho que executam muitas operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="d1331-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="d1331-192">Quando a memória é reservada para essas operações, ela não fica disponível para o armazenamento de dados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="d1331-193">Olá **reservado maxfragmentationmemory** configuração define a quantidade de saudação de memória em MB é reservado tooaccommodate de fragmentação de memória.</span><span class="sxs-lookup"><span data-stu-id="d1331-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="d1331-194">Definir esse valor permite que você toohave uma experiência mais consistente do servidor Redis quando Olá cache estiver cheio ou fechar taxa de fragmentação toofull e hello também é alta.</span><span class="sxs-lookup"><span data-stu-id="d1331-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="d1331-195">Quando a memória é reservada para essas operações, ela não fica disponível para o armazenamento de dados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="d1331-196">Uma coisa tooconsider ao escolher um novo valor de reserva de memória (**reservado maxmemory** ou **reservado maxfragmentationmemory**) é como essa alteração pode afetar um cache que já está em execução com grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="d1331-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="d1331-197">Por exemplo, se você tem um cache 53 GB com 49 GB de dados e alterar Olá reserva valor too8 GB, isso removerá Olá max a memória disponível para o sistema Olá too45 GB.</span><span class="sxs-lookup"><span data-stu-id="d1331-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="d1331-198">Se seu atual `used_memory` ou `used_memory_rss` valores são maiores que o novo limite Olá de 45 GB, em seguida, sistema Olá terá tooevict dados até que as `used_memory` e `used_memory_rss` estão abaixo 45 GB.</span><span class="sxs-lookup"><span data-stu-id="d1331-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="d1331-199">A remoção pode aumentar a fragmentação de memória e carregamento do servidor.</span><span class="sxs-lookup"><span data-stu-id="d1331-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="d1331-200">Para obter mais informações sobre métricas do cache, como `used_memory` e `used_memory_rss`, consulte [Métricas disponíveis e intervalos de relatórios](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="d1331-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-201">Olá **reservado maxmemory** e **reservado maxfragmentationmemory** configurações só estão disponíveis para Standard e Premium armazena em cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="d1331-202">Notificações de Keyspace (configurações avançadas)</span><span class="sxs-lookup"><span data-stu-id="d1331-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="d1331-203">Redis keyspace as notificações são configuradas no hello **configurações avançadas** folha.</span><span class="sxs-lookup"><span data-stu-id="d1331-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="d1331-204">Notificações Keyspace permitem que os clientes tooreceive notificações quando ocorrem determinados eventos.</span><span class="sxs-lookup"><span data-stu-id="d1331-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Configurações avançadas de Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="d1331-206">Keyspace notificações e hello **eventos notificar de keyspace** configuração só estão disponíveis para os caches Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="d1331-207">Para obter mais informações, veja [Notificações de Keyspace do Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="d1331-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="d1331-208">Para exemplo de código, consulte Olá [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) arquivo hello [Olá, mundo](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) exemplo.</span><span class="sxs-lookup"><span data-stu-id="d1331-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="d1331-209">Supervisor do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-209">Redis Cache Advisor</span></span>
<span data-ttu-id="d1331-210">Olá **Redis Cache Advisor** folha exibe recomendações para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="d1331-211">Durante as operações normais, nenhuma recomendação é exibida.</span><span class="sxs-lookup"><span data-stu-id="d1331-211">During normal operations, no recommendations are displayed.</span></span> 

![Recomendações](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="d1331-213">Se qualquer condição ocorrer durante as operações de saudação do cache como alto uso da memória, largura de banda de rede ou de carga do servidor, um alerta é exibido na Olá **Redis Cache** folha.</span><span class="sxs-lookup"><span data-stu-id="d1331-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Recomendações](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="d1331-215">Informações adicionais podem ser encontradas em Olá **recomendações** folha.</span><span class="sxs-lookup"><span data-stu-id="d1331-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Recomendações](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="d1331-217">Você pode monitorar essas métricas em Olá [gráficos de monitoramento](cache-how-to-monitor.md#monitoring-charts) e [gráficos de uso](cache-how-to-monitor.md#usage-charts) seções de saudação **Redis Cache** folha.</span><span class="sxs-lookup"><span data-stu-id="d1331-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="d1331-218">Cada tipo de preço tem limites diferentes para conexões de cliente, memória e largura de banda.</span><span class="sxs-lookup"><span data-stu-id="d1331-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="d1331-219">Se o cache se aproximar da capacidade máxima para essas métricas durante um período prolongado, uma recomendação será criada.</span><span class="sxs-lookup"><span data-stu-id="d1331-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="d1331-220">Para obter mais informações sobre métricas hello e limites de revisores Olá **recomendações** ferramenta, consulte Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1331-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="d1331-221">Métrica do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-221">Redis Cache metric</span></span> | <span data-ttu-id="d1331-222">Mais informações</span><span class="sxs-lookup"><span data-stu-id="d1331-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="d1331-223">Uso de largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="d1331-223">Network bandwidth usage</span></span> |[<span data-ttu-id="d1331-224">Desempenho do cache - largura de banda disponível</span><span class="sxs-lookup"><span data-stu-id="d1331-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="d1331-225">Clientes conectados</span><span class="sxs-lookup"><span data-stu-id="d1331-225">Connected clients</span></span> |[<span data-ttu-id="d1331-226">Configuração padrão do servidor Redis - maxclients</span><span class="sxs-lookup"><span data-stu-id="d1331-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="d1331-227">Carga do servidor</span><span class="sxs-lookup"><span data-stu-id="d1331-227">Server load</span></span> |[<span data-ttu-id="d1331-228">Gráficos de uso - carga do servidor Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="d1331-229">Uso de memória</span><span class="sxs-lookup"><span data-stu-id="d1331-229">Memory usage</span></span> |[<span data-ttu-id="d1331-230">Desempenho do cache - tamanho</span><span class="sxs-lookup"><span data-stu-id="d1331-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="d1331-231">tooupgrade seu cache, clique em **atualizar agora** toochange Olá preço e [escala](#scale) seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="d1331-232">Para obter mais informações sobre como escolher um tipo de preço, confira [Qual oferta e tamanho de Cache Redis devo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="d1331-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="d1331-233">Escala</span><span class="sxs-lookup"><span data-stu-id="d1331-233">Scale</span></span>
<span data-ttu-id="d1331-234">Clique em **escala** Olá tooview ou alteração de preços para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="d1331-235">Para obter mais informações sobre dimensionamento, consulte [como tooScale Cache Redis do Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Tipo de preço do Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="d1331-237">Tamanho do cluster Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-237">Redis Cluster Size</span></span>
<span data-ttu-id="d1331-238">Clique em **tamanho de Cluster Redis (visualização)** o cache de tamanho do cluster Olá toochange para um premium em execução com cluster habilitado.</span><span class="sxs-lookup"><span data-stu-id="d1331-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="d1331-239">Observe que, enquanto hello Azure Redis Cache Premium camada foi liberado tooGeneral disponibilidade, o recurso de tamanho de Cluster Redis hello está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="d1331-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Tamanho do cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="d1331-241">tamanho do cluster Olá toochange, use o controle deslizante de saudação ou digite um número entre 1 e 10 Olá **contagem de fragmento** caixa de texto e clique em **Okey** toosave.</span><span class="sxs-lookup"><span data-stu-id="d1331-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-242">O clustering está disponível apenas para os Caches premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="d1331-243">Para obter mais informações, consulte [como tooconfigure clustering para um Premium do Azure Redis Cache](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="d1331-244">Persistência de dados do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-244">Redis data persistence</span></span>
<span data-ttu-id="d1331-245">Clique em **Redis a persistência de dados** tooenable, desabilitar ou configurar persistência de dados para seu cache premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="d1331-246">O Cache Redis do Microsoft Azure oferece persistência Redis usando [persistência RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) ou [persistência AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="d1331-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="d1331-247">Para obter mais informações, consulte [como tooconfigure persistência para um Premium do Azure Redis Cache](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="d1331-248">A persistência de dados do Redis só está disponível para os caches Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="d1331-249">Agende atualizações</span><span class="sxs-lookup"><span data-stu-id="d1331-249">Schedule updates</span></span>
<span data-ttu-id="d1331-250">Olá **agendar atualizações** folha permite que você toodesignate uma janela de manutenção para atualizações de servidor Redis para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d1331-251">janela de manutenção de saudação se aplica apenas atualizações de servidor tooRedis e não tooany Azure atualiza ou atualiza o sistema operacional de toohello de saudação VMs que hospedam o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Agende atualizações](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="d1331-253">toospecify uma janela de manutenção, verifique dias Olá desejado e especifique a hora de início de janela de manutenção de saudação para cada dia e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d1331-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="d1331-254">Observe que o tempo de janela de manutenção de saudação é em UTC.</span><span class="sxs-lookup"><span data-stu-id="d1331-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d1331-255">Olá **agendar atualizações** funcionalidade está disponível somente para os caches da camada Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="d1331-256">Para saber mais e instruções, confira [Como administrar o Cache Redis do Azure – Agendar atualizações](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="d1331-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="d1331-257">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="d1331-257">Geo-replication</span></span>

<span data-ttu-id="d1331-258">Olá **georeplicação** folha fornece um mecanismo para vincular as duas instâncias de Cache Redis do Azure da camada Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="d1331-259">Um cache é designado como o cache de vinculado primário hello e hello como cache de vinculado secundário hello.</span><span class="sxs-lookup"><span data-stu-id="d1331-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="d1331-260">cache de vinculado secundário Olá se torna somente leitura e dados cache primário toohello escrito é replicada toohello cache secundário de vinculado.</span><span class="sxs-lookup"><span data-stu-id="d1331-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="d1331-261">Essa funcionalidade pode ser usado tooreplicate um cache em regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-262">A **replicação geográfica** está disponível somente para caches de camada Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="d1331-263">Para obter mais informações e instruções, consulte [como tooconfigure replicação geográfica para Cache Redis do Azure](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="d1331-264">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="d1331-264">Virtual Network</span></span>
<span data-ttu-id="d1331-265">Olá **rede Virtual** seção permite que as configurações de rede virtual de saudação tooconfigure para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="d1331-266">Para obter informações sobre como criar um cache premium com uma rede virtual suporte e atualizar suas configurações, consulte [como tooconfigure dar suporte a rede Virtual para um Premium do Azure Redis Cache](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-267">As configurações de rede virtual só estão disponíveis para os caches premium configurados com suporte para rede virtual durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="d1331-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="d1331-268">Firewall</span></span>

<span data-ttu-id="d1331-269">Clique em **Firewall** tooview e configure as regras de firewall para o Cache Redis do Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="d1331-271">É possível especificar regras de firewall com um intervalo de endereços IP inicial e final.</span><span class="sxs-lookup"><span data-stu-id="d1331-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="d1331-272">Quando as regras de firewall estão configuradas, apenas as conexões de cliente de saudação especificado intervalos de endereços IP podem se conectar a toohello cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="d1331-273">Quando uma regra de firewall é salvo há um pequeno atraso antes de regra de saudação é eficaz.</span><span class="sxs-lookup"><span data-stu-id="d1331-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="d1331-274">Normalmente, esse atraso é inferior a um minuto.</span><span class="sxs-lookup"><span data-stu-id="d1331-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-275">Conexões dos sistemas de monitoramento do Cache Redis do Azure serão sempre permitidas, mesmo se regras de firewall forem configuradas.</span><span class="sxs-lookup"><span data-stu-id="d1331-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="d1331-276">As regras de firewall estão disponíveis apenas para os caches da camada Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="d1331-277">Propriedades</span><span class="sxs-lookup"><span data-stu-id="d1331-277">Properties</span></span>
<span data-ttu-id="d1331-278">Clique em **propriedades** tooview informações sobre seu cache, incluindo o ponto de extremidade de cache hello e portas.</span><span class="sxs-lookup"><span data-stu-id="d1331-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Propriedades de Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="d1331-280">Bloqueios</span><span class="sxs-lookup"><span data-stu-id="d1331-280">Locks</span></span>
<span data-ttu-id="d1331-281">Olá **bloqueia** seção permite que você toolock uma assinatura, o grupo de recursos ou o recurso tooprevent outros usuários na sua organização do acidentalmente excluir ou modificar recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="d1331-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="d1331-282">Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="d1331-283">Script de automação</span><span class="sxs-lookup"><span data-stu-id="d1331-283">Automation script</span></span>

<span data-ttu-id="d1331-284">Clique em **script de automação** toobuild e exportar um modelo de seus recursos implantados para implantações futuras.</span><span class="sxs-lookup"><span data-stu-id="d1331-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="d1331-285">Para saber mais sobre como trabalhar com modelos, confira [Implantar recursos com modelos do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="d1331-286">Configurações de administração</span><span class="sxs-lookup"><span data-stu-id="d1331-286">Administration settings</span></span>
<span data-ttu-id="d1331-287">Olá configurações Olá **administração** seção permitir Olá tooperform tarefas administrativas para o cache a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1331-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Administração](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="d1331-289">Importar dados</span><span class="sxs-lookup"><span data-stu-id="d1331-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="d1331-290">Exportar Dados</span><span class="sxs-lookup"><span data-stu-id="d1331-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="d1331-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="d1331-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="d1331-292">Importar/exportar</span><span class="sxs-lookup"><span data-stu-id="d1331-292">Import/Export</span></span>
<span data-ttu-id="d1331-293">Importação/exportação é uma operação de gerenciamento de dados do Cache Redis do Azure, que permite que você tooimport e exportar dados em cache Olá importando e exportando um instantâneo de banco de dados de Cache Redis (RDB) de um blob de páginas de tooa de cache premium em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="d1331-294">Importação/exportação permite toomigrate entre instâncias diferentes do Cache Redis do Azure ou popular Olá cache com os dados antes do uso.</span><span class="sxs-lookup"><span data-stu-id="d1331-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="d1331-295">Importação pode ser usado toobring Redis compatível RDB arquivos de qualquer servidor Redis em execução em qualquer nuvem ou o ambiente, incluindo o Redis em execução no Linux, Windows ou em qualquer provedor de nuvem como Amazon Web Services e outros.</span><span class="sxs-lookup"><span data-stu-id="d1331-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="d1331-296">Importação de dados é uma maneira fácil de toocreate um cache com dados preenchidos previamente.</span><span class="sxs-lookup"><span data-stu-id="d1331-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="d1331-297">Durante o processo de importação Olá, Cache Redis do Azure carrega arquivos RDB saudação do armazenamento do Azure na memória e insere chaves Olá cache hello.</span><span class="sxs-lookup"><span data-stu-id="d1331-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="d1331-298">Exportação permite que dados de saudação tooexport armazenados em Cache Redis do Azure tooRedis compatível RDB arquivos.</span><span class="sxs-lookup"><span data-stu-id="d1331-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="d1331-299">Você pode usar esses dados de toomove do recurso de um Cache Redis do Azure instância tooanother ou servidor do Redis tooanother.</span><span class="sxs-lookup"><span data-stu-id="d1331-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="d1331-300">Durante o processo de exportação hello, um arquivo temporário é criado no hello VM que hospeda Olá instância de servidor de Cache Redis do Azure e arquivo hello é carregado toohello designado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d1331-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="d1331-301">Quando a operação de exportação Olá for concluído com o status de êxito ou falha, o arquivo temporário de saudação é excluído.</span><span class="sxs-lookup"><span data-stu-id="d1331-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-302">A opção Importar/Exportar está disponível somente para caches do nível Premium.</span><span class="sxs-lookup"><span data-stu-id="d1331-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="d1331-303">Para saber mais e instruções, confira [Importar e exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="d1331-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="d1331-304">Reboot</span></span>
<span data-ttu-id="d1331-305">Olá **reinicializar** folha permite tooreboot nós de saudação do cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="d1331-306">Esse recurso de reinicialização permite que você tootest seu aplicativo para garantir a resiliência se houver uma falha de um nó de cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="d1331-308">Se você tiver um cache premium com cluster habilitado, você pode selecionar quais fragmentos de saudação tooreboot de cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="d1331-310">tooreboot um ou mais nós de seu cache, selecione nós de saudação desejado e clique em **reinicializar**.</span><span class="sxs-lookup"><span data-stu-id="d1331-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="d1331-311">Se você tiver um cache premium com cluster habilitado, selecione Olá shard(s) tooreboot e, em seguida, clique em **reinicializar**.</span><span class="sxs-lookup"><span data-stu-id="d1331-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="d1331-312">Depois de alguns minutos, Olá reinicialização do nó (s) selecionado e estiverem online novamente depois de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d1331-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1331-313">A reinicialização agora está disponível para todos os tipos de preço.</span><span class="sxs-lookup"><span data-stu-id="d1331-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="d1331-314">Para saber mais e instruções, confira [Como administrar o Cache Redis do Azure – Reinicializar](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="d1331-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="d1331-315">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="d1331-315">Monitoring</span></span>

<span data-ttu-id="d1331-316">Olá **monitoramento** seção permite que você tooconfigure diagnóstico e monitoramento para seu Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="d1331-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="d1331-317">Para obter mais informações sobre diagnóstico e monitoramento do Cache Redis do Azure, consulte [como toomonitor Cache Redis do Azure](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostics](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="d1331-319">Métricas do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="d1331-320">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="d1331-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="d1331-321">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d1331-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="d1331-322">Métricas do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-322">Redis metrics</span></span>
<span data-ttu-id="d1331-323">Clique em **Redis métricas** muito[exibir métricas](cache-how-to-monitor.md#view-cache-metrics) para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="d1331-324">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="d1331-324">Alert rules</span></span>

<span data-ttu-id="d1331-325">Clique em **regras de alerta** tooconfigure alertas com base nas métricas de Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="d1331-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="d1331-326">Para obter mais informações, consulte [Alertas](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="d1331-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="d1331-327">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="d1331-327">Diagnostics</span></span>

<span data-ttu-id="d1331-328">Por padrão, as métricas de cache no Azure Monitor são [armazenadas durante 30 dias](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e, em seguida, excluídas.</span><span class="sxs-lookup"><span data-stu-id="d1331-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="d1331-329">toopersist suas métricas de cache por mais de 30 dias, clique **diagnóstico** muito[configurar conta de armazenamento Olá](cache-how-to-monitor.md#export-cache-metrics) usado toostore diagnósticos de cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="d1331-330">Em adição tooarchiving seu toostorage de métricas de cache, você também pode [transmiti-los tooan hub de eventos ou enviá-los tooLog análise](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="d1331-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="d1331-331">Configurações de suporte e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="d1331-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="d1331-332">Olá configurações Olá **suporte + solução de problemas** seção fornecerá opções para resolver problemas com seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Suporte + solução de problemas](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="d1331-334">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="d1331-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="d1331-335">Nova solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="d1331-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="d1331-336">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="d1331-336">Resource health</span></span>
<span data-ttu-id="d1331-337">**Resource Health** observa seu recurso e informa se ele está sendo executado conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="d1331-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="d1331-338">Para obter mais informações sobre Olá serviço de integridade de recursos do Azure, consulte [visão geral da integridade do recurso Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d1331-339">Integridade do recurso é atualmente não é possível tooreport na integridade de saudação de instâncias de Cache Redis do Azure hospedado em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d1331-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="d1331-340">Para saber mais, confira [Todos os recursos de cache funcionam ao hospedar um cache em uma rede virtual?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="d1331-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="d1331-341">Nova solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="d1331-341">New support request</span></span>
<span data-ttu-id="d1331-342">Clique em **nova solicitação de suporte** tooopen uma solicitação de suporte para seu cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="d1331-343">Configuração padrão do servidor Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-343">Default Redis server configuration</span></span>
<span data-ttu-id="d1331-344">Novo Cache Redis do Azure são configuradas com hello valores de configuração de Redis a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1331-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="d1331-345">configurações de saudação nesta seção não podem ser alteradas usando Olá `StackExchange.Redis.IServer.ConfigSet` método.</span><span class="sxs-lookup"><span data-stu-id="d1331-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="d1331-346">Se esse método for chamado com um dos comandos de saudação nesta seção, é gerada uma exceção semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1331-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="d1331-347">Quaisquer valores que podem ser configuradas como **máxima de memória de política**, podem ser configuradas por meio de saudação portal do Azure ou ferramentas de gerenciamento de linha de comando como CLI do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1331-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="d1331-348">Configuração</span><span class="sxs-lookup"><span data-stu-id="d1331-348">Setting</span></span> | <span data-ttu-id="d1331-349">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d1331-349">Default value</span></span> | <span data-ttu-id="d1331-350">Descrição</span><span class="sxs-lookup"><span data-stu-id="d1331-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="d1331-351">16</span><span class="sxs-lookup"><span data-stu-id="d1331-351">16</span></span> |<span data-ttu-id="d1331-352">número de bancos de dados padrão de saudação é 16, mas você pode configurar uma saudação de com base no número diferente de preço. <sup>1</sup> o banco de dados do saudação padrão é o DB 0, você pode selecionar um diferente em uma base por conexão que usa `connection.GetDatabase(dbid)` onde `dbid` é um número entre `0` e `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="d1331-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="d1331-353">Depende de saudação preço<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d1331-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="d1331-354">Isso é que o número máximo de saudação de clientes conectados é permitida Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="d1331-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="d1331-355">Quando Olá limite é atingido o Redis fecha todas as conexões novas hello, retornando um erro de 'número máximo de clientes atingido'.</span><span class="sxs-lookup"><span data-stu-id="d1331-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="d1331-356">Política MaxMemory é a configuração de saudação para como o Redis seleciona qual tooremove quando `maxmemory` (Olá o tamanho do cache Olá oferta selecionado quando você criou o cache de saudação) é atingido.</span><span class="sxs-lookup"><span data-stu-id="d1331-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="d1331-357">Padrão de saudação do Cache Redis do Azure com a configuração é `volatile-lru`, que remove as chaves de saudação com um vencimento definido usando um algoritmo LRU.</span><span class="sxs-lookup"><span data-stu-id="d1331-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="d1331-358">Essa configuração pode ser definida em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="d1331-359">Para obter mais informações, consulte [Políticas de memória](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="d1331-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="d1331-360">3</span><span class="sxs-lookup"><span data-stu-id="d1331-360">3</span></span> |<span data-ttu-id="d1331-361">memória toosave, LRU e algoritmos TTL mínimo são aproximados algoritmos em vez de algoritmos precisos.</span><span class="sxs-lookup"><span data-stu-id="d1331-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="d1331-362">Por padrão o Redis verificações três chaves e escolhe Olá um usada menos recentemente.</span><span class="sxs-lookup"><span data-stu-id="d1331-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="d1331-363">5.000</span><span class="sxs-lookup"><span data-stu-id="d1331-363">5,000</span></span> |<span data-ttu-id="d1331-364">Tempo máximo de execução de um script Lua em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="d1331-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="d1331-365">Se Olá tempo de execução máximo for atingido, o Redis registra que um script ainda está em execução após Olá máximo permitida de tempo e tooreply tooqueries é iniciado com um erro.</span><span class="sxs-lookup"><span data-stu-id="d1331-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="d1331-366">500</span><span class="sxs-lookup"><span data-stu-id="d1331-366">500</span></span> |<span data-ttu-id="d1331-367">O tamanho máximo da fila de eventos de script.</span><span class="sxs-lookup"><span data-stu-id="d1331-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="d1331-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="d1331-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="d1331-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="d1331-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="d1331-370">Olá limites de buffer de saída do cliente podem ser usado tooforce desconexão de clientes que não estão lendo dados do servidor de saudação rápido o suficiente, por algum motivo (um motivo comum é que um cliente Pub/Sub não consegue consumir mensagens assim que o publicador Olá pode produzi-las).</span><span class="sxs-lookup"><span data-stu-id="d1331-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="d1331-371">Para obter mais informações, veja [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="d1331-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="d1331-372"><a name="databases"></a>
<sup>1</sup>limite Olá para `databases` é diferente para cada Cache Redis do Azure, preço e pode ser definido na criação do cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="d1331-373">Se nenhum `databases` configuração é especificada durante a criação do cache, Olá padrão é 16.</span><span class="sxs-lookup"><span data-stu-id="d1331-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="d1331-374">Caches Básico e Standard</span><span class="sxs-lookup"><span data-stu-id="d1331-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="d1331-375">C0 cache (250 MB) – backup de bancos de dados too16</span><span class="sxs-lookup"><span data-stu-id="d1331-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d1331-376">C1 cache (1 GB) - backup too16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d1331-377">C2 cache (2,5 GB) - backup too16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d1331-378">C3 cache (6 GB) - backup too16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d1331-379">C4 cache (13 GB) - backup too32 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="d1331-380">C5 cache (26 GB) - backup too48 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="d1331-381">C6 cache (53 GB) - backup too64 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="d1331-382">Caches Premium</span><span class="sxs-lookup"><span data-stu-id="d1331-382">Premium caches</span></span>
  * <span data-ttu-id="d1331-383">P1 (6 GB - 60 GB) - backup too16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="d1331-384">P2 (13 GB - 130 GB) - backup too32 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="d1331-385">P3 (26 GB - 260 GB) - backup too48 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="d1331-386">P4 (53 GB - 530 GB) - backup too64 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="d1331-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="d1331-387">Todos os caches premium com cluster Redis habilitado - Redis cluster só dá suporte ao uso do banco de dados 0 então Olá `databases` limite para qualquer cache premium com cluster Redis habilitada efetivamente é 1 e hello [selecione](http://redis.io/commands/select) comando não é permitido.</span><span class="sxs-lookup"><span data-stu-id="d1331-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="d1331-388">Para obter mais informações, consulte [preciso toomake qualquer toouse de aplicativo alterações toomy cliente clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="d1331-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="d1331-389">Para saber mais sobre bancos de dados, veja [O que são bancos de dados Redis?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="d1331-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="d1331-390">Olá `databases` configuração pode ser configurado somente durante a criação do cache e somente usando o PowerShell, CLI ou outros clientes de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="d1331-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="d1331-391">Para obter um exemplo de configuração `databases` durante a criação de cache usando o PowerShell, confira [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="d1331-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="d1331-392"><a name="maxclients"></a> 
<sup>2</sup>`maxclients` é diferente para cada tipo de preço do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="d1331-393">Caches Básico e Standard</span><span class="sxs-lookup"><span data-stu-id="d1331-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="d1331-394">C0 cache (250 MB) - too256 conexões</span><span class="sxs-lookup"><span data-stu-id="d1331-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="d1331-395">C1 cache (1 GB) - backup too1, conexões, 000</span><span class="sxs-lookup"><span data-stu-id="d1331-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="d1331-396">C2 cache (2,5 GB) - backup too2, conexões, 000</span><span class="sxs-lookup"><span data-stu-id="d1331-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="d1331-397">C3 cache (6 GB) - backup too5, conexões, 000</span><span class="sxs-lookup"><span data-stu-id="d1331-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="d1331-398">C4 cache (13 GB) - backup too10, conexões, 000</span><span class="sxs-lookup"><span data-stu-id="d1331-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="d1331-399">C5 cache (26 GB) - backup too15, conexões, 000</span><span class="sxs-lookup"><span data-stu-id="d1331-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="d1331-400">C6 cache (53 GB) - backup too20, conexões, 000</span><span class="sxs-lookup"><span data-stu-id="d1331-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="d1331-401">Caches Premium</span><span class="sxs-lookup"><span data-stu-id="d1331-401">Premium caches</span></span>
  * <span data-ttu-id="d1331-402">P1 (6 GB - 60 GB) - backup too7, conexões de 500</span><span class="sxs-lookup"><span data-stu-id="d1331-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="d1331-403">P2 (13 GB - 130 GB) - backup too15, 000 conexões</span><span class="sxs-lookup"><span data-stu-id="d1331-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="d1331-404">P3 (26 GB - 260 GB) - backup too30, 000 conexões</span><span class="sxs-lookup"><span data-stu-id="d1331-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="d1331-405">P4 (53 GB - 530 GB) - backup too40, 000 conexões</span><span class="sxs-lookup"><span data-stu-id="d1331-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="d1331-406">Embora cada tamanho de cache permite que *até* um determinado número de conexões, tooRedis cada conexão tem sobrecarga associados a ele.</span><span class="sxs-lookup"><span data-stu-id="d1331-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="d1331-407">Um exemplo de tal sobrecarga seria o uso da CPU e de memória como resultado de criptografia TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="d1331-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="d1331-408">limite de conexão máximo Olá para um tamanho de cache determinado pressupõe um cache pouco carregado.</span><span class="sxs-lookup"><span data-stu-id="d1331-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="d1331-409">Se carregar de sobrecarga de conexão *mais* carga a partir de operações do cliente excede a capacidade de sistema hello, cache Olá pode enfrentar problemas de capacidade, mesmo se você não tiver excedido o limite de conexão de saudação para o tamanho do cache atual hello.</span><span class="sxs-lookup"><span data-stu-id="d1331-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="d1331-410">Comandos Redis não têm suporte no Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="d1331-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d1331-411">Porque a configuração e gerenciamento de instâncias de Cache Redis do Azure é gerenciada pela Microsoft, hello comandos a seguir são desabilitados.</span><span class="sxs-lookup"><span data-stu-id="d1331-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="d1331-412">Se você tentar tooinvoke-las, você recebe uma mensagem de erro semelhante muito`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="d1331-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="d1331-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="d1331-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="d1331-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="d1331-414">BGSAVE</span></span>
> * <span data-ttu-id="d1331-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="d1331-415">CONFIG</span></span>
> * <span data-ttu-id="d1331-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="d1331-416">DEBUG</span></span>
> * <span data-ttu-id="d1331-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="d1331-417">MIGRATE</span></span>
> * <span data-ttu-id="d1331-418">Salvar</span><span class="sxs-lookup"><span data-stu-id="d1331-418">SAVE</span></span>
> * <span data-ttu-id="d1331-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="d1331-419">SHUTDOWN</span></span>
> * <span data-ttu-id="d1331-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="d1331-420">SLAVEOF</span></span>
> * <span data-ttu-id="d1331-421">CLUSTER - Os comandos de gravação do cluster estão desabilitados, mas comandos do Cluster somente leitura são permitidos.</span><span class="sxs-lookup"><span data-stu-id="d1331-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="d1331-422">Para saber mais sobre os comandos do Redis, confira [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="d1331-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="d1331-423">Console do Redis</span><span class="sxs-lookup"><span data-stu-id="d1331-423">Redis console</span></span>
<span data-ttu-id="d1331-424">Podem emitir comandos de forma segura tooyour instâncias de Cache Redis do Azure usando Olá **Console Redis**, que está disponível no portal do Azure para todas as camadas de cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="d1331-425">Olá Console Redis não funciona com [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="d1331-426">Quando o cache faz parte de uma rede virtual, somente a clientes em redes de saudação pode acessar o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="d1331-427">Como Redis Console é executado no navegador local, que está fora da saudação VNET, ele não pode se conectar tooyour cache.</span><span class="sxs-lookup"><span data-stu-id="d1331-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="d1331-428">Nem todos os comandos do Redis têm suporte no Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1331-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="d1331-429">Para obter uma lista de comandos do Redis que estão desabilitados para o Cache Redis do Azure, consulte Olá anterior [Redis comandos não tem suportados no Cache Redis do Azure](#redis-commands-not-supported-in-azure-redis-cache) seção.</span><span class="sxs-lookup"><span data-stu-id="d1331-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="d1331-430">Para saber mais sobre os comandos do Redis, confira [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="d1331-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="d1331-431">Olá tooaccess Console Redis, clique em **Console** de saudação **Redis Cache** folha.</span><span class="sxs-lookup"><span data-stu-id="d1331-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Console do Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="d1331-433">comandos de tooissue em sua instância de cache, simplesmente saudação do tipo desejado comando no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Console do Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="d1331-435">Usando Olá Console Redis com um premium cache clusterizados</span><span class="sxs-lookup"><span data-stu-id="d1331-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="d1331-436">Quando o cache usando Olá Console Redis com um premium em cluster, você pode emitir comandos tooa único fragmento de cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="d1331-437">tooissue um fragmento específico do tooa de comando, primeiro conecte-se fragmento desejado toohello clicando no selecionador de fragmento de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1331-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Console do Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="d1331-439">Se você tenta tooaccess uma chave armazenada em um fragmento diferente de Olá fragmento conectado, você receberá um toohello semelhantes da mensagem de erro seguinte mensagem.</span><span class="sxs-lookup"><span data-stu-id="d1331-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="d1331-440">No exemplo anterior de saudação, o fragmento 1 é fragmento selecionado do hello, mas `myKey` está localizado no fragmento 0, conforme indicado pelo Olá `(shard 0)` parte da mensagem de saudação do erro.</span><span class="sxs-lookup"><span data-stu-id="d1331-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="d1331-441">Neste exemplo, tooaccess `myKey`, selecione fragmento 0 usando Olá seletor de fragmento e comando de saudação desejado do problema.</span><span class="sxs-lookup"><span data-stu-id="d1331-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="d1331-442">Mover o cache tooa nova assinatura</span><span class="sxs-lookup"><span data-stu-id="d1331-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="d1331-443">Você pode mover o cache tooa nova assinatura clicando **mover**.</span><span class="sxs-lookup"><span data-stu-id="d1331-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Mover o Cache Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="d1331-445">Para obter informações sobre como mover os recursos de um recurso grupo tooanother e de tooanother de uma assinatura, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d1331-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1331-446">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1331-446">Next steps</span></span>
* <span data-ttu-id="d1331-447">Para obter mais informações sobre como trabalhar com os comandos do Redis, consulte [Como posso executar comandos do Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="d1331-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

