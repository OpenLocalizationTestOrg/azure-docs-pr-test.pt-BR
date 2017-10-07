---
title: "aaaTroubleshoot Implantando problemas de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Solução de problemas de implantação de máquina virtual do Windows no modelo de implantação do Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="77ae5-103">Solução de problemas de implantação de máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="77ae5-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="77ae5-104">tootroubleshoot problemas de implantação de máquina virtual (VM) no Azure, examine Olá [principais problemas](#top-issues) de falhas e resoluções comuns.</span><span class="sxs-lookup"><span data-stu-id="77ae5-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="77ae5-105">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="77ae5-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="77ae5-106">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ae5-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="77ae5-107">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="77ae5-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="77ae5-108">Principais problemas</span><span class="sxs-lookup"><span data-stu-id="77ae5-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="77ae5-109">não oferece suporte a cluster Olá Olá solicitado tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="77ae5-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="77ae5-110">Repita a solicitação de saudação com um tamanho menor de VM.</span><span class="sxs-lookup"><span data-stu-id="77ae5-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="77ae5-111">Se hello tamanho Olá solicitado de que VM não pode ser alterada:</span><span class="sxs-lookup"><span data-stu-id="77ae5-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="77ae5-112">Pare todas as VMs Olá Olá conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="77ae5-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="77ae5-113">Clique em **Grupos de recursos** > seu grupo de recursos > **Recursos** > seu conjunto de disponibilidade > **Máquinas Virtuais** > sua máquina virtual > **Parar**.</span><span class="sxs-lookup"><span data-stu-id="77ae5-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="77ae5-114">Depois que todos os Olá parar máquinas virtuais, criar hello VM de tamanho de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="77ae5-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="77ae5-115">Iniciar Olá nova VM primeiro e, em seguida, selecione Olá parado VMs e clique em Iniciar.</span><span class="sxs-lookup"><span data-stu-id="77ae5-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="77ae5-116">Olá cluster não tem recursos gratuitos</span><span class="sxs-lookup"><span data-stu-id="77ae5-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="77ae5-117">Repetir a solicitação de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="77ae5-117">Retry hello request later.</span></span>
- <span data-ttu-id="77ae5-118">Se hello nova VM pode ser definida parte de uma disponibilidade diferente</span><span class="sxs-lookup"><span data-stu-id="77ae5-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="77ae5-119">Criar uma máquina virtual em um conjunto de disponibilidade diferente (em Olá mesma região).</span><span class="sxs-lookup"><span data-stu-id="77ae5-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="77ae5-120">Adicionar Olá nova VM toohello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="77ae5-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="77ae5-121">Como usar e implantar uma imagem do cliente Windows no Azure?</span><span class="sxs-lookup"><span data-stu-id="77ae5-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="77ae5-122">Você pode usar o Windows 7, Windows 8 ou Windows 10 no Azure para cenários de desenvolvimento + teste, desde que você tenha uma assinatura apropriada do Visual Studio (anteriormente conhecido como MSDN).</span><span class="sxs-lookup"><span data-stu-id="77ae5-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="77ae5-123">Isso [artigo](client-images.md) contornos Olá requisitos de qualificação para executar o cliente do Windows no Azure e usos de saudação imagens da Galeria do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ae5-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="77ae5-124">Como implantar uma máquina virtual usando Olá benefício de usar híbrida (HUB)?</span><span class="sxs-lookup"><span data-stu-id="77ae5-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="77ae5-125">Há duas maneiras diferentes toodeploy Windows as máquinas virtuais com hello benefício de uso do Azure híbrido.</span><span class="sxs-lookup"><span data-stu-id="77ae5-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="77ae5-126">Para uma assinatura do Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="77ae5-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="77ae5-127">•   Implantar VMs com base em imagens específicas do Marketplace pré-configuradas com o Benefício de Uso Híbrido do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ae5-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="77ae5-128">Para o Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="77ae5-128">For Enterprise agreement:</span></span>

<span data-ttu-id="77ae5-129">•   Carregar uma VM personalizada e implantar usando um modelo do Resource Manager ou do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77ae5-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="77ae5-130">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="77ae5-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="77ae5-131">Visão geral sobre o Benefício de Uso Híbrido do Azure</span><span class="sxs-lookup"><span data-stu-id="77ae5-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="77ae5-132">Perguntas frequentes para download</span><span class="sxs-lookup"><span data-stu-id="77ae5-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="77ae5-133">[Benefício do Uso Híbrido do Azure para o Windows Server e o Windows Client](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="77ae5-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="77ae5-134">Como usar Olá benefício de usar híbrido no Azure</span><span class="sxs-lookup"><span data-stu-id="77ae5-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="77ae5-135">Como ativar o crédito mensal para o Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="77ae5-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="77ae5-136">tooactivate seu mensal de crédito, consulte este [artigo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="77ae5-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="77ae5-137">Como tooadd desenvolvimento/teste Enterprise toomy EA (Enterprise Agreement) tooget acessar imagens do cliente tooWindow?</span><span class="sxs-lookup"><span data-stu-id="77ae5-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="77ae5-138">assinaturas de toocreate de capacidade de saudação com base na Olá desenvolvimento/teste Enterprise oferecem é proprietários de tooAccount restrito que receberam permissão toodo caso por um administrador de empresa.</span><span class="sxs-lookup"><span data-stu-id="77ae5-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="77ae5-139">Olá proprietário da conta cria assinaturas via Olá Portal de conta do Azure e, em seguida, deverá adicionar os assinantes ativos do Visual Studio como administradores.</span><span class="sxs-lookup"><span data-stu-id="77ae5-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="77ae5-140">Para que eles podem gerenciar e usar recursos de saudação necessários para desenvolvimento e teste.</span><span class="sxs-lookup"><span data-stu-id="77ae5-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="77ae5-141">Para obter mais informações, consulte [Desenvolvimento/Teste Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="77ae5-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="77ae5-142">Meus drivers estão ausentes para minha VM série N do Windows</span><span class="sxs-lookup"><span data-stu-id="77ae5-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="77ae5-143">Drivers para VMs baseadas em Windows estão localizados [aqui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="77ae5-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="77ae5-144">Não é possível localizar uma instância GPU em minha VM série N</span><span class="sxs-lookup"><span data-stu-id="77ae5-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="77ae5-145">tootake vantagem dos recursos GPU Olá de VMs série N do Azure executando o Windows Server 2016 ou Windows Server 2012 R2, você deve instalar os drivers gráficos NVIDIA em cada VM após a implantação.</span><span class="sxs-lookup"><span data-stu-id="77ae5-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="77ae5-146">Também há informações de instalação de driver disponíveis para [VMs do Windows](n-series-driver-setup.md) e [VMs do Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="77ae5-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="77ae5-147">Imagens do cliente têm suporte para a série N?</span><span class="sxs-lookup"><span data-stu-id="77ae5-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="77ae5-148">Atualmente, o Azure suporta apenas série N em VMs que executam sistemas operacionais Windows Server e Linux.</span><span class="sxs-lookup"><span data-stu-id="77ae5-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="77ae5-149">As VMs da série N estão disponíveis na minha região?</span><span class="sxs-lookup"><span data-stu-id="77ae5-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="77ae5-150">Você pode verificar a disponibilidade de saudação do hello [produtos disponíveis pela tabela de região](https://azure.microsoft.com/regions/services)e preços [aqui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="77ae5-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="77ae5-151">Quais imagens de cliente é possível usar e implantar no Azure e como tooI obtê-los?</span><span class="sxs-lookup"><span data-stu-id="77ae5-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="77ae5-152">Você pode usar o Windows 7, Windows 8 ou Windows 10 no Azure para cenários de desenvolvimento + teste, desde que você tenha uma assinatura apropriada do Visual Studio (anteriormente conhecido como MSDN).</span><span class="sxs-lookup"><span data-stu-id="77ae5-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="77ae5-153">Imagens do Windows 10 estão disponíveis na Galeria do Azure Olá em [qualificados de desenvolvimento/teste oferece](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="77ae5-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="77ae5-154">Assinantes do Visual Studio em qualquer tipo de oferta também podem [adequadamente preparar e criar](prepare-for-upload-vhd-image.md) uma imagem do Windows 7, Windows 8 ou Windows 10 64 bits e, em seguida, [carregar tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="77ae5-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="77ae5-155">use Olá permanece toodev/teste limitado por assinantes ativos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77ae5-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="77ae5-156">Isso [artigo](client-images.md) contornos Olá requisitos de qualificação para executar o cliente do Windows no Azure e o uso de saudação imagens da Galeria do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ae5-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="77ae5-157">Não tenho toosee capaz de família de tamanho da VM que desejo ao redimensionar a minha VM.</span><span class="sxs-lookup"><span data-stu-id="77ae5-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="77ae5-158">Quando uma máquina virtual está em execução, é o servidor físico tooa implantado.</span><span class="sxs-lookup"><span data-stu-id="77ae5-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="77ae5-159">servidores físicos de saudação em regiões do Azure são agrupados em clusters de hardware físico comum.</span><span class="sxs-lookup"><span data-stu-id="77ae5-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="77ae5-160">Redimensionar uma VM que exige clusters de hardware Olá VM toobe movido toodifferent é diferente dependendo de qual modelo de implantação foi usado toodeploy Olá VM.</span><span class="sxs-lookup"><span data-stu-id="77ae5-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="77ae5-161">As VMs implantadas no modelo de implantação clássico, implantação de serviço de nuvem Olá devem ser removidas e reimplantado tamanho do toochange Olá VMs tooa outra família de tamanho.</span><span class="sxs-lookup"><span data-stu-id="77ae5-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="77ae5-162">VMs implantadas no modelo de implantação do Gerenciador de recursos, você deve interromper todas as VMs no conjunto antes de alterar o tamanho de saudação de qualquer máquina virtual no conjunto de disponibilidade de saudação de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="77ae5-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="77ae5-163">Olá listado tamanho da VM não é suportado durante a implantação no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="77ae5-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="77ae5-164">Escolha um tamanho que é compatível com cluster do conjunto de disponibilidade hello.</span><span class="sxs-lookup"><span data-stu-id="77ae5-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="77ae5-165">Recomenda-se ao criar que um conjunto de disponibilidade toochoose Olá maior tamanho da VM achar que precisa e tem que ser seu toohello implantação primeiro que conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="77ae5-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="77ae5-166">É possível adicionar um conjunto de disponibilidade de tooan clássico VM existente?</span><span class="sxs-lookup"><span data-stu-id="77ae5-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="77ae5-167">Sim.</span><span class="sxs-lookup"><span data-stu-id="77ae5-167">Yes.</span></span> <span data-ttu-id="77ae5-168">Você pode adicionar um existente clássico VM tooa nova ou conjunto de disponibilidade existente.</span><span class="sxs-lookup"><span data-stu-id="77ae5-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="77ae5-169">Para obter mais informações, consulte [adicionar um conjunto de disponibilidade de tooan de máquina virtual existente](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="77ae5-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="77ae5-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77ae5-170">Next steps</span></span>
<span data-ttu-id="77ae5-171">Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="77ae5-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="77ae5-172">Como alternativa, você pode registrar um incidente de suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ae5-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="77ae5-173">Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.</span><span class="sxs-lookup"><span data-stu-id="77ae5-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
