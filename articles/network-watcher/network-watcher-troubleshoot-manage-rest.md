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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="f75bf-103">Como solucionar problemas de conexões e gateway de rede virtual do usando o observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="f75bf-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f75bf-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f75bf-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="f75bf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f75bf-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="f75bf-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f75bf-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="f75bf-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f75bf-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="f75bf-108">API REST</span><span class="sxs-lookup"><span data-stu-id="f75bf-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="f75bf-109">Observador de rede fornece vários recursos que diz respeito a toounderstanding seus recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="f75bf-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="f75bf-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="f75bf-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="f75bf-111">Recursos de solução de problemas pode ser chamada por meio do portal de saudação, o PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="f75bf-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="f75bf-112">Quando chamado, o observador de rede inspeciona a integridade de saudação de um Gateway de rede Virtual ou uma Conexão e retorna suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="f75bf-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="f75bf-113">Este artigo o orienta por Olá diversas tarefas de gerenciamento que estão atualmente disponíveis para solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="f75bf-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="f75bf-114">**Solução de problemas de um gateway de rede virtual**</span><span class="sxs-lookup"><span data-stu-id="f75bf-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="f75bf-115">**Como solucionar problemas de uma conexão**</span><span class="sxs-lookup"><span data-stu-id="f75bf-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="f75bf-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f75bf-116">Before you begin</span></span>

<span data-ttu-id="f75bf-117">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f75bf-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="f75bf-118">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="f75bf-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="f75bf-119">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="f75bf-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="f75bf-120">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="f75bf-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="f75bf-121">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f75bf-121">Overview</span></span>

<span data-ttu-id="f75bf-122">Solução de problemas do Inspetor de rede fornece a capacidade de saudação solucionar problemas que surgem com gateways de rede Virtual e conexões.</span><span class="sxs-lookup"><span data-stu-id="f75bf-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="f75bf-123">Quando uma solicitação é feita toohello recursos de solução de problemas, logs consultar e inspecionados.</span><span class="sxs-lookup"><span data-stu-id="f75bf-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="f75bf-124">Quando inspeção estiver concluída, os resultados de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="f75bf-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="f75bf-125">Olá solucionar API solicitações são longos solicitações, que podem levar vários tooreturn de minutos que um resultado de execução.</span><span class="sxs-lookup"><span data-stu-id="f75bf-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="f75bf-126">Os logs são armazenados em um contêiner em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f75bf-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="f75bf-127">Como fazer logon com ARMClient</span><span class="sxs-lookup"><span data-stu-id="f75bf-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="f75bf-128">Solução de problemas de um gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f75bf-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="f75bf-129">Saudação POST solucionar problemas de solicitação</span><span class="sxs-lookup"><span data-stu-id="f75bf-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="f75bf-130">Olá seguintes status de saudação de consultas de exemplo de um gateway de rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="f75bf-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="f75bf-131">Desde que esta operação é longa em execução, Olá URI de consulta de operação de saudação e hello URI para o resultado de saudação é retornado no cabeçalho de resposta Olá conforme Olá resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="f75bf-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="f75bf-132">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="f75bf-132">**Important Values**</span></span>

* <span data-ttu-id="f75bf-133">**Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async solucionar problemas de operações</span><span class="sxs-lookup"><span data-stu-id="f75bf-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="f75bf-134">**Local** -esta propriedade contém Olá URI onde Olá resultados são quando hello operação for concluída</span><span class="sxs-lookup"><span data-stu-id="f75bf-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="f75bf-135">Operação assíncrona de saudação para conclusão da consulta</span><span class="sxs-lookup"><span data-stu-id="f75bf-135">Query hello async operation for completion</span></span>

<span data-ttu-id="f75bf-136">Use Olá operações URI tooquery para o andamento da operação de Olá Olá como visto no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f75bf-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="f75bf-137">Enquanto a operação de saudação está em andamento, Olá resposta mostra **em andamento** como visto no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f75bf-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="f75bf-138">Quando operação Olá é alterações de status de saudação completa muito**êxito**.</span><span class="sxs-lookup"><span data-stu-id="f75bf-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="f75bf-139">Recuperar resultados Olá</span><span class="sxs-lookup"><span data-stu-id="f75bf-139">Retrieve hello results</span></span>

