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
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="2bddb-103">Configurar um gateway de rede virtual para ExpressRoute usando PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="2bddb-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2bddb-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bddb-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="2bddb-105">Clássico - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bddb-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="2bddb-106">Vídeo – Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2bddb-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="2bddb-107">Este artigo vai orientá-lo por meio de saudação etapas tooadd, redimensionar e remover um gateway de rede virtual (VNet) para uma rede virtual já existente.</span><span class="sxs-lookup"><span data-stu-id="2bddb-107">This article will walk you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="2bddb-108">Hello etapas para essa configuração são específicas para VNets que foram criados usando Olá **modelo de implantação clássico** e que seja usado em uma configuração de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="2bddb-108">hello steps for this configuration are specifically for VNets that were created using hello **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="2bddb-109">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="2bddb-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="2bddb-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2bddb-110">Before beginning</span></span>
<span data-ttu-id="2bddb-111">Verifique se você instalou Olá cmdlets do PowerShell do Azure necessários para essa configuração (1.0.2 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="2bddb-111">Verify that you have installed hello Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="2bddb-112">Se você ainda não instalou Olá cmdlets, você precisará toodo caso antes de começar as etapas de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2bddb-112">If you haven't installed hello cmdlets, you'll need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="2bddb-113">Para obter mais informações sobre como instalar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2bddb-113">For more information about installing Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2bddb-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2bddb-114">Next steps</span></span>
<span data-ttu-id="2bddb-115">Depois que você criou o gateway de rede virtual Olá, você pode vincular sua rede virtual tooan circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="2bddb-115">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="2bddb-116">Consulte [vincular um circuito de rota expressa do tooan de rede Virtual](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="2bddb-116">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

