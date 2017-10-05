---
title: "Configurar pontos de extremidade em uma VM do Windows clássica | Microsoft Docs"
description: "Saiba como configurar pontos de extremidade para uma VM do Windows no portal clássico do Azure para permitir a comunicação com uma máquina virtual do Windows no Azure."
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
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="9c18d-103">Como configurar pontos de extremidade em uma máquina virtual clássica do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="9c18d-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="9c18d-104">Todas as máquinas virtuais do Windows criadas no Azure usando o modelo de implantação clássico podem se comunicar automaticamente com outras máquinas virtuais no mesmo serviço de nuvem ou rede virtual por um canal de rede privada.</span><span class="sxs-lookup"><span data-stu-id="9c18d-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="9c18d-105">No entanto, os computadores na Internet ou outras redes virtuais requerem pontos de extremidade para direcionar o tráfego de rede de entrada para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9c18d-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="9c18d-106">Este artigo também está disponível para [máquinas virtuais Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="9c18d-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c18d-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c18d-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c18d-108">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="9c18d-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9c18d-109">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="9c18d-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="9c18d-110">No modelo de implantação **Resource Manager**, os pontos de extremidade são configurados usando **NSGs (Grupos de Segurança de Rede)**.</span><span class="sxs-lookup"><span data-stu-id="9c18d-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="9c18d-111">Para obter mais informações, consulte [Permitir o acesso externo à sua VM usando o Portal do Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c18d-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="9c18d-112">Quando você cria uma máquina virtual do Windows no portal do Azure, pontos de extremidade comuns como aqueles para a Área de Trabalho Remota e a Comunicação Remota do Windows PowerShell normalmente são criados para você automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c18d-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="9c18d-113">Você pode configurar pontos de extremidade adicionais criando a máquina virtual ou posteriormente, conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="9c18d-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="9c18d-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c18d-114">Next steps</span></span>
* <span data-ttu-id="9c18d-115">Para usar um cmdlet do Azure PowerShell para configurar um ponto de extremidade de VM, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c18d-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="9c18d-116">Para usar um cmdlet do Azure PowerShell para gerenciar uma ACL em um ponto de extremidade, consulte [Como gerenciar ACLs (listas de controle de acesso) para pontos de extremidade usando o PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9c18d-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="9c18d-117">Se você criou uma máquina virtual no modelo de implantação do Resource Manager, é possível usar o Azure PowerShell para [criar grupos de segurança de rede](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) a fim de controlar o tráfego para a VM.</span><span class="sxs-lookup"><span data-stu-id="9c18d-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
