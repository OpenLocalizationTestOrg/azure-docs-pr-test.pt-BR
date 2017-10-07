---
title: "aaaIntroduction tooStream análise | Microsoft Docs"
description: "Saiba mais sobre o Stream Analytics, um serviço gerenciado que ajuda a analisar dados de streaming de saudação Internet das coisas (IoT) em tempo real."
keywords: "análise como um serviço, serviços gerenciados, processamento de fluxo, análise de fluxo, o que é Stream Analytics"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>O que é o Stream Analytics?

O Azure Stream Analytics é um mecanismo de processamento de eventos totalmente gerenciado que lhe permite configurar cálculos de análise em tempo real no fluxo de dados. Olá dados podem vir de dispositivos, sensores, sites da web, feeds de mídia social, aplicativos, sistemas de infraestrutura e muito mais. 

## <a name="what-can-i-do-with-stream-analytics"></a>O que posso fazer com o Stream Analytics?

Usar a análise de fluxo tooexamine grandes volumes de dados que fluem de dispositivos ou processos, extrair informações saudação do fluxo de dados e procurar padrões, tendências e relações. Com base no que é em dados hello, em seguida, você pode executar tarefas de aplicativo. Por exemplo, você pode gerar alertas, disparar fluxos de trabalho de automação, feed tooa informações ferramenta como o Power BI de relatório ou armazenar dados para investigação posterior. 

Exemplos:

* Análise e alertas de negociação na bolsa em tempo real oferecidas por empresas de serviços financeiros.
* Detecção de fraudes em tempo real com base no exame dos dados da transação. 
* Serviços de proteção de dados e identidade.
* Análise de dados gerados por sensores e acionadores inseridos em objetos físicos (Internet das Coisas, ou IoT).
* Análise de sequência de cliques da Web.
* Usos CRM (gerenciamento de relacionamento com o cliente) clientes, como a emissão de alertas quando a experiência do cliente piora em determinado intervalo de tempo.

## <a name="how-does-stream-analytics-work"></a>Como funciona o Stream Analytics?

Este diagrama ilustra o pipeline de análise de fluxo hello, mostrando como os dados são incluídos, analisados e, em seguida, enviados para apresentação ou ação. 

