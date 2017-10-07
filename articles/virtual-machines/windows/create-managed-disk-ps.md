---
title: aaaCreate um disco gerenciado em um VHD no Azure | Microsoft Docs
description: "Crie um disco gerenciado de um VHD que está atualmente em uma conta de armazenamento do Azure, usando o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Criar discos gerenciados a partir de discos não gerenciados em uma conta de armazenamento

É possível criar um disco gerenciado a partir de um disco de dados existente ou de um disco de sistema operacional que está localizado atualmente em uma conta de armazenamento do Azure. Também é possível criar um disco vazio que pode ser usado como um novo disco de dados para uma VM. 

## <a name="before-you-begin"></a>Antes de começar
Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. Executar Olá tooinstall de comando a seguir.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Criar um disco gerenciado de um VHD em uma conta de armazenamento do Azure

No exemplo hello, podemos criar um disco de um VHD como disco gerenciado e atribua-o parâmetro toohello **$Disco1** toouse mais tarde. 

Olá disco gerenciado será criado no hello **Oeste dos EUA** local, em um grupo de recursos denominado **myResourceGroup**. disco Olá será nomeado **myDisk** e ele será criado de um arquivo do VHD chamado **myDisk.vhd** é carregado anteriormente chamada de conta de armazenamento tooa **mystorageaccount**. disco gerenciado Olá será criado no armazenamento de premium localmente redundante (LRS). StandardLRS e PremiumLRS são apenas Olá **- AccountType** opções disponíveis para discos de gerenciado. 

1.  Defina alguns parâmetros

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Crie disco de dados de saudação. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Criar um disco de dados vazio como um disco gerenciado

No exemplo hello, podemos criar um disco de dados vazio como disco gerenciado e atribua-o parâmetro toohello **$dataDisk2** toouse mais tarde. Um disco de dados vazio será necessário toobe inicializado logon toohello VM e usar o diskmgmt.msc ou [remotamente usando um script e WinRM](attach-disk-ps.md#initialize-the-disk), uma vez que é anexado tooa executando VM.

disco de dados vazio do Hello será criado na Olá **Central Oeste dos EUA** local, em um grupo de recursos denominado **myResourceGroup**. disco Olá será nomeado **myEmptyDataDisk**. disco vazio Olá será criado no armazenamento de premium localmente redundante (LRS). StandardLRS e PremiumLRS são apenas Olá **- AccountType** opções disponíveis para discos de gerenciado.

tamanho do disco Olá neste exemplo é de 128GB, mas você deve escolher um tamanho que atenda às necessidades de saudação de aplicativos em execução na sua VM.

1.  Defina alguns parâmetros

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Crie disco de dados de saudação.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Próximas etapas   
- Se você já tiver uma máquina virtual, poderá [anexar um disco de dados](attach-disk-portal.md).
