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
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Análise de logs para NSGs (grupos de segurança de rede)

Você pode habilitar Olá categorias de log de diagnóstico a seguir para NSGs:

* **Evento:** contém entradas para o NSG as regras são aplicadas tooVMs e funções de instância com base no endereço MAC. status Olá para essas regras são coletados a cada 60 segundos.
* **Contador da regra:** contém entradas para quantas vezes cada NSG regra é aplicada toodeny ou permitir o tráfego.

> [!NOTE]
> Logs de diagnóstico só estão disponíveis para os NSGs implantados por meio do modelo de implantação do Azure Resource Manager hello. Não é possível habilitar o log de diagnóstico para os NSGs implantadas por meio do modelo de implantação clássico hello. Para melhor compreensão de modelos de saudação dois, referência Olá [modelos de implantação do Azure Noções básicas sobre](../resource-manager-deployment-model.md) artigo.

O log de atividades (anteriormente conhecido como logs de auditoria ou operacionais) está habilitado por padrão para NSGs criados por meio de qualquer modelo de implantação do Azure. toodetermine quais operações foram concluídas no NSGs no log de atividades de hello, procure entradas que contenham Olá tipos de recursos a seguir: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Saudação de leitura [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artigo toolearn mais informações sobre logs de atividade. 

## <a name="enable-diagnostic-logging"></a>Habilitar registro em log de diagnóstico

Log de diagnóstico deve ser habilitado para *cada* NSG que você deseja toocollect dados. Olá [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo explica onde os logs de diagnóstico podem ser enviados. Se você não tiver um NSG existente, Olá concluir etapas no hello [criar um grupo de segurança de rede](virtual-networks-create-nsg-arm-pportal.md) toocreate artigo um. Você pode habilitar o diagnóstico de log usando qualquer um dos métodos a seguir de saudação do NSG:

### <a name="azure-portal"></a>Portal do Azure

toouse Olá tooenable portal registro em log, logon toohello [portal](https://portal.azure.com). Clique em **Mais serviços** e digite *grupos de segurança de rede*. Selecione Olá NSG que você deseja tooenable o log de. Siga as instruções de saudação para recursos de computação não Olá [habilitar logs de diagnóstico no portal de saudação](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artigo. Selecione **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter** ou ambas as categorias de log.

### <a name="powershell"></a>PowerShell

toouse PowerShell tooenable log, siga as instruções de Olá Olá [habilitar logs de diagnóstico por meio do PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artigo. Avalie Olá informações antes de inserir um comando do artigo Olá a seguir:

- Você pode determinar Olá valor toouse para Olá `-ResourceId` parâmetro substituindo Olá seguir [texto], conforme apropriado, digitando o comando Olá `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. Olá ID saída do comando Olá se assemelha muito*/subscriptions/ [nome da assinatura Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Se você desejar apenas toocollect dados da categoria do log adicione `-Categories [category]` toohello final do comando Olá artigo hello, onde categoria é *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*. Se você não usar Olá `-Categories` parâmetro, coleta de dados está habilitado para categorias de log.

### <a name="azure-command-line-interface-cli"></a>CLI (interface de linha de comando) do Azure

toouse Olá log de tooenable CLI, siga as instruções de Olá Olá [habilitar logs de diagnóstico por meio de CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artigo. Avalie Olá informações antes de inserir um comando do artigo Olá a seguir:

- Você pode determinar Olá valor toouse para Olá `-ResourceId` parâmetro substituindo Olá seguir [texto], conforme apropriado, digitando o comando Olá `azure network nsg show [resource-group-name] [nsg-name]`. Olá ID saída do comando Olá se assemelha muito*/subscriptions/ [nome da assinatura Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Se você desejar apenas toocollect dados da categoria do log adicione `-Categories [category]` toohello final do comando Olá artigo hello, onde categoria é *NetworkSecurityGroupEvent* ou *NetworkSecurityGroupRuleCounter*. Se você não usar Olá `-Categories` parâmetro, coleta de dados está habilitado para categorias de log.

## <a name="logged-data"></a>Dados registrados

Os dados formatados pelo JSON são gravados em ambos os logs. dados específicos de saudação gravados para cada tipo de log está listado no hello seções a seguir:

### <a name="event-log"></a>Log de eventos
Este log contém informações sobre quais NSG regras são aplicadas tooVMs e instâncias de função de serviço, com base no endereço MAC de nuvem. Olá, dados de exemplo a seguir é registrada para cada evento:

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

### <a name="rule-counter-log"></a>Log de contador de regra

Este log contém informações sobre cada regra aplicada tooresources. Olá dados de exemplo a seguir são registrados sempre que uma regra será aplicada:

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

## <a name="view-and-analyze-logs"></a>Exibir e analisar os logs

toolearn como dados de log de atividade tooview ler Olá [visão geral da saudação Log de atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo. toolearn como dados de log de diagnóstico tooview ler Olá [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo. Se você enviar dados de diagnóstico tooLog análise, você pode usar o hello [análise do grupo de segurança de rede do Azure](../log-analytics/log-analytics-azure-networking-analytics.md) solução de gerenciamento (visualização) para insights aprimorado. 
