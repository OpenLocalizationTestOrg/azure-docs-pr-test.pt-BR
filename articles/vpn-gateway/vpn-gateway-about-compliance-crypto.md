---
title: aaaAbout requisitos de criptografia e gateways de VPN do Azure | Microsoft Docs
description: "Este artigo discute os requisitos criptográficos e os gateways de VPN do Azure"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="751f2-103">Sobre os requisitos criptográficos e os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="751f2-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="751f2-104">Este artigo descreve como você pode configurar toosatisfy de gateways de VPN do Azure seus requisitos de criptografia para conexões de VNet para VNet no Azure e de túneis de VPN S2S entre locais.</span><span class="sxs-lookup"><span data-stu-id="751f2-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="751f2-105">Sobre os parâmetros de política IKE e IPsec para os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="751f2-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="751f2-106">O padrão de protocolo IKE e IPsec suporta uma ampla gama de algoritmos criptográficos em várias combinações.</span><span class="sxs-lookup"><span data-stu-id="751f2-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="751f2-107">Se os clientes não solicitarem uma combinação específica de parâmetros e algoritmos criptográficos, os gateways de VPN do Azure utilizarão um conjunto de propostas padrão.</span><span class="sxs-lookup"><span data-stu-id="751f2-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="751f2-108">conjuntos de política padrão Olá foram escolhidos toomaximize interoperabilidade com uma ampla variedade de dispositivos VPN de terceiros nas configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="751f2-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="751f2-109">Como resultado, políticas hello e número de saudação de propostas não podem abranger todas as combinações possíveis de algoritmos de criptografia disponíveis e restrições de chave.</span><span class="sxs-lookup"><span data-stu-id="751f2-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="751f2-110">Olá política padrão definida para o gateway de VPN do Azure está listado no documento hello: [sobre dispositivos VPN e os parâmetros de IPsec/IKE para conexões de Gateway de VPN Site a Site](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="751f2-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="751f2-111">Requisitos criptográficos</span><span class="sxs-lookup"><span data-stu-id="751f2-111">Cryptographic requirements</span></span>
<span data-ttu-id="751f2-112">Para comunicações que exigem algoritmos criptográficos específicos ou parâmetros, normalmente devido a requisitos de segurança ou toocompliance, os clientes agora podem configurar sua toouse de gateways de VPN do Azure uma política personalizada do IPsec/IKE com específico criptográfico algoritmos e restrições de chave, em vez de conjuntos de política saudação padrão do Azure.</span><span class="sxs-lookup"><span data-stu-id="751f2-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="751f2-113">Por exemplo, políticas de modo principal Olá IKEv2 para gateways de VPN do Azure utilizam apenas Diffie-Hellman grupo 2 (1024 bits), enquanto que os clientes podem precisar toospecify mais forte grupos toobe usado no IKE, como 14 de grupo (2048 bits), grupo 24 (grupo de MODP de 2048 bits) ou ECP (elíptica curva grupos) 384 ou 256 bits (grupo 19 e 20 de grupo, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="751f2-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="751f2-114">Requisitos semelhantes de aplicam políticas de modo rápido de tooIPsec também.</span><span class="sxs-lookup"><span data-stu-id="751f2-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="751f2-115">Política de IPsec/IKE personalizada com gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="751f2-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="751f2-116">Os gateways de VPN agora suportam política de IPsec/IKE personalizada por conexão.</span><span class="sxs-lookup"><span data-stu-id="751f2-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="751f2-117">Para um Site a Site ou a conexão de rede virtual a rede, você pode escolher uma combinação específica de algoritmos de criptografia de IPsec e IKE com restrição de chave de saudação desejada, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="751f2-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="751f2-119">Você pode criar uma política de IPsec/IKE e aplicar tooa conexão de novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="751f2-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="751f2-120">Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="751f2-120">Workflow</span></span>

1. <span data-ttu-id="751f2-121">Criar redes virtuais Olá, gateways de VPN ou gateways de rede local para a sua topologia de conectividade, conforme descrito em outras toodocuments como</span><span class="sxs-lookup"><span data-stu-id="751f2-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="751f2-122">Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="751f2-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="751f2-123">Você pode aplicar a política de hello quando você cria uma conexão S2S ou VNet para VNet</span><span class="sxs-lookup"><span data-stu-id="751f2-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="751f2-124">Se a conexão de saudação já foi criado, você pode aplicar ou atualizar a conexão existente do hello política tooan</span><span class="sxs-lookup"><span data-stu-id="751f2-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="751f2-125">FAQ sobre a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="751f2-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="751f2-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="751f2-126">Next steps</span></span>
<span data-ttu-id="751f2-127">Consulte [Configurar a política de IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter as instruções passo a passo sobre a configuração da política de IPsec/IKE personalizada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="751f2-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="751f2-128">Consulte também [conectar vários dispositivos VPN com base na política](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn mais sobre Olá UsePolicyBasedTrafficSelectors opção.</span><span class="sxs-lookup"><span data-stu-id="751f2-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
