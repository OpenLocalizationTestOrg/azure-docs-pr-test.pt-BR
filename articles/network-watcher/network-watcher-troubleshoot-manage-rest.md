---
title: "Como solucionar problemas de conexões e gateway de rede virtual do usando o observador de rede do Azure - REST | Microsoft Docs"
description: "Esta página explica como solucionar problemas de conexões e gateways de rede virtual com o observador de rede do Azure usando a REST"
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="ac521-103">Como solucionar problemas de conexões e gateway de rede virtual do usando o observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="ac521-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ac521-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ac521-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="ac521-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac521-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="ac521-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ac521-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="ac521-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ac521-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="ac521-108">API REST</span><span class="sxs-lookup"><span data-stu-id="ac521-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="ac521-109">O observador de rede oferece muitos recursos que dizem respeito às noções básicas sobre os recursos de rede no Azure.</span><span class="sxs-lookup"><span data-stu-id="ac521-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="ac521-110">Um desses recursos é a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac521-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="ac521-111">A solução de problemas de recursos pode ser chamada pelo Portal, pelo PowerShell, pela CLI ou pela API REST.</span><span class="sxs-lookup"><span data-stu-id="ac521-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="ac521-112">Quando chamado, o Observador de rede inspeciona a integridade de uma conexão ou um gateway de rede virtual e faz um relatório sobre suas descobertas.</span><span class="sxs-lookup"><span data-stu-id="ac521-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="ac521-113">Neste artigo, você conhecerá as diferentes tarefas de gerenciamento que estão disponíveis para a solução de problemas de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac521-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="ac521-114">**Solução de problemas de um gateway de rede virtual**</span><span class="sxs-lookup"><span data-stu-id="ac521-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="ac521-115">**Como solucionar problemas de uma conexão**</span><span class="sxs-lookup"><span data-stu-id="ac521-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="ac521-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="ac521-116">Before you begin</span></span>

