---
title: "Configurar um gateway VNet para o ExpressRoute usando o PowerShell: clássico: Azure | Microsoft Docs"
description: "Configure um gateway de VNet para uma VNet do modelo de implantação clássica usando o PowerShell para uma configuração do ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 6f37d4d9cba546b5416ab99040f5ef6dae273380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a>Configurar um gateway de rede virtual para ExpressRoute usando PowerShell (clássico)
> [!div class="op_single_selector"]
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clássico - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Este artigo vai orientá-lo por meio de saudação etapas tooadd, redimensionar e remover um gateway de rede virtual (VNet) para uma rede virtual já existente. Hello etapas para essa configuração são específicas para VNets que foram criados usando Olá **modelo de implantação clássico** e que seja usado em uma configuração de rota expressa. 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a>Antes de começar
Verifique se você instalou Olá cmdlets do PowerShell do Azure necessários para essa configuração (1.0.2 ou posterior). Se você ainda não instalou Olá cmdlets, você precisará toodo caso antes de começar as etapas de configuração de saudação. Para obter mais informações sobre como instalar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a>Próximas etapas
Depois que você criou o gateway de rede virtual Olá, você pode vincular sua rede virtual tooan circuito de rota expressa. Consulte [vincular um circuito de rota expressa do tooan de rede Virtual](expressroute-howto-linkvnet-classic.md).

