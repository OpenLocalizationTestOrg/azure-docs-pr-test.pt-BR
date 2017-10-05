---
title: "Sobre os requisitos criptográficos e os gateways de VPN do Azure| Microsoft Docs"
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
ms.openlocfilehash: c789e6c278fc0c58c64f5d96e57f94aee5a6cefc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="7f751-103">Sobre os requisitos criptográficos e os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="7f751-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="7f751-104">Este artigo discute como é possível configurar os gateways de VPN do Azure para satisfazer seus requisitos criptográficos para ambos os túneis de VPN S2S entre instalações e as conexões Rede Virtual a Rede Virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="7f751-104">This article discusses how you can configure Azure VPN gateways to satisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="7f751-105">Sobre os parâmetros de política IKE e IPsec para os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="7f751-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="7f751-106">O padrão de protocolo IKE e IPsec suporta uma ampla gama de algoritmos criptográficos em várias combinações.</span><span class="sxs-lookup"><span data-stu-id="7f751-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="7f751-107">Se os clientes não solicitarem uma combinação específica de parâmetros e algoritmos criptográficos, os gateways de VPN do Azure utilizarão um conjunto de propostas padrão.</span><span class="sxs-lookup"><span data-stu-id="7f751-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="7f751-108">Os conjuntos de políticas padrão foram escolhidos para maximizar a interoperabilidade com uma ampla gama de dispositivos de VPN de terceiros em configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="7f751-108">The default policy sets were chosen to maximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="7f751-109">Como resultado, as políticas e o número de propostas não podem abranger todas as combinações possíveis de intensidades de chave e algoritmos criptográficos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7f751-109">As a result, the policies and the number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="7f751-110">O conjunto de políticas padrão para o gateway de VPN do Azure está listado no documento: [Sobre dispositivos de VPN e parâmetros de IPsec/IKE para conexões de Gateway de VPN Site a Site](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="7f751-110">The default policy set for Azure VPN gateway is listed in the document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="7f751-111">Requisitos criptográficos</span><span class="sxs-lookup"><span data-stu-id="7f751-111">Cryptographic requirements</span></span>
<span data-ttu-id="7f751-112">Para comunicações que exigem parâmetros ou algoritmos criptográficos específicos, geralmente, devido a requisitos de segurança ou conformidade, os clientes agora podem configurar seus gateways de VPN do Azure para utilizar uma política de IPsec/IKE personalizada com algoritmos criptográficos específicos e intensidades de chave, em vez dos conjuntos de políticas padrão do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f751-112">For communications that require specific cryptographic algorithms or parameters, typically due to compliance or security requirements, customers can now configure their Azure VPN gateways to use a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than the Azure default policy sets.</span></span>

<span data-ttu-id="7f751-113">Por exemplo, as políticas de modo principal do IKEv2 para os gateways de VPN do Azure utilizam apenas o Grupo Diffie-Hellman 2 (1024 bits), enquanto os clientes podem precisar especificar grupos mais fortes a serem utilizados no IKE, como o Grupo 14 (2048 bits), o Grupo 24 (Grupo MODP de 2048 bits) ou o ECP (grupos de curvas elípticas) 256 ou 384 bits (Grupo 19 e Grupo 20, respectivamente).</span><span class="sxs-lookup"><span data-stu-id="7f751-113">For example, the IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need to specify stronger groups to be used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="7f751-114">Requisitos semelhantes aplicam-se também às políticas de modo rápido do IPsec.</span><span class="sxs-lookup"><span data-stu-id="7f751-114">Similar requirements apply to IPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="7f751-115">Política de IPsec/IKE personalizada com gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="7f751-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="7f751-116">Os gateways de VPN agora suportam política de IPsec/IKE personalizada por conexão.</span><span class="sxs-lookup"><span data-stu-id="7f751-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="7f751-117">Para uma conexão Site a Site ou Rede Virtual a Rede Virtual, você pode escolher uma combinação específica de algoritmos criptográficos para IPsec e IKE com a intensidade de chave desejada, como mostrado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="7f751-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with the desired key strength, as shown in the following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="7f751-119">Você pode criar uma política de IPsec/IKE e aplicar a uma conexão nova ou existente.</span><span class="sxs-lookup"><span data-stu-id="7f751-119">You can create an IPsec/IKE policy and apply to a new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="7f751-120">Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="7f751-120">Workflow</span></span>

1. <span data-ttu-id="7f751-121">Crie redes virtuais, gateways de VPN ou gateways de rede locais para a sua topologia de conectividade, conforme descrito em outros documentos de instruções</span><span class="sxs-lookup"><span data-stu-id="7f751-121">Create the virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-to documents</span></span>
2. <span data-ttu-id="7f751-122">Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="7f751-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="7f751-123">Você pode aplicar a política ao criar uma conexão VNet-to-VNet ou S2S</span><span class="sxs-lookup"><span data-stu-id="7f751-123">You can apply the policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="7f751-124">Se a conexão já foi criada, você poderá aplicar ou atualizar a política para uma conexão existente</span><span class="sxs-lookup"><span data-stu-id="7f751-124">If the connection is already created, you can apply or update the policy to an existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="7f751-125">FAQ sobre a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="7f751-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="7f751-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f751-126">Next steps</span></span>
<span data-ttu-id="7f751-127">Consulte [Configurar a política de IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter as instruções passo a passo sobre a configuração da política de IPsec/IKE personalizada em uma conexão.</span><span class="sxs-lookup"><span data-stu-id="7f751-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="7f751-128">Consulte também [Conectar vários dispositivos de VPN baseados em políticas](vpn-gateway-connect-multiple-policybased-rm-ps.md) para saber mais sobre a opção UsePolicyBasedTrafficSelectors.</span><span class="sxs-lookup"><span data-stu-id="7f751-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) to learn more about the UsePolicyBasedTrafficSelectors option.</span></span>