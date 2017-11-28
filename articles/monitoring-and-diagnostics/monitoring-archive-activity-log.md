---
title: "Olá aaaArchive Log de atividades do Azure | Microsoft Docs"
description: "Saiba como tooarchive sua atividade do Azure Log para retenção de longo prazo em uma conta de armazenamento."
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
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a><span data-ttu-id="83808-103">Olá arquivar o Log de atividades do Azure</span><span class="sxs-lookup"><span data-stu-id="83808-103">Archive hello Azure Activity Log</span></span>
<span data-ttu-id="83808-104">Neste artigo, mostramos como você pode usar o hello portal do Azure, Cmdlets do PowerShell ou CLI de plataforma cruzada tooarchive seu [ **o Log de atividades do Azure** ](monitoring-overview-activity-logs.md) em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="83808-104">In this article, we show how you can use hello Azure portal, PowerShell Cmdlets, or Cross-Platform CLI tooarchive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="83808-105">Essa opção é útil se você quiser tooretain mais de 90 dias (com controle total sobre a política de retenção Olá) para o Log de atividades de auditoria, análise estática, ou de backup.</span><span class="sxs-lookup"><span data-stu-id="83808-105">This option is useful if you would like tooretain your Activity Log longer than 90 days (with full control over hello retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="83808-106">Se você precisar somente tooretain seus eventos por 90 dias ou menos que você não é necessário tooset tooa arquivamento conta de armazenamento, desde que os eventos de Log de atividades são mantidos no hello plataforma Windows Azure por 90 dias sem habilitar arquivamento.</span><span class="sxs-lookup"><span data-stu-id="83808-106">If you only need tooretain your events for 90 days or less you do not need tooset up archival tooa storage account, since Activity Log events are retained in hello Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83808-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83808-107">Prerequisites</span></span>
<span data-ttu-id="83808-108">Antes de começar, é preciso muito[criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich poderá arquivar o Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="83808-108">Before you begin, you need too[create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich you can archive your Activity Log.</span></span> <span data-ttu-id="83808-109">É altamente recomendável que você não use uma conta de armazenamento existente que tenha outros monitoramento não dados armazenados nela, para que você pode controlar melhor acesso toomonitoring dados.</span><span class="sxs-lookup"><span data-stu-id="83808-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access toomonitoring data.</span></span> <span data-ttu-id="83808-110">No entanto, se você também estiver arquivando Logs de diagnóstico e a conta de armazenamento tooa métricas, talvez faça sentido toouse essa conta de armazenamento para a atividade de Log também tookeep todos os dados de monitoramento em um local central.</span><span class="sxs-lookup"><span data-stu-id="83808-110">However, if you are also archiving Diagnostic Logs and metrics tooa storage account, it may make sense toouse that storage account for your Activity Log as well tookeep all monitoring data in a central location.</span></span> <span data-ttu-id="83808-111">conta de armazenamento Olá usada deve ser uma conta de armazenamento de propósito geral, não uma conta de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="83808-111">hello storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="83808-112">conta de armazenamento Olá não tem toobe Olá mesma assinatura que Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.</span><span class="sxs-lookup"><span data-stu-id="83808-112">hello storage account does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="83808-113">Perfil de Log</span><span class="sxs-lookup"><span data-stu-id="83808-113">Log Profile</span></span>
<span data-ttu-id="83808-114">Olá tooarchive Log de atividades, usando qualquer um dos métodos de saudação abaixo, você definir Olá **Log perfil** para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="83808-114">tooarchive hello Activity Log using any of hello methods below, you set hello **Log Profile** for a subscription.</span></span> <span data-ttu-id="83808-115">Olá Log perfil define o tipo de saudação de eventos que são armazenadas ou transmitidas e Olá saídas — hub de conta e/ou evento de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="83808-115">hello Log Profile defines hello type of events that are stored or streamed and hello outputs—storage account and/or event hub.</span></span> <span data-ttu-id="83808-116">Ele também define a política de retenção de saudação (número de dias tooretain) para eventos armazenados em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="83808-116">It also defines hello retention policy (number of days tooretain) for events stored in a storage account.</span></span> <span data-ttu-id="83808-117">Se toozero é definir a política de retenção de hello, eventos são armazenados indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="83808-117">If hello retention policy is set toozero, events are stored indefinitely.</span></span> <span data-ttu-id="83808-118">Caso contrário, isso pode ser definido tooany valor entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="83808-118">Otherwise, this can be set tooany value between 1 and 2147483647.</span></span> <span data-ttu-id="83808-119">Políticas de retenção são aplicadas por dia, para em Olá final de um dia (UTC), logs do dia Olá que agora está além da política de retenção hello serão excluídas.</span><span class="sxs-lookup"><span data-stu-id="83808-119">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy will be deleted.</span></span> <span data-ttu-id="83808-120">Por exemplo, se você tiver uma política de retenção de um dia, no início de saudação do dia Olá hoje hello logs de anteontem Olá seriam excluídas.</span><span class="sxs-lookup"><span data-stu-id="83808-120">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span> <span data-ttu-id="83808-121">[Você pode ler mais sobre perfis de log aqui](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span><span class="sxs-lookup"><span data-stu-id="83808-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile).</span></span> 

## <a name="archive-hello-activity-log-using-hello-portal"></a><span data-ttu-id="83808-122">Arquivo hello usando o portal de saudação do Log de atividades</span><span class="sxs-lookup"><span data-stu-id="83808-122">Archive hello Activity Log using hello portal</span></span>
1. <span data-ttu-id="83808-123">No portal de saudação, clique em Olá **Log de atividades** link de navegação do lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="83808-123">In hello portal, click hello **Activity Log** link on hello left-side navigation.</span></span> <span data-ttu-id="83808-124">Se você não vir um link para Olá Log de atividades, clique em Olá **mais serviços** link primeiro.</span><span class="sxs-lookup"><span data-stu-id="83808-124">If you don’t see a link for hello Activity Log, click hello **More Services** link first.</span></span>
   
    ![Navegue tooActivity folha de Log](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="83808-126">Na parte superior de saudação da folha de saudação, clique em **exportar**.</span><span class="sxs-lookup"><span data-stu-id="83808-126">At hello top of hello blade, click **Export**.</span></span>
   
    ![Botão de exportação Olá](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="83808-128">Na folha de saudação que aparece, marque a caixa de saudação do **exportar a conta de armazenamento tooa** e selecione uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="83808-128">In hello blade that appears, check hello box for **Export tooa storage account** and select a storage account.</span></span>
   
    ![De uma conta de armazenamento](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="83808-130">Usando o controle deslizante de saudação ou caixa de texto, defina um número de dias que os eventos de Log de atividades devem ser mantidos na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="83808-130">Using hello slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="83808-131">Se você preferir toohave seus dados persistentes na conta de armazenamento Olá indefinidamente, defina este número toozero.</span><span class="sxs-lookup"><span data-stu-id="83808-131">If you prefer toohave your data persisted in hello storage account indefinitely, set this number toozero.</span></span>
5. <span data-ttu-id="83808-132">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="83808-132">Click **Save**.</span></span>

## <a name="archive-hello-activity-log-via-powershell"></a><span data-ttu-id="83808-133">Olá arquivar o Log de atividades por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="83808-133">Archive hello Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="83808-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="83808-134">Property</span></span> | <span data-ttu-id="83808-135">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="83808-135">Required</span></span> | <span data-ttu-id="83808-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="83808-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83808-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="83808-137">StorageAccountId</span></span> |<span data-ttu-id="83808-138">Não</span><span class="sxs-lookup"><span data-stu-id="83808-138">No</span></span> |<span data-ttu-id="83808-139">ID do recurso de toowhich de conta de armazenamento Olá Logs de atividade deve ser salvo.</span><span class="sxs-lookup"><span data-stu-id="83808-139">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="83808-140">Locais</span><span class="sxs-lookup"><span data-stu-id="83808-140">Locations</span></span> |<span data-ttu-id="83808-141">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-141">Yes</span></span> |<span data-ttu-id="83808-142">Lista separada por vírgulas de regiões para o qual você gostaria que os eventos de Log de atividades de toocollect.</span><span class="sxs-lookup"><span data-stu-id="83808-142">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="83808-143">Você pode exibir uma lista de todas as regiões [visitando esta página](https://azure.microsoft.com/en-us/regions) ou usando [Olá API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="83808-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="83808-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="83808-144">RetentionInDays</span></span> |<span data-ttu-id="83808-145">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-145">Yes</span></span> |<span data-ttu-id="83808-146">Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="83808-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="83808-147">Um valor de zero armazena logs Olá indefinidamente (sempre).</span><span class="sxs-lookup"><span data-stu-id="83808-147">A value of zero stores hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="83808-148">Categorias</span><span class="sxs-lookup"><span data-stu-id="83808-148">Categories</span></span> |<span data-ttu-id="83808-149">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-149">Yes</span></span> |<span data-ttu-id="83808-150">Lista separada por vírgulas de categorias de eventos que devem ser coletados.</span><span class="sxs-lookup"><span data-stu-id="83808-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="83808-151">Os valores possíveis são Gravação, Exclusão e Ação.</span><span class="sxs-lookup"><span data-stu-id="83808-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-hello-activity-log-via-cli"></a><span data-ttu-id="83808-152">Olá arquivar o Log de atividade via CLI</span><span class="sxs-lookup"><span data-stu-id="83808-152">Archive hello Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="83808-153">Propriedade</span><span class="sxs-lookup"><span data-stu-id="83808-153">Property</span></span> | <span data-ttu-id="83808-154">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="83808-154">Required</span></span> | <span data-ttu-id="83808-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="83808-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83808-156">name</span><span class="sxs-lookup"><span data-stu-id="83808-156">name</span></span> |<span data-ttu-id="83808-157">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-157">Yes</span></span> |<span data-ttu-id="83808-158">Nome de seu perfil de log.</span><span class="sxs-lookup"><span data-stu-id="83808-158">Name of your log profile.</span></span> |
| <span data-ttu-id="83808-159">storageId</span><span class="sxs-lookup"><span data-stu-id="83808-159">storageId</span></span> |<span data-ttu-id="83808-160">Não</span><span class="sxs-lookup"><span data-stu-id="83808-160">No</span></span> |<span data-ttu-id="83808-161">ID do recurso de toowhich de conta de armazenamento Olá Logs de atividade deve ser salvo.</span><span class="sxs-lookup"><span data-stu-id="83808-161">Resource ID of hello Storage Account toowhich Activity Logs should be saved.</span></span> |
| <span data-ttu-id="83808-162">locais</span><span class="sxs-lookup"><span data-stu-id="83808-162">locations</span></span> |<span data-ttu-id="83808-163">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-163">Yes</span></span> |<span data-ttu-id="83808-164">Lista separada por vírgulas de regiões para o qual você gostaria que os eventos de Log de atividades de toocollect.</span><span class="sxs-lookup"><span data-stu-id="83808-164">Comma-separated list of regions for which you would like toocollect Activity Log events.</span></span> <span data-ttu-id="83808-165">Você pode exibir uma lista de todas as regiões [visitando esta página](https://azure.microsoft.com/en-us/regions) ou usando [Olá API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="83808-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [hello Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="83808-166">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="83808-166">retentionInDays</span></span> |<span data-ttu-id="83808-167">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-167">Yes</span></span> |<span data-ttu-id="83808-168">Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="83808-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="83808-169">Um valor de zero armazenará logs Olá indefinidamente (sempre).</span><span class="sxs-lookup"><span data-stu-id="83808-169">A value of zero will store hello logs indefinitely (forever).</span></span> |
| <span data-ttu-id="83808-170">Categorias</span><span class="sxs-lookup"><span data-stu-id="83808-170">categories</span></span> |<span data-ttu-id="83808-171">Sim</span><span class="sxs-lookup"><span data-stu-id="83808-171">Yes</span></span> |<span data-ttu-id="83808-172">Lista separada por vírgulas de categorias de eventos que devem ser coletados.</span><span class="sxs-lookup"><span data-stu-id="83808-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="83808-173">Os valores possíveis são Gravação, Exclusão e Ação.</span><span class="sxs-lookup"><span data-stu-id="83808-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-hello-activity-log"></a><span data-ttu-id="83808-174">Esquema de armazenamento de Log de atividades de hello</span><span class="sxs-lookup"><span data-stu-id="83808-174">Storage schema of hello Activity Log</span></span>
<span data-ttu-id="83808-175">Depois que você configurar arquivamento, um contêiner de armazenamento será criado na conta de armazenamento hello, assim como ocorre um evento de Log de atividades.</span><span class="sxs-lookup"><span data-stu-id="83808-175">Once you have set up archival, a storage container will be created in hello storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="83808-176">blobs Hello dentro do contêiner de saudação siga Olá mesmo formato em hello atividade de Log e Logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="83808-176">hello blobs within hello container follow hello same format across hello Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="83808-177">estrutura Olá esses blobs é:</span><span class="sxs-lookup"><span data-stu-id="83808-177">hello structure of these blobs is:</span></span>

> <span data-ttu-id="83808-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID da assinatura}/y={ano de quatro dígitos}/m={mês numérico de dois dígitos}/d={dia numérico de dois dígitos}/h={hora de relógio de 24 horas de dois dígitos}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="83808-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="83808-179">Por exemplo, um nome de blob poderia ser:</span><span class="sxs-lookup"><span data-stu-id="83808-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="83808-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="83808-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="83808-181">Cada blob PT1H.json contém um blob JSON de eventos que ocorreram na hora de saudação especificada na URL de blob de saudação (por exemplo, h = 12).</span><span class="sxs-lookup"><span data-stu-id="83808-181">Each PT1H.json blob contains a JSON blob of events that occurred within hello hour specified in hello blob URL (e.g. h=12).</span></span> <span data-ttu-id="83808-182">Durante a saudação hora presente, os eventos são acrescentadas toohello PT1H.json arquivo conforme elas ocorrem.</span><span class="sxs-lookup"><span data-stu-id="83808-182">During hello present hour, events are appended toohello PT1H.json file as they occur.</span></span> <span data-ttu-id="83808-183">Olá valor de minuto (m = 00) é sempre 00, desde que os eventos de Log de atividades são divididos em blobs individuais por hora.</span><span class="sxs-lookup"><span data-stu-id="83808-183">hello minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="83808-184">No arquivo de PT1H.json hello, cada evento é armazenado na matriz de registros"hello", neste formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="83808-184">Within hello PT1H.json file, each event is stored in hello “records” array, following this format:</span></span>

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


| <span data-ttu-id="83808-185">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="83808-185">Element name</span></span> | <span data-ttu-id="83808-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="83808-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83808-187">tempo real</span><span class="sxs-lookup"><span data-stu-id="83808-187">time</span></span> |<span data-ttu-id="83808-188">Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="83808-188">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="83808-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="83808-189">resourceId</span></span> |<span data-ttu-id="83808-190">ID do recurso da saudação afetados recursos.</span><span class="sxs-lookup"><span data-stu-id="83808-190">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="83808-191">operationName</span><span class="sxs-lookup"><span data-stu-id="83808-191">operationName</span></span> |<span data-ttu-id="83808-192">Nome da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="83808-192">Name of hello operation.</span></span> |
| <span data-ttu-id="83808-193">categoria</span><span class="sxs-lookup"><span data-stu-id="83808-193">category</span></span> |<span data-ttu-id="83808-194">Categoria de ação hello, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="83808-194">Category of hello action, eg.</span></span> <span data-ttu-id="83808-195">Gravação, Leitura e Ação.</span><span class="sxs-lookup"><span data-stu-id="83808-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="83808-196">resultType</span><span class="sxs-lookup"><span data-stu-id="83808-196">resultType</span></span> |<span data-ttu-id="83808-197">Olá tipo de resultado hello, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="83808-197">hello type of hello result, eg.</span></span> <span data-ttu-id="83808-198">Êxito, Falha e Início</span><span class="sxs-lookup"><span data-stu-id="83808-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="83808-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="83808-199">resultSignature</span></span> |<span data-ttu-id="83808-200">Depende do tipo de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="83808-200">Depends on hello resource type.</span></span> |
| <span data-ttu-id="83808-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="83808-201">durationMs</span></span> |<span data-ttu-id="83808-202">Duração da operação de saudação em milissegundos</span><span class="sxs-lookup"><span data-stu-id="83808-202">Duration of hello operation in milliseconds</span></span> |
| <span data-ttu-id="83808-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="83808-203">callerIpAddress</span></span> |<span data-ttu-id="83808-204">Endereço IP do usuário de saudação que executou a operação de hello, declaração UPN ou declaração SPN com base na disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="83808-204">IP address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="83808-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="83808-205">correlationId</span></span> |<span data-ttu-id="83808-206">Normalmente um GUID no formato de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="83808-206">Usually a GUID in hello string format.</span></span> <span data-ttu-id="83808-207">Os eventos que compartilham um correlationId pertencem toohello mesma ação uber.</span><span class="sxs-lookup"><span data-stu-id="83808-207">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="83808-208">identidade</span><span class="sxs-lookup"><span data-stu-id="83808-208">identity</span></span> |<span data-ttu-id="83808-209">Blob JSON que descreve a declarações e autorização hello.</span><span class="sxs-lookup"><span data-stu-id="83808-209">JSON blob describing hello authorization and claims.</span></span> |
| <span data-ttu-id="83808-210">autorização</span><span class="sxs-lookup"><span data-stu-id="83808-210">authorization</span></span> |<span data-ttu-id="83808-211">Blob de propriedades RBAC do evento hello.</span><span class="sxs-lookup"><span data-stu-id="83808-211">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="83808-212">Geralmente inclui propriedades de "ação", "função" e "escopo" hello.</span><span class="sxs-lookup"><span data-stu-id="83808-212">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="83808-213">level</span><span class="sxs-lookup"><span data-stu-id="83808-213">level</span></span> |<span data-ttu-id="83808-214">Nível de evento hello.</span><span class="sxs-lookup"><span data-stu-id="83808-214">Level of hello event.</span></span> <span data-ttu-id="83808-215">Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"</span><span class="sxs-lookup"><span data-stu-id="83808-215">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="83808-216">location</span><span class="sxs-lookup"><span data-stu-id="83808-216">location</span></span> |<span data-ttu-id="83808-217">Região na qual local Olá ocorreu (ou global).</span><span class="sxs-lookup"><span data-stu-id="83808-217">Region in which hello location occurred (or global).</span></span> |
| <span data-ttu-id="83808-218">propriedades</span><span class="sxs-lookup"><span data-stu-id="83808-218">properties</span></span> |<span data-ttu-id="83808-219">Conjunto de `<Key, Value>` pares (ou seja, o dicionário) que descreve os detalhes de saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="83808-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing hello details of hello event.</span></span> |

> [!NOTE]
> <span data-ttu-id="83808-220">Propriedades de saudação e o uso dessas propriedades podem variar dependendo de recurso hello.</span><span class="sxs-lookup"><span data-stu-id="83808-220">hello properties and usage of those properties can vary depending on hello resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83808-221">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83808-221">Next steps</span></span>
* [<span data-ttu-id="83808-222">Baixar blobs para análise</span><span class="sxs-lookup"><span data-stu-id="83808-222">Download blobs for analysis</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="83808-223">Fluxo de tooEvent do Log de atividades de saudação Hubs</span><span class="sxs-lookup"><span data-stu-id="83808-223">Stream hello Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="83808-224">Leia mais sobre Olá Log de atividades</span><span class="sxs-lookup"><span data-stu-id="83808-224">Read more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)

