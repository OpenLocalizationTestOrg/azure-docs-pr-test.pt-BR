---
title: "Verifique se o tráfego com a Verificação de Fluxo de IP do Observador de Rede do Azure - CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como verificar se o tráfego de ou para uma máquina virtual é permitido ou negado usando a CLI do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0b52257a6c38a4392573672b7190d2269c2f145a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="06266-103">Verifique se o tráfego é permitido ou negado para ou de uma VM com IP fluxo verificar um componente do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="06266-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="06266-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="06266-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="06266-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06266-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="06266-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="06266-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="06266-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="06266-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="06266-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="06266-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="06266-109">A Verificação de Fluxo de IP é um recurso do Observador de Rede que permite verificar se o tráfego é permitido para ou de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06266-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="06266-110">Esse cenário é útil para obter o estado atual de se uma máquina virtual pode se comunicar com um recurso externo ou um back-end.</span><span class="sxs-lookup"><span data-stu-id="06266-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="06266-111">A Verificação de Fluxo de IP pode ser usada para verificar se as regras do Grupo de Segurança de Rede (NSG) estão configuradas corretamente e solucionar problemas de fluxos que estão sendo bloqueados por regras do NSG.</span><span class="sxs-lookup"><span data-stu-id="06266-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="06266-112">Outro motivo para usar IP fluxo Verifique se é para garantir que deseja bloquear o tráfego está sendo bloqueado corretamente por NSG.</span><span class="sxs-lookup"><span data-stu-id="06266-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="06266-113">Este artigo usa nossa CLI de próxima geração para o modelo de implantação do gerenciamento de recursos, CLI do Azure 2.0, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="06266-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="06266-114">Para executar as etapas deste artigo, será necessário [instalar a Interface de Linha de Comando do Azure para Mac, Linux e Windows (CLI do Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="06266-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="06266-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="06266-115">Before you begin</span></span>

<span data-ttu-id="06266-116">Este cenário pressupõe que você já tenha seguido as etapas em [criar um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede ou ter uma instância existente do Gerenciador da rede.</span><span class="sxs-lookup"><span data-stu-id="06266-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="06266-117">O cenário também pressupõe que exista um grupo de recursos com uma máquina virtual válida a ser usada.</span><span class="sxs-lookup"><span data-stu-id="06266-117">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="06266-118">Cenário</span><span class="sxs-lookup"><span data-stu-id="06266-118">Scenario</span></span>

<span data-ttu-id="06266-119">Esse cenário usa o IP fluxo verificar para verificar se uma máquina virtual pode se comunicar com um endereço IP do Bing conhecido.</span><span class="sxs-lookup"><span data-stu-id="06266-119">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="06266-120">Se o tráfego é negado, ele retorna a regra de segurança que está negando esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="06266-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="06266-121">Para saber mais sobre IP fluxo verificar, visite [fluxo verificar visão geral de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="06266-121">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="06266-122">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="06266-122">Get a VM</span></span>

<span data-ttu-id="06266-123">A Verificação de Fluxo de IP testa o tráfego para ou de um endereço IP em uma máquina virtual ou de um destino remoto.</span><span class="sxs-lookup"><span data-stu-id="06266-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="06266-124">Uma Id de uma máquina virtual é necessária para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06266-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="06266-125">Se você já souber a ID da máquina virtual para usar, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="06266-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a><span data-ttu-id="06266-126">Obter as NICS</span><span class="sxs-lookup"><span data-stu-id="06266-126">Get the NICS</span></span>

<span data-ttu-id="06266-127">O endereço IP de uma NIC na máquina virtual é necessária neste exemplo, recuperamos as NICs em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="06266-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="06266-128">Se você já souber o endereço IP que você deseja testar na máquina virtual, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="06266-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="06266-129">Executar a verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="06266-129">Run IP flow verify</span></span>

<span data-ttu-id="06266-130">Agora que temos as informações necessárias para executar o cmdlet, executamos o `az network watcher test-ip-flow` para testar o tráfego.</span><span class="sxs-lookup"><span data-stu-id="06266-130">Now that we have the information needed to run the cmdlet, we run the `az network watcher test-ip-flow` cmdlet to test the traffic.</span></span> <span data-ttu-id="06266-131">Neste exemplo, estamos usando o primeiro endereço IP na primeira NIC.</span><span class="sxs-lookup"><span data-stu-id="06266-131">In this example, we are using the first IP address on the first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="06266-132">A Verificação de Fluxo de IP requer que o recurso de máquina virtual seja alocado para executar.</span><span class="sxs-lookup"><span data-stu-id="06266-132">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="06266-133">Analisar Resultados</span><span class="sxs-lookup"><span data-stu-id="06266-133">Review Results</span></span>

<span data-ttu-id="06266-134">Após a execução do `az network watcher test-ip-flow` os resultados são retornados, o exemplo a seguir é os resultados retornados da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="06266-134">After running `az network watcher test-ip-flow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="06266-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06266-135">Next steps</span></span>

<span data-ttu-id="06266-136">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para rastrear as rede segurança e grupo de regras de segurança que são definidas.</span><span class="sxs-lookup"><span data-stu-id="06266-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="06266-137">Aprenda a auditar as configurações de NSG visitando [auditoria de segurança grupos NSG (rede) com o Observador de Rede](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="06266-137">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
