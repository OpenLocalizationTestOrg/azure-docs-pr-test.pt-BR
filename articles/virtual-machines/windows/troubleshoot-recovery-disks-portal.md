---
title: "Usar uma VM Windows de solução de problemas no portal do Azure | Microsoft Docs"
description: "Saiba como solucionar problemas de máquinas virtuais Windows no Azure conectando o disco do sistema operacional a uma VM de recuperação usando o portal do Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 2c1524949931d69d7553d284bb92c550a61c521a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="113a0-103">Solucionar problemas de uma VM Windows anexando o disco do sistema operacional a uma VM de recuperação usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="113a0-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="113a0-104">Se ocorrer um erro de disco ou de inicialização na VM (máquina virtual) Windows no Azure, talvez você precise realizar etapas de solução de problemas no próprio disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="113a0-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="113a0-105">Um exemplo comum seria uma atualização de aplicativo com falha que impede a inicialização bem-sucedida da VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="113a0-106">Este artigo fornece detalhes sobre como usar o portal do Azure para conectar o disco rígido virtual a outra VM Windows para corrigir erros e, em seguida, recriar a VM original.</span><span class="sxs-lookup"><span data-stu-id="113a0-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="113a0-107">Visão geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="113a0-107">Recovery process overview</span></span>
<span data-ttu-id="113a0-108">O processo de solução de problemas é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="113a0-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="113a0-109">Exclua a VM que tem problemas, mantendo os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="113a0-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="113a0-110">Anexe e monte o disco rígido virtual em outra VM Windows para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="113a0-111">Conecte-se à VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="113a0-112">Edite os arquivos ou execute as ferramentas para corrigir os problemas no disco rígido virtual original.</span><span class="sxs-lookup"><span data-stu-id="113a0-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="113a0-113">Desmonte e desanexe o disco rígido virtual da VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="113a0-114">Crie uma VM usando o disco rígido virtual original.</span><span class="sxs-lookup"><span data-stu-id="113a0-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="113a0-115">Determinar problemas de inicialização</span><span class="sxs-lookup"><span data-stu-id="113a0-115">Determine boot issues</span></span>
<span data-ttu-id="113a0-116">Para determinar por que a VM não pode ser inicializada corretamente, examine a captura de tela da VM do diagnóstico de inicialização.</span><span class="sxs-lookup"><span data-stu-id="113a0-116">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span></span> <span data-ttu-id="113a0-117">Um exemplo comum seria uma atualização de aplicativo com falha ou um disco rígido virtual subjacente que está sendo excluído ou movido.</span><span class="sxs-lookup"><span data-stu-id="113a0-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="113a0-118">Selecione a VM no portal e role para baixo até a seção **Suporte + Solução de problemas**.</span><span class="sxs-lookup"><span data-stu-id="113a0-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="113a0-119">Clique em **Diagnóstico de inicialização** para exibir a captura de tela.</span><span class="sxs-lookup"><span data-stu-id="113a0-119">Click **Boot diagnostics** to view the screenshot.</span></span> <span data-ttu-id="113a0-120">Observe códigos de erro e mensagens de erro específicos para ajudar a determinar por que a VM está com um problema.</span><span class="sxs-lookup"><span data-stu-id="113a0-120">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span></span> <span data-ttu-id="113a0-121">O seguinte exemplo mostra uma VM aguardando a interrupção dos serviços:</span><span class="sxs-lookup"><span data-stu-id="113a0-121">The following example shows a VM waiting on stopping services:</span></span>

