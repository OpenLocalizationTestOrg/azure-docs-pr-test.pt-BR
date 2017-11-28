---
title: "Problemas de reinicialização ou redimensionamento da VM | Microsoft Docs"
description: "Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma máquina virtual Windows existente no Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 7fe0636366c60d4679cfc69bd96cd532695b080e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="8db1c-103">Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma máquina virtual Windows existente no Azure</span><span class="sxs-lookup"><span data-stu-id="8db1c-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8db1c-104">Clássico</span><span class="sxs-lookup"><span data-stu-id="8db1c-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="8db1c-105">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="8db1c-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="8db1c-106">Ao tentar iniciar uma VM (Máquina Virtual) do Azure parada ou redimensionar uma VM do Azure existente, o erro comum encontrado é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="8db1c-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="8db1c-107">Esse erro ocorre quando o cluster ou a região não tem recursos disponíveis ou quando não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="8db1c-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8db1c-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8db1c-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8db1c-109">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="8db1c-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="8db1c-110">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="8db1c-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="8db1c-111">Coletar logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="8db1c-111">Collect audit logs</span></span>
<span data-ttu-id="8db1c-112">Para iniciar a solução de problemas, colete os logs de auditoria para identificar o erro associado ao problema.</span><span class="sxs-lookup"><span data-stu-id="8db1c-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="8db1c-113">No Portal do Azure, clique em **Procurar** > **Máquinas virtuais** > *sua máquina virtual Windows* > **Configurações** > **Logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="8db1c-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="8db1c-114">Problema: erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="8db1c-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="8db1c-115">Você tenta iniciar uma VM parada, mas ocorre uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="8db1c-115">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="8db1c-116">Causa</span><span class="sxs-lookup"><span data-stu-id="8db1c-116">Cause</span></span>
<span data-ttu-id="8db1c-117">Deve-se tentar fazer a solicitação de início da VM parada no cluster original que hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8db1c-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="8db1c-118">No entanto, o cluster não tem espaço livre disponível para atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="8db1c-118">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="8db1c-119">Resolução</span><span class="sxs-lookup"><span data-stu-id="8db1c-119">Resolution</span></span>
* <span data-ttu-id="8db1c-120">Crie um novo serviço de nuvem e o associe a uma região ou a uma rede virtual baseada em região, mas não a um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="8db1c-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="8db1c-121">Exclua a VM parada.</span><span class="sxs-lookup"><span data-stu-id="8db1c-121">Delete the stopped VM.</span></span>
* <span data-ttu-id="8db1c-122">Recrie a VM no novo serviço de nuvem usando os discos.</span><span class="sxs-lookup"><span data-stu-id="8db1c-122">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="8db1c-123">Inicie a VM recriada.</span><span class="sxs-lookup"><span data-stu-id="8db1c-123">Start the re-created VM.</span></span>

<span data-ttu-id="8db1c-124">Se você obtiver um erro ao tentar criar um novo serviço de nuvem, tente novamente ou altere a região para o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8db1c-124">If you get an error when trying to create a new cloud service, either retry later or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8db1c-125">O novo serviço de nuvem terá um novo nome e VIP e, portanto, será necessário alterar essas informações em todas as dependências que usam essas informações para o serviço de nuvem existente.</span><span class="sxs-lookup"><span data-stu-id="8db1c-125">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="8db1c-126">Problema: erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="8db1c-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="8db1c-127">Você tenta redimensionar uma VM existente, mas ocorre uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="8db1c-127">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="8db1c-128">Causa</span><span class="sxs-lookup"><span data-stu-id="8db1c-128">Cause</span></span>
<span data-ttu-id="8db1c-129">Deve-se tentar fazer a solicitação de redimensionamento da VM no cluster original que hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8db1c-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="8db1c-130">No entanto, o cluster não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="8db1c-130">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="8db1c-131">Resolução</span><span class="sxs-lookup"><span data-stu-id="8db1c-131">Resolution</span></span>
<span data-ttu-id="8db1c-132">Reduza o tamanho de VM solicitado e tente fazer novamente a solicitação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8db1c-132">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="8db1c-133">Clique em **Procurar tudo** > **Máquinas virtuais (clássicas)** > *sua máquina virtual* > **Configurações** > **Tamanho**.</span><span class="sxs-lookup"><span data-stu-id="8db1c-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="8db1c-134">Para obter as etapas detalhadas, consulte [Redimensionar a máquina virtual](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="8db1c-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="8db1c-135">Se não for possível reduzir o tamanho da VM, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8db1c-135">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="8db1c-136">Crie um novo serviço de nuvem, garantindo que ele não esteja vinculado a um grupo de afinidades nem associado a uma rede virtual vinculada a um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="8db1c-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="8db1c-137">Crie uma nova VM maior nele.</span><span class="sxs-lookup"><span data-stu-id="8db1c-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="8db1c-138">É possível consolidar todas as VMs no mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8db1c-138">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="8db1c-139">Se o serviço de nuvem existente estiver associado a uma rede virtual baseada em região, será possível conectar o novo serviço de nuvem à rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8db1c-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="8db1c-140">Se o serviço de nuvem existente não estiver associado a uma rede virtual baseada em região, será necessário excluir as VMs no serviço de nuvem existente e recriá-las no novo serviço de nuvem por meio de seus discos.</span><span class="sxs-lookup"><span data-stu-id="8db1c-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="8db1c-141">No entanto, é importante lembrar-se de que o novo serviço de nuvem terá um novo nome e VIP e, portanto, será necessário atualizá-los em todas as dependências que atualmente usam essas informações para o serviço de nuvem existente.</span><span class="sxs-lookup"><span data-stu-id="8db1c-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8db1c-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8db1c-142">Next steps</span></span>
<span data-ttu-id="8db1c-143">Se você encontrar problemas ao criar uma nova VM do Windows no Azure, veja [Solucionar problemas de implantação com a criação de uma máquina virtual do Windows no Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8db1c-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

