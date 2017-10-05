---
title: Capturar uma imagem de uma VM do Windows do Azure | Microsoft Docs
description: "Capture uma imagem de uma máquina virtual do Windows do Azure criada com o modelo de implantação clássico."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="88640-103">Capture uma imagem de uma máquina virtual do Windows do Azure criada com o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="88640-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="88640-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="88640-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="88640-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="88640-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="88640-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="88640-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="88640-107">Para obter informações de modelo do Resource Manager, consulte [Capturar uma imagem gerenciada de uma VM generalizada no Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="88640-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="88640-108">Esse artigo mostra como capturar uma máquina virtual do Azure executando Windows para que você a use como uma imagem para criar outras máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="88640-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="88640-109">Essa imagem inclui o disco do sistema operacional e discos de dados anexados à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="88640-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="88640-110">Ele não inclui as configurações da rede; portanto, você precisará defini-las ao criar as outras máquinas virtuais que usam a imagem.</span><span class="sxs-lookup"><span data-stu-id="88640-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="88640-111">O Azure armazena a imagem em **Imagens de VM (clássico)**, um serviço de **Computação** listado quando todos os serviços do Azure são exibidos.</span><span class="sxs-lookup"><span data-stu-id="88640-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="88640-112">Esse é o mesmo local em que as imagens que você carregou são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="88640-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="88640-113">Para obter detalhes sobre imagens, consulte [Sobre as imagens de máquinas virtuais](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="88640-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="88640-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="88640-114">Before you begin</span></span>
<span data-ttu-id="88640-115">Essas etapas assumem que você já criou uma máquina virtual do Azure e já configurou o sistema operacional, incluindo os anexos de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="88640-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="88640-116">Se você ainda não fez isso, consulte os seguintes artigos para obter informações sobre como criar e preparar a máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="88640-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="88640-117">Criar uma máquina virtual de uma imagem</span><span class="sxs-lookup"><span data-stu-id="88640-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="88640-118">Como anexar um disco de dados à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="88640-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="88640-119">Verifique se que as funções de servidor são compatíveis com Sysprep.</span><span class="sxs-lookup"><span data-stu-id="88640-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="88640-120">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="88640-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="88640-121">Esse processo exclui a máquina virtual original depois de ela ser capturada.</span><span class="sxs-lookup"><span data-stu-id="88640-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="88640-122">Antes de capturar uma imagem de uma máquina virtual do Azure, é recomendável fazer backup da máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="88640-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="88640-123">O backup das máquinas virtuais do Azure pode ser feito usando o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="88640-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="88640-124">Para obter detalhes, veja [Fazer backup de máquinas virtuais do Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="88640-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="88640-125">Existem outras soluções de parceiros certificados.</span><span class="sxs-lookup"><span data-stu-id="88640-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="88640-126">Para descobrir o que está disponível no momento, pesquise no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="88640-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="88640-127">Capturar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="88640-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="88640-128">No [portal do Azure](http://portal.azure.com), **conecte-se** à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="88640-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="88640-129">Para obter instruções, confira [Como entrar em uma máquina virtual que executa o Windows Server][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="88640-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="88640-130">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="88640-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="88640-131">Altere o diretório para `%windir%\system32\sysprep`e execute sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="88640-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="88640-132">A caixa de diálogo **Ferramenta de Preparação do Sistema** é aberta.</span><span class="sxs-lookup"><span data-stu-id="88640-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="88640-133">Faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="88640-133">Do the following:</span></span>

   * <span data-ttu-id="88640-134">Em **Ação de Limpeza do Sistema**, selecione **Entrar na Configuração Inicial pelo Usuário do Sistema (OOBE)** e verifique se a opção **Generalizar** está marcada.</span><span class="sxs-lookup"><span data-stu-id="88640-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="88640-135">Para obter mais informações sobre como usar o Sysprep, consulte [Como usar Sysprep: uma introdução][How to Use Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="88640-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="88640-136">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="88640-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="88640-137">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="88640-137">Click **OK**.</span></span>

   ![Executar o Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="88640-139">O Sysprep desliga a máquina virtual, alterando o status dela no portal do Azure para **Parado**.</span><span class="sxs-lookup"><span data-stu-id="88640-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="88640-140">No portal do Azure, clique em **Máquinas Virtuais (clássico)** e selecione a máquina virtual que você deseja capturar.</span><span class="sxs-lookup"><span data-stu-id="88640-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="88640-141">O grupo **Imagens de VM (clássico)** é listado em **Computação** ao exibir **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="88640-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="88640-142">Na barra de comandos, clique em **Capturar**.</span><span class="sxs-lookup"><span data-stu-id="88640-142">On the command bar, click **Capture**.</span></span>

   ![Capturar a máquina virtual](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="88640-144">A caixa de diálogo **Capturar máquina virtual** é exibida.</span><span class="sxs-lookup"><span data-stu-id="88640-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="88640-145">Em **Nome da imagem**, digite um nome para a nova imagem.</span><span class="sxs-lookup"><span data-stu-id="88640-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="88640-146">Em **Rótulo da imagem**, digite um rótulo para a nova imagem.</span><span class="sxs-lookup"><span data-stu-id="88640-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="88640-147">Clique em **Executei o Sysprep na máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="88640-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="88640-148">Essa caixa de seleção se refere às ações com o Sysprep nas etapas 3 a 5.</span><span class="sxs-lookup"><span data-stu-id="88640-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="88640-149">Uma imagem _deve_ ser generalizada com a execução do Sysprep antes que uma imagem do Windows Server seja adicionada ao conjunto de imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="88640-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="88640-150">Após a conclusão da captura, a nova imagem fica disponível no **Marketplace**, em **Computação**, no contêiner **Imagens de VM (clássico)**.</span><span class="sxs-lookup"><span data-stu-id="88640-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Captura de imagem bem-sucedida](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="88640-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88640-152">Next steps</span></span>
<span data-ttu-id="88640-153">A imagem está pronta para ser usada para criar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="88640-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="88640-154">Para fazer isso, você criará uma máquina virtual selecionando o item de menu **Mais serviços** na parte inferior do menu de serviços e, em seguida, **Imagens de VM (clássico)** no grupo **Computação**.</span><span class="sxs-lookup"><span data-stu-id="88640-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="88640-155">Para obter instruções, consulte [Criar uma máquina virtual de uma imagem](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="88640-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
