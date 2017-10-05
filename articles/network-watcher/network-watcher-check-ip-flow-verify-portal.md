---
title: "Verificar o tráfego com a verificação de fluxo de IP do Observador de Rede do Azure - Portal do Azure | Microsoft Docs"
description: "Esse artigo descreve como verificar se o tráfego de ou para uma máquina virtual é permitido ou negado"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="79db4-103">Verifique se o tráfego é permitido ou negado para ou de uma VM com IP fluxo verificar um componente do Observador de Rede do Azure</span><span class="sxs-lookup"><span data-stu-id="79db4-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="79db4-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="79db4-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="79db4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79db4-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="79db4-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="79db4-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="79db4-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="79db4-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="79db4-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="79db4-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="79db4-109">Fluxo de IP Verifique se é um recurso do Observador de Rede que permite verificar se o tráfego é permitido para ou de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="79db4-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="79db4-110">A validação pode ser executada para o tráfego de entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="79db4-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="79db4-111">Esse cenário é útil para obter o estado atual de condição de uma máquina virtual poder se comunicar com um recurso externo ou outro recurso.</span><span class="sxs-lookup"><span data-stu-id="79db4-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="79db4-112">Fluxo IP, verifique se pode ser usado para verificar se as regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas de fluxos que estão sendo bloqueados por regras NSG.</span><span class="sxs-lookup"><span data-stu-id="79db4-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="79db4-113">Outro motivo para usar IP fluxo Verifique se é para garantir que deseja bloquear o tráfego está sendo bloqueado corretamente por NSG.</span><span class="sxs-lookup"><span data-stu-id="79db4-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="79db4-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="79db4-114">Before you begin</span></span>

<span data-ttu-id="79db4-115">Este cenário pressupõe que você já tenha seguido as etapas em [criar um Observador de Rede](network-watcher-create.md) para criar um Observador de Rede ou ter uma instância existente do Gerenciador da rede.</span><span class="sxs-lookup"><span data-stu-id="79db4-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="79db4-116">O cenário também pressupõe que exista um grupo de recursos com uma máquina virtual válida a ser usada.</span><span class="sxs-lookup"><span data-stu-id="79db4-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="79db4-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="79db4-117">Scenario</span></span>

<span data-ttu-id="79db4-118">Esse cenário usa a Verificação de Fluxo de IP para verificar se uma máquina virtual pode se comunicar com outra máquina pela porta 443.</span><span class="sxs-lookup"><span data-stu-id="79db4-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="79db4-119">Se o tráfego é negado, ele retorna a regra de segurança que está negando esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="79db4-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="79db4-120">Para saber mais sobre IP fluxo verificar, visite [fluxo verificar visão geral de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="79db4-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="79db4-121">Executar a verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="79db4-121">Run IP flow verify</span></span>

<span data-ttu-id="79db4-122">Navegue até o Observador de Rede e clique em **Verificação de fluxo de IP**.</span><span class="sxs-lookup"><span data-stu-id="79db4-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="79db4-123">Selecione a máquina virtual e a interface de rede a partir da qual você deseja verificar.</span><span class="sxs-lookup"><span data-stu-id="79db4-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="79db4-124">Insira as informações adicionais de filtragem e clique em **Verificar**.</span><span class="sxs-lookup"><span data-stu-id="79db4-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="79db4-125">Após clicar em **Verificar**, o fluxo com base nos critérios que você forneceu será verificado.</span><span class="sxs-lookup"><span data-stu-id="79db4-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="79db4-126">O resultado é **Acesso permitido** ou **Acesso negado**.</span><span class="sxs-lookup"><span data-stu-id="79db4-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="79db4-127">Se o acesso for negado, o NSG (Grupo de segurança de rede) e a regra de segurança que bloqueiam o tráfego serão fornecidos.</span><span class="sxs-lookup"><span data-stu-id="79db4-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="79db4-128">Se a negação do tráfego for o comportamento esperado, a regra terá sido bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="79db4-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="79db4-129">A verificação de fluxo de IP exige que o recurso de máquina virtual seja alocado.</span><span class="sxs-lookup"><span data-stu-id="79db4-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="79db4-130">Como você pode ver na imagem a seguir, o tráfego HTTPS de saída foi permitido.</span><span class="sxs-lookup"><span data-stu-id="79db4-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![visão geral da verificação de fluxo de IP][1]

<span data-ttu-id="79db4-132">Conforme a imagem a seguir mostra, o tráfego é alterado para entrada e a porta de entrada para 123.</span><span class="sxs-lookup"><span data-stu-id="79db4-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="79db4-133">O tráfego agora é negado, a mensagem "Acesso negado" é fornecida junto com o grupo de segurança de rede e a regra de segurança que negam o tráfego.</span><span class="sxs-lookup"><span data-stu-id="79db4-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![resultados do fluxo de IP][2]

## <a name="next-steps"></a><span data-ttu-id="79db4-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79db4-135">Next steps</span></span>

<span data-ttu-id="79db4-136">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para rastrear as rede segurança e grupo de regras de segurança que são definidas.</span><span class="sxs-lookup"><span data-stu-id="79db4-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













