---
title: "aaaFind próximo salto com Azure rede Inspetor de próximo salto - PowerShell | Microsoft Docs"
description: "Este artigo descreve como descobrir quais saudação do tipo de próximo salto é e usando o endereço ip do próximo salto usando o PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="6e7d3-103">Descobrir que tipo de próximo salto Olá está usando o recurso de próximo salto Olá no Inspetor de rede do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e7d3-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6e7d3-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e7d3-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="6e7d3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e7d3-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="6e7d3-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6e7d3-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="6e7d3-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6e7d3-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="6e7d3-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="6e7d3-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="6e7d3-109">Próximo salto é um recurso do observador de rede que fornece a capacidade de saudação tipo hello de próximo salto e o endereço IP com base em uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="6e7d3-110">Esse recurso é útil para determinar se o tráfego que deixa uma máquina virtual atravessa um gateway, internet ou redes virtuais tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6e7d3-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6e7d3-111">Before you begin</span></span>

<span data-ttu-id="6e7d3-112">Nesse cenário, você usará a saudação tipo toofind portal do Azure Olá de próximo salto e o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="6e7d3-113">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="6e7d3-114">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="6e7d3-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="6e7d3-115">Scenario</span></span>

<span data-ttu-id="6e7d3-116">cenário de saudação abordado neste artigo usa um recurso do observador de rede que localiza o tipo de próximo salto hello e endereço IP para um recurso de próximo salto.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="6e7d3-117">toolearn mais sobre o próximo nó, visite [visão geral próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e7d3-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="6e7d3-118">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="6e7d3-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="6e7d3-119">Olá primeira etapa é a instância do tooretrieve Olá observador de rede.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="6e7d3-120">Olá `$networkWatcher` variável é passada toohello próximo salto verificar cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="6e7d3-121">Obter uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6e7d3-121">Get a virtual machine</span></span>

<span data-ttu-id="6e7d3-122">Próximo salto retorna o próximo salto de saudação e endereço IP de saudação do próximo salto de saudação de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="6e7d3-123">Uma Id de uma máquina virtual é necessária para o cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="6e7d3-124">Se você já souber a ID de saudação do hello toouse de máquina virtual, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="6e7d3-125">Próximo salto requer que o recurso VM hello está alocado toorun.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="6e7d3-126">Obter interfaces de rede Olá</span><span class="sxs-lookup"><span data-stu-id="6e7d3-126">Get hello network interfaces</span></span>

<span data-ttu-id="6e7d3-127">endereço IP de saudação de uma NIC na máquina virtual de saudação é necessária neste exemplo recuperamos Olá NICs em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="6e7d3-128">Se você já souber Olá IP endereço que você deseja tootest na máquina virtual de saudação, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="6e7d3-129">Obter o próximo salto</span><span class="sxs-lookup"><span data-stu-id="6e7d3-129">Get Next Hop</span></span>

<span data-ttu-id="6e7d3-130">Agora podemos chamar hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="6e7d3-131">Podemos passar Olá cmdlet Olá observador de rede, a máquina virtual Id, endereço IP e endereço IP de destino de origem.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="6e7d3-132">Neste exemplo, o endereço IP de destino Olá é tooa VM em outra rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="6e7d3-133">Há um gateway de rede virtual entre duas redes virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="6e7d3-134">Analisar resultados</span><span class="sxs-lookup"><span data-stu-id="6e7d3-134">Review results</span></span>

<span data-ttu-id="6e7d3-135">Ao concluir, resultados de saudação são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-135">When complete, hello results are provided.</span></span> <span data-ttu-id="6e7d3-136">Olá próximo endereço IP será retornado, bem como o tipo de saudação do recurso é.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="6e7d3-137">Nesse cenário, é endereço IP público de saudação do gateway de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="6e7d3-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="6e7d3-138">Hello lista a seguir mostra valores de NextHopType disponíveis no momento da saudação:</span><span class="sxs-lookup"><span data-stu-id="6e7d3-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="6e7d3-139">**Tipo do próximo salto**</span><span class="sxs-lookup"><span data-stu-id="6e7d3-139">**Next Hop Type**</span></span>

* <span data-ttu-id="6e7d3-140">Internet</span><span class="sxs-lookup"><span data-stu-id="6e7d3-140">Internet</span></span>
* <span data-ttu-id="6e7d3-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="6e7d3-141">VirtualAppliance</span></span>
* <span data-ttu-id="6e7d3-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="6e7d3-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="6e7d3-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="6e7d3-143">VnetLocal</span></span>
* <span data-ttu-id="6e7d3-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="6e7d3-144">HyperNetGateway</span></span>
* <span data-ttu-id="6e7d3-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="6e7d3-145">VnetPeering</span></span>
* <span data-ttu-id="6e7d3-146">Nenhum</span><span class="sxs-lookup"><span data-stu-id="6e7d3-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e7d3-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e7d3-147">Next steps</span></span>

<span data-ttu-id="6e7d3-148">Saiba como tooreview as configurações de grupo de segurança de rede por meio de programação visitando [NSG auditoria com o observador de rede](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="6e7d3-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















