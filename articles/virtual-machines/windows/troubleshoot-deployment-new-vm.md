---
title: "Solucionar problemas de implantação da VM Windows no Azure| Microsoft Docs"
description: "Solucionar problemas de implantação do Resource Manager ao criar uma nova máquina virtual Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 86795ba6eab3505a3d539e4fc4e032bdeecc2e78
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="d6433-103">Solucionar problemas de implantação ao criar uma nova VM Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="d6433-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="d6433-104">Principais problemas</span><span class="sxs-lookup"><span data-stu-id="d6433-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="d6433-105">Para outros problemas de implantação de VM e perguntas, confira [Solucionar problemas de implantação de máquina virtual Windows no Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="d6433-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="d6433-106">Coletar logs de atividades</span><span class="sxs-lookup"><span data-stu-id="d6433-106">Collect activity logs</span></span>
<span data-ttu-id="d6433-107">Para iniciar a solução de problemas, colete os logs de atividades para identificar o erro associado ao problema.</span><span class="sxs-lookup"><span data-stu-id="d6433-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="d6433-108">Os links a seguir contêm informações detalhadas sobre o processo a ser seguido.</span><span class="sxs-lookup"><span data-stu-id="d6433-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="d6433-109">Exibir operações de implantação</span><span class="sxs-lookup"><span data-stu-id="d6433-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="d6433-110">Exibir logs de atividades para gerenciar recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d6433-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="d6433-111">**Y:** se o sistema operacional for Windows generalizado e ele for carregado e/ou capturado com a configuração generalizada, não haverá erros.</span><span class="sxs-lookup"><span data-stu-id="d6433-111">**Y:** If the OS is Windows generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="d6433-112">Da mesma forma, se o sistema operacional for Windows especializado e ele for carregado e/ou capturado com a configuração especializada, não haverá erros.</span><span class="sxs-lookup"><span data-stu-id="d6433-112">Similarly, if the OS is Windows specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="d6433-113">**Erros de upload:**</span><span class="sxs-lookup"><span data-stu-id="d6433-113">**Upload Errors:**</span></span>

<span data-ttu-id="d6433-114">**N<sup>1</sup>:** se o sistema operacional for Windows generalizado e ele for carregado como especializado, você receberá um erro de tempo limite de provisionamento, com a VM paralisada na tela do OOBE.</span><span class="sxs-lookup"><span data-stu-id="d6433-114">**N<sup>1</sup>:** If the OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with the VM stuck at the OOBE screen.</span></span>

<span data-ttu-id="d6433-115">**N<sup>2</sup>:** se o sistema operacional for Windows especializado e ele for carregado como generalizado, você receberá um erro de falha no provisionamento com a VM paralisada na tela do OOBE, pois a nova VM estará em execução com o nome do computador, nome de usuário e senha originais.</span><span class="sxs-lookup"><span data-stu-id="d6433-115">**N<sup>2</sup>:** If the OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with the VM stuck at the OOBE screen because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="d6433-116">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d6433-116">**Resolution**</span></span>

<span data-ttu-id="d6433-117">Para resolver ambos os erros, use o [Add-AzureRmVhd para carregar o VHD original](https://msdn.microsoft.com/library/mt603554.aspx), disponível localmente, com a mesma configuração usada para o SO (generalizado/especializado).</span><span class="sxs-lookup"><span data-stu-id="d6433-117">To resolve both these errors, use [Add-AzureRmVhd to upload the original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="d6433-118">Para carregar como generalizado, lembre-se de executar sysprep primeiro.</span><span class="sxs-lookup"><span data-stu-id="d6433-118">To upload as generalized, remember to run sysprep first.</span></span>

<span data-ttu-id="d6433-119">**Erros de captura:**</span><span class="sxs-lookup"><span data-stu-id="d6433-119">**Capture Errors:**</span></span>

<span data-ttu-id="d6433-120">**N<sup>3</sup>:** se o sistema operacional for Windows generalizado e ele for capturado como especializado, você receberá um erro de tempo limite de provisionamento, pois a VM original não será utilizável, já que estará marcada como generalizada.</span><span class="sxs-lookup"><span data-stu-id="d6433-120">**N<sup>3</sup>:** If the OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="d6433-121">**N<sup>4</sup>:** se o sistema operacional for Windows especializado e ele for capturado como generalizado, você receberá um erro de falha no provisionamento, pois a nova VM estará em execução com o nome do computador, nome de usuário e senha originais.</span><span class="sxs-lookup"><span data-stu-id="d6433-121">**N<sup>4</sup>:** If the OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username, and password.</span></span> <span data-ttu-id="d6433-122">Além disso, a VM original não será utilizável, já que estará marcada como especializada.</span><span class="sxs-lookup"><span data-stu-id="d6433-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="d6433-123">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="d6433-123">**Resolution**</span></span>

<span data-ttu-id="d6433-124">Para resolver ambos os erros, exclua a imagem atual do portal e [recapture-a dos VHDs atuais](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) com a mesma configuração usada para o sistema operacional (generalizado/especializado).</span><span class="sxs-lookup"><span data-stu-id="d6433-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="d6433-125">Problema: imagem personalizada/da galeria/do Marketplace; falha de alocação</span><span class="sxs-lookup"><span data-stu-id="d6433-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="d6433-126">Esse erro ocorre em situações nas quais a nova solicitação de VM é fixada em um cluster que não tem suporte para o tamanho da VM sendo solicitado ou não tem espaço livre disponível para acomodar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="d6433-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="d6433-127">**Causa 1:** o cluster não dá suporte ao tamanho de VM solicitado.</span><span class="sxs-lookup"><span data-stu-id="d6433-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="d6433-128">**Resolução 1:**</span><span class="sxs-lookup"><span data-stu-id="d6433-128">**Resolution 1:**</span></span>

* <span data-ttu-id="d6433-129">Repita a solicitação com um tamanho de VM menor.</span><span class="sxs-lookup"><span data-stu-id="d6433-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="d6433-130">Se o tamanho da VM solicitada não puder ser alterado:</span><span class="sxs-lookup"><span data-stu-id="d6433-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="d6433-131">Pare todas as VMs no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d6433-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="d6433-132">Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="d6433-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="d6433-133">Depois de parar todas as máquinas virtuais, crie a nova VM no tamanho desejado.</span><span class="sxs-lookup"><span data-stu-id="d6433-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="d6433-134">Inicie a nova VM primeiro e, em seguida, selecione cada uma das VMs paradas e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d6433-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="d6433-135">**Causa 2:** o cluster não tem recursos livres.</span><span class="sxs-lookup"><span data-stu-id="d6433-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="d6433-136">**Resolução 2:**</span><span class="sxs-lookup"><span data-stu-id="d6433-136">**Resolution 2:**</span></span>

* <span data-ttu-id="d6433-137">Repita a solicitação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d6433-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="d6433-138">Se a nova VM puder ser parte de um conjunto de disponibilidade diferente</span><span class="sxs-lookup"><span data-stu-id="d6433-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="d6433-139">Crie uma nova VM em um conjunto de disponibilidade diferente (na mesma região).</span><span class="sxs-lookup"><span data-stu-id="d6433-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="d6433-140">Adicione a nova VM à mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d6433-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6433-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6433-141">Next steps</span></span>
<span data-ttu-id="d6433-142">Se você encontrar problemas ao iniciar uma VM do Windows parada ou redimensionar uma VM do Windows existente no Azure, consulte [Solucionar problemas de implantação do Resource Manager com a reinicialização ou o redimensionamento de uma máquina virtual Windows no Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6433-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

