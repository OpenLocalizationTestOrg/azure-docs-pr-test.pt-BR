---
title: "Verifique se o tráfego aaaVerify com fluxo de IP de Inspetor de rede do Azure - portal do Azure | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual é permitido ou negado"
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
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="34c6f-103">Verifique se o tráfego é permitido ou negado tooor de uma VM com IP fluxo verificar um componente do observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="34c6f-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="34c6f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="34c6f-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="34c6f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34c6f-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="34c6f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="34c6f-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="34c6f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34c6f-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="34c6f-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="34c6f-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="34c6f-109">Fluxo IP, verifique se é um recurso do observador de rede que permite que você tooverify se o tráfego é permitido tooor de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="34c6f-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="34c6f-110">validação de saudação pode ser executada para o tráfego de entrada ou saído.</span><span class="sxs-lookup"><span data-stu-id="34c6f-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="34c6f-111">Esse cenário é útil tooget um estado atual do se uma máquina virtual pode se comunicar recursos externos tooan ou outro recurso.</span><span class="sxs-lookup"><span data-stu-id="34c6f-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="34c6f-112">Fluxo IP, verifique se pode ser usado tooverify se suas regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas fluxos que estão sendo bloqueados por regras NSG.</span><span class="sxs-lookup"><span data-stu-id="34c6f-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="34c6f-113">Outro motivo para usar IP fluxo Verifique se está tooensure tráfego que deseja bloquear está sendo bloqueado corretamente pelo Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="34c6f-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="34c6f-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="34c6f-114">Before you begin</span></span>

<span data-ttu-id="34c6f-115">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="34c6f-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="34c6f-116">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="34c6f-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="34c6f-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="34c6f-117">Scenario</span></span>

<span data-ttu-id="34c6f-118">Esse cenário usa tooverify IP fluxo verificar se uma máquina virtual pode se comunicar tooanother máquina pela porta 443.</span><span class="sxs-lookup"><span data-stu-id="34c6f-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="34c6f-119">Se Olá tráfego é negado, ele retornará regra de segurança de saudação que está negando esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="34c6f-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="34c6f-120">toolearn mais sobre IP fluxo verificar, visite [fluxo verificar a visão geral de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="34c6f-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="34c6f-121">Executar a verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="34c6f-121">Run IP flow verify</span></span>

<span data-ttu-id="34c6f-122">Navegue tooyour observador de rede e clique em **Verifique se o fluxo IP**.</span><span class="sxs-lookup"><span data-stu-id="34c6f-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="34c6f-123">Selecione máquina virtual de saudação e interface de rede que você deseja que o tráfego de tooverify do.</span><span class="sxs-lookup"><span data-stu-id="34c6f-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="34c6f-124">Insira as informações adicionais de filtragem e clique em **Verificar**.</span><span class="sxs-lookup"><span data-stu-id="34c6f-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="34c6f-125">Depois de clicar em **verificar**, fluxo de saudação com base em critérios de saudação fornecida é verificado.</span><span class="sxs-lookup"><span data-stu-id="34c6f-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="34c6f-126">é o resultado de saudação **acesso permitido** ou **acesso negado**.</span><span class="sxs-lookup"><span data-stu-id="34c6f-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="34c6f-127">Se o acesso é negado, Olá o grupo de segurança de rede (NSG) e regra de segurança que bloqueiam o tráfego é fornecida.</span><span class="sxs-lookup"><span data-stu-id="34c6f-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="34c6f-128">Se a negação de saudação do tráfego é o comportamento esperado, regra Olá foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="34c6f-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="34c6f-129">Fluxo IP verificar requer que o recurso VM hello está alocado.</span><span class="sxs-lookup"><span data-stu-id="34c6f-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="34c6f-130">Como você pode ver da saudação imagem a seguir, o tráfego HTTPS de saída Olá foi permitido.</span><span class="sxs-lookup"><span data-stu-id="34c6f-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![visão geral da verificação de fluxo de IP][1]

<span data-ttu-id="34c6f-132">Conforme visto no Olá a imagem a seguir, o tráfego é alterado tooinbound e hello too123 alterada de porta de entrada.</span><span class="sxs-lookup"><span data-stu-id="34c6f-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="34c6f-133">O tráfego é negado Agora, mensagem de saudação "Acesso negado" é fornecida junto com hello rede segurança e o grupo de regra de segurança que negar o tráfego de saudação.</span><span class="sxs-lookup"><span data-stu-id="34c6f-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![resultados do fluxo de IP][2]

## <a name="next-steps"></a><span data-ttu-id="34c6f-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="34c6f-135">Next steps</span></span>

<span data-ttu-id="34c6f-136">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que são definidas.</span><span class="sxs-lookup"><span data-stu-id="34c6f-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