![Pipeline do Stream Analytics](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

O Stream Analytics começa com uma fonte de dados de streaming. dados de saudação podem ser incluídos no Azure de um dispositivo usando um hub de eventos do Azure ou o hub IoT. dados de saudação também podem ser extraídos de um repositório de dados como o armazenamento de BLOBs do Azure. 

fluxo de saudação tooexamine, criar uma análise de fluxo *trabalho* que especifica onde Olá origem dos dados. trabalho de saudação também especifica um *transformação*&mdash;como toolook dados, padrões ou relações. Nesta tarefa, o Stream Analytics dá suporte a uma linguagem de consulta do tipo SQL que lhe permite filtrar, classificar, agregar e associar dados de streaming em um período de tempo.

Por fim, o trabalho de saudação especifica um saída toosend Olá transformado de dados para. Isso lhe permite controlar quais toodo na resposta toohello informações analisadas. Por exemplo, em resposta tooanalysis, você pode:

* Envie um comando toochange configurações do dispositivo. 
* Fila de tooa de dados que é monitorada por um processo que executa ação com base em suas descobertas de envio. 
* Envie o dashboard do Power BI tooa dados para relatórios.
* Envie dados toostorage como repositório Data Lake, o banco de dados do SQL Server ou o armazenamento de BLOBs do Azure ou tabela.

É possível monitorar e ajustar quantos eventos são processados por segundo enquanto um trabalho está em execução. Você também pode fazer com que trabalhos gerem logs de diagnóstico para solução de problemas.

## <a name="key-capabilities-and-benefits"></a>Principais recursos e benefícios

Análise de fluxo é projetado toobe fácil toouse, flexível e escalonável tooany trabalho tamanho e econômico.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Conectividade toomany entradas e saídas

Análise de fluxo se conecta diretamente muito[Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) e [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) para inclusão de fluxo e hello [serviço de armazenamento de BLOBs do Azure](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest os dados históricos. Se você receber dados de hubs de eventos, poderá combinar o Stream Analytics com outras fontes de dados e mecanismos de processamento.

A entrada de trabalho também pode incluir dados de referência (dados estáticos ou alterados lentamente). Você pode unir streaming dados toothis Referência dados tooperform pesquisa operações Olá mesma maneira que faria com consultas de banco de dados.

Rotear a saída de trabalho do Stream Analytics em muitas direções. Você pode escrever toostorage, como blobs de armazenamento do Azure ou tabelas, banco de dados de SQL do Azure, Azure Data Lake repositórios ou banco de dados do Azure Cosmos. A partir daí, dados saudação podem ir para análise de lote por meio do Azure HDInsight. Você pode enviar Olá saída tooanother serviço para consumo por outro processo, como filas, tópicos de barramento de serviço do Azure ou hubs de eventos. Você pode enviar Olá saída tooPower BI para visualização.

### <a name="ease-of-use"></a>Fácil de uso

transformações toodefine, você usa um simples, declarativo [linguagem de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) que lhe permite criar análises sofisticadas sem programação. linguagem de consulta Olá usa o fluxo de dados como entrada. Você pode filtrar e classificar dados hello, agregar valores, executar cálculos, unir dados (dentro de um fluxo ou tooreference dados) e usar as funções geoespaciais. Você pode editar consultas no portal de hello, usando o IntelliSense e a verificação de sintaxe, e você pode testar consultas usando dados de exemplo que você pode extrair do fluxo ao vivo hello.

### <a name="extensible-query-language"></a>Linguagem de consulta extensível

Você pode estender as capacidades de saudação da linguagem de consulta Olá definindo e chamar funções adicionais. Você pode definir as chamadas de função em Olá aprendizado de máquina do Azure serviço tootake aproveitar soluções de aprendizado de máquina do Azure. Você também pode integrar as funções do JavaScript definido pelo usuário (UDFs) em cálculos complexos de tooperform ordem como parte de uma consulta de análise de fluxo.

### <a name="scalability"></a>Escalabilidade

Análise de fluxo pode lidar com a too1 GB de dados de entrada por segundo. Integração com [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) e [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) permite trabalhos tooingest milhões de eventos por segundo surgimento de dispositivos conectados, clickstreams e arquivos de log, tooname alguns. Usando o recurso de partição de saudação dos hubs de eventos, você pode dividir os cálculos em etapas lógicas, cada um com hello toobe de capacidade adicional particionada tooincrease escalabilidade.

### <a name="low-cost"></a>Baixo custo

Como um serviço de nuvem, o Stream Analytics é otimizada toolet você começar a baixo custo. Você paga conforme você avança com base na quantidade de uso e hello de unidade de streaming de dados processados pelo sistema de saudação. Uso é derivado com base no volume de saudação de eventos processados e quantidade de saudação de capacidade de computação provisionado em Olá cluster toohandle trabalhos do Stream Analytics.

### <a name="reliability-quick-recovery-and-repeatability"></a>Confiabilidade, recuperação rápida e capacidade de repetição

Como um serviço gerenciado na nuvem hello, análise de fluxo ajuda a evitar a perda de dados e fornece continuidade dos negócios. Se ocorrerem falhas, o serviço de saudação fornece recursos internos de recuperação. Com capacidade de saudação toointernally manter o estado, serviço Olá fornece resultados repetíveis garantindo é tooarchive possíveis eventos e reaplicar o processamento em um futuro hello, sempre obterá Olá mesmos resultados. Isso permite que você toogo de volta no tempo e investigue cálculos ao fazer a análise da causa raiz, análise hipotética e assim por diante.

## <a name="next-steps"></a>Próximas etapas

* Comece [experimentando entradas e consultas de dispositivos IoT](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md).
* Criar um [solução de análise de fluxo de ponta a ponta](stream-analytics-real-time-fraud-detection.md) que examina toolook de metadados de telefone para chamadas fraudulentas.
* Saiba mais sobre Olá linguagem de consulta do tipo SQL para análise de fluxo e sobre os conceitos exclusivos como [funções de janela](stream-analytics-window-functions.md).
* Saiba como muito[dimensionar trabalhos do Stream Analytics](stream-analytics-scale-jobs.md). 
* Saiba como muito[integrar análise de fluxo e aprendizado de máquina do Azure](stream-analytics-machine-learning-integration-tutorial.md).
* Encontrar respostas a questões de análise de fluxo de tooyour em Olá [Fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

