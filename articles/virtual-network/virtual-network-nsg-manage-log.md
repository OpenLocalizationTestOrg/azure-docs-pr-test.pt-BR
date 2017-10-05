---
title: "Monitorar operações, eventos e contadores para NSGs | Microsoft Docs"
description: Saiba como habilitar logs operacionais , de eventos e de contadores para NSGs
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: 552f37dd704de25159bc0f0ad34fdae9ed8b73f5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="0ee88-103">Análise de logs para NSGs (grupos de segurança de rede)</span><span class="sxs-lookup"><span data-stu-id="0ee88-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="0ee88-104">Você pode habilitar as seguintes categorias de log de diagnóstico para NSGs:</span><span class="sxs-lookup"><span data-stu-id="0ee88-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="0ee88-105">**Evento:** contém entradas para as regras NSG que são aplicadas às VMs e funções de instância com base no endereço MAC.</span><span class="sxs-lookup"><span data-stu-id="0ee88-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="0ee88-106">O status para essas regras é coletado a cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="0ee88-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="0ee88-107">**Contador de regras:** contém entradas de quantas vezes cada regra NSG é aplicada para negar ou permitir tráfego.</span><span class="sxs-lookup"><span data-stu-id="0ee88-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="0ee88-108">Os logs de diagnóstico estão disponíveis apenas para NSGs implantados por meio do modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ee88-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0ee88-109">Você não pode habilitar o log de diagnóstico para NSGs implantados por meio do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="0ee88-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="0ee88-110">Para entender melhor esses dois modelos, leia o artigo [Understanding Azure deployment models](../resource-manager-deployment-model.md) (Noções básicas sobre os modelos de implantação do Azure).</span><span class="sxs-lookup"><span data-stu-id="0ee88-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="0ee88-111">O log de atividades (anteriormente conhecido como logs de auditoria ou operacionais) está habilitado por padrão para NSGs criados por meio de qualquer modelo de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee88-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="0ee88-112">Para determinar quais operações foram concluídas em NSGs no log de atividades, procure entradas contendo os seguintes tipos de recursos:</span><span class="sxs-lookup"><span data-stu-id="0ee88-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="0ee88-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="0ee88-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="0ee88-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="0ee88-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="0ee88-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="0ee88-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="0ee88-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="0ee88-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="0ee88-117">Leia o artigo [Visão geral do Log de Atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) para saber mais sobre os logs de atividade.</span><span class="sxs-lookup"><span data-stu-id="0ee88-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="0ee88-118">Habilitar registro em log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0ee88-118">Enable diagnostic logging</span></span>

<span data-ttu-id="0ee88-119">O log de diagnóstico deve ser habilitado para *cada* NSG do qual você quer coletar dados.</span><span class="sxs-lookup"><span data-stu-id="0ee88-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="0ee88-120">O artigo [Visão geral dos Logs de Diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) explica para onde os logs de diagnóstico podem ser enviados.</span><span class="sxs-lookup"><span data-stu-id="0ee88-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="0ee88-121">Caso não tenha um NSG, conclua as etapas no artigo sobre como [criar um grupo de segurança de rede](virtual-networks-create-nsg-arm-pportal.md) para criar um.</span><span class="sxs-lookup"><span data-stu-id="0ee88-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="0ee88-122">Você pode habilitar o log de diagnóstico do NSG usando qualquer um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="0ee88-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="0ee88-123">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0ee88-123">Azure portal</span></span>

