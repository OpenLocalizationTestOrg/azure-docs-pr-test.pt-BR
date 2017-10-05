---
title: "Arquivar Logs de Diagnóstico do Azure | Microsoft Docs"
description: "Saiba como arquivar os Logs de Diagnóstico do Azure para retenção de longo prazo em uma conta de armazenamento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: dbc5f89001dcb6cd1ab061cb0a9632e4e5d2c1c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="5cff3-103">Arquivar Logs de Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="5cff3-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="5cff3-104">Neste artigo, mostraremos como você pode usar o portal do Azure, os cmdlets do PowerShell, CLI ou API REST para arquivar seu [log de diagnóstico do Azure](monitoring-overview-of-diagnostic-logs.md) em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, CLI, or REST API to archive your [Azure diagnostic logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="5cff3-105">Essa opção será útil se você quiser manter seu log de diagnóstico com uma política de retenção opcional para auditoria, análise estática ou backup.</span><span class="sxs-lookup"><span data-stu-id="5cff3-105">This option is useful if you would like to retain your diagnostic logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="5cff3-106">A conta de armazenamento não precisa estar na mesma assinatura que o recurso que emite os logs, contanto que o usuário que define a configuração tenha acesso RBAC apropriado a ambas as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="5cff3-106">The storage account does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cff3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5cff3-107">Prerequisites</span></span>
<span data-ttu-id="5cff3-108">Antes de começar, você precisará [criar uma conta de armazenamento](../storage/storage-create-storage-account.md) na qual é possível arquivar os seus logs de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="5cff3-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md) to which you can archive your diagnostic logs.</span></span> <span data-ttu-id="5cff3-109">É altamente recomendável que você não use uma conta de armazenamento existente que tenha outros dados sem monitoramento armazenados para que você possa controlar melhor o acesso aos dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="5cff3-110">No entanto, se você estiver arquivando também os Logs de Atividade e as métricas de diagnóstico em uma conta de armazenamento, talvez faça sentido usar essa conta de armazenamento para o log de diagnóstico, bem como manter todos os dados de monitoramento em um local central.</span><span class="sxs-lookup"><span data-stu-id="5cff3-110">However, if you are also archiving your Activity Log and diagnostic metrics to a storage account, it may make sense to use that storage account for your diagnostic logs as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="5cff3-111">A conta de armazenamento usada deve ser uma conta de armazenamento de finalidade geral e não uma conta de armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="5cff3-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="5cff3-112">Configurações de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="5cff3-112">Diagnostic settings</span></span>
<span data-ttu-id="5cff3-113">Para arquivar os logs de diagnóstico usando qualquer um dos métodos abaixo, defina uma **configuração de diagnóstico** para um determinado recurso.</span><span class="sxs-lookup"><span data-stu-id="5cff3-113">To archive your diagnostic logs using any of the methods below, you set a **diagnostic setting** for a particular resource.</span></span> <span data-ttu-id="5cff3-114">Uma configuração de diagnóstico para um recurso define as categorias de logs e dados de métrica enviados a um destino (conta de armazenamento, namespace de Hubs de Eventos ou Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="5cff3-114">A diagnostic setting for a resource defines the categories of logs and metric data sent to a destination (storage account, Event Hubs namespace, or Log Analytics).</span></span> <span data-ttu-id="5cff3-115">Ela também define a política de retenção (número de dias para armazenamento) para eventos de cada categoria de log e dados de métrica armazenados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-115">It also defines the retention policy (number of days to retain) for events of each log category and metric data stored in a storage account.</span></span> <span data-ttu-id="5cff3-116">Se uma política de retenção for definida como zero, os eventos para essa categoria de log serão armazenados indefinidamente (ou seja, para sempre).</span><span class="sxs-lookup"><span data-stu-id="5cff3-116">If a retention policy is set to zero, events for that log category are stored indefinitely (that is to say, forever).</span></span> <span data-ttu-id="5cff3-117">Uma política de retenção pode ser qualquer quantidade de dias, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="5cff3-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="5cff3-118">[Leia mais sobre configurações de diagnóstico aqui](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="5cff3-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span> <span data-ttu-id="5cff3-119">As políticas de retenção são aplicadas por dia, para que, ao final de um dia (UTC), os logs do dia após a política de retenção sejam excluídos.</span><span class="sxs-lookup"><span data-stu-id="5cff3-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="5cff3-120">Por exemplo, se você tiver uma política de retenção de um dia, no início do dia de hoje, os logs de anteontem serão excluídos</span><span class="sxs-lookup"><span data-stu-id="5cff3-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-the-portal"></a><span data-ttu-id="5cff3-121">Arquivar logs de diagnóstico usando o portal</span><span class="sxs-lookup"><span data-stu-id="5cff3-121">Archive diagnostic logs using the portal</span></span>
1. <span data-ttu-id="5cff3-122">No portal, navegue até o Azure Monitor e clique em **Configurações de Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="5cff3-122">In the portal, navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Seção de monitoramento do Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="5cff3-124">Se desejar filtrar a lista por tipo de recurso ou grupo de recursos, clique no recurso para o qual você deseja definir uma configuração de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="5cff3-124">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="5cff3-125">Se nenhuma configuração existir no recurso que você selecionou, será solicitada a criação de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="5cff3-125">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="5cff3-126">Clique em “Ativar diagnóstico”.</span><span class="sxs-lookup"><span data-stu-id="5cff3-126">Click "Turn on diagnostics."</span></span>

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="5cff3-128">Se houver configurações existentes no recurso, você verá uma lista de configurações já definidas nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="5cff3-128">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="5cff3-129">Clique em "Adicionar configuração de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="5cff3-129">Click "Add diagnostic setting."</span></span>

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="5cff3-131">Dê um nome à sua configuração e marque a caixa **Exportar para Conta de Armazenamento** e então selecione uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-131">Give your setting a name and check the box for **Export to Storage Account**, then select a storage account.</span></span> <span data-ttu-id="5cff3-132">Como opção, defina um número de dias para manter esses logs usando os controles deslizantes **Retenção (dias)** .</span><span class="sxs-lookup"><span data-stu-id="5cff3-132">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders.</span></span> <span data-ttu-id="5cff3-133">Uma retenção de zero dias armazena os logs indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="5cff3-133">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="5cff3-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5cff3-135">Click **Save**.</span></span>

<span data-ttu-id="5cff3-136">Após alguns instantes, a nova configuração aparece na lista de configurações para esse recurso e os logs de diagnóstico são arquivados para essa conta de armazenamento assim que os novos dados de evento são gerados.</span><span class="sxs-lookup"><span data-stu-id="5cff3-136">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are archived to that storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-azure-powershell"></a><span data-ttu-id="5cff3-137">Arquivar logs de diagnóstico por meio do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cff3-137">Archive diagnostic logs via Azure PowerShell</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="5cff3-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5cff3-138">Property</span></span> | <span data-ttu-id="5cff3-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5cff3-139">Required</span></span> | <span data-ttu-id="5cff3-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="5cff3-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5cff3-141">ResourceId</span><span class="sxs-lookup"><span data-stu-id="5cff3-141">ResourceId</span></span> |<span data-ttu-id="5cff3-142">Sim</span><span class="sxs-lookup"><span data-stu-id="5cff3-142">Yes</span></span> |<span data-ttu-id="5cff3-143">ID de Recurso do recurso no qual você deseja definir uma configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5cff3-143">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="5cff3-144">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="5cff3-144">StorageAccountId</span></span> |<span data-ttu-id="5cff3-145">Não</span><span class="sxs-lookup"><span data-stu-id="5cff3-145">No</span></span> |<span data-ttu-id="5cff3-146">A ID de Recurso da Conta de Armazenamento na qual os Logs de Diagnóstico devem ser salvos.</span><span class="sxs-lookup"><span data-stu-id="5cff3-146">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="5cff3-147">Categorias</span><span class="sxs-lookup"><span data-stu-id="5cff3-147">Categories</span></span> |<span data-ttu-id="5cff3-148">Não</span><span class="sxs-lookup"><span data-stu-id="5cff3-148">No</span></span> |<span data-ttu-id="5cff3-149">Lista separada por vírgulas de categorias de log para habilitar.</span><span class="sxs-lookup"><span data-stu-id="5cff3-149">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="5cff3-150">Habilitado</span><span class="sxs-lookup"><span data-stu-id="5cff3-150">Enabled</span></span> |<span data-ttu-id="5cff3-151">Sim</span><span class="sxs-lookup"><span data-stu-id="5cff3-151">Yes</span></span> |<span data-ttu-id="5cff3-152">Booliano indicando se os diagnósticos estão habilitados ou desabilitados nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="5cff3-152">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="5cff3-153">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="5cff3-153">RetentionEnabled</span></span> |<span data-ttu-id="5cff3-154">Não</span><span class="sxs-lookup"><span data-stu-id="5cff3-154">No</span></span> |<span data-ttu-id="5cff3-155">Booliano indicando se há uma política de retenção habilitada nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="5cff3-155">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="5cff3-156">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="5cff3-156">RetentionInDays</span></span> |<span data-ttu-id="5cff3-157">Não</span><span class="sxs-lookup"><span data-stu-id="5cff3-157">No</span></span> |<span data-ttu-id="5cff3-158">Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="5cff3-158">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="5cff3-159">Um valor de zero armazena os logs indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="5cff3-159">A value of zero stores the logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-the-cross-platform-cli"></a><span data-ttu-id="5cff3-160">Arquivar os logs de diagnóstico por meio da CLI de Plataforma Cruzada</span><span class="sxs-lookup"><span data-stu-id="5cff3-160">Archive diagnostic logs via the Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="5cff3-161">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5cff3-161">Property</span></span> | <span data-ttu-id="5cff3-162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5cff3-162">Required</span></span> | <span data-ttu-id="5cff3-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="5cff3-163">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5cff3-164">ResourceId</span><span class="sxs-lookup"><span data-stu-id="5cff3-164">resourceId</span></span> |<span data-ttu-id="5cff3-165">Sim</span><span class="sxs-lookup"><span data-stu-id="5cff3-165">Yes</span></span> |<span data-ttu-id="5cff3-166">ID de Recurso do recurso no qual você deseja definir uma configuração de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5cff3-166">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="5cff3-167">storageId</span><span class="sxs-lookup"><span data-stu-id="5cff3-167">storageId</span></span> |<span data-ttu-id="5cff3-168">Não</span><span class="sxs-lookup"><span data-stu-id="5cff3-168">No</span></span> |<span data-ttu-id="5cff3-169">A ID de Recurso da Conta de Armazenamento na qual os logs de diagnóstico devem ser salvos.</span><span class="sxs-lookup"><span data-stu-id="5cff3-169">Resource ID of the Storage Account to which diagnostic logs should be saved.</span></span> |
| <span data-ttu-id="5cff3-170">Categorias</span><span class="sxs-lookup"><span data-stu-id="5cff3-170">categories</span></span> |<span data-ttu-id="5cff3-171">Não</span><span class="sxs-lookup"><span data-stu-id="5cff3-171">No</span></span> |<span data-ttu-id="5cff3-172">Lista separada por vírgulas de categorias de log para habilitar.</span><span class="sxs-lookup"><span data-stu-id="5cff3-172">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="5cff3-173">Habilitado</span><span class="sxs-lookup"><span data-stu-id="5cff3-173">enabled</span></span> |<span data-ttu-id="5cff3-174">Sim</span><span class="sxs-lookup"><span data-stu-id="5cff3-174">Yes</span></span> |<span data-ttu-id="5cff3-175">Booliano indicando se os diagnósticos estão habilitados ou desabilitados nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="5cff3-175">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-the-rest-api"></a><span data-ttu-id="5cff3-176">Arquivar logs de diagnóstico por meio da API REST</span><span class="sxs-lookup"><span data-stu-id="5cff3-176">Archive diagnostic logs via the REST API</span></span>
<span data-ttu-id="5cff3-177">[Confira este documento](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) para saber mais sobre como definir uma configuração de diagnóstico usando a API REST do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="5cff3-177">[See this document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) for information on how you can set up a diagnostic setting using the Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="5cff3-178">Esquema de logs de diagnóstico na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5cff3-178">Schema of diagnostic logs in the storage account</span></span>
<span data-ttu-id="5cff3-179">Após a configuração do arquivamento, um contêiner de armazenamento será criado na conta de armazenamento assim que ocorrer um evento em uma das categorias de log habilitadas.</span><span class="sxs-lookup"><span data-stu-id="5cff3-179">Once you have set up archival, a storage container is created in the storage account as soon as an event occurs in one of the log categories you have enabled.</span></span> <span data-ttu-id="5cff3-180">Os blobs no contêiner seguem o mesmo formato em todos os Logs de Diagnóstico e no Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="5cff3-180">The blobs within the container follow the same format across Diagnostic Logs and the Activity Log.</span></span> <span data-ttu-id="5cff3-181">A estrutura desses blobs é:</span><span class="sxs-lookup"><span data-stu-id="5cff3-181">The structure of these blobs is:</span></span>

> <span data-ttu-id="5cff3-182">insights-logs-{nome da categoria de log}/resourceId=/SUBSCRIPTIONS/{ID da assinatura}/RESOURCEGROUPS/{nome do grupo de recursos}/PROVIDERS/{nome do provedor de recursos}/{tipo de recurso}/{nome do recurso}/y={ano com quatro dígitos numéricos}/m={mês com dois dígitos numéricos}/d={dia com dois dígitos numéricos}/h={horário com dois dígitos no formato 24 horas}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="5cff3-182">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="5cff3-183">Ou, mais simplesmente,</span><span class="sxs-lookup"><span data-stu-id="5cff3-183">Or, more simply,</span></span>

> <span data-ttu-id="5cff3-184">insights-logs-{nome da categoria de log}/resourceId=/{ID do recurso}/y={ano com quatro dígitos numéricos}/m={mês com dois dígitos numéricos}/d={dia com dois dígitos numéricos}/h={horário com dois dígitos no formato 24 horas}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="5cff3-184">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="5cff3-185">Por exemplo, um nome de blob poderia ser:</span><span class="sxs-lookup"><span data-stu-id="5cff3-185">For example, a blob name might be:</span></span>

> <span data-ttu-id="5cff3-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="5cff3-186">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="5cff3-187">Cada blob PT1H.json contém um blob JSON de eventos que ocorreram dentro de uma hora especificada na URL do blob (por exemplo, h=12).</span><span class="sxs-lookup"><span data-stu-id="5cff3-187">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span></span> <span data-ttu-id="5cff3-188">Durante a hora presente, os eventos são acrescentados ao arquivo PT1H.json conforme eles ocorrem.</span><span class="sxs-lookup"><span data-stu-id="5cff3-188">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="5cff3-189">O valor de minuto (m=00) é sempre 00, como eventos de logs de diagnóstico são divididos em blobs individuais por hora.</span><span class="sxs-lookup"><span data-stu-id="5cff3-189">The minute value (m=00) is always 00, since diagnostic log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="5cff3-190">No arquivo PT1H.json, cada evento é armazenado na matriz de "registros", seguindo este formato:</span><span class="sxs-lookup"><span data-stu-id="5cff3-190">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| <span data-ttu-id="5cff3-191">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="5cff3-191">Element name</span></span> | <span data-ttu-id="5cff3-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="5cff3-192">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5cff3-193">tempo real</span><span class="sxs-lookup"><span data-stu-id="5cff3-193">time</span></span> |<span data-ttu-id="5cff3-194">Carimbo de hora quando o evento foi gerado pelo serviço do Azure que está processando a solicitação correspondente ao evento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-194">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="5cff3-195">ResourceId</span><span class="sxs-lookup"><span data-stu-id="5cff3-195">resourceId</span></span> |<span data-ttu-id="5cff3-196">ID de recurso do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="5cff3-196">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="5cff3-197">operationName</span><span class="sxs-lookup"><span data-stu-id="5cff3-197">operationName</span></span> |<span data-ttu-id="5cff3-198">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="5cff3-198">Name of the operation.</span></span> |
| <span data-ttu-id="5cff3-199">categoria</span><span class="sxs-lookup"><span data-stu-id="5cff3-199">category</span></span> |<span data-ttu-id="5cff3-200">Categoria de log do evento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-200">Log category of the event.</span></span> |
| <span data-ttu-id="5cff3-201">propriedades</span><span class="sxs-lookup"><span data-stu-id="5cff3-201">properties</span></span> |<span data-ttu-id="5cff3-202">Conjunto de pares de `<Key, Value>` (ou seja, Dicionário) que descreve os detalhes do evento.</span><span class="sxs-lookup"><span data-stu-id="5cff3-202">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="5cff3-203">As propriedades e o uso dessas propriedades podem variar dependendo do recurso.</span><span class="sxs-lookup"><span data-stu-id="5cff3-203">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5cff3-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5cff3-204">Next steps</span></span>
* [<span data-ttu-id="5cff3-205">Baixar blobs para análise</span><span class="sxs-lookup"><span data-stu-id="5cff3-205">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="5cff3-206">Logs de diagnóstico de fluxo para um namespace de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5cff3-206">Stream diagnostic logs to an Event Hubs namespace</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="5cff3-207">Leia mais sobre logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="5cff3-207">Read more about diagnostic logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
