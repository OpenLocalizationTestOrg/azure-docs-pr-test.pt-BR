---
title: "Solução de problemas de implantação de máquina virtual do Linux no Azure | Microsoft Docs"
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
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="9e75a-103">Solução de problemas de implantação de máquina virtual do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="9e75a-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="9e75a-104">Para solucionar problemas de implantação de VM (máquina virtual) no Azure, examine os [principais problemas](#top-issues) para falhas e resoluções comuns.</span><span class="sxs-lookup"><span data-stu-id="9e75a-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="9e75a-105">Caso precise de mais ajuda a qualquer momento neste artigo, entre em contato com os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="9e75a-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="9e75a-106">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e75a-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9e75a-107">Vá para o [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **Obter Suporte**.</span><span class="sxs-lookup"><span data-stu-id="9e75a-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="9e75a-108">Principais problemas</span><span class="sxs-lookup"><span data-stu-id="9e75a-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="9e75a-109">O cluster não dá suporte ao tamanho de VM solicitado</span><span class="sxs-lookup"><span data-stu-id="9e75a-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="9e75a-110">Repita a solicitação com um tamanho de VM menor.</span><span class="sxs-lookup"><span data-stu-id="9e75a-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="9e75a-111">Se o tamanho da VM solicitada não puder ser alterado:</span><span class="sxs-lookup"><span data-stu-id="9e75a-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="9e75a-112">Pare todas as VMs no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9e75a-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="9e75a-113">Clique em **Grupos de recursos** > seu grupo de recursos > **Recursos** > seu conjunto de disponibilidade > **Máquinas Virtuais** > sua máquina virtual > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="9e75a-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="9e75a-114">Depois de parar todas as VMs, crie a VM no tamanho desejado.</span><span class="sxs-lookup"><span data-stu-id="9e75a-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="9e75a-115">Inicie a nova VM primeiro e, em seguida, selecione cada uma das VMs paradas e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="9e75a-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="9e75a-116">O cluster não tem recursos livres</span><span class="sxs-lookup"><span data-stu-id="9e75a-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="9e75a-117">Tente fazer novamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="9e75a-117">Retry the request later.</span></span>
- <span data-ttu-id="9e75a-118">Se a nova VM puder ser parte de um conjunto de disponibilidade diferente</span><span class="sxs-lookup"><span data-stu-id="9e75a-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="9e75a-119">Crie uma nova VM em um conjunto de disponibilidade diferente (na mesma região).</span><span class="sxs-lookup"><span data-stu-id="9e75a-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="9e75a-120">Adicione a nova VM à mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9e75a-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="9e75a-121">Como ativar o crédito mensal para o Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="9e75a-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="9e75a-122">Para ativar o seu crédito mensal, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="9e75a-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="9e75a-123">Por que posso não instalar o driver GPU em uma VM Ubuntu NV?</span><span class="sxs-lookup"><span data-stu-id="9e75a-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="9e75a-124">No momento, o suporte ao GPU do Linux está disponível apenas em VMs NC do Azure que executam o Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="9e75a-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="9e75a-125">Para saber mais, confira [Configurar drivers GPU para VMs série N executando o Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9e75a-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="9e75a-126">Meus drivers estão ausentes para minha VM série N do Linux</span><span class="sxs-lookup"><span data-stu-id="9e75a-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="9e75a-127">Drivers para VMs baseadas em Linux estão localizados [aqui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9e75a-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="9e75a-128">Não é possível localizar uma instância GPU em minha VM série N</span><span class="sxs-lookup"><span data-stu-id="9e75a-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="9e75a-129">Para aproveitar as funcionalidades de GPU das VMs da série N do Azure que executam o Windows Server 2016 ou o Windows Server 2012 R2, é necessário instalar os drivers gráficos NVIDIA em cada VM após a implantação.</span><span class="sxs-lookup"><span data-stu-id="9e75a-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="9e75a-130">Também há informações de instalação de driver disponíveis para [VMs do Windows](../windows/n-series-driver-setup.md) e [VMs do Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9e75a-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="9e75a-131">As VMs da série N estão disponíveis na minha região?</span><span class="sxs-lookup"><span data-stu-id="9e75a-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="9e75a-132">Você pode verificar a disponibilidade em [Produtos disponíveis pela tabela de região](https://azure.microsoft.com/regions/services) e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="9e75a-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="9e75a-133">Não consigo ver a família de tamanho da VM que desejo ao redimensionar a minha VM.</span><span class="sxs-lookup"><span data-stu-id="9e75a-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="9e75a-134">Quando uma máquina virtual está em execução, ela é implantada em um servidor físico.</span><span class="sxs-lookup"><span data-stu-id="9e75a-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="9e75a-135">Os servidores físicos nas regiões do Azure são agrupados em clusters de hardware físico comum.</span><span class="sxs-lookup"><span data-stu-id="9e75a-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="9e75a-136">Redimensionar uma VM que requer que a VM seja movida para clusters de hardware diferentes é diferente dependendo de qual modelo de implantação foi usado para implantar a VM.</span><span class="sxs-lookup"><span data-stu-id="9e75a-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="9e75a-137">As VMs implantadas no modelo de implantação Clássico, a implantação do serviço de nuvem deve ser removida e reimplantada para alterar as VMs para um tamanho em outra família de tamanho.</span><span class="sxs-lookup"><span data-stu-id="9e75a-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="9e75a-138">Para VMs implantadas no modelo de implantação do Gerenciador de Recursos, você deve interromper todas as VMs no conjunto antes de alterar o tamanho de uma VM no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9e75a-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="9e75a-139">Não há suporte para o tamanho da VM listado durante a implantação no Conjunto de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9e75a-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="9e75a-140">Escolha um tamanho que seja compatível com o cluster do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9e75a-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="9e75a-141">É recomendável escolher o maior tamanho de VM que você achar necessário ao criar um conjunto de disponibilidade e faça com que ela seja a primeira implantação para o conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="9e75a-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="9e75a-142">Quais versões/distribuições do Linux têm suporte no Azure?</span><span class="sxs-lookup"><span data-stu-id="9e75a-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="9e75a-143">Você pode encontrar a lista no Linux em [Distribuições endossadas pelo Azure](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="9e75a-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="9e75a-144">Posso adicionar uma VM Clássica existente a um conjunto de disponibilidade?</span><span class="sxs-lookup"><span data-stu-id="9e75a-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="9e75a-145">Sim.</span><span class="sxs-lookup"><span data-stu-id="9e75a-145">Yes.</span></span> <span data-ttu-id="9e75a-146">Você pode adicionar uma VM clássica existente para um Conjunto de Disponibilidade novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="9e75a-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="9e75a-147">Para obter mais informações, consulte [Adicionar uma máquina virtual existente ao conjunto de disponibilidade](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="9e75a-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9e75a-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e75a-148">Next steps</span></span>
<span data-ttu-id="9e75a-149">Caso precise de mais ajuda a qualquer momento neste artigo, entre em contato com os especialistas do Azure nos [fóruns do Azure e do Stack Overflow no MSDN](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="9e75a-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="9e75a-150">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e75a-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="9e75a-151">Vá para o [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **Obter Suporte**.</span><span class="sxs-lookup"><span data-stu-id="9e75a-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
