---
title: "Verifique se o tráfego com a verificação de fluxo de IP do Observador de Rede do Azure – PowerShell | Microsoft Docs"
description: "Este artigo descreve como verificar se o tráfego de ou para uma máquina virtual é permitido ou negado usando o PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: bf0c01a9af0e28647d11ad89a9d164716d5c8312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="f36ce-103">Verifique se o tráfego é permitido ou negado de ou para uma VM com uma verificação de fluxo de IP, um componente do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="f36ce-103">Check if traffic is allowed or denied to or from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f36ce-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f36ce-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="f36ce-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f36ce-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="f36ce-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f36ce-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="f36ce-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f36ce-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="f36ce-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="f36ce-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="f36ce-109">Fluxo de IP Verifique se é um recurso do Observador de Rede que permite verificar se o tráfego é permitido para ou de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f36ce-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="f36ce-110">Esse cenário é útil para obter o estado atual de se uma máquina virtual pode se comunicar com um recurso externo ou um back-end.</span><span class="sxs-lookup"><span data-stu-id="f36ce-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="f36ce-111">A Verificação de Fluxo de IP pode ser usada para verificar se as regras do Grupo de Segurança de Rede (NSG) estão configuradas corretamente e solucionar problemas de fluxos que estão sendo bloqueados por regras do NSG.</span><span class="sxs-lookup"><span data-stu-id="f36ce-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="f36ce-112">Outro motivo para usar IP fluxo Verifique se é para garantir que deseja bloquear o tráfego está sendo bloqueado corretamente por NSG.</span><span class="sxs-lookup"><span data-stu-id="f36ce-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f36ce-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f36ce-113">Before you begin</span></span>

<span data-ttu-id="f36ce-114">Este cenário pressupõe que você já tenha seguido as etapas em [criar um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede ou ter uma instância existente do Gerenciador da rede.</span><span class="sxs-lookup"><span data-stu-id="f36ce-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="f36ce-115">O cenário também pressupõe que exista um grupo de recursos com uma máquina virtual válida a ser usada.</span><span class="sxs-lookup"><span data-stu-id="f36ce-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f36ce-116">Cenário</span><span class="sxs-lookup"><span data-stu-id="f36ce-116">Scenario</span></span>

<span data-ttu-id="f36ce-117">Esse cenário usa a verificação de fluxo de IP para verificar se uma máquina virtual pode se comunicar com um endereço IP do Bing conhecido.</span><span class="sxs-lookup"><span data-stu-id="f36ce-117">This scenario uses IP flow verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="f36ce-118">Se o tráfego é negado, ele retorna a regra de segurança que está negando esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="f36ce-118">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="f36ce-119">Para saber mais sobre a verificação de fluxo de IP, visite [Visão geral de verificação de fluxo de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f36ce-119">To learn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="f36ce-120">Recuperar o Observador de Rede</span><span class="sxs-lookup"><span data-stu-id="f36ce-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="f36ce-121">A primeira etapa é recuperar a instância do Observador de Rede.</span><span class="sxs-lookup"><span data-stu-id="f36ce-121">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="f36ce-122">A variável `$networkWatcher` é passada para o cmdlet verificação de fluxo de IP.</span><span class="sxs-lookup"><span data-stu-id="f36ce-122">The `$networkWatcher` variable is passed to the IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="f36ce-123">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="f36ce-123">Get a VM</span></span>

<span data-ttu-id="f36ce-124">A Verificação de Fluxo de IP testa o tráfego para ou de um endereço IP em uma máquina virtual ou de um destino remoto.</span><span class="sxs-lookup"><span data-stu-id="f36ce-124">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="f36ce-125">Uma Id de uma máquina virtual é necessária para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f36ce-125">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="f36ce-126">Se você já souber a ID da máquina virtual para usar, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="f36ce-126">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-the-nics"></a><span data-ttu-id="f36ce-127">Obter as NICS</span><span class="sxs-lookup"><span data-stu-id="f36ce-127">Get the NICS</span></span>

<span data-ttu-id="f36ce-128">O endereço IP de uma NIC na máquina virtual é necessária neste exemplo, recuperamos as NICs em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f36ce-128">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="f36ce-129">Se você já souber o endereço IP que você deseja testar na máquina virtual, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="f36ce-129">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="f36ce-130">Executar a verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="f36ce-130">Run IP flow verify</span></span>

<span data-ttu-id="f36ce-131">Agora que temos as informações necessárias para executar o cmdlet, executamos o `Test-AzureRmNetworkWatcherIPFlow` para testar o tráfego.</span><span class="sxs-lookup"><span data-stu-id="f36ce-131">Now that we have the information needed to run the cmdlet, we run the `Test-AzureRmNetworkWatcherIPFlow` cmdlet to test the traffic.</span></span> <span data-ttu-id="f36ce-132">Neste exemplo, estamos usando o primeiro endereço IP na primeira NIC.</span><span class="sxs-lookup"><span data-stu-id="f36ce-132">In this example, we are using the first IP address on the first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="f36ce-133">A verificação de fluxo de IP requer que o recurso de VM esteja alocado para que possa ser executada.</span><span class="sxs-lookup"><span data-stu-id="f36ce-133">IP flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="f36ce-134">Analisar Resultados</span><span class="sxs-lookup"><span data-stu-id="f36ce-134">Review Results</span></span>

<span data-ttu-id="f36ce-135">Após a execução do `Test-AzureRmNetworkWatcherIPFlow` os resultados são retornados, o exemplo a seguir é os resultados retornados da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f36ce-135">After running `Test-AzureRmNetworkWatcherIPFlow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="f36ce-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f36ce-136">Next steps</span></span>

<span data-ttu-id="f36ce-137">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para rastrear as rede segurança e grupo de regras de segurança que são definidas.</span><span class="sxs-lookup"><span data-stu-id="f36ce-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













