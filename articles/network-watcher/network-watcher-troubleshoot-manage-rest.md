---
title: "aaaTroubleshoot Gateway de rede Virtual e conexões usando o observador de rede do Azure - REST | Microsoft Docs"
description: "Esta página explica como Gateways de rede Virtual tootroubleshoot e conexões com o observador de rede do Azure usando REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>Como solucionar problemas de conexões e gateway de rede virtual do usando o observador de rede do Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API REST](network-watcher-troubleshoot-manage-rest.md)

Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure. Um desses recursos é a solução de problemas de recursos. Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST. Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.

Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para solução de problemas de recursos.

- [**Solução de problemas de um gateway de rede virtual**](#troubleshoot-a-virtual-network-gateway)
- [**Como solucionar problemas de uma conexão**](#troubleshoot-connections)

## <a name="before-you-begin"></a>Antes de começar

ARMclient é toocall usado Olá REST API usando o PowerShell. O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)

Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.

Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Visão geral

Solução de problemas do Inspetor de rede fornece a capacidade de saudação solucionar problemas que surgem com gateways de rede Virtual e conexões. Quando uma solicitação é feita toohello recursos de solução de problemas, logs consultar e inspecionados. Quando inspeção estiver concluída, os resultados de saudação são retornados. Olá solucionar API solicitações são longos solicitações, que podem levar vários tooreturn de minutos que um resultado de execução. Os logs são armazenados em um contêiner em uma conta de armazenamento.

## <a name="log-in-with-armclient"></a>Como fazer logon com ARMClient

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>Solução de problemas de um gateway de rede virtual


### <a name="post-hello-troubleshoot-request"></a>Saudação POST solucionar problemas de solicitação

Olá seguintes status de saudação de consultas de exemplo de um gateway de rede Virtual.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

Desde que esta operação é longa em execução, Olá URI de consulta de operação de saudação e hello URI para o resultado de saudação é retornado no cabeçalho de resposta Olá conforme Olá resposta a seguir:

**Valores importantes**

* **Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async solucionar problemas de operações
* **Local** -esta propriedade contém Olá URI onde Olá resultados são quando hello operação for concluída

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Operação assíncrona de saudação para conclusão da consulta

Use Olá operações URI tooquery para o andamento da operação de Olá Olá como visto no exemplo a seguir de saudação:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Enquanto a operação de saudação está em andamento, Olá resposta mostra **em andamento** como visto no exemplo a seguir de saudação:

```json
{
  "status": "InProgress"
}
```

Quando operação Olá é alterações de status de saudação completa muito**êxito**.

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>Recuperar resultados Olá

Depois que o status de saudação retornado é **êxito**, chamar um método GET em Olá operationResult URI tooretrieve resultados hello.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Hello respostas seguintes são exemplos de uma resposta degradada típico retornados ao consultar os resultados de saudação de um gateway de solução de problemas. Consulte [Entendendo os resultados da saudação](#understanding-the-results) tooget esclarecimento em quais propriedades Olá em média de resposta de saudação.

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a>Conexões da solução de problemas

Olá status de saudação de consultas de exemplo de uma Conexão a seguir.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> Olá solucionar problemas de operações não podem ser executados em paralelo em uma Conexão e seus gateways correspondentes. Olá é necessário concluir operação anterior toorunning-o em um recurso de saudação anterior.

Como esta é uma transação de longa execução, no cabeçalho de resposta hello, Olá URI para consultar operação hello e hello URI para o resultado de saudação é retornado conforme Olá resposta a seguir:

**Valores importantes**

* **Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async solucionar problemas de operações
* **Local** -esta propriedade contém Olá URI onde Olá resultados são quando hello operação for concluída

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Operação assíncrona de saudação para conclusão da consulta

Use Olá operações URI tooquery para o andamento da operação de Olá Olá como visto no exemplo a seguir de saudação:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Enquanto a operação de saudação está em andamento, Olá resposta mostra **em andamento** como visto no exemplo a seguir de saudação:

```json
{
  "status": "InProgress"
}
```

Quando Olá operação estiver concluída, o status de saudação muda muito**êxito**.

```json
{
  "status": "Succeeded"
}
```

Olá respostas seguintes são exemplos de uma resposta típica retornados ao consultar os resultados de saudação de uma Conexão de solução de problemas.

### <a name="retrieve-hello-results"></a>Recuperar resultados Olá

Depois que o status de saudação retornado é **êxito**, chamar um método GET em Olá operationResult URI tooretrieve resultados hello.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Olá respostas seguintes são exemplos de uma resposta típica retornados ao consultar os resultados de saudação de uma Conexão de solução de problemas.

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a>Entendendo os resultados da saudação

texto da ação de saudação fornece diretrizes gerais sobre como tooresolve Olá problema. Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais. No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.  Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)

Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que pode ser usada é o Gerenciador de armazenamento. Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)

## <a name="next-steps"></a>Próximas etapas

Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.
