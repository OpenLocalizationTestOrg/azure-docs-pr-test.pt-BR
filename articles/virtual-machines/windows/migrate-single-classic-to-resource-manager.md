---
title: "aaaMigrate tooan uma VM clássico VM do ARM gerenciados disco | Microsoft Docs"
description: "Migrar uma VM do Azure de implantação clássico Olá tooManaged discos no modelo de implantação do Gerenciador de recursos de saudação do modelo."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Migrar manualmente um VM clássico tooa nova ARM gerenciados disco VM da saudação VHD 


Esta seção ajuda você toomigrate suas VMs do Azure existente do modelo de implantação clássico Olá muito[discos gerenciados](managed-disks-overview.md) no modelo de implantação do Gerenciador de recursos de saudação.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planejar a migração de saudação do tooManaged discos

Esta seção Ajuda toomake Olá melhor decisão sobre tipos de VM e disco.


### <a name="location"></a>Local

Escolha um local onde o Azure Managed Disks estão disponíveis. Se você estiver migrando tooPremium gerenciados discos, também Verifique se o armazenamento Premium está disponível na região Olá onde você está planejando toomigrate para. Confira [Serviços do Azure por região](https://azure.microsoft.com/regions/#services) para obter informações atualizadas sobre as localizações disponíveis.

### <a name="vm-sizes"></a>Tamanhos de VM

Se você estiver migrando tooPremium gerenciados discos, você tem tooupdate tamanho de saudação do hello VM tooPremium tamanho com capacidade de armazenamento disponível na região Olá onde a VM está localizada. Examine os tamanhos de VM Olá que são compatíveis com um armazenamento Premium. especificações de tamanho de VM do Azure Olá são listadas na [tamanhos das máquinas virtuais](sizes.md).
Examine as características de desempenho de saudação de máquinas virtuais que funcionam com o armazenamento Premium e escolha o tamanho VM mais apropriado hello mais adequada para sua carga de trabalho. Certifique-se de que há largura de banda suficiente disponível no seu tráfego de disco VM toodrive hello.

### <a name="disk-sizes"></a>Tamanhos do disco

**Managed Disks Premium**

Há sete tipos de discos Gerenciados premium que podem ser usados com sua VM e cada um tem IOPs e limites de taxa de transferência específicos. Considere esses limites ao escolher Olá tipo de disco Premium para sua VM com base nas necessidades de saudação do seu aplicativo em termos de capacidade, escalabilidade e desempenho e cargas de pico.

| Tipo de discos premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Tamanho do disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS por disco       | 120   | 240   | 500   | 2.300              | 5.000              | 7500              | 7500              | 
| Taxa de transferência por disco | 25 MB por segundo  | 50 MB por segundo  | 100 MB por segundo | 150 MB por segundo | 200 MB por segundo | 250 MB por segundo | 250 MB por segundo | 

**Managed Disks Standard**

Há sete tipos de discos Gerenciados Padrão que podem ser usados com sua VM. Cada um deles tem uma capacidade diferente, mas com os mesmos limites de taxa de transferência e IOPS. Escolha o tipo de saudação de discos gerenciados padrão com base nas necessidades de capacidade de saudação do seu aplicativo.

| Tipo de disco Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Tamanho do disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| IOPS por disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Taxa de transferência por disco | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 60 MB por segundo | 


### <a name="disk-caching-policy"></a>Política de cache de disco 

**Managed Disks Premium**

Por padrão, a política de cache de disco é *somente leitura* para todos os discos de dados Premium, de hello e *leitura-gravação* para o disco do sistema operacional Premium Olá anexado toohello VM. Esta configuração é recomendável tooachieve Olá o desempenho ideal para IOs seu aplicativo. Para discos de dados de gravação intensa ou somente gravação (como arquivos de log do SQL Server), desabilite o cache de disco para que possa obter o melhor desempenho do aplicativo.

### <a name="pricing"></a>Preços

Saudação de revisão [preços para discos gerenciados](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Preços de discos gerenciados do Premium são igual a saudação discos de Premium não gerenciado. No entanto, os preços do Standard Managed Disks são diferentes dos preços do Standard Unmanaged Disks.


## <a name="checklist"></a>Lista de verificação

1.  Se você estiver migrando tooPremium gerenciados discos, verifique se que ele está disponível na região Olá que você estiver migrando para o.

2.  Decida Olá nova VM série que usará. Se você estiver migrando tooPremium gerenciados discos, ele deve ser uma capacidade de armazenamento Premium.

3.  Decida Olá VM tamanho exato você usará que estão disponíveis na região Olá que você estiver migrando para o. Tamanho da VM precisa toobe toosupport grande o suficiente Olá quantos discos de dados que você tem. Por exemplo, se você tiver quatro discos de dados, Olá VM deve ter dois ou mais núcleos. Considere também as necessidades de capacidade de processamento, memória e largura de banda de rede.

4.  Ter Olá detalhes atuais de VM úteis, inclusive Olá lista de discos e blobs VHD correspondentes.

Prepare seu aplicativo para o tempo de inatividade. toodo uma migração limpa, você tem toostop todo o processamento Olá Olá atual sistema. Somente então você poderá obtê-lo estado tooconsistent que você pode migrar toohello nova plataforma. Duração de tempo de inatividade depende da quantidade de saudação de dados em Olá discos toomigrate.


## <a name="migrate-hello-vm"></a>Migrar Olá VM

Prepare seu aplicativo para o tempo de inatividade. toodo uma migração limpa, você tem toostop todo o processamento Olá Olá atual sistema. Somente então você poderá obtê-lo estado tooconsistent que você pode migrar toohello nova plataforma. Duração do tempo de inatividade depende da quantidade de saudação de dados em Olá discos toomigrate.


1.  Primeiro, defina os parâmetros comuns de saudação:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Criar um disco do sistema operacional gerenciado usando Olá VHD do hello VM clássico.

    Certifique-se de que você tenha fornecido Olá completar URI de saudação parâmetro toohello $osVhdUri de VHD do sistema operacional. Além disso, insira **-AccountType** como **PremiumLRS** ou **StandardLRS** com base no tipo dos discos (Premium ou Standard) que você está migrando.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Anexar Olá OS disco toohello nova VM.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Criar um disco de dados gerenciado Olá VHD do arquivo de dados e adicioná-lo toohello nova VM.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Criar hello nova VM, definindo o IP público, rede Virtual e NIC.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Pode haver toosupport necessárias etapas adicionais seu aplicativo não será coberto por este guia.
>
>

## <a name="next-steps"></a>Próximas etapas

- Conecte-se a máquina virtual de toohello. Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

