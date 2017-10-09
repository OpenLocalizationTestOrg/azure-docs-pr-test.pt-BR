---
title: "aaaAzure telemetria de serviços de mídia | Microsoft Docs"
description: "Este artigo fornece uma visão geral da telemetria dos Serviços de Mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Telemetria dos Serviços de Mídia do Azure

Serviços de mídia do Azure (AMS) permite que dados de telemetria/métricas tooaccess para seus serviços. versão atual de saudação do AMS permite coletar dados de telemetria de ao vivo **Channel**, **StreamingEndpoint**e em tempo real **arquivamento** entidades. 

Telemetria escrita tooa tabela de armazenamento em uma conta de armazenamento do Azure que você especificar (normalmente, você poderia usar a conta de armazenamento Olá associada à sua conta AMS). 

sistema de telemetria Olá não gerenciar a retenção de dados. Você pode remover dados antigos de telemetria Olá excluindo tabelas de armazenamento de saudação.

Este tópico discute como tooconfigure e consumir telemetria Olá AMS.

## <a name="configuring-telemetry"></a>Configurar a telemetria

Você pode configurar a telemetria com granularidade no nível de componente. Há dois níveis de detalhe, "Normal" e "Detalhado". Atualmente, ambos os níveis de retornam Olá mesmas informações. É recomendável toouse "Normal. 

Olá mostrar tópicos a seguir como tooenable telemetria:

[Habilitar a telemetria com .NET](media-services-dotnet-telemetry.md) 

