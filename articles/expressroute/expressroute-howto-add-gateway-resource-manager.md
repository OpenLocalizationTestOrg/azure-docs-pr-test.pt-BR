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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="519b7-103">Configurar um gateway de rede virtual para ExpressRoute usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="519b7-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="519b7-104">Resource Manager - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="519b7-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="519b7-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="519b7-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="519b7-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="519b7-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="519b7-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="519b7-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="519b7-108">Este artigo orienta Olá etapas tooadd, redimensionar e remover um gateway de rede virtual (VNet) para uma rede virtual já existente.</span><span class="sxs-lookup"><span data-stu-id="519b7-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="519b7-109">etapas de saudação para essa configuração são específicas para VNets que foram criados usando o modelo de implantação do Gerenciador de recursos de saudação que será usado em uma configuração de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="519b7-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="519b7-110">Para obter mais informações sobre gateways de rede virtual e definições de configuração do ExpressRoute, consulte [Sobre gateways de rede virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="519b7-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="519b7-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="519b7-111">Before beginning</span></span>
<span data-ttu-id="519b7-112">Verifique se você instalou Olá cmdlets de PowerShell do Azure mais recentes.</span><span class="sxs-lookup"><span data-stu-id="519b7-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="519b7-113">Se você ainda não instalou os cmdlets mais recentes Olá, será necessário toodo caso antes de começar as etapas de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="519b7-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="519b7-114">Para obter mais informações, consulte [Instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="519b7-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="519b7-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="519b7-115">Next steps</span></span>
<span data-ttu-id="519b7-116">Depois que você criou o gateway de rede virtual Olá, você pode vincular sua rede virtual tooan circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="519b7-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="519b7-117">Consulte [vincular um circuito de rota expressa do tooan de rede Virtual](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="519b7-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

