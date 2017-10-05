---
title: "Configurar pontos de extremidade em uma VM do Linux clássica | Microsoft Docs"
description: "Saiba como configurar pontos de extremidade para uma VM do Linux no Portal Clássico do Azure para permitir a comunicação com uma máquina virtual do Linux no Azure"
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
ms.openlocfilehash: 4fd8b847b0f60648d1661ce5a8667c641e616ed4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="1b47d-103">Como configurar pontos de extremidade em uma máquina virtual clássica do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="1b47d-103">How to set up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="1b47d-104">Todas as máquinas virtuais do Linux criadas no Azure usando o modelo de implantação clássico podem se comunicar automaticamente com outras máquinas virtuais no mesmo serviço de nuvem ou rede virtual por um canal de rede privada.</span><span class="sxs-lookup"><span data-stu-id="1b47d-104">All Linux virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="1b47d-105">No entanto, os computadores na Internet ou outras redes virtuais requerem pontos de extremidade para direcionar o tráfego de rede de entrada para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1b47d-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="1b47d-106">Este artigo também está disponível para [máquinas virtuais do Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b47d-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b47d-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1b47d-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1b47d-108">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="1b47d-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1b47d-109">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="1b47d-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="1b47d-110">No modelo de implantação **Resource Manager**, os pontos de extremidade são configurados usando **NSGs (Grupos de Segurança de Rede)**.</span><span class="sxs-lookup"><span data-stu-id="1b47d-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="1b47d-111">Para saber mais, consulte [Abrir portas e pontos de extremidade](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b47d-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1b47d-112">Ao criar uma máquina virtual Linux no portal do Azure, no geral, um ponto de extremidade para o SSH (Secure Shell) é criado para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1b47d-112">When you create a Linux virtual machine in the Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="1b47d-113">Você pode configurar pontos de extremidade adicionais criando a máquina virtual ou posteriormente, conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="1b47d-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="1b47d-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b47d-114">Next steps</span></span>
* <span data-ttu-id="1b47d-115">Também é possível criar um ponto de extremidade de VM usando a [Interface de Linha de Comando do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="1b47d-115">You can also create a VM endpoint by using the [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="1b47d-116">Execute o comando **azure vm endpoint create** .</span><span class="sxs-lookup"><span data-stu-id="1b47d-116">Run the **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="1b47d-117">Se você criou uma máquina virtual no modelo de implantação do Gerenciador de Recursos, é possível usar a CLI do Azure no modo do Gerenciador de Recursos para [criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) a fim de controlar o tráfego para a VM.</span><span class="sxs-lookup"><span data-stu-id="1b47d-117">If you created a virtual machine in the Resource Manager deployment model, you can use the Azure CLI in Resource Manager mode to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) to control traffic to the VM.</span></span>
