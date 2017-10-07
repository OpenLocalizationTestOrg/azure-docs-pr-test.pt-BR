---
title: "aaaMonitor operações, eventos e contadores de NSGs | Microsoft Docs"
description: Saiba como tooenable contadores, eventos e log operacional para os NSGs
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
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="0c70d-103">Análise de logs para NSGs (grupos de segurança de rede)</span><span class="sxs-lookup"><span data-stu-id="0c70d-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="0c70d-104">Você pode habilitar Olá categorias de log de diagnóstico a seguir para NSGs:</span><span class="sxs-lookup"><span data-stu-id="0c70d-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="0c70d-105">**Evento:** contém entradas para o NSG as regras são aplicadas tooVMs e funções de instância com base no endereço MAC.</span><span class="sxs-lookup"><span data-stu-id="0c70d-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="0c70d-106">status Olá para essas regras são coletados a cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="0c70d-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="0c70d-107">**Contador da regra:** contém entradas para quantas vezes cada NSG regra é aplicada toodeny ou permitir o tráfego.</span><span class="sxs-lookup"><span data-stu-id="0c70d-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="0c70d-108">Logs de diagnóstico só estão disponíveis para os NSGs implantados por meio do modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0c70d-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0c70d-109">Não é possível habilitar o log de diagnóstico para os NSGs implantadas por meio do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="0c70d-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="0c70d-110">Para melhor compreensão de modelos de saudação dois, referência Olá [modelos de implantação do Azure Noções básicas sobre](../resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0c70d-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="0c70d-111">O log de atividades (anteriormente conhecido como logs de auditoria ou operacionais) está habilitado por padrão para NSGs criados por meio de qualquer modelo de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c70d-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="0c70d-112">toodetermine quais operações foram concluídas no NSGs no log de atividades de hello, procure entradas que contenham Olá tipos de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c70d-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="0c70d-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="0c70d-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="0c70d-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="0c70d-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="0c70d-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="0c70d-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="0c70d-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="0c70d-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="0c70d-117">Saudação de leitura [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artigo toolearn mais informações sobre logs de atividade.</span><span class="sxs-lookup"><span data-stu-id="0c70d-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="0c70d-118">Habilitar registro em log de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="0c70d-118">Enable diagnostic logging</span></span>

<span data-ttu-id="0c70d-119">Log de diagnóstico deve ser habilitado para *cada* NSG que você deseja toocollect dados.</span><span class="sxs-lookup"><span data-stu-id="0c70d-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="0c70d-120">Olá [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo explica onde os logs de diagnóstico podem ser enviados.</span><span class="sxs-lookup"><span data-stu-id="0c70d-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="0c70d-121">Se você não tiver um NSG existente, Olá concluir etapas no hello [criar um grupo de segurança de rede](virtual-networks-create-nsg-arm-pportal.md) toocreate artigo um.</span><span class="sxs-lookup"><span data-stu-id="0c70d-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="0c70d-122">Você pode habilitar o diagnóstico de log usando qualquer um dos métodos a seguir de saudação do NSG:</span><span class="sxs-lookup"><span data-stu-id="0c70d-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="0c70d-123">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0c70d-123">Azure portal</span></span>

<span data-ttu-id="0c70d-124">toouse Olá tooenable portal registro em log, logon toohello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c70d-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c70d-125">Clique em **Mais serviços** e digite *grupos de segurança de rede*.</span><span class="sxs-lookup"><span data-stu-id="0c70d-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="0c70d-126">Selecione Olá NSG que você deseja tooenable o log de.</span><span class="sxs-lookup"><span data-stu-id="0c70d-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="0c70d-127">Siga as instruções de saudação para recursos de computação não Olá [habilitar logs de diagnóstico no portal de saudação](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artigo.</span><span class="sxs-lookup"><span data-stu-id="0c70d-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="0c70d-128">Selecione **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** ou ambas as categorias de log.</span><span class="sxs-lookup"><span data-stu-id="0c70d-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="0c70d-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c70d-129">PowerShell</span></span>

