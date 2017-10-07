---
title: "aaaPrerequisites para a adoção de rota expressa do Azure | Microsoft Docs"
description: "Esta página fornece uma lista de requisitos toobe atendido antes que você pode solicitar um circuito de rota expressa do Azure."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>Pré-requisitos e lista de verificação do ExpressRoute
tooconnect tooMicrosoft nuvem serviços usando o ExpressRoute, você precisa tooverify que Olá seguindo os requisitos listados em Olá seções a seguir foram atendidos.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Conta do Azure
* Uma conta válida e ativa do Microsoft Azure. Essa conta é necessária tooset backup Olá circuito de rota expressa. Os circuitos do ExpressRoute são recursos das assinaturas do Azure. Uma assinatura do Azure é um requisito, mesmo se a conectividade for limitado Azure toonon serviços em nuvem Microsoft, como serviços do Office 365 e Dynamics 365.
* Uma assinatura ativa do Office 365 (se estiver usando os serviços do Office 365). Para obter mais informações, consulte Olá [requisitos específicos do Office 365](#office-365-specific-requirements) deste artigo.

## <a name="connectivity-provider"></a>Provedor de conectividade

* Você pode trabalhar com um [parceiro de conectividade de rota expressa](expressroute-locations.md#partners) tooconnect toohello nuvem da Microsoft. Você pode configurar uma conexão entre sua rede local e a Microsoft de [três maneiras](expressroute-introduction.md).
* Se seu provedor não é um parceiro de conectividade de rota expressa, você ainda pode se conectar toohello nuvem da Microsoft por meio de um [provedor do exchange de nuvem](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Requisitos de rede
* **Conectividade redundante**: não há nenhum requisito de redundância de conectividade física entre você e seu provedor. Microsoft exigem toobe de sessões BGP redundante definida entre os roteadores da Microsoft e os roteadores de emparelhamento Olá, mesmo quando você tem apenas [uma conexão física tooa nuvem exchange](expressroute-faqs.md#onep2plink).
* **Roteamento**: dependendo de como você conecta toohello Microsoft Cloud, você ou o provedor necessário tooset backup e gerenciar sessões BGP Olá para [domínios de roteamento](expressroute-circuit-peerings.md). Algum provedor de conectividade Ethernet ou o provedor de troca de nuvem pode oferecer gerenciamento BGP como um serviço de valor agregado.
* **NAT**: a Microsoft só aceita endereços IP públicos por meio de emparelhamento da Microsoft. Se você estiver usando endereços IP privados em sua rede local, você ou seu provedor necessidade tootranslate Olá privada endereços IP endereços IP públicos de toohello [usando Olá NAT](expressroute-nat.md).
* **QoS**: o Skype for Business tem vários serviços (por exemplo: voz, vídeo, texto) que exigem tratamento diferenciado de QoS. Você e seu provedor devem seguir Olá [requisitos de QoS](expressroute-qos.md).
* **Segurança de rede**: considere [segurança de rede](../best-practices-network-security.md) ao conectar-se toohello Microsoft Cloud por meio de rota expressa.

## <a name="office-365"></a>Office 365
Se você planeja tooenable Office 365 rota expressa, examine Olá seguintes documentos para obter mais informações sobre os requisitos do Office 365.

* [Visão geral do ExpressRoute para Office 365](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Roteamento com o ExpressRoute para Office 365](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Intervalos de endereços IP e URLs do Office 365](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Planejamento da rede e ajuste de desempenho para Office 365](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Ferramentas e calculadoras da largura de banda da rede](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Integração do Office 365 com ambientes locais](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Vídeos de treinamento avançados do ExpressRoute no Office 365](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Se você planeja tooenable Dynamics 365 rota expressa, examine Olá documentos para obter mais informações sobre Dynamics 365 a seguir

* [Whitepaper Dynamics 365 e ExpressRoute](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [Intervalos de endereços IP](https://support.microsoft.com/kb/2655102) e [URLs do Dynamics 365](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
* Localize um provedor de conectividade do ExpressRoute. Consulte [Parceiros e locais de emparelhamento do ExpressRoute](expressroute-locations.md).
* Consulte toorequirements para [roteamento](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurar sua conexão da Rota Expressa.
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configurar o roteamento](expressroute-howto-routing-classic.md)
  * [Vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-classic.md)
