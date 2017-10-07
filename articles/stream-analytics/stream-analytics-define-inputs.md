---
title: "Conexão de dados: entradas de transmissão de dados de uma transmissão de eventos | Microsoft Docs"
description: "Saiba mais sobre como configurar uma conexão de dados tooStream análise chamado 'entradas'. As entradas incluem um fluxo de dados de eventos e também dados de referência."
keywords: "fluxo de dados, conexão de dados, fluxo de eventos"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>Conexão de dados: Saiba mais sobre dados entradas de fluxo de eventos tooStream análise
Olá, trabalho de análise de fluxo de tooa de conexão de dados é um fluxo de eventos de uma fonte de dados do trabalho de Olá chamado tooas *entrada*. O Stream Analytics tem integração de primeira classe com fontes de fluxo de dados do Azure, incluindo [Hubs de Eventos do Azure](https://azure.microsoft.com/services/event-hubs/), [Hub IoT do Azure](https://azure.microsoft.com/services/iot-hub/) e [Armazenamento de Blobs do Azure](https://azure.microsoft.com/services/storage/blobs/). Esses entrada fontes podem ser de saudação mesma assinatura do Azure como o trabalho de análise, ou de uma assinatura diferente.

## <a name="data-input-types-data-stream-and-reference-data"></a>Tipos de entrada de dados: fluxo de dados e dados de referência
Como os dados são enviados a fonte de dados tooa, ela tem consumidos pelo trabalho de análise de fluxo de saudação e processados em tempo real. As entradas são divididas em dois tipos: entradas de fluxo de dados e entradas de dados de referência.

### <a name="data-stream-inputs"></a>Entradas de fluxo de dados
Um fluxo de dados é uma sequência ilimitada de eventos ao longo do tempo. Os trabalhos do Stream Analytics devem conter pelo menos uma fonte de entrada de fluxo de dados. O Armazenamento de Blobs, os Hubs de Eventos e o Hub IoT têm suporte como fontes de entrada de fluxo de dados. Hubs de eventos são usados toocollect fluxos de eventos de vários dispositivos e serviços. Esses fluxos podem incluir os feeds de atividades de mídia social, informações de mercado de ações ou dados de sensores. Hubs IoT são otimizados toocollect dados dos dispositivos conectados em cenários de Internet das coisas (IoT).  O Armazenamento de Blobs pode ser usado como uma fonte de entrada para ingerir dados em massa como uma transmissão, tais como arquivos de log.  

### <a name="reference-data"></a>Dados de referência
O Stream Analytics também dá suporte à entrada conhecida como *dados de referência*. Esses são dados auxiliares que são estáticos ou que são alterados lentamente. Ela é normalmente usada para executar correlação e pesquisas. Por exemplo, você pode associar dados no fluxo de dados de saudação entrada toodata nos dados de referência Olá, assim como você executaria um toolook de junção SQL valores estáticos. Armazenamento de BLOBs do Azure está atualmente a fonte de entrada hello só tem suportada para dados de referência. Blobs de fonte de dados de referência são limitados too100 MB de tamanho.

toolearn como toocreate entradas de dados de referência, consulte [usar dados de referência](stream-analytics-use-reference-data.md).  

## <a name="create-data-stream-input-from-event-hubs"></a>Criar entrada de fluxo de dados dos Hubs de Eventos

Os Hubs de Eventos do Azure fornecem ingestores de eventos altamente escalonável de publicação/assinatura. Um hub de eventos pode coletar milhões de eventos por segundo, para que você possa processar e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados. Juntos, os Hubs de Eventos e o Stream Analytics oferecem a você uma solução ponta a ponta para análise em tempo real – os Hubs de Eventos permitem que você alimente eventos no Azure em tempo real e os trabalhos do Stream Analytics podem processar esses eventos em tempo real. Por exemplo, você pode enviar cliques da web, as leituras do sensor ou eventos de log online tooEvent Hubs. Você pode criar trabalhos de análise de fluxo toouse Hubs de eventos como fluxos de dados de entrada hello em tempo real de filtragem, agregação e correlação.

Olá carimbo de hora padrão de eventos provenientes de Hubs de eventos de análise de fluxo é timestamp Olá que Olá evento chegou no hub de eventos hello, que é `EventEnqueuedUtcTime`. tooprocess Olá dados como um fluxo usando um carimbo de hora na carga do evento hello, você deve usar o hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) palavra-chave.

