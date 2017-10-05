---
title: "Visão geral dos Logs de Diagnóstico do Azure | Microsoft Docs"
description: "Saiba quais são os logs de diagnóstico do Azure e como você pode usá-los para compreender os eventos que ocorrem dentro de um recurso do Azure."
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
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="d32c7-103">Coletar e consumir dados de log dos recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d32c7-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="d32c7-104">O que são os logs de diagnóstico de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d32c7-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="d32c7-105">**Os logs de diagnóstico no nível do recurso do Azure** são logs emitidos por um recurso que fornece dados avançados e frequentes sobre a operação do recurso.</span><span class="sxs-lookup"><span data-stu-id="d32c7-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="d32c7-106">O conteúdo desses logs varia de acordo com o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="d32c7-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="d32c7-107">Por exemplo, os contadores de regra do Grupo de Segurança de Rede e as auditorias do Key Vault são duas categorias de logs de recursos.</span><span class="sxs-lookup"><span data-stu-id="d32c7-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="d32c7-108">Os logs de diagnóstico no nível do recurso são diferentes do [Log de Atividades](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="d32c7-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="d32c7-109">O Log de Atividades fornece informações sobre as operações executadas em recursos em sua assinatura usando o Gerenciador de Recursos, por exemplo, criar uma máquina virtual ou excluir um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d32c7-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="d32c7-110">O Log de Atividades é um log no nível da assinatura.</span><span class="sxs-lookup"><span data-stu-id="d32c7-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="d32c7-111">Os logs de diagnóstico no nível do recurso fornecem informações sobre as operações executadas dentro do próprio recurso, por exemplo, obtenção de um segredo de um Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d32c7-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="d32c7-112">Os logs de diagnóstico no nível do recurso também diferem dos logs de diagnóstico no nível do sistema operacional convidado.</span><span class="sxs-lookup"><span data-stu-id="d32c7-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="d32c7-113">Os logs de diagnóstico do sistema operacional convidado são aqueles coletados por um agente em execução dentro de uma máquina virtual ou outro tipo de recurso com suporte.</span><span class="sxs-lookup"><span data-stu-id="d32c7-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="d32c7-114">Os logs de diagnóstico no nível do recurso não exigem um agente e capturam dados específicos ao recurso da própria plataforma do Azure, enquanto os logs de diagnóstico no nível do sistema operacional convidado capturam dados do sistema operacional e de aplicativos em execução em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d32c7-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="d32c7-115">Nem todos os recursos oferecem suporte ao novo tipo de logs de diagnóstico descritos aqui.</span><span class="sxs-lookup"><span data-stu-id="d32c7-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="d32c7-116">Este artigo contém uma seção que lista os tipos de recursos que dão suporte aos novos logs de diagnóstico no nível do recurso.</span><span class="sxs-lookup"><span data-stu-id="d32c7-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="d32c7-117">Logs de diagnóstico do recurso versus outros tipos de logs</span><span class="sxs-lookup"><span data-stu-id="d32c7-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="d32c7-118">O que você pode fazer com os logs de diagnóstico no nível do recurso</span><span class="sxs-lookup"><span data-stu-id="d32c7-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="d32c7-119">Aqui estão algumas coisas que você pode fazer com os logs de diagnóstico de recurso:</span><span class="sxs-lookup"><span data-stu-id="d32c7-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Posicionamento lógico dos Logs de Diagnóstico de recurso](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="d32c7-121">Salve-os em uma [**Conta de Armazenamento**](monitoring-archive-diagnostic-logs.md) para auditoria ou inspeção manual.</span><span class="sxs-lookup"><span data-stu-id="d32c7-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="d32c7-122">Você pode especificar o tempo de retenção (em dias) usando as **Configurações de Diagnóstico do Recurso**.</span><span class="sxs-lookup"><span data-stu-id="d32c7-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="d32c7-123">[Transmita-os para os **Hubs de Eventos**](monitoring-stream-diagnostic-logs-to-event-hubs.md) para o consumo por um serviço de terceiros ou uma solução de análises personalizadas, como o PowerBI.</span><span class="sxs-lookup"><span data-stu-id="d32c7-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="d32c7-124">Analise-os com o [Log Analytics do OMS](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d32c7-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="d32c7-125">Você pode usar uma conta de armazenamento ou um namespace de Hubs de Evento que não esteja na mesma assinatura que os logs emissores.</span><span class="sxs-lookup"><span data-stu-id="d32c7-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="d32c7-126">O usuário que define a configuração deve ter o devido acesso RBAC para ambas as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="d32c7-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="d32c7-127">Configurações do Diagnóstico do recurso</span><span class="sxs-lookup"><span data-stu-id="d32c7-127">Resource diagnostic settings</span></span>
<span data-ttu-id="d32c7-128">Os logs de diagnóstico do recurso para os recursos que não são de computação são configurados usando as configurações de diagnóstico do recurso.</span><span class="sxs-lookup"><span data-stu-id="d32c7-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="d32c7-129">**Configurações de Diagnóstico do Recurso** para um controle de recursos:</span><span class="sxs-lookup"><span data-stu-id="d32c7-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="d32c7-130">Para onde os logs de diagnóstico e as métricas do recurso são enviados (Conta de Armazenamento, Hubs de Eventos e/ou Log Analytics do OMS).</span><span class="sxs-lookup"><span data-stu-id="d32c7-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="d32c7-131">Quais categorias de log são enviadas e se os dados de métrica também são enviados.</span><span class="sxs-lookup"><span data-stu-id="d32c7-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="d32c7-132">Quanto tempo cada categoria de log deve ser mantida em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d32c7-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="d32c7-133">Uma retenção de zero dias significa que os registros serão mantidos indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="d32c7-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="d32c7-134">O valor pode ser qualquer quantidade de dias, entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="d32c7-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="d32c7-135">Se as políticas de retenção são definidas, mas o armazenamento dos logs em uma Conta de Armazenamento está desabilitado (por exemplo, se apenas as opções Hubs de Eventos ou OMS estão selecionadas), as políticas de retenção não têm nenhum efeito.</span><span class="sxs-lookup"><span data-stu-id="d32c7-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="d32c7-136">As políticas de retenção são aplicadas por dia, para que, ao final de um dia (UTC), os logs do dia após a política de retenção sejam excluídos.</span><span class="sxs-lookup"><span data-stu-id="d32c7-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="d32c7-137">Por exemplo, se você tiver uma política de retenção de um dia, no início do dia de hoje, os logs de anteontem serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="d32c7-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="d32c7-138">Essas configurações são facilmente definidas por meio das configurações de diagnóstico para um recurso no Portal do Azure, via Azure PowerShell e comandos da CLI ou via [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="d32c7-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="d32c7-139">Os logs de diagnóstico e as métricas da camada do sistema operacional convidado dos recursos de Computação (por exemplo, VMs ou Service Fabric) usam [um mecanismo separado para a configuração e a seleção de saídas](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d32c7-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="d32c7-140">Como habilitar a coleção de logs de diagnóstico do recurso</span><span class="sxs-lookup"><span data-stu-id="d32c7-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="d32c7-141">A coleção de logs de diagnóstico do recurso pode ser habilitada [como parte da criação de um recurso em um modelo do Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) ou depois de um recurso ser criado por meio da página do recurso no portal.</span><span class="sxs-lookup"><span data-stu-id="d32c7-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="d32c7-142">Você também pode habilitar a coleção a qualquer momento usando os comandos do Azure PowerShell ou da CLI, ou usando a API REST do Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="d32c7-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="d32c7-143">Essas instruções não podem ser aplicadas diretamente em cada recurso.</span><span class="sxs-lookup"><span data-stu-id="d32c7-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="d32c7-144">Confira os links do esquema na parte inferior desta página para entender as etapas especiais que podem ser aplicadas em certos tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="d32c7-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="d32c7-145">Como habilitar a coleção de logs de diagnóstico de recurso no Portal</span><span class="sxs-lookup"><span data-stu-id="d32c7-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="d32c7-146">Você poderá habilitar a coleta de logs de diagnóstico de recursos no portal do Azure depois que um recurso tiver sido criado, acessando um recurso específico ou navegando até o Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="d32c7-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="d32c7-147">Para habilitar isso por meio do Azure Monitor:</span><span class="sxs-lookup"><span data-stu-id="d32c7-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="d32c7-148">No [portal do Azure](http://portal.azure.com), navegue até o Azure Monitor e clique em **Configurações de Diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="d32c7-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Seção de monitoramento do Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="d32c7-150">Se desejar filtrar a lista por tipo de recurso ou grupo de recursos, clique no recurso para o qual você deseja definir uma configuração de diagnóstica.</span><span class="sxs-lookup"><span data-stu-id="d32c7-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="d32c7-151">Se nenhuma configuração existir no recurso que você selecionou, será solicitada a criação de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="d32c7-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="d32c7-152">Clique em “Ativar diagnóstico”.</span><span class="sxs-lookup"><span data-stu-id="d32c7-152">Click "Turn on diagnostics."</span></span>

   ![Adicionar configuração de diagnóstico - nenhuma configuração existente](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="d32c7-154">Se houver configurações existentes no recurso, você verá uma lista de configurações já definidas nesse recurso.</span><span class="sxs-lookup"><span data-stu-id="d32c7-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="d32c7-155">Clique em "Adicionar configuração de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="d32c7-155">Click "Add diagnostic setting."</span></span>

   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="d32c7-157">Dê um nome para sua configuração, marque as caixas para cada destino ao qual você gostaria de enviar dados e configure o recurso usado para cada destino.</span><span class="sxs-lookup"><span data-stu-id="d32c7-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="d32c7-158">Opcionalmente, defina um número de dias para manter esses logs usando os controles deslizantes **Retenção (dias)** (aplicáveis somente ao destino da conta de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="d32c7-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="d32c7-159">Uma retenção de zero dias armazena os logs indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="d32c7-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Adicionar configuração de diagnóstico - configurações existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="d32c7-161">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d32c7-161">Click **Save**.</span></span>

<span data-ttu-id="d32c7-162">Após alguns instantes, a nova configuração aparece na lista de configurações para esse recurso e os logs de diagnóstico são enviados para os destinos especificados assim que os novos dados de evento são gerados.</span><span class="sxs-lookup"><span data-stu-id="d32c7-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="d32c7-163">Habilitar a coleção de logs de diagnóstico de recurso via PowerShell</span><span class="sxs-lookup"><span data-stu-id="d32c7-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="d32c7-164">Para habilitar a coleção de logs de diagnóstico de recurso via Azure PowerShell, use os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d32c7-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="d32c7-165">Para habilitar o armazenamento dos logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="d32c7-166">A ID da conta de armazenamento é a ID de recurso da conta de armazenamento para a qual você deseja enviar os logs.</span><span class="sxs-lookup"><span data-stu-id="d32c7-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="d32c7-167">Para habilitar o streaming dos logs de diagnóstico para um hub de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="d32c7-168">A ID da regra do barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="d32c7-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="d32c7-169">Para habilitar o envio dos logs de diagnóstico para um espaço de trabalho do Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="d32c7-170">É possível obter a ID de recurso do seu espaço de trabalho do Log Analytics usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="d32c7-171">Você pode combinar esses parâmetros para permitir várias opções de saída.</span><span class="sxs-lookup"><span data-stu-id="d32c7-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="d32c7-172">Habilitar a coleção de logs de diagnóstico do recurso via CLI</span><span class="sxs-lookup"><span data-stu-id="d32c7-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="d32c7-173">Para habilitar a coleção de logs de diagnóstico de recurso via CLI do Azure, use os comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d32c7-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="d32c7-174">Para habilitar o armazenamento dos logs de diagnóstico em uma conta de armazenamento, use este comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="d32c7-175">A ID da conta de armazenamento é a ID de recurso da conta de armazenamento para a qual você deseja enviar os logs.</span><span class="sxs-lookup"><span data-stu-id="d32c7-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="d32c7-176">Para habilitar o streaming dos logs de diagnóstico para um hub de eventos, use este comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="d32c7-177">A ID da regra do barramento de serviço é uma cadeia de caracteres com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="d32c7-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="d32c7-178">Para habilitar o envio dos logs de diagnóstico para um espaço de trabalho do Log Analytics, use este comando:</span><span class="sxs-lookup"><span data-stu-id="d32c7-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="d32c7-179">Você pode combinar esses parâmetros para permitir várias opções de saída.</span><span class="sxs-lookup"><span data-stu-id="d32c7-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="d32c7-180">Habilitar a coleção de logs de diagnóstico do recurso via API REST</span><span class="sxs-lookup"><span data-stu-id="d32c7-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="d32c7-181">Para alterar as configurações de diagnóstico usando a API REST do Azure Monitor, confira [este documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="d32c7-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="d32c7-182">Gerenciar configurações de diagnóstico de recurso no Portal</span><span class="sxs-lookup"><span data-stu-id="d32c7-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="d32c7-183">Verifique se todos os seus recursos estão definidos com as configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="d32c7-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="d32c7-184">Navegue até **Monitor** no portal e abra **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="d32c7-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Folha Logs de Diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="d32c7-186">Você talvez tenha que clicar em "Mais serviços" para localizar a seção Monitoramento.</span><span class="sxs-lookup"><span data-stu-id="d32c7-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="d32c7-187">Ali, você pode exibir e filtrar todos os recursos que dão suporte a configurações de diagnóstico para ver se eles têm o diagnóstico habilitado.</span><span class="sxs-lookup"><span data-stu-id="d32c7-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="d32c7-188">Você também pode fazer uma busca detalhada para ver se várias configurações estão definidas em um recurso e verificar para qual conta de armazenamento, namespace de Hubs de Eventos e/ou espaço de trabalho do Log Analytics os dados estão fluindo.</span><span class="sxs-lookup"><span data-stu-id="d32c7-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Resultados da folha Logs de Diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="d32c7-190">A adição de uma configuração de diagnóstico mostra a exibição Configurações de Diagnóstico, onde você pode habilitar, desabilitar ou modificar as configurações de diagnóstico para o recurso selecionado.</span><span class="sxs-lookup"><span data-stu-id="d32c7-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="d32c7-191">Serviços, categorias e esquemas com suporte para os logs de diagnóstico de recurso</span><span class="sxs-lookup"><span data-stu-id="d32c7-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="d32c7-192">[Consulte este artigo](monitoring-diagnostic-logs-schema.md) para obter uma lista de serviços com suporte e as categorias de log e os esquemas usados por esses serviços.</span><span class="sxs-lookup"><span data-stu-id="d32c7-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d32c7-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d32c7-193">Next steps</span></span>

* [<span data-ttu-id="d32c7-194">Transmitir logs de diagnóstico de recurso os **Hubs de Eventos**</span><span class="sxs-lookup"><span data-stu-id="d32c7-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="d32c7-195">Alterar as configurações de diagnóstico do recurso usando a API REST do Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="d32c7-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="d32c7-196">Analisar logs do Armazenamento do Azure com o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d32c7-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
