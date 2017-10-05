---
title: Limites e cotas de assinatura do Azure | Microsoft Docs
description: "Fornece uma lista de assinaturas comuns do Azure e limites de serviço, cotas e restrições. Isso inclui informações sobre como aumentar os limites junto com os valores máximos."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a76acd67e9ba7822f2837b3c08e2ede389047f11
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="20f77-104">Assinatura do Azure e limite de serviços, cotas e restrições</span><span class="sxs-lookup"><span data-stu-id="20f77-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="20f77-105">Este documento lista alguns dos limites mais comuns do Microsoft Azure, que também são chamados de cotas.</span><span class="sxs-lookup"><span data-stu-id="20f77-105">This document lists some of the most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="20f77-106">Esse documento não cobre atualmente todos os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="20f77-107">Com o passar do tempo, a lista será expandida e atualizada para uma maior cobertura da plataforma.</span><span class="sxs-lookup"><span data-stu-id="20f77-107">Over time, the list will be expanded and updated to cover more of the platform.</span></span>

<span data-ttu-id="20f77-108">Visite [Visão geral de preços do Azure](https://azure.microsoft.com/pricing/) para saber mais sobre preços do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) to learn more about Azure pricing.</span></span> <span data-ttu-id="20f77-109">Lá, você pode estimar os custos usando a [Calculadora de Preços](https://azure.microsoft.com/pricing/calculator/) ou visitando a página de detalhes de preços para um serviço (por exemplo, [VMs do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="20f77-109">There, you can estimate your costs using the [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting the pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="20f77-110">Para obter dicas sobre como ajudar a gerenciar custos, consulte [Evitar custos inesperados com o gerenciamento de custo e cobrança do Azure](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-110">For tips to help manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="20f77-111">Se você deseja aumentar o limite ou a cota acima do **Limite Padrão**, [abra uma solicitação no suporte ao cliente online sem custo](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-111">If you want to raise the limit or quota above the **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="20f77-112">Os limites não podem ser aumentados acima do valor **Limite Máximo** mostrado nas tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="20f77-112">The limits can't be raised above the **Maximum Limit** value shown in the following tables.</span></span> <span data-ttu-id="20f77-113">Se não houver nenhuma coluna **Limite Máximo**, o recurso não terá limites ajustáveis.</span><span class="sxs-lookup"><span data-stu-id="20f77-113">If there is no **Maximum Limit** column, then the resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="20f77-114">As assinaturas de Avaliação Gratuita não estão qualificadas para os aumentos de cota ou limite.</span><span class="sxs-lookup"><span data-stu-id="20f77-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="20f77-115">Se tiver uma Avaliação Gratuita, você poderá atualizar para uma assinatura [Pré-paga](https://azure.microsoft.com/offers/ms-azr-0003p/) .</span><span class="sxs-lookup"><span data-stu-id="20f77-115">If you have a Free Trial, you can upgrade to a [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="20f77-116">Para obter mais informações, consulte [Atualizar a Versão de Avaliação Gratuita do Azure para Pré-Pago](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-116">For more information, see [Upgrade Azure Free Trial to Pay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-the-azure-resource-manager"></a><span data-ttu-id="20f77-117">Limites e o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-117">Limits and the Azure Resource Manager</span></span>
<span data-ttu-id="20f77-118">Agora é possível combinar vários recursos do Azure em um único Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-118">It is now possible to combine multiple Azure resources in to a single Azure Resource Group.</span></span> <span data-ttu-id="20f77-119">Ao usar os Grupos de Recursos, limites que antes eram globais passam a ser gerenciados em nível regional com o Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-119">When using Resource Groups, limits that once were global become managed at a regional level with the Azure Resource Manager.</span></span> <span data-ttu-id="20f77-120">Para saber mais sobre os Grupos de Recursos do Azure, confira [Visão geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="20f77-121">Nos limites abaixo, uma nova tabela foi adicionada para refletir quaisquer diferenças nos limites ao usar o Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-121">In the limits below, a new table has been added to reflect any differences in limits when using the Azure Resource Manager.</span></span> <span data-ttu-id="20f77-122">Por exemplo, há uma tabela de **Limites de Assinatura** e uma tabela de **Limites de Assinatura – Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="20f77-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="20f77-123">Quando um limite se aplica a ambos os cenários, ele é mostrado apenas na primeira tabela.</span><span class="sxs-lookup"><span data-stu-id="20f77-123">When a limit applies to both scenarios, it is only shown in the first table.</span></span> <span data-ttu-id="20f77-124">A menos que indicado de outro modo, os limites são globais em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="20f77-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="20f77-125">É importante enfatizar que as cotas para recursos nos Grupos de Recursos do Azure são acessíveis de acordo com a região pela assinatura e não de acordo com a assinatura, assim como acontece com as cotas de gerenciamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="20f77-125">It is important to emphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as the service management quotas are.</span></span> <span data-ttu-id="20f77-126">Vamos usar cotas de núcleos como exemplo.</span><span class="sxs-lookup"><span data-stu-id="20f77-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="20f77-127">Se você precisar solicitar um aumento de cota com suporte para núcleos, você precisa decidir quantos núcleos deseja usar em quais regiões e, em seguida, fazer uma solicitação específica de cotas de núcleos do Grupo de Recursos do Azure para as quantidades e regiões desejadas.</span><span class="sxs-lookup"><span data-stu-id="20f77-127">If you need to request a quota increase with support for cores, you need to decide how many cores you want to use in which regions, and then make a specific request for Azure Resource Group core quotas for the amounts and regions that you want.</span></span> <span data-ttu-id="20f77-128">Portanto, se precisar usar 30 núcleos na Europa Ocidental para executar seu aplicativo lá, você deve solicitar especificamente 30 núcleos na Europa Ocidental.</span><span class="sxs-lookup"><span data-stu-id="20f77-128">Therefore, if you need to use 30 cores in West Europe to run your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="20f77-129">Mas você não terá um aumento na cota de núcleos em nenhuma outra região – somente a Europa Ocidental terá a cota de 30 núcleos.</span><span class="sxs-lookup"><span data-stu-id="20f77-129">But you will not have a core quota increase in any other region -- only West Europe will have the 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="20f77-130">Como resultado, pode ser útil pensar em decidir quais devem ser as cotas do Grupo de Recursos do Azure para a carga de trabalho em determinada região e solicitar essa quantidade em cada região na qual esteja considerando a possibilidade de implantação.</span><span class="sxs-lookup"><span data-stu-id="20f77-130">As a result, you may find it useful to consider deciding what your Azure Resource Group quotas need to be for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="20f77-131">Consulte [Solucionando problemas de implantação](resource-manager-common-deployment-errors.md) para obter mais ajuda ao descobrir suas cotas atuais para regiões específicas.</span><span class="sxs-lookup"><span data-stu-id="20f77-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="20f77-132">Limites específicos de serviço</span><span class="sxs-lookup"><span data-stu-id="20f77-132">Service-specific limits</span></span>
* [<span data-ttu-id="20f77-133">Active Directory</span><span class="sxs-lookup"><span data-stu-id="20f77-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="20f77-134">Gerenciamento da API</span><span class="sxs-lookup"><span data-stu-id="20f77-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="20f77-135">Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="20f77-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="20f77-136">Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="20f77-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="20f77-137">Application Insights</span><span class="sxs-lookup"><span data-stu-id="20f77-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="20f77-138">Automação</span><span class="sxs-lookup"><span data-stu-id="20f77-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="20f77-139">Banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="20f77-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="20f77-140">Grade de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="20f77-141">Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="20f77-142">RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="20f77-143">Backup</span><span class="sxs-lookup"><span data-stu-id="20f77-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="20f77-144">Batch</span><span class="sxs-lookup"><span data-stu-id="20f77-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="20f77-145">Serviços do BizTalk</span><span class="sxs-lookup"><span data-stu-id="20f77-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="20f77-146">CDN</span><span class="sxs-lookup"><span data-stu-id="20f77-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="20f77-147">Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="20f77-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="20f77-148">Instâncias de Contêiner</span><span class="sxs-lookup"><span data-stu-id="20f77-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="20f77-149">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="20f77-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="20f77-150">Análises Data Lake</span><span class="sxs-lookup"><span data-stu-id="20f77-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="20f77-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20f77-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="20f77-152">DNS</span><span class="sxs-lookup"><span data-stu-id="20f77-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="20f77-153">Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="20f77-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="20f77-154">Hub IoT</span><span class="sxs-lookup"><span data-stu-id="20f77-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="20f77-155">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="20f77-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="20f77-156">Log Analytics/Insights Operacionais</span><span class="sxs-lookup"><span data-stu-id="20f77-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="20f77-157">Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="20f77-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="20f77-158">Engajamento Móvel</span><span class="sxs-lookup"><span data-stu-id="20f77-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="20f77-159">Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="20f77-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="20f77-160">Monitorar</span><span class="sxs-lookup"><span data-stu-id="20f77-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="20f77-161">Autenticação Multifator</span><span class="sxs-lookup"><span data-stu-id="20f77-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="20f77-162">Rede</span><span class="sxs-lookup"><span data-stu-id="20f77-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="20f77-163">Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="20f77-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="20f77-164">Serviço de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="20f77-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="20f77-165">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="20f77-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="20f77-166">Agendador</span><span class="sxs-lookup"><span data-stu-id="20f77-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="20f77-167">Search</span><span class="sxs-lookup"><span data-stu-id="20f77-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="20f77-168">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="20f77-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="20f77-169">Recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="20f77-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="20f77-170">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="20f77-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="20f77-171">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="20f77-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="20f77-172">Sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="20f77-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="20f77-173">Análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="20f77-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="20f77-174">Assinatura</span><span class="sxs-lookup"><span data-stu-id="20f77-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="20f77-175">Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="20f77-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="20f77-176">Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="20f77-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="20f77-177">Conjuntos de Escala de Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="20f77-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="20f77-178">Limites de assinatura</span><span class="sxs-lookup"><span data-stu-id="20f77-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="20f77-179">Limites de assinatura</span><span class="sxs-lookup"><span data-stu-id="20f77-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="20f77-180">Limites de Assinatura – Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="20f77-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="20f77-181">Os limites a seguir se aplicam ao usar o Gerenciador de Recursos do Azure e os Grupos de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-181">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="20f77-182">Limites que não foram alterados com o Gerenciador de Recursos do Azure não estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="20f77-182">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="20f77-183">Consulte a tabela anterior para obter esses limites.</span><span class="sxs-lookup"><span data-stu-id="20f77-183">Please refer to the previous table for those limits.</span></span>

<span data-ttu-id="20f77-184">Para obter informações sobre como lidar com limites de solicitações do Resource Manager, confira [Throttling Resource Manager requests](resource-manager-request-limits.md) (Limitando as solicitações do Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="20f77-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="20f77-185">Limites do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="20f77-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="20f77-186">Limites de Máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="20f77-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="20f77-187">Limites de Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="20f77-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="20f77-188">Limites de Máquinas Virtuais – Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="20f77-189">Os limites a seguir se aplicam ao usar o Gerenciador de Recursos do Azure e os Grupos de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-189">The following limits apply when using the Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="20f77-190">Limites que não foram alterados com o Gerenciador de Recursos do Azure não estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="20f77-190">Limits that have not changed with the Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="20f77-191">Consulte a tabela anterior para obter esses limites.</span><span class="sxs-lookup"><span data-stu-id="20f77-191">Please refer to the previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="20f77-192">Limites de conjuntos de escala de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="20f77-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="20f77-193">Limites de Instâncias de Contêiner</span><span class="sxs-lookup"><span data-stu-id="20f77-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="20f77-194">Limites de rede</span><span class="sxs-lookup"><span data-stu-id="20f77-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="20f77-195">Limites de rede</span><span class="sxs-lookup"><span data-stu-id="20f77-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="20f77-196">Limites do Gateway de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="20f77-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="20f77-197">Limites do Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="20f77-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="20f77-198">Limites do Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="20f77-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="20f77-199">Limites de DNS</span><span class="sxs-lookup"><span data-stu-id="20f77-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="20f77-200">Limites de armazenamento</span><span class="sxs-lookup"><span data-stu-id="20f77-200">Storage limits</span></span>
<span data-ttu-id="20f77-201">Para obter mais detalhes sobre os limites da conta de armazenamento, veja [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="20f77-202">Limites de Serviço de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="20f77-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="20f77-203">Limites de disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="20f77-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="20f77-204">Consulte [Tamanhos de máquina virtual](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para saber mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="20f77-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="20f77-205">Discos de máquina virtual gerenciados</span><span class="sxs-lookup"><span data-stu-id="20f77-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="20f77-206">Discos de máquina virtual não gerenciados</span><span class="sxs-lookup"><span data-stu-id="20f77-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="20f77-207">Limites de Provedor de Recursos de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="20f77-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="20f77-208">Limites de Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="20f77-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="20f77-209">Limites do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="20f77-209">App Service limits</span></span>
<span data-ttu-id="20f77-210">Os limites de Serviço de Aplicativo a seguir incluem limites para Aplicativos Web, Aplicativos Móveis, Aplicativos de API e Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="20f77-210">The following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="20f77-211">Limites do Agendador</span><span class="sxs-lookup"><span data-stu-id="20f77-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="20f77-212">Limites de lote</span><span class="sxs-lookup"><span data-stu-id="20f77-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="20f77-213">Limites dos Serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="20f77-213">BizTalk Services limits</span></span>
<span data-ttu-id="20f77-214">A tabela a seguir mostra os limites para os serviços Biztalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="20f77-214">The following table shows the limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="20f77-215">Limites do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="20f77-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="20f77-216">O Azure Cosmos DB é um banco de dados de escala global no qual o armazenamento e a produtividade podem ser dimensionados para atender às necessidades de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20f77-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled to handle whatever your application requires.</span></span> <span data-ttu-id="20f77-217">Em caso de dúvidas sobre a escala fornecida pelo Azure Cosmos DB, envie um email para askcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="20f77-217">If you have any questions about the scale Azure Cosmos DB provides, please send email to askcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="20f77-218">Limites do Mobile Engagement </span><span class="sxs-lookup"><span data-stu-id="20f77-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="20f77-219">Limites do Search</span><span class="sxs-lookup"><span data-stu-id="20f77-219">Search limits</span></span>
<span data-ttu-id="20f77-220">Os tipos de preço determinam a capacidade e os limites de seu serviço Search.</span><span class="sxs-lookup"><span data-stu-id="20f77-220">Pricing tiers determine the capacity and limits of your search service.</span></span> <span data-ttu-id="20f77-221">Eles incluem:</span><span class="sxs-lookup"><span data-stu-id="20f77-221">Tiers include:</span></span>

* <span data-ttu-id="20f77-222">*Gratuito* serviço multilocatário, compartilhado com outros assinantes do Azure, destinado à avaliação e a pequenos projetos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="20f77-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="20f77-223">*Básico* fornece recursos de computação dedicados para cargas de trabalho de produção em uma escala menor, com até três réplicas para cargas de trabalho de consulta altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="20f77-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up to three replicas for highly available query workloads.</span></span>
* <span data-ttu-id="20f77-224">*Standard (S1, S2, S3, S3 de alta densidade)* para cargas de trabalho de produção maiores.</span><span class="sxs-lookup"><span data-stu-id="20f77-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="20f77-225">Há vários níveis dentro da camada Standard para que você possa escolher uma configuração de recursos que corresponda ao seu perfil de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="20f77-225">Multiple levels exist within the standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="20f77-226">**Limites por assinatura**</span><span class="sxs-lookup"><span data-stu-id="20f77-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="20f77-227">**Limites por serviço Search**</span><span class="sxs-lookup"><span data-stu-id="20f77-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="20f77-228">Para saber mais sobre limites em um nível mais granular, como o tamanho do documento, consultas por segundo, chaves, solicitações e respostas, confira [Limites de serviço no Azure Search](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-228">To learn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="20f77-229">Limites de Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="20f77-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="20f77-230">Limites de CDN</span><span class="sxs-lookup"><span data-stu-id="20f77-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="20f77-231">Limites de Serviços Móveis</span><span class="sxs-lookup"><span data-stu-id="20f77-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="20f77-232">Monitorar limites</span><span class="sxs-lookup"><span data-stu-id="20f77-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="20f77-233">Limites de serviço de hub de notificação</span><span class="sxs-lookup"><span data-stu-id="20f77-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="20f77-234">Limites de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="20f77-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="20f77-235">Limites de Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="20f77-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="20f77-236">Limites do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="20f77-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="20f77-237">Limites de fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="20f77-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="20f77-238">Limites do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="20f77-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="20f77-239">Limites do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20f77-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="20f77-240">Limites do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20f77-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="20f77-241">Limites do Active Directory</span><span class="sxs-lookup"><span data-stu-id="20f77-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="20f77-242">Limites de Grade de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="20f77-243">Limites do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="20f77-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="20f77-244">Limites do sistema StorSimple</span><span class="sxs-lookup"><span data-stu-id="20f77-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="20f77-245">Limites do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="20f77-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="20f77-246">Limites do Backup</span><span class="sxs-lookup"><span data-stu-id="20f77-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="20f77-247">Limites da Recuperação de Site</span><span class="sxs-lookup"><span data-stu-id="20f77-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="20f77-248">Limites do Application Insights</span><span class="sxs-lookup"><span data-stu-id="20f77-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="20f77-249">Limites de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="20f77-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="20f77-250">Limites do Cache Redis do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="20f77-251">Limites do Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="20f77-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="20f77-252">Autenticação Multifator</span><span class="sxs-lookup"><span data-stu-id="20f77-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="20f77-253">Limites de automação</span><span class="sxs-lookup"><span data-stu-id="20f77-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="20f77-254">Limites de banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="20f77-254">SQL Database limits</span></span>
<span data-ttu-id="20f77-255">Para obter os limites do Banco de Dados SQL, veja [Limites de recurso de Banco de Dados SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="20f77-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="20f77-256">Confira também</span><span class="sxs-lookup"><span data-stu-id="20f77-256">See also</span></span>
[<span data-ttu-id="20f77-257">Entendendo os limites e aumentos do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="20f77-258">Tamanhos de máquinas virtuais e serviços de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="20f77-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="20f77-259">Tamanhos dos serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="20f77-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

