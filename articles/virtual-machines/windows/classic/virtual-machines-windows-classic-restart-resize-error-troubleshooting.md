---
title: aaaVM reiniciar ou redimensionar problemas | Microsoft Docs
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
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="bcf6f-103">Solucionar problemas de implantação clássica ao reinicializar ou redimensionar uma máquina virtual Windows existente no Azure</span><span class="sxs-lookup"><span data-stu-id="bcf6f-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcf6f-104">Clássico</span><span class="sxs-lookup"><span data-stu-id="bcf6f-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="bcf6f-105">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="bcf6f-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="bcf6f-106">Quando você tentar toostart uma parada Máquina Virtual (VM) do Azure, ou redimensiona uma VM do Azure existente, o erro comum de saudação que encontrar é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="bcf6f-107">Esse erro ocorre quando o cluster hello ou região ou não tem recursos disponíveis ou não suporte Olá solicitada tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf6f-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bcf6f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="bcf6f-109">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="bcf6f-110">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="bcf6f-111">Coletar logs de auditoria</span><span class="sxs-lookup"><span data-stu-id="bcf6f-111">Collect audit logs</span></span>
<span data-ttu-id="bcf6f-112">toostart de solução de problemas, auditoria Olá coletar registra o erro de saudação de tooidentify associado Olá problema.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="bcf6f-113">No portal do Azure de Olá, clique em **procurar** > **máquinas virtuais** > *sua máquina virtual do Windows*  >   **Configurações de** > **logs de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="bcf6f-114">Problema: erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="bcf6f-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="bcf6f-115">Tente toostart uma VM parada mas obterão uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="bcf6f-116">Causa</span><span class="sxs-lookup"><span data-stu-id="bcf6f-116">Cause</span></span>
<span data-ttu-id="bcf6f-117">solicitação de Olá Olá toostart interrompido VM tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="bcf6f-118">No entanto, o cluster de saudação não tem solicitação de saudação do espaço livre disponível toofulfill.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="bcf6f-119">Resolução</span><span class="sxs-lookup"><span data-stu-id="bcf6f-119">Resolution</span></span>
* <span data-ttu-id="bcf6f-120">Crie um novo serviço de nuvem e o associe a uma região ou a uma rede virtual baseada em região, mas não a um grupo de afinidades.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="bcf6f-121">Excluir Olá interrompido VM.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="bcf6f-122">Recrie Olá VM no novo serviço de nuvem hello usando discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="bcf6f-123">Iniciar Olá recriado VM.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-123">Start hello re-created VM.</span></span>

<span data-ttu-id="bcf6f-124">Se você receber um erro ao tentar toocreate um novo serviço de nuvem, tente novamente mais tarde ou alterar a região Olá Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf6f-125">novo serviço de nuvem Olá terá um novo nome e o VIP, portanto, será necessário toochange essas informações para todas as dependências de saudação que usam essas informações para o serviço de nuvem existente hello.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="bcf6f-126">Problema: erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="bcf6f-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="bcf6f-127">Tente tooresize uma VM existente mas obterão uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="bcf6f-128">Causa</span><span class="sxs-lookup"><span data-stu-id="bcf6f-128">Cause</span></span>
<span data-ttu-id="bcf6f-129">solicitação Olá Olá tooresize VM tem toobe tentado no cluster original Olá serviço em nuvem Olá hosts.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="bcf6f-130">No entanto, não oferece suporte cluster Olá Olá solicitado tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="bcf6f-131">Resolução</span><span class="sxs-lookup"><span data-stu-id="bcf6f-131">Resolution</span></span>
<span data-ttu-id="bcf6f-132">Reduzir Olá solicitado tamanho da VM e repetição Olá redimensionar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="bcf6f-133">Clique em **Procurar tudo** > **Máquinas virtuais (clássicas)** > *sua máquina virtual* > **Configurações** > **Tamanho**.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="bcf6f-134">Para obter etapas detalhadas, consulte [redimensionar a máquina virtual de saudação](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="bcf6f-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="bcf6f-135">Se não for possível tooreduce Olá tamanho da VM, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="bcf6f-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="bcf6f-136">Criar um novo serviço de nuvem, garantir que não é vinculado tooan grupo de afinidade e não associado a uma rede virtual que é o grupo de afinidade tooan vinculado.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="bcf6f-137">Crie uma nova VM maior nele.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="bcf6f-138">Você pode consolidar todas as suas VMs em Olá mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="bcf6f-139">Se seu serviço de nuvem existente estiver associado uma rede virtual com base em região, você pode conectar Olá nova nuvem serviço toohello rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="bcf6f-140">Se o serviço de nuvem existente Olá não está associado uma rede virtual com base em região, depois você ter toodelete Olá VMs no serviço de nuvem existente hello e recriá-los no novo serviço de nuvem Olá de seus discos.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="bcf6f-141">No entanto, é importante tooremember que novo serviço de nuvem Olá terá um novo nome e o VIP, portanto, será necessário tooupdate para todas as dependências de saudação que atualmente usam essas informações para o serviço de nuvem existente hello.</span><span class="sxs-lookup"><span data-stu-id="bcf6f-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcf6f-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bcf6f-142">Next steps</span></span>
<span data-ttu-id="bcf6f-143">Se você encontrar problemas ao criar uma nova VM do Windows no Azure, veja [Solucionar problemas de implantação com a criação de uma máquina virtual do Windows no Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bcf6f-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

