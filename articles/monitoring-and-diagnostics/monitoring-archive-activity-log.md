---
title: Arquivar o Log de Atividades do Azure | Microsoft Docs
description: "Saiba como arquivar o Log de Atividades do Azure para retenção de longo prazo em uma conta de armazenamento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 0e3a5b84f57eac96249430fa1c2c4cc076c2926a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="2c98c-103">Arquivar o Log de Atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="2c98c-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="2c98c-104">Neste artigo, mostraremos como você pode usar o portal do Azure, os cmdlets do PowerShell ou a CLI de Plataforma Cruzada para arquivar seu [**Log de Atividades do Azure**](monitoring-overview-activity-logs.md) em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="2c98c-105">Essa opção será útil se você quiser manter seu Log de Atividades por mais de 90 dias (com controle total sobre a política de retenção) para auditoria, análise estática ou backup.</span><span class="sxs-lookup"><span data-stu-id="2c98c-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="2c98c-106">Se você só precisar manter seus eventos por 90 dias ou menos, não será necessário configurar o arquivamento em uma conta de armazenamento, já que os eventos de Log de Atividades são mantidos na plataforma do Azure por 90 dias sem habilitar o arquivamento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c98c-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c98c-107">Prerequisites</span></span>
<span data-ttu-id="2c98c-108">Antes de começar, você precisará [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) na qual é possível arquivar o seu Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="2c98c-108">Before you begin, you need to [create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="2c98c-109">É altamente recomendável que você não use uma conta de armazenamento existente que tenha outros dados sem monitoramento armazenados para que você possa controlar melhor o acesso aos dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="2c98c-110">No entanto, se você estiver arquivando também os Logs de Diagnóstico e as métricas em uma conta de armazenamento, talvez faça sentido usar essa conta de armazenamento para o Log de Atividades, bem como manter todos os dados de monitoramento em um local central.</span><span class="sxs-lookup"><span data-stu-id="2c98c-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="2c98c-111">A conta de armazenamento usada deve ser uma conta de armazenamento de finalidade geral e não uma conta de armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="2c98c-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="2c98c-112">A conta de armazenamento não precisa estar na mesma assinatura que a assinatura que emite os logs, contanto que o usuário que define a configuração tenha acesso RBAC apropriado a ambas as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="2c98c-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="2c98c-113">Perfil de Log</span><span class="sxs-lookup"><span data-stu-id="2c98c-113">Log Profile</span></span>
<span data-ttu-id="2c98c-114">Para arquivar o Log de Atividades usando qualquer um dos métodos abaixo, você deverá definir o **Log de Perfil** para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="2c98c-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="2c98c-115">O Perfil de Log define o tipo de eventos armazenados ou transmitidos e as saídas — conta de armazenamento e/ou hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="2c98c-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="2c98c-116">Ele também define a política de retenção (número de dias para manter) para eventos armazenados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="2c98c-117">Se a política de retenção for definida como zero, os eventos serão armazenados indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="2c98c-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="2c98c-118">Caso contrário, isso pode ser definido como qualquer valor entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="2c98c-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="2c98c-119">As políticas de retenção são aplicadas por dia, para que, ao final de um dia (UTC), os logs do dia após a política de retenção sejam excluídos.</span><span class="sxs-lookup"><span data-stu-id="2c98c-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="2c98c-120">Por exemplo, se você tiver uma política de retenção de um dia, no início do dia de hoje, os logs de anteontem serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="2c98c-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="2c98c-121">[Você pode ler mais sobre perfis de log aqui](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="2c98c-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="2c98c-122">Arquivar o Log de Atividades usando o portal</span><span class="sxs-lookup"><span data-stu-id="2c98c-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="2c98c-123">No portal, clique no link **Log de atividades** na barra de navegação do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="2c98c-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="2c98c-124">Se você não vir um link para o Log de Atividades, clique no link **Mais Serviços** primeiro.</span><span class="sxs-lookup"><span data-stu-id="2c98c-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![Navegue até a folha Log de Atividades](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="2c98c-126">Na parte superior da folha, clique **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="2c98c-126">At the top of the blade, click **Export**.</span></span>
   
    ![Clique no botão Exportar](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="2c98c-128">Na folha que aparece, marque a caixa de **Exportar para uma conta de armazenamento** e selecione uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![De uma conta de armazenamento](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="2c98c-130">Usando o controle deslizante ou a caixa de texto, defina um número de dias para os quais eventos do Log de Atividades devem ser mantidos em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="2c98c-131">Se você preferir que os dados persistam na conta de armazenamento indefinidamente, defina esse número como zero.</span><span class="sxs-lookup"><span data-stu-id="2c98c-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="2c98c-132">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2c98c-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="2c98c-133">Arquivar o Log de Atividades por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c98c-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="2c98c-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2c98c-134">Property</span></span> | <span data-ttu-id="2c98c-135">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2c98c-135">Required</span></span> | <span data-ttu-id="2c98c-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="2c98c-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c98c-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="2c98c-137">StorageAccountId</span></span> |<span data-ttu-id="2c98c-138">Não</span><span class="sxs-lookup"><span data-stu-id="2c98c-138">No</span></span> |<span data-ttu-id="2c98c-139">A ID de Recurso da Conta de Armazenamento na qual os Logs de Atividades devem ser salvos.</span><span class="sxs-lookup"><span data-stu-id="2c98c-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="2c98c-140">Locais</span><span class="sxs-lookup"><span data-stu-id="2c98c-140">Locations</span></span> |<span data-ttu-id="2c98c-141">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-141">Yes</span></span> |<span data-ttu-id="2c98c-142">Lista separada por vírgulas de regiões para as quais você gostaria de coletar eventos do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="2c98c-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="2c98c-143">Você pode exibir uma lista de todas as regiões [ao visitar esta página](https://azure.microsoft.com/en-us/regions) ou usando [a API REST de Gerenciamento do Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c98c-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="2c98c-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="2c98c-144">RetentionInDays</span></span> |<span data-ttu-id="2c98c-145">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-145">Yes</span></span> |<span data-ttu-id="2c98c-146">Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="2c98c-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="2c98c-147">Um valor de zero armazena os logs indefinidamente (para sempre).</span><span class="sxs-lookup"><span data-stu-id="2c98c-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="2c98c-148">Categorias</span><span class="sxs-lookup"><span data-stu-id="2c98c-148">Categories</span></span> |<span data-ttu-id="2c98c-149">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-149">Yes</span></span> |<span data-ttu-id="2c98c-150">Lista separada por vírgulas de categorias de eventos que devem ser coletados.</span><span class="sxs-lookup"><span data-stu-id="2c98c-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="2c98c-151">Os valores possíveis são Gravação, Exclusão e Ação.</span><span class="sxs-lookup"><span data-stu-id="2c98c-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="2c98c-152">Arquivar o Log de Atividades por meio da CLI</span><span class="sxs-lookup"><span data-stu-id="2c98c-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="2c98c-153">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2c98c-153">Property</span></span> | <span data-ttu-id="2c98c-154">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2c98c-154">Required</span></span> | <span data-ttu-id="2c98c-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="2c98c-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c98c-156">name</span><span class="sxs-lookup"><span data-stu-id="2c98c-156">name</span></span> |<span data-ttu-id="2c98c-157">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-157">Yes</span></span> |<span data-ttu-id="2c98c-158">Nome de seu perfil de log.</span><span class="sxs-lookup"><span data-stu-id="2c98c-158">Name of your log profile.</span></span> |
| <span data-ttu-id="2c98c-159">storageId</span><span class="sxs-lookup"><span data-stu-id="2c98c-159">storageId</span></span> |<span data-ttu-id="2c98c-160">Não</span><span class="sxs-lookup"><span data-stu-id="2c98c-160">No</span></span> |<span data-ttu-id="2c98c-161">A ID de Recurso da Conta de Armazenamento na qual os Logs de Atividades devem ser salvos.</span><span class="sxs-lookup"><span data-stu-id="2c98c-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="2c98c-162">Locais</span><span class="sxs-lookup"><span data-stu-id="2c98c-162">locations</span></span> |<span data-ttu-id="2c98c-163">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-163">Yes</span></span> |<span data-ttu-id="2c98c-164">Lista separada por vírgulas de regiões para as quais você gostaria de coletar eventos do Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="2c98c-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="2c98c-165">Você pode exibir uma lista de todas as regiões [ao visitar esta página](https://azure.microsoft.com/en-us/regions) ou usando [a API REST de Gerenciamento do Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c98c-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="2c98c-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="2c98c-166">retentionInDays</span></span> |<span data-ttu-id="2c98c-167">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-167">Yes</span></span> |<span data-ttu-id="2c98c-168">Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="2c98c-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="2c98c-169">Um valor de zero armazenará os logs indefinidamente (para sempre).</span><span class="sxs-lookup"><span data-stu-id="2c98c-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="2c98c-170">Categorias</span><span class="sxs-lookup"><span data-stu-id="2c98c-170">categories</span></span> |<span data-ttu-id="2c98c-171">Sim</span><span class="sxs-lookup"><span data-stu-id="2c98c-171">Yes</span></span> |<span data-ttu-id="2c98c-172">Lista separada por vírgulas de categorias de eventos que devem ser coletados.</span><span class="sxs-lookup"><span data-stu-id="2c98c-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="2c98c-173">Os valores possíveis são Gravação, Exclusão e Ação.</span><span class="sxs-lookup"><span data-stu-id="2c98c-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="2c98c-174">Esquema de armazenamento do Log de Atividades</span><span class="sxs-lookup"><span data-stu-id="2c98c-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="2c98c-175">Depois de você configurar arquivamento, um contêiner de armazenamento será criado na conta de armazenamento assim que ocorrer um evento de Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="2c98c-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="2c98c-176">Os blobs no contêiner seguem o mesmo formato em todos os Logs de Diagnóstico e no Log de Atividades.</span><span class="sxs-lookup"><span data-stu-id="2c98c-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="2c98c-177">A estrutura desses blobs é:</span><span class="sxs-lookup"><span data-stu-id="2c98c-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="2c98c-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID da assinatura}/y={ano de quatro dígitos}/m={mês numérico de dois dígitos}/d={dia numérico de dois dígitos}/h={hora de relógio de 24 horas de dois dígitos}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2c98c-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2c98c-179">Por exemplo, um nome de blob poderia ser:</span><span class="sxs-lookup"><span data-stu-id="2c98c-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="2c98c-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2c98c-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2c98c-181">Cada blob PT1H.json contém um blob JSON de eventos que ocorreram dentro de uma hora especificada na URL do blob (por exemplo, h=12).</span><span class="sxs-lookup"><span data-stu-id="2c98c-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="2c98c-182">Durante a hora presente, os eventos são acrescentados ao arquivo PT1H.json conforme eles ocorrem.</span><span class="sxs-lookup"><span data-stu-id="2c98c-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="2c98c-183">O valor de minuto (m=00) é sempre 00, como eventos de Log de Atividades são divididos em blobs individuais por hora.</span><span class="sxs-lookup"><span data-stu-id="2c98c-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="2c98c-184">No arquivo PT1H.json, cada evento é armazenado na matriz de "registros", seguindo este formato:</span><span class="sxs-lookup"><span data-stu-id="2c98c-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="2c98c-185">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="2c98c-185">Element name</span></span> | <span data-ttu-id="2c98c-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="2c98c-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c98c-187">tempo real</span><span class="sxs-lookup"><span data-stu-id="2c98c-187">time</span></span> |<span data-ttu-id="2c98c-188">Carimbo de hora quando o evento foi gerado pelo serviço do Azure que está processando a solicitação correspondente ao evento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="2c98c-189">ResourceId</span><span class="sxs-lookup"><span data-stu-id="2c98c-189">resourceId</span></span> |<span data-ttu-id="2c98c-190">ID de recurso do recurso afetado.</span><span class="sxs-lookup"><span data-stu-id="2c98c-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="2c98c-191">operationName</span><span class="sxs-lookup"><span data-stu-id="2c98c-191">operationName</span></span> |<span data-ttu-id="2c98c-192">Nome da operação.</span><span class="sxs-lookup"><span data-stu-id="2c98c-192">Name of the operation.</span></span> |
| <span data-ttu-id="2c98c-193">categoria</span><span class="sxs-lookup"><span data-stu-id="2c98c-193">category</span></span> |<span data-ttu-id="2c98c-194">Categoria da ação, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="2c98c-194">Category of the action, eg.</span></span> <span data-ttu-id="2c98c-195">Gravação, Leitura e Ação.</span><span class="sxs-lookup"><span data-stu-id="2c98c-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="2c98c-196">resultType</span><span class="sxs-lookup"><span data-stu-id="2c98c-196">resultType</span></span> |<span data-ttu-id="2c98c-197">O tipo do resultado, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="2c98c-197">The type of the result, eg.</span></span> <span data-ttu-id="2c98c-198">Êxito, Falha e Início</span><span class="sxs-lookup"><span data-stu-id="2c98c-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="2c98c-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="2c98c-199">resultSignature</span></span> |<span data-ttu-id="2c98c-200">Depende do tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="2c98c-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="2c98c-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="2c98c-201">durationMs</span></span> |<span data-ttu-id="2c98c-202">Duração da operação em milissegundos</span><span class="sxs-lookup"><span data-stu-id="2c98c-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="2c98c-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="2c98c-203">callerIpAddress</span></span> |<span data-ttu-id="2c98c-204">Endereço IP do usuário que realizou a operação, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2c98c-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="2c98c-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="2c98c-205">correlationId</span></span> |<span data-ttu-id="2c98c-206">Geralmente, um GUID no formato de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2c98c-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="2c98c-207">Os eventos que compartilham um correlationId pertencem à mesma ação superior.</span><span class="sxs-lookup"><span data-stu-id="2c98c-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="2c98c-208">identidade</span><span class="sxs-lookup"><span data-stu-id="2c98c-208">identity</span></span> |<span data-ttu-id="2c98c-209">Blob JSON que descreve a autorização e as declarações.</span><span class="sxs-lookup"><span data-stu-id="2c98c-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="2c98c-210">authorization</span><span class="sxs-lookup"><span data-stu-id="2c98c-210">authorization</span></span> |<span data-ttu-id="2c98c-211">Blob de propriedades RBAC do evento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="2c98c-212">Geralmente, inclui as propriedades "action", "role" e "scope".</span><span class="sxs-lookup"><span data-stu-id="2c98c-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="2c98c-213">level</span><span class="sxs-lookup"><span data-stu-id="2c98c-213">level</span></span> |<span data-ttu-id="2c98c-214">Nível do evento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-214">Level of the event.</span></span> <span data-ttu-id="2c98c-215">Um dos seguintes valores: “Crítico”, “Erro”, “Aviso”, “Informativo” e “Detalhado”</span><span class="sxs-lookup"><span data-stu-id="2c98c-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="2c98c-216">location</span><span class="sxs-lookup"><span data-stu-id="2c98c-216">location</span></span> |<span data-ttu-id="2c98c-217">Região na qual ocorreu o local (ou global).</span><span class="sxs-lookup"><span data-stu-id="2c98c-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="2c98c-218">propriedades</span><span class="sxs-lookup"><span data-stu-id="2c98c-218">properties</span></span> |<span data-ttu-id="2c98c-219">Conjunto de pares de `<Key, Value>` (ou seja, Dicionário) que descreve os detalhes do evento.</span><span class="sxs-lookup"><span data-stu-id="2c98c-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="2c98c-220">As propriedades e o uso dessas propriedades podem variar dependendo do recurso.</span><span class="sxs-lookup"><span data-stu-id="2c98c-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2c98c-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c98c-221">Next steps</span></span>
* [<span data-ttu-id="2c98c-222">Baixar blobs para análise</span><span class="sxs-lookup"><span data-stu-id="2c98c-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="2c98c-223">Transmitir o Log de Atividades para os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2c98c-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="2c98c-224">Leia mais sobre o Log de Atividades</span><span class="sxs-lookup"><span data-stu-id="2c98c-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)

