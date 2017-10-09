---
title: "aaaUse uma VM com o Azure PowerShell de solução de problemas do Windows | Microsoft Docs"
description: "Saiba como tootroubleshoot VM do Windows problemas no Azure por meio da conexão recuperação tooa de disco Olá SO VM usando o PowerShell do Azure"
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
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="99bd3-103">Solucionar problemas de uma VM do Windows, anexando recuperação tooa de disco Olá SO VM usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="99bd3-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="99bd3-104">Se sua máquina virtual do Windows (VM) no Azure encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="99bd3-105">Um exemplo comum seria uma atualização de aplicativo com falha que impede que Olá VM seja capaz de tooboot com êxito.</span><span class="sxs-lookup"><span data-stu-id="99bd3-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="99bd3-106">Este artigo detalhes como toouse do Azure PowerShell tooconnect seu toofix de VM do Windows do disco rígido virtual tooanother erros, em seguida, recrie a VM original.</span><span class="sxs-lookup"><span data-stu-id="99bd3-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="99bd3-107">Visão geral do processo de recuperação</span><span class="sxs-lookup"><span data-stu-id="99bd3-107">Recovery process overview</span></span>
<span data-ttu-id="99bd3-108">Olá Solucionando problemas do processo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="99bd3-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="99bd3-109">Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="99bd3-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="99bd3-110">Anexar e montar o disco rígido virtual de saudação tooanother VM do Windows para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="99bd3-111">Conecte-se toohello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="99bd3-112">Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="99bd3-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="99bd3-113">Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="99bd3-114">Crie uma VM usando Olá original do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="99bd3-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="99bd3-115">Certifique-se de que você tenha [hello Azure PowerShell mais recente](/powershell/azure/overview) instalado e registrado na assinatura tooyour:</span><span class="sxs-lookup"><span data-stu-id="99bd3-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="99bd3-116">Em Olá exemplos a seguir, substitua os nomes de parâmetro com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="99bd3-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="99bd3-117">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="99bd3-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="99bd3-118">Determinar problemas de inicialização</span><span class="sxs-lookup"><span data-stu-id="99bd3-118">Determine boot issues</span></span>
<span data-ttu-id="99bd3-119">Você pode exibir uma captura de tela da VM no Azure toohelp solucionar problemas de inicialização.</span><span class="sxs-lookup"><span data-stu-id="99bd3-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="99bd3-120">Esta captura de tela pode ajudar a identificar a causa da falha de uma VM tooboot.</span><span class="sxs-lookup"><span data-stu-id="99bd3-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="99bd3-121">Olá exemplo a seguir obtém captura de tela de saudação do hello VM do Windows chamado `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="99bd3-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="99bd3-122">Examine toodetermine de captura de tela de saudação por Olá VM está falhando tooboot.</span><span class="sxs-lookup"><span data-stu-id="99bd3-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="99bd3-123">Anote as mensagens de erro ou os códigos de erro específicos fornecidos.</span><span class="sxs-lookup"><span data-stu-id="99bd3-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="99bd3-124">Exibir detalhes do disco rígido virtual existente</span><span class="sxs-lookup"><span data-stu-id="99bd3-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="99bd3-125">Antes que você pode anexar o disco rígido virtual de tooanother VM, é necessário tooidentify nome de saudação do hello virtual VHD (disco rígido).</span><span class="sxs-lookup"><span data-stu-id="99bd3-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="99bd3-126">Olá, exemplo a seguir obtém informações de saudação VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="99bd3-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="99bd3-127">Procure `Vhd URI` em Olá `StorageProfile` seção da saída Olá Olá precede o comando.</span><span class="sxs-lookup"><span data-stu-id="99bd3-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="99bd3-128">Olá seguinte truncado exemplo mostra Olá `Vhd URI` final Olá Olá de bloco de código:</span><span class="sxs-lookup"><span data-stu-id="99bd3-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="99bd3-129">Excluir VM existente</span><span class="sxs-lookup"><span data-stu-id="99bd3-129">Delete existing VM</span></span>
<span data-ttu-id="99bd3-130">Discos rígidos virtuais e VMs são dois recursos distintos no Azure.</span><span class="sxs-lookup"><span data-stu-id="99bd3-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="99bd3-131">Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações.</span><span class="sxs-lookup"><span data-stu-id="99bd3-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="99bd3-132">Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="99bd3-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="99bd3-133">Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="99bd3-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="99bd3-134">Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída.</span><span class="sxs-lookup"><span data-stu-id="99bd3-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="99bd3-135">concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.</span><span class="sxs-lookup"><span data-stu-id="99bd3-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="99bd3-136">Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso.</span><span class="sxs-lookup"><span data-stu-id="99bd3-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="99bd3-137">Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="99bd3-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="99bd3-138">Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.</span><span class="sxs-lookup"><span data-stu-id="99bd3-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="99bd3-139">Olá exclusões de exemplo a seguir Olá VM denominada `myVM` saudação do grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="99bd3-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="99bd3-140">Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM.</span><span class="sxs-lookup"><span data-stu-id="99bd3-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="99bd3-141">concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.</span><span class="sxs-lookup"><span data-stu-id="99bd3-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="99bd3-142">Anexar tooanother de disco rígido virtual existente VM</span><span class="sxs-lookup"><span data-stu-id="99bd3-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="99bd3-143">Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="99bd3-144">Anexar Olá toothis do disco rígido virtual existente VM toobrowse de solução de problemas e editar o conteúdo do disco hello.</span><span class="sxs-lookup"><span data-stu-id="99bd3-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="99bd3-145">Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="99bd3-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="99bd3-146">Escolha ou crie outro toouse VM para fins de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="99bd3-147">Quando você anexa Olá existente do disco rígido virtual, especifique o disco de toohello de URL de saudação obtido na saudação anterior `Get-AzureRmVM` comando.</span><span class="sxs-lookup"><span data-stu-id="99bd3-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="99bd3-148">Olá, exemplo a seguir anexa um toohello de disco rígido virtual existente Solucionando problemas de VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="99bd3-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="99bd3-149">Adicionar um disco requer toospecify tamanho de saudação do disco hello.</span><span class="sxs-lookup"><span data-stu-id="99bd3-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="99bd3-150">Como podemos anexar um disco existente, Olá `-DiskSizeInGB` é especificado como `$null`.</span><span class="sxs-lookup"><span data-stu-id="99bd3-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="99bd3-151">Esse valor garante o disco de dados de saudação está conectado corretamente e sem Olá necessário toodetermine Olá tamanho real do disco de dados.</span><span class="sxs-lookup"><span data-stu-id="99bd3-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="99bd3-152">Montar o disco de dados anexado Olá</span><span class="sxs-lookup"><span data-stu-id="99bd3-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="99bd3-153">Tooyour RDP VM usando as credenciais apropriadas Olá de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="99bd3-154">exemplo a seguir Hello baixa Olá arquivo de conexão de RDP para Olá VM denominada `myVMRecovery` no grupo de recursos de saudação denominado `myResourceGroup`e baixa muito`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="99bd3-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="99bd3-155">disco de dados Olá é automaticamente detectado e anexado.</span><span class="sxs-lookup"><span data-stu-id="99bd3-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="99bd3-156">Exiba lista de saudação volumes anexados toodetermine Olá da letra da unidade da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="99bd3-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="99bd3-157">saudação de saída de exemplo a seguir mostra a saudação do disco rígido virtual conectado a um disco **2**.</span><span class="sxs-lookup"><span data-stu-id="99bd3-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="99bd3-158">(Você também pode usar `Get-Volume` letra da unidade tooview Olá):</span><span class="sxs-lookup"><span data-stu-id="99bd3-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="99bd3-159">Corrigir problemas no disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="99bd3-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="99bd3-160">Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="99bd3-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="99bd3-161">Depois que você resolveu problemas hello, continue com hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="99bd3-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="99bd3-162">Desmontar e desanexar o disco rígido virtual original</span><span class="sxs-lookup"><span data-stu-id="99bd3-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="99bd3-163">Depois que os erros são resolvidos, você desmontar e desanexar Olá existente do disco rígido virtual da VM sua solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="99bd3-164">Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.</span><span class="sxs-lookup"><span data-stu-id="99bd3-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="99bd3-165">De dentro de sua sessão RDP, desmonte o disco de dados Olá em sua VM de recuperação.</span><span class="sxs-lookup"><span data-stu-id="99bd3-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="99bd3-166">É necessário o número do disco de saudação do hello anterior `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="99bd3-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="99bd3-167">Em seguida, use `Set-Disk` tooset Olá em disco como offline:</span><span class="sxs-lookup"><span data-stu-id="99bd3-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="99bd3-168">Confirmar disco Olá agora está definido como offline usando `Get-Disk` novamente.</span><span class="sxs-lookup"><span data-stu-id="99bd3-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="99bd3-169">Olá saída de exemplo a seguir mostra disco Olá agora está definido como offline:</span><span class="sxs-lookup"><span data-stu-id="99bd3-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="99bd3-170">Saia da sessão RDP.</span><span class="sxs-lookup"><span data-stu-id="99bd3-170">Exit your RDP session.</span></span> <span data-ttu-id="99bd3-171">Sua sessão do PowerShell do Azure, remova saudação do disco rígido virtual de saudação VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="99bd3-172">Criar a VM com base no disco rígido original</span><span class="sxs-lookup"><span data-stu-id="99bd3-172">Create VM from original hard disk</span></span>
<span data-ttu-id="99bd3-173">toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="99bd3-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="99bd3-174">modelo JSON real Hello está no hello link a seguir:</span><span class="sxs-lookup"><span data-stu-id="99bd3-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="99bd3-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="99bd3-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="99bd3-176">modelo Olá implanta uma VM em uma rede virtual existente, usando Olá URL do VHD de saudação do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="99bd3-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="99bd3-177">Olá exemplo a seguir implanta o grupo de recursos do hello modelo toohello chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="99bd3-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="99bd3-178">Saudação de resposta solicita modelo hello como nome VM, o tipo de sistema operacional e o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="99bd3-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="99bd3-179">Olá `osDiskVhdUri` é Olá mesmo usada anteriormente ao anexar Olá toohello do disco rígido virtual existente VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="99bd3-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="99bd3-180">Habilitar o diagnóstico de inicialização novamente</span><span class="sxs-lookup"><span data-stu-id="99bd3-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="99bd3-181">Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="99bd3-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="99bd3-182">Olá exemplo a seguir habilita a extensão de diagnóstico Olá no hello VM denominada `myVMDeployed` no grupo de recursos de saudação chamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="99bd3-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="99bd3-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99bd3-183">Next steps</span></span>
<span data-ttu-id="99bd3-184">Se você estiver tendo problemas para se conectar tooyour VM, consulte [tooan de conexões RDP de solucionar problemas de VM do Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99bd3-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="99bd3-185">Para problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99bd3-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="99bd3-186">Para obter mais informações sobre como usar o Resource Manager, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99bd3-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
