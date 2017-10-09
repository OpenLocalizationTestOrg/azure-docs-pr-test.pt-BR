---
title: "aaaOverview dos Logs de diagnóstico do Azure | Microsoft Docs"
description: "Saiba quais são os logs de diagnósticos do Azure e como você pode usá-los toounderstand eventos que ocorrem dentro de um recurso do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="03fb2-103">Coletar e consumir dados de log dos recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="03fb2-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="03fb2-104">O que são os logs de diagnóstico de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="03fb2-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="03fb2-105">**Logs de diagnóstico do Azure de nível de recurso** logs emitido por um recurso que fornecem dados ricos, frequentes sobre a operação de saudação do recurso.</span><span class="sxs-lookup"><span data-stu-id="03fb2-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="03fb2-106">conteúdo de saudação desses logs varia por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="03fb2-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="03fb2-107">Por exemplo, os contadores de regra do Grupo de Segurança de Rede e as auditorias do Key Vault são duas categorias de logs de recursos.</span><span class="sxs-lookup"><span data-stu-id="03fb2-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="03fb2-108">Logs de diagnóstico do nível de recursos diferem das Olá [Log de atividades](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="03fb2-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="03fb2-109">Olá Log de atividades fornece informações sobre operações Olá que foram executadas em recursos em sua assinatura usando o Gerenciador de recursos, por exemplo, criar uma máquina virtual ou a exclusão de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="03fb2-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="03fb2-110">Hello atividade de Log é um log de nível de assinatura.</span><span class="sxs-lookup"><span data-stu-id="03fb2-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="03fb2-111">Os logs de diagnóstico no nível do recurso fornecem informações sobre as operações executadas dentro do próprio recurso, por exemplo, obtenção de um segredo de um Key Vault.</span><span class="sxs-lookup"><span data-stu-id="03fb2-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="03fb2-112">Os logs de diagnóstico no nível do recurso também diferem dos logs de diagnóstico no nível do sistema operacional convidado.</span><span class="sxs-lookup"><span data-stu-id="03fb2-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="03fb2-113">Os logs de diagnóstico do sistema operacional convidado são aqueles coletados por um agente em execução dentro de uma máquina virtual ou outro tipo de recurso com suporte.</span><span class="sxs-lookup"><span data-stu-id="03fb2-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="03fb2-114">Logs de diagnóstico do nível de recursos exigem que os dados de recursos específicos sem agente e a captura de saudação plataforma Windows Azure, enquanto os logs de diagnóstico de nível de sistema operacional convidado capturam dados de sistema de operacional hello e aplicativos em execução em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03fb2-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="03fb2-115">Nem todos os recursos oferecem suporte a saudação novo tipo de logs de diagnóstico recursos descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="03fb2-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="03fb2-116">Este artigo contém uma lista de seção quais tipos de recursos oferecer suporte a novos logs de diagnóstico nível do recurso hello.</span><span class="sxs-lookup"><span data-stu-id="03fb2-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="03fb2-117">Logs de diagnóstico do recurso versus outros tipos de logs</span><span class="sxs-lookup"><span data-stu-id="03fb2-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="03fb2-118">O que você pode fazer com os logs de diagnóstico no nível do recurso</span><span class="sxs-lookup"><span data-stu-id="03fb2-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="03fb2-119">Aqui estão algumas das coisas Olá que você pode fazer com os logs de diagnóstico de recursos:</span><span class="sxs-lookup"><span data-stu-id="03fb2-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Posicionamento lógico dos Logs de Diagnóstico de recurso](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="03fb2-121">Salvá-las tooa [ **conta de armazenamento** ](monitoring-archive-diagnostic-logs.md) para inspeção de auditoria ou manual.</span><span class="sxs-lookup"><span data-stu-id="03fb2-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="03fb2-122">Você pode especificar Olá retenção tempo (em dias) usando **configurações de diagnóstico de recurso**.</span><span class="sxs-lookup"><span data-stu-id="03fb2-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="03fb2-123">[Transmiti-los muito**Hubs de eventos** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) para ingestão por um serviço de terceiros ou a solução de análise personalizado, como o Power BI.</span><span class="sxs-lookup"><span data-stu-id="03fb2-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="03fb2-124">Analise-os com o [Log Analytics do OMS](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="03fb2-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="03fb2-125">Você pode usar uma conta de armazenamento ou o namespace de Hubs de eventos que não está em Olá mesma assinatura conforme Olá um emissor logs.</span><span class="sxs-lookup"><span data-stu-id="03fb2-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="03fb2-126">usuário de saudação que configura a configuração de saudação deve ter assinaturas do hello apropriadas RBAC acesso tooboth.</span><span class="sxs-lookup"><span data-stu-id="03fb2-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="03fb2-127">Configurações do Diagnóstico do recurso</span><span class="sxs-lookup"><span data-stu-id="03fb2-127">Resource diagnostic settings</span></span>
<span data-ttu-id="03fb2-128">Os logs de diagnóstico do recurso para os recursos que não são de computação são configurados usando as configurações de diagnóstico do recurso.</span><span class="sxs-lookup"><span data-stu-id="03fb2-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="03fb2-129">**Configurações de Diagnóstico do Recurso** para um controle de recursos:</span><span class="sxs-lookup"><span data-stu-id="03fb2-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="03fb2-130">Para onde os logs de diagnóstico e as métricas do recurso são enviados (Conta de Armazenamento, Hubs de Eventos e/ou Log Analytics do OMS).</span><span class="sxs-lookup"><span data-stu-id="03fb2-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="03fb2-131">Quais categorias de log são enviadas e se os dados de métrica também são enviados.</span><span class="sxs-lookup"><span data-stu-id="03fb2-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="03fb2-132">Quanto tempo cada categoria de log deve ser mantida em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="03fb2-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="03fb2-133">Uma retenção de zero dias significa que os registros serão mantidos indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="03fb2-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="03fb2-134">Caso contrário, o valor de saudação pode ser qualquer número de dias entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="03fb2-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="03fb2-135">Se as políticas de retenção são definidas, mas o armazenamento de logs em uma conta de armazenamento está desabilitado (por exemplo, se apenas as opções de Hubs de eventos ou do OMS são selecionadas), políticas de retenção de saudação não têm efeito.</span><span class="sxs-lookup"><span data-stu-id="03fb2-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="03fb2-136">Políticas de retenção são aplicadas por dia, para em Olá final de um dia (UTC), logs de dia de saudação que agora está além da política de retenção de saudação são excluídos.</span><span class="sxs-lookup"><span data-stu-id="03fb2-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="03fb2-137">Por exemplo, se você tiver uma política de retenção de um dia, no início de saudação do dia Olá hoje hello logs de anteontem Olá seriam excluídas.</span><span class="sxs-lookup"><span data-stu-id="03fb2-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="03fb2-138">Essas configurações são definidas facilmente por meio de configurações de diagnóstico Olá para um recurso em Olá portal do Azure, por meio de comandos do PowerShell do Azure e a CLI ou Olá [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="03fb2-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="03fb2-139">Logs de diagnóstico e métricas da camada de sistema operacional convidado Olá de uso de recursos (por exemplo, máquinas virtuais ou malha do serviço) de computação [um mecanismo separado para configuração e seleção de saídas](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03fb2-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="03fb2-140">Como coleção tooenable dos logs de diagnóstico de recurso</span><span class="sxs-lookup"><span data-stu-id="03fb2-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="03fb2-141">Coleta de logs de diagnóstico de recursos podem ser habilitadas [como parte da criação de um recurso em um modelo do Gerenciador de recursos](./monitoring-enable-diagnostic-logs-using-template.md) ou depois que um recurso é criado na página desse recurso no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="03fb2-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="03fb2-142">Você também pode habilitar a coleção a qualquer momento usando comandos do Azure PowerShell ou CLI ou Olá API de REST do Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="03fb2-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="03fb2-143">Essas instruções podem não se aplicam diretamente tooevery recursos.</span><span class="sxs-lookup"><span data-stu-id="03fb2-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="03fb2-144">Consulte Olá esquema links na parte inferior de saudação dessa página toounderstand especiais as etapas que podem ser aplicadas a tipos de recurso toocertain.</span><span class="sxs-lookup"><span data-stu-id="03fb2-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="03fb2-145">Habilitar a coleta de logs de diagnóstico de recursos no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="03fb2-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="03fb2-146">Você pode habilitar a coleta de logs de diagnóstico de recurso no hello Azure portal depois que um recurso foi criado pelo recurso específico tooa vai ou navegando tooAzure Monitor.</span><span class="sxs-lookup"><span data-stu-id="03fb2-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="03fb2-147">tooenable isso por meio do Monitor do Azure:</span><span class="sxs-lookup"><span data-stu-id="03fb2-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="03fb2-148">Em Olá [portal do Azure](http://portal.azure.com), navegar tooAzure Monitor e clique em **configurações de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="03fb2-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Seção de monitoramento do Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="03fb2-150">Se desejar filtrar lista Olá por tipo de recurso ou grupo de recursos, clique no recurso Olá para o qual você gostaria que tooset uma configuração de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="03fb2-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="03fb2-151">Se nenhuma configuração existir no recurso de saudação selecionado, você está toocreate solicitada uma configuração.</span><span class="sxs-lookup"><span data-stu-id="03fb2-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="03fb2-152">Clique em “Ativar diagnóstico”.</span><span class="sxs-lookup"><span data-stu-id="03fb2-152">Click "Turn on diagnostics."</span></span>

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="03fb2-154">Se houver configurações existentes no recurso hello, você verá uma lista de configurações já configurado nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="03fb2-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="03fb2-155">Clique em "Adicionar configuração de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="03fb2-155">Click "Add diagnostic setting."</span></span>

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="03fb2-157">Dê sua configuração para um nome, caixas de saudação de seleção para cada toowhich de destino que você deseja toosend dados e configurar o recurso que será usado para cada destino.</span><span class="sxs-lookup"><span data-stu-id="03fb2-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="03fb2-158">Opcionalmente, defina um número de dias tooretain esses logs usando Olá **retenção (dias)** controles deslizantes (somente aplicável toohello conta destino de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="03fb2-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="03fb2-159">Uma retenção de zero dias armazena logs Olá indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="03fb2-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="03fb2-161">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="03fb2-161">Click **Save**.</span></span>

<span data-ttu-id="03fb2-162">Após alguns instantes, Olá nova configuração é exibida na sua lista de configurações para esse recurso e logs de diagnóstico são enviados toohello especificado destinos assim que novos dados de evento são gerados.</span><span class="sxs-lookup"><span data-stu-id="03fb2-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="03fb2-163">Habilitar a coleção de logs de diagnóstico de recurso via PowerShell</span><span class="sxs-lookup"><span data-stu-id="03fb2-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="03fb2-164">coleção de tooenable dos logs de diagnóstico de recursos por meio do PowerShell do Azure, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="03fb2-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="03fb2-165">armazenamento de tooenable dos logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="03fb2-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="03fb2-166">armazenamento Olá ID da conta é Olá ID de recurso para toowhich de conta de armazenamento Olá deseja toosend Olá logs.</span><span class="sxs-lookup"><span data-stu-id="03fb2-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="03fb2-167">tooenable streaming de hub de eventos de tooan de logs de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="03fb2-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="03fb2-168">Olá ID da regra de barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="03fb2-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="03fb2-169">Enviar tooenable do espaço de trabalho de análise de Log de tooa logs de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="03fb2-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="03fb2-170">Você pode obter a ID de recurso de saudação do seu espaço de trabalho de análise de Log usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="03fb2-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="03fb2-171">Você pode combinar várias opções de saída para tooenable esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="03fb2-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="03fb2-172">Habilitar a coleção de logs de diagnóstico do recurso via CLI</span><span class="sxs-lookup"><span data-stu-id="03fb2-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="03fb2-173">coleção de tooenable dos logs de diagnóstico de recursos por meio de saudação CLI do Azure, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="03fb2-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="03fb2-174">armazenamento de tooenable dos logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="03fb2-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="03fb2-175">armazenamento Olá ID da conta é Olá ID de recurso para toowhich de conta de armazenamento Olá deseja toosend Olá logs.</span><span class="sxs-lookup"><span data-stu-id="03fb2-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="03fb2-176">tooenable streaming de hub de eventos de tooan de logs de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="03fb2-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="03fb2-177">Olá ID da regra de barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="03fb2-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="03fb2-178">Enviar tooenable do espaço de trabalho de análise de Log de tooa logs de diagnóstico, use este comando:</span><span class="sxs-lookup"><span data-stu-id="03fb2-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="03fb2-179">Você pode combinar várias opções de saída para tooenable esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="03fb2-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="03fb2-180">Habilitar a coleção de logs de diagnóstico do recurso via API REST</span><span class="sxs-lookup"><span data-stu-id="03fb2-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="03fb2-181">configurações de diagnóstico toochange usando Olá API de REST do Monitor do Azure, consulte [neste documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="03fb2-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="03fb2-182">Gerenciar configurações de diagnóstico de recursos no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="03fb2-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="03fb2-183">Verifique se todos os seus recursos estão definidos com as configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="03fb2-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="03fb2-184">Navegue muito**Monitor** em Olá portal e abra **configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="03fb2-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Folha de Logs de diagnóstico no portal de saudação](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="03fb2-186">Você pode ter tooclick seção de Monitor "Mais serviços" toofind hello.</span><span class="sxs-lookup"><span data-stu-id="03fb2-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="03fb2-187">Aqui você pode visualizar e filtrar todos os recursos que oferecem suporte a configurações de diagnóstico toosee se eles tiverem diagnóstico habilitado.</span><span class="sxs-lookup"><span data-stu-id="03fb2-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="03fb2-188">Você também pode fazer drill down toosee se várias configurações são definidas em um recurso e verificar qual conta de armazenamento, o namespace de Hubs de eventos e/ou espaço de trabalho de análise de Log que os dados estão fluindo para.</span><span class="sxs-lookup"><span data-stu-id="03fb2-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Resultados da folha Logs de Diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="03fb2-190">Adicionar que uma configuração de diagnóstica exibe Olá modo de exibição de configurações de diagnóstico, onde você pode habilitar, desabilitar ou modificar as configurações de diagnósticas para Olá selecionado recursos.</span><span class="sxs-lookup"><span data-stu-id="03fb2-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="03fb2-191">Serviços, categorias e esquemas com suporte para os logs de diagnóstico de recurso</span><span class="sxs-lookup"><span data-stu-id="03fb2-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="03fb2-192">[Consulte este artigo](monitoring-diagnostic-logs-schema.md) para obter uma lista de serviços com suporte e categorias de log hello e esquemas usados por esses serviços.</span><span class="sxs-lookup"><span data-stu-id="03fb2-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03fb2-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03fb2-193">Next steps</span></span>

* [<span data-ttu-id="03fb2-194">Logs de diagnóstico do recurso de fluxo muito**Hubs de eventos**</span><span class="sxs-lookup"><span data-stu-id="03fb2-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="03fb2-195">Alterar configurações de diagnóstico de recursos usando Olá API de REST do Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="03fb2-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="03fb2-196">Analisar logs do Armazenamento do Azure com o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="03fb2-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
