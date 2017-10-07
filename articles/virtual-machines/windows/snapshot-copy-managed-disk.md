---
title: "aaaCreate uma cópia de um disco gerenciado do Azure para backup | Microsoft Docs"
description: "Saiba como toocreate uma cópia de um toouse de disco gerenciado do Azure para fazer backup ou solução de problemas de disco emite."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Criar uma cópia de um VHD armazenado como um Disco Gerenciado do Azure usando instantâneos gerenciados
Tirar um instantâneo de um disco gerenciados para backup ou criar um disco gerenciado de instantâneo hello e anexá-lo tooa tootroubleshoot de máquina virtual de teste. Um Instantâneo Gerenciado é uma cópia pontual completa de um Disco Gerenciado da VM. Ele cria uma cópia somente leitura do seu VHD e, por padrão, a armazena como um Disco Gerenciado Standard. Para saber mais sobre Managed Disks, confira [Visão geral dos Managed Disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Para saber mais sobre preços, confira [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Antes de começar
Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. Executar Olá tooinstall de comando a seguir.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Copiar Olá VHD com um instantâneo
Use Olá portal do Azure ou do PowerShell tootake um instantâneo de saudação disco gerenciado.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Use tootake portal do Azure um instantâneo 

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Iniciando na parte superior esquerda do hello, clique em **novo** e procure **instantâneo**.
3. Na folha de instantâneo hello, clique em **criar**.
4. Insira um **nome** para instantâneo de saudação.
5. Selecione uma existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nome de saudação do tipo para um novo. 
6. Selecione um Local do datacenter do Azure.  
7. Para **disco de origem**, selecione Olá toosnapshot de disco gerenciado.
8. Selecione Olá **tipo de conta** instantâneo de saudação do toouse toostore. É recomendável **Standard_LRS**, a menos que você precise dele armazenado em um disco de alto desempenho.
9. Clique em **Criar**.

### <a name="use-powershell-tootake-a-snapshot"></a>Use o PowerShell tootake um instantâneo
Hello etapas a seguir mostram como tooget Olá VHD disco toobe copiado, criar hello configurações de instantâneos e tirar um instantâneo do disco hello usando o cmdlet Olá novo AzureRmSnapshot<!--Add link toocmdlet when available-->. 

1. Defina alguns parâmetros. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Substitua os valores de parâmetro hello:
  -  "myResourceGroup" com o grupo de recursos da VM hello.
  -  "southeastasia" com a localização geográfica hello, onde você deseja que o instantâneo gerenciado armazenado. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" com o nome de saudação do disco VHD Olá que você deseja toocopy.
  -  "ContosoMD_datadisk1_snapshot1" hello nome você deseja toouse para novo instantâneo de saudação.

2. Obter toobe de disco VHD Olá copiado.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Crie hello configurações de instantâneos. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Tire instantâneo hello.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Se você planejar toouse Olá instantâneo toocreate um disco gerenciado e anexá-lo uma VM que precisa toobe alto desempenho, use o parâmetro hello `-AccountType Premium_LRS` com o comando Olá AzureRmSnapshot de novo. parâmetro Hello cria o instantâneo de saudação para que ela é armazenada como um disco de gerenciado para Premium. Os Discos Gerenciados Premium são mais caros que os Standard. Portanto, assegure-se de que os discos Premium sejam realmente necessários antes de usar esse parâmetro.


