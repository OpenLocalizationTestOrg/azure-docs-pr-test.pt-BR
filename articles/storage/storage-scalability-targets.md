---
title: aaaAzure metas de desempenho e escalabilidade de armazenamento | Microsoft Docs
description: "Saiba mais sobre Olá escalabilidade e metas de desempenho para o armazenamento do Azure, incluindo a capacidade, a taxa de solicitação e a largura de banda de entrada e saída para ambas as contas de armazenamento standard e premium. Entenda as metas de desempenho para partições dentro de cada um dos serviços de armazenamento do Azure hello."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 98de116a01b64f3418808a5f626b6c70d8d432e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Metas de desempenho e escalabilidade do Armazenamento do Azure
## <a name="overview"></a>Visão geral
Este tópico descreve os tópicos de escalabilidade e desempenho Olá para armazenamento do Microsoft Azure. Para obter um resumo de outros limites do Azure, confira [Assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md).

> [!NOTE]
> Todas as contas de armazenamento executam na nova topologia de rede simples hello e oferecem suporte a destinos de escalabilidade e desempenho de saudação descritos abaixo, independentemente de quando foram criados. Para obter mais informações sobre a arquitetura de rede simples do armazenamento do Azure hello e sobre escalabilidade, consulte [armazenamento do Microsoft Azure: um altamente disponível armazenamento de serviço de nuvem com forte consistência](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> Olá escalabilidade e metas de desempenho listadas aqui são metas avançadas, mas são exequíveis. Em todos os casos, a solicitação de saudação taxa e largura de banda obtida por sua conta de armazenamento depende do tamanho de saudação de objetos armazenados, padrões de acesso Olá utilizados em Olá tipo de carga de trabalho que executa o aplicativo. Se tootest-se de que seu serviço toodetermine se seu desempenho atende às suas necessidades. Se possível, evite picos repentinos na taxa de saudação do tráfego e certifique-se de que o tráfego esteja bem distribuído nas partições.
> 
> Quando seu aplicativo atinge o limite de saudação do que uma partição pode suportar para sua carga de trabalho, o armazenamento do Azure começará tooreturn código de erro 503 (servidor ocupado) ou código de erro 500 respostas (tempo limite da operação). Quando isso ocorrer, o aplicativo hello deve usar uma política de retirada exponencial para repetições. retirada exponencial Olá permite que a carga de Olá Olá partição toodecrease e tooease os picos na partição de toothat de tráfego.
> 
> 

Se Olá precisa de seu aplicativo exceder os destinos de escalabilidade de saudação de uma única conta de armazenamento, você pode criar várias contas de armazenamento de seu aplicativo toouse e particionar seus objetos de dados entre as contas de armazenamento. Consulte [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/) para obter informações sobre preço por volume.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Metas de escalabilidade para blobs, filas, tabelas e arquivos
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Metas de escalabilidade para discos de máquina virtual
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

Veja [Tamanhos de VM do Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Tamanhos de VM do Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter detalhes adicionais.

## <a name="managed-virtual-machine-disks"></a>Discos de máquina virtual gerenciados

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Discos de máquina virtual não gerenciados
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Metas de escalabilidade para o Gerenciador de recursos do Azure
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Partições no Armazenamento do Azure
Cada objeto que contém os dados que são armazenados no armazenamento do Azure (blobs, mensagens, entidades e arquivos) pertence a partição tooa e é identificado por uma chave de partição. partição de saudação determina como o armazenamento do Azure balanceia a carga blobs, mensagens, entidades e arquivos entre necessidades de tráfego de saudação servidores toomeet desses objetos. chave de partição Olá é exclusiva e é usado toolocate um blob, mensagem ou entidade.

tabela Olá mostrada acima na [alvos de escalabilidade para contas de armazenamento padrão](#standard-storage-accounts) listas Olá metas de desempenho para uma única partição para cada serviço.

As partições afetam o balanceamento de carga e escalabilidade para cada um dos serviços de armazenamento de saudação no hello maneiras a seguir:

* **BLOBs**: chave de partição de saudação para um blob é o nome da conta, o nome do contêiner + nome do blob. Isso significa que cada blob pode ter sua própria partição se a carga no blob Olá necessárias. BLOBs podem ser distribuídos em vários servidores em ordem tooscale out toothem de acesso, mas um único blob só pode ser atendido por um único servidor. Embora os blobs possam ser agrupados logicamente em contêineres de blob, o particionamento não é afetado de forma alguma por esse agrupamento.
* **Arquivos**: chave de partição de saudação para um arquivo é o nome de compartilhamento de arquivo + de nome de conta. Isso significa que todos os arquivos em um compartilhamento de arquivos também estão em uma única partição.
* **Mensagens**: chave de partição de saudação para uma mensagem é o nome de conta Olá + nome de fila, para todas as mensagens em uma fila são agrupadas em uma única partição e são atendidas por um único servidor. Diferentes filas podem ser processadas por diferentes servidores toobalance Olá carregar para Embora muitas filas uma conta de armazenamento pode ter.
* **Entidades**: chave de partição Olá para uma entidade é o nome da conta + nome da tabela + chave da partição, onde a chave de partição de Olá é valor Olá Olá necessárias definidas pelo usuário **PartitionKey** propriedade de entidade hello. Todas as entidades com hello mesmo valor de chave de partição são agrupadas em Olá mesma partição e são atendidas por Olá mesmo servidor de partição. Este é um toounderstand ponto importante na criação de seu aplicativo. Seu aplicativo deve equilibrar os benefícios de escalabilidade de saudação de propagação de entidades por várias partições com hello vantagens de acesso de dados de agrupamento de entidades em uma única partição.  

Uma vantagem importante de toogrouping um conjunto de entidades em uma tabela em uma única partição é que é possível tooperform operações de lote atômicas nas entidades numa mesma partição, já que existe uma partição em um único servidor de saudação. Portanto, se você desejar tooperform operações em lotes em um grupo de entidades, considere agrupá-los com hello mesma chave de partição. 

Em Olá outro lado, entidades que estão em Olá mesma tabela, mas tem diferentes chaves de partição podem ser a carga balanceada entre servidores diferentes, tornando possível toohave maior escalabilidade.

Recomendações detalhadas para a criação de estratégias de particionamento de tabelas podem ser encontradas [aqui](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Consulte também
* [Detalhes de preços de armazenamento](https://azure.microsoft.com/pricing/details/storage/)
* [Assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md)
* [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](storage-premium-storage.md)
* [Replicação de armazenamento do Azure](storage-redundancy.md)
* [Lista de verificação de desempenho e escalabilidade do Armazenamento do Microsoft Azure](storage-performance-checklist.md)
* [Armazenamento do Microsoft Azure: um serviço de armazenamento em nuvem altamente disponível com coerência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

