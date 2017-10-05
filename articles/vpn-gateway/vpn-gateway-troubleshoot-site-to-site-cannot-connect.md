---
title: "Solução de problemas de conexão VPN site a site do Azure | Microsoft Docs"
description: "Saiba como solucionar problemas de conexão VPN site a site que repentinamente para de funcionar e não pode ser reconectada."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="7a17f-103">Solução de problemas: uma conexão VPN site a site do Azure não consegue se conectar e deixa de funcionar</span><span class="sxs-lookup"><span data-stu-id="7a17f-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="7a17f-104">Depois de configurar uma conexão VPN site a site entre uma rede local e uma rede virtual do Azure, a conexão VPN repentinamente deixa de funcionar e não pode ser reconectada.</span><span class="sxs-lookup"><span data-stu-id="7a17f-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="7a17f-105">Este artigo apresenta etapas para a solução de problemas para ajudá-lo a resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="7a17f-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="7a17f-106">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="7a17f-106">Troubleshooting steps</span></span>

<span data-ttu-id="7a17f-107">Para resolver o problema, primeiro tente [redefinir o gateway de VPN do Azure](vpn-gateway-resetgw-classic.md) e redefinir o túnel do dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="7a17f-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="7a17f-108">Se o problema persistir, siga essas etapas para identificar a causa do problema.</span><span class="sxs-lookup"><span data-stu-id="7a17f-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="7a17f-109">Etapa de pré-requisito</span><span class="sxs-lookup"><span data-stu-id="7a17f-109">Prerequisite step</span></span>

