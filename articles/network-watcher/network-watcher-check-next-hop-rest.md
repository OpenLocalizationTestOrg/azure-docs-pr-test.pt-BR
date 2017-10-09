---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - REST | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e endereço ip usando próximo salto Olá API REST do Azure"
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
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="3511f-103">Descobrir que tipo de próximo salto hello está usando o recurso de próximo salto Olá no Aure observador de rede usando a API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="3511f-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3511f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3511f-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="3511f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3511f-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="3511f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3511f-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="3511f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3511f-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="3511f-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="3511f-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="3511f-109">Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="3511f-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="3511f-110">Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="3511f-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3511f-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3511f-111">Before you begin</span></span>

<span data-ttu-id="3511f-112">ARMclient é toocall usado Olá REST API usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3511f-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="3511f-113">O ARMClient é encontrado no chocolatey em [ARMClient no Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="3511f-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="3511f-114">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="3511f-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="3511f-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="3511f-115">Scenario</span></span>

<span data-ttu-id="3511f-116">cenário de saudação abordado neste artigo usa um recurso do observador de rede que localiza o tipo de próximo salto hello e endereço IP para um recurso de próximo salto.</span><span class="sxs-lookup"><span data-stu-id="3511f-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="3511f-117">toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3511f-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="3511f-118">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="3511f-118">In this scenario, you will:</span></span>

* <span data-ttu-id="3511f-119">Recupere o próximo salto Olá para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3511f-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="3511f-120">Fazer logon com o ARMClient</span><span class="sxs-lookup"><span data-stu-id="3511f-120">Log in with ARMClient</span></span>

<span data-ttu-id="3511f-121">Faça logon no tooarmclient com suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="3511f-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="3511f-122">Recuperar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3511f-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="3511f-123">Execute Olá tooreturn de script a seguir em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3511f-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="3511f-124">Essas informações são necessárias para a execução do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="3511f-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="3511f-125">saudação de código a seguir precisa de valores para Olá variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="3511f-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="3511f-126">**subscriptionId** -Olá toouse de Id de assinatura.</span><span class="sxs-lookup"><span data-stu-id="3511f-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="3511f-127">**resourceGroupName** - Olá nome de um grupo de recursos que contém máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="3511f-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="3511f-128">De saída a seguir hello, id de saudação da máquina virtual de saudação é usado em Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3511f-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="3511f-129">Obter o próximo salto</span><span class="sxs-lookup"><span data-stu-id="3511f-129">Get Next Hop</span></span>

<span data-ttu-id="3511f-130">Depois de criar o cabeçalho de autorização hello, próximo salto saudação de uma máquina virtual pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="3511f-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="3511f-131">Olá valores a seguir devem ser substituídos para Olá toowork de exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="3511f-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="3511f-132">Para a API de REST do Inspetor de rede chamadas Olá nome do grupo de recursos na solicitação Olá que URI é o grupo de recursos de saudação que contém Olá observador de rede, não os recursos de saudação estiver executando ações de diagnóstico Olá em.</span><span class="sxs-lookup"><span data-stu-id="3511f-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

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
> <span data-ttu-id="3511f-133">Próximo salto requer que o recurso VM hello está alocado toorun.</span><span class="sxs-lookup"><span data-stu-id="3511f-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="3511f-134">Resultados</span><span class="sxs-lookup"><span data-stu-id="3511f-134">Results</span></span>

<span data-ttu-id="3511f-135">Olá trecho a seguir é um exemplo de saída de hello recebida.</span><span class="sxs-lookup"><span data-stu-id="3511f-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="3511f-136">resultados de saudação contêm Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="3511f-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="3511f-137">**nextHopType** -esse valor é um Olá valores a seguir: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway ou None.</span><span class="sxs-lookup"><span data-stu-id="3511f-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="3511f-138">**nextHopIpAddress** -Olá o endereço IP do próximo salto de saudação.</span><span class="sxs-lookup"><span data-stu-id="3511f-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="3511f-139">**routeTableId** - valor hello ou um uri para tabela de rota de saudação associada à rota hello, ou se não definida pelo usuário rota está valor definido Olá *sistema rota* é retornado.</span><span class="sxs-lookup"><span data-stu-id="3511f-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="3511f-140">Olá seguem resultados Olá no formato json.</span><span class="sxs-lookup"><span data-stu-id="3511f-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="3511f-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3511f-141">Next steps</span></span>

<span data-ttu-id="3511f-142">Depois de ter sido capaz de toofind-out de próximo salto Olá para uma máquina virtual, você pode exibir segurança Olá dos recursos da rede visitando [visão geral do modo de segurança](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3511f-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














