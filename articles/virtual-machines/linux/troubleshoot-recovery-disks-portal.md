---
title: "aaaUse uma VM de solução de problemas no portal do Azure de saudação do Linux | Microsoft Docs"
description: "Saiba como problemas de máquinas virtuais Linux tootroubleshoot usando conexão Olá OS disco tooa recuperação VM Olá portal do Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="8d527-103">Solucionar problemas de uma VM do Linux, anexando a VM de recuperação do hello OS disco tooa usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8d527-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="8d527-104">Se sua máquina virtual do Linux (VM) encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="8d527-105">Um exemplo comum seria uma entrada inválida na `/etc/fstab` que impede que Olá VM seja capaz de tooboot com êxito.</span><span class="sxs-lookup"><span data-stu-id="8d527-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="8d527-106">Este artigo detalha como toouse Olá tooconnect portal do Azure seu virtual rígida disco tooanother VM Linux toofix quaisquer erros e crie novamente sua VM original.</span><span class="sxs-lookup"><span data-stu-id="8d527-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="8d527-107">Visão geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="8d527-107">Recovery process overview</span></span>
<span data-ttu-id="8d527-108">Olá Solucionando problemas do processo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8d527-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="8d527-109">Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="8d527-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="8d527-110">Anexar e monte tooanother de disco rígido virtual Olá VM Linux para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="8d527-111">Conecte-se toohello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="8d527-112">Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="8d527-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="8d527-113">Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="8d527-114">Crie uma VM usando Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="8d527-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="8d527-115">Determinar problemas de inicialização</span><span class="sxs-lookup"><span data-stu-id="8d527-115">Determine boot issues</span></span>
<span data-ttu-id="8d527-116">Examine o diagnóstico de inicialização hello e toodetermine de captura de tela VM por que a VM não é capaz de tooboot corretamente.</span><span class="sxs-lookup"><span data-stu-id="8d527-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="8d527-117">Um exemplo comum seria uma entrada inválida em `/etc/fstab` ou a exclusão ou movimentação do disco rígido virtual subjacente.</span><span class="sxs-lookup"><span data-stu-id="8d527-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="8d527-118">Selecione a VM no portal de saudação e, em seguida, role para baixo toohello **suporte + solução de problemas** seção.</span><span class="sxs-lookup"><span data-stu-id="8d527-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="8d527-119">Clique em **diagnósticos de inicialização** mensagens do console Olá tooview transmitido de sua VM.</span><span class="sxs-lookup"><span data-stu-id="8d527-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="8d527-120">Revisão Olá logs do console toosee se você pode determinar por que hello VM estiver apresentando um problema.</span><span class="sxs-lookup"><span data-stu-id="8d527-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="8d527-121">Olá exemplo a seguir mostra que uma VM presa no modo de manutenção que requer interação manual:</span><span class="sxs-lookup"><span data-stu-id="8d527-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Exibindo os logs do console do diagnóstico de inicialização da VM](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="8d527-123">Você também pode clicar em **captura de tela de** na superior Olá Olá inicialização diagnostics log toodownload uma captura de captura de tela VM hello.</span><span class="sxs-lookup"><span data-stu-id="8d527-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="8d527-124">Exibir detalhes do disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="8d527-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="8d527-125">Antes que você pode anexar o disco rígido virtual de tooanother VM, é necessário tooidentify nome de saudação do hello virtual VHD (disco rígido).</span><span class="sxs-lookup"><span data-stu-id="8d527-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="8d527-126">Selecione o grupo de recursos do portal de saudação e selecione sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8d527-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="8d527-127">Clique em **Blobs**, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="8d527-127">Click **Blobs**, as in hello following example:</span></span>

![Selecionar os blobs de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="8d527-129">Normalmente, você tem um contêiner chamado **vhds** que armazena os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="8d527-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="8d527-130">Selecione Olá contêiner tooview uma lista de discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="8d527-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="8d527-131">Nome de saudação de observação do seu VHD (prefixo Olá geralmente é Olá nome da VM):</span><span class="sxs-lookup"><span data-stu-id="8d527-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Identificar o VHD no contêiner de armazenamento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="8d527-133">Selecione o disco rígido virtual existente na lista de saudação e copie a URL de saudação para uso em Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d527-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Copiar a URL do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="8d527-135">Excluir VM existente</span><span class="sxs-lookup"><span data-stu-id="8d527-135">Delete existing VM</span></span>
<span data-ttu-id="8d527-136">Discos rígidos virtuais e VMs são dois recursos distintos no Azure.</span><span class="sxs-lookup"><span data-stu-id="8d527-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="8d527-137">Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações.</span><span class="sxs-lookup"><span data-stu-id="8d527-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="8d527-138">Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="8d527-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="8d527-139">Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="8d527-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="8d527-140">Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída.</span><span class="sxs-lookup"><span data-stu-id="8d527-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="8d527-141">concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.</span><span class="sxs-lookup"><span data-stu-id="8d527-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="8d527-142">Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="8d527-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="8d527-143">Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8d527-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="8d527-144">Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d527-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="8d527-145">Selecione a VM no portal de saudação, clique **excluir**:</span><span class="sxs-lookup"><span data-stu-id="8d527-145">Select your VM in hello portal, then click **Delete**:</span></span>

![Captura de tela do diagnóstico de inicialização da VM mostrando um erro de inicialização](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="8d527-147">Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="8d527-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="8d527-148">concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8d527-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="8d527-149">Anexar tooanother de disco rígido virtual existente VM</span><span class="sxs-lookup"><span data-stu-id="8d527-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="8d527-150">Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="8d527-151">Anexar Olá toothis do disco rígido virtual existente VM toobe capaz de toobrowse de solução de problemas e editar o conteúdo do disco hello.</span><span class="sxs-lookup"><span data-stu-id="8d527-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="8d527-152">Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="8d527-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="8d527-153">Escolha ou crie outro toouse VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="8d527-154">Selecione o grupo de recursos do portal de saudação e selecione a VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="8d527-155">Selecione **Discos** e clique em **Anexar existente**:</span><span class="sxs-lookup"><span data-stu-id="8d527-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Anexar um disco existente no portal de saudação](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="8d527-157">tooselect o disco rígido virtual existente, clique em **arquivo VHD**:</span><span class="sxs-lookup"><span data-stu-id="8d527-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Procurar VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="8d527-159">Selecione sua conta de armazenamento e seu contêiner e clique no VHD existente.</span><span class="sxs-lookup"><span data-stu-id="8d527-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="8d527-160">Clique em Olá **selecione** botão tooconfirm sua escolha:</span><span class="sxs-lookup"><span data-stu-id="8d527-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Selecionar o VHD existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="8d527-162">Com o VHD selecionado agora, clique em **Okey** tooattach Olá disco rígido virtual existente:</span><span class="sxs-lookup"><span data-stu-id="8d527-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Confirmar a anexação do disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="8d527-164">Depois de alguns segundos, Olá **discos** painel para sua VM lista o disco rígido virtual existente conectado como um disco de dados:</span><span class="sxs-lookup"><span data-stu-id="8d527-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disco rígido virtual existente anexado como um disco de dados](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="8d527-166">Montar o disco de dados anexado Olá</span><span class="sxs-lookup"><span data-stu-id="8d527-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="8d527-167">Olá exemplos a seguir detalham etapas Olá necessárias em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8d527-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="8d527-168">Se você estiver usando uma distribuição diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá locais de arquivo de log e `mount` comandos podem ser um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="8d527-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="8d527-169">Consulte a documentação de toohello para sua distribuição específica para as alterações apropriadas Olá em comandos.</span><span class="sxs-lookup"><span data-stu-id="8d527-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="8d527-170">SSH tooyour VM usando as credenciais apropriadas Olá de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8d527-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="8d527-171">Se o disco estiver Olá primeiro dados disco anexado tooyour VM de solução de problemas, ele provavelmente está conectado muito`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="8d527-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="8d527-172">Use `dmseg` toolist anexou discos:</span><span class="sxs-lookup"><span data-stu-id="8d527-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="8d527-173">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d527-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="8d527-174">Nos Olá anterior de exemplo, disco Olá SO está em `/dev/sda` e Olá disco temporário fornecido para cada máquina virtual está em `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="8d527-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="8d527-175">Se você tiver vários discos de dados, eles deverão estar em `/dev/sdd`, `/dev/sde` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="8d527-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="8d527-176">Crie um diretório toomount seu disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8d527-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="8d527-177">Olá, exemplo a seguir cria um diretório chamado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="8d527-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="8d527-178">Se você tiver várias partições no disco rígido virtual existente, monte partição Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="8d527-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="8d527-179">exemplo a seguir Hello monta primeira partição primária Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="8d527-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="8d527-180">Prática recomendada é toomount os discos de dados em máquinas virtuais no Azure usando Olá identificador universalmente exclusivo (UUID) de disco rígido virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d527-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="8d527-181">Para este cenário de solução de problemas curto, montagem Olá disco rígido virtual usando Olá UUID não é necessário.</span><span class="sxs-lookup"><span data-stu-id="8d527-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="8d527-182">No entanto, em uso normal, edição `/etc/fstab` toomount os discos rígidos virtuais usando o nome do dispositivo, em vez de UUID pode causar Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="8d527-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="8d527-183">Corrigir problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="8d527-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="8d527-184">Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8d527-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="8d527-185">Depois que você resolveu problemas hello, continue com hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d527-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="8d527-186">Desmontar e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="8d527-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="8d527-187">Depois que os erros são resolvidos, desanexe Olá disco rígido virtual existente de sua solução de problemas de VM.</span><span class="sxs-lookup"><span data-stu-id="8d527-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="8d527-188">Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.</span><span class="sxs-lookup"><span data-stu-id="8d527-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="8d527-189">De saudação SSH tooyour de sessão VM de solução de problemas, desmonte Olá existente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="8d527-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="8d527-190">Altere primeiro fora do diretório do pai Olá para o seu ponto de montagem:</span><span class="sxs-lookup"><span data-stu-id="8d527-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="8d527-191">Agora, desmonte-Olá existente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="8d527-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="8d527-192">exemplo a seguir Hello desmonta dispositivo Olá no `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="8d527-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="8d527-193">Agora Desanexe o disco rígido virtual de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="8d527-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="8d527-194">Selecione a VM no portal de saudação e clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="8d527-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="8d527-195">Selecione o disco rígido virtual existente e clique em **Desanexar**:</span><span class="sxs-lookup"><span data-stu-id="8d527-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Desanexar um disco rígido virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="8d527-197">Aguarde até que a saudação VM tem disco desanexado com êxito Olá dados antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="8d527-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="8d527-198">Criar a VM com base no disco rígido original</span><span class="sxs-lookup"><span data-stu-id="8d527-198">Create VM from original hard disk</span></span>
<span data-ttu-id="8d527-199">toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="8d527-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="8d527-200">modelo Olá implanta uma VM em uma rede virtual existente, usando Olá URL do VHD de saudação do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="8d527-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="8d527-201">Clique em Olá **implantar tooAzure** botão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8d527-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Implantar a VM com base no modelo do GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="8d527-203">modelo de saudação é carregado no hello portal do Azure para implantação.</span><span class="sxs-lookup"><span data-stu-id="8d527-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="8d527-204">Digite os nomes de saudação para sua nova VM e os recursos do Azure existentes e, em seguida, cole Olá URL tooyour disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="8d527-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="8d527-205">implantação de saudação toobegin, clique em **compra**:</span><span class="sxs-lookup"><span data-stu-id="8d527-205">toobegin hello deployment, click **Purchase**:</span></span>

![Implantar a VM com base no modelo](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="8d527-207">Habilitar o diagnóstico de inicialização novamente</span><span class="sxs-lookup"><span data-stu-id="8d527-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="8d527-208">Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8d527-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="8d527-209">toocheck Olá status de diagnóstico de inicialização e ativar se necessário, selecione a VM no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d527-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="8d527-210">Em **Monitoramento**, clique em **Configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="8d527-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="8d527-211">Verificar status de saudação é **na**, e Olá marca de seleção ao lado de muito**diagnósticos de inicialização** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="8d527-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="8d527-212">Se fizer alguma alteração, clique em **Salvar**:</span><span class="sxs-lookup"><span data-stu-id="8d527-212">If you make any changes, click **Save**:</span></span>

![Atualizar as configurações do diagnóstico de inicialização](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="8d527-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d527-214">Next steps</span></span>
<span data-ttu-id="8d527-215">Se você estiver tendo problemas para se conectar tooyour VM, consulte [solucionar problemas de SSH conexões tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8d527-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8d527-216">Para ver problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8d527-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8d527-217">Para obter mais informações sobre como usar o Resource Manager, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8d527-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
