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
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Solucionar problemas de uma VM do Windows, anexando recuperação tooa de disco Olá SO VM usando o PowerShell do Azure
Se sua máquina virtual do Windows (VM) no Azure encontra um erro de inicialização ou do disco, talvez seja necessário tooperform etapas no disco rígido virtual Olá própria solução de problemas. Um exemplo comum seria uma atualização de aplicativo com falha que impede que Olá VM seja capaz de tooboot com êxito. Este artigo detalhes como toouse do Azure PowerShell tooconnect seu toofix de VM do Windows do disco rígido virtual tooanother erros, em seguida, recrie a VM original.


## <a name="recovery-process-overview"></a>Visão geral do processo de recuperação
Olá Solucionando problemas do processo é o seguinte:

1. Exclua Olá VM encontrar problemas, mantendo os discos rígidos virtuais hello.
2. Anexar e montar o disco rígido virtual de saudação tooanother VM do Windows para fins de solução de problemas.
3. Conecte-se toohello VM de solução de problemas. Editar arquivos ou execute qualquer ferramenta toofix problemas em Olá original do disco rígido virtual.
4. Desmonte e desanexar o disco rígido virtual de saudação do hello VM de solução de problemas.
5. Crie uma VM usando Olá original do disco rígido virtual.

Certifique-se de que você tenha [hello Azure PowerShell mais recente](/powershell/azure/overview) instalado e registrado na assinatura tooyour:

```powershell
Login-AzureRMAccount
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro com seus próprios valores. Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.


## <a name="determine-boot-issues"></a>Determinar problemas de inicialização
Você pode exibir uma captura de tela da VM no Azure toohelp solucionar problemas de inicialização. Esta captura de tela pode ajudar a identificar a causa da falha de uma VM tooboot. Olá exemplo a seguir obtém captura de tela de saudação do hello VM do Windows chamado `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Examine toodetermine de captura de tela de saudação por Olá VM está falhando tooboot. Anote as mensagens de erro ou os códigos de erro específicos fornecidos.


## <a name="view-existing-virtual-hard-disk-details"></a>Exibir detalhes do disco rígido virtual existente
Antes que você pode anexar o disco rígido virtual de tooanother VM, é necessário tooidentify nome de saudação do hello virtual VHD (disco rígido).

Olá, exemplo a seguir obtém informações de saudação VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Procure `Vhd URI` em Olá `StorageProfile` seção da saída Olá Olá precede o comando. Olá seguinte truncado exemplo mostra Olá `Vhd URI` final Olá Olá de bloco de código:

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


## <a name="delete-existing-vm"></a>Excluir VM existente
Discos rígidos virtuais e VMs são dois recursos distintos no Azure. Um disco rígido virtual é onde são armazenadas Olá sistema operacional, aplicativos e configurações. Olá própria máquina virtual é os metadados que definem Olá tamanho ou local e faz referência a recursos, como um disco rígido virtual ou placa de interface de rede virtual (NIC). Cada disco rígido virtual tem uma concessão atribuída quando anexado tooa VM. Embora os discos de dados podem ser anexados e desanexados mesmo enquanto Olá VM está em execução, disco de SO Olá não pode ser desanexado, a menos que Olá recursos de máquina virtual é excluída. concessão de saudação continua tooassociate disco de saudação SO com uma VM mesmo quando a VM está em um estado parado e desalocado.

Olá primeiro toorecover de etapa sua VM é toodelete Olá VM próprio recurso. Excluindo Olá VM deixa Olá os discos rígidos virtuais em sua conta de armazenamento. Após Olá que VM é excluída, você anexar Olá disco rígido virtual tooanother VM tootroubleshoot e resolver erros de saudação.

