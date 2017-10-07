---
title: "aaaTroubleshoot uma conexão de VPN site a site do Azure que não é possível conectar | Microsoft Docs"
description: "Saiba como tootroubleshoot uma conexão de VPN site a site que repentinamente para de funcionar e não pode ser reconectada."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="2a845-103">Solução de problemas: uma conexão VPN site a site do Azure não consegue se conectar e deixa de funcionar</span><span class="sxs-lookup"><span data-stu-id="2a845-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="2a845-104">Depois de configurar uma conexão de VPN site a site entre uma rede local e uma rede virtual do Azure, Olá conexão VPN, de repente, para de funcionar e não pode ser reconectada.</span><span class="sxs-lookup"><span data-stu-id="2a845-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="2a845-105">Este artigo fornece toohelp de etapas de solução de problemas é resolver esse problema.</span><span class="sxs-lookup"><span data-stu-id="2a845-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="2a845-106">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2a845-106">Troubleshooting steps</span></span>

<span data-ttu-id="2a845-107">problema de saudação tooresolve, primeiro tente muito[gateway de VPN do Azure Olá redefinição](vpn-gateway-resetgw-classic.md) e redefinir o túnel de saudação do dispositivo VPN de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a845-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="2a845-108">Se Olá problema persistir, siga estas causa etapas tooidentify Olá problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a845-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="2a845-109">Etapa de pré-requisito</span><span class="sxs-lookup"><span data-stu-id="2a845-109">Prerequisite step</span></span>

