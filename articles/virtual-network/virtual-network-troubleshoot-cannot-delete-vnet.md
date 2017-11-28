---
title: "Não é possível excluir uma rede virtual no Azure | Microsoft Docs"
description: "Saiba como solucionar um problema em que você não consegue excluir uma rede virtual no Azure."
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
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="12b64-103">Solução de problemas: falha ao excluir uma rede virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="12b64-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="12b64-104">Você poderá receber erros ao tentar excluir uma rede virtual no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="12b64-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="12b64-105">Este artigo apresenta etapas para a solução de problemas para ajudá-lo a resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="12b64-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="12b64-106">Diretriz de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="12b64-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="12b64-107">[Verifique se um gateway de rede virtual está em execução na rede virtual](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="12b64-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="12b64-108">[Verifique se um gateway de aplicativo está em execução na rede virtual](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="12b64-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="12b64-109">[Verifique se o Serviço de Domínio do Azure Active Directory está habilitado na rede virtual](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="12b64-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="12b64-110">[Verifique se a rede virtual está conectada a outro recurso](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="12b64-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="12b64-111">[Verifique se uma máquina virtual ainda está em execução na rede virtual](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="12b64-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="12b64-112">[Verifique se a rede virtual está presa na migração](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="12b64-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="12b64-113">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="12b64-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="12b64-114">Verifique se um gateway de rede virtual está em execução na rede virtual</span><span class="sxs-lookup"><span data-stu-id="12b64-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="12b64-115">Para remover a rede virtual, você deve remover primeiro o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="12b64-116">Para redes virtuais clássicas, vá para a página **Visão geral** da rede virtual clássica no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="12b64-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="12b64-117">Na seção **conexões VPN**, se o gateway estiver em execução na rede virtual, você verá o endereço IP do gateway.</span><span class="sxs-lookup"><span data-stu-id="12b64-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Verifique se o gateway está em execução](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="12b64-119">Para redes virtuais, vá para a página **Visão geral** da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="12b64-120">Confira **Dispositivos conectados** para o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Verifique o dispositivo conectado](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="12b64-122">Antes de remover o gateway, primeiro remova qualquer objeto de **Conexão** no gateway.</span><span class="sxs-lookup"><span data-stu-id="12b64-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="12b64-123">Verifique se um gateway de aplicativo está em execução na rede virtual</span><span class="sxs-lookup"><span data-stu-id="12b64-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="12b64-124">Vá para a página **Visão geral** da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="12b64-125">Verifique os **Dispositivos conectados** para o gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12b64-125">Check the **Connected devices** for the application gateway.</span></span>

![Verifique o dispositivo conectado](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="12b64-127">Se houver um gateway de aplicativo, você deverá removê-lo antes de você pode excluir a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="12b64-128">Verifique se o Serviço de Domínio do Azure Active Directory está habilitado na rede virtual</span><span class="sxs-lookup"><span data-stu-id="12b64-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="12b64-129">Se o Serviço de Domínio do Active Directory estiver habilitado e conectado à rede virtual, não será possível excluir essa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Verifique o dispositivo conectado](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="12b64-131">Para desabilitar o serviço, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="12b64-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="12b64-132">Vá para o [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="12b64-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="12b64-133">No painel esquerdo, selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12b64-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="12b64-134">Selecione o diretório do Azure AD (Azure Active Directory) que tem o Serviço de Domínio do Active Directory habilitado.</span><span class="sxs-lookup"><span data-stu-id="12b64-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="12b64-135">Selecione a guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="12b64-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="12b64-136">Em **serviços de domínio**, altere a opção **Habilitar serviços de domínio para este diretório** para **Não**.</span><span class="sxs-lookup"><span data-stu-id="12b64-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="12b64-137">Verifique se a rede virtual está conectada a outro recurso</span><span class="sxs-lookup"><span data-stu-id="12b64-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="12b64-138">Verifique se há Links de Circuito, conexões e emparelhamentos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="12b64-139">Qualquer uma dessas opções pode fazer a exclusão de uma rede virtual falhar.</span><span class="sxs-lookup"><span data-stu-id="12b64-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="12b64-140">A ordem de exclusão recomendada é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="12b64-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="12b64-141">Conexões de gateway</span><span class="sxs-lookup"><span data-stu-id="12b64-141">Gateway connections</span></span>
2. <span data-ttu-id="12b64-142">Gateways</span><span class="sxs-lookup"><span data-stu-id="12b64-142">Gateways</span></span>
3. <span data-ttu-id="12b64-143">IPs</span><span class="sxs-lookup"><span data-stu-id="12b64-143">IPs</span></span>
4. <span data-ttu-id="12b64-144">Emparelhamentos de rede virtual</span><span class="sxs-lookup"><span data-stu-id="12b64-144">Virtual network peerings</span></span>
5. <span data-ttu-id="12b64-145">ASE (Ambiente do Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="12b64-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="12b64-146">Verifique se uma máquina virtual ainda está em execução na rede virtual</span><span class="sxs-lookup"><span data-stu-id="12b64-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="12b64-147">Verifique se nenhuma máquina virtual está na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="12b64-148">Verifique se a rede virtual está presa na migração</span><span class="sxs-lookup"><span data-stu-id="12b64-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="12b64-149">Se a rede virtual estiver presa em um estado de migração, ela não poderá ser excluída.</span><span class="sxs-lookup"><span data-stu-id="12b64-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="12b64-150">Execute o comando a seguir para anular a migração e, em seguida, excluir a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="12b64-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="12b64-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12b64-151">Next steps</span></span>

- [<span data-ttu-id="12b64-152">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="12b64-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="12b64-153">Perguntas frequentes sobre a rede virtual do Azure (Perguntas frequentes)</span><span class="sxs-lookup"><span data-stu-id="12b64-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)