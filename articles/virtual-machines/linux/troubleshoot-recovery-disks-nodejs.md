---
title: "aaaUse uma VM de solução de problemas com hello Azure CLI 1.0 do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de VM do Linux usando conexão Olá OS disco tooa recuperação VM Olá 1.0 da CLI do Azure"
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
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="42f9a-103">Solucionar problemas de uma VM do Linux, anexando a VM de recuperação do hello OS disco tooa usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="42f9a-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="42f9a-104">Se sua máquina virtual do Linux (VM) encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="42f9a-105">Um exemplo comum seria uma entrada inválida na `/etc/fstab` que impede que Olá VM seja capaz de tooboot com êxito.</span><span class="sxs-lookup"><span data-stu-id="42f9a-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="42f9a-106">Este artigo detalha como toouse hello Azure CLI 1.0 tooconnect seu virtual rígida disco tooanother VM Linux toofix quaisquer erros e crie novamente sua VM original.</span><span class="sxs-lookup"><span data-stu-id="42f9a-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="42f9a-107">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="42f9a-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="42f9a-108">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="42f9a-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="42f9a-109">[1.0 de CLI do Azure](#recovery-process-overview) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="42f9a-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="42f9a-110">[2.0 do CLI do Azure](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="42f9a-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="42f9a-111">Visão geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="42f9a-111">Recovery process overview</span></span>
<span data-ttu-id="42f9a-112">Olá Solucionando problemas do processo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="42f9a-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="42f9a-113">Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="42f9a-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="42f9a-114">Anexar e monte tooanother de disco rígido virtual Olá VM Linux para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="42f9a-115">Conecte-se toohello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="42f9a-116">Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="42f9a-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="42f9a-117">Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="42f9a-118">Crie uma VM usando Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="42f9a-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="42f9a-119">Certifique-se de que você tenha [hello mais recente do Azure CLI 1.0](../../cli-install-nodejs.md) instalado e conectado e usando o modo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="42f9a-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="42f9a-120">Em Olá exemplos a seguir, substitua os nomes de parâmetro com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="42f9a-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="42f9a-121">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="42f9a-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="42f9a-122">Determinar problemas de inicialização</span><span class="sxs-lookup"><span data-stu-id="42f9a-122">Determine boot issues</span></span>
<span data-ttu-id="42f9a-123">Examine Olá saída serial toodetermine por que a VM não é capaz de tooboot corretamente.</span><span class="sxs-lookup"><span data-stu-id="42f9a-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="42f9a-124">Um exemplo comum é uma entrada inválida na `/etc/fstab`, ou Olá subjacente do disco rígido virtual que está sendo excluído ou movido.</span><span class="sxs-lookup"><span data-stu-id="42f9a-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="42f9a-125">Olá exemplo a seguir obtém Olá serial saída de hello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="42f9a-126">Examine Olá saída serial toodetermine por hello VM está falhando tooboot.</span><span class="sxs-lookup"><span data-stu-id="42f9a-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="42f9a-127">Se a saída serial Olá não fornece nenhuma indicação, talvez seja necessário tooreview arquivos de log em `/var/log` depois que você tiver Olá virtual disco rígido conectado tooa VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="42f9a-128">Exibir detalhes do disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="42f9a-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="42f9a-129">Antes que você pode anexar o disco rígido virtual de tooanother VM, é necessário tooidentify nome de saudação do hello virtual VHD (disco rígido).</span><span class="sxs-lookup"><span data-stu-id="42f9a-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="42f9a-130">Olá, exemplo a seguir obtém informações de saudação VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="42f9a-131">Procure `Vhd URI` na saída de saudação da saudação anterior de comando.</span><span class="sxs-lookup"><span data-stu-id="42f9a-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="42f9a-132">Olá seguinte truncado exemplo mostra Olá `Vhd URI` na última linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="42f9a-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="42f9a-133">Excluir VM existente</span><span class="sxs-lookup"><span data-stu-id="42f9a-133">Delete existing VM</span></span>
<span data-ttu-id="42f9a-134">Discos rígidos virtuais e VMs são dois recursos distintos no Azure.</span><span class="sxs-lookup"><span data-stu-id="42f9a-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="42f9a-135">Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações.</span><span class="sxs-lookup"><span data-stu-id="42f9a-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="42f9a-136">Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="42f9a-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="42f9a-137">Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="42f9a-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="42f9a-138">Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída.</span><span class="sxs-lookup"><span data-stu-id="42f9a-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="42f9a-139">concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.</span><span class="sxs-lookup"><span data-stu-id="42f9a-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="42f9a-140">Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="42f9a-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="42f9a-141">Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="42f9a-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="42f9a-142">Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f9a-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="42f9a-143">Olá exclusões de exemplo a seguir Olá VM denominada `myVM` saudação do grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="42f9a-144">Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="42f9a-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="42f9a-145">concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.</span><span class="sxs-lookup"><span data-stu-id="42f9a-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="42f9a-146">Anexar tooanother de disco rígido virtual existente VM</span><span class="sxs-lookup"><span data-stu-id="42f9a-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="42f9a-147">Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="42f9a-148">Anexar Olá toothis do disco rígido virtual existente VM toobrowse de solução de problemas e editar o conteúdo do disco hello.</span><span class="sxs-lookup"><span data-stu-id="42f9a-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="42f9a-149">Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="42f9a-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="42f9a-150">Escolha ou crie outro toouse VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="42f9a-151">Quando você anexa Olá existente do disco rígido virtual, especifique o disco de toohello de URL de saudação obtido na saudação anterior `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="42f9a-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="42f9a-152">Olá, exemplo a seguir anexa um toohello de disco rígido virtual existente Solucionando problemas de VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="42f9a-153">Montar o disco de dados anexado Olá</span><span class="sxs-lookup"><span data-stu-id="42f9a-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="42f9a-154">Olá exemplos a seguir detalham etapas Olá necessárias em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="42f9a-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="42f9a-155">Se você estiver usando uma distribuição diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá locais de arquivo de log e `mount` comandos podem ser um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="42f9a-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="42f9a-156">Consulte a documentação de toohello para sua distribuição específica para as alterações apropriadas Olá em comandos.</span><span class="sxs-lookup"><span data-stu-id="42f9a-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="42f9a-157">SSH tooyour VM usando as credenciais apropriadas Olá de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="42f9a-158">Se o disco estiver Olá primeiro dados disco anexado tooyour Solucionando problemas de VM, disco Olá provavelmente está conectado muito`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="42f9a-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="42f9a-159">Use `dmseg` tooview anexou discos:</span><span class="sxs-lookup"><span data-stu-id="42f9a-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="42f9a-160">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="42f9a-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="42f9a-161">Nos Olá anterior de exemplo, disco Olá SO está em `/dev/sda` e Olá disco temporário fornecido para cada máquina virtual está em `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="42f9a-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="42f9a-162">Se você tiver vários discos de dados, eles deverão estar em `/dev/sdd`, `/dev/sde` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="42f9a-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="42f9a-163">Crie um diretório toomount seu disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="42f9a-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="42f9a-164">Olá, exemplo a seguir cria um diretório chamado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="42f9a-165">Se você tiver várias partições no disco rígido virtual existente, monte partição Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="42f9a-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="42f9a-166">exemplo a seguir Hello monta primeira partição primária Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="42f9a-167">Prática recomendada é toomount os discos de dados em máquinas virtuais no Azure usando Olá identificador universalmente exclusivo (UUID) de disco rígido virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="42f9a-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="42f9a-168">Para este cenário de solução de problemas curto, montagem Olá disco rígido virtual usando Olá UUID não é necessário.</span><span class="sxs-lookup"><span data-stu-id="42f9a-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="42f9a-169">No entanto, em uso normal, edição `/etc/fstab` toomount os discos rígidos virtuais usando o nome do dispositivo, em vez de UUID pode causar Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="42f9a-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="42f9a-170">Corrigir problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="42f9a-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="42f9a-171">Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="42f9a-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="42f9a-172">Depois que você resolveu problemas hello, continue com hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="42f9a-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="42f9a-173">Desmontar e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="42f9a-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="42f9a-174">Depois que os erros são resolvidos, você desmontar e desanexar Olá existente do disco rígido virtual da VM sua solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="42f9a-175">Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.</span><span class="sxs-lookup"><span data-stu-id="42f9a-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="42f9a-176">De saudação SSH tooyour de sessão VM de solução de problemas, desmonte Olá existente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="42f9a-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="42f9a-177">Altere primeiro fora do diretório do pai Olá para o seu ponto de montagem:</span><span class="sxs-lookup"><span data-stu-id="42f9a-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="42f9a-178">Agora, desmonte-Olá existente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="42f9a-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="42f9a-179">exemplo a seguir Hello desmonta dispositivo Olá no `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="42f9a-180">Agora Desanexe o disco rígido virtual de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="42f9a-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="42f9a-181">Sair Olá SSH sessão tooyour VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="42f9a-182">No hello CLI do Azure, primeiro Olá de lista anexado tooyour de discos de dados VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="42f9a-183">Olá, exemplo a seguir lista Olá discos de dados anexado toohello VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="42f9a-184">Saudação de Observação `Lun` valor para o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="42f9a-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="42f9a-185">Olá, saída de comando de exemplo a seguir mostra disco virtual existente Olá anexado ao LUN 0:</span><span class="sxs-lookup"><span data-stu-id="42f9a-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="42f9a-186">Desanexar o disco de dados Olá de sua VM usando Olá aplicável `Lun` valor:</span><span class="sxs-lookup"><span data-stu-id="42f9a-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="42f9a-187">Criar a VM com base no disco rígido original</span><span class="sxs-lookup"><span data-stu-id="42f9a-187">Create VM from original hard disk</span></span>
<span data-ttu-id="42f9a-188">toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="42f9a-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="42f9a-189">modelo JSON real Hello está no hello link a seguir:</span><span class="sxs-lookup"><span data-stu-id="42f9a-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="42f9a-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="42f9a-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="42f9a-191">modelo Olá implanta uma VM em uma rede virtual existente, usando Olá URL do VHD de saudação do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="42f9a-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="42f9a-192">Olá exemplo a seguir implanta o grupo de recursos do hello modelo toohello chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="42f9a-193">Saudação de resposta solicita modelo hello como o nome da VM (`myDeployedVM` Olá exemplo a seguir), tipo de sistema operacional (`Linux`) e o tamanho da VM (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="42f9a-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="42f9a-194">Olá `osDiskVhdUri` é Olá mesmo usada anteriormente ao anexar Olá toohello do disco rígido virtual existente VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="42f9a-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="42f9a-195">Um exemplo de saída do comando hello e prompts é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="42f9a-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="42f9a-196">Habilitar o diagnóstico de inicialização novamente</span><span class="sxs-lookup"><span data-stu-id="42f9a-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="42f9a-197">Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="42f9a-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="42f9a-198">Olá exemplo a seguir habilita a extensão de diagnóstico Olá no hello VM denominada `myDeployedVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="42f9a-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="42f9a-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42f9a-199">Next steps</span></span>
<span data-ttu-id="42f9a-200">Se você estiver tendo problemas para se conectar tooyour VM, consulte [solucionar problemas de SSH conexões tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42f9a-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="42f9a-201">Para ver problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42f9a-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
