---
title: "aaaManage fluxo de grupo de segurança de rede registra com o observador de rede do Azure - CLI do Azure | Microsoft Docs"
description: "Esta página explica como os logs de toomanage fluxo de grupo de segurança de rede no Azure observador de rede com a CLI do Azure"
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Configurar logs de fluxo de grupo de segurança de rede com a CLI do Azure

> [!div class="op_single_selector"]
> - [Portal do Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Logs de fluxo de grupo de segurança de rede são um recurso do observador de rede que permite que você tooview informações sobre o tráfego IP de entrada e saída por meio de um grupo de segurança de rede. Esses logs de fluxo são gravados no formato json e mostram saídas fluxos de entrada em uma base por regra, Olá fluxo de saudação do NIC se aplica, 5-tupla informações sobre o fluxo de saudação (protocolo IP de origem/destino, porta de origem/destino) e se hello tráfego foi permitido ou negado.

Este artigo usa nossa próxima geração CLI para o modelo de implantação de gerenciamento de recursos do hello, 2.0 do CLI do Azure, que está disponível para Windows, Mac e Linux.

Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="register-insights-provider"></a>Provedor de informações de registro

Em ordem para o fluxo de log toowork com êxito, Olá **Insights** provedor deve ser registrado. Se você não tiver certeza se hello **Insights** provedor está registrado, execute hello script a seguir.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Habilitar os logs do Fluxo de Grupo de Segurança de Rede

Olá comando tooenable fluxo logs é mostrado no exemplo a seguir de saudação:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>Desabilitar os logs do Fluxo de Grupo de Segurança de Rede

Olá Use logs de fluxo de toodisable de exemplo a seguir:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
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
