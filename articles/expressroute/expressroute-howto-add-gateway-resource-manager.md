---
title: 'Adicionar um gateway de rede virtual tooa VNet para o ExpressRoute: PowerShell: Azure | Microsoft Docs'
description: "Este artigo o orienta por meio de adicionar um tooan de gateway de rede virtual já criado VNet Gerenciador de recursos para o ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a>Configurar um gateway de rede virtual para ExpressRoute usando PowerShell
> [!div class="op_single_selector"]
> * [Resource Manager - portal do Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Clássico - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vídeo – Portal do Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Este artigo orienta Olá etapas tooadd, redimensionar e remover um gateway de rede virtual (VNet) para uma rede virtual já existente. etapas de saudação para essa configuração são específicas para VNets que foram criados usando o modelo de implantação do Gerenciador de recursos de saudação que será usado em uma configuração de rota expressa. Para obter mais informações sobre gateways de rede virtual e definições de configuração do ExpressRoute, consulte [Sobre gateways de rede virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Antes de começar
Verifique se você instalou Olá cmdlets de PowerShell do Azure mais recentes. Se você ainda não instalou os cmdlets mais recentes Olá, será necessário toodo caso antes de começar as etapas de configuração de saudação. Para obter mais informações, consulte [Instalar e configurar o Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a>Próximas etapas
Depois que você criou o gateway de rede virtual Olá, você pode vincular sua rede virtual tooan circuito de rota expressa. Consulte [vincular um circuito de rota expressa do tooan de rede Virtual](expressroute-howto-linkvnet-arm.md).