<span data-ttu-id="0c70d-130">toouse PowerShell tooenable log, siga as instruções de Olá Olá [habilitar logs de diagnóstico por meio do PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artigo.</span><span class="sxs-lookup"><span data-stu-id="0c70d-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="0c70d-131">Avalie Olá informações antes de inserir um comando do artigo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c70d-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="0c70d-132">Você pode determinar Olá valor toouse para Olá `-ResourceId` parâmetro substituindo Olá seguir [texto], conforme apropriado, digitando o comando Olá `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="0c70d-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="0c70d-133">Olá ID saída do comando Olá se assemelha muito*/subscriptions/ [nome da assinatura Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="0c70d-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="0c70d-134">Se você desejar apenas toocollect dados da categoria do log adicione `-Categories [category]` toohello final do comando Olá artigo hello, onde categoria é *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="0c70d-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="0c70d-135">Se você não usar Olá `-Categories` parâmetro, coleta de dados está habilitado para categorias de log.</span><span class="sxs-lookup"><span data-stu-id="0c70d-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="0c70d-136">CLI (interface de linha de comando) do Azure</span><span class="sxs-lookup"><span data-stu-id="0c70d-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="0c70d-137">toouse Olá log de tooenable CLI, siga as instruções de Olá Olá [habilitar logs de diagnóstico por meio de CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artigo.</span><span class="sxs-lookup"><span data-stu-id="0c70d-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="0c70d-138">Avalie Olá informações antes de inserir um comando do artigo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c70d-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="0c70d-139">Você pode determinar Olá valor toouse para Olá `-ResourceId` parâmetro substituindo Olá seguir [texto], conforme apropriado, digitando o comando Olá `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="0c70d-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="0c70d-140">Olá ID saída do comando Olá se assemelha muito*/subscriptions/ [nome da assinatura Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="0c70d-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="0c70d-141">Se você desejar apenas toocollect dados da categoria do log adicione `-Categories [category]` toohello final do comando Olá artigo hello, onde categoria é *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="0c70d-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="0c70d-142">Se você não usar Olá `-Categories` parâmetro, coleta de dados está habilitado para categorias de log.</span><span class="sxs-lookup"><span data-stu-id="0c70d-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="0c70d-143">Dados registrados</span><span class="sxs-lookup"><span data-stu-id="0c70d-143">Logged data</span></span>

<span data-ttu-id="0c70d-144">Os dados formatados pelo JSON são gravados em ambos os logs.</span><span class="sxs-lookup"><span data-stu-id="0c70d-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="0c70d-145">dados específicos de saudação gravados para cada tipo de log está listado no hello seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c70d-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="0c70d-146">Log de eventos</span><span class="sxs-lookup"><span data-stu-id="0c70d-146">Event log</span></span>
<span data-ttu-id="0c70d-147">Este log contém informações sobre quais NSG regras são aplicadas tooVMs e instâncias de função de serviço, com base no endereço MAC de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0c70d-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="0c70d-148">Olá, dados de exemplo a seguir é registrada para cada evento:</span><span class="sxs-lookup"><span data-stu-id="0c70d-148">hello following example data is logged for each event:</span></span>

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

### <a name="rule-counter-log"></a><span data-ttu-id="0c70d-149">Log de contador de regra</span><span class="sxs-lookup"><span data-stu-id="0c70d-149">Rule counter log</span></span>

<span data-ttu-id="0c70d-150">Este log contém informações sobre cada regra aplicada tooresources.</span><span class="sxs-lookup"><span data-stu-id="0c70d-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="0c70d-151">Olá dados de exemplo a seguir são registrados sempre que uma regra será aplicada:</span><span class="sxs-lookup"><span data-stu-id="0c70d-151">hello following example data is logged each time a rule is applied:</span></span>

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

## <a name="view-and-analyze-logs"></a><span data-ttu-id="0c70d-152">Exibir e analisar os logs</span><span class="sxs-lookup"><span data-stu-id="0c70d-152">View and analyze logs</span></span>

<span data-ttu-id="0c70d-153">toolearn como dados de log de atividade tooview ler Olá [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0c70d-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="0c70d-154">toolearn como dados de log de diagnóstico tooview ler Olá [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0c70d-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="0c70d-155">Se você enviar dados de diagnóstico tooLog análise, você pode usar o hello [análise do grupo de segurança de rede do Azure](../log-analytics/log-analytics-azure-networking-analytics.md) solução de gerenciamento (visualização) para insights aprimorado.</span><span class="sxs-lookup"><span data-stu-id="0c70d-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
