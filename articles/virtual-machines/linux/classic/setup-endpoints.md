---
title: "aaaSet pontos de extremidade em uma VM do Linux clássica | Microsoft Docs"
description: "Saiba mais sobre o tooset pontos de extremidade para uma VM do Linux no hello comunicação tooallow de portal clássico do Azure com uma máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="7ff67-103">Como tooset pontos de extremidade em uma máquina virtual clássica do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="7ff67-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="7ff67-104">Todas as máquinas virtuais Linux criadas no Azure usando o modelo de implantação clássico Olá podem se comunicar automaticamente por um canal de rede privada com outras máquinas virtuais no hello que mesmo serviço ou de rede virtual na nuvem.</span><span class="sxs-lookup"><span data-stu-id="7ff67-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="7ff67-105">No entanto, os computadores Olá Internet ou outras redes virtuais requerem pontos de extremidade toodirect Olá rede de entrada tráfego tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7ff67-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="7ff67-106">Este artigo também está disponível para [máquinas virtuais do Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ff67-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ff67-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7ff67-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7ff67-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="7ff67-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7ff67-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ff67-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="7ff67-110">Em Olá **Gerenciador de recursos de** modelo de implantação, pontos de extremidade são configurados usando **grupos de segurança de rede (NSGs)**.</span><span class="sxs-lookup"><span data-stu-id="7ff67-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="7ff67-111">Para saber mais, consulte [Abrir portas e pontos de extremidade](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ff67-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7ff67-112">Quando você cria uma máquina virtual Linux em Olá portal do Azure, um ponto de extremidade para o Secure Shell (SSH) é normalmente criado para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7ff67-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="7ff67-113">Você pode configurar pontos de extremidade adicionais durante a criação de máquina virtual de hello, ou posteriormente, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7ff67-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="7ff67-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ff67-114">Next steps</span></span>
* <span data-ttu-id="7ff67-115">Você também pode criar um ponto de extremidade VM usando Olá [Interface de linha de comando do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7ff67-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="7ff67-116">Executar Olá **criar ponto de extremidade de vm do azure** comando.</span><span class="sxs-lookup"><span data-stu-id="7ff67-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="7ff67-117">Se você criou uma máquina virtual no modelo de implantação do Gerenciador de recursos de saudação, você pode usar Olá CLI do Azure no Gerenciador de recursos de modo muito[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol tráfego toohello VM.</span><span class="sxs-lookup"><span data-stu-id="7ff67-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
