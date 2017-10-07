---
title: "aaaJob dimensionamento com funções do Azure Stream Analytics & AzureML | Microsoft Docs"
description: "Saiba como tooproperly dimensionar trabalhos do Stream Analytics (particionamento, quantidade SU e muito mais) ao usar as funções de aprendizado de máquina do Azure."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 47ce7c5e-1de1-41ca-9a26-b5ecce814743
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fbdfaf7e8e86896c56f1d18bbde3a10bd3dca04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-stream-analytics-job-with-azure-machine-learning-functions"></a>Dimensionar seu trabalho do Stream Analytics com funções do Azure Machine Learning
Ele geralmente é muito fácil tooset um trabalho de análise de fluxo e executar alguns dados de exemplo por meio dele. O que podemos fazer quando precisamos toorun Olá mesmo trabalho com o maior volume de dados? Ela requer toounderstand como tooconfigure Olá análise de fluxo de trabalho para que a escala. Neste documento, abordaremos aspectos especiais de saudação da análise de fluxo de dimensionamento de trabalhos com funções de aprendizado de máquina. Para obter informações sobre como trabalhos do Stream Analytics tooscale em geral consulte artigo Olá [dimensionamento de trabalhos](stream-analytics-scale-jobs.md).

## <a name="what-is-an-azure-machine-learning-function-in-stream-analytics"></a>O que é uma função do Azure Machine Learning no Stream Analytics?
Uma função de aprendizado de máquina no Stream Analytics pode ser usada como uma chamada de função regular Olá linguagem de consulta do Stream Analytics. No entanto, por trás da cena hello, chamadas de função hello são, na verdade, as solicitações de serviço de Web de aprendizado de máquina do Azure. Suporte "processamento em lotes" várias linhas, que é chamado de minia lote serviços web do aprendizado de máquina, em Olá mesmo web chamada de API de serviço, tooimprove produtividade geral. Consulte Olá seguintes artigos para obter mais detalhes. [Funções de aprendizado de máquina do azure no Stream Analytics](https://blogs.technet.microsoft.com/machinelearning/2015/12/10/azure-ml-now-available-as-a-function-in-azure-stream-analytics/) e [serviços de Web de aprendizado de máquina do Azure](../machine-learning/machine-learning-consume-web-services.md).

## <a name="configure-a-stream-analytics-job-with-machine-learning-functions"></a>Configurar seu trabalho do Stream Analytics com funções de Machine Learning
Ao configurar uma função de aprendizado de máquina para o trabalho do Stream Analytics, há dois parâmetros tooconsider, tamanho de lote de saudação de chamadas de função de aprendizado de máquina hello e Olá unidades (SUs) configuradas para o trabalho de análise de fluxo de saudação de streaming. toodetermine Olá os valores apropriados para esses, primeiro uma decisão deve ser feita entre a latência e taxa de transferência, ou seja, latência de trabalho do Stream Analytics hello e taxa de transferência de cada SU. SUs podem sempre ser adicionado tooa throughput de tooincrease de trabalho de uma consulta do Stream Analytics bem particionado, embora SUs adicional aumenta o custo de saudação de execução do trabalho hello.

Portanto, é importante toodetermine Olá *tolerância* de latência em um trabalho de análise de fluxo de execução. Naturalmente, latência adicional da execução de solicitações de serviço de aprendizado de máquina do Azure aumentará com tamanho de lote, que vai compor a latência de saudação do trabalho de análise de fluxo de saudação. Olá outro lado, aumentando o tamanho do lote permite que tooprocess de trabalho do Stream Analytics hello * mais eventos por hello *mesmo número* de aprendizado de máquina solicitações ao serviço web. Geralmente aumento de saudação de latência de serviço de web do aprendizado de máquina é inferior linear toohello aumento de tamanho do lote, portanto, é importante tooconsider hello mais eficiente tamanho de lote para um serviço web de aprendizado de máquina em qualquer situação. tamanho do lote saudação padrão para o serviço web de saudação solicitações é 1000 e pode ser modificado usando Olá [API de REST de análise de fluxo](https://msdn.microsoft.com/library/mt653706.aspx "API de REST de análise de fluxo") ou hello [cliente do PowerShell para análise de fluxo](stream-analytics-monitor-and-manage-jobs-use-powershell.md "PowerShell de cliente para análise de fluxo").

Depois que um tamanho de lote tiver sido determinado, quantidade de saudação de streaming de unidades (SUs) podem ser determinadas, com base no hello número de eventos de função hello precisa tooprocess por segundo. Para obter mais informações sobre o unidades de streaming, consulte Dimensionar trabalhos do [Trabalhos de escala do Stream Analytics](stream-analytics-scale-jobs.md).

Em geral, há 20 conexões simultâneas toohello serviço de web de aprendizado de máquina para cada 6 SUs, exceto que os trabalhos de SU 1 e 3 SU obterá 20 conexões simultâneas também.  Por exemplo, se a taxa de dados de entrada hello está 200.000 eventos por segundo e o tamanho de lote Olá fica toohello padrão de 1000 Olá resultante web serviço latência com lotes simplificado de eventos de 1000 é 200 ms. Isso significa que cada conexão pode fazer 5 solicitações de serviço de web de aprendizado de máquina toohello em um segundo. Com 20 conexões, trabalho de análise de fluxo de saudação pode processar 20.000 eventos em 200 MS e, portanto, 100.000 eventos em um segundo. Portanto tooprocess 200.000 eventos por segundo, trabalho de análise de fluxo de saudação precisa 40 conexões simultâneas, que são fornecidos too12 SUs. Olá diagrama a seguir ilustra a solicitações de saudação de extremidade de serviço web de aprendizado de máquina toohello de trabalho do Stream Analytics de hello – cada SUs de 6 tem 20 serviço de web de aprendizado para tooMachine conexões simultâneas no máximo.

![Dimensionar o Stream Analytics com as funções de Machine Learning, exemplo de trabalho 2](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-00.png "Dimensionar o Stream Analytics com as funções do Machine Learning, exemplo de trabalho 2")

Em geral, ***B*** para tamanho de lote, ***L*** para latência de serviço Olá web no tamanho do lote B em milissegundos, Olá taxa de transferência de um trabalho do Stream Analytics com ***N*** é:

![Fórmula para Dimensionar o Stream Analytics com as funções do Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-02.png "Fórmula para Dimensionar o Stream Analytics com as funções do Machine Learning")

Uma consideração adicional pode ser Olá 'máximo de chamadas simultâneas' em Olá no lado do serviço de web do aprendizado de máquina, é recomendável tooset esse valor máximo de toohello (200 no momento).

Para obter mais informações sobre essa configuração, consulte Olá [artigo de escala para serviços de Web do aprendizado de máquina](../machine-learning/machine-learning-scaling-webservice.md).

## <a name="example--sentiment-analysis"></a>Exemplo – análise de sentimento
Olá exemplo a seguir inclui um trabalho do Stream Analytics com análise de sentimento Olá função de aprendizado de máquina, conforme descrito em Olá [tutorial de integração de aprendizado de máquina de análise de fluxo](stream-analytics-machine-learning-integration-tutorial.md).

Olá, consulta é uma consulta totalmente particionada simple seguida de saudação **sentimento** de função, conforme mostrado abaixo:

    WITH subquery AS (
        SELECT text, sentiment(text) as result from input
    )

    Select text, result.[Score]
    Into output
    From subquery

Considere Olá seguindo o cenário. com uma taxa de transferência de 10.000 tweets por segundo, um trabalho de análise de fluxo deve ser criado tooperform análise de sentimento de tweets de saudação (eventos). Usando 1 SU, este trabalho do Stream Analytics foi toohandle capaz de tráfego de Olá? Com tamanho de lote de padrão de saudação do trabalho de saudação 1000 deve ser capaz de tookeep backup com entrada hello. Olá mais Adicionar função de aprendizado de máquina deve gerar não mais do que um segundo de latência, que é a latência geral padrão de Olá de análise de sentimento Olá serviço web de aprendizado de máquina (com um tamanho de lote padrão de 1000). trabalho de análise de fluxo Olá **geral** ou latência de ponta a ponta normalmente seria alguns segundos. Dê uma olhada mais detalhada para esse trabalho do Stream Analytics, *especialmente* Olá chamadas de função de aprendizado de máquina. Com o tamanho do lote hello como 1.000, uma taxa de transferência de 10.000 eventos levará aproximadamente 10 solicitações tooweb serviço. Mesmo com 1 SU, há suficiente tooaccommodate conexões simultâneas esse tráfego de entrada.

Mas e se aumenta a taxa de eventos de entrada hello x 100 e agora precisa de trabalho do Stream Analytics Olá tweets de 1.000.000 tooprocess por segundo? Há duas opções:

1. Aumentar o tamanho do lote hello, ou
2. Tooprocess de fluxo de entrada hello partição Olá eventos em paralelo

Com a opção de primeiro hello, Olá trabalho **latência** aumentará.

Com a segunda opção de hello, SUs mais seria necessário toobe provisionado e, portanto, gerar simultâneas mais solicitações de serviço web de aprendizado de máquina. Isso significa que o trabalho de saudação **custo** aumentará.

Presumem que a latência de saudação de análise de sentimento Olá serviço web de aprendizado de máquina é 200 ms para lotes de 1000 eventos ou abaixo, 250ms para lotes de 5.000 eventos, 300 ms de lotes de 10.000 eventos ou 500 ms para lotes de eventos de 25.000.

1. Usando a opção de primeira Olá, (**não** provisionamento mais SUs), tamanho do lote Olá pode ser aumentado muito**25.000**. Isso seria permitir Olá trabalho tooprocess 1.000.000 eventos com 20 conexões simultâneas toohello serviço web de aprendizado de máquina (com uma latência de 500 ms por chamada). Olá assim a latência adicional de trabalho do Stream Analytics Olá devido a solicitações de função de sentimento toohello contra Olá aprendizado de máquina, solicitações de serviço web deve ser aumentadas de **200 MS** muito**500 MS**. No entanto, observe que tamanho de lote **não é possível** ser aumentado infinitamente como serviços web do aprendizado de máquina hello requer tamanho da carga de saudação de uma solicitação de 4 MB ou web menor tempo limite de solicitações de serviço depois de 100 segundos da operação.
2. Usando a opção segundo Olá, tamanho do lote Olá é deixado em 1.000, com latência de serviço web 200 MS, cada serviço de web toohello 20 conexões simultâneas deve ser capaz de tooprocess 1000 * 20 * 5 eventos = 100.000 por segundo. Para eventos de 1.000.000 tooprocess por segundo, o trabalho de saudação precisaria 60 SUs. Primeira opção toohello comparados, análise de fluxo de trabalho criam web mais solicitações de lote de serviço, por sua vez gerando um aumento de custo.

Abaixo está uma tabela para a taxa de transferência de saudação do trabalho do Stream Analytics Olá para SUs diferente e tamanhos de lote (em número de eventos por segundo).

| tamanho do lote (latência de AM) | 500 (200 ms) | 1.000 (200 ms) | 5.000 (250 ms) | 10.000 (300 ms) | 25.000 (500 ms) |
| --- | --- | --- | --- | --- | --- |
| **1 SU** |2.500 |5.000 |20.000 |30.000 |50.000 |
| **3 SUs** |2.500 |5.000 |20.000 |30.000 |50.000 |
| **6 SUs** |2.500 |5.000 |20.000 |30.000 |50.000 |
| **12 SUs** |5.000 |10.000 |40.000 |60.000 |100.000 |
| **18 SUs** |7.500 |15.000 |60.000 |90.000 |150.000 |
| **24 SUs** |10.000 |20.000 |80.000 |120.000 |200.000 |
| **…** |… |… |… |… |… |
| **60 SUs** |25.000 |50.000 |200.000 |300.000 |500.000 |

Agora, você já deve ter uma boa compreensão de como as funções do Machine Learning funcionam no Stream Analytics. Você provavelmente também entender que os trabalhos do Stream Analytics "pull" dados de fontes de dados e cada "pull" retorna um lote de eventos para Olá tooprocess de trabalho do Stream Analytics. Como esse modelo de pull afeta solicitações de serviço de web de aprendizado de máquina Olá?

Normalmente, tamanho do lote Olá que definimos para funções de aprendizado de máquina não exatamente é divisível pelo número de saudação de eventos retornados por cada análise de fluxo de trabalho "pull". Quando isso ocorre, Olá serviço web de aprendizado de máquina com lotes "parciais" será chamado. Isso é feito toonot incorrer em latência de trabalho adicional sobrecarga em eventos de conciliação de toopull pull.

## <a name="new-function-related-monitoring-metrics"></a>Novas métricas de monitoramentos relacionadas à função
Na área de Monitor de um trabalho de análise de fluxo de Olá, foram adicionadas três métricas adicionais relacionadas à função. Eles são solicitações de função, eventos de função e solicitações de função com falha, conforme mostrado no gráfico de saudação abaixo.

![Métricas para Dimensionar o Stream Analytics com as funções de Machine Learning](./media/stream-analytics-scale-with-ml-functions/stream-analytics-scale-with-ml-functions-01.png "Métricas para Dimensionar o Stream Analytics com as funções do Machine Learning")

Olá são definidas da seguinte maneira:

**FUNÇÃO solicitações**: Olá o número de solicitações de função.

**EVENTOS de função**: número eventos Olá Olá função solicitações.

**Falha na função solicitações**: Olá o número de solicitações de função com falha.

## <a name="key-takeaways"></a>Principais observações
toosummarize Olá principais pontos, em ordem tooscale um trabalho do Stream Analytics com funções de aprendizado de máquina, hello itens a seguir devem ser considerados:

1. taxa de eventos de entrada Hello
2. Olá tolerado latência para Olá executar análise de fluxo de trabalho (e, portanto, o tamanho de lote de saudação do serviço de web de aprendizado de máquina saudação de solicitações)
3. Olá provisionado SUs de análise de fluxo e número de saudação de solicitações de serviço web de aprendizado de máquina (Olá adicionais função custos relacionados)

Uma consulta do Stream Analytics totalmente particionada foi usada como exemplo. Se for necessária uma consulta mais complexa Olá [Fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) é um ótimo recurso para obter ajuda adicional da equipe de análise de fluxo de saudação.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre análise de fluxo, consulte:

* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
