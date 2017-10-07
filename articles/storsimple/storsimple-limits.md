---
title: limites de sistema aaaStorSimple 8000 series | Microsoft Docs
description: "Descreve os limites do sistema e os tamanhos recomendados para componentes e conexões do StorSimple série 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f21862989f23f2fa4cf02c884cc0fc85c6cc2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>O que são limites do sistema do StorSimple série 8000?
## <a name="overview"></a>Visão geral
O StorSimple fornece armazenamento escalonável e flexível para seu datacenter. No entanto, há algumas limitações que você deve ter em mente ao planejar, implantar e operar a solução StorSimple. Olá tabela a seguir descreve esses limites e fornece algumas recomendações para que você possa obter hello mais fora da sua solução StorSimple.

| Identificador de limite | Limite | Comentários |
| --- | --- | --- |
| Número máximo de credenciais de conta de armazenamento |64 | |
| Número máximo de contêineres de volume |64 | |
| Número máximo de volumes |255 | |
| Número máximo de volumes afixados localmente |32 | |
| Número máximo de agendas por modelo de largura de banda |168 |Uma agenda para cada hora, todos os dias da semana hello (7 * 24). |
| Tamanho máximo de um volume em camadas em dispositivos físicos |64 TB para 8100 e 8600 |8100 e 8600 são dispositivos físicos. |
| Tamanho máximo de um volume em camadas em dispositivos virtuais no Azure |30 TB para 8010  <br></br> 64 TB para 8020 |8010 e 8020 são dispositivos virtuais no Azure que usam armazenamento Standard e Premium, respectivamente. |
| Tamanho máximo de um volume localmente afixado em dispositivos físicos |8,5 TB para 8100 <br></br> 22,5 TB para 8600 |8100 e 8600 são dispositivos físicos. |
| Número máximo de conexões iSCSI |512 | |
| Número máximo de conexões iSCSI dos iniciadores |512 | |
| Número máximo de registros de controle de acesso por dispositivo |64 | |
| Número máximo de volumes por política de backup |20 | |
| Número máximo de backups retidos por programação (em uma política de backup) |64 | |
| Número máximo de agendas por política de backup |10 | |
| Número máximo de instantâneos de qualquer tipo que podem ser retidos por volume |256 |Esse número inclui instantâneos locais e na nuvem. |
| Número máximo de instantâneos que podem estar presentes em qualquer dispositivo |10.000 | |
| Número máximo de volumes que podem ser processados paralelamente para backup, restauração e clonagem |16 |<ul><li>Se houver mais de 16 volumes, eles serão processados sequencialmente conforme os slots de processamento ficarem disponíveis.</li><li>Novos backups de clonado ou um volume em camadas restaurado não pode ocorrer até a conclusão da operação de saudação. No entanto, para um volume local, backups são permitidos depois que o volume hello está online.</li></ul> |
| Tempo de recuperação de clonagem e restauração para volumes em camadas |Menos de 2 minutos |<ul><li>Olá volume é disponibilizado em 2 minutos da operação de restauração ou clonagem, independentemente do tamanho do volume hello.</li><li>desempenho do volume de saudação inicialmente pode ser mais lento do que o normal, pois a maioria dos dados hello e metadados ainda reside na nuvem de saudação. Como os fluxos de dados do dispositivo StorSimple do hello nuvem toohello pode aumentar o desempenho.</li><li>Olá tempo total toodownload metadados depende Olá tamanho de volume alocado. Metadados automaticamente são trazidos para o dispositivo de Olá no plano de fundo de saudação na taxa de saudação de 5 minutos por TB de dados de volume alocado. Essa taxa pode ser afetada pela nuvem de toohello de largura de banda de Internet.</li><li>Olá restauração ou operação de clonagem é concluída quando todos os metadados de saudação estão no dispositivo de saudação.</li><li>Operações de backup não podem ser executadas até que a restauração de saudação ou operação de clonagem esteja totalmente concluída. |
| Tempo de recuperação de restauração para volumes localmente fixados |Menos de 2 minutos |<ul><li>Olá volume é disponibilizado em 2 minutos da operação de restauração hello, independentemente do tamanho do volume hello.</li><li>desempenho do volume de saudação inicialmente pode ser mais lento do que o normal, pois a maioria dos dados hello e metadados ainda reside na nuvem de saudação. Como os fluxos de dados do dispositivo StorSimple do hello nuvem toohello pode aumentar o desempenho.</li><li>Olá tempo total toodownload metadados depende Olá tamanho de volume alocado. Metadados automaticamente são trazidos para o dispositivo de Olá no plano de fundo de saudação na taxa de saudação de 5 minutos por TB de dados de volume alocado. Essa taxa pode ser afetada pela nuvem de toohello de largura de banda de Internet.</li><li>Ao contrário de volumes em camadas, para volumes localmente afixados, dados de volume de saudação também seja baixados localmente no dispositivo de saudação. operação de restauração de saudação é concluída quando todos os dados de volume Olá foi colocado toohello dispositivo.</li><li>operações de restauração Olá podem ser longos. restauração de Olá Olá tempo total toocomplete vai depender de tamanho de saudação de volume local Olá provisionado, largura de banda de Internet e os dados existentes no dispositivo Olá Olá. Operações de backup no volume localmente afixada de saudação são permitidas enquanto a operação de restauração hello está em andamento. |
| Taxa de processamento de instantâneos de nuvem |15 minutos/TB |<ul><li>Tempo mínimo toomake Olá instantâneo em nuvem pronto para carregamento, por TB de dados de volume alocado no backup. </li><li> Hora do instantâneo de nuvem total é calculada adicionando o tempo de carregamento esse tempo toohello instantâneo, que é afetado por Olá toocloud de largura de banda de Internet. |
| Produção de leitura/gravação do cliente máxima (quando servido pela camada SSD de saudação) * |920/720 MB/s com uma única interface de rede de 10 GbE |Backup too2x com MPIO e duas interfaces de rede. |
| Produção de leitura/gravação do cliente máximo (quando servido pela camada HDD Olá) * |120/250 MB/s | |
| Produção de leitura/gravação do cliente máxima (quando servido pela camada de nuvem Olá) * e posterior para atualização 3 * * |40/60 MB/s para volumes em camadas<br><br>60/80 MB/s para volumes em camadas com a opção de arquivamento selecionada durante a criação do volume |A taxa de transferência de leitura depende dos clientes que geram e mantêm profundidade suficiente de fila de E/S. <br><br>Velocidade obtida depende da velocidade de Olá Olá subjacente da conta de armazenamento usada. |

&#42; A taxa de transferência máxima por tipo de E/S foi medida com cenários 100% de gravação e 100% de leitura. A taxa de transferência real pode ser menor e depende da combinação de E/S e das condições da rede.

&#42; &#42; Desempenho de números anterior tooUpdate 3 pode ser menor.

## <a name="next-steps"></a>Próximas etapas
Saudação de revisão [requisitos do sistema StorSimple](storsimple-system-requirements.md). 

