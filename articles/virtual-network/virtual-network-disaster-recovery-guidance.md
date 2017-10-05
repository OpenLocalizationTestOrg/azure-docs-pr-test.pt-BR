---
title: "O que fazer caso uma interrupção de serviço do Azure afete as Redes Virtuais do Azure | Microsoft Docs"
description: "Saiba o que fazer caso uma interrupção de serviço do Azure afete as Redes Virtuais do Azure."
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: 4e125406d2e798138c45e3fbbf61a610afab69fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="virtual-network--business-continuity"></a><span data-ttu-id="86e2c-103">Rede Virtual – Continuidade de Negócios</span><span class="sxs-lookup"><span data-stu-id="86e2c-103">Virtual Network – Business Continuity</span></span>
## <a name="overview"></a><span data-ttu-id="86e2c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="86e2c-104">Overview</span></span>
<span data-ttu-id="86e2c-105">Uma Rede Virtual (VNet) é uma representação da sua rede na nuvem.</span><span class="sxs-lookup"><span data-stu-id="86e2c-105">A Virtual Network (VNet) is a logical representation of your network in the cloud.</span></span> <span data-ttu-id="86e2c-106">Ela permite que você defina seu próprio espaço de endereço IP privado e segmente a rede em sub-redes.</span><span class="sxs-lookup"><span data-stu-id="86e2c-106">It allows you to define your own private IP address space and segment the network into subnets.</span></span> <span data-ttu-id="86e2c-107">As VNets servem como um limite de confiança para hospedar seus recursos de computação, como as Máquinas Virtuais e os Serviços de Nuvem do Azure (funções web/de trabalho).</span><span class="sxs-lookup"><span data-stu-id="86e2c-107">VNets serves as a trust boundary to host your compute resources such as Azure Virtual Machines and Cloud Services (web/worker roles).</span></span> <span data-ttu-id="86e2c-108">Uma VNet permite a comunicação de IP privada direta entre os recursos hospedados nela.</span><span class="sxs-lookup"><span data-stu-id="86e2c-108">A VNet allows direct private IP communication between the resources hosted in it.</span></span> <span data-ttu-id="86e2c-109">Uma Rede Virtual também pode ser vinculada a uma rede local por meio de uma das opções híbridas, como um Gateway de VPN ou ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="86e2c-109">A Virtual Network can also be linked to an on-premises network through one of the hybrid options such as a VPN Gateway or ExpressRoute.</span></span>

<span data-ttu-id="86e2c-110">Uma VNet é criada dentro do escopo de uma região.</span><span class="sxs-lookup"><span data-stu-id="86e2c-110">A VNet is created within the scope of a region.</span></span> <span data-ttu-id="86e2c-111">Você pode criar VNets com o mesmo espaço de endereço em duas regiões diferentes (ou seja, Leste dos EUA e Oeste dos EUA, mas não é possível conectá-las entre si diretamente).</span><span class="sxs-lookup"><span data-stu-id="86e2c-111">You can create VNets with same address space in two different regions (i.e. US East and US West but cannot connect them to one another directly).</span></span> 

## <a name="business-continuity"></a><span data-ttu-id="86e2c-112">Continuidade dos negócios</span><span class="sxs-lookup"><span data-stu-id="86e2c-112">Business Continuity</span></span>
<span data-ttu-id="86e2c-113">O seu aplicativo pode ser interrompido de várias maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="86e2c-113">There could be several different ways that your application could be disrupted.</span></span> <span data-ttu-id="86e2c-114">Uma determinada região poderia ser cortada completamente devido a um desastre natural ou a um desastre parcial devido a uma falha de vários dispositivos/serviços.</span><span class="sxs-lookup"><span data-stu-id="86e2c-114">A given region could be completely cut off due to a natural disaster or a partial disaster due to a failure of multiple devices/services.</span></span> <span data-ttu-id="86e2c-115">O impacto sobre o serviço de Rede Virtual é diferente em cada uma dessas situações.</span><span class="sxs-lookup"><span data-stu-id="86e2c-115">The impact on the VNet service is different in each of these situations.</span></span>

<span data-ttu-id="86e2c-116">**P: O que fazer caso ocorra uma interrupção em uma região inteira? Por exemplo, se uma região fosse completamente cortada devido a um desastre natural? O que acontece com as Redes Virtuais hospedadas na região?**</span><span class="sxs-lookup"><span data-stu-id="86e2c-116">**Q: What do you do in the event of an outage to an entire region? i.e. if a region is completely cutoff due to a natural disaster? What happens to the Virtual Networks hosted in the region?**</span></span>

