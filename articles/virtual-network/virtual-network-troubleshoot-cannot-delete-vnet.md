---
title: aaaCannot excluir uma rede virtual no Azure | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema em que você não pode excluir uma rede virtual no Azure."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="fe44e-103">Solução de problemas: Falha toodelete uma rede virtual no Azure</span><span class="sxs-lookup"><span data-stu-id="fe44e-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="fe44e-104">Você poderá receber erros ao tentar toodelete uma rede virtual no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fe44e-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="fe44e-105">Este artigo fornece toohelp de etapas de solução de problemas é resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="fe44e-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="fe44e-106">Diretriz de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="fe44e-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="fe44e-107">[Verifique se um gateway de rede virtual está em execução na rede virtual Olá](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="fe44e-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="fe44e-108">[Verifique se um gateway de aplicativo está em execução na rede virtual Olá](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="fe44e-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="fe44e-109">[Verifique se o serviço de domínio do Azure Active Directory está habilitado na rede virtual Olá](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="fe44e-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="fe44e-110">[Verificar se a rede virtual Olá é conectado tooother recurso](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="fe44e-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="fe44e-111">[Verifique se uma máquina virtual ainda está em execução na rede virtual Olá](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="fe44e-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="fe44e-112">[Verifique se a rede virtual hello está preso em migração](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="fe44e-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="fe44e-113">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="fe44e-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="fe44e-114">Verifique se um gateway de rede virtual está em execução na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="fe44e-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="fe44e-115">rede virtual do tooremove hello, remova primeiro o gateway de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="fe44e-116">Para redes virtuais clássicas, vá toohello **visão geral** página Olá clássico virtual em rede Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe44e-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="fe44e-117">Em Olá **conexões VPN** seção, se o gateway de saudação está em execução na rede virtual hello, você verá Olá IP endereço do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe44e-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Verifique se o gateway está em execução](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="fe44e-119">Para redes virtuais, consulte toohello **visão geral** página da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="fe44e-120">Verificar **dispositivos conectados** para gateway de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Verifique o dispositivo conectado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="fe44e-122">Antes de remover gateway hello, primeiro remova qualquer **Conexão** objetos no gateway hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="fe44e-123">Verifique se um gateway de aplicativo está em execução na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="fe44e-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="fe44e-124">Vá toohello **visão geral** página da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="fe44e-125">Verificar Olá **dispositivos conectados** para gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Verifique o dispositivo conectado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="fe44e-127">Se houver um application gateway, você deve removê-lo antes de você pode excluir a rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="fe44e-128">Verifique se o serviço de domínio do Azure Active Directory está habilitado na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="fe44e-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="fe44e-129">Se Olá serviço de domínio do Active Directory é a rede virtual do toohello habilitado e conectado, você não pode excluir esta rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fe44e-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Verifique o dispositivo conectado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="fe44e-131">toodisable Olá serviço, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="fe44e-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="fe44e-132">Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fe44e-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fe44e-133">No painel esquerdo do hello, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe44e-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="fe44e-134">Selecione o diretório de Azure Active Directory (AD do Azure) de saudação que tem o serviço de domínio do Active Directory habilitada.</span><span class="sxs-lookup"><span data-stu-id="fe44e-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="fe44e-135">Selecione Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="fe44e-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="fe44e-136">Em **dos serviços de domínio**, alterar Olá **habilitar serviços de domínio para este diretório** opção muito**não**.</span><span class="sxs-lookup"><span data-stu-id="fe44e-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="fe44e-137">Verificar se a rede virtual Olá é conectado tooother recursos</span><span class="sxs-lookup"><span data-stu-id="fe44e-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="fe44e-138">Verifique se há Links de Circuito, conexões e emparelhamentos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fe44e-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="fe44e-139">Qualquer um deles pode causar um toofail de exclusão de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fe44e-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="fe44e-140">Olá ordem exclusão recomendado é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fe44e-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="fe44e-141">Conexões de gateway</span><span class="sxs-lookup"><span data-stu-id="fe44e-141">Gateway connections</span></span>
2. <span data-ttu-id="fe44e-142">Gateways</span><span class="sxs-lookup"><span data-stu-id="fe44e-142">Gateways</span></span>
3. <span data-ttu-id="fe44e-143">IPs</span><span class="sxs-lookup"><span data-stu-id="fe44e-143">IPs</span></span>
4. <span data-ttu-id="fe44e-144">Emparelhamentos de rede virtual</span><span class="sxs-lookup"><span data-stu-id="fe44e-144">Virtual network peerings</span></span>
5. <span data-ttu-id="fe44e-145">ASE (Ambiente do Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="fe44e-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="fe44e-146">Verifique se uma máquina virtual ainda está em execução na rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="fe44e-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="fe44e-147">Certifique-se de que nenhuma máquina virtual é na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="fe44e-148">Verifique se a rede virtual hello está preso na migração</span><span class="sxs-lookup"><span data-stu-id="fe44e-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="fe44e-149">Se a rede virtual hello está preso em um estado de migração, ele não pode ser excluído.</span><span class="sxs-lookup"><span data-stu-id="fe44e-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="fe44e-150">Execute Olá após a migração de saudação do comando tooabort e, em seguida, excluir a rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fe44e-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="fe44e-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe44e-151">Next steps</span></span>

- [<span data-ttu-id="fe44e-152">Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="fe44e-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="fe44e-153">Perguntas frequentes sobre a rede virtual do Azure (Perguntas frequentes)</span><span class="sxs-lookup"><span data-stu-id="fe44e-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)