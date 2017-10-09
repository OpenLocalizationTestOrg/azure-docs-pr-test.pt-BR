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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Sobre os requisitos criptográficos e os gateways de VPN do Azure

Este artigo descreve como você pode configurar toosatisfy de gateways de VPN do Azure seus requisitos de criptografia para conexões de VNet para VNet no Azure e de túneis de VPN S2S entre locais. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Sobre os parâmetros de política IKE e IPsec para os gateways de VPN do Azure
O padrão de protocolo IKE e IPsec suporta uma ampla gama de algoritmos criptográficos em várias combinações. Se os clientes não solicitarem uma combinação específica de parâmetros e algoritmos criptográficos, os gateways de VPN do Azure utilizarão um conjunto de propostas padrão. conjuntos de política padrão Olá foram escolhidos toomaximize interoperabilidade com uma ampla variedade de dispositivos VPN de terceiros nas configurações padrão. Como resultado, políticas hello e número de saudação de propostas não podem abranger todas as combinações possíveis de algoritmos de criptografia disponíveis e restrições de chave.

Olá política padrão definida para o gateway de VPN do Azure está listado no documento hello: [sobre dispositivos VPN e os parâmetros de IPsec/IKE para conexões de Gateway de VPN Site a Site](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Requisitos criptográficos
Para comunicações que exigem algoritmos criptográficos específicos ou parâmetros, normalmente devido a requisitos de segurança ou toocompliance, os clientes agora podem configurar sua toouse de gateways de VPN do Azure uma política personalizada do IPsec/IKE com específico criptográfico algoritmos e restrições de chave, em vez de conjuntos de política saudação padrão do Azure.

Por exemplo, políticas de modo principal Olá IKEv2 para gateways de VPN do Azure utilizam apenas Diffie-Hellman grupo 2 (1024 bits), enquanto que os clientes podem precisar toospecify mais forte grupos toobe usado no IKE, como 14 de grupo (2048 bits), grupo 24 (grupo de MODP de 2048 bits) ou ECP (elíptica curva grupos) 384 ou 256 bits (grupo 19 e 20 de grupo, respectivamente). Requisitos semelhantes de aplicam políticas de modo rápido de tooIPsec também.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Política de IPsec/IKE personalizada com gateways de VPN do Azure
Os gateways de VPN agora suportam política de IPsec/IKE personalizada por conexão. Para um Site a Site ou a conexão de rede virtual a rede, você pode escolher uma combinação específica de algoritmos de criptografia de IPsec e IKE com restrição de chave de saudação desejada, conforme mostrado no exemplo a seguir de saudação:

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Você pode criar uma política de IPsec/IKE e aplicar tooa conexão de novo ou existente. 

### <a name="workflow"></a>Fluxo de trabalho

1. Criar redes virtuais Olá, gateways de VPN ou gateways de rede local para a sua topologia de conectividade, conforme descrito em outras toodocuments como
2. Criar uma política de IPsec/IKE
3. Você pode aplicar a política de hello quando você cria uma conexão S2S ou VNet para VNet
4. Se a conexão de saudação já foi criado, você pode aplicar ou atualizar a conexão existente do hello política tooan


## <a name="ipsecike-policy-faq"></a>FAQ sobre a política de IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Próximas etapas
Consulte [Configurar a política de IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter as instruções passo a passo sobre a configuração da política de IPsec/IKE personalizada em uma conexão.

Consulte também [conectar vários dispositivos VPN com base na política](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn mais sobre Olá UsePolicyBasedTrafficSelectors opção.
