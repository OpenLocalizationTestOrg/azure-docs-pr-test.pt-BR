---
title: 'Adicionar um gateway de rede virtual a uma VNet para a ExpressRoute: PowerShell: Azure| Microsoft Docs'
description: "Este artigo explica como adicionar um gateway de VNet a uma VNet já criada do Resource Manager para a ExpressRoute."
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
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="c2379-103">Configurar um gateway de rede virtual para ExpressRoute usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2379-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2379-104">Resource Manager - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c2379-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="c2379-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2379-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="c2379-106">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2379-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="c2379-107">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c2379-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="c2379-108">Este artigo explica as etapas para adicionar, redimensionar e remover um gateway de VNet (rede virtual) para uma VNet existente.</span><span class="sxs-lookup"><span data-stu-id="c2379-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="c2379-109">As etapas para essa configuração destinam-se especificamente a VNets criadas usando o modelo de implantação do Resource Manager que será usado em uma configuração do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2379-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="c2379-110">Para obter mais informações sobre gateways de rede virtual e definições de configuração do ExpressRoute, consulte [Sobre gateways de rede virtual para ExpressRoute](expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="c2379-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="c2379-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c2379-111">Before beginning</span></span>
<span data-ttu-id="c2379-112">Verifique se você instalou os cmdlets mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2379-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c2379-113">Se ainda não os instalou, será necessário fazer isso antes de iniciar as etapas de configuração.</span><span class="sxs-lookup"><span data-stu-id="c2379-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="c2379-114">Para obter mais informações, consulte [Instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c2379-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c2379-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2379-115">Next steps</span></span>
<span data-ttu-id="c2379-116">Depois de criar o gateway de VNet, é possível vincular sua VNet a um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c2379-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="c2379-117">Consulte [Vincular uma Rede Virtual a um circuito do ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c2379-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

