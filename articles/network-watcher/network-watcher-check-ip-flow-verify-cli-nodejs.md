---
title: "tráfego de aaaVerify com Azure rede Inspetor IP fluxo verificar - CLI do Azure | Microsoft Docs"
description: "Este artigo descreve como toocheck se tooor de tráfego de uma máquina virtual é permitido ou negado usando a CLI do Azure"
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
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="a5e9e-103">Verifique se o tráfego é permitido ou negado tooor de uma VM com IP fluxo verificar um componente do observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e9e-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a5e9e-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e9e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="a5e9e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5e9e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="a5e9e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a5e9e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="a5e9e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a5e9e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="a5e9e-108">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e9e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="a5e9e-109">Fluxo de IP Verifique se é um recurso do observador de rede que permite que você tooverify se o tráfego é permitido tooor de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="a5e9e-110">Esse cenário é útil tooget um estado atual do se uma máquina virtual pode se comunicar recursos externos tooan ou back-end.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="a5e9e-111">Fluxo IP, verifique se pode ser usado tooverify se suas regras de grupo de segurança de rede (NSG) estão configuradas corretamente e solucionar problemas fluxos que estão sendo bloqueados por regras NSG.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="a5e9e-112">Outro motivo para usar IP fluxo Verifique se está tooensure tráfego que deseja bloquear está sendo bloqueado corretamente pelo Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="a5e9e-113">Este artigo usa a CLI 1.0 do Azure para plataforma cruzada, que está disponível para Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a5e9e-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a5e9e-114">Before you begin</span></span>

<span data-ttu-id="a5e9e-115">Este cenário pressupõe que você já seguiu etapas Olá [criar um observador de rede](network-watcher-create.md) toocreate um observador de rede ou ter uma instância existente do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="a5e9e-116">cenário de Olá também pressupõe que um grupo de recursos com uma máquina virtual válida existe toobe usado.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a5e9e-117">Cenário</span><span class="sxs-lookup"><span data-stu-id="a5e9e-117">Scenario</span></span>

<span data-ttu-id="a5e9e-118">Esse cenário usa tooverify IP fluxo verificar se uma máquina virtual pode se comunicar tooa conhecido endereço IP do Bing.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="a5e9e-119">Se Olá tráfego é negado, ele retornará regra de segurança de saudação que está negando esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="a5e9e-120">toolearn mais sobre IP fluxo verificar, visite [fluxo verificar a visão geral de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a5e9e-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="a5e9e-121">Obter uma VM</span><span class="sxs-lookup"><span data-stu-id="a5e9e-121">Get a VM</span></span>

<span data-ttu-id="a5e9e-122">Fluxo IP verificar tooor de tráfego de testes de um endereço IP no tooor máquina virtual de um destino remoto.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-122">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="a5e9e-123">Uma Id de uma máquina virtual é necessária para o cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="a5e9e-124">Se você já souber a ID de saudação do hello toouse de máquina virtual, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a><span data-ttu-id="a5e9e-125">Obter Olá NICS</span><span class="sxs-lookup"><span data-stu-id="a5e9e-125">Get hello NICS</span></span>

<span data-ttu-id="a5e9e-126">endereço IP de saudação de uma NIC na máquina virtual de saudação é necessária neste exemplo recuperamos Olá NICs em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-126">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="a5e9e-127">Se você já souber Olá IP endereço que você deseja tootest na máquina virtual de saudação, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-127">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="a5e9e-128">Executar a verificação de fluxo de IP</span><span class="sxs-lookup"><span data-stu-id="a5e9e-128">Run IP flow verify</span></span>

<span data-ttu-id="a5e9e-129">Agora que temos informações Olá necessário toorun Olá cmdlet, executamos Olá `network watcher ip-flow-verify` tráfego de saudação do cmdlet tootest.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-129">Now that we have hello information needed toorun hello cmdlet, we run hello `network watcher ip-flow-verify` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="a5e9e-130">Neste exemplo, estamos usando endereço IP primeiro Olá em Olá primeira NIC.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-130">In this example, we are using hello first IP address on hello first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="a5e9e-131">Fluxo de IP verificar requer que o recurso VM hello está alocado toorun.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-131">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="a5e9e-132">Analisar Resultados</span><span class="sxs-lookup"><span data-stu-id="a5e9e-132">Review Results</span></span>

<span data-ttu-id="a5e9e-133">Depois de executar `network watcher ip-flow-verify` Olá resultados são retornados, hello, exemplo a seguir é resultados Olá de saudação anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-133">After running `network watcher ip-flow-verify` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="a5e9e-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5e9e-134">Next steps</span></span>

<span data-ttu-id="a5e9e-135">Se o tráfego está sendo bloqueado e não deve ser, consulte [gerenciar grupos de segurança de rede](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack para baixo Olá rede segurança e o grupo de regras de segurança que são definidas.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="a5e9e-136">Saiba tooaudit suas configurações NSG visitando [auditoria rede segurança grupos (NSG) com o observador de rede](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9e-136">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
