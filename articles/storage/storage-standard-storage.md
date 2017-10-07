---
title: "com base em aaaHD padrão armazenamento econômico e discos de VM do Azure | Microsoft Docs"
description: "Discuta o Armazenamento Standard econômico e discos de VM gerenciados e não gerenciados."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Armazenamento Standard econômico e discos de VM do Azure gerenciados e não gerenciados

O Armazenamento Standard do Azure oferece suporte de disco confiável e de baixo custo para VMs que executam cargas de trabalho insensíveis a latência. Ele também oferece suporte a tabelas, blobs, filas e arquivos. Com o armazenamento padrão, os dados de saudação são armazenados em unidades de disco rígido (HDDs). Ao trabalhar com VMs, você pode usar discos de armazenamento padrão para cenários de desenvolvimento/teste e cargas de trabalho menos críticas e discos de armazenamento premium para aplicativos de produção de missão crítica. O Armazenamento Standard está disponível em todas as regiões do Azure por Standard. 

Este artigo concentra-se no uso de saudação de armazenamento padrão para discos de VM. Para obter mais informações sobre o uso de saudação do armazenamento com tabelas, blobs, filas e arquivos, consulte toohello [tooStorage Introdução](storage-introduction.md).

## <a name="disk-types"></a>Tipos de disco

Há duas maneiras de discos de padrão de toocreate para máquinas virtuais do Azure:

**Não gerenciado discos**: Este é método original hello onde você gerencia Olá contas usadas toostore Olá VHD arquivos de armazenamento que correspondem a toohello discos de VM. Os arquivos VHD são armazenados como blobs de páginas nas contas de armazenamento. Os discos não gerenciados podem ser anexado tooany tamanho da VM do Azure, incluindo as VMs de saudação que usem armazenamento Premium, principalmente como Olá série DSv2 e série GS. Suporte de VMs do Azure anexar vários discos padrão, permitindo que até too256 TB de armazenamento por VM.

[**Os discos do Azure gerenciados**](storage-managed-disks-overview.md): esse recurso gerencia contas de armazenamento Olá usadas para discos de VM Olá para você. Especificar o tipo de saudação (Premium ou padrão) e o tamanho do disco é necessário e Azure cria e gerencia disco Olá para você. Você não tem tooworry sobre onde colocar os discos de saudação entre várias contas de armazenamento em ordem tooensure que permanecer dentro dos limites de escalabilidade Olá Olá para contas de armazenamento - Azure lida com isso para você.

Mesmo que os dois tipos de discos disponíveis, é recomendável usar vantagem de tootake discos gerenciados de seus muitos recursos.