<span data-ttu-id="0ee88-124">Para usar o portal a fim de habilitar o log, entre no [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ee88-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="0ee88-125">Clique em **Mais serviços** e digite *grupos de segurança de rede*.</span><span class="sxs-lookup"><span data-stu-id="0ee88-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="0ee88-126">Escolha o NSG para o qual quer habilitar o log.</span><span class="sxs-lookup"><span data-stu-id="0ee88-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="0ee88-127">Siga as instruções para recursos de não computação no artigo [Habilite os logs de diagnóstico no portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="0ee88-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="0ee88-128">Selecione **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** ou ambas as categorias de log.</span><span class="sxs-lookup"><span data-stu-id="0ee88-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="0ee88-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ee88-129">PowerShell</span></span>

<span data-ttu-id="0ee88-130">Para usar o PowerShell a fim de habilitar o log, siga as instruções no artigo [Habilitar os Logs de Diagnóstico pelo PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="0ee88-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="0ee88-131">Avalie as seguintes informações antes de inserir um comando do artigo:</span><span class="sxs-lookup"><span data-stu-id="0ee88-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="0ee88-132">Você pode determinar o valor a ser usado para o parâmetro `-ResourceId` substituindo o seguinte [texto], conforme apropriado, e digitando o comando `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="0ee88-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="0ee88-133">A saída de ID do comando é semelhante a */subscriptions/[ID da Assinatura]/resourceGroups/[grupo de recursos]/providers/Microsoft.Network/networkSecurityGroups/[nome do NSG]*.</span><span class="sxs-lookup"><span data-stu-id="0ee88-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="0ee88-134">Se quiser coletar apenas dados da categoria de log, adicione `-Categories [category]` ao fim do comando no artigo, onde a categoria é *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="0ee88-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="0ee88-135">Se não quiser usar o parâmetro `-Categories`, a coleta de dados será habilitada para ambas as categorias de log.</span><span class="sxs-lookup"><span data-stu-id="0ee88-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="0ee88-136">CLI (interface de linha de comando) do Azure</span><span class="sxs-lookup"><span data-stu-id="0ee88-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="0ee88-137">Para usar a CLI a fim de habilitar o log, siga as instruções no artigo [Habilitar os Logs de Diagnóstico pela CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs).</span><span class="sxs-lookup"><span data-stu-id="0ee88-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="0ee88-138">Avalie as seguintes informações antes de inserir um comando do artigo:</span><span class="sxs-lookup"><span data-stu-id="0ee88-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="0ee88-139">Você pode determinar o valor a ser usado para o parâmetro `-ResourceId` substituindo o seguinte [texto], conforme apropriado, e digitando o comando `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="0ee88-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="0ee88-140">A saída de ID do comando é semelhante a */subscriptions/[ID da Assinatura]/resourceGroups/[grupo de recursos]/providers/Microsoft.Network/networkSecurityGroups/[nome do NSG]*.</span><span class="sxs-lookup"><span data-stu-id="0ee88-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="0ee88-141">Se quiser coletar apenas dados da categoria de log, adicione `-Categories [category]` ao fim do comando no artigo, onde a categoria é *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="0ee88-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="0ee88-142">Se não quiser usar o parâmetro `-Categories`, a coleta de dados será habilitada para ambas as categorias de log.</span><span class="sxs-lookup"><span data-stu-id="0ee88-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="0ee88-143">Dados registrados</span><span class="sxs-lookup"><span data-stu-id="0ee88-143">Logged data</span></span>

<span data-ttu-id="0ee88-144">Os dados formatados pelo JSON são gravados em ambos os logs.</span><span class="sxs-lookup"><span data-stu-id="0ee88-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="0ee88-145">Os dados específicos gravados para cada tipo de log são listados nas seguintes seções:</span><span class="sxs-lookup"><span data-stu-id="0ee88-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="0ee88-146">Log de eventos</span><span class="sxs-lookup"><span data-stu-id="0ee88-146">Event log</span></span>
<span data-ttu-id="0ee88-147">Esse log contém informações sobre quais regras NSG são aplicadas às VMs e instâncias de função de serviço de nuvem, com base no endereço MAC.</span><span class="sxs-lookup"><span data-stu-id="0ee88-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="0ee88-148">Os seguintes dados de exemplo são registrados para cada evento:</span><span class="sxs-lookup"><span data-stu-id="0ee88-148">The following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="0ee88-149">Log de contador de regra</span><span class="sxs-lookup"><span data-stu-id="0ee88-149">Rule counter log</span></span>

<span data-ttu-id="0ee88-150">Esse log contém informações sobre cada regra aplicada aos recursos.</span><span class="sxs-lookup"><span data-stu-id="0ee88-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="0ee88-151">Os seguintes dados de exemplo são registrados toda vez que uma regra é aplicada:</span><span class="sxs-lookup"><span data-stu-id="0ee88-151">The following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="0ee88-152">Exibir e analisar os logs</span><span class="sxs-lookup"><span data-stu-id="0ee88-152">View and analyze logs</span></span>

<span data-ttu-id="0ee88-153">Para saber como exibir os dados do log de atividade, leia o artigo [Visão Geral dos Logs de Atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="0ee88-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="0ee88-154">Para saber como exibir os dados do log de diagnóstico, leia o artigo [Visão Geral dos Logs de Diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="0ee88-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="0ee88-155">Se você enviar dados de diagnóstico ao Log Analytics, será possível usar a solução de gerenciamento de [análise de Grupo de Segurança de Rede do Azure](../log-analytics/log-analytics-azure-networking-analytics.md) (visualização) para obter informações avançadas.</span><span class="sxs-lookup"><span data-stu-id="0ee88-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
