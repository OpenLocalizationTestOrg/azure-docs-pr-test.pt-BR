---
title: aaaMoving grandes quantidades de dados para/do armazenamento em nuvem no Azure | Microsoft Docs
description: "Uma visão geral dos métodos diferentes Olá para tooand movimentação de dados do armazenamento do Azure."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 7c8ec9d99cbd48042b8146130c8827f9f25c024d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Movendo dados tooand do armazenamento do Azure
Se você quiser toomove local dados tooAzure armazenamento (ou vice-versa), há uma variedade de maneiras toodo isso. abordagem de saudação que funciona melhor para você depende de seu cenário. Este artigo fornece uma visão geral rápida de diferentes cenários e ofertas apropriadas para cada um.

## <a name="building-applications"></a>Criando aplicativos
Se você estiver criando um aplicativo, o desenvolvimento em relação a saudação API REST ou uma das muitas bibliotecas de cliente é tooand de dados de toomove uma ótima maneira de armazenamento do Azure.

O Armazenamento do Azure fornece ricas bibliotecas de cliente para .NET, iOS, Java, Android, UWP (Plataforma Universal do Windows), Xamarin, C++, Node.JS, PHP, Ruby e Python. bibliotecas de cliente Olá oferecem recursos avançados, como a lógica de repetição, registro em log e carregamentos paralelos. Você também pode desenvolver diretamente em Olá API REST, que podem ser chamados por qualquer linguagem que faz solicitações HTTP/HTTPS.

Consulte [Introdução ao armazenamento de BLOBs do Azure](../blobs/storage-dotnet-how-to-use-blobs.md) toolearn mais.

Além disso, também oferecemos Olá [biblioteca de movimentação de dados de armazenamento do Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) que é uma biblioteca projetada para alto desempenho cópia dos dados tooand do Azure. Consulte tooour biblioteca de movimentação de dados [documentação](https://github.com/Azure/azure-storage-net-data-movement) toolearn mais. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Exibindo/interagindo rapidamente com seus dados
Se você quiser uma maneira fácil tooview seus dados de armazenamento do Azure enquanto também tem tooupload de capacidade de saudação e baixar seus dados, considere usar um Gerenciador de armazenamento do Azure.

Check-out de nossa lista de [gerenciadores de armazenamento do Azure](../storage-explorers.md) toolearn mais.

## <a name="system-administration"></a>Administração do Sistema
Se você exige ou mais confortável com um utilitário de linha de comando (por exemplo, os administradores do sistema), aqui estão algumas opções para você tooconsider:

### <a name="azcopy"></a>AzCopy
AzCopy é um utilitário de linha de comando do Windows desenvolvido para alto desempenho cópia dos dados tooand do armazenamento do Azure. Você também pode copiar dados em uma conta de armazenamento ou entre diferentes contas de armazenamento.

Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md) toolearn mais.

### <a name="azure-powershell"></a>Azure PowerShell
O Azure PowerShell é um módulo que fornece cmdlets para gerenciar serviços no Azure. Trata-se de uma linguagem de scripts e shell de linha de comando baseada em tarefas projetada especialmente para administração do sistema.

Consulte [usando o PowerShell do Azure com o armazenamento do Azure](storage-powershell-guide-full.md) toolearn mais.

### <a name="azure-cli"></a>CLI do Azure
A CLI do Azure fornece um conjunto de comandos entre plataformas de software livre para trabalhar com os serviços do Azure. A CLI do Azure está disponível no Windows, OSX e Linux.

Consulte [hello usando a CLI do Azure com o armazenamento do Azure](../storage-azure-cli.md) toolearn mais.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Mover grandes quantidades de dados com uma rede lenta
Um dos maiores desafios de saudação associados à movimentação de grandes quantidades de dados é o tempo de transferência de saudação. Se você quiser tooget dados de/para o armazenamento do Azure sem se preocupar com os custos de redes ou escrever código, importação/exportação do Azure é uma solução apropriada.

Consulte [importação/exportação do Azure](../storage-import-export-service.md) toolearn mais.

## <a name="backing-up-your-data"></a>Fazendo backup dos dados
Se você simplesmente precisa toobackup tooAzure seus dados armazenamento, Backup do Azure é Olá toogo de maneira. Trata-se de uma solução potente para fazer backup de dados locais e de VMs do Azure.

Consulte [Backup do Azure](../../backup/backup-introduction-to-azure-backup.md) toolearn mais.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>Acessando seus dados locais e de nuvem Olá
Se você precisar de uma solução para acessar seus dados locais e de nuvem hello, você deve considerar usar a solução de armazenamento de nuvem de híbrido do Azure, StorSimple. Essa solução consiste em um dispositivo StorSimple físico que, de maneira inteligente, armazena dados usados com frequência em SSDs, dados usados ocasionalmente em HDDs e dados inativos/de backup/de arquivamento no Armazenamento do Azure.

Consulte [StorSimple](../../storsimple/storsimple-overview.md) toolearn mais.

## <a name="recovering-your-data"></a>Recuperando dados
Quando você tem aplicativos e cargas de trabalho local, você precisará de uma solução que permita seu toocontinue de negócios em execução no evento de saudação de um desastre. O Azure Site Recovery cuida da replicação, do failover e da recuperação de máquinas virtuais e servidores físicos. Dados replicados são armazenados no armazenamento do Azure, permitindo que você tooeliminate Olá necessário para um datacenter local secundário.

Consulte [do Azure Site Recovery](../../site-recovery/site-recovery-overview.md) toolearn mais.
### <a name="moving-data-faq"></a>Perguntas frequentes sobre a movimentação de dados:
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>Posso migrar VHDs de um tooanother de região sem copiar?
Olá, somente modo toocopy VHDs entre região é dados de saudação toocopy entre contas de armazenamento em cada região. Você pode usar o AZCopy para isso. Consulte a transferência de dados com mais de toolearn o utilitário de linha de comando AzCopy hello. Para grandes quantidades de dados, também é possível Importar/Exportar do Azure. Consulte [importação/exportação do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn mais.