<span data-ttu-id="7a17f-110">Verifique o tipo do gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a17f-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="7a17f-111">Vá para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a17f-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7a17f-112">Verifique a página **Visão Geral** do gateway de VPN para as informações de tipo.</span><span class="sxs-lookup"><span data-stu-id="7a17f-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![Visão geral do gateway](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="7a17f-114">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="7a17f-114">Step 1.</span></span> <span data-ttu-id="7a17f-115">Verifique se o dispositivo VPN local está validado</span><span class="sxs-lookup"><span data-stu-id="7a17f-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="7a17f-116">Verifique se você está usando um [dispositivo VPN e uma versão do sistema operacional validados](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="7a17f-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="7a17f-117">Se o dispositivo não for um dispositivo VPN validado, talvez seja necessário contatar o fabricante do dispositivo para verificar se há algum problema de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="7a17f-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="7a17f-118">Verifique se o dispositivo VPN está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="7a17f-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="7a17f-119">Para obter mais informações, consulte [Editar exemplos de configuração de dispositivo](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="7a17f-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="7a17f-120">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="7a17f-120">Step 2.</span></span> <span data-ttu-id="7a17f-121">Verifique a chave compartilhada</span><span class="sxs-lookup"><span data-stu-id="7a17f-121">Verify the shared key</span></span>

<span data-ttu-id="7a17f-122">Compare a chave compartilhada do dispositivo VPN local e VPN de Rede Virtual do Azure para assegurar que as chaves correspondem.</span><span class="sxs-lookup"><span data-stu-id="7a17f-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="7a17f-123">Para exibir a chave compartilhada para a conexão VPN do Azure, utilize um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="7a17f-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="7a17f-124">**Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="7a17f-124">**Azure portal**</span></span>

1. <span data-ttu-id="7a17f-125">Vá para a conexão site a site do gateway de VPN que você criou.</span><span class="sxs-lookup"><span data-stu-id="7a17f-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="7a17f-126">Na seção **Configurações**, clique em **Chave Compartilhada**.</span><span class="sxs-lookup"><span data-stu-id="7a17f-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![Chave compartilhada](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="7a17f-128">**PowerShell do Azure**</span><span class="sxs-lookup"><span data-stu-id="7a17f-128">**Azure PowerShell**</span></span>

<span data-ttu-id="7a17f-129">Para o modelo de implantação do Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="7a17f-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="7a17f-130">Para o modelo de implantação clássico:</span><span class="sxs-lookup"><span data-stu-id="7a17f-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="7a17f-131">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="7a17f-131">Step 3.</span></span> <span data-ttu-id="7a17f-132">Verifique os IPs pares de VPN</span><span class="sxs-lookup"><span data-stu-id="7a17f-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="7a17f-133">A definição do IP no objeto do **Gateway de Rede Local** no Azure deve corresponder com o IP do dispositivo local.</span><span class="sxs-lookup"><span data-stu-id="7a17f-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="7a17f-134">A definição de IP do gateway do Azure que está configurada no dispositivo local deve corresponder ao IP de gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a17f-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="7a17f-135">Etapa 4.</span><span class="sxs-lookup"><span data-stu-id="7a17f-135">Step 4.</span></span> <span data-ttu-id="7a17f-136">Verifique UDR e NSGs na sub-rede do gateway</span><span class="sxs-lookup"><span data-stu-id="7a17f-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="7a17f-137">Verifique e remova o UDR (roteamento definido pelo usuário) ou NSG (grupos de segurança de rede) na sub-rede de gateway e, em seguida, teste o resultado.</span><span class="sxs-lookup"><span data-stu-id="7a17f-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="7a17f-138">Se o problema for resolvido, valide as configurações aplicadas pelo UDR ou NSG.</span><span class="sxs-lookup"><span data-stu-id="7a17f-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="7a17f-139">Etapa 5.</span><span class="sxs-lookup"><span data-stu-id="7a17f-139">Step 5.</span></span> <span data-ttu-id="7a17f-140">Verifique o endereço da interface externa do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="7a17f-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="7a17f-141">Se o endereço IP voltado para a Internet do dispositivo VPN estiver incluído na definição de **Rede local** no Azure, você poderá experimentar desconexões esporádicas.</span><span class="sxs-lookup"><span data-stu-id="7a17f-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="7a17f-142">A interface externa do dispositivo deve estar diretamente na Internet.</span><span class="sxs-lookup"><span data-stu-id="7a17f-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="7a17f-143">Não deve haver nenhuma conversão de endereços de rede ou firewall entre a Internet e o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7a17f-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="7a17f-144">Para configurar o clustering de firewall para ter um IP virtual, será necessário interromper o cluster e expor o dispositivo VPN diretamente a uma interface pública com a qual o gateway pode se conectar.</span><span class="sxs-lookup"><span data-stu-id="7a17f-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="7a17f-145">Etapa 6.</span><span class="sxs-lookup"><span data-stu-id="7a17f-145">Step 6.</span></span> <span data-ttu-id="7a17f-146">Verifique se as sub-redes coincidem exatamente (gateways baseados em políticas do Azure)</span><span class="sxs-lookup"><span data-stu-id="7a17f-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="7a17f-147">Verifique se as sub-redes correspondem exatamente entre a rede virtual do Azure e as definições locais para a rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="7a17f-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="7a17f-148">Verifique se as sub-redes correspondem exatamente entre o **Gateway de Rede Local** e as definições locais para a rede local.</span><span class="sxs-lookup"><span data-stu-id="7a17f-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="7a17f-149">Etapa 7.</span><span class="sxs-lookup"><span data-stu-id="7a17f-149">Step 7.</span></span> <span data-ttu-id="7a17f-150">Verifique a investigação de integridade do gateway do Azure</span><span class="sxs-lookup"><span data-stu-id="7a17f-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="7a17f-151">Vá para a [investigação de integridade](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="7a17f-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="7a17f-152">Clique no aviso do certificado.</span><span class="sxs-lookup"><span data-stu-id="7a17f-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="7a17f-153">Se você receber uma resposta, o gateway de VPN será considerado íntegro.</span><span class="sxs-lookup"><span data-stu-id="7a17f-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="7a17f-154">Se você não receber uma resposta, o gateway poderá não estar íntegro ou um NSG na sub-rede do gateway estará causando o problema.</span><span class="sxs-lookup"><span data-stu-id="7a17f-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="7a17f-155">O texto a seguir é uma resposta de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7a17f-155">The following text is a sample response:</span></span>

    <span data-ttu-id="7a17f-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Instância primária: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="7a17f-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="7a17f-157">Etapa 8.</span><span class="sxs-lookup"><span data-stu-id="7a17f-157">Step 8.</span></span> <span data-ttu-id="7a17f-158">Verifique se o dispositivo VPN local tem o recurso PFS habilitado</span><span class="sxs-lookup"><span data-stu-id="7a17f-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="7a17f-159">O recurso PFS pode causar os problemas de desconexão.</span><span class="sxs-lookup"><span data-stu-id="7a17f-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="7a17f-160">Se o dispositivo VPN estiver com PFS habilitado, desabilite o recurso.</span><span class="sxs-lookup"><span data-stu-id="7a17f-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="7a17f-161">Em seguida, atualize a política IPsec do gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="7a17f-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a17f-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a17f-162">Next steps</span></span>

-   [<span data-ttu-id="7a17f-163">Configurar uma conexão site a site para uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="7a17f-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="7a17f-164">Configurar uma política IPsec/IKE para conexões VPN site a site</span><span class="sxs-lookup"><span data-stu-id="7a17f-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