[Habilitar a telemetria com REST](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>Consumindo informações de telemetria

Telemetria é gravada tooan tabela de armazenamento do Azure na conta de armazenamento Olá que você especificou quando configurou a telemetria para Olá conta do Media Services. Esta seção descreve as tabelas de armazenamento Olá para métricas de saudação.

Você pode consumir dados de telemetria em uma saudação maneiras a seguir:

- Ler dados diretamente do armazenamento de tabela do Azure (por exemplo, usando Olá SDK de armazenamento). Para descrição Olá das tabelas de armazenamento de telemetria, consulte Olá **consumindo informações de telemetria** na [isso](https://msdn.microsoft.com/library/mt742089.aspx) tópico.

Ou

- Usar o suporte de Olá no SDK do Media Services .NET de saudação para ler dados de armazenamento, conforme descrito em [isso](media-services-dotnet-telemetry.md) tópico. 


esquema de telemetria Olá descrita abaixo é bom desempenho projetado toogive dentro dos limites de saudação do armazenamento de tabela do Azure:

- Os dados são particionados por conta de ID e a ID do serviço de telemetria tooallow de cada toobe serviço consultado independentemente.
- Partições contêm Olá data toogive um limite superior razoável no tamanho da partição hello.
- Chaves de linha são em tempo inversa ordem tooallow hello mais recente da telemetria itens toobe consultadas para um determinado serviço.

Isso deve permitir muitas toobe de consultas comuns da saudação eficiente:

- Download paralelo e independente de dados para serviços separados.
- Recuperação de todos os dados de um serviço específico em um intervalo de datas.
- Recuperando dados mais recentes de saudação para um serviço.

### <a name="telemetry-table-storage-output-schema"></a>Esquema de saída do armazenamento de tabelas de telemetria

Dados de telemetria são armazenados na agregação em uma tabela, "TelemetryMetrics20160321" onde "20160321" é a data da tabela Olá criado. O sistema de telemetria cria uma tabela separada para cada dia novo com base em 00:00 UTC. saudação de tabela é usada valores recorrentes toostore ingestão, como taxas de bits em uma determinada janela de tempo, bytes enviados, etc. 

Propriedade|Valor|Exemplos/notas
---|---|---
PartitionKey|{account ID}_{entity ID}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>Olá conta ID é incluída no hello partição chave toosimplify fluxos de trabalho em que várias contas de serviços de mídia estiver gravando toohello mesma conta de armazenamento.
RowKey|{toomidnight segundos} _ {valor aleatório}|01688_00199<br/><br/>chave de linha de saudação começa com o número de saudação de consultas em segundos toomidnight tooallow estilo n superior dentro de uma partição. Para saber mais, confira [este artigo](../cosmos-db/table-storage-design-guide.md#log-tail-pattern). 
Timestamp|Data/hora|Auto timestamp do hello tabela do Azure 2016-09-09T22:43:42.241Z
Tipo|tipo de saudação da entidade de saudação fornecendo os dados de telemetria|Channel/StreamingEndpoint/Archive<br/><br/>Tipo de evento é apenas um valor de cadeia de caracteres.
Nome|nome de saudação do evento de telemetria Olá|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|Olá Olá telemetria evento ocorreu (UTC)|2016-09-09T22:42:36.924Z<br/><br/>Olá observada é fornecido pelos telemetria Olá entidade envio hello (por exemplo, um canal). Pode haver problemas de sincronização de hora entre os componentes para que esse valor seja aproximado
ServiceID|{service ID}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
Propriedades específicas da entidade|Conforme definido pelo evento Olá|StreamName: stream1, Bitrate 10123, …<br/><br/>propriedades restantes Olá são definidas para Olá recebe o tipo de evento. O conteúdo da Tabela do Azure são pares de chave/valor.  (isto é, linhas diferentes na tabela Olá tem diferentes conjuntos de propriedades).

### <a name="entity-specific-schema"></a>Esquema específico à entidade

Há três tipos de entradas de dados de entidade específico telemetric que cada enviada por push com hello frequência a seguir:

- Pontos de extremidade de streaming: cada 30 segundos
- Canais dinâmicos: a cada minuto
- Arquivo dinâmico: a cada minuto

**Ponto de Extremidade de Streaming**

Propriedade|Valor|Exemplos
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Carimbo de hora automática da Tabela do Azure 2016-09-09T22:43:42.241Z
Tipo|Tipo|StreamingEndpoint
Nome|Nome|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID do Serviço|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Nome do host do ponto de extremidade Olá|builddemoserver.origin.mediaservices.windows.net
StatusCode|Status HTTP dos registros|200
ResultCode|Detalhe do código do resultado|S_OK
RequestCount|Solicitação total na agregação Olá|3
BytesSent|Bytes agregados enviados|2987358
ServerLatency|Latência média do servidor (incluindo armazenamento)|129
E2ELatency|Latência média de ponta a ponta|250

**Canal dinâmico**

Propriedade|Valor|Exemplos/notas
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto timestamp do hello tabela do Azure 2016-09-09T22:43:42.241Z
Tipo|Tipo|Canal
Nome|Nome|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID do Serviço|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|Tipo de faixa de áudio/vídeo/texto|vídeo/áudio
TrackName|Nome da faixa de saudação|vídeo/áudio_1
Bitrate|Controlar taxa de bits|785000
CustomAttributes||   
IncomingBitrate|Taxa de bits de entrada real|784548
OverlapCount|Ingestão de sobreposição no Olá|0
DiscontinuityCount|Descontinuidade para controle|0
LastTimestamp|Carimbo de hora dos últimos dados ingeridos|1800488800
NonincreasingCount|Contagem de fragmentos descartados devido aumentando toonon timestamp|2
UnalignedKeyFrames|Se recebemos fragmentos (em níveis de qualidade) quando os quadros-chave não estão alinhados |Verdadeiro
UnalignedPresentationTime|Se recebemos fragmentos (em níveis/controle de qualidade) quando o tempo de apresentação não estiver alinhado|Verdadeiro
UnexpectedBitrate|True, se a taxa de bits calculada/real para controle de áudio/vídeo for maior do que 40.000 bps, e IncomingBitrate == 0 OU IncomingBitrate e actualBitrate diferirem em 50% |Verdadeiro
Healthy|True, se <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> são todos 0|Verdadeiro<br/><br/>Íntegra é uma função composta que retorna false quando qualquer Olá espera condições a seguir:<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames == True<br/>- UnalignedPresentationTime == True<br/>- UnexpectedBitrate == True

**Arquivamento dinâmico**

Propriedade|Valor|Exemplos/notas
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Auto timestamp do hello tabela do Azure 2016-09-09T22:43:42.241Z
Tipo|Tipo|Arquivo
Nome|Nome|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|ID do Serviço|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|URL do programa|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Nome da faixa de saudação|áudio_1
TrackType|Tipo de faixa de saudação|Áudio/vídeo
CustomAttribute|Cadeia de caracteres hexadecimal que diferencia faixas diferentes com o mesmo nome e a taxa de bits (ângulo da câmeras múltiplas)|
Bitrate|Controlar taxa de bits|785000
Healthy|True, se FragmentDiscardedCount == 0 && ArchiveAcquisitionError == False|True (esses dois valores não estão presentes na métrica Olá mas estiverem presentes no evento de origem Olá)<br/><br/>Íntegra é uma função composta que retorna false quando qualquer Olá espera condições a seguir:<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError == True

## <a name="general-qa"></a>Perguntas e respostas gerais

### <a name="how-tooconsume-metrics-data"></a>Como os dados de métricas de tooconsume?

Dados de métricas são armazenados como uma série de tabelas do Azure na conta de armazenamento do cliente hello. Esses dados podem ser consumidos usando Olá ferramentas a seguir:

- SDK do AMS
- Microsoft Azure Storage Explorer (dá suporte ao formato de valores separados por toocomma de exportação e processada no Excel)
- API REST

### <a name="how-toofind-average-bandwidth-consumption"></a>Como toofind média de consumo de largura de banda?

Olá consumo de largura de banda média é a média de saudação de BytesSent em um intervalo de tempo.

### <a name="how-toodefine-streaming-unit-count"></a>Como contagem de unidade de streaming toodefine?

Olá, contagem de unidade de streaming pode ser definida como Olá taxa de transferência máxima de pontos de extremidade de streaming do serviço Olá dividido pela taxa de transferência de pico de saudação de um ponto de extremidade de streaming. Olá pico utilizável taxa de transferência de um ponto de extremidade de streaming é 160 Mbps.
Por exemplo, suponha a taxa de transferência de pico de saudação do serviço do cliente é de 40 MBps (Olá valor máximo de BytesSent em um intervalo de tempo). Em seguida, Olá contagem de unidade de streaming é igual too(40 MBps) * (8 bits/byte) /(160 Mbps) = 2 unidades de streaming.

### <a name="how-toofind-average-requestssecond"></a>Como média toofind solicitações/segundo?

toofind Olá média de solicitações por segundo, computar número médio de saudação de solicitações (RequestCount) em um intervalo de tempo.

### <a name="how-toodefine-channel-health"></a>Como toodefine canal integridade?

Integridade de canal pode ser definida como uma composição função booleana é false quando qualquer uma das seguintes condições de saudação mantém:

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>Como toodetect descontinuidades?

descontinuidades toodetect, localizar todas as entradas de dados de canal onde DiscontinuityCount > 0. Olá correspondente ObservedTime timestamp indica vezes Olá na qual ocorreram descontinuidades hello.

### <a name="how-toodetect-timestamp-overlaps"></a>Como o carimbo de hora toodetect sobrepõe?

sobreposições de carimbo de hora toodetect, localizar todas as entradas de dados de canal onde OverlapCount > 0. Olá correspondente ObservedTime timestamp indica Olá vezes no qual Olá timestamp sobrepõe ocorreram.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Como toofind streaming solicitar falhas e os motivos?

falhas de solicitação streaming toofind e motivos, encontrar todas as entradas de dados de ponto de extremidade de Streaming onde ResultCode não é igual tooS_OK. campo correspondente de StatusCode Olá indica motivo Olá falha de solicitação de saudação.

### <a name="how-tooconsume-data-with-external-tools"></a>Como os dados de tooconsume com ferramentas externas?

Dados telemetric podem ser processados e visualizados por hello ferramentas a seguir:

- PowerBI
- Application Insights
- Azure Monitor (anteriormente Shoebox)
- Painel dinâmico do AMS
- Portal do Azure (pendente versão)

### <a name="how-toomanage-data-retention"></a>Como a retenção de dados toomanage?

sistema de telemetria Olá não fornece gerenciamento de retenção de dados ou exclusão automática antigos registros. Portanto, você precisa toomanage e excluir registros antigos manualmente da tabela de armazenamento hello. Você pode consultar toostorage SDK como toodo-lo.

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
