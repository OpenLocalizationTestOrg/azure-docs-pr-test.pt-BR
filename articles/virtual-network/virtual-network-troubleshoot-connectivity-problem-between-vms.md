---
title: "aaaTroubleshooting problemas de conectividade entre máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba como tooTroubleshoot Olá problemas de conectividade entre máquinas virtuais do Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="8f024-103">Solucionar problemas de conectividade entre VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="8f024-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="8f024-104">Você pode enfrentar problemas de conectividade entre máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f024-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="8f024-105">Este artigo fornece toohelp de etapas de solução de problemas é resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="8f024-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="8f024-106">Sintoma</span><span class="sxs-lookup"><span data-stu-id="8f024-106">Symptom</span></span>

<span data-ttu-id="8f024-107">Uma VM do Azure não pode se conectar a tooanother VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f024-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="8f024-108">Diretriz de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="8f024-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="8f024-109">Verifique se o NIC está configurada incorretamente</span><span class="sxs-lookup"><span data-stu-id="8f024-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="8f024-110">Verifique se o tráfego de rede está bloqueado por NSG ou UDR</span><span class="sxs-lookup"><span data-stu-id="8f024-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="8f024-111">Verifique se o tráfego de rede é bloqueado pelo firewall da VM</span><span class="sxs-lookup"><span data-stu-id="8f024-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="8f024-112">Verifique se o aplicativo de máquina virtual ou serviço está escutando na porta de Olá</span><span class="sxs-lookup"><span data-stu-id="8f024-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="8f024-113">Verifique se o problema de saudação é causado por SNAT</span><span class="sxs-lookup"><span data-stu-id="8f024-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="8f024-114">Verifique se o tráfego é bloqueado por ACLs para Olá VM clássico</span><span class="sxs-lookup"><span data-stu-id="8f024-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="8f024-115">Verifique se o ponto de extremidade de saudação é criado para Olá VM clássico</span><span class="sxs-lookup"><span data-stu-id="8f024-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="8f024-116">Compartilhamento de rede VM não é possível tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="8f024-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="8f024-117">Conectividade de rede entre virtuais</span><span class="sxs-lookup"><span data-stu-id="8f024-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="8f024-118">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8f024-118">Troubleshooting steps</span></span>

<span data-ttu-id="8f024-119">Siga o problema de saudação de tootroubleshoot essas etapas.</span><span class="sxs-lookup"><span data-stu-id="8f024-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="8f024-120">Verifique se o problema de saudação for resolvido após cada etapa.</span><span class="sxs-lookup"><span data-stu-id="8f024-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="8f024-121">Etapa 1: Verificar se o NIC está configurada incorretamente</span><span class="sxs-lookup"><span data-stu-id="8f024-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="8f024-122">Execute [como tooreset interface de rede de VM do Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="8f024-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="8f024-123">Se o problema de saudação ocorre depois de modificar a interface de rede (NIC) do hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8f024-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="8f024-124">**VMs de NIC redimensionável**</span><span class="sxs-lookup"><span data-stu-id="8f024-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="8f024-125">Adicionar um NIC.</span><span class="sxs-lookup"><span data-stu-id="8f024-125">Add a NIC.</span></span>
2. <span data-ttu-id="8f024-126">Corrigir problemas de saudação em Olá incorreta NIC ou remover NIC inválida.</span><span class="sxs-lookup"><span data-stu-id="8f024-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="8f024-127">Em seguida, readd NIC hello.</span><span class="sxs-lookup"><span data-stu-id="8f024-127">Then readd hello NIC.</span></span>

