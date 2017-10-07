---
title: "aaaUse de instantâneos incrementais para backup e recuperação de discos de VM do Azure não gerenciados | Microsoft Docs"
description: "Crie uma solução personalizada para backup e recuperação de seus discos de máquina virtual do Azure usando instantâneos incrementais."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: 3524b987-bd65-4e35-83e7-fbc2136643e5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: aungoo
ms.openlocfilehash: 6d3e6d78e953f77a1028ac35dcde1ef046dbc3bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Faça backup dos discos não gerenciados de VM do Azure com instantâneos incrementais
## <a name="overview"></a>Visão geral
Armazenamento do Azure fornece a capacidade de saudação tootake instantâneos de blobs. Instantâneos de capturem o estado de blob Olá no momento. Neste artigo, descrevemos um cenário de como você pode manter backups dos discos de máquinas virtuais usando instantâneos. Você pode usar essa metodologia quando você escolher não toouse Backup do Azure e o serviço de recuperação e desejos toocreate uma estratégia de backup personalizada para os discos de máquina virtual.

Os discos de máquinas virtuais do Azure são armazenados como blobs de página no Armazenamento do Azure. Já que estamos falando de estratégia de backup para discos de máquina virtual neste artigo, vamos fará referência toosnapshots no contexto de saudação de blobs de página. toolearn mais informações sobre instantâneos, consulte muito[criando um instantâneo de um Blob](https://msdn.microsoft.com/library/azure/hh488361.aspx).

## <a name="what-is-a-snapshot"></a>O que é um instantâneo?
Um instantâneo de blob é uma versão somente leitura de um blob capturada em um dado momento. Quando um instantâneo tiver sido criado, ele pode ser lido, copiado ou excluído, mas não modificado. Os instantâneos fornecem uma tooback de forma a um blob conforme ele aparece em um momento específico. Até REST versão 2015-04-05, você precisava instantâneos completa da saudação capacidade toocopy. Com hello REST versão 2015-07-08 e posterior, você também pode copiar instantâneos incrementais.

## <a name="full-snapshot-copy"></a>Cópia de instantâneo completo
Instantâneos podem ser copiados tooanother conta de armazenamento como backups de tookeep um blob de blob de base de saudação. Você também pode copiar um instantâneo sobre seu blob de base, que é similar à restauração Olá blob tooan versão anterior. Quando um instantâneo é copiado de um tooanother de conta de armazenamento, ele ocupará Olá mesmo espaço como blob de página de base de saudação. Portanto, copiando instantâneos inteiros de um tooanother de conta de armazenamento será lento e também irá consumir muito espaço na conta de armazenamento de destino hello.

> [!NOTE]
> Se você copiar o destino de tooanother de blob de base hello, instantâneos de saudação do blob Olá não são copiados junto com ele. Da mesma forma, se você substituir um blob de base com uma cópia, instantâneos associados Olá blob de base não são afetados e permanecem intactos sob o nome de blob de base.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Fazer backup de discos usando instantâneos
Como uma estratégia de backup para os discos de máquina virtual, você pode tirar instantâneos periódicos do blob de página ou disco hello e copiá-los usando ferramentas como de conta de armazenamento tooanother [cópia Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) operação ou [AzCopy](storage-use-azcopy.md). Você pode copiar um blob de página de destino do instantâneo tooa com um nome diferente. blob de páginas de destino resultante Olá é um blob de página gravável e não um instantâneo. Neste artigo, descreveremos os backups de tootake etapas do uso de instantâneos de discos de máquina virtual.

### <a name="restore-disks-using-snapshots"></a>Restaurar discos usando instantâneos
Quando for hora toorestore seu disco tooa anterior a versão estável capturada em um dos instantâneos de backup hello, você pode copiar um instantâneo sobre o blob de página de base de saudação. Depois que o instantâneo de saudação é promovida toohello blob de página de base, Olá instantâneo permanece, mas sua origem é substituída por uma cópia que pode ser lida e gravada. Neste artigo, descreveremos etapas toorestore uma versão anterior do disco do seu instantâneo.

### <a name="implementing-full-snapshot-copy"></a>Implementando uma cópia completa do instantâneo
Você pode implementar uma cópia completa de instantâneo, fazendo o seguinte Olá,

* Primeiro, tire um instantâneo de blob de base hello usando Olá [Blob de instantâneo](https://msdn.microsoft.com/library/azure/ee691971.aspx) operação.
* Em seguida, copie Olá instantâneo tooa destino armazenamento conta usando [cópia Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx).
* Repita este processo toomaintain cópias de backup o blob de base.

## <a name="incremental-snapshot-copy"></a>Cópia de instantâneo incremental
novo recurso de saudação do [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) API fornece uma tooback de maneira muito melhor do backup de instantâneos de saudação do blobs de página ou discos. Olá API retorna a lista de saudação de alterações entre o blob de base hello e instantâneos de saudação. Isso reduz a quantidade de saudação do espaço de armazenamento usado na conta de backup hello. Olá API dá suporte a blobs de página no armazenamento Premium, bem como o armazenamento padrão. Com essa API, você pode criar soluções de backup mais rápidas e eficientes para VMs do Azure. Isso será disponível Olá REST versão 08 / 07 / 2015 e superior.

A cópia do instantâneo incremental permite que você toocopy de um armazenamento conta tooanother Olá diferença entre,

* o blob de base e seu instantâneo OU
* Todos os dois instantâneos de blob de base Olá

Olá fornecido seguintes condições forem atendidas,

* blob de saudação foi criada em 1 de janeiro de 2016 ou posterior.
* blob de saudação não foi substituído com [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) ou [cópia Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) entre dois instantâneos.

**Observação**: este recurso está disponível para os Blobs de Página do Azure Premium e Standard.

Quando você tem uma estratégia de backup personalizada que usa os instantâneos, copiando instantâneos de saudação de um tooanother de conta de armazenamento pode ser muito lento e consome muito espaço de armazenamento. Em vez de copiar a conta de armazenamento de backup em tooa Olá todo o instantâneo, você pode escrever diferença Olá entre blob de página backup tooa instantâneos consecutivos. Dessa forma, Olá tempo toocopy e espaço toostore backups é reduzido significativamente.

### <a name="implementing-incremental-snapshot-copy"></a>Implementando a Cópia de instantâneo incremental
Você pode implementar a cópia do instantâneo incremental, fazendo o seguinte Olá,

* Tirar um instantâneo do uso de blob de base Olá [Blob de instantâneo](https://msdn.microsoft.com/library/azure/ee691971.aspx).
* Cópia Olá instantâneo toohello destino de armazenamento de backup conta usando [cópia Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx). Esse será o blob de página backup hello. Tire um instantâneo do blob de páginas backup e armazene na conta de backup.
* Tire outro instantâneo do blob de base hello usando o Blob de instantâneo.
* Obter a diferença de saudação entre o primeiro e segundo instantâneos de blob de base usando [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx). Usar o novo parâmetro de saudação **prevsnapshot** toospecify Olá Olá instantâneo de diferença de saudação tooget com valor DateTime. Quando esse parâmetro estiver presente, Olá resposta REST incluirá apenas as páginas de saudação que foram alteradas entre o instantâneo de destino e o instantâneo anterior, incluindo páginas claras.
* Use [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) tooapply blob de página de backup de toohello essas alterações.
* Finalmente, tire um instantâneo de blob de página backup hello e armazená-la na conta de armazenamento de backup hello.

Na próxima seção, Olá, descreveremos mais detalhadamente como você pode manter backups de discos usando a cópia do instantâneo Incremental

## <a name="scenario"></a>Cenário
Nesta seção, descreveremos um cenário que envolve uma estratégia de backup personalizada para discos de máquina virtual usando instantâneos.

Considere uma VM do Azure da série DS com um disco P30 de armazenamento premium anexado. disco Olá P30 chamado *mypremiumdisk* é armazenado em uma conta de armazenamento premium denominada *mypremiumaccount*. Uma conta de armazenamento padrão chamado *mybackupstdaccount* será usado para armazenar o backup de saudação do *mypremiumdisk*. Gostaríamos tookeep um instantâneo de *mypremiumdisk* cada 12 horas.

toolearn sobre a criação de conta de armazenamento e discos, consulte muito[contas de armazenamento do Azure sobre](storage-create-storage-account.md).

toolearn sobre como fazer backup de máquinas virtuais do Azure, consulte muito[backups de VM do Azure planejar](../backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Backups de toomaintain de etapas de um disco usando instantâneos incrementais
Olá etapas descritas abaixo irá tirar instantâneos de *mypremiumdisk* e manter backups de saudação em *mybackupstdaccount*. Olá backup será um blob de página padrão chamado *mybackupstdpageblob*. Olá blob de página de backup sempre refletirá Olá mesmo estado como último instantâneo de saudação do *mypremiumdisk*.

1. Primeiro, crie o blob de página backup Olá para o disco de armazenamento premium. toodo, tirar um instantâneo da *mypremiumdisk* chamado *mypremiumdisk_ss1*.
2. Copie esse Instantâneo toomybackupstdaccount como um blob de página chamado *mybackupstdpageblob*.
3. Faça um instantâneo de *mybackupstdpageblob* chamado *mybackupstdpageblob_ss1* usando [Blob de Instantâneo](https://msdn.microsoft.com/library/azure/ee691971.aspx) e armazene-o em *mybackupstdaccount*.
4. Durante a janela de backup Olá, crie outro instantâneo do *mypremiumdisk*, digamos que *mypremiumdisk_ss2*e armazená-la na *mypremiumaccount*.
5. Obter alterações incrementais de saudação entre os instantâneos de saudação dois *mypremiumdisk_ss2* e *mypremiumdisk_ss1*usando [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) em  *mypremiumdisk_ss2* com **prevsnapshot** parâmetro definido de carimbo de hora toohello *mypremiumdisk_ss1*. Gravação de blob de página de backup de toohello essas alterações incrementais *mybackupstdpageblob* na *mybackupstdaccount*. Se houver intervalos excluídos em alterações incrementais hello, deve ser limpo de blob de página backup hello. Use [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) blob de página de backup de toohello toowrite alterações incrementais.
6. Tirar um instantâneo de blob de página backup Olá *mybackupstdpageblob*, chamado *mybackupstdpageblob_ss2*. Excluir o instantâneo anterior Olá *mypremiumdisk_ss1* da conta de armazenamento premium.
7. Repita as etapas 4 a 6 em cada janela de backup. Dessa forma, você pode manter backups de *mypremiumdisk* em uma conta de armazenamento padrão.

![Fazer backup de disco usando instantâneos incrementais](./media/storage-incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Etapas toorestore um disco de instantâneos
Olá etapas descritas abaixo irá restaurar disco premium, *mypremiumdisk* tooan instantâneo anterior da conta de armazenamento de backup Olá *mybackupstdaccount*.

1. Identifica Olá ponto no tempo que você deseja que o disco de premium Olá toorestore para. Digamos que é snapshot *mybackupstdpageblob_ss2*, que é armazenado na conta de armazenamento de backup Olá *mybackupstdaccount*.
2. Em mybackupstdaccount, promover o instantâneo Olá *mybackupstdpageblob_ss2* como novo blob de página de base backup Olá *mybackupstdpageblobrestored*.
3. Faça um instantâneo do blob de páginas de backup denominado *mybackupstdpageblobrestored_ss1*.
4. Cópia de blob de página de Olá restaurado *mybackupstdpageblobrestored* de *mybackupstdaccount* muito*mypremiumaccount* como o novo disco de premium Olá  *mypremiumdiskrestored*.
5. Tirar um instantâneo do *mypremiumdiskrestored*, chamado *mypremiumdiskrestored_ss1* para fazer backups incrementais futuros.
6. Ponto de série Olá DS toohello restaurado o disco de VM *mypremiumdiskrestored* e desanexar Olá antigo *mypremiumdisk* de saudação VM.
7. Iniciar processo de Backup Olá descrito na seção anterior para disco Olá restaurado *mypremiumdiskrestored*, usando Olá *mybackupstdpageblobrestored* como blob de página backup hello.

![Restaurar disco por meio de instantâneos](./media/storage-incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como criar instantâneos de um blob e planejar sua infraestrutura de backup de VM usando Olá links abaixo.

* [Criando um instantâneo de um Blob](https://msdn.microsoft.com/library/azure/hh488361.aspx)
* [Planejar sua Infraestrutura de backup de VM](../backup/backup-azure-vms-introduction.md)

