---
title: "Sobre armazenamento de discos não gerenciado (blobs de página) e gerenciado para VMs Windows do Microsoft Azure | Microsoft Docs"
description: "Saiba mais sobre os fundamentos de armazenamento de discos não gerenciado (blobs de página) e gerenciados para máquinas virtuais do Windows no Azure."
services: virtual-machines
author: iainfoulds
manager: jeconnoc
ms.service: virtual-machines
ms.workload: storage
ms.tgt_pltfrm: windows
ms.topic: article
ms.date: 11/15/2017
ms.author: iainfou
ms.openlocfilehash: bf5c5cc0637b9a515bf567ff8933170d7fc1a8ba
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="about-disks-storage-for-azure-windows-vms"></a>Sobre armazenamento de discos para VMs do Windows do Azure
Assim como qualquer outro computador, as máquinas virtuais do Azure usam os discos como locais onde armazenar um sistema operacional, aplicativos e dados. Todas as máquinas virtuais do Azure têm pelo menos dois discos – um disco do sistema operacional Windows e um disco temporário. O disco do sistema operacional é criado por meio de uma imagem, e o disco do sistema operacional e a imagem são VHDs (discos rígidos virtuais) armazenados em uma conta de armazenamento do Azure. Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs. 

Neste artigo, vamos falar sobre os diferentes usos dos discos e discutir os diferentes tipos de discos que você pode criar e usar. Este artigo também está disponível para [máquinas virtuais Linux](../linux/about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos usados por VMs

Vamos dar uma olhada em como os discos são usados pelas máquinas virtuais.

### <a name="operating-system-disk"></a>Disco do sistema operacional
Cada máquina virtual tem um disco de sistema operacional anexado. Ele é registrado como uma unidade SATA e rotulado como a unidade C: por padrão. Este disco tem uma capacidade máxima de 2048 gigabytes (GB). 

### <a name="temporary-disk"></a>Disco temporário
Cada VM contém um disco temporário. O disco temporário fornece armazenamento de curto prazo para aplicativos e processos e destina-se apenas a armazenar dados, como arquivos de paginação ou de permuta. Os dados no disco temporário podem ser perdidos durante um [evento de manutenção](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou durante a [reimplantação de uma VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Durante a reinicialização padrão da VM, os dados na unidade temporária devem persistir.

O disco temporário é rotulado como a unidade D: por padrão e é usado para armazenar o arquivo pagefile.sys. Para remapear este disco para uma letra de unidade diferente, consulte [Alterar a letra da unidade de disco temporário do Windows](change-drive-letter.md). O tamanho do disco temporário varia com base no tamanho da máquina virtual. Para obter mais informações, consulte [Tamanhos de máquinas virtuais do Windows](sizes.md).

Para obter mais informações sobre como o Azure usa o disco temporário, consulte [Noções básicas sobre a unidade temporária nas Máquinas Virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Disco de dados
Um disco de dados é um VHD anexado a uma máquina virtual para armazenar dados de aplicativos ou outros dados que precisam ser mantidos. Discos de dados são registrados como unidades SCSI e rotulados com a letra que você escolher. Cada disco de dados tem uma capacidade máxima de 4095 GB. O tamanho da máquina virtual determina quantos discos de dados você pode anexar a ele e o tipo de armazenamento que pode usar para hospedar os discos.

> [!NOTE]
> Para obter mais informações sobre as capacidades de máquinas virtuais, veja [Tamanhos das máquinas virtuais do Windows](sizes.md).
> 

Quando você cria uma máquina virtual por meio de uma imagem, o Azure cria um disco do sistema operacional. Se você usar uma imagem que inclui discos de dados, o Azure também cria os discos de dados quando cria a máquina virtual. Caso contrário, adicione discos de dados após criar a máquina virtual.

Você pode adicionar discos de dados a uma máquina virtual a qualquer momento **anexando** o disco à máquina virtual. Você pode usar um VHD carregado ou copiado para sua conta de armazenamento ou usar um VHD vazio criado pelo Azure para você. A anexação de um disco de dados associa o arquivo VHD à VM fazendo uma “concessão” ao VHD, de forma que ele não possa ser excluído do armazenamento enquanto estiver anexado.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Uma última recomendação: use o TRIM com discos padrão não gerenciados 

Se você usar discos padrão não gerenciados (HDD), será necessário habilitar o TRIM. O TRIM descarta os blocos não usados do disco para que você seja cobrado apenas pelo armazenamento que está efetivamente sendo usado. Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los. 

Você pode executar esse comando para verificar a configuração de TRIM. Abra um prompt de comando na sua VM do Windows e digite:


```
fsutil behavior query DisableDeleteNotify
```

Se o comando retornar 0, o TRIM estará habilitado corretamente. Se ele retornar 1, execute o seguinte comando para habilitar o TRIM:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Observação: O suporte de corte começa com o Windows Server 2012 / Windows 8 e posterior, consulte [Nova API permite que aplicativos enviem "CORTE e desmapeamento" dicas para mídia de armazenamento](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a>Próximas etapas
* [Anexar um disco](attach-disk-portal.md) para adicionar mais armazenamento à sua VM.
* [Criar um instantâneo](snapshot-copy-managed-disk.md).
* [Converter em discos gerenciados](convert-unmanaged-to-managed-disks.md).


