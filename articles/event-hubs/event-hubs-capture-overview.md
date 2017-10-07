---
title: aaaOverview de captura de Hubs de eventos do Azure | Microsoft Docs
description: "Capturar dados telemétricos com a Captura de Hubs de Eventos"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Captura de Hubs de Eventos do Azure

Captura de Hubs de eventos do Azure permite que você tooautomatically entregar Olá fluxo de dados em Hubs de eventos tooan [armazenamento de BLOBs do Azure](https://azure.microsoft.com/services/storage/blobs/) ou [repositório Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) conta de sua escolha, com hello maior flexibilidade especificar um intervalo de tempo ou tamanho. Configuração de captura é rápido, não há nenhuma toorun os custos administrativos e ele é dimensionado automaticamente com Hubs de eventos [unidades de taxa de transferência](event-hubs-features.md#capacity). Hubs de evento captura é tooload de maneira mais fácil Olá fluxo de dados no Azure e permite que você toofocus no processamento de dados em vez de na captura de dados.

Captura de Hubs de eventos permite que você tooprocess em tempo real e pipelines com base em lotes em Olá mesmo fluxo. Isso significa que você pode criar soluções que crescem com suas necessidades ao longo do tempo. Se você estiver criando sistemas baseados em lote com o objetivo de serem processadas em tempo real, ou se desejar tooadd caminho frios eficiente tooan existente em tempo real da solução, Hubs de evento captura torna o trabalho com dados mais fáceis de streaming.

## <a name="how-event-hubs-capture-works"></a>Como a Captura de Hubs de Eventos funciona

Hubs de eventos é um buffer de tempo de retenção durável para entrada de telemetria, log distribuído de tooa semelhante. Olá tooscaling de chave em Hubs de eventos é hello [modelo de consumidor particionado](event-hubs-features.md#partitions). Cada partição é um segmento independente de dados e é consumido de forma independente. Ao longo do tempo que esses dados idades off, com base no período de retenção configurável de saudação. Assim, um Hub de Eventos específico nunca fica “cheio demais”.

Captura de Hubs de eventos permite que você toospecify sua própria conta de armazenamento de BLOBs do Azure e o contêiner ou a conta do repositório Azure Data Lake, que são usados toostore Olá capturado dados. Essas contas podem estar em Olá mesma região, como o hub de eventos ou em outra região, adicionando flexibilidade toohello do recurso de Hubs de evento captura hello.

Os dados capturados são gravados no formato [Apache Avro][Apache Avro]: um formato compacto, rápido e binário que fornece estruturas de dados avançados com esquema embutido. Esse formato é amplamente usado no ecossistema do Hadoop hello, análise de fluxo e do Azure Data Factory. Mais informações sobre como trabalhar com Avro estão disponíveis neste artigo.

### <a name="capture-windowing"></a>Janelas da Captura

Captura de Hubs de eventos permite que você tooset a captura de toocontrol uma janela. Esta janela é um tamanho mínimo e a configuração de tempo com uma "primeira política de vitórias" significando que Olá primeiro causas de gatilho encontrada uma operação de captura. Se você tiver um quinze minutos, 100 MB janela de captura e enviar 1 MB por segundo, os gatilhos de janela de tamanho Olá antes da janela de tempo de saudação. Cada partição captura independentemente e grava um blob de bloco concluído no tempo de saudação de captura, nomeado para o tempo de saudação no qual Olá intervalo de captura foi encontrado. convenção de nomenclatura de armazenamento de saudação é da seguinte maneira:

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Unidades de escala toothroughput

O tráfego dos Hubs de Eventos é controlado por [unidades de produtividade](event-hubs-features.md#capacity). Uma única unidade de produtividade permite o ingresso de 1 MB por segundo ou 1.000 eventos por segundo e duas vezes essa quantidade de saída. Os Hubs de Evento Standard podem ser configurados com 1 a 20 unidades de produtividade e outras podem ser adquiridas por meio de uma [solicitação de suporte][support request] para aumento de cota. O uso além das unidades de produtividade adquiridas é restringido. Hubs de evento captura copia os dados diretamente do armazenamento de Hubs de evento interno hello, ignorando as cotas de saída de unidade de taxa de transferência e salvando a saída para outros leitores de processamento, como análise de fluxo ou Spark.

Uma vez configurado, a Captura de Hubs de Eventos é executada automaticamente quando você envia o primeiro evento e continua em execução. toomake mais fácil para tooknow seu processamento downstream que Olá processo está funcionando, os Hubs de eventos grava arquivos vazios quando não há nenhum dado. Esse processo fornece cadência e marcador previsíveis que podem alimentar os processadores em lotes.

## <a name="setting-up-event-hubs-capture"></a>Configurando a Captura de Hubs de Eventos

Você pode configurar a captura no momento da criação Olá evento hub usando Olá [portal do Azure](https://portal.azure.com), ou usando modelos do Gerenciador de recursos do Azure. Para obter mais informações, consulte Olá artigos a seguir:

- [Habilitar a captura de Hubs de evento usando Olá portal do Azure](event-hubs-capture-enable-through-portal.md)
- [Criar um namespace de Hubs de Eventos com o hub de eventos e habilitar a Captura usando um modelo do Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Explorar arquivos Olá capturado e trabalhar com Avro

Hubs de evento captura cria arquivos no formato Avro, conforme especificado na janela de tempo de saudação configurada. Você pode exibir esses arquivos em qualquer ferramenta, como o [Gerenciador de Armazenamento do Azure][Azure Storage Explorer]. Você pode baixar Olá localmente arquivos toowork neles.

arquivos de saudação produzidos pela captura de Hubs de evento têm Olá esquema Avro a seguir:

![][3]

Arquivos de Avro de tooexplore uma maneira fácil é usando Olá [Avro ferramentas] [ Avro Tools] jar do Apache. Depois de baixar este jar, você pode ver o esquema de saudação de um arquivo do Avro específico executando o comando a seguir de saudação:

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Esse comando retorna

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

Você também pode usar ferramentas Avro tooconvert Olá tooJSON formato e executar outros tipos de processamento.

tooperform mais avançados de processamento, baixe e instale o Avro para a escolha da plataforma. Olá momento da redação deste artigo, há implementações disponíveis para C, C++, C\#, Java, NodeJS, Perl, PHP, Python e Ruby.

O Apache Avro tem guias de Introdução completos para [Java][Java] e [Python][Python]. Você também pode ler Olá [Introdução aos Hubs de evento captura](event-hubs-capture-python.md) artigo.

## <a name="how-event-hubs-capture-is-charged"></a>Como a Captura de Hubs de Eventos é cobrada

Hubs de evento captura medição da mesma forma toothroughput unidades: como uma taxa por hora. custos de saudação é diretamente proporcional toohello o número de unidades de taxa de transferência adquirido para o namespace de saudação. Como unidades de taxa de transferência são aumentadas e reduzidas, metros de Hubs de evento captura aumentam e diminuir tooprovide correspondência de desempenho. medidores de saudação ocorrerem em tandem. Para detalhes de preços, consulte [Preços dos Hubs de Eventos](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Próximas etapas

Captura de Hubs de evento é tooget dados de maneira mais fácil de saudação no Azure. Usando o Azure Data Lake, o Azure Data Factory e o Azure HDInsight, você pode executar processamento em lotes e outras análises usando ferramentas familiares e plataformas de sua escolha, na escala que precisar.

Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Começar a enviar e receber eventos](event-hubs-dotnet-framework-getstarted-send.md)
* Um [aplicativo de exemplo completo que usa os Hubs de Eventos][sample application that uses Event Hubs]
* [Visão Geral dos Hubs de Eventos][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
