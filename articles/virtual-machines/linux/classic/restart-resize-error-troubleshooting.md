---
title: "Problemas de reinicialização ou redimensionamento da VM | Microsoft Docs"
description: "Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma Máquina Virtual Linux existente no Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="181b9-103">Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma Máquina Virtual Linux existente no Azure</span><span class="sxs-lookup"><span data-stu-id="181b9-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="181b9-104">Clássico</span><span class="sxs-lookup"><span data-stu-id="181b9-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="181b9-105">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="181b9-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="181b9-106">Ao tentar iniciar uma VM (Máquina Virtual) do Azure parada ou redimensionar uma VM do Azure existente, o erro comum encontrado é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="181b9-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="181b9-107">Esse erro ocorre quando o cluster ou a região não tem recursos disponíveis ou quando não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="181b9-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="181b9-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="181b9-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="181b9-109">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="181b9-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="181b9-110">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="181b9-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="181b9-111">Para a versão do Resource Manager, consulte [aqui](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="181b9-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="181b9-112">Coletar logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="181b9-112">Collect audit logs</span></span>
<span data-ttu-id="181b9-113">Para iniciar a solução de problemas, colete os logs de auditoria para identificar o erro associado ao problema.</span><span class="sxs-lookup"><span data-stu-id="181b9-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="181b9-114">No Portal do Azure, clique em **Procurar** > **Máquinas virtuais** > *sua máquina virtual do Linux* > **Configurações** > **Logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="181b9-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="181b9-115">Problema: erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="181b9-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="181b9-116">Você tenta iniciar uma VM parada, mas ocorre uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="181b9-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="181b9-117">Causa</span><span class="sxs-lookup"><span data-stu-id="181b9-117">Cause</span></span>
<span data-ttu-id="181b9-118">Deve-se tentar fazer a solicitação de início da VM parada no cluster original que hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="181b9-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="181b9-119">No entanto, o cluster não tem espaço livre disponível para atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="181b9-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="181b9-120">Resolução</span><span class="sxs-lookup"><span data-stu-id="181b9-120">Resolution</span></span>
* <span data-ttu-id="181b9-121">Crie um novo serviço de nuvem e o associe a uma região ou a uma rede virtual baseada em região, mas não a um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="181b9-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="181b9-122">Exclua a VM parada.</span><span class="sxs-lookup"><span data-stu-id="181b9-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="181b9-123">Recrie a VM no novo serviço de nuvem usando os discos.</span><span class="sxs-lookup"><span data-stu-id="181b9-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="181b9-124">Inicie a VM recriada.</span><span class="sxs-lookup"><span data-stu-id="181b9-124">Start the re-created VM.</span></span>

<span data-ttu-id="181b9-125">Se você receber um erro ao tentar criar um novo serviço de nuvem, tente novamente mais tarde ou altere a região do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="181b9-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="181b9-126">O novo serviço de nuvem terá um novo nome e VIP e, portanto, será necessário alterar essas informações em todas as dependências que usam essas informações para o serviço de nuvem existente.</span><span class="sxs-lookup"><span data-stu-id="181b9-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="181b9-127">Problema: erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="181b9-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="181b9-128">Você tenta redimensionar uma VM existente, mas ocorre uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="181b9-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="181b9-129">Causa</span><span class="sxs-lookup"><span data-stu-id="181b9-129">Cause</span></span>
<span data-ttu-id="181b9-130">Deve-se tentar fazer a solicitação de redimensionamento da VM no cluster original que hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="181b9-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="181b9-131">No entanto, o cluster não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="181b9-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="181b9-132">Resolução</span><span class="sxs-lookup"><span data-stu-id="181b9-132">Resolution</span></span>
<span data-ttu-id="181b9-133">Reduza o tamanho de VM solicitado e tente fazer novamente a solicitação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="181b9-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="181b9-134">Clique em **Procurar tudo** > **Máquinas virtuais (clássicas)** > *sua máquina virtual* > **Configurações** > **Tamanho**.</span><span class="sxs-lookup"><span data-stu-id="181b9-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="181b9-135">Para obter as etapas detalhadas, consulte [Redimensionar a máquina virtual](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="181b9-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="181b9-136">Se não for possível reduzir o tamanho da VM, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="181b9-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="181b9-137">Crie um novo serviço de nuvem, garantindo que ele não esteja vinculado a um grupo de afinidades nem associado a uma rede virtual vinculada a um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="181b9-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="181b9-138">Crie uma nova VM maior nele.</span><span class="sxs-lookup"><span data-stu-id="181b9-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="181b9-139">É possível consolidar todas as VMs no mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="181b9-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="181b9-140">Se o serviço de nuvem existente estiver associado a uma rede virtual baseada em região, será possível conectar o novo serviço de nuvem à rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="181b9-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="181b9-141">Se o serviço de nuvem existente não estiver associado a uma rede virtual baseada em região, será necessário excluir as VMs no serviço de nuvem existente e recriá-las no novo serviço de nuvem por meio de seus discos.</span><span class="sxs-lookup"><span data-stu-id="181b9-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="181b9-142">No entanto, é importante lembrar-se de que o novo serviço de nuvem terá um novo nome e VIP e, portanto, será necessário atualizá-los em todas as dependências que atualmente usam essas informações para o serviço de nuvem existente.</span><span class="sxs-lookup"><span data-stu-id="181b9-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="181b9-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="181b9-143">Next steps</span></span>
<span data-ttu-id="181b9-144">Se você encontrar problemas ao criar uma nova VM do Linux no Azure, veja [Solucionar problemas de implantação com a criação de uma nova máquina virtual do Linux no Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="181b9-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

