---
title: "Localizar próximo salto com o Próximo Salto do Observador de Rede do Azure - REST | Microsoft Docs"
description: "Este artigo descreve como você pode encontrar o que é o tipo do próximo salto e o endereço ip com o próximo salto usando a API REST do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="960a7-103">Descubra qual o tipo do próximo salto é usando o recurso de próximo salto no Observador de Rede do Azure usando a API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="960a7-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="960a7-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="960a7-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="960a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="960a7-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="960a7-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="960a7-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="960a7-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="960a7-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="960a7-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="960a7-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="960a7-109">Próximo salto é um recurso do Observador de Rede fornece o capacidade de obter o tipo do próximo salto e o endereço IP com base em uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="960a7-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="960a7-110">Esse recurso é útil para determinar se o tráfego deixar uma máquina virtual atravessa um gateway, internet ou redes virtuais para chegar ao seu destino.</span><span class="sxs-lookup"><span data-stu-id="960a7-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="960a7-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="960a7-111">Before you begin</span></span>

<span data-ttu-id="960a7-112">O ARMclient é usado para chamar a API REST usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="960a7-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="960a7-113">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="960a7-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="960a7-114">Este cenário pressupõe que você seguiu as etapas em [Criação de um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="960a7-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="960a7-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="960a7-115">Scenario</span></span>

<span data-ttu-id="960a7-116">O cenário abordado neste artigo usa o próximo salto, um recurso do Observador de Rede que localiza o tipo do próximo salto e o endereço IP para um recurso.</span><span class="sxs-lookup"><span data-stu-id="960a7-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="960a7-117">Para saber mais sobre o próximo nó, visite [Visão geral do próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="960a7-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="960a7-118">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="960a7-118">In this scenario, you will:</span></span>

* <span data-ttu-id="960a7-119">Recuperará o próximo salto de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="960a7-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="960a7-120">Faça logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="960a7-120">Log in with ARMClient</span></span>

<span data-ttu-id="960a7-121">Faça logon no armclient com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="960a7-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="960a7-122">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="960a7-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="960a7-123">Execute o script a seguir para retornar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="960a7-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="960a7-124">Essas informações são necessárias para a execução do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="960a7-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="960a7-125">O código a seguir precisa de valores para as variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="960a7-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="960a7-126">**subscriptionId** - A Id da assinatura a ser usada.</span><span class="sxs-lookup"><span data-stu-id="960a7-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="960a7-127">**resourceGroupName** - o nome de um grupo de recursos que contém as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="960a7-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="960a7-128">Na saída a seguir, a id da máquina virtual é usada no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="960a7-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="960a7-129">Obter o próximo salto</span><span class="sxs-lookup"><span data-stu-id="960a7-129">Get Next Hop</span></span>

<span data-ttu-id="960a7-130">Depois de criar o cabeçalho de autorização, o próximo salto de uma máquina virtual pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="960a7-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="960a7-131">Os valores a seguir devem ser substituídos para que o exemplo de código funcione.</span><span class="sxs-lookup"><span data-stu-id="960a7-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="960a7-132">Para chamadas da API REST do Observador de Rede o nome do grupo de recursos no URI da solicitação é o grupo de recursos que contém o Observador de Rede, não os recursos nos quais você está executando as ações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="960a7-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="960a7-133">O próximo salto exige a alocação do recurso de VM para ser executado.</span><span class="sxs-lookup"><span data-stu-id="960a7-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="960a7-134">Resultados</span><span class="sxs-lookup"><span data-stu-id="960a7-134">Results</span></span>

<span data-ttu-id="960a7-135">O trecho a seguir é um exemplo da saída recebida.</span><span class="sxs-lookup"><span data-stu-id="960a7-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="960a7-136">Os resultados contêm os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="960a7-136">The results contain the following values:</span></span>

* <span data-ttu-id="960a7-137">**nextHopType** - Esse valor pode ser um dos seguintes valores: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway ou Nenhum.</span><span class="sxs-lookup"><span data-stu-id="960a7-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="960a7-138">**nextHopIpAddress** - o endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="960a7-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="960a7-139">**routeTableId** - O valor é um uri para a tabela de rotas associada à rota, ou se nenhuma rota for definida pelo usuário o valor *Rota do Sistema* retornará.</span><span class="sxs-lookup"><span data-stu-id="960a7-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="960a7-140">Veja a seguir os resultados no formato json.</span><span class="sxs-lookup"><span data-stu-id="960a7-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="960a7-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="960a7-141">Next steps</span></span>

<span data-ttu-id="960a7-142">Depois que você conseguir descobrir o próximo salto para uma máquina virtual, exiba a segurança de seus recursos de rede visitando [Visão geral do modo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="960a7-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