### <a name="consumer-groups"></a>Grupos de consumidores
Você deve configurar cada toohave entrada do hub de eventos de análise de fluxo em seu próprio grupo de consumidores. Quando um trabalho contém uma autojunção ou ele tem várias entradas, algumas entradas podem ser lidas por mais de um leitor de downstream. Essa situação afeta o número de saudação de leitores em um grupo único consumidor. tooavoid excedente Olá Hubs de eventos limite de cinco leitores por grupo de consumidores por partição, é um toodesignate de prática recomendada, um consumidor de grupo para cada trabalho de análise de fluxo. Também há um limite de 20 grupos de consumidores por Hub de Eventos. Para obter mais informações, confira o [Guia de programação de Hubs de Eventos](../event-hubs/event-hubs-programming-guide.md).

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>Configurar um Hub de Eventos como um fluxo de dados de entrada
Olá, tabela a seguir explica cada propriedade no hello **nova entrada** folha em Olá portal do Azure quando você configura um hub de eventos como entrada.

| Propriedade | Descrição |
| --- | --- |
| **Alias de entrada** |Um nome amigável que você usa em tooreference de consulta do trabalho Olá entrada. |
| **Namespace do barramento de serviço** |Um namespace do Barramento de Serviço do Azure, que é um contêiner para um conjunto de entidades de mensagens. Ao criar um novo Hub de Eventos, você também cria um namespace do Barramento de Serviço. |
| **Nome do Hub de Eventos** |nome de saudação do hello toouse de hub de eventos como entrada. |
| **Nome da política do Hub de Eventos** |Olá política de acesso compartilhado que fornece acesso toohello evento hub. Cada política de acesso compartilhado tem um nome, as permissões definidas por você e as chaves de acesso. |
| **Grupo de consumidores de Hub de Eventos** (opcional) |Olá consumidor toouse tooingest dados do grupo de hub de eventos de saudação. Se nenhum grupo de consumidores for especificado, o trabalho de análise de fluxo de saudação usa grupo de consumidores saudação padrão. É recomendável usar um grupo de consumidores distinto para cada trabalho do Stream Analytics. |
| **Formato de serialização do evento** |Olá formato de serialização (JSON, CSV ou Avro) de fluxo de dados de entrada hello. |
| **Codificação** | No momento, UTF-8 é o formato de codificação Olá só tem suportada. |

Quando seus dados vêm de um hub de eventos, você tem acesso toohello campos de metadados em sua consulta de análise de fluxo a seguir:

| Propriedade | Descrição |
| --- | --- |
| **EventProcessedUtcTime** |Olá data e hora que o evento Olá foi processado pela análise de fluxo. |
| **EventEnqueuedUtcTime** |Olá data e hora que o evento Olá foi recebido por Hubs de eventos. |
| **PartitionId** |Olá ID de partição com base em zero para o adaptador de entrada hello. |

Por exemplo, usando esses campos, você pode escrever uma consulta como Olá exemplo a seguir:

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>Criar entrada de fluxo de dados do Hub IoT
O Hub IoT do Azure é um ingestor de eventos altamente escalonável de publicação/assinatura e otimizado para cenários de IoT.

Olá carimbo de hora padrão de eventos provenientes de um hub IoT no Stream Analytics é timestamp Olá que Olá evento chegou no hub IoT hello, o que é `EventEnqueuedUtcTime`. tooprocess Olá dados como um fluxo usando um carimbo de hora na carga do evento hello, você deve usar o hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) palavra-chave.

> [!NOTE]
> Apenas as mensagens enviadas com uma propriedade `DeviceClient` podem ser processadas.
> 
> 