![Exibindo os logs do console do diagnóstico de inicialização da VM](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="113a0-123">Também é possível clicar em **Captura de Tela** para baixar uma captura de tela da VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-123">You can also click **Screenshot** to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="113a0-124">Exibir detalhes do disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="113a0-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="113a0-125">Antes de anexar o disco rígido virtual a outra VM, você precisa identificar o nome do VHD (disco rígido virtual).</span><span class="sxs-lookup"><span data-stu-id="113a0-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="113a0-126">Selecione o grupo de recursos no portal e sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="113a0-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="113a0-127">Clique em **Blobs**, como no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="113a0-127">Click **Blobs**, as in the following example:</span></span>

![Selecionar os blobs de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="113a0-129">Normalmente, você tem um contêiner chamado **vhds** que armazena os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="113a0-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="113a0-130">Selecione o contêiner para exibir uma lista de discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="113a0-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="113a0-131">Anote o nome do VHD (o prefixo é geralmente o nome da VM):</span><span class="sxs-lookup"><span data-stu-id="113a0-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Identificar o VHD no contêiner de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="113a0-133">Selecione o disco rígido virtual existente na lista e copie a URL para uso nas próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="113a0-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Copiar a URL do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="113a0-135">Excluir VM existente</span><span class="sxs-lookup"><span data-stu-id="113a0-135">Delete existing VM</span></span>
<span data-ttu-id="113a0-136">Discos rígidos virtuais e VMs são dois recursos distintos no Azure.</span><span class="sxs-lookup"><span data-stu-id="113a0-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="113a0-137">Um disco rígido virtual é o local em que o próprio sistema operacional, os aplicativos e as configurações são armazenados.</span><span class="sxs-lookup"><span data-stu-id="113a0-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="113a0-138">A VM em si são apenas os metadados que definem o tamanho ou a localização e que faz referência a recursos como um disco rígido virtual ou a NIC (placa de interface de rede) virtual.</span><span class="sxs-lookup"><span data-stu-id="113a0-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="113a0-139">Cada disco rígido virtual tem uma concessão atribuída quando anexado a uma VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="113a0-140">Embora os discos de dados possam ser anexados e desanexados mesmo durante a execução da VM, o disco do sistema operacional não pode ser desanexado, a menos que o recurso de VM seja excluído.</span><span class="sxs-lookup"><span data-stu-id="113a0-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="113a0-141">A concessão continua associando o disco do sistema operacional a uma VM mesmo quando a VM está em um estado parado e desalocado.</span><span class="sxs-lookup"><span data-stu-id="113a0-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="113a0-142">A primeira etapa para recuperar a VM é excluir o recurso de VM em si.</span><span class="sxs-lookup"><span data-stu-id="113a0-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="113a0-143">A exclusão da VM deixa os discos rígidos virtuais na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="113a0-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="113a0-144">Depois que a VM for excluída, você anexa o disco rígido virtual a outra VM para solucionar os erros.</span><span class="sxs-lookup"><span data-stu-id="113a0-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="113a0-145">Selecione a VM no portal e clique em **Excluir**:</span><span class="sxs-lookup"><span data-stu-id="113a0-145">Select your VM in the portal, then click **Delete**:</span></span>

![Captura de tela do diagnóstico de inicialização da VM mostrando um erro de inicialização](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="113a0-147">Aguarde até que a VM tenha concluído a exclusão antes de anexar o disco rígido virtual a outra VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="113a0-148">A concessão no disco rígido virtual que o associa à VM precisa ser liberada antes da anexação do disco rígido virtual a outra VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="113a0-149">Anexar um disco rígido virtual existente a outra VM</span><span class="sxs-lookup"><span data-stu-id="113a0-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="113a0-150">Para as próximas etapas, você pode usar outra VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="113a0-151">Você anexa o disco rígido virtual existente a essa VM de solução de problemas para poder procurar e editar o conteúdo do disco.</span><span class="sxs-lookup"><span data-stu-id="113a0-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="113a0-152">Esse processo permite que você corrija os erros de configuração ou examine arquivos de aplicativo ou de log do sistema adicionais, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="113a0-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="113a0-153">Escolha ou crie outra VM a ser usada para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="113a0-154">Selecione o grupo de recursos no portal e a VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="113a0-155">Selecione **Discos** e clique em **Anexar existente**:</span><span class="sxs-lookup"><span data-stu-id="113a0-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Anexar um disco existente no portal](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="113a0-157">Para selecionar o disco rígido virtual existente, clique em **Arquivo VHD**:</span><span class="sxs-lookup"><span data-stu-id="113a0-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Procurar VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="113a0-159">Selecione sua conta de armazenamento e seu contêiner e clique no VHD existente.</span><span class="sxs-lookup"><span data-stu-id="113a0-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="113a0-160">Clique no botão **Selecionar** para confirmar sua escolha:</span><span class="sxs-lookup"><span data-stu-id="113a0-160">Click the **Select** button to confirm your choice:</span></span>

    ![Selecionar o VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="113a0-162">Com o VHD agora selecionado, clique em **OK** para anexar o disco rígido virtual existente:</span><span class="sxs-lookup"><span data-stu-id="113a0-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Confirmar a anexação do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="113a0-164">Depois de alguns segundos, o painel **Discos** da VM lista o disco rígido virtual existente conectado como um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="113a0-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disco rígido virtual existente anexado como um disco de dados](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="113a0-166">Montar o disco de dados anexado</span><span class="sxs-lookup"><span data-stu-id="113a0-166">Mount the attached data disk</span></span>

1. <span data-ttu-id="113a0-167">Abra uma conexão de Área de Trabalho Remota para a VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-167">Open a Remote Desktop connection to your VM.</span></span> <span data-ttu-id="113a0-168">Selecione a VM no portal e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="113a0-168">Select your VM in the portal and click **Connect**.</span></span> <span data-ttu-id="113a0-169">Baixe e abra o arquivo de conexão RDP.</span><span class="sxs-lookup"><span data-stu-id="113a0-169">Download and open the RDP connection file.</span></span> <span data-ttu-id="113a0-170">Insira suas credenciais para fazer logon na VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="113a0-170">Enter your credentials to log in to your VM as follows:</span></span>

    ![Fazer logon na VM usando a Área de Trabalho Remota](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="113a0-172">Abra **Gerenciador do Servidor** e selecione **Serviços de Arquivo e Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="113a0-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![Selecionar Serviços de Arquivo e Armazenamento no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="113a0-174">O disco de dados é detectado e anexado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="113a0-174">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="113a0-175">Para ver uma lista dos discos conectados, selecione **Discos**.</span><span class="sxs-lookup"><span data-stu-id="113a0-175">To see a list of the connected disks, select **Disks**.</span></span> <span data-ttu-id="113a0-176">É possível selecionar o disco de dados para exibir informações de volume, incluindo a letra da unidade.</span><span class="sxs-lookup"><span data-stu-id="113a0-176">You can select your data disk to view volume information, including the drive letter.</span></span> <span data-ttu-id="113a0-177">O seguinte exemplo mostra o disco de dados anexado e usando **F:**:</span><span class="sxs-lookup"><span data-stu-id="113a0-177">The following example shows the data disk attached and using **F:**:</span></span>

    ![Disco anexado e informações de volume no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="113a0-179">Corrigir problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="113a0-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="113a0-180">Com o disco rígido virtual existente montado, agora você pode realizar as etapas de manutenção e solução de problemas necessárias.</span><span class="sxs-lookup"><span data-stu-id="113a0-180">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="113a0-181">Depois de resolver os problemas, continue com as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="113a0-181">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="113a0-182">Desmontar e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="113a0-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="113a0-183">Depois de resolver os erros, desanexe o disco rígido virtual existente da VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="113a0-183">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="113a0-184">Não é possível usar o disco rígido virtual com nenhuma outra VM até que a concessão que anexa o disco rígido virtual à VM de solução de problemas seja liberada.</span><span class="sxs-lookup"><span data-stu-id="113a0-184">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="113a0-185">Na sessão RDP da VM, abra **Gerenciador do Servidor** e selecione **Serviços de Arquivo e Armazenamento**:</span><span class="sxs-lookup"><span data-stu-id="113a0-185">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![Selecionar Serviços de Arquivo e Armazenamento no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="113a0-187">Selecione **Discos** e, em seguida, o disco de dados.</span><span class="sxs-lookup"><span data-stu-id="113a0-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="113a0-188">Clique com o botão direito do mouse no disco de dados e selecione **Colocar Offline**:</span><span class="sxs-lookup"><span data-stu-id="113a0-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![Definir o disco de dados como offline no Gerenciador do Servidor](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="113a0-190">Agora desanexe o disco rígido virtual da VM.</span><span class="sxs-lookup"><span data-stu-id="113a0-190">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="113a0-191">Selecione a VM no portal do Azure e clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="113a0-191">Select your VM in the Azure portal and click **Disks**.</span></span> <span data-ttu-id="113a0-192">Selecione o disco rígido virtual existente e clique em **Desanexar**:</span><span class="sxs-lookup"><span data-stu-id="113a0-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Desanexar um disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="113a0-194">Aguarde até que a VM tenha desanexo o disco de dados corretamente antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="113a0-194">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="113a0-195">Criar a VM com base no disco rígido original</span><span class="sxs-lookup"><span data-stu-id="113a0-195">Create VM from original hard disk</span></span>
<span data-ttu-id="113a0-196">Para criar uma VM com base no disco rígido virtual original, use [esse modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="113a0-196">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="113a0-197">O modelo implanta uma VM em uma rede virtual existente, usando a URL do VHD do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="113a0-197">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="113a0-198">Clique no botão **Implantar no Azure** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="113a0-198">Click the **Deploy to Azure** button as follows:</span></span>

![Implantar a VM com base no modelo do GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="113a0-200">O modelo é carregado no portal do Azure para implantação.</span><span class="sxs-lookup"><span data-stu-id="113a0-200">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="113a0-201">Insira os nomes da nova VM e dos recursos do Azure existentes e cole a URL no disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="113a0-201">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="113a0-202">Para iniciar a implantação, clique em **Comprar**:</span><span class="sxs-lookup"><span data-stu-id="113a0-202">To begin the deployment, click **Purchase**:</span></span>

![Implantar a VM com base no modelo](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="113a0-204">Habilitar o diagnóstico de inicialização novamente</span><span class="sxs-lookup"><span data-stu-id="113a0-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="113a0-205">Ao criar a VM com base no disco rígido virtual existente, o diagnóstico de inicialização poderá não ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="113a0-205">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="113a0-206">Para verificar o status do diagnóstico de inicialização e ativá-lo, se necessário, selecione a VM no portal.</span><span class="sxs-lookup"><span data-stu-id="113a0-206">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="113a0-207">Em **Monitoramento**, clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="113a0-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="113a0-208">Verifique se o status é **Ativado** e se a marca de seleção ao lado de **Diagnóstico de inicialização** está marcada.</span><span class="sxs-lookup"><span data-stu-id="113a0-208">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="113a0-209">Se fizer alguma alteração, clique em **Salvar**:</span><span class="sxs-lookup"><span data-stu-id="113a0-209">If you make any changes, click **Save**:</span></span>

![Atualizar as configurações do diagnóstico de inicialização](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="113a0-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="113a0-211">Next steps</span></span>
<span data-ttu-id="113a0-212">Se estiver tendo problemas para se conectar à VM, consulte [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Solucionar conexões RDP a uma VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="113a0-212">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="113a0-213">Para problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="113a0-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="113a0-214">Para obter mais informações sobre como usar o Resource Manager, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="113a0-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>