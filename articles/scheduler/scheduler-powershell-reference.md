---
title: "aaaScheduler Referência dos Cmdlets do PowerShell"
description: "Referência de cmdlets do PowerShell do Agendador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="c46dd-103">Referência de cmdlets do PowerShell do Agendador</span><span class="sxs-lookup"><span data-stu-id="c46dd-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="c46dd-104">Olá, a tabela a seguir descreve e vincula a página de referência toohello de cada um dos cmdlets principais do hello no Agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="c46dd-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="c46dd-105">tooinstall PowerShell do Azure e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c46dd-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="c46dd-106">Para obter mais informações sobre os [Cmdlets do Azure Resource Manager](/powershell/azure/overview), consulte [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md) (Usando o Azure PowerShell com o Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c46dd-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="c46dd-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c46dd-107">Cmdlet</span></span> | <span data-ttu-id="c46dd-108">Descrição do cmdlet</span><span class="sxs-lookup"><span data-stu-id="c46dd-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="c46dd-109">Disable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="c46dd-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="c46dd-110">Desabilita uma coleção de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="c46dd-111">Enable-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="c46dd-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="c46dd-112">Habilita uma coleção de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="c46dd-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="c46dd-114">Obtém os trabalhos do Agendador.</span><span class="sxs-lookup"><span data-stu-id="c46dd-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="c46dd-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="c46dd-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="c46dd-116">Obtém coleções de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-116">Gets job collections.</span></span> |
| [<span data-ttu-id="c46dd-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="c46dd-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="c46dd-118">Obtém o histórico de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-118">Gets job history.</span></span> |
| [<span data-ttu-id="c46dd-119">New-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="c46dd-120">Cria um trabalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="c46dd-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="c46dd-121">New-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="c46dd-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="c46dd-122">Cria uma coleção de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="c46dd-123">New-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="c46dd-124">Cria um trabalho de fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c46dd-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="c46dd-125">New-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="c46dd-126">Cria um trabalho de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c46dd-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="c46dd-127">New-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="c46dd-128">Cria um trabalho da fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c46dd-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="c46dd-129">Remove-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="c46dd-130">Remove um trabalho do Agendador.</span><span class="sxs-lookup"><span data-stu-id="c46dd-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="c46dd-131">Remove-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="c46dd-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="c46dd-132">Remove uma coleção de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="c46dd-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="c46dd-134">Modifica um trabalho HTTP do Agendador.</span><span class="sxs-lookup"><span data-stu-id="c46dd-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="c46dd-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="c46dd-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="c46dd-136">Modifica uma coleção de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c46dd-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="c46dd-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="c46dd-138">Modifica um trabalho da fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c46dd-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="c46dd-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="c46dd-140">Modifica um trabalho de tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c46dd-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="c46dd-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="c46dd-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="c46dd-142">Modifica um trabalho da fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c46dd-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="c46dd-143">Para obter mais informações, você pode executar qualquer um dos Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="c46dd-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="c46dd-144">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c46dd-144">See Also</span></span>
 [<span data-ttu-id="c46dd-145">O que é o Agendador?</span><span class="sxs-lookup"><span data-stu-id="c46dd-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="c46dd-146">Conceitos, terminologia e hierarquia de entidades do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="c46dd-147">Começar a usar o Agendador no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="c46dd-148">Planos e Cobrança no Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="c46dd-149">Referência da API REST do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="c46dd-150">Alta disponibilidade e confiabilidade do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="c46dd-151">Limites, padrões e códigos de erro do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="c46dd-152">Autenticação de saída do Agendador do Azure</span><span class="sxs-lookup"><span data-stu-id="c46dd-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

