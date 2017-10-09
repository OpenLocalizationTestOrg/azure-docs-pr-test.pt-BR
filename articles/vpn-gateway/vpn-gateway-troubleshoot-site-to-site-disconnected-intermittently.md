---
title: aaaTroubleshoot VPN Site a Site do Azure desconecta intermitentemente | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema no qual conexão de VPN Site a Site Olá desconectado regularmente."
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
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="b59cb-103">Solução de problemas: desconexão intermitente da VPN Site a Site do Azure</span><span class="sxs-lookup"><span data-stu-id="b59cb-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="b59cb-104">Você pode experimentar o problema de saudação que uma conexão de VPN do Microsoft Azure ponto a Site novo ou existente não é estável ou desconecta regularmente.</span><span class="sxs-lookup"><span data-stu-id="b59cb-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="b59cb-105">Este artigo fornece etapas toohelp identificar e resolver Olá causa do problema de saudação de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="b59cb-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="b59cb-106">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b59cb-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="b59cb-107">Etapa de pré-requisito</span><span class="sxs-lookup"><span data-stu-id="b59cb-107">Prerequisite step</span></span>

<span data-ttu-id="b59cb-108">Verifique o tipo de saudação do gateway de rede virtual do Azure:</span><span class="sxs-lookup"><span data-stu-id="b59cb-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="b59cb-109">Vá muito[portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b59cb-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b59cb-110">Verificar Olá **visão geral** página Olá virtual do gateway de rede para obter informações de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="b59cb-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Visão geral de saudação do gateway Olá](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="b59cb-112">Etapa 1 Verifique se Olá dispositivo VPN é validado ao local</span><span class="sxs-lookup"><span data-stu-id="b59cb-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="b59cb-113">Verifique se você está usando um [dispositivo VPN e uma versão do sistema operacional validados](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="b59cb-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="b59cb-114">Se o dispositivo VPN Olá não for validado, você pode ter toocontact Olá dispositivo fabricante toosee se houver qualquer problema de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="b59cb-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="b59cb-115">Verifique se o que dispositivo VPN hello está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="b59cb-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="b59cb-116">Para obter mais informações, consulte [Editando amostras de configuração de dispositivo](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="b59cb-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="b59cb-117">Configurações de associação de segurança de saudação de verificação de etapa 2 (para gateways de rede virtual do Azure baseado em políticas)</span><span class="sxs-lookup"><span data-stu-id="b59cb-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="b59cb-118">Certifique-se de qual Olá a rede virtual, sub-redes e intervalos de saudação **gateway de rede Local** definição no Microsoft Azure são os mesmos configuração Olá no dispositivo VPN de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="b59cb-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="b59cb-119">Verifique se que coincidirem com as configurações de associação de segurança hello.</span><span class="sxs-lookup"><span data-stu-id="b59cb-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="b59cb-120">Etapa 3 Verificar as Rotas Definidas pelo Usuário ou os Grupos de Segurança de Rede na Sub-rede do Gateway</span><span class="sxs-lookup"><span data-stu-id="b59cb-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="b59cb-121">Uma rota definida pelo usuário na sub-rede de gateway Olá pode ser restringir o tráfego e permitindo que o outro tráfego.</span><span class="sxs-lookup"><span data-stu-id="b59cb-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="b59cb-122">Isso torna aparecem que conexão de VPN Olá é confiável para o tráfego e boa para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="b59cb-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="b59cb-123">Etapa 4 seleção hello "um túnel VPN por par de sub-rede" configuração (para gateways de rede virtual baseado em políticas)</span><span class="sxs-lookup"><span data-stu-id="b59cb-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="b59cb-124">Certifique-se de que Olá dispositivo de VPN está definido toohave ao local **um túnel VPN por par de sub-rede** para gateways de rede virtual baseado em políticas.</span><span class="sxs-lookup"><span data-stu-id="b59cb-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="b59cb-125">Etapa 5 Verificar a Limitação de Associação de Segurança (para gateways de rede virtual baseados em políticas)</span><span class="sxs-lookup"><span data-stu-id="b59cb-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="b59cb-126">gateway de rede virtual com base na política Olá tem limite de 200 pares de associação de segurança de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b59cb-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="b59cb-127">Se vezes o número de saudação de sub-redes de rede virtual do Azure multiplicado por Olá número de sub-redes locais é maior que 200, consulte sub-redes esporádicas desconectando.</span><span class="sxs-lookup"><span data-stu-id="b59cb-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="b59cb-128">Etapa 6 Verificar o endereço da interface externa do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="b59cb-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="b59cb-129">Se hello Internet voltada para o endereço IP do dispositivo VPN hello está incluída no hello **gateway de rede Local** definição no Azure, você pode enfrentar desconexões esporádicas.</span><span class="sxs-lookup"><span data-stu-id="b59cb-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="b59cb-130">Olá interface externa do dispositivo deve ser diretamente no hello da Internet.</span><span class="sxs-lookup"><span data-stu-id="b59cb-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="b59cb-131">Não deve haver nenhuma conversão de endereço de rede (NAT) ou um firewall entre hello da Internet e o dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="b59cb-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="b59cb-132">Se você configurar o Firewall Clustering toohave um IP virtual, interrompa o cluster hello e expor o dispositivo de VPN Olá diretamente tooa interface pública que Olá gateway pode fazer a interface com.</span><span class="sxs-lookup"><span data-stu-id="b59cb-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="b59cb-133">Etapa 7 de seleção se Olá dispositivo VPN tem sigilo habilitado ao local</span><span class="sxs-lookup"><span data-stu-id="b59cb-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="b59cb-134">Olá **sigilo** recurso pode causar problemas de desconexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b59cb-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="b59cb-135">Se o dispositivo de VPN Olá tem **sigilo** habilitado, desabilite o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b59cb-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="b59cb-136">Em seguida, [atualizar a política de IPsec de gateway de rede virtual Olá](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="b59cb-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b59cb-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b59cb-137">Next steps</span></span>

- [<span data-ttu-id="b59cb-138">Configurar uma rede virtual de tooa de conexão Site a Site</span><span class="sxs-lookup"><span data-stu-id="b59cb-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="b59cb-139">Configure a política IPsec/IKE para conexões VPN Site a Site</span><span class="sxs-lookup"><span data-stu-id="b59cb-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

