---
title: aaaVM reiniciar ou redimensionar problemas no Azure | Microsoft Docs
description: "Solucionar problemas de implantação do Resource Manager com a reinicialização ou o redimensionamento de uma máquina virtual Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 0756b52d-4f5a-4503-ae45-c00a6a2edcdf
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.workload: required
ms.date: 06/13/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cf7c2d19bf5f79fab4ffc0eff9ccc1182d601c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-windows-vm-in-azure"></a><span data-ttu-id="870c5-103">Solucionar problemas de implantação ao reiniciar ou redimensionar uma VM Windows existente no Azure</span><span class="sxs-lookup"><span data-stu-id="870c5-103">Troubleshoot deployment issues with restarting or resizing an existing Windows VM in Azure</span></span>
<span data-ttu-id="870c5-104">Quando você tentar toostart uma parada Máquina Virtual (VM) do Azure, ou redimensiona uma VM do Azure existente, o erro comum de saudação que encontrar é uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="870c5-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="870c5-105">Esse erro ocorre quando o cluster hello ou região ou não tem recursos disponíveis ou não suporte Olá solicitada tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="870c5-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="870c5-106">Coletar logs de atividades</span><span class="sxs-lookup"><span data-stu-id="870c5-106">Collect activity logs</span></span>
<span data-ttu-id="870c5-107">toostart solução de problemas, atividade de coletar Olá registra o erro de saudação de tooidentify associado Olá problema.</span><span class="sxs-lookup"><span data-stu-id="870c5-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="870c5-108">Olá links a seguir contêm informações detalhadas sobre o processo de saudação:</span><span class="sxs-lookup"><span data-stu-id="870c5-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="870c5-109">Exibir operações de implantação</span><span class="sxs-lookup"><span data-stu-id="870c5-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="870c5-110">Exibir logs de atividade toomanage Azure recursos</span><span class="sxs-lookup"><span data-stu-id="870c5-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="870c5-111">Problema: erro ao iniciar uma VM parada</span><span class="sxs-lookup"><span data-stu-id="870c5-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="870c5-112">Tente toostart uma VM parada mas obterão uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="870c5-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="870c5-113">Causa</span><span class="sxs-lookup"><span data-stu-id="870c5-113">Cause</span></span>
<span data-ttu-id="870c5-114">solicitação de Olá Olá toostart interrompido VM tem toobe tentado no cluster original de saudação que hospeda o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="870c5-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="870c5-115">No entanto, o cluster de saudação não tem solicitação de saudação do espaço livre disponível toofulfill.</span><span class="sxs-lookup"><span data-stu-id="870c5-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="870c5-116">Resolução</span><span class="sxs-lookup"><span data-stu-id="870c5-116">Resolution</span></span>
* <span data-ttu-id="870c5-117">Pare Olá todas as VMs em disponibilidade Olá definido e, em seguida, reiniciar cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="870c5-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="870c5-118">Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="870c5-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="870c5-119">Depois que todos os Olá parar de VMs, selecione cada uma das VMs Olá interrompido e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="870c5-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="870c5-120">Repita a solicitação de reinicialização de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="870c5-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="870c5-121">Problema: erro ao redimensionar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="870c5-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="870c5-122">Tente tooresize uma VM existente mas obterão uma falha de alocação.</span><span class="sxs-lookup"><span data-stu-id="870c5-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="870c5-123">Causa</span><span class="sxs-lookup"><span data-stu-id="870c5-123">Cause</span></span>
<span data-ttu-id="870c5-124">solicitação Olá Olá tooresize VM tem toobe tentado no cluster original Olá serviço em nuvem Olá hosts.</span><span class="sxs-lookup"><span data-stu-id="870c5-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="870c5-125">No entanto, não oferece suporte cluster Olá Olá solicitado tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="870c5-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="870c5-126">Resolução</span><span class="sxs-lookup"><span data-stu-id="870c5-126">Resolution</span></span>
* <span data-ttu-id="870c5-127">Repita a solicitação de saudação com um tamanho menor de VM.</span><span class="sxs-lookup"><span data-stu-id="870c5-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="870c5-128">Se hello tamanho Olá solicitado de que VM não pode ser alterada:</span><span class="sxs-lookup"><span data-stu-id="870c5-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="870c5-129">Pare todas as VMs Olá Olá conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="870c5-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="870c5-130">Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="870c5-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="870c5-131">Depois que todos os hello VMs parar, redimensione a VM de saudação desejado tooa tamanho maior.</span><span class="sxs-lookup"><span data-stu-id="870c5-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="870c5-132">Selecione Olá redimensionado VM e clique em **iniciar**, e, em seguida, iniciar Olá interrompido VMs.</span><span class="sxs-lookup"><span data-stu-id="870c5-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="870c5-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="870c5-133">Next steps</span></span>
<span data-ttu-id="870c5-134">Se você encontrar problemas ao criar uma nova VM do Windows no Azure, veja [Solucionar problemas de implantação com a criação de uma nova máquina virtual do Windows no Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="870c5-134">If you encounter issues when you create a new Windows VM in Azure, see [Troubleshoot deployment issues with creating a new Windows virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

