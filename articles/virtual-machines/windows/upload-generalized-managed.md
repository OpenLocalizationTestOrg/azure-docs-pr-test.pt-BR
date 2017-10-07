---
title: aaaCreate uma VM do Azure gerenciados de um VHD local generalizado | Microsoft Docs
description: "Carregar um tooAzure VHD generalizado e usá-lo toocreate novas VMs, no modelo de implantação do Gerenciador de recursos de saudação."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Carregar um VHD generalizado e usá-lo toocreate novas VMs no Azure

Este tópico orienta você a usar PowerShell tooupload um VHD de um tooAzure VM generalizado, criar uma imagem de saudação VHD e criar uma nova VM da imagem. Você pode carregar um VHD exportado de uma ferramenta de virtualização local ou de outra nuvem. Usando [discos gerenciados](managed-disks-overview.md) para Olá nova VM simplifica o gerenciamento de VM hello e fornece maior disponibilidade quando Olá VM é colocada em um conjunto de disponibilidade. 

Se você quiser toouse um exemplo de script, consulte [tooupload script tooAzure um VHD de exemplo e criar uma nova VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Antes de começar

- Antes de carregar qualquer tooAzure VHD, você deve seguir [preparar um tooAzure de tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Revisão [planejar a migração de saudação do discos tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) antes de iniciar a migração muito[discos gerenciados](managed-disks-overview.md).
- Certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. Executar Olá tooinstall de comando a seguir.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).


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



## <a name="log-in-tooazure"></a>Faça logon no tooAzure
Se você ainda não tiver o PowerShell versão 1.4 ou superior instalado, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

1. Abra o PowerShell do Azure e entrar tooyour conta do Azure. Uma janela pop-up é aberto para você tooenter suas credenciais de conta do Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Obter IDs de assinatura Olá para suas assinaturas disponíveis.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Definir Olá assinatura correto usando a ID de assinatura de saudação. Substituir  *<subscriptionID>*  com ID Olá Olá corrigir a assinatura.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Obter a conta de armazenamento Olá
Você precisa de uma conta de armazenamento na imagem VM do Azure toostore Olá carregado. Você pode usar uma conta de armazenamento existente ou criar uma nova. 

Se usar o hello VHD toocreate um disco gerenciado para uma VM, local de conta de armazenamento Olá deve ser mesmo local Olá onde você estará criando Olá VM.

as contas de armazenamento disponível Olá tooshow, digite:

```powershell
Get-AzureRmStorageAccount
```

Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregar imagem VM Olá](#upload-the-vm-vhd-to-your-storage-account) seção.

Se você precisar toocreate uma conta de armazenamento, siga estas etapas:

1. Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada. toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate um grupo de recursos denominado **myResourceGroup** em Olá **Leste dos EUA** região, digite:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Criar uma conta de armazenamento denominada **mystorageaccount** neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    Os valores válidos para -SkuName são:
   
   * **Standard_LRS** – Armazenamento com redundância local. 
   * **Standard_ZRS** – Armazenamento com redundância de zona.
   * **Standard_GRS** – Armazenamento com redundância geográfica. 
   * **Standard_RAGRS** – Armazenamento com redundância geográfica com acesso de leitura. 
   * **Premium_LRS** – Armazenamento com redundância local Premium. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Carregar conta de armazenamento Olá VHD tooyour

Saudação de uso [AzureRmVhd adicionar](https://msdn.microsoft.com/library/mt603554.aspx) contêiner de tooa do VHD do cmdlet tooupload Olá em sua conta de armazenamento. Este exemplo hello de carregamentos de arquivo *myVHD.vhd* de *"discos de rígidos C:\Users\Public\Documents\Virtual\"*  tooa conta de armazenamento denominada *mystorageaccount*em Olá *myResourceGroup* grupo de recursos. arquivo Hello será colocado no contêiner Olá denominado *mycontainer* e o novo nome de arquivo hello serão *myUploadedVHD.vhd*.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Se for bem-sucedido, você receberá uma resposta que parece semelhante toothis:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete

Salvar Olá **URI de destino** toouse caminho mais tarde, se você vai toocreate um disco gerenciado ou uma nova VM usando Olá carregar o VHD.

### <a name="other-options-for-uploading-a-vhd"></a>Outras opções para carregar um VHD
 
 
Você também pode carregar uma conta de armazenamento de tooyour VHD usando um dos seguintes hello:

- [AzCopy](http://aka.ms/downloadazcopy)
- [API do Blob da Cópia de Armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Carregamento de Blobs do Gerenciador de Armazenamento do Azure](https://azurestorageexplorer.codeplex.com/)
- [Referência de API REST do Serviço de Importação/Exportação do Armazenamento](https://msdn.microsoft.com/library/dn529096.aspx)
-   É recomendável usar o Serviço de Importação/Exportação se o tempo de carregamento estimado é de mais de sete dias. Você pode usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tempo de saudação da unidade de tamanho e a transferência de dados. 
    Importação/exportação pode ser usado a conta de armazenamento padrão de tooa toocopy. Você precisará toocopy da conta de armazenamento toopremium de armazenamento padrão usando uma ferramenta como AzCopy.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Criar um gerenciado imagem de saudação carregar o VHD 

Crie uma imagem gerenciada usando o VHD do sistema operacional generalizado. Substitua valores hello com suas próprias informações.


1.  Primeiro, defina os parâmetros comuns de saudação:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Crie imagem de saudação usando o VHD do sistema operacional generalizado.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Criar uma rede virtual
Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).

1. Crie uma sub-rede de saudação. Este exemplo cria uma sub-rede denominada *mySubnet* com prefixo de endereço de saudação *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crie rede virtual hello. Este exemplo cria uma rede virtual denominada *myVnet* com prefixo de endereço de saudação *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Criar um endereço IP público e um adaptador de rede

comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.

1. Criar um endereço IP público. Este exemplo cria um endereço IP público chamado *myPip*. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Criar NIC hello. Este exemplo cria uma NIC chamada **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar um grupo de segurança de rede hello e uma regra RDP

toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança de rede (NSG) que permite o acesso RDP na porta 3389. 

Este exemplo cria um NSG chamado *myNsg* que contém uma regra chamada *myRdpRule* que permite tráfego RDP pela porta 3389. Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Criar uma variável para a rede virtual Olá

Crie uma variável para a rede virtual Olá concluída. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obter credenciais Olá Olá VM

Olá seguinte cmdlet abrirá uma janela onde você inserirá um novo toouse de nome e senha de usuário como conta de administrador local Olá para acessar remotamente Olá VM. 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Adicione hello nome da VM e a configuração da VM toohello tamanho.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Imagem VM do conjunto hello como imagem de origem para Olá nova VM

Definir a imagem de origem de hello usando uma ID de Olá Olá gerenciado da imagem da VM.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Definir configuração de SO hello e adicionar NIC hello.

Insira o tipo de armazenamento da saudação (PremiumLRS ou StandardLRS) e o tamanho de saudação do disco do sistema operacional hello. Este exemplo define o tipo de conta Olá muito*PremiumLRS*, Olá muito o tamanho do disco*128 GB* e cache de disco muito*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Criar hello VM

Criar hello nova VM usando a configuração de saudação armazenado em Olá **$vm** variável.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Verifique se esse Olá que VM foi criada
Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Próximas etapas

toosign em tooyour nova máquina virtual toohello procurar VM em Olá [portal](https://portal.azure.com), clique em **conectar**e abra Olá o RDP. Use credenciais de conta de saudação do seu toosign de máquina virtual original na nova máquina de virtual tooyour. Para obter mais informações, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

