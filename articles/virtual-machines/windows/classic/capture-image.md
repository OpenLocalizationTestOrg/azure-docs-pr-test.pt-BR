---
title: aaaCapture uma imagem de uma VM do Windows Azure | Microsoft Docs
description: "Capture uma imagem de uma máquina virtual do Windows Azure criada com o modelo de implantação clássico hello."
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
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="d94a1-103">Capture uma imagem de uma máquina virtual do Windows Azure criada com o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="d94a1-103">Capture an image of an Azure Windows virtual machine created with hello classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d94a1-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d94a1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d94a1-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="d94a1-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d94a1-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d94a1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d94a1-107">Para obter informações de modelo do Resource Manager, consulte [Capturar uma imagem gerenciada de uma VM generalizada no Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d94a1-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="d94a1-108">Este artigo mostra como toocapture uma máquina virtual do Azure que executam o Windows para que você pode usá-lo como uma imagem toocreate outras máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d94a1-108">This article shows you how toocapture an Azure virtual machine running Windows so you can use it as an image toocreate other virtual machines.</span></span> <span data-ttu-id="d94a1-109">Esta imagem inclui o disco do sistema operacional Olá e discos de dados que são anexados toohello máquina de virtual.</span><span class="sxs-lookup"><span data-stu-id="d94a1-109">This image includes hello operating system disk and any data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="d94a1-110">Não inclui configurações de rede, portanto, você precisará tooset as configurações de rede ao criar outras máquinas virtuais que usam imagem Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="d94a1-110">It doesn't include networking configurations, so you'll need tooset up network configurations when you create hello other virtual machines that use hello image.</span></span>

<span data-ttu-id="d94a1-111">Repositórios do Azure Olá imagem em **imagens da VM (clássico)**, um **de computação** Olá de serviço listado quando você exibe todos os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="d94a1-111">Azure stores hello image under **VM images (classic)**, a **Compute** service that is listed when you view all hello Azure services.</span></span> <span data-ttu-id="d94a1-112">Isso é hello mesmo local onde as imagens que você carregou são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="d94a1-112">This is hello same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="d94a1-113">Para obter detalhes sobre imagens, consulte [Sobre as imagens de máquinas virtuais](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d94a1-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d94a1-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d94a1-114">Before you begin</span></span>
<span data-ttu-id="d94a1-115">Essas etapas pressupõem que você já criou uma máquina virtual do Azure e configurado o sistema operacional de hello, incluindo anexar discos de dados.</span><span class="sxs-lookup"><span data-stu-id="d94a1-115">These steps assume that you've already created an Azure virtual machine and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="d94a1-116">Se você ainda não tiver feito isso ainda, consulte Olá seguintes artigos para obter informações sobre como criar e preparar a máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="d94a1-116">If you haven't done this yet, see hello following articles for information on creating and preparing hello virtual machine:</span></span>

* [<span data-ttu-id="d94a1-117">Criar uma máquina virtual de uma imagem</span><span class="sxs-lookup"><span data-stu-id="d94a1-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="d94a1-118">Como tooattach dados de um disco tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="d94a1-118">How tooattach a data disk tooa virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="d94a1-119">Verifique se as funções de servidor de saudação são compatíveis com Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d94a1-119">Make sure hello server roles are supported with Sysprep.</span></span> <span data-ttu-id="d94a1-120">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="d94a1-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="d94a1-121">Esse processo exclui a máquina virtual original de saudação depois de ser capturada.</span><span class="sxs-lookup"><span data-stu-id="d94a1-121">This process deletes hello original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="d94a1-122">Toocapturing anterior de uma imagem de uma máquina virtual do Azure, é recomendável backup Olá máquina de virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="d94a1-122">Prior toocapturing an image of an Azure virtual machine, it is recommended hello target virtual machine be backed up.</span></span> <span data-ttu-id="d94a1-123">O backup das máquinas virtuais do Azure pode ser feito usando o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="d94a1-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="d94a1-124">Para obter detalhes, veja [Fazer backup de máquinas virtuais do Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="d94a1-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="d94a1-125">Existem outras soluções de parceiros certificados.</span><span class="sxs-lookup"><span data-stu-id="d94a1-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="d94a1-126">toofind o que está disponível no momento, pesquise hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d94a1-126">toofind out what’s currently available, search hello Azure Marketplace.</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="d94a1-127">Capturar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="d94a1-127">Capture hello virtual machine</span></span>
1. <span data-ttu-id="d94a1-128">Em Olá [portal do Azure](http://portal.azure.com), **conectar** toohello VM.</span><span class="sxs-lookup"><span data-stu-id="d94a1-128">In hello [Azure portal](http://portal.azure.com), **Connect** toohello virtual machine.</span></span> <span data-ttu-id="d94a1-129">Para obter instruções, consulte [como toosign na máquina virtual de tooa executando o Windows Server][How toosign in tooa virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="d94a1-129">For instructions, see [How toosign in tooa virtual machine running Windows Server][How toosign in tooa virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="d94a1-130">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="d94a1-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="d94a1-131">Altere o diretório de saudação muito`%windir%\system32\sysprep`, e execute sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="d94a1-131">Change hello directory too`%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="d94a1-132">Olá **ferramenta de preparação do sistema** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="d94a1-132">hello **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="d94a1-133">Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d94a1-133">Do hello following:</span></span>

   * <span data-ttu-id="d94a1-134">Em **Ação de Limpeza do Sistema**, selecione **Entrar na Configuração Inicial pelo Usuário do Sistema (OOBE)** e verifique se a opção **Generalizar** está marcada.</span><span class="sxs-lookup"><span data-stu-id="d94a1-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="d94a1-135">Para obter mais informações sobre como usar o Sysprep, consulte [como tooUse Sysprep: uma introdução][How tooUse Sysprep: An Introduction].</span><span class="sxs-lookup"><span data-stu-id="d94a1-135">For more information about using Sysprep, see [How tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="d94a1-136">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="d94a1-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="d94a1-137">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d94a1-137">Click **OK**.</span></span>

   ![Executar o Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="d94a1-139">Sysprep desliga a máquina virtual de saudação, que altera o status de saudação da máquina virtual Olá Olá portal do Azure muito**parado**.</span><span class="sxs-lookup"><span data-stu-id="d94a1-139">Sysprep shuts down hello virtual machine, which changes hello status of hello virtual machine in hello Azure portal too**Stopped**.</span></span>
6. <span data-ttu-id="d94a1-140">No portal do Azure de Olá, clique em **máquinas virtuais (clássicas)** e selecione Olá a máquina virtual que deseja toocapture.</span><span class="sxs-lookup"><span data-stu-id="d94a1-140">In hello Azure portal, click **Virtual Machines (classic)** and select hello virtual machine you want toocapture.</span></span> <span data-ttu-id="d94a1-141">Olá **imagens da VM (clássico)** grupo é listado em **de computação** quando você exibir **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="d94a1-141">hello **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="d94a1-142">Na barra de comandos de saudação, clique em **capturar**.</span><span class="sxs-lookup"><span data-stu-id="d94a1-142">On hello command bar, click **Capture**.</span></span>

   ![Capturar a máquina virtual](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="d94a1-144">Olá **captura Olá Máquina Virtual** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="d94a1-144">hello **Capture hello Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="d94a1-145">Em **nome da imagem**, digite um nome para a nova imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d94a1-145">In **Image name**, type a name for hello new image.</span></span> <span data-ttu-id="d94a1-146">Em **rótulo da imagem**, digite um rótulo para a nova imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d94a1-146">In **Image label**, type a label for hello new image.</span></span>

9. <span data-ttu-id="d94a1-147">Clique em **executei o Sysprep na máquina virtual de saudação**.</span><span class="sxs-lookup"><span data-stu-id="d94a1-147">Click **I've run Sysprep on hello virtual machine**.</span></span> <span data-ttu-id="d94a1-148">Essa caixa de seleção se refere a ações de toohello com Sysprep nas etapas 3 a 5.</span><span class="sxs-lookup"><span data-stu-id="d94a1-148">This checkbox refers toohello actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="d94a1-149">Uma imagem _deve_ ser generalizado executando o Sysprep antes de adicionar um servidor Windows tooyour o conjunto de imagens de imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d94a1-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image tooyour set of custom images.</span></span>

10. <span data-ttu-id="d94a1-150">Após a conclusão da captura hello, nova imagem de saudação se torna disponível no hello **Marketplace**, em Olá **de computação**, **imagens da VM (clássico)** contêiner.</span><span class="sxs-lookup"><span data-stu-id="d94a1-150">Once hello capture completes, hello new image becomes available in hello **Marketplace**, in hello **Compute**, **VM images (classic)** container.</span></span>

    ![Captura de imagem bem-sucedida](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="d94a1-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d94a1-152">Next steps</span></span>
<span data-ttu-id="d94a1-153">imagem de saudação é máquinas de virtuais toocreate toobe pronto usado.</span><span class="sxs-lookup"><span data-stu-id="d94a1-153">hello image is ready toobe used toocreate virtual machines.</span></span> <span data-ttu-id="d94a1-154">toodo isso, você criará uma máquina virtual selecionando Olá **mais serviços** item de menu na parte inferior de saudação do menu de serviços hello, em seguida, **imagens da VM (clássico)** em Olá **computação**grupo.</span><span class="sxs-lookup"><span data-stu-id="d94a1-154">toodo this, you'll create a virtual machine by selecting hello **More services** menu item at hello bottom of hello services menu, then **VM images (classic)** in hello **Compute** group.</span></span> <span data-ttu-id="d94a1-155">Para obter instruções, consulte [Criar uma máquina virtual de uma imagem](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="d94a1-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
