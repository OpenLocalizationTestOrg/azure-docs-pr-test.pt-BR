---
title: "aaaUse uma VM de solução de problemas com hello Azure 2.0 do CLI do Linux | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de VM do Linux usando conexão Olá OS disco tooa recuperação VM Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="3cad7-103">Solucionar problemas de uma VM do Linux, anexando Olá OS disco tooa VM de recuperação com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3cad7-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="3cad7-104">Se sua máquina virtual do Linux (VM) encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="3cad7-105">Um exemplo comum seria uma entrada inválida na `/etc/fstab` que impede que Olá VM seja capaz de tooboot com êxito.</span><span class="sxs-lookup"><span data-stu-id="3cad7-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="3cad7-106">Este artigo detalha como toouse hello Azure CLI 2.0 tooconnect seu virtual rígida disco tooanother VM Linux toofix quaisquer erros e crie novamente sua VM original.</span><span class="sxs-lookup"><span data-stu-id="3cad7-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="3cad7-107">Você também pode executar essas etapas com hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3cad7-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="3cad7-108">Visão geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="3cad7-108">Recovery process overview</span></span>
<span data-ttu-id="3cad7-109">Olá Solucionando problemas do processo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3cad7-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="3cad7-110">Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="3cad7-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="3cad7-111">Anexar e monte tooanother de disco rígido virtual Olá VM Linux para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="3cad7-112">Conecte-se toohello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="3cad7-113">Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="3cad7-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="3cad7-114">Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="3cad7-115">Crie uma VM usando Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="3cad7-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="3cad7-116">tooperform essas etapas de solução de problemas mais recente precisar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3cad7-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3cad7-117">Em Olá exemplos a seguir, substitua os nomes de parâmetro com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="3cad7-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="3cad7-118">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="3cad7-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="3cad7-119">Determinar problemas de inicialização</span><span class="sxs-lookup"><span data-stu-id="3cad7-119">Determine boot issues</span></span>
<span data-ttu-id="3cad7-120">Examine Olá saída serial toodetermine por que a VM não é capaz de tooboot corretamente.</span><span class="sxs-lookup"><span data-stu-id="3cad7-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="3cad7-121">Um exemplo comum é uma entrada inválida na `/etc/fstab`, ou Olá subjacente do disco rígido virtual que está sendo excluído ou movido.</span><span class="sxs-lookup"><span data-stu-id="3cad7-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="3cad7-122">Obter logs de inicialização Olá [az vm diagnóstico de inicialização get-inicialização-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="3cad7-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="3cad7-123">Olá exemplo a seguir obtém Olá serial saída de hello VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="3cad7-124">Examine Olá saída serial toodetermine por hello VM está falhando tooboot.</span><span class="sxs-lookup"><span data-stu-id="3cad7-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="3cad7-125">Se a saída serial Olá não fornece nenhuma indicação, talvez seja necessário tooreview arquivos de log em `/var/log` depois que você tiver Olá virtual disco rígido conectado tooa VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="3cad7-126">Exibir detalhes do disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="3cad7-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="3cad7-127">Antes de você pode anexar o disco rígido virtual (VHD) de tooanother VM, é necessário tooidentify Olá URI do disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="3cad7-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="3cad7-128">Exiba informações sobre a VM com [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="3cad7-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="3cad7-129">Saudação de uso `--query` disco toohello SO do sinalizador tooextract Olá URI.</span><span class="sxs-lookup"><span data-stu-id="3cad7-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="3cad7-130">Olá, exemplo a seguir obtém informações de disco para Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="3cad7-131">Olá URI é muito semelhante**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="3cad7-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="3cad7-132">Excluir VM existente</span><span class="sxs-lookup"><span data-stu-id="3cad7-132">Delete existing VM</span></span>
<span data-ttu-id="3cad7-133">Discos rígidos virtuais e VMs são dois recursos distintos no Azure.</span><span class="sxs-lookup"><span data-stu-id="3cad7-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="3cad7-134">Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações.</span><span class="sxs-lookup"><span data-stu-id="3cad7-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="3cad7-135">Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="3cad7-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="3cad7-136">Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="3cad7-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="3cad7-137">Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída.</span><span class="sxs-lookup"><span data-stu-id="3cad7-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="3cad7-138">concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.</span><span class="sxs-lookup"><span data-stu-id="3cad7-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="3cad7-139">Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="3cad7-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="3cad7-140">Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3cad7-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="3cad7-141">Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cad7-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="3cad7-142">Excluir Olá VM com [az vm excluir](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="3cad7-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="3cad7-143">Olá exclusões de exemplo a seguir Olá VM denominada `myVM` saudação do grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="3cad7-144">Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="3cad7-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="3cad7-145">concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.</span><span class="sxs-lookup"><span data-stu-id="3cad7-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="3cad7-146">Anexar tooanother de disco rígido virtual existente VM</span><span class="sxs-lookup"><span data-stu-id="3cad7-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="3cad7-147">Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="3cad7-148">Anexar Olá toothis do disco rígido virtual existente VM toobrowse de solução de problemas e editar o conteúdo do disco hello.</span><span class="sxs-lookup"><span data-stu-id="3cad7-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="3cad7-149">Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="3cad7-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="3cad7-150">Escolha ou crie outro toouse VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="3cad7-151">Anexar Olá disco rígido virtual existente com [az vm não gerenciado disco anexar](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="3cad7-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="3cad7-152">Quando você anexa Olá existente do disco rígido virtual, especifique o disco de toohello URI de saudação obtido na saudação anterior `az vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="3cad7-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="3cad7-153">Olá, exemplo a seguir anexa um toohello de disco rígido virtual existente Solucionando problemas de VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="3cad7-154">Montar o disco de dados anexado Olá</span><span class="sxs-lookup"><span data-stu-id="3cad7-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="3cad7-155">Olá exemplos a seguir detalham etapas Olá necessárias em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3cad7-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="3cad7-156">Se você estiver usando uma distribuição diferente do Linux, como Red Hat Enterprise Linux ou SUSE, Olá locais de arquivo de log e `mount` comandos podem ser um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="3cad7-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="3cad7-157">Consulte a documentação de toohello para sua distribuição específica para as alterações apropriadas Olá em comandos.</span><span class="sxs-lookup"><span data-stu-id="3cad7-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="3cad7-158">SSH tooyour VM usando as credenciais apropriadas Olá de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="3cad7-159">Se o disco estiver Olá primeiro dados disco anexado tooyour Solucionando problemas de VM, disco Olá provavelmente está conectado muito`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="3cad7-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="3cad7-160">Use `dmseg` tooview anexou discos:</span><span class="sxs-lookup"><span data-stu-id="3cad7-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="3cad7-161">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cad7-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="3cad7-162">Nos Olá anterior de exemplo, disco Olá SO está em `/dev/sda` e Olá disco temporário fornecido para cada máquina virtual está em `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="3cad7-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="3cad7-163">Se você tiver vários discos de dados, eles deverão estar em `/dev/sdd`, `/dev/sde` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="3cad7-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="3cad7-164">Crie um diretório toomount seu disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="3cad7-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="3cad7-165">Olá, exemplo a seguir cria um diretório chamado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="3cad7-166">Se você tiver várias partições no disco rígido virtual existente, monte partição Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="3cad7-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="3cad7-167">exemplo a seguir Hello monta primeira partição primária Olá em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="3cad7-168">Prática recomendada é toomount os discos de dados em máquinas virtuais no Azure usando Olá identificador universalmente exclusivo (UUID) de disco rígido virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="3cad7-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="3cad7-169">Para este cenário de solução de problemas curto, montagem Olá disco rígido virtual usando Olá UUID não é necessário.</span><span class="sxs-lookup"><span data-stu-id="3cad7-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="3cad7-170">No entanto, em uso normal, edição `/etc/fstab` toomount os discos rígidos virtuais usando o nome do dispositivo, em vez de UUID pode causar Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="3cad7-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="3cad7-171">Corrigir problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="3cad7-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="3cad7-172">Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="3cad7-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="3cad7-173">Depois que você resolveu problemas hello, continue com hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3cad7-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="3cad7-174">Desmontar e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="3cad7-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="3cad7-175">Depois que os erros são resolvidos, você desmontar e desanexar Olá existente do disco rígido virtual da VM sua solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="3cad7-176">Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.</span><span class="sxs-lookup"><span data-stu-id="3cad7-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="3cad7-177">De saudação SSH tooyour de sessão VM de solução de problemas, desmonte Olá existente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="3cad7-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="3cad7-178">Altere primeiro fora do diretório do pai Olá para o seu ponto de montagem:</span><span class="sxs-lookup"><span data-stu-id="3cad7-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="3cad7-179">Agora, desmonte-Olá existente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="3cad7-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="3cad7-180">exemplo a seguir Hello desmonta dispositivo Olá no `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="3cad7-181">Agora Desanexe o disco rígido virtual de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="3cad7-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="3cad7-182">Sair Olá SSH sessão tooyour VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="3cad7-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="3cad7-183">Olá lista anexado tooyour de discos de dados, solucionando problemas de VM com [lista de disco não gerenciado de vm az](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="3cad7-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="3cad7-184">Olá, exemplo a seguir lista Olá discos de dados anexado toohello VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="3cad7-185">Observe o nome de saudação para o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="3cad7-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="3cad7-186">Por exemplo, o nome de saudação de um disco com hello URI do **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** é **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="3cad7-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="3cad7-187">Desanexar o disco de dados de saudação da sua VM [az vm não gerenciado disco desanexar](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="3cad7-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="3cad7-188">Olá, exemplo a seguir desanexa disco Olá denominado `myVHD` de saudação VM denominada `myVMRecovery` em Olá `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="3cad7-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="3cad7-189">Criar a VM com base no disco rígido original</span><span class="sxs-lookup"><span data-stu-id="3cad7-189">Create VM from original hard disk</span></span>
<span data-ttu-id="3cad7-190">toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="3cad7-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="3cad7-191">modelo JSON real Hello está no hello link a seguir:</span><span class="sxs-lookup"><span data-stu-id="3cad7-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="3cad7-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="3cad7-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="3cad7-193">modelo Hello implanta uma VM usando Olá URI do VHD de saudação do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="3cad7-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="3cad7-194">Implantar o modelo de saudação com [criar implantação de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="3cad7-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="3cad7-195">Fornecer Olá URI tooyour VHD original e especifique o tipo de Olá sistema operacional, o tamanho da VM e o nome VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3cad7-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="3cad7-196">Habilitar o diagnóstico de inicialização novamente</span><span class="sxs-lookup"><span data-stu-id="3cad7-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="3cad7-197">Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3cad7-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="3cad7-198">Habilite o diagnóstico de inicialização com [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="3cad7-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="3cad7-199">Olá exemplo a seguir habilita a extensão de diagnóstico Olá no hello VM denominada `myDeployedVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="3cad7-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="3cad7-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3cad7-200">Next steps</span></span>
<span data-ttu-id="3cad7-201">Se você estiver tendo problemas para se conectar tooyour VM, consulte [solucionar problemas de SSH conexões tooan VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3cad7-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="3cad7-202">Para ver problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3cad7-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