<span data-ttu-id="f75bf-140">Depois que o status de saudação retornado é **êxito**, chamar um método GET em Olá operationResult URI tooretrieve resultados hello.</span><span class="sxs-lookup"><span data-stu-id="f75bf-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="f75bf-141">Hello respostas seguintes são exemplos de uma resposta degradada típico retornados ao consultar os resultados de saudação de um gateway de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="f75bf-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="f75bf-142">Consulte [Entendendo os resultados da saudação](#understanding-the-results) tooget esclarecimento em quais propriedades Olá em média de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f75bf-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

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


## <a name="troubleshoot-connections"></a><span data-ttu-id="f75bf-143">Conexões da solução de problemas</span><span class="sxs-lookup"><span data-stu-id="f75bf-143">Troubleshoot Connections</span></span>

<span data-ttu-id="f75bf-144">Olá status de saudação de consultas de exemplo de uma Conexão a seguir.</span><span class="sxs-lookup"><span data-stu-id="f75bf-144">hello following example queries hello status of a Connection.</span></span>

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
> <span data-ttu-id="f75bf-145">Olá solucionar problemas de operações não podem ser executados em paralelo em uma Conexão e seus gateways correspondentes.</span><span class="sxs-lookup"><span data-stu-id="f75bf-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="f75bf-146">Olá é necessário concluir operação anterior toorunning-o em um recurso de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="f75bf-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="f75bf-147">Como esta é uma transação de longa execução, no cabeçalho de resposta hello, Olá URI para consultar operação hello e hello URI para o resultado de saudação é retornado conforme Olá resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="f75bf-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="f75bf-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="f75bf-148">**Important Values**</span></span>

* <span data-ttu-id="f75bf-149">**Azure AsyncOperation** -esta propriedade contém Olá URI tooquery Olá Async solucionar problemas de operações</span><span class="sxs-lookup"><span data-stu-id="f75bf-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="f75bf-150">**Local** -esta propriedade contém Olá URI onde Olá resultados são quando hello operação for concluída</span><span class="sxs-lookup"><span data-stu-id="f75bf-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="f75bf-151">Operação assíncrona de saudação para conclusão da consulta</span><span class="sxs-lookup"><span data-stu-id="f75bf-151">Query hello async operation for completion</span></span>

<span data-ttu-id="f75bf-152">Use Olá operações URI tooquery para o andamento da operação de Olá Olá como visto no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f75bf-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="f75bf-153">Enquanto a operação de saudação está em andamento, Olá resposta mostra **em andamento** como visto no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f75bf-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="f75bf-154">Quando Olá operação estiver concluída, o status de saudação muda muito**êxito**.</span><span class="sxs-lookup"><span data-stu-id="f75bf-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="f75bf-155">Olá respostas seguintes são exemplos de uma resposta típica retornados ao consultar os resultados de saudação de uma Conexão de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="f75bf-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="f75bf-156">Recuperar resultados Olá</span><span class="sxs-lookup"><span data-stu-id="f75bf-156">Retrieve hello results</span></span>

<span data-ttu-id="f75bf-157">Depois que o status de saudação retornado é **êxito**, chamar um método GET em Olá operationResult URI tooretrieve resultados hello.</span><span class="sxs-lookup"><span data-stu-id="f75bf-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="f75bf-158">Olá respostas seguintes são exemplos de uma resposta típica retornados ao consultar os resultados de saudação de uma Conexão de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="f75bf-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="f75bf-159">Entendendo os resultados da saudação</span><span class="sxs-lookup"><span data-stu-id="f75bf-159">Understanding hello results</span></span>

<span data-ttu-id="f75bf-160">texto da ação de saudação fornece diretrizes gerais sobre como tooresolve Olá problema.</span><span class="sxs-lookup"><span data-stu-id="f75bf-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="f75bf-161">Se uma ação pode ser executada para o problema de saudação, um link é fornecido com diretrizes adicionais.</span><span class="sxs-lookup"><span data-stu-id="f75bf-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="f75bf-162">No caso de Olá onde não há nenhuma orientação adicional, resposta Olá fornece Olá url tooopen um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="f75bf-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="f75bf-163">Para obter mais informações sobre propriedades de saudação de resposta hello e o que está incluído, visite [visão geral da solução de problemas do Inspetor de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f75bf-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="f75bf-164">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="f75bf-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="f75bf-165">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f75bf-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="f75bf-166">Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="f75bf-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f75bf-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f75bf-167">Next steps</span></span>

<span data-ttu-id="f75bf-168">Se as configurações foram alteradas se parar a conectividade de VPN, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que podem ser em questão.</span><span class="sxs-lookup"><span data-stu-id="f75bf-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