<span data-ttu-id="8f024-128">Para obter mais informações, consulte [remover adicionar tooor de interfaces de rede de máquinas virtuais](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="8f024-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="8f024-129">**VM com NIC único**</span><span class="sxs-lookup"><span data-stu-id="8f024-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="8f024-130">Reimplantar VM do Windows</span><span class="sxs-lookup"><span data-stu-id="8f024-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="8f024-131">Reimplantar VM Linux</span><span class="sxs-lookup"><span data-stu-id="8f024-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="8f024-132">Etapa 2: Verifique se o tráfego de rede está bloqueado por NSG ou UDR</span><span class="sxs-lookup"><span data-stu-id="8f024-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="8f024-133">Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="8f024-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="8f024-134">Etapa 3: Verifique se o tráfego de rede é bloqueado pelo firewall da VM</span><span class="sxs-lookup"><span data-stu-id="8f024-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="8f024-135">Desabilitar Olá firewall e teste o resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f024-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="8f024-136">Se Olá problema for resolvido, validar as configurações de saudação no firewall hello e habilite novamente.</span><span class="sxs-lookup"><span data-stu-id="8f024-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="8f024-137">Etapa 4: Verifique se o aplicativo de máquina virtual ou serviço está escutando na porta de Olá</span><span class="sxs-lookup"><span data-stu-id="8f024-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="8f024-138">Você pode usar uma saudação toocheck métodos a seguir se VM aplicativo ou serviço está escutando na porta Olá</span><span class="sxs-lookup"><span data-stu-id="8f024-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="8f024-139">Execute Olá toocheck comandos a seguir se Olá servidor está escutando nessa porta.</span><span class="sxs-lookup"><span data-stu-id="8f024-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="8f024-140">**VM Windows**</span><span class="sxs-lookup"><span data-stu-id="8f024-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="8f024-141">**VM Linux**</span><span class="sxs-lookup"><span data-stu-id="8f024-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="8f024-142">Executar Olá **Telnet** comando Olá porta de saudação do VM tooitself tootest.</span><span class="sxs-lookup"><span data-stu-id="8f024-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="8f024-143">Se Olá teste falhar, aplicativo ou serviço não é toolisten configurado na porta hello.</span><span class="sxs-lookup"><span data-stu-id="8f024-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="8f024-144">Etapa 5: Verificar se o problema de saudação é causado por SNAT</span><span class="sxs-lookup"><span data-stu-id="8f024-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="8f024-145">Em alguns cenários, hello VM é colocada atrás de uma solução de balanceamento de carga que tem uma dependência em recursos fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f024-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="8f024-146">Nesses cenários, se você tiver problemas de conexão intermitente, Olá problema pode ser causado por [esgotamento de porta SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="8f024-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="8f024-147">problema de saudação tooresolve, crie um VIP (ou ILPIP para clássico) para cada VM que está por trás do balanceador de carga Olá e proteger com ACL ou NSG.</span><span class="sxs-lookup"><span data-stu-id="8f024-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="8f024-148">Etapa 6: Verifique se o tráfego é bloqueado por ACLs para Olá VM clássico</span><span class="sxs-lookup"><span data-stu-id="8f024-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="8f024-149">Uma ACL fornece Olá capacidade tooselectively permitir ou negar o tráfego para um ponto de extremidade de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f024-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="8f024-150">Para obter mais informações, consulte [gerenciar Olá ACL em um ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="8f024-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="8f024-151">Etapa 7: Verifique se o ponto de extremidade de saudação é criado para Olá VM clássico</span><span class="sxs-lookup"><span data-stu-id="8f024-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="8f024-152">Todas as máquinas virtuais que você criar no Azure usando o modelo de implantação clássico Olá podem se comunicar automaticamente por um canal de rede privada com outras máquinas virtuais no hello que mesmo serviço ou de rede virtual na nuvem.</span><span class="sxs-lookup"><span data-stu-id="8f024-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="8f024-153">No entanto, os computadores em outras redes virtuais requerem pontos de extremidade toodirect Olá rede de entrada tráfego tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f024-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="8f024-154">Para obter mais informações, consulte [como tooset pontos de extremidade](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="8f024-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="8f024-155">Etapa 8: O compartilhamento de rede VM não é possível tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="8f024-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="8f024-156">Se você for um compartilhamento de rede VM não é possível tooconnect tooa, problema de saudação pode ser causado por NICs indisponíveis em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8f024-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="8f024-157">toodelete Olá NICs disponíveis, consulte [como toodelete Olá NICs indisponíveis](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="8f024-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="8f024-158">Etapa 9: Conectividade de rede entre virtuais</span><span class="sxs-lookup"><span data-stu-id="8f024-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="8f024-159">Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="8f024-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="8f024-160">Você também pode validar a configuração de rede entre [aqui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="8f024-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="8f024-161">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="8f024-161">Need help?</span></span> <span data-ttu-id="8f024-162">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="8f024-162">Contact support.</span></span>
<span data-ttu-id="8f024-163">Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="8f024-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
