---
title: gateways de rede virtual de rota expressa aaaAbout | Microsoft Docs
description: Saiba mais sobre os gateways de rede virtual para ExpressRoute.
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a>Sobre os gateways de rede virtual para ExpressRoute
Um gateway de rede virtual é usado toosend o tráfego de rede entre redes virtuais do Azure e locais de local. Quando você configura uma conexão ExpressRoute, é necessário criar e configurar um gateway de rede virtual e uma conexão de gateway de rede virtual.

Quando você cria um gateway de rede virtual, especifica várias configurações. Uma das configurações necessárias de saudação especifica se o gateway de saudação será usado para o tráfego de rota expressa ou VPN Site a Site. No modelo de implantação do Gerenciador de recursos de hello, configuração de saudação for '-GatewayType'.

Quando o tráfego de rede é enviado em uma conexão privada, use o tipo de gateway de saudação 'ExpressRoute'. Isso também é chamado tooas um gateway de rota expressa. Quando o tráfego é enviado criptografado em Olá Internet pública, use o tipo de gateway Olá 'Vpn'. Isso é chamado tooas um gateway de VPN. As conexões Site a Site, Ponto a Site e VNet a VNet usam um gateway VPN.

Cada rede virtual pode ter apenas um gateway de rede virtual por tipo de gateway. Por exemplo, você pode ter um gateway de rede virtual que usa - GatewayType Vpn, e outro que usa -GatewayType ExpressRoute. Este artigo se concentra no gateway de rede virtual de rota expressa hello.

## <a name="gwsku"></a>SKUs do Gateway
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

Se você quiser tooupgrade tooa seu gateway mais poderoso gateway SKU, na maioria dos casos, você pode usar Olá cmdlet do PowerShell 'Redimensionamento AzureRmVirtualNetworkGateway'. Isso funcionará para atualizações tooStandard e SKUs de alto desempenho. No entanto, tooupgrade toohello UltraPerformance SKU, você precisará de gateway de saudação toorecreate.

### <a name="aggthroughput"></a>Taxa de transferência agregada estimada por SKU de gateway
Olá tabela a seguir mostra os tipos de gateway hello e Olá estimado taxa de transferência. Esta tabela se aplica a saudação tooboth Gerenciador de recursos e modelos de implantação clássico.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Taxa de transferência de aplicativos depende de vários fatores, como latência de ponta a ponta Olá, e o número de saudação do tráfego de flui Olá aplicativo aberto. obtêm números Olá Olá tabela representam Olá limite superior que o aplicativo hello pode theorectically em um ambiente ideal. 
> 
>

## <a name="resources"></a>Cmdlets do PowerShell e APIs REST
Para obter recursos técnicos adicionais e requisitos de sintaxe específica ao usar APIs REST e cmdlets do PowerShell para configurações de gateway de rede virtual, consulte Olá páginas a seguir:

| **Clássico** | **Gerenciador de Recursos** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [API REST](https://msdn.microsoft.com/library/jj154113.aspx) |[API REST](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>Próximas etapas
Consulte [Visão geral de ExpressRoute](expressroute-introduction.md) para saber mais sobre as configurações de conexão disponíveis. 

