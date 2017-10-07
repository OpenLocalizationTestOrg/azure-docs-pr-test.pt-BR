---
title: aaaAbout discos e VHDs para VMs do Windows do Microsoft Azure | Microsoft Docs
description: "Saiba mais sobre Olá Noções básicas sobre discos e máquinas virtuais de VHDs para Windows no Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Sobre discos e VHDs para VMs do Windows do Azure
Assim como qualquer outro computador, máquinas virtuais no Azure usam discos como toostore um local de um sistema operacional, aplicativos e dados. Todas as máquinas virtuais do Azure têm pelo menos dois discos – um disco do sistema operacional Windows e um disco temporário. disco do sistema operacional Olá é criado a partir de uma imagem e disco do sistema operacional hello e imagem Olá são discos rígidos virtuais (VHDs) armazenados em uma conta de armazenamento do Azure. Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs. 

Neste artigo, nós falar sobre os diferentes usos Olá discos hello e, em seguida, aborde tipos diferentes de saudação de discos, você pode criar e usar. Este artigo também está disponível para [máquinas virtuais Linux](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos usados por VMs

Vamos dar uma olhada em como discos de saudação são usados pelo Olá VMs.

### <a name="operating-system-disk"></a>Disco do sistema operacional
Cada máquina virtual tem um disco de sistema operacional anexado. Ele foi registrado como uma unidade SATA e rotulado como unidade c: de saudação por padrão. Este disco tem uma capacidade máxima de 2048 gigabytes (GB). 

### <a name="temporary-disk"></a>Disco temporário
Cada VM contém um disco temporário. disco temporário Olá fornece armazenamento de curto prazo para aplicativos e processos e dados de repositório tooonly desejado, como arquivos de paginação ou de permuta. Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando você [reimplantar uma VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Durante uma reinicialização padrão do hello VM, devem persistir os dados de saudação na unidade temporária hello.

disco temporário Olá é rotulado como Olá unidade d: por padrão e ele é usado para armazenar pagefile.sys. tooremap essa letra de unidade diferente de tooa de disco, consulte [alterar a letra da unidade saudação do disco temporário do Windows hello](../virtual-machines/windows/change-drive-letter.md). tamanho de saudação do disco temporário Olá varia de acordo com base no tamanho de saudação da máquina virtual de saudação. Para obter mais informações, consulte [Tamanhos de máquinas virtuais do Windows](../virtual-machines/windows/sizes.md).

Para obter mais informações sobre como o Azure usa o disco temporário hello, consulte [Noções básicas sobre unidades temporárias de saudação em máquinas virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Disco de dados
Um disco de dados é um VHD anexado tooa máquina virtual toostore aplicativo dados ou outros dados que você precisa tookeep. Discos de dados são registrados como unidades SCSI e rotulados com a letra que você escolher. Cada disco de dados tem uma capacidade máxima de 4095 GB. tamanho da máquina virtual de saudação Hello determina quantos discos de dados, você pode anexar tooit e hello tipo de armazenamento que você pode usar discos de saudação toohost.

> [!NOTE]
> Para obter mais informações sobre as capacidades de máquinas virtuais, veja [Tamanhos das máquinas virtuais do Windows](../virtual-machines/windows/sizes.md).
> 

Quando você cria uma máquina virtual por meio de uma imagem, o Azure cria um disco do sistema operacional. Se você usar uma imagem que inclui discos de dados, Azure também cria Olá discos de dados quando ele cria a máquina virtual de saudação. Caso contrário, adicione discos de dados depois de criar a máquina virtual de saudação.

Você pode adicionar dados discos tooa virtuais máquina a qualquer momento, por **anexando** Olá disco toohello VM. Você pode usar um VHD que você carregou ou copiou tooyour conta de armazenamento ou um que o Azure cria para você. Anexar um disco de dados associa arquivo VHD Olá Olá VM colocando uma concessão em Olá VHD não pode ser excluído do armazenamento enquanto ele ainda está conectado.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Uma última recomendação: use o TRIM com discos padrão não gerenciados 

Se você usar discos padrão não gerenciados (HDD), será necessário habilitar o TRIM. TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando. Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los. 

Você pode executar essa configuração de CORTE de saudação do comando toocheck. Abra um prompt de comando na sua VM do Windows e digite:


```
fsutil behavior query DisableDeleteNotify
```

Se o comando Olá retorna 0, TRIM está habilitada corretamente. Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Observação: O suporte de corte começa com o Windows Server 2012 / Windows 8 e posterior, consulte consulte [nova API permite que aplicativos da mídia de toostorage dicas toosend "CORTE e desmapeamento"](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Próximas etapas
* [Anexar um disco](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd de armazenamento adicional para sua VM.
* [Alterar a letra da unidade saudação do disco temporário do Windows hello](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para seu aplicativo pode usar a unidade d: de saudação para dados.

