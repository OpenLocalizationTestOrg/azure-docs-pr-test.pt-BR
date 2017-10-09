---
title: "aaaTroubleshoot Implantando problemas de máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Solução de problemas de implantação de máquina virtual do Linux no modelo de implantação do Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="d015e-103">Solução de problemas de implantação de máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="d015e-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="d015e-104">tootroubleshoot problemas de implantação de máquina virtual (VM) no Azure, examine Olá [principais problemas](#top-issues) de falhas e resoluções comuns.</span><span class="sxs-lookup"><span data-stu-id="d015e-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="d015e-105">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="d015e-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="d015e-106">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="d015e-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="d015e-107">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="d015e-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="d015e-108">Principais problemas</span><span class="sxs-lookup"><span data-stu-id="d015e-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="d015e-109">não oferece suporte a cluster Olá Olá solicitado tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="d015e-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="d015e-110">Repita a solicitação de saudação com um tamanho menor de VM.</span><span class="sxs-lookup"><span data-stu-id="d015e-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="d015e-111">Se hello tamanho Olá solicitado de que VM não pode ser alterada:</span><span class="sxs-lookup"><span data-stu-id="d015e-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="d015e-112">Pare todas as VMs Olá Olá conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d015e-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="d015e-113">Clique em **Grupos de recursos** > seu grupo de recursos > **Recursos** > seu conjunto de disponibilidade > **Máquinas Virtuais** > sua máquina virtual > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="d015e-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="d015e-114">Depois que todos os Olá parar máquinas virtuais, criar hello VM de tamanho de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="d015e-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="d015e-115">Iniciar Olá nova VM primeiro e, em seguida, selecione Olá parado VMs e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="d015e-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="d015e-116">Olá cluster não tem recursos gratuitos</span><span class="sxs-lookup"><span data-stu-id="d015e-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="d015e-117">Repetir a solicitação de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="d015e-117">Retry hello request later.</span></span>
- <span data-ttu-id="d015e-118">Se hello nova VM pode ser definida parte de uma disponibilidade diferente</span><span class="sxs-lookup"><span data-stu-id="d015e-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="d015e-119">Criar uma máquina virtual em um conjunto de disponibilidade diferente (em Olá mesma região).</span><span class="sxs-lookup"><span data-stu-id="d015e-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="d015e-120">Adicionar Olá nova VM toohello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d015e-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="d015e-121">Como ativar o crédito mensal para o Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="d015e-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="d015e-122">tooactivate seu mensal de crédito, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="d015e-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="d015e-123">Por que pode não instalar Olá GPU driver para uma VM do Ubuntu NV?</span><span class="sxs-lookup"><span data-stu-id="d015e-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="d015e-124">No momento, o suporte ao GPU do Linux está disponível apenas em VMs NC do Azure que executam o Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="d015e-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="d015e-125">Para saber mais, confira [Configurar drivers GPU para VMs série N executando o Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d015e-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="d015e-126">Meus drivers estão ausentes para minha VM série N do Linux</span><span class="sxs-lookup"><span data-stu-id="d015e-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="d015e-127">Drivers para VMs baseadas em Linux estão localizados [aqui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d015e-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="d015e-128">Não é possível localizar uma instância GPU em minha VM série N</span><span class="sxs-lookup"><span data-stu-id="d015e-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="d015e-129">tootake vantagem dos recursos GPU Olá de VMs série N do Azure executando o Windows Server 2016 ou Windows Server 2012 R2, você deve instalar os drivers gráficos NVIDIA em cada VM após a implantação.</span><span class="sxs-lookup"><span data-stu-id="d015e-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="d015e-130">Também há informações de instalação de driver disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md) e [VMs do Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d015e-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="d015e-131">As VMs da série N estão disponíveis na minha região?</span><span class="sxs-lookup"><span data-stu-id="d015e-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="d015e-132">Você pode verificar a disponibilidade de saudação do hello [produtos disponíveis pela tabela de região](https://azure.microsoft.com/regions/services)e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="d015e-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="d015e-133">Não tenho toosee capaz de família de tamanho da VM que desejo ao redimensionar a minha VM.</span><span class="sxs-lookup"><span data-stu-id="d015e-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="d015e-134">Quando uma máquina virtual está em execução, é o servidor físico tooa implantado.</span><span class="sxs-lookup"><span data-stu-id="d015e-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="d015e-135">servidores físicos de saudação em regiões do Azure são agrupados em clusters de hardware físico comum.</span><span class="sxs-lookup"><span data-stu-id="d015e-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="d015e-136">Redimensionar uma VM que exige clusters de hardware Olá VM toobe movido toodifferent é diferente dependendo de qual modelo de implantação foi usado toodeploy Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d015e-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="d015e-137">As VMs implantadas no modelo de implantação clássico, implantação de serviço de nuvem Olá devem ser removidas e reimplantado tamanho do toochange Olá VMs tooa outra família de tamanho.</span><span class="sxs-lookup"><span data-stu-id="d015e-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="d015e-138">VMs implantadas no modelo de implantação do Gerenciador de recursos, você deve interromper todas as VMs no conjunto antes de alterar o tamanho de saudação de qualquer máquina virtual no conjunto de disponibilidade de saudação de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d015e-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="d015e-139">Olá listado tamanho da VM não é suportado durante a implantação no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d015e-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="d015e-140">Escolha um tamanho que é compatível com cluster do conjunto de disponibilidade hello.</span><span class="sxs-lookup"><span data-stu-id="d015e-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="d015e-141">Recomenda-se ao criar que um conjunto de disponibilidade toochoose Olá maior tamanho da VM achar que precisa e tem que ser seu toohello implantação primeiro que conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d015e-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="d015e-142">Quais versões/distribuições do Linux têm suporte no Azure?</span><span class="sxs-lookup"><span data-stu-id="d015e-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="d015e-143">Você pode encontrar a lista de saudação em Linux em [Azure-Endorsed distribuições](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="d015e-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="d015e-144">É possível adicionar um conjunto de disponibilidade de tooan clássico VM existente?</span><span class="sxs-lookup"><span data-stu-id="d015e-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="d015e-145">Sim.</span><span class="sxs-lookup"><span data-stu-id="d015e-145">Yes.</span></span> <span data-ttu-id="d015e-146">Você pode adicionar um existente clássico VM tooa nova ou conjunto de disponibilidade existente.</span><span class="sxs-lookup"><span data-stu-id="d015e-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="d015e-147">Para obter mais informações, consulte [adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="d015e-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d015e-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d015e-148">Next steps</span></span>
<span data-ttu-id="d015e-149">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="d015e-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="d015e-150">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="d015e-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="d015e-151">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="d015e-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