### <a name="consumer-groups"></a>Grupos de consumidores
Você deve configurar cada toohave de entrada de hub IoT de análise de fluxo em seu próprio grupo de consumidores. Quando um trabalho contém uma autojunção ou ele tem várias entradas, algumas entradas podem ser lidas por mais de um leitor de downstream. Essa situação afeta o número de saudação de leitores em um grupo único consumidor. tooavoid excedente hello Azure IoT Hub limite de cinco leitores por grupo de consumidores por partição, é um toodesignate de prática recomendada, um consumidor de grupo para cada trabalho de análise de fluxo.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>Configurar um Hub IoT como um fluxo de dados de entrada
Olá, tabela a seguir explica cada propriedade no hello **nova entrada** folha em Olá portal do Azure quando você configura um hub IoT como entrada.

| Propriedade | Descrição |
| --- | --- |
| **Alias de entrada** |Um nome amigável que você usa em tooreference de consulta do trabalho Olá entrada.|
| **Hub IoT** |nome de saudação do hello IoT hub toouse como entrada. |
| **Ponto de extremidade** |Olá ponto de extremidade para o hub IoT de saudação.|
| **Nome da política de acesso compartilhado** |política de acesso compartilhada de saudação que fornece acesso toohello IoT hub. Cada política de acesso compartilhado tem um nome, as permissões definidas por você e as chaves de acesso. |
| **Chave da política de acesso compartilhado** |chave de acesso compartilhado Olá usado hub IoT do tooauthorize acesso toohello. |
| **Grupo de Consumidores** (opcional) |Olá consumidor grupo toouse tooingest os dados de hub IoT de saudação. Se nenhum grupo de consumidores for especificado, um trabalho do Stream Analytics usa o grupo de consumidores saudação padrão. É recomendável usar um grupo de consumidores distinto para cada trabalho do Stream Analytics. |
| **Formato de serialização do evento** |Olá formato de serialização (JSON, CSV ou Avro) de fluxo de dados de entrada hello. |
| **Codificação** |No momento, UTF-8 é o formato de codificação Olá só tem suportada. |

Quando seus dados vêm de um hub IoT, você tem acesso toohello campos de metadados em sua consulta de análise de fluxo a seguir:

| Propriedade | Descrição |
| --- | --- |
| **EventProcessedUtcTime** |saudação de data e hora que o evento Olá foi processado. |
| **EventEnqueuedUtcTime** |Olá data e hora que o evento Olá foi recebido pelo hub IoT de saudação. |
| **PartitionId** |Olá ID de partição com base em zero para o adaptador de entrada hello. |
| **IoTHub.MessageId** | Uma ID que usou a comunicação bidirecional toocorrelate no hub IoT. |
| **IoTHub.CorrelationId** |Uma ID usada em respostas a mensagens e comentários no Hub IoT. |
| **IoTHub.ConnectionDeviceId** |ID de saudação de autenticação usado toosend essa mensagem. Esse valor é marcado em servicebound mensagens pelo hub IoT de saudação. |
| **IoTHub.ConnectionDeviceGenerationId** |ID de geração de saudação do hello autenticado dispositivo que era usado toosend essa mensagem. Esse valor é marcado em servicebound mensagens pelo hub IoT de saudação. |
| **IoTHub.EnqueuedTime** |tempo de saudação quando a mensagem de saudação foi recebida pelo hub IoT de saudação. |
| **IoTHub.StreamId** |Uma propriedade de evento personalizado adicionada pelo dispositivo de remetente hello. |


## <a name="create-data-stream-input-from-blob-storage"></a>Criar entrada de fluxo de dados do Armazenamento de Blobs
Para cenários com grandes quantidades de dados não estruturados toostore na nuvem hello, armazenamento de BLOBs do Azure oferece uma solução econômica e dimensionável. Dados no Armazenamento de Blobs geralmente são considerados dados em repouso. No entanto, ele pode ser processado como um fluxo de dados pelo Stream Analytics. Um cenário típico para entradas de Armazenamento de Blobs com o Stream Analytics é o processamento de log. Nesse cenário, os dados de telemetria tem sido capturados de um sistema e necessidades toobe analisada e processar dados significativos tooextract.