<span data-ttu-id="ac521-117">O ARMclient é usado para chamar a API REST usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac521-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="ac521-118">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="ac521-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="ac521-119">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="ac521-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="ac521-120">Para obter uma lista de tipos de gateway com suporte, visite [Tipos de Gateway com suporte](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="ac521-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="ac521-121">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ac521-121">Overview</span></span>

<span data-ttu-id="ac521-122">A solução de problemas do observador de rede fornece a capacidade de solucionar problemas que podem surgir com as conexões e os gateways de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ac521-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="ac521-123">Quando se faz uma solicitação para a solução de problemas de recursos, os logs são consultados e inspecionados.</span><span class="sxs-lookup"><span data-stu-id="ac521-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="ac521-124">Você receberá um relatório com os resultados assim que a inspeção estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="ac521-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="ac521-125">As solicitações de API de solução de problemas são solicitações de execução longa e podem demorar para gerar um resultado.</span><span class="sxs-lookup"><span data-stu-id="ac521-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="ac521-126">Os logs são armazenados em um contêiner em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac521-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="ac521-127">Como fazer logon com ARMClient</span><span class="sxs-lookup"><span data-stu-id="ac521-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="ac521-128">Solução de problemas de um gateway de rede virtual</span><span class="sxs-lookup"><span data-stu-id="ac521-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="ac521-129">POST da solicitação de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="ac521-129">POST the troubleshoot request</span></span>

<span data-ttu-id="ac521-130">O exemplo a seguir consulta o status de um gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ac521-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="ac521-131">Como essa operação tem execução longa, o URI para consultar a operação e o URI para o resultado são retornados no cabeçalho de resposta, como mostra a seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="ac521-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="ac521-132">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="ac521-132">**Important Values**</span></span>

* <span data-ttu-id="ac521-133">**Azure-AsyncOperation** - esta propriedade contém o URI para a consulta da operação de solução de problemas do Async</span><span class="sxs-lookup"><span data-stu-id="ac521-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="ac521-134">**Local** - esta propriedade contém o URI do local para o qual os resultados são enviados após a conclusão da operação</span><span class="sxs-lookup"><span data-stu-id="ac521-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="ac521-135">Consulta da operação assíncrona para conclusão</span><span class="sxs-lookup"><span data-stu-id="ac521-135">Query the async operation for completion</span></span>

<span data-ttu-id="ac521-136">Use as operações de URI para consulta do andamento da operação conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac521-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="ac521-137">Enquanto a operação está em andamento, a resposta mostra **InProgress** conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac521-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="ac521-138">Quando a operação estiver concluída o status será alterado para **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="ac521-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="ac521-139">Recuperar os resultados</span><span class="sxs-lookup"><span data-stu-id="ac521-139">Retrieve the results</span></span>

<span data-ttu-id="ac521-140">Assim que o status é definido com **Succeeded**, chame um método GET no URI do operationResult para recuperar os resultados.</span><span class="sxs-lookup"><span data-stu-id="ac521-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="ac521-141">As respostas a seguir são exemplos de uma resposta típica e degradada retornada ao consultar os resultados de um gateway de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="ac521-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="ac521-142">Confira [Compressão dos resultados](#understanding-the-results) para aprender os significados das propriedades das respostas.</span><span class="sxs-lookup"><span data-stu-id="ac521-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="ac521-143">Conexões da solução de problemas</span><span class="sxs-lookup"><span data-stu-id="ac521-143">Troubleshoot Connections</span></span>

<span data-ttu-id="ac521-144">O exemplo a seguir consulta o status de uma conexão.</span><span class="sxs-lookup"><span data-stu-id="ac521-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="ac521-145">A operação de solução de problemas não pode ser executada em paralelo em uma conexão e seus gateways correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ac521-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="ac521-146">A operação deve ser concluída antes de ser executada no recurso anterior.</span><span class="sxs-lookup"><span data-stu-id="ac521-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="ac521-147">Como essa é uma transação de longa execução, o URI para consultar a operação e o URI para o resultado são retornados no cabeçalho de resposta, veja um exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac521-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="ac521-148">**Valores importantes**</span><span class="sxs-lookup"><span data-stu-id="ac521-148">**Important Values**</span></span>

* <span data-ttu-id="ac521-149">**Azure-AsyncOperation** - esta propriedade contém o URI para a consulta da operação de solução de problemas do Async</span><span class="sxs-lookup"><span data-stu-id="ac521-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="ac521-150">**Local** - esta propriedade contém o URI do local para o qual os resultados são enviados após a conclusão da operação</span><span class="sxs-lookup"><span data-stu-id="ac521-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="ac521-151">Consulta da operação assíncrona para conclusão</span><span class="sxs-lookup"><span data-stu-id="ac521-151">Query the async operation for completion</span></span>

<span data-ttu-id="ac521-152">Use as operações de URI para consulta do andamento da operação conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac521-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="ac521-153">Enquanto a operação está em andamento, a resposta mostra **InProgress** conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac521-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="ac521-154">Quando a operação for concluída, o status será alterado para **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="ac521-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="ac521-155">As respostas a seguir são exemplos de uma resposta típica e degradada retornada ao consultar os resultados de uma conexão de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="ac521-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="ac521-156">Recuperar os resultados</span><span class="sxs-lookup"><span data-stu-id="ac521-156">Retrieve the results</span></span>

<span data-ttu-id="ac521-157">Assim que o status é definido com **Succeeded**, chame um método GET no URI do operationResult para recuperar os resultados.</span><span class="sxs-lookup"><span data-stu-id="ac521-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="ac521-158">As respostas a seguir são exemplos de uma resposta típica e degradada retornada ao consultar os resultados de uma conexão de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="ac521-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="ac521-159">Como entender os resultados</span><span class="sxs-lookup"><span data-stu-id="ac521-159">Understanding the results</span></span>

<span data-ttu-id="ac521-160">O texto de ação fornece orientação geral sobre como resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="ac521-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="ac521-161">Se for possível executar uma ação para solucionar o problema, você receberá um link com orientações adicionais.</span><span class="sxs-lookup"><span data-stu-id="ac521-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="ac521-162">Nos casos em que não há orientações adicionais, a resposta fornecerá a url para abrir um caso de suporte.</span><span class="sxs-lookup"><span data-stu-id="ac521-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="ac521-163">Para obter mais informações sobre as propriedades da resposta e o do que está incluído, acesse [Visão geral da solução de problemas do observador de rede](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ac521-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="ac521-164">Para obter instruções sobre como baixar os arquivos de contas de armazenamento do Azure, confira [Introdução ao armazenamento de Blobs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="ac521-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="ac521-165">Outra ferramenta que pode ser usada é o Gerenciador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ac521-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="ac521-166">Para obter mais informações sobre o Gerenciador de armazenamento acesse o link: [Gerenciador de armazenamento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="ac521-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac521-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac521-167">Next steps</span></span>

<span data-ttu-id="ac521-168">Se as configurações para a conectividade VPN foram alteradas, confira [Gerenciamento de grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para acompanhar quais são as regras de segurança e o grupo de segurança de rede envolvidos na questão.</span><span class="sxs-lookup"><span data-stu-id="ac521-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
