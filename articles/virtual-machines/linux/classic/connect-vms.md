---
title: "Conectar VMs Linux em um serviço de nuvem | Microsoft Docs"
description: "Conectar máquinas virtuais Linux criadas com o modelo clássico de implantação a um serviço de nuvem ou de rede virtual do Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 2fd23055-6b34-4ef0-88a8-fc19e32fb3c9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: cynthn
ms.openlocfilehash: e222645509640b104410f87e4bcd22834c8d9ec1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-linux-virtual-machines-created-with-the-classic-deployment-model-with-a-virtual-network-or-cloud-service"></a><span data-ttu-id="d1a79-103">Conectar máquinas virtuais Linux criadas com o modelo clássico de implantação com um serviço de nuvem ou de rede virtual</span><span class="sxs-lookup"><span data-stu-id="d1a79-103">Connect Linux virtual machines created with the classic deployment model with a virtual network or cloud service</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d1a79-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d1a79-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d1a79-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="d1a79-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d1a79-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="d1a79-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="d1a79-107">As máquinas virtuais Linux criadas com o modelo de implantação clássico sempre são colocadas em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d1a79-107">Linux virtual machines created with the classic deployment model are always placed in a cloud service.</span></span> <span data-ttu-id="d1a79-108">O serviço de nuvem funciona como um contêiner e fornece um nome DNS público exclusivo, um endereço IP público e um conjunto de pontos de extremidade para acessar a máquina virtual pela Internet.</span><span class="sxs-lookup"><span data-stu-id="d1a79-108">The cloud service acts as a container and provides a unique public DNS name, a public IP address, and a set of endpoints to access the virtual machine over the Internet.</span></span> <span data-ttu-id="d1a79-109">O serviço de nuvem pode estar em uma rede virtual, mas isso não é um requisito.</span><span class="sxs-lookup"><span data-stu-id="d1a79-109">The cloud service can be in a virtual network, but that's not a requirement.</span></span> <span data-ttu-id="d1a79-110">Você também pode [Conectar máquinas virtuais do Windows a uma rede virtual ou serviço de nuvem](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1a79-110">You can also [connect Windows virtual machines with a virtual network or cloud service](../../windows/classic/connect-vms.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="d1a79-111">Se um serviço de nuvem não estiver em uma rede virtual, ele será chamado de serviço de nuvem *autônomo* .</span><span class="sxs-lookup"><span data-stu-id="d1a79-111">If a cloud service isn't in a virtual network, it's called a *standalone* cloud service.</span></span> <span data-ttu-id="d1a79-112">As máquinas virtuais em um serviço de nuvem autônomo se comunicam com outras máquinas virtuais usando os nomes DNS públicos de outras máquinas virtuais, e o tráfego viaja pela Internet.</span><span class="sxs-lookup"><span data-stu-id="d1a79-112">The virtual machines in a standalone cloud service communicate with other virtual machines by using the other virtual machines’ public DNS names, and the traffic travels over the Internet.</span></span> <span data-ttu-id="d1a79-113">Se um serviço de nuvem estiver em uma rede virtual, as máquinas virtuais no serviço de nuvem podem se comunicar com todas as outras máquinas virtuais na rede virtual sem enviar tráfego pela Internet.</span><span class="sxs-lookup"><span data-stu-id="d1a79-113">If a cloud service is in a virtual network, the virtual machines in that cloud service can communicate with all other virtual machines in the virtual network without sending any traffic over the Internet.</span></span>

<span data-ttu-id="d1a79-114">Ao colocar as máquinas virtuais no mesmo serviço de nuvem autônomo, você ainda pode usar o balanceamento de carga e os conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d1a79-114">If you place your virtual machines in the same standalone cloud service, you can still use load balancing and availability sets.</span></span> <span data-ttu-id="d1a79-115">Para obter detalhes, confira [Máquinas virtuais de balanceamento de carga](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Gerenciar a disponibilidade de máquinas virtuais](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1a79-115">For details, see [Load balancing virtual machines](../../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Manage the availability of virtual machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d1a79-116">No entanto, você não pode organizar as máquinas virtuais em sub-redes ou conectar um serviço de nuvem autônomo à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="d1a79-116">However, you can't organize the virtual machines on subnets or connect a standalone cloud service to your on-premises network.</span></span> <span data-ttu-id="d1a79-117">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="d1a79-117">Here's an example:</span></span>

[!INCLUDE [virtual-machines-common-classic-connect-vms](../../../../includes/virtual-machines-common-classic-connect-vms.md)]

## <a name="next-steps"></a><span data-ttu-id="d1a79-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1a79-118">Next steps</span></span>
<span data-ttu-id="d1a79-119">Após criar uma máquina virtual, é uma boa ideia [adicionar um disco de dados](attach-disk.md) para que seus serviços e cargas de trabalho tenham um local para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="d1a79-119">After you create a virtual machine, it's a good idea to [add a data disk](attach-disk.md) so your services and workloads have a location to store data.</span></span>
