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
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="1b0c2-103">Configurar um gateway de rede virtual para ExpressRoute usando PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="1b0c2-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b0c2-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b0c2-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="1b0c2-105">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b0c2-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="1b0c2-106">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1b0c2-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="1b0c2-107">Este artigo explica as etapas para adicionar, redimensionar e remover um gateway de VNet (rede virtual) para uma VNet já existente.</span><span class="sxs-lookup"><span data-stu-id="1b0c2-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="1b0c2-108">As etapas desta configuração se destinam especificamente a VNets criadas com o **modelo de implantação clássica** e que serão usadas em uma configuração do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1b0c2-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="1b0c2-109">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="1b0c2-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="1b0c2-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1b0c2-110">Before beginning</span></span>
<span data-ttu-id="1b0c2-111">Verifique se você instalou os cmdlets do Azure PowerShell necessários para esta configuração (1.0.2 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="1b0c2-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="1b0c2-112">Se ainda não os instalou, será necessário fazer isso antes de iniciar as etapas de configuração.</span><span class="sxs-lookup"><span data-stu-id="1b0c2-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="1b0c2-113">Para obter mais informações sobre como instalar o Azure PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b0c2-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1b0c2-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b0c2-114">Next steps</span></span>
<span data-ttu-id="1b0c2-115">Depois de criar o gateway de VNet, é possível vincular sua VNet a um circuito do ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="1b0c2-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="1b0c2-116">Consulte [Vincular uma Rede Virtual a um circuito do ExpressRoute](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="1b0c2-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