tooget iniciado com o armazenamento padrão do Azure, visite [comece gratuitamente](https://azure.microsoft.com/pricing/free-trial/). 

Para obter informações sobre como toocreate uma VM com discos gerenciados, consulte uma saudação seguintes artigos.

* [Criar uma VM do Windows usando o Gerenciador de Recursos e o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)
* [Criar uma VM do Linux usando Olá 2.0 do CLI do Azure](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>Recursos do Armazenamento Standard 

Vamos dar uma olhada em alguns dos recursos de saudação do armazenamento padrão. Para obter mais detalhes, consulte [tooAzure Introdução armazenamento](storage-introduction.md).

**Armazenamento Standard**: o Armazenamento Standard do Azure dá suporte a Discos, Blobs, Armazenamento de Arquivos, Tabelas e Filas do Azure. Serviços de armazenamento padrão de toouse, inicie com [criar uma conta de armazenamento do Azure](storage-create-storage-account.md#create-a-storage-account).

**Discos de armazenamento padrão:** armazenamento padrão, os discos podem ser anexado VMs do Azure tooall incluindo as VMs da série de tamanho usadas com o armazenamento Premium, como a série de série DSv2 e GS hello. Um disco de armazenamento padrão só pode ser anexado tooone VM. No entanto, você pode anexar um ou mais desses tooa discos VM, o toohello de contagem de disco máximo definido para esse tamanho VM. Olá seção a seguir sobre escalabilidade de armazenamento padrão e metas de desempenho, descreveremos especificações hello mais detalhadamente. 

**Blob de página padrão**: blobs de página padrão são usado toohold discos persistentes para VMs e também pode ser acessados diretamente por meio do REST como outros tipos de Blobs do Azure. [Blobs de páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) são uma coleção de páginas de 512 bytes otimizadas para leitura aleatória e operações de gravação. 

**Replicação de armazenamento:** na maioria das regiões, dados em uma conta de armazenamento padrão podem ser replicados geograficamente ou replicados localmente em vários data centers. tipos de saudação quatro de replicação disponível são armazenamento localmente redundante (LRS), o armazenamento com redundância de zona (ZRS), o armazenamento com redundância geográfica (GRS) e o armazenamento com redundância geográfica com acesso de leitura (RA-GRS). O Managed Disks no Armazenamento Standard atualmente suportam apenas o Armazenamento Localmente Redundante (LRS). Para saber mais, consulte [Replicação de armazenamento](storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Metas de Escalabilidade e Desempenho

Nesta seção, descreveremos Olá escalabilidade e metas de desempenho tooconsider é necessário ao usar o armazenamento padrão.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Limites de conta – não se aplica a toomanaged discos

| **Recurso** | **Limite padrão** |
|--------------|-------------------|
| TB por conta de armazenamento  | 500 TB |
| Entrada máxima<sup>1</sup> por conta de armazenamento (regiões dos EUA) | 10 Gbps se o GRS/ZRS estiver habilitado, 20 Gbps para o LRS |
| Saída máxima<sup>1</sup> por conta de armazenamento (regiões dos EUA) | 20 Gbps se o RA-GRS/GRS/ZRS estiver habilitado, 30 Gbps para o LRS |
| Entrada máxima<sup>1</sup> por conta de armazenamento (regiões da Ásia e Europa) | 5 Gbps se o GRS/ZRS estiver habilitado, 10 Gbps para o LRS |
| Saída máxima<sup>1</sup> por conta de armazenamento (regiões da Ásia e Europa) | 10 Gbps se o RA-GRS/GRS/ZRS estiver habilitado, 15 Gbps para o LRS |
| Taxa de solicitação total (presumindo um tamanho de objeto de 1KB) por conta de armazenamento | Backup too20, IOPS 000, entidades por segundo ou mensagens por segundo |

<sup>1</sup> entrada refere-se a dados tooall (solicitações) sendo enviados tooa conta de armazenamento. Saída refere-se tooall dados (respostas) sendo recebidos de uma conta de armazenamento.

Para saber mais, consulte [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md).

Se Olá precisa de seu aplicativo exceder os destinos de escalabilidade de saudação de uma única conta de armazenamento, criar várias contas de armazenamento de seu aplicativo toouse e particionar seus dados entre as contas de armazenamento. Como alternativa, você pode discos gerenciado do Azure e Azure gerenciará Olá particionamento e o posicionamento de seus dados para você.

### <a name="standard-disks-limits"></a>Limites de discos Standard

Diferentemente dos discos de Premium, as operações de entrada/saída Olá por segundo (IOPS) e taxa de transferência (largura de banda) de discos padrão não são provisionadas. Olá desempenho de discos padrão varia de acordo com hello VM tamanho toowhich Olá disco estiver anexado, não toohello tamanho de disco hello. Você pode esperar tooachieve o limite de desempenho toohello listada na tabela de saudação abaixo.

**Limites de discos Standard (gerenciados e não gerenciados)**

| **Camada de VM**            | **VM de camada básica** | **VM de camada Standard** |
|------------------------|-------------------|----------------------|
| Tamanho máximo do disco          | 4095 GB           | 4095 GB              |
| Máx. de 8 KB de IOPS por disco | Backup too300         | Backup too500            |
| Largura de banda máxima por disco | O too60 MB/s     | O too60 MB/s        |

Se a sua carga de trabalho requer suporte de disco de alto desempenho e baixa latência, considere usar o armazenamento Premium. tooknow mais benefícios do armazenamento Premium, visite [Premium de alto desempenho, armazenamento e discos de VM do Azure](storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Instantâneos e blob de cópia

toohello serviço de armazenamento do arquivo VHD Olá é um blob de página. Você pode tirar instantâneos de blobs de página e copiá-los tooanother local, como uma conta de armazenamento diferente.

### <a name="unmanaged-disks"></a>Discos não gerenciados

Você pode criar [instantâneos incrementais](storage-incremental-snapshots.md) para discos de padrão de não gerenciado em Olá mesma forma como você usa instantâneos com o armazenamento padrão. É recomendável que você crie instantâneos e, em seguida, copie esses conta de armazenamento com redundância geográfica de padrão de tooa instantâneos se o disco de origem estiver em uma conta de armazenamento com redundância local. Para saber mais, consulte [Opções de redundância do Armazenamento do Azure](storage-redundancy.md).

Se um disco estiver anexado tooa VM, determinadas operações de API não são permitidas em discos de saudação. Por exemplo, você não pode executar uma [cópia Blob](/rest/api/storageservices/Copy-Blob) operação no blob desde que o disco de saudação anexado tooa VM. Em vez disso, primeiro crie um instantâneo do blob usando Olá [Blob de instantâneo](/rest/api/storageservices/Snapshot-Blob) método API de REST e, em seguida, executar Olá [cópia Blob](/rest/api/storageservices/Copy-Blob) de saudação do hello instantâneo toocopy disco anexado. Como alternativa, você pode desanexar o disco hello e, em seguida, executar todas as operações necessárias.

toomaintain cópias com redundância geográfica de seus instantâneos, você pode copiar os instantâneos de uma conta de armazenamento padrão com redundância geográfica do armazenamento localmente redundante conta tooa usando AzCopy ou cópia de Blob. Para obter mais informações, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md) e [cópia Blob](/rest/api/storageservices/Copy-Blob).

Para obter informações detalhadas sobre como executar operações REST em blobs de páginas nas contas de armazenamento padrão, consulte [API REST de serviços de armazenamento do Azure](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Discos gerenciados

Um instantâneo de um disco gerenciado é uma cópia somente leitura de disco gerenciado hello, que é armazenado como um disco gerenciado padrão. Instantâneos incrementais atualmente não há suporte para discos gerenciados, mas terá suporte em Olá futuras.

Se um disco gerenciado é anexado tooa VM, determinadas operações de API não são permitidas em discos de saudação. Por exemplo, você não pode gerar uma SAS (assinatura) de acesso compartilhado tooperform uma operação de cópia enquanto o disco de saudação está anexado tooa VM. Em vez disso, primeiro criar um instantâneo do disco hello e, em seguida, executar a cópia de saudação do instantâneo de saudação. Como alternativa, você pode desanexar o disco hello e, em seguida, gerar uma operação de cópia do acesso compartilhado (SAS) de assinatura tooperform hello.

## <a name="pricing-and-billing"></a>Preços e cobrança

Ao usar o armazenamento padrão, hello cobrança considerações a seguir se aplicam:

* Tamanho de discos/dados não gerenciados de armazenamento Standard 
* Standard Managed Disks
* Instantâneos de Armazenamento Standard
* Transferências de dados de saída
* Transações

**Não gerenciado de tamanho do armazenamento de dados e de disco:** de discos não gerenciados e outros dados (blobs, tabelas, filas e arquivos), você é cobrado apenas para a quantidade de saudação de espaço está usando. Por exemplo, se você tiver uma VM cujo blob de página é provisionado como 127 GB, mas hello VM está realmente somente usando 10 GB de espaço, você será cobrado para 10 GB de espaço. Há suporte para o armazenamento padrão a too8191 GB e discos padrão de não gerenciados a too4095 GB. 

**Discos gerenciado:** discos gerenciado são cobrados tamanho Olá provisionado. Se o disco é provisionado como um disco de 10 GB e você estiver usando apenas 5 GB, você ainda será cobrado para tamanho de provisionar Olá de 10 GB.

**Instantâneos**: instantâneos de discos padrão são cobrados para capacidade adicional de saudação usada por instantâneos do hello. Para saber mais sobre instantâneos, consulte [Criando um instantâneo de um Blob](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Transferências de dados de saída**: as [transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) (dados saindo dos datacenters do Azure) incorrem em cobrança por uso de largura de banda.

**Transação**: o Azure cobra US $0.0036 por 100.000 transações de armazenamento padrão. Transações incluem leitura e gravação toostorage de operações.

Para obter informações detalhadas sobre os preços de armazenamento Standard, Máquinas Virtuais e Managed Disks, consulte:

* [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Preços de Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Preços do Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Suporte de serviço do Backup do Azure 

O backup das máquinas virtuais com discos não gerenciados pode ser feito usando o Backup do Azure. [Mais detalhes](../backup/backup-azure-vms-first-look-arm.md).

Você também pode usar o hello serviço Backup do Azure com discos gerenciados toocreate um trabalho de backup com backups baseados em tempo, fácil restauração de VM e políticas de retenção de backup. Você pode ler mais sobre isso em [Usando o serviço de backup do Azure para VMs com Managed Disks](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="next-steps"></a>Próximas etapas

* [Introdução tooAzure armazenamento](storage-introduction.md)

* [Criar uma conta de armazenamento](storage-create-storage-account.md)

* [Visão Geral do Managed Disks](storage-managed-disks-overview.md)

* [Criar uma VM do Windows usando o Gerenciador de Recursos e o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Criar uma VM do Linux usando Olá 2.0 do CLI do Azure](../virtual-machines/linux/quick-create-cli.md)
