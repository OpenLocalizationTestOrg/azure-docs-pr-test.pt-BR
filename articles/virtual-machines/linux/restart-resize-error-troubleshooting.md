---
title: "Problemas de reinicialização ou redimensionamento da VM no Azure | Microsoft Docs"
description: "Solucionar problemas de implantação do Resource Manager com a reinicialização ou o redimensionamento de uma máquina virtual Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="6c321-103">Solucionar problemas de implantação ao reiniciar ou redimensionar uma VM Linux existente no Azure</span><span class="sxs-lookup"><span data-stu-id="6c321-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="6c321-104">Ao tentar iniciar uma VM (Máquina Virtual) do Azure parada ou redimensionar uma VM do Azure existente, o erro comum encontrado é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="6c321-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="6c321-105">Esse erro ocorre quando o cluster ou a região não tem recursos disponíveis ou quando não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="6c321-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="6c321-106">Coletar logs de atividades</span><span class="sxs-lookup"><span data-stu-id="6c321-106">Collect activity logs</span></span>
<span data-ttu-id="6c321-107">Para iniciar a solução de problemas, colete os logs de atividades para identificar o erro associado ao problema.</span><span class="sxs-lookup"><span data-stu-id="6c321-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="6c321-108">Os links a seguir contêm informações detalhadas sobre o processo:</span><span class="sxs-lookup"><span data-stu-id="6c321-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="6c321-109">Exibir operações de implantação</span><span class="sxs-lookup"><span data-stu-id="6c321-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="6c321-110">Exibir logs de atividades para gerenciar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="6c321-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="6c321-111">Problema: erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="6c321-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="6c321-112">Você tenta iniciar uma VM parada, mas ocorre uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="6c321-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="6c321-113">Causa</span><span class="sxs-lookup"><span data-stu-id="6c321-113">Cause</span></span>
<span data-ttu-id="6c321-114">Deve-se tentar fazer a solicitação de início da VM parada no cluster original que hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6c321-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="6c321-115">No entanto, o cluster não tem espaço livre disponível para atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="6c321-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="6c321-116">Resolução</span><span class="sxs-lookup"><span data-stu-id="6c321-116">Resolution</span></span>
* <span data-ttu-id="6c321-117">Parar todas as VMs no conjunto de disponibilidade e, em seguida, reiniciar cada VM.</span><span class="sxs-lookup"><span data-stu-id="6c321-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="6c321-118">Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="6c321-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="6c321-119">Depois que todas as VMs pararem, selecione cada uma das VMs paradas e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="6c321-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="6c321-120">Repita a solicitação de reinicialização mais tarde.</span><span class="sxs-lookup"><span data-stu-id="6c321-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="6c321-121">Problema: erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="6c321-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="6c321-122">Você tenta redimensionar uma VM existente, mas ocorre uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="6c321-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="6c321-123">Causa</span><span class="sxs-lookup"><span data-stu-id="6c321-123">Cause</span></span>
<span data-ttu-id="6c321-124">Deve-se tentar fazer a solicitação de redimensionamento da VM no cluster original que hospeda o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6c321-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="6c321-125">No entanto, o cluster não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="6c321-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="6c321-126">Resolução</span><span class="sxs-lookup"><span data-stu-id="6c321-126">Resolution</span></span>
* <span data-ttu-id="6c321-127">Repita a solicitação com um tamanho de VM menor.</span><span class="sxs-lookup"><span data-stu-id="6c321-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="6c321-128">Se o tamanho da VM solicitada não puder ser alterado:</span><span class="sxs-lookup"><span data-stu-id="6c321-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="6c321-129">Pare todas as VMs no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="6c321-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="6c321-130">Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="6c321-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="6c321-131">Depois de parar todas as VMs, redimensione a VM desejada para um tamanho maior.</span><span class="sxs-lookup"><span data-stu-id="6c321-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="6c321-132">Selecione a VM redimensionada, clique em **Iniciar**e inicie cada uma das VMs paradas.</span><span class="sxs-lookup"><span data-stu-id="6c321-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c321-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c321-133">Next steps</span></span>
<span data-ttu-id="6c321-134">Se você encontrar problemas ao criar uma nova VM do Linux no Azure, veja [Solucionar problemas de implantação com a criação de uma nova máquina virtual do Linux no Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c321-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

