---
title: "aaaTroubleshoot implantação de VM do Windows no Azure | Microsoft Docs"
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
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a><span data-ttu-id="3e4dc-103">Solucionar problemas de implantação ao criar uma nova VM Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="3e4dc-103">Troubleshoot deployment issues when creating a new Windows VM in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="3e4dc-104">Principais problemas</span><span class="sxs-lookup"><span data-stu-id="3e4dc-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="3e4dc-105">Para outros problemas de implantação de VM e perguntas, confira [Solucionar problemas de implantação de máquina virtual Windows no Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3e4dc-105">For other VM deployment issues and questions, see [Troubleshoot deploying Windows virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>

## <a name="collect-activity-logs"></a><span data-ttu-id="3e4dc-106">Coletar logs de atividades</span><span class="sxs-lookup"><span data-stu-id="3e4dc-106">Collect activity logs</span></span>
<span data-ttu-id="3e4dc-107">toostart solução de problemas, atividade de coletar Olá registra o erro de saudação de tooidentify associado Olá problema.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="3e4dc-108">Hello links a seguir contêm informações detalhadas sobre Olá processo toofollow.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="3e4dc-109">Exibir operações de implantação</span><span class="sxs-lookup"><span data-stu-id="3e4dc-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="3e4dc-110">Exibir logs de atividade toomanage Azure recursos</span><span class="sxs-lookup"><span data-stu-id="3e4dc-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="3e4dc-111">**Y:** se Olá sistema operacional for Windows generalizado e ele é carregado e/ou capturado com hello generalizado configuração, não haja erros.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-111">**Y:** If hello OS is Windows generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="3e4dc-112">Da mesma forma, se Olá SO é especializada do Windows, e ele é carregado e/ou capturado com hello especializado configuração, e não haja erros.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-112">Similarly, if hello OS is Windows specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="3e4dc-113">**Erros de upload:**</span><span class="sxs-lookup"><span data-stu-id="3e4dc-113">**Upload Errors:**</span></span>

<span data-ttu-id="3e4dc-114">**N<sup>1</sup>:** se Olá sistema operacional for Windows generalizado e ele é carregado como especializado, você obterá um erro de tempo limite de provisionamento com hello VM presa na tela OOBE hello.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-114">**N<sup>1</sup>:** If hello OS is Windows generalized, and it is uploaded as specialized, you will get a provisioning timeout error with hello VM stuck at hello OOBE screen.</span></span>

<span data-ttu-id="3e4dc-115">**N<sup>2</sup>:** se Olá SO é especializada do Windows, e ele é carregado como generalizado, você receberá um erro de falha de provisionamento com hello VM presa na tela OOBE Olá porque hello nova máquina virtual está em execução com o computador original Olá nome, nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-115">**N<sup>2</sup>:** If hello OS is Windows specialized, and it is uploaded as generalized, you will get a provisioning failure error with hello VM stuck at hello OOBE screen because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="3e4dc-116">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="3e4dc-116">**Resolution**</span></span>

<span data-ttu-id="3e4dc-117">tooresolve ambos esses erros, use [tooupload AzureRmVhd adicionar Olá VHD original](https://msdn.microsoft.com/library/mt603554.aspx), disponíveis no local, com hello configuração mesmo que para hello (generalizado/especializado) de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-117">tooresolve both these errors, use [Add-AzureRmVhd tooupload hello original VHD](https://msdn.microsoft.com/library/mt603554.aspx), available on-premises, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="3e4dc-118">tooupload como generalizado, lembre-se sysprep toorun primeiro.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-118">tooupload as generalized, remember toorun sysprep first.</span></span>

<span data-ttu-id="3e4dc-119">**Erros de captura:**</span><span class="sxs-lookup"><span data-stu-id="3e4dc-119">**Capture Errors:**</span></span>

<span data-ttu-id="3e4dc-120">**N<sup>3</sup>:** se Olá sistema operacional for Windows generalizada e ele é capturado como especializado, você obterá um erro de tempo limite de provisionamento porque Olá original VM não é utilizável que está marcado como generalizado.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-120">**N<sup>3</sup>:** If hello OS is Windows generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="3e4dc-121">**N<sup>4</sup>:** se Olá SO é especializada do Windows, e eles são capturados como generalizado, você receberá um erro de falha no provisionamento porque hello nova máquina virtual está em execução com o nome do computador original hello, username e password.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-121">**N<sup>4</sup>:** If hello OS is Windows specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username, and password.</span></span> <span data-ttu-id="3e4dc-122">Além disso, Olá original VM não é utilizável porque ele está marcado como especializadas.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="3e4dc-123">**Resolução**</span><span class="sxs-lookup"><span data-stu-id="3e4dc-123">**Resolution**</span></span>

<span data-ttu-id="3e4dc-124">tooresolve ambos esses erros, excluir imagem atual de saudação do portal de saudação e [recapturá-lo da saudação VHDs atuais](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) com Olá a mesma configuração que para hello (generalizado/especializado) de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a><span data-ttu-id="3e4dc-125">Problema: imagem personalizada/da galeria/do Marketplace; falha de alocação</span><span class="sxs-lookup"><span data-stu-id="3e4dc-125">Issue: Custom/gallery/marketplace image; allocation failure</span></span>
<span data-ttu-id="3e4dc-126">Esse erro ocorre em situações quando Olá nova solicitação VM é cluster tooa fixo que não oferece suporte a tamanho da VM hello está sendo solicitado ou não tem uma solicitação de saudação do tooaccommodate de espaço livre disponível.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="3e4dc-127">**Causa 1:** não oferece suporte a cluster Olá Olá solicitado tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="3e4dc-128">**Resolução 1:**</span><span class="sxs-lookup"><span data-stu-id="3e4dc-128">**Resolution 1:**</span></span>

* <span data-ttu-id="3e4dc-129">Repita a solicitação de saudação com um tamanho menor de VM.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="3e4dc-130">Se hello tamanho Olá solicitado de que VM não pode ser alterada:</span><span class="sxs-lookup"><span data-stu-id="3e4dc-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="3e4dc-131">Pare todas as VMs Olá Olá conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="3e4dc-132">Clique em **Grupos de recursos** > *seu grupo de recursos* > **Recursos** > *seu conjunto de disponibilidade* > **Máquinas Virtuais** > *sua máquina virtual* > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="3e4dc-133">Depois que todos hello parar máquinas virtuais, criar hello nova VM no hello desejado de tamanho.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="3e4dc-134">Iniciar Olá nova VM primeiro e, em seguida, selecione Olá interrompido VMs e clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="3e4dc-135">**Causa 2:** Olá cluster não tem recursos gratuitos.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="3e4dc-136">**Resolução 2:**</span><span class="sxs-lookup"><span data-stu-id="3e4dc-136">**Resolution 2:**</span></span>

* <span data-ttu-id="3e4dc-137">Repita a solicitação de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="3e4dc-138">Se hello nova VM pode ser definida parte de uma disponibilidade diferente</span><span class="sxs-lookup"><span data-stu-id="3e4dc-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="3e4dc-139">Criar uma nova VM em um conjunto de disponibilidade diferente (em Olá mesma região).</span><span class="sxs-lookup"><span data-stu-id="3e4dc-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="3e4dc-140">Adicionar Olá nova VM toohello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3e4dc-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e4dc-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e4dc-141">Next steps</span></span>
<span data-ttu-id="3e4dc-142">Se você encontrar problemas ao iniciar uma VM do Windows parada ou redimensionar uma VM do Windows existente no Azure, consulte [Solucionar problemas de implantação do Resource Manager com a reinicialização ou o redimensionamento de uma máquina virtual Windows no Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e4dc-142">If you encounter issues when you start a stopped Windows VM or resize an existing Windows VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

