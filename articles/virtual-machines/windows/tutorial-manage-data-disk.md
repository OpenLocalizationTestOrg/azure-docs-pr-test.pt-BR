---
title: aaaManage Azure discos com hello Azure PowerShell | Microsoft Docs
description: Tutorial - gerenciar discos do Azure com hello Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Gerenciar discos do Azure com o PowerShell

Máquinas virtuais do Azure usam o sistema operacional do discos toostore Olá VMs, aplicativos e dados. Ao criar uma VM é importante toochoose um tamanho de disco e carga de trabalho de configuração apropriado toohello esperado. Este tutorial aborda a implantação e gerenciamento de discos de VM. Você saberá mais sobre:

> [!div class="checklist"]
> * Discos de sistema operacional e discos temporários
> * Discos de dados
> * Discos Standard e Premium
> * Desempenho do disco
> * Anexar e preparar os discos de dados

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Discos padrão do Azure

Quando uma máquina virtual do Azure é criada, dois discos são automaticamente anexados toohello máquina de virtual. 

**Disco do sistema operacional** - discos do sistema operacional podem ser dimensionados para cima too1 terabyte e hosts Olá sistema operacional de máquinas virtuais.  disco Olá SO é atribuído uma letra de unidade de *c:* por padrão. configuração de disco do sistema operacional de saudação de cache de disco de saudação é otimizado para desempenho do sistema operacional. disco Olá SO **não devem** hospedar aplicativos ou dados. Para aplicativos e dados, use um disco de dados, que é detalhado posteriormente neste artigo.

**Disco temporário** -discos temporários usam uma unidade de estado sólido está localizada em Olá mesmo host do Azure como Olá VM. Os discos temporários são altamente eficazes e podem ser usados para operações como o processamento de dados temporário. No entanto, se Olá VM for movida tooa novo host, todos os dados armazenados em um disco temporário são removidos. tamanho de saudação do disco temporário Olá é determinado pelo Olá tamanho da VM. Os discos temporários são atribuídos à letra de unidade *d:* por padrão.

### <a name="temporary-disk-sizes"></a>Tamanhos do disco temporário

| Tipo | Tamanho da VM | Tamanho máximo do disco temporário (GB) |
|----|----|----|
| [Propósito geral](sizes-general.md) | Série A e D | 800 |
| [Computação otimizada](sizes-compute.md) | Série F | 800 |
| [Memória otimizada](../virtual-machines-windows-sizes-memory.md) | Série D e G | 6144 |
| [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md) | Série L | 5630 |
| [GPU](sizes-gpu.md) | Série N | 1440 |
| [Alto desempenho](sizes-hpc.md) | Séries A e H | 2000 |

## <a name="azure-data-disks"></a>Discos de dados do Azure

Os discos de dados extras podem ser adicionados para instalação de aplicativos e armazenamento de dados. Os discos de dados devem ser usados em qualquer situação onde o armazenamento de dados durável e responsivo é desejado. Cada disco de dados tem uma capacidade máxima de 1 terabyte. Olá tamanho da saudação máquina virtual determina quantos discos de dados podem ser anexado tooa VM. Para cada núcleo da VM, podem ser anexados dois discos de dados. 

### <a name="max-data-disks-per-vm"></a>Máximo de discos de dados por VM

| Tipo | Tamanho da VM | Máximo de discos de dados por VM |
|----|----|----|
| [Propósito geral](sizes-general.md) | Série A e D | 32 |
| [Computação otimizada](sizes-compute.md) | Série F | 32 |
| [Memória otimizada](../virtual-machines-windows-sizes-memory.md) | Série D e G | 64 |
| [Armazenamento otimizado](../virtual-machines-windows-sizes-storage.md) | Série L | 64 |
| [GPU](sizes-gpu.md) | Série N | 48 |
| [Alto desempenho](sizes-hpc.md) | Série A e H | 32 |

## <a name="vm-disk-types"></a>Tipos de disco da máquina virtual

O Azure fornece dois tipos de disco.

### <a name="standard-disk"></a>Disco Standard

Armazenamento padrão é apoiado por HDDs e oferece armazenamento econômico e eficaz. Os discos Standard são ideais para uma carga de trabalho econômica de desenvolvimento e teste.

### <a name="premium-disk"></a>Disco Premium

Os discos Premium são apoiados por disco de baixa latência e alto desempenho baseado em SSD. Perfeitos para VMs que executam carga de trabalho de produção. O Armazenamento Premium dá suporte às VMs das séries DS, DSv2, GS e FS. Discos Premium vêm em três tipos (P10, P20, P30), o tamanho de saudação do disco de saudação determina o tipo de disco de saudação. Selecionar um valor de saudação do tamanho de disco é arredondado até o próximo tipo de toohello. Por exemplo, se for tamanho Olá abaixo de tipo de disco de saudação de 128 GB será P10, entre 129 e 512 P20 e mais de 512 P30. 

### <a name="premium-disk-performance"></a>Desempenho do disco Premium

|Tipo de disco de armazenamento Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Tamanho do disco (arredondado) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOPS por disco | 500 | 2.300 | 5.000 |
Taxa de transferência por disco | 100 MB/s | 150 MB/s | 200 MB/s |

Enquanto Olá acima tabela identifica o IOPS máximo por disco, um nível mais alto de desempenho pode ser obtido com a distribuição de vários discos de dados. Por exemplo, dados de 64 discos podem ser anexados tooStandard_GS5 VM. Se cada um desses discos for dimensionado como um P30, será possível chegar a um máximo de 80.000 IOPS. Para obter informações detalhadas sobre o máximo de IOPS por VM, confira [Tamanhos da VM Linux](./sizes.md).

## <a name="create-and-attach-disks"></a>Criar e anexar discos

exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente. Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você. Trabalho tutorial hello, substitua VM e o grupo de recursos de saudação nomes onde for necessário.

Criar a configuração inicial com hello [AzureRmDiskConfig novo](/powershell/module/azurerm.compute/new-azurermdiskconfig). saudação de exemplo a seguir configura um disco que é 128 gigabytes de tamanho.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Criar disco de dados de saudação com hello [AzureRmDisk novo](/powershell/module/azurerm.compute/new-azurermdisk) comando.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Get hello VM que você deseja tooadd Olá Olá de toowith de disco de dados [AzureRmVM Get](/powershell/module/azurerm.compute/get-azurermvm) comando.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Adicionar Olá dados disco toohello configuração de máquina virtual com hello [AzureRmVMDataDisk adicionar](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Atualizar a máquina virtual de saudação com hello [AzureRmVM atualização](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Preparar discos de dados

Depois que um disco tenha sido anexado toohello máquina de virtual, o sistema de operacional de saudação precisa toobe configurado toouse Olá disco. Olá exemplo a seguir mostra como configurar o primeiro disco de saudação adicionado toomanually toohello VM. Esse processo também pode ser automatizado usando Olá [extensão do script personalizado](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configuração manual

Crie uma conexão de RDP com a máquina virtual de saudação. Abra o PowerShell e execute este script.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre tópicos de discos da VM como:

> [!div class="checklist"]
> * Discos de sistema operacional e discos temporários
> * Discos de dados
> * Discos Standard e Premium
> * Desempenho do disco
> * Anexar e preparar os discos de dados

Avançar toohello toolearn próximo de tutorial sobre como automatizar a configuração da VM.

> [!div class="nextstepaction"]
> [Automatizar a configuração da VM](./tutorial-automate-vm-deployment.md)
