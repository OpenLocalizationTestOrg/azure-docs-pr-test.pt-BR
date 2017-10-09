---
title: "soluções aaaStorage para VMs do Linux no Azure | Microsoft Docs"
description: "Saiba mais sobre Olá design e implementação diretrizes importantes para a implantação de soluções de armazenamento nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3c368f07-189b-4520-bbe2-f4080253bbf2
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d270c4786d7b55b18b011aa345063b6816a80876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-linux-vms"></a>Diretrizes de infraestrutura de armazenamento do Azure para VMs Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Este artigo destaca as noções básicas sobre as necessidades de armazenamento e considerações de design para atingir o desempenho de VM (máquina virtual) ideal.

## <a name="implementation-guidelines-for-storage"></a>Diretrizes de implementação de armazenamento
Decisões:

* Você vai toouse Azure gerenciados discos ou discos não gerenciados?
* Você precisa de armazenamento de toouse Standard ou Premium para sua carga de trabalho?
* Você precisa de disco distribuição toocreate discos maiores que 4TB?
* Você precisa de disco distribuição tooachieve i / o desempenho ideal para sua carga de trabalho?
* O conjunto de contas de armazenamento você precisa toohost a infra-estrutura ou carga de trabalho TI?

Tarefas:

* Examine as demandas de e/s de aplicativos de saudação você está implantando e planeja o número apropriado de saudação e o tipo de contas de armazenamento.
* Crie conjunto de saudação de contas de armazenamento usando a convenção de nomenclatura. Você pode usar o portal de CLI do Azure ou Olá Olá.

## <a name="storage"></a>Armazenamento
O Armazenamento do Azure é uma parte fundamental de implantação e gerenciamento de aplicativos e VMs (máquinas virtuais). Armazenamento do Azure fornece serviços para armazenar dados de arquivos, dados não estruturados e mensagens, e também faz parte da infraestrutura de saudação dando suporte a máquinas virtuais.

[Os discos do Azure gerenciados](../../storage/storage-managed-disks-overview.md) lida com armazenamento para você em segundo plano da saudação. Com discos não gerenciados, você cria contas de armazenamento toohold Olá discos (arquivos VHD) para as VMs do Azure. Na adição de hardware, você deve verificar se que criação de contas de armazenamento adicional para não exceder o limite de IOPS de saudação do armazenamento com qualquer um dos seus discos. Com discos gerenciados tratamento de armazenamento, você não está limitado pela Olá limites da conta de armazenamento (como 20.000 IOPS / conta). Você também não tem mais toocopy suas contas de armazenamento toomultiple imagens personalizadas (arquivos VHD). Você pode gerenciá-los em um local central – uma conta de armazenamento por região do Azure – e usá-los toocreate centenas de VMs em uma assinatura. Recomendamos o uso do Managed Disks para novas implantações.

Há dois tipos de conta de armazenamento disponíveis para dar suporte às VMs:

* Forneça contas de armazenamento padrão você acessar o armazenamento de tooblob (usado para armazenar discos de VM do Azure), armazenamento, armazenamento de fila, de tabela e armazenamento de arquivos.
* [Armazenamento Premium](../../storage/storage-premium-storage.md) dão suporte a discos de alto desempenho e baixa latência para cargas de trabalho de E/S intensiva, como cluster fragmentado do MongoDB. Um armazenamento premium dá suporte no momento somente a discos de VM do Azure.

O Azure cria VMs com um disco do sistema operacional, um disco temporário e zero ou mais discos de dados opcionais. disco do sistema operacional Hello e discos de dados são blobs de página do Azure, enquanto o disco temporário Olá é armazenado localmente no nó Olá onde reside a máquina de saudação. Tome cuidado ao criar aplicativos tooonly usar esse disco temporário para dados não são persistentes como Olá VM pode ser migrada entre hosts durante um evento de manutenção. Todos os dados armazenados em disco temporário Olá seriam perdidos.

Alta disponibilidade e durabilidade é fornecido pelo Olá subjacente tooensure de ambiente de armazenamento do Azure que seus dados permaneçam protegidos contra falhas de hardware ou de manutenção não planejadas. Ao projetar seu ambiente de armazenamento do Azure, você pode escolher tooreplicate armazenamento de máquina virtual:

* localmente em um datacenter do Azure fornecido
* entre os datacenters do Azure dentro de uma determinada região
* entre os datacenters do Azure em regiões diferentes.

Você pode ler [mais sobre opções de replicação Olá para alta disponibilidade](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

Discos do sistema operacional e discos de dados possuem um tamanho máximo de 4TB. Você pode usar o Gerenciador de Volume lógico (LVM) toosurpass esse limite pelo pool de discos toopresent lógico volumes de dados maiores do que 1.023 GB tooyour VM juntos.

Há alguns limites de escalabilidade ao projetar suas implantações do Armazenamento do Azure. Para obter mais informações, consulte [Assinatura do Microsoft Azure e limite de serviços, cotas e restrições](../../azure-subscription-service-limits.md#storage-limits). Consulte também [Metas de desempenho e escalabilidade do armazenamento do Azure](../../storage/storage-scalability-targets.md).

Para armazenamento de aplicativos, é possível armazenar dados de objeto não estruturados, como documentos, imagens, backups, dados de configuração, logs etc. usando o armazenamento de blobs. Em vez de seu aplicativo gravar tooa toohello de disco virtual anexado VMs, aplicativo hello pode gravar diretamente a tooAzure armazenamento de blob. Armazenamento de blob também oferece a opção de saudação do [hot e interessantes camadas de armazenamento](../../storage/storage-blob-storage-tiers.md) dependendo de suas necessidades de disponibilidade e restrições de custo.

## <a name="striped-disks"></a>Discos distribuídos
Além de permitir que você toocreate discos maior do que 1.023 GB, em muitos casos, usar a distribuição para discos de dados melhora o desempenho, permitindo que vários blobs tooback armazenamento de saudação para um único volume. Com a distribuição, hello e/s necessária toowrite e dados de leitura de um único disco lógico continua em paralelo.

O Azure impõe limites no número de saudação de discos de dados e a quantidade de largura de banda disponível, dependendo do tamanho da VM hello. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md)

Se você estiver usando a distribuição de disco para discos de dados do Azure, considere Olá diretrizes a seguir:

* Anexe discos de dados máximo de saudação permitidos para Olá tamanho da VM.
* Use o LVM.
* Evite usar opções de cache de disco de dados do Azure (política de cache = Nenhuma).

Para obter mais informações, veja [Configuração de LVM em uma VM do Linux](configure-lvm.md).

## <a name="multiple-storage-accounts"></a>Várias contas de armazenamento
Esta seção não se aplica muito[discos gerenciado do Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), pois você não criar contas de armazenamento separada. 

Ao criar seu ambiente de armazenamento do Azure para discos não gerenciados, você pode usar várias contas de armazenamento como número de saudação de VMs implantar aumenta. Essa abordagem ajuda a distribuir o hello e/s em Olá subjacente armazenamento do Azure infraestrutura toomaintain um desempenho ideal para suas máquinas virtuais e aplicativos. Como projetar aplicativos Olá que você está implantando, considere os requisitos de e/s de saudação que cada VM tem e balancear essas VMs entre contas de armazenamento do Azure. Tente tooavoid agrupamento Olá alta e/s mais exigentes VMs em toojust uma ou duas contas de armazenamento.

Para obter mais informações sobre os recursos de e/s de saudação das diferentes opções de armazenamento do Azure hello e alguns recomendam máximos, consulte [destinos de escalabilidade e desempenho do armazenamento do Azure](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