<span data-ttu-id="2a845-110">Verifique o tipo de saudação do gateway de VPN do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2a845-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="2a845-111">Vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2a845-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2a845-112">Verificar Olá **visão geral** página do gateway de VPN Olá para obter informações de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="2a845-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Visão geral do gateway de saudação](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="2a845-114">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="2a845-114">Step 1.</span></span> <span data-ttu-id="2a845-115">Verifique se o dispositivo VPN de local de saudação é validado</span><span class="sxs-lookup"><span data-stu-id="2a845-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="2a845-116">Verifique se você está usando um [dispositivo VPN e uma versão do sistema operacional validados](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="2a845-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="2a845-117">Se o dispositivo de saudação não for um dispositivo VPN validado, você terá toocontact Olá dispositivo fabricante toosee se houver um problema de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="2a845-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="2a845-118">Verifique se o que dispositivo VPN hello está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2a845-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="2a845-119">Para obter mais informações, consulte [Editar exemplos de configuração de dispositivo](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="2a845-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="2a845-120">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="2a845-120">Step 2.</span></span> <span data-ttu-id="2a845-121">Verifique se a chave compartilhada Olá</span><span class="sxs-lookup"><span data-stu-id="2a845-121">Verify hello shared key</span></span>

<span data-ttu-id="2a845-122">Compare a chave compartilhada Olá Olá local VPN dispositivo toohello VPN de rede Virtual do Azure toomake se chaves Olá correspondem.</span><span class="sxs-lookup"><span data-stu-id="2a845-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="2a845-123">chave compartilhada do tooview Olá para Olá conexão VPN do Azure, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="2a845-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="2a845-124">**Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="2a845-124">**Azure portal**</span></span>

1. <span data-ttu-id="2a845-125">Vá conexão site a site de gateway VPN de toohello que você criou.</span><span class="sxs-lookup"><span data-stu-id="2a845-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="2a845-126">Em Olá **configurações** seção, clique em **chave compartilhada**.</span><span class="sxs-lookup"><span data-stu-id="2a845-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Chave compartilhada](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="2a845-128">**PowerShell do Azure**</span><span class="sxs-lookup"><span data-stu-id="2a845-128">**Azure PowerShell**</span></span>

<span data-ttu-id="2a845-129">Para o modelo de implantação do Azure Resource Manager hello:</span><span class="sxs-lookup"><span data-stu-id="2a845-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="2a845-130">Para o modelo de implantação clássico hello:</span><span class="sxs-lookup"><span data-stu-id="2a845-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="2a845-131">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="2a845-131">Step 3.</span></span> <span data-ttu-id="2a845-132">Verifique se o par VPN Olá IPs</span><span class="sxs-lookup"><span data-stu-id="2a845-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="2a845-133">Olá definição de IP no hello **Gateway de rede Local** objeto no Azure deve corresponder o IP do dispositivo local hello.</span><span class="sxs-lookup"><span data-stu-id="2a845-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="2a845-134">Olá definição de IP do gateway do Azure que é definida em hello local dispositivo deve corresponder a saudação IP de gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a845-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="2a845-135">Etapa 4.</span><span class="sxs-lookup"><span data-stu-id="2a845-135">Step 4.</span></span> <span data-ttu-id="2a845-136">Verifique UDR e NSGs na sub-rede de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="2a845-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="2a845-137">Verificar e remover roteamento definido pelo usuário (UDR) ou grupos de segurança de rede (NSGs) na sub-rede de gateway de saudação e, em seguida, o resultado de saudação de teste.</span><span class="sxs-lookup"><span data-stu-id="2a845-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="2a845-138">Se Olá problema for resolvido, valide configurações Olá UDR ou NSG aplicada.</span><span class="sxs-lookup"><span data-stu-id="2a845-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="2a845-139">Etapa 5.</span><span class="sxs-lookup"><span data-stu-id="2a845-139">Step 5.</span></span> <span data-ttu-id="2a845-140">Saudação de verificação de endereço de interface externa do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="2a845-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="2a845-141">Se Olá endereço IP da Internet do dispositivo VPN hello está incluído no hello **rede Local** definição no Azure, você pode experimentar desconexões esporádicas.</span><span class="sxs-lookup"><span data-stu-id="2a845-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="2a845-142">Olá interface externa do dispositivo deve ser diretamente no hello da Internet.</span><span class="sxs-lookup"><span data-stu-id="2a845-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="2a845-143">Não deve haver nenhuma conversão de endereços de rede ou um firewall entre hello da Internet e o dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a845-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="2a845-144">tooconfigure firewall toohave clustering um IP virtual, interrompa o cluster hello e expor o dispositivo de VPN Olá diretamente a interface pública tooa gateway Olá pode fazer a interface com.</span><span class="sxs-lookup"><span data-stu-id="2a845-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="2a845-145">Etapa 6.</span><span class="sxs-lookup"><span data-stu-id="2a845-145">Step 6.</span></span> <span data-ttu-id="2a845-146">Verifique se as sub-redes de saudação correspondem exatamente (gateways com base na política do Azure)</span><span class="sxs-lookup"><span data-stu-id="2a845-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="2a845-147">Verifique se as sub-redes de saudação correspondem exatamente entre hello rede virtual do Azure e definições de local para Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a845-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="2a845-148">Verifique se as sub-redes de saudação correspondem exatamente entre hello **Gateway de rede Local** e definições de rede do local de saudação local.</span><span class="sxs-lookup"><span data-stu-id="2a845-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="2a845-149">Etapa 7.</span><span class="sxs-lookup"><span data-stu-id="2a845-149">Step 7.</span></span> <span data-ttu-id="2a845-150">Verifique se a investigação de integridade de gateway do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="2a845-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="2a845-151">Vá toohello [investigação de integridade](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="2a845-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="2a845-152">Clique em aviso de saudação do certificado.</span><span class="sxs-lookup"><span data-stu-id="2a845-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="2a845-153">Se você receber uma resposta, o gateway VPN Olá será considerada íntegra.</span><span class="sxs-lookup"><span data-stu-id="2a845-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="2a845-154">Se você não receber uma resposta, gateway Olá pode não ser Íntegro ou um NSG na sub-rede de gateway hello está causando o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a845-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="2a845-155">Olá texto a seguir é um exemplo de resposta:</span><span class="sxs-lookup"><span data-stu-id="2a845-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="2a845-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Instância primária: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="2a845-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="2a845-157">Etapa 8.</span><span class="sxs-lookup"><span data-stu-id="2a845-157">Step 8.</span></span> <span data-ttu-id="2a845-158">Verifique se Olá local dispositivo VPN tem Olá sigilo habilitado</span><span class="sxs-lookup"><span data-stu-id="2a845-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="2a845-159">recurso de sigilo Olá pode causar problemas de desconexão.</span><span class="sxs-lookup"><span data-stu-id="2a845-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="2a845-160">Se o dispositivo de VPN Olá sigilo total, desabilite o recurso de hello.</span><span class="sxs-lookup"><span data-stu-id="2a845-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="2a845-161">Atualize política de IPsec de gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="2a845-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a845-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a845-162">Next steps</span></span>

-   [<span data-ttu-id="2a845-163">Configurar uma rede virtual de tooa conexão site a site</span><span class="sxs-lookup"><span data-stu-id="2a845-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="2a845-164">Configurar uma política IPsec/IKE para conexões VPN site a site</span><span class="sxs-lookup"><span data-stu-id="2a845-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
