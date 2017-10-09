---
title: aaaSet pontos de extremidade em uma VM do Windows classic | Microsoft Docs
description: "Saiba tooset pontos de extremidade para uma VM do Windows no hello comunicação tooallow de portal clássico do Azure com uma máquina virtual do Windows no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="f8f61-103">Como tooset pontos de extremidade em uma máquina virtual do Windows clássica no Azure</span><span class="sxs-lookup"><span data-stu-id="f8f61-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="f8f61-104">Olá a todas as janelas de máquinas virtuais que você criar no Azure usando o modelo de implantação clássico Olá automaticamente podem se comunicar através de um canal de rede privada com outras máquinas virtuais no mesmo serviço de nuvem ou rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f8f61-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="f8f61-105">No entanto, os computadores Olá Internet ou outras redes virtuais requerem pontos de extremidade toodirect Olá rede de entrada tráfego tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8f61-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="f8f61-106">Este artigo também está disponível para [máquinas virtuais Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="f8f61-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8f61-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f8f61-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f8f61-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="f8f61-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f8f61-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8f61-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="f8f61-110">Em Olá **Gerenciador de recursos de** modelo de implantação, pontos de extremidade são configurados usando **grupos de segurança de rede (NSGs)**.</span><span class="sxs-lookup"><span data-stu-id="f8f61-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="f8f61-111">Para obter mais informações, consulte [permitir acesso externo tooyour VM usando Olá portal do Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f8f61-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f8f61-112">Quando você cria uma máquina virtual Windows no hello portal do Azure, os pontos de extremidade comuns como as de área de trabalho remota e comunicação remota do Windows PowerShell são geralmente criados para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f8f61-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="f8f61-113">Você pode configurar pontos de extremidade adicionais durante a criação de máquina virtual de hello, ou posteriormente, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f8f61-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="f8f61-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8f61-114">Next steps</span></span>
* <span data-ttu-id="f8f61-115">toouse um tooset de cmdlet do PowerShell do Azure a um ponto de extremidade VM, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f61-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="f8f61-116">toouse um toomanage de cmdlet do PowerShell do Azure uma ACL em um ponto de extremidade, consulte [listas de controle de acesso de gerenciamento (ACLs) para pontos de extremidade usando o PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f8f61-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="f8f61-117">Se você criou uma máquina virtual no modelo de implantação do Gerenciador de recursos de saudação, você pode usar Azure PowerShell muito[criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol tráfego toohello VM.</span><span class="sxs-lookup"><span data-stu-id="f8f61-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
