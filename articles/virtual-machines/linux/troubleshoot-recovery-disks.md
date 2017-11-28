---
title: "Usar uma VM de solução de problemas Linux com a CLI 2.0 do Azure | Microsoft Docs"
description: "Saiba como solucionar problemas de VM Linux conectando o disco do SO a uma VM de recuperação usando a CLI 2.0 do Azure"
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
ms.openlocfilehash: 7a28accce1bd328b2b486b588c44d91b03e42122
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-with-the-azure-cli-20"></a><span data-ttu-id="d3dae-103">Solucionar problemas de uma VM Linux anexando o disco do SO a uma VM de recuperação com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="d3dae-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="d3dae-104">Se a VM (máquina virtual) do Linux tiver um erro de disco ou de inicialização, talvez você precise realizar etapas de solução de problemas no próprio disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="d3dae-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="d3dae-105">Um exemplo comum seria uma entrada inválida em `/etc/fstab` que impede que a VM possa ser inicializada corretamente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="d3dae-106">Este artigo fornece detalhes sobre como usar a CLI 2.0 do Azure para conectar o disco rígido virtual a outra VM Linux para corrigir erros e recriar a VM original.</span><span class="sxs-lookup"><span data-stu-id="d3dae-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span> <span data-ttu-id="d3dae-107">Você também pode executar essas etapas com a [CLI do Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3dae-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="d3dae-108">Visão geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="d3dae-108">Recovery process overview</span></span>
<span data-ttu-id="d3dae-109">O processo de solução de problemas é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d3dae-109">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="d3dae-110">Exclua a VM que tem problemas, mantendo os discos rígidos virtuais.</span><span class="sxs-lookup"><span data-stu-id="d3dae-110">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="d3dae-111">Anexe e monte o disco rígido virtual em outra VM do Linux para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="d3dae-112">Conecte-se à VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-112">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="d3dae-113">Edite os arquivos ou execute as ferramentas para corrigir os problemas no disco rígido virtual original.</span><span class="sxs-lookup"><span data-stu-id="d3dae-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="d3dae-114">Desmonte e desanexe o disco rígido virtual da VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="d3dae-115">Crie uma VM usando o disco rígido virtual original.</span><span class="sxs-lookup"><span data-stu-id="d3dae-115">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="d3dae-116">Para realizar essas etapas de solução de problemas, é preciso ter a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente instalada e conectada a uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="d3dae-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="d3dae-117">Nos exemplos a seguir, substitua os nomes de parâmetro pelos seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="d3dae-117">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="d3dae-118">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="d3dae-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="d3dae-119">Determinar problemas de inicialização</span><span class="sxs-lookup"><span data-stu-id="d3dae-119">Determine boot issues</span></span>
<span data-ttu-id="d3dae-120">Examine a saída serial para determinar por que a VM não pode ser inicializada corretamente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-120">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="d3dae-121">Um exemplo comum é uma entrada inválida em `/etc/fstab` ou a exclusão ou movimentação do disco rígido virtual subjacente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="d3dae-122">Obtenha os logs de inicialização com [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="d3dae-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="d3dae-123">O exemplo a seguir obtém a saída serial da VM chamada `myVM` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="d3dae-124">Examine a saída serial para determinar por que a VM não é inicializada corretamente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-124">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="d3dae-125">Se a saída serial não fornecer nenhuma indicação, talvez seja necessário examinar os arquivos de log em `/var/log` depois de conectar o disco rígido virtual a uma VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="d3dae-126">Exibir detalhes do disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="d3dae-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="d3dae-127">Antes de anexar o VHD (disco rígido virtual) a outra VM, você precisa identificar o URI do disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d3dae-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span></span> 

<span data-ttu-id="d3dae-128">Exiba informações sobre a VM com [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="d3dae-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="d3dae-129">Use o sinalizador `--query` para extrair o URI para o disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d3dae-129">Use the `--query` flag to extract the URI to the OS disk.</span></span> <span data-ttu-id="d3dae-130">O exemplo a seguir obtém informações de disco da VM chamada `myVM` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="d3dae-131">O URI é semelhante a **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="d3dae-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="d3dae-132">Excluir VM existente</span><span class="sxs-lookup"><span data-stu-id="d3dae-132">Delete existing VM</span></span>
<span data-ttu-id="d3dae-133">Discos rígidos virtuais e VMs são dois recursos distintos no Azure.</span><span class="sxs-lookup"><span data-stu-id="d3dae-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="d3dae-134">Um disco rígido virtual é o local em que o próprio sistema operacional, os aplicativos e as configurações são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d3dae-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="d3dae-135">A VM em si são apenas os metadados que definem o tamanho ou a localização e que faz referência a recursos como um disco rígido virtual ou a NIC (placa de interface de rede) virtual.</span><span class="sxs-lookup"><span data-stu-id="d3dae-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="d3dae-136">Cada disco rígido virtual tem uma concessão atribuída quando anexado a uma VM.</span><span class="sxs-lookup"><span data-stu-id="d3dae-136">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="d3dae-137">Embora os discos de dados possam ser anexados e desanexados mesmo durante a execução da VM, o disco do sistema operacional não pode ser desanexado, a menos que o recurso de VM seja excluído.</span><span class="sxs-lookup"><span data-stu-id="d3dae-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="d3dae-138">A concessão continua associando o disco do sistema operacional a uma VM mesmo quando a VM está em um estado parado e desalocado.</span><span class="sxs-lookup"><span data-stu-id="d3dae-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="d3dae-139">A primeira etapa para recuperar a VM é excluir o recurso de VM em si.</span><span class="sxs-lookup"><span data-stu-id="d3dae-139">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="d3dae-140">A exclusão da VM deixa os discos rígidos virtuais na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d3dae-140">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="d3dae-141">Depois que a VM for excluída, você anexa o disco rígido virtual a outra VM para solucionar os erros.</span><span class="sxs-lookup"><span data-stu-id="d3dae-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="d3dae-142">Exclua a VM com [az vm delete](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="d3dae-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="d3dae-143">O seguinte exemplo exclui a VM chamada `myVM` do grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="d3dae-144">Aguarde até que a VM tenha concluído a exclusão antes de anexar o disco rígido virtual a outra VM.</span><span class="sxs-lookup"><span data-stu-id="d3dae-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="d3dae-145">A concessão no disco rígido virtual que o associa à VM precisa ser liberada antes da anexação do disco rígido virtual a outra VM.</span><span class="sxs-lookup"><span data-stu-id="d3dae-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="d3dae-146">Anexar um disco rígido virtual existente a outra VM</span><span class="sxs-lookup"><span data-stu-id="d3dae-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="d3dae-147">Para as próximas etapas, você pode usar outra VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="d3dae-148">Você anexa o disco rígido virtual existente a essa VM de solução de problemas para procurar e editar o conteúdo do disco.</span><span class="sxs-lookup"><span data-stu-id="d3dae-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="d3dae-149">Esse processo permite que você corrija os erros de configuração ou examine arquivos de aplicativo ou de log do sistema adicionais, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="d3dae-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="d3dae-150">Escolha ou crie outra VM a ser usada para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="d3dae-151">Anexe o disco rígido virtual existente com [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="d3dae-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="d3dae-152">Ao anexar o disco rígido virtual existente, especifique o URI para o disco obtido no comando `az vm show` anterior.</span><span class="sxs-lookup"><span data-stu-id="d3dae-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span></span> <span data-ttu-id="d3dae-153">O seguinte exemplo anexa um disco rígido virtual existente à VM de solução de problemas chamada `myVMRecovery` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="d3dae-154">Montar o disco de dados anexado</span><span class="sxs-lookup"><span data-stu-id="d3dae-154">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="d3dae-155">Os exemplos a seguir fornecem detalhes das etapas necessárias em uma VM do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d3dae-155">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="d3dae-156">Se você estiver usando outra distribuição Linux, como Red Hat Enterprise Linux ou SUSE, as localizações do arquivo de log e os comandos `mount` poderão ser um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="d3dae-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="d3dae-157">Consulte a documentação da distribuição específica para obter as alterações apropriadas aos comandos.</span><span class="sxs-lookup"><span data-stu-id="d3dae-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="d3dae-158">SSH para a VM de solução de problemas usando as credenciais apropriadas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-158">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="d3dae-159">Se esse disco for o primeiro disco de dados anexado à VM de solução de problemas, provavelmente ele estará conectado a `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="d3dae-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="d3dae-160">Use `dmseg` para exibir os discos anexados:</span><span class="sxs-lookup"><span data-stu-id="d3dae-160">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="d3dae-161">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="d3dae-161">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="d3dae-162">No exemplo anterior, o disco do sistema operacional está em `/dev/sda` e o disco temporário fornecido para cada VM está em `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="d3dae-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="d3dae-163">Se você tiver vários discos de dados, eles deverão estar em `/dev/sdd`, `/dev/sde` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d3dae-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="d3dae-164">Crie um diretório para montar o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-164">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="d3dae-165">O seguinte exemplo cria um diretório chamado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-165">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="d3dae-166">Se você tiver várias partições no disco rígido virtual existente, monte a partição necessária.</span><span class="sxs-lookup"><span data-stu-id="d3dae-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="d3dae-167">O seguinte exemplo monta a primeira partição primária em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-167">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="d3dae-168">A prática recomendada é montar os discos de dados em VMs no Azure usando o UUID (identificador universal exclusivo) do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="d3dae-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="d3dae-169">Para este cenário de solução de problemas breve, não é necessário montar o disco rígido virtual usando o UUID.</span><span class="sxs-lookup"><span data-stu-id="d3dae-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="d3dae-170">No entanto, no uso normal, editar `/etc/fstab` para montar os discos rígidos virtuais usando o nome do dispositivo em vez do UUID poderá causar falha de inicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="d3dae-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="d3dae-171">Corrigir problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="d3dae-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="d3dae-172">Com o disco rígido virtual existente montado, agora você pode realizar as etapas de manutenção e solução de problemas necessárias.</span><span class="sxs-lookup"><span data-stu-id="d3dae-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="d3dae-173">Depois de resolver os problemas, continue com as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-173">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="d3dae-174">Desmontar e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="d3dae-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="d3dae-175">Depois de resolver os erros, desmonte e desanexe o disco rígido virtual existente da VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="d3dae-176">Não é possível usar o disco rígido virtual com nenhuma outra VM até que a concessão que anexa o disco rígido virtual à VM de solução de problemas seja liberada.</span><span class="sxs-lookup"><span data-stu-id="d3dae-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="d3dae-177">Na sessão do SSH da VM de solução de problemas, desmonte o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="d3dae-178">Altere do diretório pai para o ponto de montagem primeiro:</span><span class="sxs-lookup"><span data-stu-id="d3dae-178">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="d3dae-179">Agora desmonte o disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-179">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="d3dae-180">O seguinte exemplo desmonta o dispositivo em `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-180">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="d3dae-181">Agora desanexe o disco rígido virtual da VM.</span><span class="sxs-lookup"><span data-stu-id="d3dae-181">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="d3dae-182">Saia da sessão do SSH da VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="d3dae-182">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="d3dae-183">Liste os discos de dados anexados à VM de solução de problemas com [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="d3dae-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="d3dae-184">O seguinte exemplo lista os discos de dados anexados à VM chamada `myVMRecovery` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="d3dae-185">Observe o nome do disco rígido virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-185">Note the name for your existing virtual hard disk.</span></span> <span data-ttu-id="d3dae-186">Por exemplo, o nome de um disco com o URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** é **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="d3dae-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="d3dae-187">Desanexe o disco de dados da sua VM com [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="d3dae-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="d3dae-188">O exemplo a seguir desanexa o disco chamado `myVHD` da VM chamada `myVMRecovery` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="d3dae-189">Criar a VM com base no disco rígido original</span><span class="sxs-lookup"><span data-stu-id="d3dae-189">Create VM from original hard disk</span></span>
<span data-ttu-id="d3dae-190">Para criar uma VM com base no disco rígido virtual original, use [esse modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="d3dae-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="d3dae-191">O modelo JSON real está no seguinte link:</span><span class="sxs-lookup"><span data-stu-id="d3dae-191">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="d3dae-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d3dae-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="d3dae-193">O modelo implanta uma VM usando o URI do VHD do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="d3dae-193">The template deploys a VM using the VHD URI from the earlier command.</span></span> <span data-ttu-id="d3dae-194">Implante o modelo com [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="d3dae-194">Deploy the template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="d3dae-195">Forneça o URI para o VHD original e, em seguida, especifique o tipo do sistema operacional, o tamanho da VM e o nome da VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d3dae-195">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="d3dae-196">Habilitar o diagnóstico de inicialização novamente</span><span class="sxs-lookup"><span data-stu-id="d3dae-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="d3dae-197">Ao criar a VM com base no disco rígido virtual existente, o diagnóstico de inicialização poderá não ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d3dae-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="d3dae-198">Habilite o diagnóstico de inicialização com [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="d3dae-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="d3dae-199">O seguinte exemplo habilita a extensão de diagnóstico na VM chamada `myDeployedVM` no grupo de recursos chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="d3dae-199">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="d3dae-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3dae-200">Next steps</span></span>
<span data-ttu-id="d3dae-201">Se você estiver tendo problemas para se conectar à VM, consulte [Solucionar problemas de conexões SSH com uma VM do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3dae-201">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d3dae-202">Para ver problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Linux](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3dae-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>