Olá exclusões de exemplo a seguir Olá VM denominada `myVM` saudação do grupo de recursos denominado `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Aguarde até que a saudação VM concluiu a exclusão antes de anexar o disco rígido virtual de saudação tooanother VM. concessão de Olá no disco rígido virtual Olá que associa a saudação VM precisa toobe liberado antes que você pode anexar tooanother de disco rígido virtual Olá VM.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Anexar tooanother de disco rígido virtual existente VM
Para Avançar Olá algumas etapas, você usar outra VM para fins de solução de problemas. Anexar Olá toothis do disco rígido virtual existente VM toobrowse de solução de problemas e editar o conteúdo do disco hello. Esse processo permite que você toocorrect quaisquer erros de configuração ou examinar aplicativos adicionais ou sistema de arquivos de log, por exemplo. Escolha ou crie outro toouse VM para fins de solução de problemas.

Quando você anexa Olá existente do disco rígido virtual, especifique o disco de toohello de URL de saudação obtido na saudação anterior `Get-AzureRmVM` comando. Olá, exemplo a seguir anexa um toohello de disco rígido virtual existente Solucionando problemas de VM denominada `myVMRecovery` no grupo de recursos de saudação chamado `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Adicionar um disco requer toospecify tamanho de saudação do disco hello. Como podemos anexar um disco existente, Olá `-DiskSizeInGB` é especificado como `$null`. Esse valor garante o disco de dados de saudação está conectado corretamente e sem Olá necessário toodetermine Olá tamanho real do disco de dados.


## <a name="mount-hello-attached-data-disk"></a>Montar o disco de dados anexado Olá

1. Tooyour RDP VM usando as credenciais apropriadas Olá de solução de problemas. exemplo a seguir Hello baixa Olá arquivo de conexão de RDP para Olá VM denominada `myVMRecovery` no grupo de recursos de saudação denominado `myResourceGroup`e baixa muito`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. disco de dados Olá é automaticamente detectado e anexado. Exiba lista de saudação volumes anexados toodetermine Olá da letra da unidade da seguinte maneira:

    ```powershell
    Get-Disk
    ```

    saudação de saída de exemplo a seguir mostra a saudação do disco rígido virtual conectado a um disco **2**. (Você também pode usar `Get-Volume` letra da unidade tooview Olá):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Corrigir problemas no disco rígido virtual original
Com hello disco rígido virtual existente montado, agora você pode executar qualquer manutenção e etapas de solução de problemas conforme necessário. Depois que você resolveu problemas hello, continue com hello etapas a seguir.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Desmontar e desanexar o disco rígido virtual original
Depois que os erros são resolvidos, você desmontar e desanexar Olá existente do disco rígido virtual da VM sua solução de problemas. Você não pode usar o disco rígido virtual com qualquer outra VM até que a concessão Olá anexando toohello do disco rígido virtual Olá Solucionando problemas de VM é liberado.

1. De dentro de sua sessão RDP, desmonte o disco de dados Olá em sua VM de recuperação. É necessário o número do disco de saudação do hello anterior `Get-Disk` cmdlet. Em seguida, use `Set-Disk` tooset Olá em disco como offline:

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Confirmar disco Olá agora está definido como offline usando `Get-Disk` novamente. Olá saída de exemplo a seguir mostra disco Olá agora está definido como offline:

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. Saia da sessão RDP. Sua sessão do PowerShell do Azure, remova saudação do disco rígido virtual de saudação VM de solução de problemas.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Criar a VM com base no disco rígido original
toocreate uma VM do seu disco rígido virtual original, use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modelo JSON real Hello está no hello link a seguir:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

modelo Olá implanta uma VM em uma rede virtual existente, usando Olá URL do VHD de saudação do comando anterior. Olá exemplo a seguir implanta o grupo de recursos do hello modelo toohello chamado `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Saudação de resposta solicita modelo hello como nome VM, o tipo de sistema operacional e o tamanho da VM. Olá `osDiskVhdUri` é Olá mesmo usada anteriormente ao anexar Olá toohello do disco rígido virtual existente VM de solução de problemas.


## <a name="re-enable-boot-diagnostics"></a>Habilitar o diagnóstico de inicialização novamente

Quando você cria a VM de saudação existente do disco rígido virtual, o diagnóstico de inicialização pode não ser habilitado automaticamente. Olá exemplo a seguir habilita a extensão de diagnóstico Olá no hello VM denominada `myVMDeployed` no grupo de recursos de saudação chamado `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Próximas etapas
Se você estiver tendo problemas para se conectar tooyour VM, consulte [tooan de conexões RDP de solucionar problemas de VM do Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para problemas com o acesso a aplicativos executados na VM, consulte [Solucionar problemas de conectividade do aplicativo em uma VM do Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Para obter mais informações sobre como usar o Resource Manager, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