Olá carimbo de hora padrão de eventos do armazenamento de Blob no Stream Analytics é timestamp Olá que Olá blob foi modificado pela última vez, que é `BlobLastModifiedUtcTime`. tooprocess Olá dados como um fluxo usando um carimbo de hora na carga do evento hello, você deve usar o hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) palavra-chave.

Formato CSV entradas *exigem* um toodefine de linha de cabeçalho de campos para o conjunto de dados Olá. Além disso, todos os campos de linha de cabeçalho adicionais devem ser exclusivos.

> [!NOTE]
> Análise de fluxo não oferece suporte à adição de blob existente tooan conteúdo. Análise de fluxo exibirão um blob apenas uma vez, e as alterações que ocorrem no blob Olá após trabalho Olá leu dados saudação não são processadas. Uma prática recomendada é tooupload todos os dados de saudação uma vez e, em seguida, não adicionar o armazenamento de blob de toothat de eventos.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>Configurar o Armazenamento de Blobs como um fluxo de dados de entrada

Olá, tabela a seguir explica cada propriedade no hello **nova entrada** folha em Olá portal do Azure quando você configurar o armazenamento de Blob como entrada.

| Propriedade | Descrição |
| --- | --- |
| **Alias de entrada** | Um nome amigável que você usa em tooreference de consulta do trabalho Olá entrada. |
| **Conta de armazenamento** | nome de Olá Olá da conta de armazenamento onde os arquivos de blob Olá estão localizados. |
| **Chave de conta de armazenamento** | chave de segredo do Hello associado à conta de armazenamento hello. |
| **Contêiner** | contêiner de Olá Olá entrada de blob. Os contêineres fornecem um agrupamento lógico para os blobs armazenados no hello serviço Blob do Microsoft Azure. Quando você carregar um blob de toohello serviço de armazenamento de BLOBs do Azure, você deve especificar um contêiner de blob. |
| **Padrão do caminho** (opcional) | caminho do arquivo Hello usado blobs de saudação toolocate no contêiner especificado hello. Caminho de hello, você pode especificar uma ou mais instâncias de saudação três variáveis a seguir: `{date}`, `{time}`, ou`{partition}`<br/><br/>Exemplo 1: `cluster1/logs/{date}/{time}/{partition}`<br/><br/>Exemplo 2: `cluster1/logs/{date}`<br/><br/>Olá `*` caractere não é um valor permitido para o prefixo de caminho hello. Apenas <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">caracteres de blobs do Azure</a> válidos são permitidos. |
| **Formato de data** (opcional) | Se você usar a variável de data de saudação no caminho hello, Olá formato de data na qual Olá arquivos são organizados. Exemplo: `YYYY/MM/DD` |
| **Formato de hora** (opcional) |  Se você usar a variável de tempo de saudação no caminho hello, Olá formato de hora na qual Olá arquivos são organizados. Atualmente, o valor de saudação só tem suportada é `HH`. |
| **Formato de serialização do evento** | Olá formato de serialização (JSON, CSV ou Avro) para fluxos de dados de entrada. |
| **Codificação** | Para CSV e JSON, UTF-8 é atualmente o formato de codificação Olá só tem suportada. |

Quando os dados provêm de uma fonte de armazenamento de Blob, você tem acesso toohello campos de metadados em sua consulta de análise de fluxo a seguir:

| Propriedade | Descrição |
| --- | --- |
| **BlobName** |nome de saudação do blob de entrada hello que Olá evento veio. |
| **EventProcessedUtcTime** |Olá data e hora que o evento Olá foi processado pela análise de fluxo. |
| **BlobLastModifiedUtcTime** |saudação de data e hora que Olá última modificação no blob. |
| **PartitionId** |Olá ID de partição com base em zero para o adaptador de entrada hello. |

Por exemplo, usando esses campos, você pode escrever uma consulta como Olá exemplo a seguir:

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
Você aprendeu sobre as opções de conexão de dados no Azure para seus trabalhos do Stream Analytics. toolearn mais sobre análise de fluxo, consulte:

* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
