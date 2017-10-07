---
title: aaaAbout discos e VHDs para VMs do Linux do Microsoft Azure | Microsoft Docs
description: "Saiba mais sobre Olá Noções básicas sobre discos e VHDs para máquinas virtuais Linux no Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 862217e4f15ff8fd2e08de71386c4f367d0c39db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Sobre discos e VHDs para VMs com Linux do Azure
Assim como qualquer outro computador, máquinas virtuais no Azure usam discos como toostore um local de um sistema operacional, aplicativos e dados. Todas as máquinas virtuais do Azure têm pelo menos dois discos - um disco do sistema operacional Linux e um disco temporário. disco do sistema operacional Olá é criado a partir de uma imagem e disco do sistema operacional hello e imagem Olá são realmente discos rígidos virtuais (VHDs) armazenados em uma conta de armazenamento do Azure. Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs. 

Neste artigo, nós falar sobre os diferentes usos Olá discos hello e, em seguida, aborde tipos diferentes de saudação de discos, você pode criar e usar. Este artigo também está disponível para [máquinas virtuais do Windows](../windows/about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Discos usados por VMs

Vamos dar uma olhada em como discos de saudação são usados pelo Olá VMs.

## <a name="operating-system-disk"></a>Disco do sistema operacional
Cada máquina virtual tem um disco de sistema operacional anexado. Ele é registrado como uma unidade SATA e rotulado como /dev/sda por padrão. Este disco tem uma capacidade máxima de 2048 gigabytes (GB). 

## <a name="temporary-disk"></a>Disco temporário
Cada VM contém um disco temporário. disco temporário Olá fornece armazenamento de curto prazo para aplicativos e processos e dados de repositório tooonly desejado, como arquivos de paginação ou de permuta. Dados em disco temporário Olá podem ser perdidos durante uma [evento de manutenção](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou quando você [reimplantar uma VM](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Durante uma reinicialização padrão do hello VM, devem persistir os dados de saudação na unidade temporária hello.

Em máquinas virtuais Linux, o disco Olá normalmente é **/desenvolvimento/sdb** e é formatado e montado muito**/mnt** por Olá agente Linux do Azure. tamanho de saudação do disco temporário Olá varia de acordo com base no tamanho de saudação da máquina virtual de saudação. Para saber mais, confira [Tamanhos de máquinas virtuais do Linux](../windows/sizes.md).

Para obter mais informações sobre como o Azure usa o disco temporário hello, consulte [Noções básicas sobre unidades temporárias de saudação em máquinas virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Disco de dados
Um disco de dados é um VHD anexado tooa máquina virtual toostore aplicativo dados ou outros dados que você precisa tookeep. Discos de dados são registrados como unidades SCSI e rotulados com a letra que você escolher. Cada disco de dados tem uma capacidade máxima de 4095 GB. tamanho da máquina virtual de saudação Hello determina quantos discos de dados, você pode anexar tooit e hello tipo de armazenamento que você pode usar discos de saudação toohost.

> [!NOTE]
> Para obter mais detalhes sobre as capacidades de máquinas virtuais, consulte [Tamanhos das máquinas virtuais do Linux](../windows/sizes.md).
> 

Quando você cria uma máquina virtual por meio de uma imagem, o Azure cria um disco do sistema operacional. Se você usar uma imagem que inclui discos de dados, Azure também cria Olá discos de dados quando ele cria a máquina virtual de saudação. Caso contrário, adicione discos de dados depois de criar a máquina virtual de saudação.

Você pode adicionar dados discos tooa virtuais máquina a qualquer momento, por **anexando** Olá disco toohello VM. Você pode usar um VHD que você carregou ou copiou tooyour conta de armazenamento ou um que o Azure cria para você. Anexar um disco de dados associa arquivo VHD Olá Olá VM, colocando uma concessão em Olá VHD não pode ser excluído do armazenamento enquanto ele ainda está conectado.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Solucionar problemas
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Próximas etapas
* [Anexar um disco](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd de armazenamento adicional para sua VM.
* [Configure o RAID de software](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para redundância.
* [Capturar uma máquina virtual do Linux](./classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para implantar rapidamente VMs adicionais.

