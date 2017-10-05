---
title: Solucionar problemas de conectividade entre VMs do Azure | Microsoft Docs
description: Saiba como solucionar os problemas de conectividade entre VMs do Azure.
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
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="0f424-103">Solucionar problemas de conectividade entre VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="0f424-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="0f424-104">Você pode enfrentar problemas de conectividade entre máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f424-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="0f424-105">Este artigo apresenta etapas para a solução de problemas para ajudá-lo a resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="0f424-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="0f424-106">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0f424-106">Symptom</span></span>

<span data-ttu-id="0f424-107">Uma VM do Azure não pode se conectar a outra VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f424-107">An Azure VM cannot connect to another Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="0f424-108">Diretriz de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="0f424-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="0f424-109">Verifique se o NIC está configurada incorretamente</span><span class="sxs-lookup"><span data-stu-id="0f424-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="0f424-110">Verifique se o tráfego de rede está bloqueado por NSG ou UDR</span><span class="sxs-lookup"><span data-stu-id="0f424-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="0f424-111">Verifique se o tráfego de rede é bloqueado pelo firewall da VM</span><span class="sxs-lookup"><span data-stu-id="0f424-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="0f424-112">Verifique se o aplicativo ou serviço de VM está escutando na porta</span><span class="sxs-lookup"><span data-stu-id="0f424-112">Check whether VM app or service is listening on the port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="0f424-113">Verifique se o problema é causado por SNAT</span><span class="sxs-lookup"><span data-stu-id="0f424-113">Check whether the problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="0f424-114">Verifique se o tráfego está bloqueado por ACLs para a VM clássica</span><span class="sxs-lookup"><span data-stu-id="0f424-114">Check whether traffic is blocked by ACLs for the classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="0f424-115">Verifique se o ponto de extremidade é criado para a VM clássica</span><span class="sxs-lookup"><span data-stu-id="0f424-115">Check whether the endpoint is created for the classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="0f424-116">Não é possível conectar a um compartilhamento de rede VM</span><span class="sxs-lookup"><span data-stu-id="0f424-116">Unable to connect to a VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="0f424-117">Conectividade de rede entre virtuais</span><span class="sxs-lookup"><span data-stu-id="0f424-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="0f424-118">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="0f424-118">Troubleshooting steps</span></span>

<span data-ttu-id="0f424-119">Execute estas etapas para solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="0f424-119">Follow these steps to troubleshoot the problem.</span></span> <span data-ttu-id="0f424-120">Verifique se o problema for resolvido após cada etapa.</span><span class="sxs-lookup"><span data-stu-id="0f424-120">Check whether the problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="0f424-121">Etapa 1: Verificar se o NIC está configurada incorretamente</span><span class="sxs-lookup"><span data-stu-id="0f424-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="0f424-122">Execute [como redefinir a interface de rede de VM do Windows Azure](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="0f424-122">Follow [How to reset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="0f424-123">Se o problema ocorrer após você modificar o NIC (adaptador de rede), execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0f424-123">If the problem occurs after you modify the network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="0f424-124">**VMs de NIC redimensionável**</span><span class="sxs-lookup"><span data-stu-id="0f424-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="0f424-125">Adicionar um NIC.</span><span class="sxs-lookup"><span data-stu-id="0f424-125">Add a NIC.</span></span>
2. <span data-ttu-id="0f424-126">Corrija os problemas no NIC incorreta ou remover NIC inválida.</span><span class="sxs-lookup"><span data-stu-id="0f424-126">Fix the problems in the bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="0f424-127">Em seguida, readd NIC.</span><span class="sxs-lookup"><span data-stu-id="0f424-127">Then readd the NIC.</span></span>

