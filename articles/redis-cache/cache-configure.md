---
title: Como configurar o Cache Redis do Azure | Microsoft Docs
description: "Entenda a configuração padrão Redis Cache Redis do Azure e aprenda a configurar as instâncias de Cache Redis do Azure"
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
ms.openlocfilehash: 0274e58eb2e83202d4dbc58da0c67d0fdde22ede
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="b888b-103">Como configurar o Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="b888b-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="b888b-104">Este tópico descreve como examinar e atualizar a configuração para suas instâncias de Cache Redis do Azure, além de incluir a configuração do servidor Redis padrão para instâncias de Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b888b-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="b888b-105">Para obter mais informações sobre como configurar e usar os recursos de cache premium, consulte [Como configurar a persistência](cache-how-to-premium-persistence.md), [Como configurar o clustering](cache-how-to-premium-clustering.md) e [Como configurar o suporte à Rede Virtual](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="b888b-106">Definir configurações de cache Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="b888b-107">As configurações de Cache Redis do Azure são exibidas e configuradas na folha **Cache Redis** usando o **Menu Recursos**.</span><span class="sxs-lookup"><span data-stu-id="b888b-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Configurações de Cache Redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="b888b-109">Você pode exibir e definir as seguintes configurações usando o **Menu recursos**.</span><span class="sxs-lookup"><span data-stu-id="b888b-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="b888b-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b888b-110">Overview</span></span>](#overview)
* [<span data-ttu-id="b888b-111">Log de atividade</span><span class="sxs-lookup"><span data-stu-id="b888b-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="b888b-112">Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="b888b-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="b888b-113">Marcas</span><span class="sxs-lookup"><span data-stu-id="b888b-113">Tags</span></span>](#tags)
* [<span data-ttu-id="b888b-114">Diagnosticar e resolver problemas</span><span class="sxs-lookup"><span data-stu-id="b888b-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="b888b-115">Configurações</span><span class="sxs-lookup"><span data-stu-id="b888b-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="b888b-116">Chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="b888b-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="b888b-117">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="b888b-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="b888b-118">Supervisor do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="b888b-119">Escala</span><span class="sxs-lookup"><span data-stu-id="b888b-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="b888b-120">Tamanho do cluster Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="b888b-121">Persistência de dados do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="b888b-122">Agendar atualizações</span><span class="sxs-lookup"><span data-stu-id="b888b-122">Schedule updates</span></span>](#schedule-updates)
    * [<span data-ttu-id="b888b-123">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="b888b-123">Geo-replication</span></span>](#geo-replication)
    * [<span data-ttu-id="b888b-124">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="b888b-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="b888b-125">Firewall</span><span class="sxs-lookup"><span data-stu-id="b888b-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="b888b-126">Propriedades</span><span class="sxs-lookup"><span data-stu-id="b888b-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="b888b-127">Bloqueios</span><span class="sxs-lookup"><span data-stu-id="b888b-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="b888b-128">Script de automação</span><span class="sxs-lookup"><span data-stu-id="b888b-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="b888b-129">Administração</span><span class="sxs-lookup"><span data-stu-id="b888b-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="b888b-130">Importar dados</span><span class="sxs-lookup"><span data-stu-id="b888b-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="b888b-131">Exportar Dados</span><span class="sxs-lookup"><span data-stu-id="b888b-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="b888b-132">Reboot</span><span class="sxs-lookup"><span data-stu-id="b888b-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="b888b-133">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="b888b-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="b888b-134">Métricas do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="b888b-135">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="b888b-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="b888b-136">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b888b-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="b888b-137">Configurações de suporte e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="b888b-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="b888b-138">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="b888b-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="b888b-139">Nova solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="b888b-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="b888b-140">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b888b-140">Overview</span></span>

<span data-ttu-id="b888b-141">**A visão geral** fornece informações básicas sobre o cache como: nome, portas, tipo de preço e métricas de cache selecionadas.</span><span class="sxs-lookup"><span data-stu-id="b888b-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="b888b-142">Log de atividades</span><span class="sxs-lookup"><span data-stu-id="b888b-142">Activity log</span></span>

<span data-ttu-id="b888b-143">Clique em **Log de auditoria** para exibir as ações executadas em seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-143">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="b888b-144">Você também pode usar a filtragem para expandir essa exibição a fim de incluir outros recursos.</span><span class="sxs-lookup"><span data-stu-id="b888b-144">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="b888b-145">Para obter mais informações sobre como trabalhar com logs de auditoria, confira [Operações de auditoria com o Resource Manager](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="b888b-146">Para saber mais sobre como monitorar eventos do Cache Redis do Azure, confira [Operações e alertas](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="b888b-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="b888b-147">Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="b888b-147">Access control (IAM)</span></span>

<span data-ttu-id="b888b-148">A seção **Controle de acesso (IAM)** dá suporte ao RBAC (controle de acesso baseado em função) no Portal do Azure para ajudar as organizações a atender aos seus requisitos de gerenciamento de acesso de maneira simples e precisa.</span><span class="sxs-lookup"><span data-stu-id="b888b-148">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="b888b-149">Para saber mais, confira [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md)(Controle de acesso baseado em função no portal do Azure).</span><span class="sxs-lookup"><span data-stu-id="b888b-149">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="b888b-150">Marcas</span><span class="sxs-lookup"><span data-stu-id="b888b-150">Tags</span></span>

<span data-ttu-id="b888b-151">A seção **Marcas** o ajuda a organizar seus recursos.</span><span class="sxs-lookup"><span data-stu-id="b888b-151">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="b888b-152">Para obter mais informações, veja [Usando marcas para organizar os recursos do Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-152">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="b888b-153">Diagnosticar e resolver problemas</span><span class="sxs-lookup"><span data-stu-id="b888b-153">Diagnose and solve problems</span></span>

<span data-ttu-id="b888b-154">Clique em **Diagnosticar e solucionar problemas** para ver problemas comuns e estratégias para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="b888b-154">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="b888b-155">Configurações</span><span class="sxs-lookup"><span data-stu-id="b888b-155">Settings</span></span>
<span data-ttu-id="b888b-156">A seção **Configurações** permite acessar e definir as seguintes configurações para seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-156">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

* [<span data-ttu-id="b888b-157">Chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="b888b-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="b888b-158">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="b888b-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="b888b-159">Supervisor do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="b888b-160">Escala</span><span class="sxs-lookup"><span data-stu-id="b888b-160">Scale</span></span>](#scale)
* [<span data-ttu-id="b888b-161">Tamanho do cluster Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="b888b-162">Persistência de dados do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="b888b-163">Agendar atualizações</span><span class="sxs-lookup"><span data-stu-id="b888b-163">Schedule updates</span></span>](#schedule-updates)
* [<span data-ttu-id="b888b-164">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="b888b-164">Geo-replication</span></span>](#geo-replication)
* [<span data-ttu-id="b888b-165">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="b888b-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="b888b-166">Firewall</span><span class="sxs-lookup"><span data-stu-id="b888b-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="b888b-167">Propriedades</span><span class="sxs-lookup"><span data-stu-id="b888b-167">Properties</span></span>](#properties)
* [<span data-ttu-id="b888b-168">Bloqueios</span><span class="sxs-lookup"><span data-stu-id="b888b-168">Locks</span></span>](#locks)
* [<span data-ttu-id="b888b-169">Script de automação</span><span class="sxs-lookup"><span data-stu-id="b888b-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="b888b-170">Chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="b888b-170">Access keys</span></span>
<span data-ttu-id="b888b-171">Clique em **Teclas de acesso** para exibir ou regenerar as teclas de acesso para seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-171">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="b888b-172">Essas chaves são usadas pelos clientes que se conectam ao seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-172">These keys are used by the clients connecting to your cache.</span></span>

![Chaves de acesso de Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="b888b-174">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="b888b-174">Advanced settings</span></span>
<span data-ttu-id="b888b-175">As configurações a seguir são definidas na folha **Configurações avançadas**.</span><span class="sxs-lookup"><span data-stu-id="b888b-175">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="b888b-176">Portas de acesso</span><span class="sxs-lookup"><span data-stu-id="b888b-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="b888b-177">Políticas de memória</span><span class="sxs-lookup"><span data-stu-id="b888b-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="b888b-178">Notificações de Keyspace (configurações avançadas)</span><span class="sxs-lookup"><span data-stu-id="b888b-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="b888b-179">Portas de acesso</span><span class="sxs-lookup"><span data-stu-id="b888b-179">Access Ports</span></span>
<span data-ttu-id="b888b-180">Por padrão, o acesso não SSL está desabilitado para novos caches.</span><span class="sxs-lookup"><span data-stu-id="b888b-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="b888b-181">Para habilitar a porta não SSL, clique em **Não** para **Permitir acesso somente via SSL** na folha **Configurações avançadas** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b888b-181">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Portas de acesso de Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="b888b-183">Políticas de memória</span><span class="sxs-lookup"><span data-stu-id="b888b-183">Memory policies</span></span>
<span data-ttu-id="b888b-184">As configurações **Política de Maxmemory**, **maxmemory-reserved** e **maxfragmentationmemory-reserved** na folha **Configurações avançadas** definem as políticas de memória do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-184">The **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span>

![Política Maxmemory de Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="b888b-186">A **política Maxmemory** configura a política de remoção do cache e permite escolher uma das seguintes políticas de remoção:</span><span class="sxs-lookup"><span data-stu-id="b888b-186">**Maxmemory policy** configures the eviction policy for the cache and allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="b888b-187">`volatile-lru` – esse é o padrão.</span><span class="sxs-lookup"><span data-stu-id="b888b-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="b888b-188">Para saber mais sobre políticas `maxmemory`, consulte [Políticas de remoção](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="b888b-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="b888b-189">A configuração **maxmemory-reserved** configura a quantidade de memória em MB reservada para operações de não cache, como replicação, durante o failover.</span><span class="sxs-lookup"><span data-stu-id="b888b-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="b888b-190">Definir esse valor permite que você tenha uma experiência mais consistente do servidor Redis quando sua carga varia.</span><span class="sxs-lookup"><span data-stu-id="b888b-190">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="b888b-191">Esse valor deve ser definido como maior para cargas de trabalho que executam muitas operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="b888b-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="b888b-192">Quando a memória é reservada para essas operações, ela não fica disponível para o armazenamento de dados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="b888b-193">A configuração **maxfragmentationmemory-reserved** define a quantidade de memória em MB reservada para acomodar a fragmentação de memória.</span><span class="sxs-lookup"><span data-stu-id="b888b-193">The **maxfragmentationmemory-reserved** setting configures the amount of memory in MB that is reserved to accommodate for memory fragmentation.</span></span> <span data-ttu-id="b888b-194">A configuração desse valor permite ter uma experiência do servidor Redis mais consistente quando o cache está cheio ou quase cheio e a taxa de fragmentação também é alta.</span><span class="sxs-lookup"><span data-stu-id="b888b-194">Setting this value allows you to have a more consistent Redis server experience when the cache is full or close to full and the fragmentation ratio is also high.</span></span> <span data-ttu-id="b888b-195">Quando a memória é reservada para essas operações, ela não fica disponível para o armazenamento de dados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="b888b-196">Uma coisa a ser considerada ao escolher um novo valor de reserva de memória (**maxmemory-reserved** ou **maxfragmentationmemory-reserved**) é como essa alteração pode afetar um cache que já está em execução com grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="b888b-196">One thing to consider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="b888b-197">Por exemplo, se você tiver um cache de 53 GB com 49 GB de dados, altere o valor de reserva para 8 GB; isso reduzirá a memória máxima disponível para o sistema para 45 GB.</span><span class="sxs-lookup"><span data-stu-id="b888b-197">For instance, if you have a 53 GB cache with 49 GB of data, then change the reservation value to 8 GB, this will drop the max available memory for the system down to 45 GB.</span></span> <span data-ttu-id="b888b-198">Se os valores `used_memory` ou `used_memory_rss` atuais forem maiores que o novo limite de 45 GB, o sistema precisará remover os dados até que `used_memory` e `used_memory_rss` fiquem abaixo de 45 GB.</span><span class="sxs-lookup"><span data-stu-id="b888b-198">If either your current `used_memory` or your `used_memory_rss` values are higher than the new limit of 45 GB, then the system will have to evict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="b888b-199">A remoção pode aumentar a fragmentação de memória e carregamento do servidor.</span><span class="sxs-lookup"><span data-stu-id="b888b-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="b888b-200">Para obter mais informações sobre métricas do cache, como `used_memory` e `used_memory_rss`, consulte [Métricas disponíveis e intervalos de relatórios](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="b888b-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-201">As configurações **maxmemory-reserved** e **maxfragmentationmemory-reserved** estão disponíveis somente para caches Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-201">The **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="b888b-202">Notificações de Keyspace (configurações avançadas)</span><span class="sxs-lookup"><span data-stu-id="b888b-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="b888b-203">As notificações keyspace do Redis são configuradas na folha **Configurações avançadas** .</span><span class="sxs-lookup"><span data-stu-id="b888b-203">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="b888b-204">As notificações keyspace permitem que clientes recebam notificações quando determinados eventos ocorrerem.</span><span class="sxs-lookup"><span data-stu-id="b888b-204">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Configurações avançadas de Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="b888b-206">As notificações de Keyspace e a configuração **notify-keyspace-events** estão disponíveis apenas para os caches Standard e Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-206">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="b888b-207">Para obter mais informações, veja [Notificações de Keyspace do Redis](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="b888b-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="b888b-208">Para o código de exemplo, veja o arquivo [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) no exemplo [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld).</span><span class="sxs-lookup"><span data-stu-id="b888b-208">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="b888b-209">Supervisor do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-209">Redis Cache Advisor</span></span>
<span data-ttu-id="b888b-210">A folha do **Supervisor do Cache Redis** exibe recomendações para seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-210">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="b888b-211">Durante as operações normais, nenhuma recomendação é exibida.</span><span class="sxs-lookup"><span data-stu-id="b888b-211">During normal operations, no recommendations are displayed.</span></span> 

![Recomendações](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="b888b-213">Se qualquer condição ocorrer durante as operações de seu cache, por exemplo, alto uso de memória, de largura de banda de rede ou de carga do servidor, um alerta será exibido na folha **Cache Redis** .</span><span class="sxs-lookup"><span data-stu-id="b888b-213">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![Recomendações](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="b888b-215">É possível encontrar mais informações na folha **Recomendações** .</span><span class="sxs-lookup"><span data-stu-id="b888b-215">Further information can be found on the **Recommendations** blade.</span></span>

![Recomendações](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="b888b-217">Você pode monitorar essas métricas nas seções [Gráficos de monitoramento](cache-how-to-monitor.md#monitoring-charts) e [Gráficos de uso](cache-how-to-monitor.md#usage-charts) da folha **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="b888b-217">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="b888b-218">Cada tipo de preço tem limites diferentes para conexões de cliente, memória e largura de banda.</span><span class="sxs-lookup"><span data-stu-id="b888b-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="b888b-219">Se o cache se aproximar da capacidade máxima para essas métricas durante um período prolongado, uma recomendação será criada.</span><span class="sxs-lookup"><span data-stu-id="b888b-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="b888b-220">Para saber mais sobre as métricas e os limites revisados pela ferramenta **Recomendações**, confira a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="b888b-220">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="b888b-221">Métrica do Cache Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-221">Redis Cache metric</span></span> | <span data-ttu-id="b888b-222">Mais informações</span><span class="sxs-lookup"><span data-stu-id="b888b-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="b888b-223">Uso de largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="b888b-223">Network bandwidth usage</span></span> |[<span data-ttu-id="b888b-224">Desempenho do cache - largura de banda disponível</span><span class="sxs-lookup"><span data-stu-id="b888b-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="b888b-225">Clientes conectados</span><span class="sxs-lookup"><span data-stu-id="b888b-225">Connected clients</span></span> |[<span data-ttu-id="b888b-226">Configuração padrão do servidor Redis - maxclients</span><span class="sxs-lookup"><span data-stu-id="b888b-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="b888b-227">Carga do servidor</span><span class="sxs-lookup"><span data-stu-id="b888b-227">Server load</span></span> |[<span data-ttu-id="b888b-228">Gráficos de uso - carga do servidor Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="b888b-229">Uso de memória</span><span class="sxs-lookup"><span data-stu-id="b888b-229">Memory usage</span></span> |[<span data-ttu-id="b888b-230">Desempenho do cache - tamanho</span><span class="sxs-lookup"><span data-stu-id="b888b-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="b888b-231">Para atualizar o cache, clique em **Atualizar agora** a fim de alterar o tipo de preço e [escalar](#scale) seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-231">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="b888b-232">Para obter mais informações sobre como escolher um tipo de preço, confira [Qual oferta e tamanho de Cache Redis devo usar?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="b888b-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="b888b-233">Escala</span><span class="sxs-lookup"><span data-stu-id="b888b-233">Scale</span></span>
<span data-ttu-id="b888b-234">Clique em **Escala** para exibir ou alterar o tipo de preço do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-234">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="b888b-235">Para obter mais informações sobre escala, veja [Como escalonar o Cache Redis do Azure](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-235">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Tipo de preço do Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="b888b-237">Tamanho do cluster Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-237">Redis Cluster Size</span></span>
<span data-ttu-id="b888b-238">Clique em **Tamanho do Cluster Redis (VISUALIZAÇÃO)** para alterar o tamanho do cluster de um cache premium em execução com clustering habilitado.</span><span class="sxs-lookup"><span data-stu-id="b888b-238">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="b888b-239">Observe que, enquanto a camada Cache Redis do Azure Premium foi liberada para disponibilidade geral, o recurso de Tamanho do Cluster Redis está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="b888b-239">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Tamanho do cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="b888b-241">Para alterar o tamanho do cluster, use o controle deslizante ou digite um número entre 1 e 10 na caixa de texto **Contagem de fragmentos** e clique em **OK** para salvar.</span><span class="sxs-lookup"><span data-stu-id="b888b-241">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-242">O clustering está disponível apenas para os Caches premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="b888b-243">Para saber mais, consulte [Como configurar um cluster para um Cache Redis do Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-243">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="b888b-244">Persistência de dados do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-244">Redis data persistence</span></span>
<span data-ttu-id="b888b-245">Clique em **Persistência de dados do Redis** para habilitar, desabilitar ou configurar a persistência de dados para o cache premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-245">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="b888b-246">O Cache Redis do Microsoft Azure oferece persistência Redis usando [persistência RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) ou [persistência AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="b888b-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="b888b-247">Para saber mais, confira [Como configurar a persistência para um Cache Redis do Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-247">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="b888b-248">A persistência de dados do Redis só está disponível para os caches Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="b888b-249">Agende atualizações</span><span class="sxs-lookup"><span data-stu-id="b888b-249">Schedule updates</span></span>
<span data-ttu-id="b888b-250">A folha **Agendar atualizações** permite designar uma janela de manutenção para atualizações do servidor Redis do seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-250">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b888b-251">A janela de manutenção se aplica apenas às atualizações do servidor Redis e não a quaisquer atualizações do Azure ou atualizações do sistema operacional das VMs que hospedam o cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-251">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![Agendar atualizações](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="b888b-253">Para especificar uma janela de manutenção, marque os dias desejados, especifique a hora de início da janela de manutenção para cada dia e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b888b-253">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="b888b-254">Observe que o horário da janela de manutenção é em UTC.</span><span class="sxs-lookup"><span data-stu-id="b888b-254">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b888b-255">A funcionalidade **Agendar atualizações** está disponível somente para caches do nível Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-255">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="b888b-256">Para saber mais e instruções, confira [Como administrar o Cache Redis do Azure – Agendar atualizações](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="b888b-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="b888b-257">Replicação geográfica</span><span class="sxs-lookup"><span data-stu-id="b888b-257">Geo-replication</span></span>

<span data-ttu-id="b888b-258">A folha **Replicação geográfica** fornece um mecanismo para vincular duas instâncias de Cache Redis do Azure de camada Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-258">The **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="b888b-259">Um cache é designado como o cache vinculado primário e o outro como o cache vinculado secundário.</span><span class="sxs-lookup"><span data-stu-id="b888b-259">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="b888b-260">O cache vinculado secundário se torna somente leitura e os dados gravados no cache primário são replicados para o cache vinculado secundário.</span><span class="sxs-lookup"><span data-stu-id="b888b-260">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="b888b-261">Essa funcionalidade pode ser usada para replicar um cache entre regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="b888b-261">This functionality can be used to replicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-262">A **replicação geográfica** está disponível somente para caches de camada Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="b888b-263">Para obter mais informações e instruções, consulte [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md) (Como configurar a replicação geográfica para o Cache Redis do Azure).</span><span class="sxs-lookup"><span data-stu-id="b888b-263">For more information and instructions, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="b888b-264">Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="b888b-264">Virtual Network</span></span>
<span data-ttu-id="b888b-265">A seção **Rede Virtual** permite que você defina as configurações de rede virtual para o cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="b888b-266">Para saber mais sobre como criar um cache premium com suporte de rede virtual e atualizar suas configurações, confira [Como configurar o suporte de Rede Virtual para um Cache Redis do Azure Premium](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-267">As configurações de rede virtual só estão disponíveis para os caches premium configurados com suporte para rede virtual durante a criação do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="b888b-268">Firewall</span><span class="sxs-lookup"><span data-stu-id="b888b-268">Firewall</span></span>

<span data-ttu-id="b888b-269">Clique em **Firewall** para exibir e configurar regras de firewall para o Cache Redis do Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Firewall](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="b888b-271">É possível especificar regras de firewall com um intervalo de endereços IP inicial e final.</span><span class="sxs-lookup"><span data-stu-id="b888b-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="b888b-272">Quando regras de firewall são configuradas, apenas as conexões de cliente de intervalos de endereços IP especificados podem se conectar ao cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="b888b-273">Quando uma regra de firewall é salva, há um pequeno atraso antes que a regra entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="b888b-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="b888b-274">Normalmente, esse atraso é inferior a um minuto.</span><span class="sxs-lookup"><span data-stu-id="b888b-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-275">Conexões dos sistemas de monitoramento do Cache Redis do Azure serão sempre permitidas, mesmo se regras de firewall forem configuradas.</span><span class="sxs-lookup"><span data-stu-id="b888b-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="b888b-276">As regras de firewall estão disponíveis apenas para os caches da camada Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="b888b-277">Propriedades</span><span class="sxs-lookup"><span data-stu-id="b888b-277">Properties</span></span>
<span data-ttu-id="b888b-278">Clique em **Propriedades** para exibir informações sobre o cache, incluindo o ponto de extremidade e as portas do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Propriedades de Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="b888b-280">Bloqueios</span><span class="sxs-lookup"><span data-stu-id="b888b-280">Locks</span></span>
<span data-ttu-id="b888b-281">A seção **Bloqueios** permite bloquear uma assinatura, um recurso ou um grupo de recursos para impedir que outros usuários em sua organização excluam ou modifiquem acidentalmente recursos críticos.</span><span class="sxs-lookup"><span data-stu-id="b888b-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="b888b-282">Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="b888b-283">Script de automação</span><span class="sxs-lookup"><span data-stu-id="b888b-283">Automation script</span></span>

<span data-ttu-id="b888b-284">Clique em **Script de automação** para compilar e exportar um modelo de seus recursos implantados para implantações futuras.</span><span class="sxs-lookup"><span data-stu-id="b888b-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="b888b-285">Para saber mais sobre como trabalhar com modelos, confira [Implantar recursos com modelos do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="b888b-286">Configurações de administração</span><span class="sxs-lookup"><span data-stu-id="b888b-286">Administration settings</span></span>
<span data-ttu-id="b888b-287">As configurações na seção **Administração** permitem que você execute as tarefas administrativas a seguir para seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your cache.</span></span> 

![Administração](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="b888b-289">Importar dados</span><span class="sxs-lookup"><span data-stu-id="b888b-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="b888b-290">Exportar Dados</span><span class="sxs-lookup"><span data-stu-id="b888b-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="b888b-291">Reboot</span><span class="sxs-lookup"><span data-stu-id="b888b-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="b888b-292">Importar/exportar</span><span class="sxs-lookup"><span data-stu-id="b888b-292">Import/Export</span></span>
<span data-ttu-id="b888b-293">A Importação/Exportação é uma operação de gerenciamento de dados do Cache Redis do Azure que permite importar e exportar dados para o cache importando e exportando um instantâneo do RDB (Banco de Dados do Cache Redis) de um cache premium para um blob de páginas em uma Conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b888b-293">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="b888b-294">A Importação/Exportação permite migrar entre diferentes instâncias do Cache Redis do Azure ou popular o cache com os dados antes de usar.</span><span class="sxs-lookup"><span data-stu-id="b888b-294">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="b888b-295">A importação pode ser usada para trazer arquivos RDB compatíveis com o Redis de qualquer servidor Redis em execução em qualquer nuvem ou ambiente, incluindo o Redis em execução no Linux, Windows ou qualquer provedor de nuvem como Amazon Web Services e similares.</span><span class="sxs-lookup"><span data-stu-id="b888b-295">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="b888b-296">Importar os dados é uma maneira fácil de criar um cache com dados previamente populados.</span><span class="sxs-lookup"><span data-stu-id="b888b-296">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="b888b-297">Durante o processo de importação, o Cache Redis do Azure carrega os arquivos RDB do armazenamento do Azure na memória e insere as chaves no cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-297">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="b888b-298">A exportação permite exportar os dados armazenados no Cache Redis do Azure para arquivos RDB compatíveis com Redis.</span><span class="sxs-lookup"><span data-stu-id="b888b-298">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="b888b-299">Você pode usar esse recurso para mover dados de uma instância do Cache Redis do Azure para outro ou para outro servidor Redis.</span><span class="sxs-lookup"><span data-stu-id="b888b-299">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="b888b-300">Durante o processo de exportação, um arquivo temporário é criado na VM que hospeda a instância de servidor do Cache Redis do Azure e o arquivo é carregado para a conta de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="b888b-300">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="b888b-301">Após a operação de exportação ser concluída com um status de êxito ou de falha, o arquivo temporário é excluído.</span><span class="sxs-lookup"><span data-stu-id="b888b-301">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-302">A opção Importar/Exportar está disponível somente para caches do nível Premium.</span><span class="sxs-lookup"><span data-stu-id="b888b-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="b888b-303">Para saber mais e instruções, confira [Importar e exportar dados no Cache Redis do Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="b888b-304">Reboot</span><span class="sxs-lookup"><span data-stu-id="b888b-304">Reboot</span></span>
<span data-ttu-id="b888b-305">A folha **Reinicializar** permite a reinicialização dos nós do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-305">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="b888b-306">Essa funcionalidade de reinicialização permite que você teste seu aplicativo para garantir a resiliência caso ocorra uma falha de um nó de cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-306">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="b888b-308">Se tiver um cache premium com clustering habilitado, você poderá selecionar quais fragmentos do cache serão reinicializados.</span><span class="sxs-lookup"><span data-stu-id="b888b-308">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="b888b-310">Para reinicializar um ou mais nós do cache, selecione os nós desejados e clique em **Reinicializar**.</span><span class="sxs-lookup"><span data-stu-id="b888b-310">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="b888b-311">Se tiver um cache premium com clustering habilitado, selecione os fragmentos a serem reinicializados e clique em **Reinicializar**.</span><span class="sxs-lookup"><span data-stu-id="b888b-311">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="b888b-312">Depois de alguns minutos, os nós selecionados são reinicializados e voltam a ficar online alguns minutos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b888b-312">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b888b-313">A reinicialização agora está disponível para todos os tipos de preço.</span><span class="sxs-lookup"><span data-stu-id="b888b-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="b888b-314">Para saber mais e instruções, confira [Como administrar o Cache Redis do Azure – Reinicializar](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="b888b-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="b888b-315">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="b888b-315">Monitoring</span></span>

<span data-ttu-id="b888b-316">A seção **Monitoramento** permite que você configure o diagnóstico e o monitoramento para seu Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="b888b-316">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="b888b-317">Para saber mais sobre o diagnóstico e monitoramento do Cache Redis do Azure, confira [Como monitorar o Cache Redis do Azure](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostics](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="b888b-319">Métricas do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="b888b-320">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="b888b-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="b888b-321">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b888b-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="b888b-322">Métricas do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-322">Redis metrics</span></span>
<span data-ttu-id="b888b-323">Clique em **Métricas do Redis** para [exibir métricas](cache-how-to-monitor.md#view-cache-metrics) para seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-323">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="b888b-324">Regras de alerta</span><span class="sxs-lookup"><span data-stu-id="b888b-324">Alert rules</span></span>

<span data-ttu-id="b888b-325">Clique em **Regras de alerta** para configurar alertas com base nas métricas do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="b888b-325">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="b888b-326">Para obter mais informações, consulte [Alertas](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="b888b-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="b888b-327">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="b888b-327">Diagnostics</span></span>

<span data-ttu-id="b888b-328">Por padrão, as métricas de cache no Azure Monitor são [armazenadas durante 30 dias](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e, em seguida, excluídas.</span><span class="sxs-lookup"><span data-stu-id="b888b-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="b888b-329">Para manter suas métricas de cache por mais de 30 dias, clique em **Diagnóstico** para [configurar a conta de armazenamento](cache-how-to-monitor.md#export-cache-metrics) usada para armazenar o diagnóstico de cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-329">To persist your cache metrics for longer than 30 days, click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#export-cache-metrics) used to store cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="b888b-330">Além de arquivar suas métricas de cache no armazenamento, você também pode [transmiti-las para um Hub de Eventos ou enviá-las para o Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="b888b-330">In addition to archiving your cache metrics to storage, you can also [stream them to an Event hub or send them to Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="b888b-331">Configurações de suporte e solução de problemas</span><span class="sxs-lookup"><span data-stu-id="b888b-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="b888b-332">As configurações na seção **Suporte + solução de problemas** fornecem opções para resolver problemas com o cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Suporte + solução de problemas](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="b888b-334">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="b888b-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="b888b-335">Nova solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="b888b-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="b888b-336">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="b888b-336">Resource health</span></span>
<span data-ttu-id="b888b-337">**Resource Health** observa seu recurso e informa se ele está sendo executado conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="b888b-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="b888b-338">Para saber mais sobre o serviço Azure Resource Health, confira [Visão geral do Azure Resource Health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b888b-339">A integridade de recursos atualmente não consegue relatar a integridade de instâncias de Cache Redis do Azure hospedadas em uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="b888b-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="b888b-340">Para saber mais, confira [Todos os recursos de cache funcionam ao hospedar um cache em uma rede virtual?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="b888b-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="b888b-341">Nova solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="b888b-341">New support request</span></span>
<span data-ttu-id="b888b-342">Clique em **Nova solicitação de suporte** para abrir uma solicitação de suporte para seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="b888b-343">Configuração padrão do servidor Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-343">Default Redis server configuration</span></span>
<span data-ttu-id="b888b-344">Novas instâncias de Cache Redis do Azure são configuradas com os seguintes valores de configuração padrão Redis.</span><span class="sxs-lookup"><span data-stu-id="b888b-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="b888b-345">As configurações nesta seção não podem ser alteradas com o método `StackExchange.Redis.IServer.ConfigSet`.</span><span class="sxs-lookup"><span data-stu-id="b888b-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="b888b-346">Se esse método for chamado com um dos comandos nesta seção, será gerada uma exceção similar à seguinte:</span><span class="sxs-lookup"><span data-stu-id="b888b-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="b888b-347">Todos os valores que podem ser configurados, como **max-memory-policy**, podem ser configurados por meio do Portal do Azure ou de ferramentas de gerenciamento de linha de comando, como a CLI do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b888b-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="b888b-348">Configuração</span><span class="sxs-lookup"><span data-stu-id="b888b-348">Setting</span></span> | <span data-ttu-id="b888b-349">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="b888b-349">Default value</span></span> | <span data-ttu-id="b888b-350">Descrição</span><span class="sxs-lookup"><span data-stu-id="b888b-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="b888b-351">16</span><span class="sxs-lookup"><span data-stu-id="b888b-351">16</span></span> |<span data-ttu-id="b888b-352">O número de bancos de dados padrão é 16, mas você pode configurar um número diferente com base no tipo de preço.<sup>1</sup> O banco de dados padrão é o DB 0; você poderá selecionar um diferente por conexão usando `connection.GetDatabase(dbid)`, em que `dbid` é um número entre `0` e `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="b888b-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="b888b-353">Depende do tipo de preço<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b888b-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="b888b-354">Esse é o número máximo de clientes conectados permitidos ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="b888b-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="b888b-355">Quando o limite é atingido o Redis fecha todas as novas conexões, retornando um erro de 'número máximo de clientes atingido'.</span><span class="sxs-lookup"><span data-stu-id="b888b-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="b888b-356">A política Maxmemory é a configuração de como o Redis seleciona o que remover quando `maxmemory` (o tamanho da oferta de cache que você selecionou quando criou o cache) é atingido.</span><span class="sxs-lookup"><span data-stu-id="b888b-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="b888b-357">Com o Cache Redis do Azure, a configuração padrão é `volatile-lru`, que remove as chaves com um conjunto de expiração usando um algoritmo LRU.</span><span class="sxs-lookup"><span data-stu-id="b888b-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="b888b-358">Essa configuração pode ser definida no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b888b-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="b888b-359">Para obter mais informações, consulte [Políticas de memória](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="b888b-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="b888b-360">3</span><span class="sxs-lookup"><span data-stu-id="b888b-360">3</span></span> |<span data-ttu-id="b888b-361">Para economizar memória, LRU e algoritmos TTL mínimos são algoritmos aproximados, em vez de algoritmos precisos.</span><span class="sxs-lookup"><span data-stu-id="b888b-361">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="b888b-362">Por padrão, o Redis verificará três chaves e escolherá aquela que foi usada há mais tempo.</span><span class="sxs-lookup"><span data-stu-id="b888b-362">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="b888b-363">5.000</span><span class="sxs-lookup"><span data-stu-id="b888b-363">5,000</span></span> |<span data-ttu-id="b888b-364">Tempo máximo de execução de um script Lua em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="b888b-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="b888b-365">Se o tempo de execução máximo for atingido, o Redis registrará em log que um script ainda está em execução depois do tempo máximo permitido e começará a responder a consultas com um erro.</span><span class="sxs-lookup"><span data-stu-id="b888b-365">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="b888b-366">500</span><span class="sxs-lookup"><span data-stu-id="b888b-366">500</span></span> |<span data-ttu-id="b888b-367">O tamanho máximo da fila de eventos de script.</span><span class="sxs-lookup"><span data-stu-id="b888b-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="b888b-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="b888b-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="b888b-369">0 0 032mb 8mb 60</span><span class="sxs-lookup"><span data-stu-id="b888b-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="b888b-370">Os limites de buffer de saída do cliente podem ser usados para impor a desconexão de clientes que não estão lendo dados do servidor de forma rápida o suficiente, por algum motivo (uma razão comum é que um cliente Pub/Sub não consegue consumir mensagens de forma tão rápida quanto o editor consegue produzi-las).</span><span class="sxs-lookup"><span data-stu-id="b888b-370">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="b888b-371">Para obter mais informações, veja [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="b888b-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="b888b-372"><a name="databases"></a> 
<sup>1</sup>O limite para `databases` é diferente para cada tipo de preço do Cache Redis do Azure e pode ser definido na criação do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-372"><a name="databases"></a>
<sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="b888b-373">Se nenhuma configuração `databases` for especificada durante a criação do cache, o padrão será 16.</span><span class="sxs-lookup"><span data-stu-id="b888b-373">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="b888b-374">Caches Básico e Standard</span><span class="sxs-lookup"><span data-stu-id="b888b-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="b888b-375">Cache C0 (250 MB) - até 16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-375">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="b888b-376">Cache C1 (1 GB) - até 16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-376">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="b888b-377">Cache C2 (2,5 GB) - até 16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-377">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="b888b-378">Cache C3 (6 GB) - até 16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-378">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="b888b-379">Cache C4 (13 GB) - até 32 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-379">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="b888b-380">Cache C5 (26 GB) - até 48 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-380">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="b888b-381">Cache C6 (53 GB) - até 64 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-381">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="b888b-382">Caches Premium</span><span class="sxs-lookup"><span data-stu-id="b888b-382">Premium caches</span></span>
  * <span data-ttu-id="b888b-383">P1 (6 GB - 60 GB) - até 16 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-383">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="b888b-384">P2 (13 - 130 GB) - até 32 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-384">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="b888b-385">P3 (26 GB - 260 GB) - até 48 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-385">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="b888b-386">P4 (53 - 530 GB) - até 64 bancos de dados</span><span class="sxs-lookup"><span data-stu-id="b888b-386">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="b888b-387">Todos os caches premium com cluster Redis habilitado – o cluster Redis permite apenas o uso do banco de dados 0 para que o limite `databases` de qualquer cache premium com o cluster Redis habilitado seja efetivamente 1 e o comando [Select](http://redis.io/commands/select) não seja permitido.</span><span class="sxs-lookup"><span data-stu-id="b888b-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="b888b-388">Para saber mais, confira [Preciso fazer alguma alteração no meu aplicativo cliente para usar clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="b888b-388">For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="b888b-389">Para saber mais sobre bancos de dados, veja [O que são bancos de dados Redis?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="b888b-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="b888b-390">As configurações `databases` pode ser definida somente durante a criação do cache e apenas usando PowerShell, CLI ou outros clientes de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="b888b-390">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="b888b-391">Para obter um exemplo de configuração `databases` durante a criação de cache usando o PowerShell, confira [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="b888b-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="b888b-392"><a name="maxclients"></a> 
<sup>2</sup>`maxclients` é diferente para cada tipo de preço do Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b888b-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="b888b-393">Caches Básico e Standard</span><span class="sxs-lookup"><span data-stu-id="b888b-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="b888b-394">Cache C0 (250 MB) - até 256 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-394">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="b888b-395">Cache C1 (1 GB) - até 1.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-395">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="b888b-396">Cache C2 (2.5 GB) - até 2.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-396">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="b888b-397">Cache C3 (6 GB) - até 5.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-397">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="b888b-398">Cache C4 (13 GB) - até 10.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-398">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="b888b-399">Cache C5 (26 GB) - até 15.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-399">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="b888b-400">Cache C6 (53 GB) - até 20.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-400">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="b888b-401">Caches Premium</span><span class="sxs-lookup"><span data-stu-id="b888b-401">Premium caches</span></span>
  * <span data-ttu-id="b888b-402">P1 (6 GB - 60 GB) - até 7.500 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-402">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="b888b-403">P2 (13 GB - 130 GB) - até 15.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-403">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="b888b-404">P3 (26 GB - 260 GB) - até 30.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-404">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="b888b-405">P4 (53 GB - 530 GB) - até 40.000 conexões</span><span class="sxs-lookup"><span data-stu-id="b888b-405">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="b888b-406">Embora cada tamanho de cache permita *até* um determinado número de conexões, cada conexão com o Redis tem sobrecarga associadas.</span><span class="sxs-lookup"><span data-stu-id="b888b-406">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="b888b-407">Um exemplo de tal sobrecarga seria o uso da CPU e de memória como resultado de criptografia TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="b888b-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="b888b-408">O limite máximo de conexão para um tamanho de cache determinado pressupõe um cache com pouca carga.</span><span class="sxs-lookup"><span data-stu-id="b888b-408">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="b888b-409">Se a carga da conexão de sobrecarga *mais* a carga de operações do cliente excederem a capacidade do sistema, o cache poderá enfrentar problemas de capacidade mesmo se não exceder o limite de conexão para o tamanho atual do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-409">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="b888b-410">Comandos Redis não têm suporte no Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="b888b-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b888b-411">Como a configuração e o gerenciamento de instâncias de Cache Redis do Azure é gerenciada pela Microsoft, os comandos a seguir são desabilitados.</span><span class="sxs-lookup"><span data-stu-id="b888b-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="b888b-412">Se você tentar invocá-los, receberá uma mensagem de erro semelhante a `"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="b888b-412">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="b888b-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="b888b-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="b888b-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="b888b-414">BGSAVE</span></span>
> * <span data-ttu-id="b888b-415">CONFIG</span><span class="sxs-lookup"><span data-stu-id="b888b-415">CONFIG</span></span>
> * <span data-ttu-id="b888b-416">DEBUG</span><span class="sxs-lookup"><span data-stu-id="b888b-416">DEBUG</span></span>
> * <span data-ttu-id="b888b-417">MIGRATE</span><span class="sxs-lookup"><span data-stu-id="b888b-417">MIGRATE</span></span>
> * <span data-ttu-id="b888b-418">Salvar</span><span class="sxs-lookup"><span data-stu-id="b888b-418">SAVE</span></span>
> * <span data-ttu-id="b888b-419">SHUTDOWN</span><span class="sxs-lookup"><span data-stu-id="b888b-419">SHUTDOWN</span></span>
> * <span data-ttu-id="b888b-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="b888b-420">SLAVEOF</span></span>
> * <span data-ttu-id="b888b-421">CLUSTER - Os comandos de gravação do cluster estão desabilitados, mas comandos do Cluster somente leitura são permitidos.</span><span class="sxs-lookup"><span data-stu-id="b888b-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="b888b-422">Para saber mais sobre os comandos do Redis, confira [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="b888b-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="b888b-423">Console do Redis</span><span class="sxs-lookup"><span data-stu-id="b888b-423">Redis console</span></span>
<span data-ttu-id="b888b-424">Você pode emitir comandos com segurança para suas instâncias do Cache Redis do Azure usando o **Console do Redis**, que está disponível no Portal do Azure para todas as camadas de cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-424">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available in the Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="b888b-425">O Console do Redis não funciona com [VNET](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-425">The Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="b888b-426">Quando o seu cache faz parte de uma VNET, somente os clientes na VNET podem acessar o cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-426">When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="b888b-427">Como o Console do Redis é executado em seu navegador local, que está fora da VNET, ele não poderá se conectar ao seu cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-427">Because Redis Console runs in your local browser, which is outside the VNET, it can't connect to your cache.</span></span>
> - <span data-ttu-id="b888b-428">Nem todos os comandos do Redis têm suporte no Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="b888b-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="b888b-429">Para obter uma lista de comandos do Redis que estão desabilitados para o Cache Redis do Azure, veja a seção anterior [Comandos do Redis sem suporte no Cache Redis do Azure](#redis-commands-not-supported-in-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="b888b-429">For a list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="b888b-430">Para saber mais sobre os comandos do Redis, confira [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="b888b-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="b888b-431">Para acessar o Console do Redis, clique em **Console** na folha **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="b888b-431">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Console do Redis](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="b888b-433">Para emitir comandos em sua instância de cache, simplesmente digite o comando desejado no console.</span><span class="sxs-lookup"><span data-stu-id="b888b-433">To issue commands against your cache instance, simply type the desired command into the console.</span></span>

![Console do Redis](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="b888b-435">Usando o Console Redis com um cache Premium clusterizado</span><span class="sxs-lookup"><span data-stu-id="b888b-435">Using the Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="b888b-436">Quando usar o Console do Redis com um cache Premium clusterizado, você pode emitir comandos para um único fragmento do cache.</span><span class="sxs-lookup"><span data-stu-id="b888b-436">When using the Redis Console with a premium clustered cache, you can issue commands to a single shard of the cache.</span></span> <span data-ttu-id="b888b-437">Para emitir um comando para um fragmento específico, primeiro conecte-se ao fragmento desejado clicando no seletor de fragmento.</span><span class="sxs-lookup"><span data-stu-id="b888b-437">To issue a command to a specific shard, first connect to the desired shard by clicking it on the shard picker.</span></span>

![Console do Redis](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="b888b-439">Se você tentar acessar uma chave armazenada em um fragmento diferente do fragmento conectado, você receberá uma mensagem de erro semelhante à mensagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="b888b-439">If you attempt to access a key that is stored in a different shard than the connected shard, you receive an error message similar to the following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="b888b-440">No exemplo anterior, o fragmento 1 é o fragmento selecionado, mas `myKey` está localizado no fragmento 0, conforme indicado pela parte `(shard 0)` da mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="b888b-440">In the previous example, shard 1 is the selected shard, but `myKey` is located in shard 0, as indicated by the `(shard 0)` portion of the error message.</span></span> <span data-ttu-id="b888b-441">Neste exemplo, para acessar `myKey`, selecione o fragmento 0 usando o seletor de fragmento e, em seguida, execute o comando desejado.</span><span class="sxs-lookup"><span data-stu-id="b888b-441">In this example, to access `myKey`, select shard 0 using the shard picker, and then issue the desired command.</span></span>


## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="b888b-442">Mover o cache para uma nova assinatura</span><span class="sxs-lookup"><span data-stu-id="b888b-442">Move your cache to a new subscription</span></span>
<span data-ttu-id="b888b-443">Você pode mover o cache para uma nova assinatura clicando em **Mover**.</span><span class="sxs-lookup"><span data-stu-id="b888b-443">You can move your cache to a new subscription by clicking **Move**.</span></span>

![Mover o Cache Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="b888b-445">Para saber mais sobre como mover os recursos de um grupo de recursos para outro, e de uma assinatura para outra, confira [Mover recursos para um novo grupo de recursos ou uma nova assinatura](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b888b-445">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b888b-446">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b888b-446">Next steps</span></span>
* <span data-ttu-id="b888b-447">Para obter mais informações sobre como trabalhar com os comandos do Redis, consulte [Como posso executar comandos do Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="b888b-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

