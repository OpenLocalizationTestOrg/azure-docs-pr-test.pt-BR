---
title: aaaCreate uma imagem gerenciada no Azure | Microsoft Docs
description: "Crie uma imagem gerenciada de uma VM ou um VHD generalizado no Azure. Imagens pode ser usado toocreate várias VMs que usam discos gerenciados."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Criar uma imagem gerenciada de uma VM generalizada no Azure

Um recurso de imagem gerenciada pode ser criado com base em uma VM generalizada que é armazenada como um disco gerenciado ou um disco não gerenciado em uma conta de armazenamento. Olá imagem pode então ser usado toocreate várias VMs. 


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Olá VM do Windows usando Sysprep

O Sysprep remove todas as suas informações de conta pessoal, entre outras coisas e prepara Olá máquina toobe usado como uma imagem. Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).

Certifique-se de funções de servidor de saudação em execução na máquina Olá Sysprep oferece suporte. Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Se você estiver executando o Sysprep antes de carregar seu tooAzure VHD para Olá primeira vez, verifique se você tem [preparado sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep. 
> 
> 

1. Entrar toohello máquina virtual do Windows.
2. Abra a janela de Prompt de comando hello como administrador. Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.
3. Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.
4. Em **Opções de Desligamento**, selecione **Desligar**.
5. Clique em **OK**.
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Quando o Sysprep for concluído, desligar máquina virtual de saudação. Não reinicie Olá VM.


## <a name="create-a-managed-image-in-hello-portal"></a>Criar uma imagem gerenciada no portal de saudação 

1. Olá abrir [portal](https://portal.azure.com).
2. Clique em Olá toocreate de sinal de adição de um novo recurso.
3. Na pesquisa do filtro hello, digite **imagem**.
4. Selecione **imagem** dos resultados de saudação.
5. Em Olá **imagem** folha, clique em **criar**.
6. Em **nome**, digite um nome para a imagem de saudação.
7. Se você tiver mais de uma assinatura, selecione Olá um correto do hello **assinatura** lista suspensa.
7. Em **grupo de recursos** selecione **criar novo** e digite um nome ou selecione **de existente** e selecione um toouse do grupo de recursos na lista suspensa de saudação.
8. Em **local**, escolha o local de saudação do seu grupo de recursos.
9. Em **tipo de SO** Selecionar tipo de saudação do sistema operacional Windows ou Linux.
11. Em **blob de armazenamento**, clique em **procurar** toolook para Olá VHD no armazenamento do Azure.
12. Em **Tipo de conta** escolha entre Standard_LRS ou Premium_LRS. O Standard usa unidades de disco rígido e premium usa unidades de estado sólido. Ambos usam o armazenamento redundante localmente.
13. Em **cache de disco** Olá selecione a opção de cache de disco adequado. Opções de saudação são **nenhum**, **somente leitura** e **leitura \ gravação**.
14. Opcional: Você também pode adicionar uma imagem de toohello de disco de dados existente, clicando em **+ adicionar disco de dados**.  
15. Quando terminar as seleções, clique em **Criar**.
16. Após a criação de imagem hello, você verá como um **imagem** recurso na lista de saudação de recursos no grupo de recursos de saudação escolhido.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Criação de uma imagem gerenciada de uma VM usando o Powershell

Criar uma imagem diretamente de saudação que VM garante essa imagem Olá inclui todos os discos de saudação associados à saudação VM, incluindo hello disco do sistema operacional e eventuais discos de dados.


Antes de começar, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. Executar Olá tooinstall de comando a seguir.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).


1. Defina algumas variáveis.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Verifique se Olá que VM ser desalocada.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Definir status da saudação da máquina virtual de saudação muito**generalizado**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Obtenha a máquina virtual de saudação. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Crie a configuração de imagem de saudação.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Crie imagem de saudação.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Crie uma imagem gerenciada de um VHD no PowerShell

Crie uma imagem gerenciada usando o VHD do sistema operacional generalizado.


1.  Primeiro, defina os parâmetros comuns de saudação:

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Olá Step\deallocate VM.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Marca Olá VM como generalizado.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Crie imagem de saudação usando o VHD do sistema operacional generalizado.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Crie uma imagem gerenciada de um instantâneo usando o Powershell

Você também pode criar uma imagem gerenciada de um instantâneo de saudação VHD de uma VM generalizada.

    
1. Defina algumas variáveis. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Obter instantâneo de saudação.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Crie a configuração de imagem de saudação.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Crie imagem de saudação.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Próximas etapas
- Agora você pode [criar uma máquina virtual de imagem gerenciada Olá generalizado](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

