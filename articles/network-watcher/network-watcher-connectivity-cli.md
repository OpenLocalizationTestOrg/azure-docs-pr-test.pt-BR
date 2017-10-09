---
title: aaaCheck conectividade com o observador de rede do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Esta página explica como toouse conectividade para verificar com o observador de rede usando o Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="cd639-103">Verificar a conectividade com o Observador de Rede do Azure usando a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="cd639-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="cd639-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd639-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="cd639-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd639-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="cd639-106">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="cd639-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="cd639-107">Saiba como toouse tooverify de conectividade se uma conexão TCP direto de tooa uma máquina virtual que recebe o ponto de extremidade pode ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cd639-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cd639-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="cd639-108">Before you begin</span></span>

<span data-ttu-id="cd639-109">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd639-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="cd639-110">Uma instância do observador de rede na região Olá deseja toocheck conectividade.</span><span class="sxs-lookup"><span data-stu-id="cd639-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="cd639-111">Conectividade de toocheck de máquinas virtuais com.</span><span class="sxs-lookup"><span data-stu-id="cd639-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="cd639-112">A verificação de conectividade requer uma extensão de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="cd639-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="cd639-113">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="cd639-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="cd639-114">Registrar o recurso de visualização de saudação</span><span class="sxs-lookup"><span data-stu-id="cd639-114">Register hello preview capability</span></span> 

<span data-ttu-id="cd639-115">Verificação de conectividade está atualmente em visualização pública, toouse esse recurso que é necessário toobe registrado.</span><span class="sxs-lookup"><span data-stu-id="cd639-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="cd639-116">toodo, Olá execução seguinte exemplo CLI</span><span class="sxs-lookup"><span data-stu-id="cd639-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="cd639-117">tooverify Olá o registro foi bem-sucedido, execute Olá CLI comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd639-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="cd639-118">Se o recurso de saudação foi registrado corretamente, saída de hello deve corresponder a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="cd639-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="cd639-119">Verifique a conectividade tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="cd639-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="cd639-120">Este exemplo verifica a máquina de virtual de destino conectividade tooa pela porta 80.</span><span class="sxs-lookup"><span data-stu-id="cd639-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="cd639-121">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cd639-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="cd639-122">Resposta</span><span class="sxs-lookup"><span data-stu-id="cd639-122">Response</span></span>

<span data-ttu-id="cd639-123">saudação de resposta a seguir é do exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd639-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="cd639-124">Essa resposta, Olá `ConnectionStatus` é **inacessível**.</span><span class="sxs-lookup"><span data-stu-id="cd639-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="cd639-125">Você pode ver que todos os Olá investigações enviadas com falha.</span><span class="sxs-lookup"><span data-stu-id="cd639-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="cd639-126">conectividade Olá falha no dispositivo virtual Olá vencimento tooa configurada pelo usuário `NetworkSecurityRule` chamado **UserRule_Port80**, configurado tooblock o tráfego de entrada na porta 80.</span><span class="sxs-lookup"><span data-stu-id="cd639-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="cd639-127">Essas informações podem ser usadas tooresearch problemas de conexão.</span><span class="sxs-lookup"><span data-stu-id="cd639-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="cd639-128">Validar problemas de roteamento</span><span class="sxs-lookup"><span data-stu-id="cd639-128">Validate routing issues</span></span>

<span data-ttu-id="cd639-129">exemplo Hello verifica a conectividade entre uma máquina virtual e um ponto de extremidade remoto.</span><span class="sxs-lookup"><span data-stu-id="cd639-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="cd639-130">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cd639-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="cd639-131">Resposta</span><span class="sxs-lookup"><span data-stu-id="cd639-131">Response</span></span>

<span data-ttu-id="cd639-132">Em Olá exemplo a seguir, Olá `connectionStatus` é mostrado como **inacessível**.</span><span class="sxs-lookup"><span data-stu-id="cd639-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="cd639-133">Em Olá `hops` detalhes, você pode ver em `issues` que o tráfego de saudação foi bloqueado devido tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="cd639-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="cd639-134">Verificar a latência de site</span><span class="sxs-lookup"><span data-stu-id="cd639-134">Check website latency</span></span>

<span data-ttu-id="cd639-135">Olá exemplo verifica Olá conectividade tooa site a seguir.</span><span class="sxs-lookup"><span data-stu-id="cd639-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="cd639-136">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cd639-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="cd639-137">Resposta</span><span class="sxs-lookup"><span data-stu-id="cd639-137">Response</span></span>

<span data-ttu-id="cd639-138">Olá resposta a seguir, você pode ver Olá `connectionStatus` mostra como **alcançável**.</span><span class="sxs-lookup"><span data-stu-id="cd639-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="cd639-139">Quando uma conexão é bem-sucedida, os valores de latência são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="cd639-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="cd639-140">Verifique o ponto de extremidade de armazenamento de tooa conectividade</span><span class="sxs-lookup"><span data-stu-id="cd639-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="cd639-141">Olá exemplo a seguir verifica a saudação conectividade de uma conta de armazenamento de blog de tooa de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cd639-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="cd639-142">Exemplo</span><span class="sxs-lookup"><span data-stu-id="cd639-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="cd639-143">Resposta</span><span class="sxs-lookup"><span data-stu-id="cd639-143">Response</span></span>

<span data-ttu-id="cd639-144">Olá json a seguir é de resposta de exemplo hello de executar o cmdlet anterior hello.</span><span class="sxs-lookup"><span data-stu-id="cd639-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="cd639-145">Como a seleção de saudação for bem-sucedida, Olá `connectionStatus` propriedade mostra como **alcançável**.</span><span class="sxs-lookup"><span data-stu-id="cd639-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="cd639-146">São fornecidos detalhes de Olá relativos ao número de saudação do blob de armazenamento saltos tooreach necessário hello e latência.</span><span class="sxs-lookup"><span data-stu-id="cd639-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="cd639-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd639-147">Next steps</span></span>

<span data-ttu-id="cd639-148">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="cd639-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="cd639-149">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cd639-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
