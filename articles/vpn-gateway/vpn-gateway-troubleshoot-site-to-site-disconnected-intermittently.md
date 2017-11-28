---
title: "Solucionar problemas de desconexão intermitente da VPN Site a Site do Azure | Microsoft Docs"
description: "Saiba como solucionar o problema em que a conexão VPN Site a Site é desconectada regularmente."
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="85d27-103">Solução de problemas: desconexão intermitente da VPN Site a Site do Azure</span><span class="sxs-lookup"><span data-stu-id="85d27-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="85d27-104">Você poderá observar o problema em que uma conexão VPN Ponto a Site nova ou existente do Microsoft Azure não é estável ou se desconecta regularmente.</span><span class="sxs-lookup"><span data-stu-id="85d27-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="85d27-105">Este artigo fornece etapas de solução de problemas para ajudá-lo a identificar e resolver a causa do problema.</span><span class="sxs-lookup"><span data-stu-id="85d27-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="85d27-106">Etapas para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="85d27-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="85d27-107">Etapa de pré-requisito</span><span class="sxs-lookup"><span data-stu-id="85d27-107">Prerequisite step</span></span>

<span data-ttu-id="85d27-108">Verifique o tipo de gateway de rede virtualdo  Azure:</span><span class="sxs-lookup"><span data-stu-id="85d27-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="85d27-109">Vá para o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="85d27-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="85d27-110">Verifique a página **Visão Geral** do gateway de rede virtual para os tipos de informações.</span><span class="sxs-lookup"><span data-stu-id="85d27-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![Visão geral do gateway](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="85d27-112">Etapa 1 Verificar se o dispositivo VPN local é validado</span><span class="sxs-lookup"><span data-stu-id="85d27-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="85d27-113">Verifique se você está usando um [dispositivo VPN e uma versão do sistema operacional validados](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="85d27-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="85d27-114">Se o dispositivo VPN não for validado, talvez você precise contatar o fabricante do dispositivo para ver se há algum problema de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="85d27-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="85d27-115">Verifique se o dispositivo VPN está configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="85d27-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="85d27-116">Para obter mais informações, consulte [Editando amostras de configuração de dispositivo](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="85d27-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="85d27-117">Etapa 2 Verificar as configurações de Associação de Segurança (para gateways de rede virtual do Azure baseados em políticas)</span><span class="sxs-lookup"><span data-stu-id="85d27-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="85d27-118">Verifique se a rede virtual, as sub-redes e os intervalos na definição de **Gateway de rede local** no Microsoft Azure são os mesmos da configuração do dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="85d27-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="85d27-119">Verifique se as configurações de Associação de Segurança correspondem.</span><span class="sxs-lookup"><span data-stu-id="85d27-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="85d27-120">Etapa 3 Verificar as Rotas Definidas pelo Usuário ou os Grupos de Segurança de Rede na Sub-rede do Gateway</span><span class="sxs-lookup"><span data-stu-id="85d27-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="85d27-121">Uma rota definida pelo usuário na sub-rede do gateway pode estar restringindo parte do tráfego e permitindo outra parte dele.</span><span class="sxs-lookup"><span data-stu-id="85d27-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="85d27-122">Isso faz com que a conexão VPN pareça não confiável para uma parte do tráfego e boa para outra parte dele.</span><span class="sxs-lookup"><span data-stu-id="85d27-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="85d27-123">Etapa 4 Verificar a configuração “um Túnel VPN por Par de Sub-rede” (para gateways de rede virtual baseados em políticas)</span><span class="sxs-lookup"><span data-stu-id="85d27-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="85d27-124">Verifique se o dispositivo VPN local está definido para ter **um túnel VPN por par de sub-rede** para gateways de rede virtual baseados em políticas.</span><span class="sxs-lookup"><span data-stu-id="85d27-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="85d27-125">Etapa 5 Verificar a Limitação de Associação de Segurança (para gateways de rede virtual baseados em políticas)</span><span class="sxs-lookup"><span data-stu-id="85d27-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="85d27-126">O Gateway de rede virtual baseado em política tem um limite de 200 pares de sub-rede de Associação de Segurança.</span><span class="sxs-lookup"><span data-stu-id="85d27-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="85d27-127">Se o número de sub-redes da rede virtual do Azure multiplicado pelo número de sub-redes locais for maior que 200, você observará a desconexão esporádica de sub-redes.</span><span class="sxs-lookup"><span data-stu-id="85d27-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="85d27-128">Etapa 6 Verificar o endereço da interface externa do dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="85d27-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="85d27-129">Se o endereço IP para a Internet do dispositivo VPN estiver incluído na definição de **Gateway de rede local** no Azure, você poderá observar desconexões esporádicas.</span><span class="sxs-lookup"><span data-stu-id="85d27-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="85d27-130">A interface externa do dispositivo deve estar diretamente na Internet.</span><span class="sxs-lookup"><span data-stu-id="85d27-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="85d27-131">Não deve haver nenhum NAT (Conversão de Endereços de Rede) ou firewall entre a Internet e o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85d27-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="85d27-132">Se você configurar o Clustering de Firewall para ter um IP virtual, deverá interromper o cluster e expor o dispositivo VPN diretamente para uma interface pública com a qual o gateway pode se comunicar.</span><span class="sxs-lookup"><span data-stu-id="85d27-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="85d27-133">Etapa 7 Verificar se o dispositivo VPN local tem o PFS habilitado</span><span class="sxs-lookup"><span data-stu-id="85d27-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="85d27-134">O recurso **PFS** pode causar problemas de desconexão.</span><span class="sxs-lookup"><span data-stu-id="85d27-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="85d27-135">Se o dispositivo VPN tiver o **PFS** habilitado, desabilite o recurso.</span><span class="sxs-lookup"><span data-stu-id="85d27-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="85d27-136">Em seguida, [atualize a política IPsec do gateway de rede virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="85d27-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="85d27-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85d27-137">Next steps</span></span>

- [<span data-ttu-id="85d27-138">Configurar uma conexão Site a Site para uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="85d27-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="85d27-139">Configure a política IPsec/IKE para conexões VPN Site a Site</span><span class="sxs-lookup"><span data-stu-id="85d27-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