<span data-ttu-id="86e2c-117">R: A Rede Virtual e os recursos na região afetada permanecem inacessíveis durante o tempo de interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="86e2c-117">A: The Virtual Network and the resources in the affected region remains inaccessible during the time of the service disruption.</span></span>

![Diagrama de Rede Virtual Simples](./media/virtual-network-disaster-recovery-guidance/vnet.png)

<span data-ttu-id="86e2c-119">**P: O que posso fazer para recriar a mesma Rede Virtual em uma região diferente?**</span><span class="sxs-lookup"><span data-stu-id="86e2c-119">**Q: What can I to do re-create the same Virtual Network in a different region?**</span></span>

<span data-ttu-id="86e2c-120">R: A Rede Virtual (VNet) é um recurso relativamente leve.</span><span class="sxs-lookup"><span data-stu-id="86e2c-120">A: Virtual Network (VNet) is fairly lightweight resource.</span></span> <span data-ttu-id="86e2c-121">Você pode invocar as APIs do Azure para criar uma VNet com o mesmo espaço de endereço em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="86e2c-121">You can invoke Azure APIs to create a VNet with the same address space in a different region.</span></span> <span data-ttu-id="86e2c-122">Para recriar o mesmo ambiente que estava presente na região afetada, você precisará fazer chamadas à API para reimplantar seus serviços de nuvem (funções web/de trabalho) e as máquinas virtuais que você tinha.</span><span class="sxs-lookup"><span data-stu-id="86e2c-122">To re-create the same environment that was present in the affected region, you have to make API calls to re-deploy your Cloud Services (web/worker roles) and Virtual Machines that you had.</span></span> <span data-ttu-id="86e2c-123">Você também precisará criar um Gateway de VPN e se conectar à sua rede local, se você tiver conectividade local (como em uma implantação híbrida).</span><span class="sxs-lookup"><span data-stu-id="86e2c-123">You will also have to spin up a VPN Gateway and connect to your on-premises network if you had on-premises connectivity (such as in a hybrid deployment).</span></span>

<span data-ttu-id="86e2c-124">As instruções para criar uma VNet são encontradas [aqui](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="86e2c-124">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span> 

<span data-ttu-id="86e2c-125">**P: Uma réplica de uma VNet em uma determinada região pode ser recriada em outra região antecipadamente?**</span><span class="sxs-lookup"><span data-stu-id="86e2c-125">**Q: Can a replica of a VNet in a given region be re-created in another region ahead of time?**</span></span>

<span data-ttu-id="86e2c-126">R: Sim, você pode criar duas VNets usando o mesmo espaço de endereço IP privado e os recursos em duas regiões diferentes antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="86e2c-126">A: Yes, you can create two VNets using the same private IP address space and resources in two different regions ahead of time.</span></span> <span data-ttu-id="86e2c-127">Se o cliente estivesse hospedando serviços voltados para a Internet na VNet, ele poderia ter configurado o Gerenciador de Tráfego para distribuir o tráfego geograficamente para a região que está ativa.</span><span class="sxs-lookup"><span data-stu-id="86e2c-127">If a customer was hosting internet facing services in the VNet, they could have set up Traffic Manager to geo-route traffic to the region that is active.</span></span> <span data-ttu-id="86e2c-128">No entanto, um cliente não pode conectar duas VNets com o mesmo espaço de endereço de rede local, uma vez que isso causaria problemas de roteamento.</span><span class="sxs-lookup"><span data-stu-id="86e2c-128">However, a customer cannot connect two VNets with the same address space to their on-premises network as it would cause routing issues.</span></span> <span data-ttu-id="86e2c-129">No momento de um desastre e da perda de uma VNet em uma região, o cliente pode se conectar a outra VNet na região disponível com espaço de endereço correspondente a rede local.</span><span class="sxs-lookup"><span data-stu-id="86e2c-129">At the time of a disaster and loss of a VNet in one region, a customer can connect the other VNet in the available region with matching address space to their on-premises network.</span></span>

<span data-ttu-id="86e2c-130">As instruções para criar uma VNet são encontradas [aqui](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="86e2c-130">The instructions for creating a VNet are found [here](virtual-networks-create-vnet-arm-pportal.md).</span></span>

