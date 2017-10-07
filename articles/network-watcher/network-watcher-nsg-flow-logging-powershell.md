---
title: "aaaManage fluxo de grupo de segurança de rede registra com o observador de rede do Azure - PowerShell | Microsoft Docs"
description: "Esta página explica como os logs de toomanage fluxo de grupo de segurança de rede no Azure observador de rede com o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 987e8728fb6459fd6ff8eb5cd3d36ff855f2ccfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a>Configurar logs de fluxo de Grupo de Segurança de Rede com o PowerShell

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede. Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.

## <a name="register-insights-provider"></a>Provedor de informações de registro

Em ordem para o fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado. Se você não tiver certeza se hello **Insights** provedor está registrado, execute hello script a seguir.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Habilitar os logs do Fluxo de Grupo de Segurança de Rede

Olá comando tooenable fluxo logs é mostrado no exemplo a seguir de saudação:

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a>Desabilitar os logs do Fluxo de Grupo de Segurança de Rede

Olá Use logs de fluxo de toodisable de exemplo a seguir:

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a>Baixar um log de fluxo

local de armazenamento de saudação de um log de fluxo é definido no momento da criação. Um tooaccess ferramenta conveniente dessas contas de armazenamento tooa fluxo salvar logs é o Microsoft Azure Storage Explorer, que pode ser baixado em: http://storageexplorer.com/

Se uma conta de armazenamento for especificada, os arquivos de captura de pacote são salvos tooa conta de armazenamento no hello local a seguir:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Para obter informações sobre a estrutura de saudação do log Olá visite [log visão geral de fluxo de grupo de segurança de rede](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Próximas etapas

Saiba como muito[visualizar seus logs de fluxo NSG com o Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Saiba como muito[visualizar seus logs de fluxo NSG com ferramentas de software livre](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