<span data-ttu-id="0f424-128">Para saber mais, confira [Adicionar ou remover adaptadores de rede de máquinas virtuais](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0f424-128">For more information, see [Add network interfaces to or remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="0f424-129">**VM com NIC único**</span><span class="sxs-lookup"><span data-stu-id="0f424-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="0f424-130">Reimplantar VM do Windows</span><span class="sxs-lookup"><span data-stu-id="0f424-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="0f424-131">Reimplantar VM Linux</span><span class="sxs-lookup"><span data-stu-id="0f424-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="0f424-132">Etapa 2: Verifique se o tráfego de rede está bloqueado por NSG ou UDR</span><span class="sxs-lookup"><span data-stu-id="0f424-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="0f424-133">Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) para identificar se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="0f424-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="0f424-134">Etapa 3: Verifique se o tráfego de rede é bloqueado pelo firewall da VM</span><span class="sxs-lookup"><span data-stu-id="0f424-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="0f424-135">Desabilite o firewall e teste o resultado.</span><span class="sxs-lookup"><span data-stu-id="0f424-135">Disable the firewall, and then test the result.</span></span> <span data-ttu-id="0f424-136">Se o problema for resolvido, valide as configurações no firewall e habilitar novamente.</span><span class="sxs-lookup"><span data-stu-id="0f424-136">If the problem is resolved, validate the settings in the firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a><span data-ttu-id="0f424-137">Etapa 4: verificar se o aplicativo ou serviço de VM está escutando na porta</span><span class="sxs-lookup"><span data-stu-id="0f424-137">Step 4: Check whether VM app or service is listening on the port</span></span>

<span data-ttu-id="0f424-138">Você pode usar um dos métodos a seguir para verificar se a VM de aplicativo ou serviço está escutando na porta</span><span class="sxs-lookup"><span data-stu-id="0f424-138">You can use one of the following methods to check whether VM Application or Service is listening on the port</span></span>

- <span data-ttu-id="0f424-139">Execute os seguintes comandos para verificar se o servidor está escutando nessa porta.</span><span class="sxs-lookup"><span data-stu-id="0f424-139">Run the following commands to check whether the server is listening on that port.</span></span>

<span data-ttu-id="0f424-140">**VM Windows**</span><span class="sxs-lookup"><span data-stu-id="0f424-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="0f424-141">**VM Linux**</span><span class="sxs-lookup"><span data-stu-id="0f424-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="0f424-142">Execute o **Telnet** comando na VM para si mesmo para testar a porta.</span><span class="sxs-lookup"><span data-stu-id="0f424-142">Run the **Telnet** command on the VM to itself to test the port.</span></span> <span data-ttu-id="0f424-143">Se o teste falhar, aplicativo ou serviço não está configurado para escutar na porta.</span><span class="sxs-lookup"><span data-stu-id="0f424-143">If the test fails, application or service is not configured to listen on the port.</span></span>

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a><span data-ttu-id="0f424-144">Etapa 5: verificar se o problema é causado por SNAT</span><span class="sxs-lookup"><span data-stu-id="0f424-144">Step 5: Check whether the problem is caused by SNAT</span></span>

<span data-ttu-id="0f424-145">Em alguns cenários, a VM é colocada atrás de uma solução de balanceamento de carga que tem uma dependência em recursos fora do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f424-145">In some scenarios, the VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="0f424-146">Nesses cenários, se você tiver problemas intermitentes de conexão, o problema pode ser causado por [esgotamento da porta SNAT](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="0f424-146">In these scenarios, if you experience intermittent connection problems, the problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="0f424-147">Para resolver o problema, crie um VIP (ou ILPIP para clássico) para cada VM que está por trás do balanceador de carga e proteger com ACL ou NSG.</span><span class="sxs-lookup"><span data-stu-id="0f424-147">To resolve the issue, create a VIP (or ILPIP for classic) for each VM that is behind the Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a><span data-ttu-id="0f424-148">Etapa 6: verificar se o tráfego está bloqueado por ACLs para a VM clássica</span><span class="sxs-lookup"><span data-stu-id="0f424-148">Step 6: Check whether traffic is blocked by ACLs for the classic VM</span></span>

<span data-ttu-id="0f424-149">Uma ACL fornece a capacidade para permitir ou negar seletivamente o tráfego para um ponto de extremidade de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f424-149">An ACL provides the ability to selectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="0f424-150">Para saber mais, confira [Gerenciar a ACL em um ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="0f424-150">For more information, see [Manage the ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a><span data-ttu-id="0f424-151">Etapa 7: verificar se o ponto de extremidade é criado para a VM clássica</span><span class="sxs-lookup"><span data-stu-id="0f424-151">Step 7: Check whether the endpoint is created for the classic VM</span></span>

<span data-ttu-id="0f424-152">Todas as máquinas virtuais que você criar no Azure usando o modelo de implantação clássico automaticamente podem se comunicar através de um canal de rede privada com outras máquinas virtuais no mesmo serviço de nuvem ou rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0f424-152">All VMs that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="0f424-153">No entanto, os computadores em outras redes virtuais exigem pontos de extremidade para direcionar o tráfego de rede de entrada para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f424-153">However, computers on other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="0f424-154">Para saber mais, confira [Como configurar pontos de extremidade](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="0f424-154">For more information, see [How to set up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a><span data-ttu-id="0f424-155">Etapa 8: Não é possível conectar a um compartilhamento de rede VM</span><span class="sxs-lookup"><span data-stu-id="0f424-155">Step 8: Unable to connect to a VM network share</span></span>

<span data-ttu-id="0f424-156">Se não for possível conectar a um compartilhamento de rede VM, o problema pode ser causado por NICs não está disponíveis na VM.</span><span class="sxs-lookup"><span data-stu-id="0f424-156">If you are unable to connect to a VM network share, the problem can be caused by unavailable NICs in the VM.</span></span> <span data-ttu-id="0f424-157">Para excluir as NICs não disponíveis, consulte [Como excluir as NICs não disponíveis](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="0f424-157">To delete the unavailable NICs, see [How to delete the unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="0f424-158">Etapa 9: Conectividade de rede entre virtuais</span><span class="sxs-lookup"><span data-stu-id="0f424-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="0f424-159">Utilizar [rede Inspetor IP fluxo verificar](../network-watcher/network-watcher-ip-flow-verify-overview.md) e [NSG fluxo log](../network-watcher/network-watcher-nsg-flow-logging-overview.md) para identificar se houver um grupo de segurança de rede ou rota definida pelo usuário que estiver interferindo com o fluxo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="0f424-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) to identify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="0f424-160">Você também pode validar a configuração de rede entre [aqui](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="0f424-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="0f424-161">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="0f424-161">Need help?</span></span> <span data-ttu-id="0f424-162">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="0f424-162">Contact support.</span></span>
<span data-ttu-id="0f424-163">Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0f424-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>