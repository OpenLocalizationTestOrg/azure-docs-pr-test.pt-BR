---
title: "aaaMonitor uso e estatísticas em um serviço de pesquisa do Azure | Microsoft Docs"
description: "Acompanhe o consumo de recursos e o tamanho de índice da Pesquisa do Azure, um serviço de pesquisa de nuvem hospedado do Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Criar um serviço do Azure Search

O Azure Search oferece vários recursos para acompanhar o uso e o desempenho de serviços de pesquisa. Isso lhe dá acesso toometrics, logs, as estatísticas de índice e os recursos de monitoramento estendidos no Power BI. Este artigo descreve como tooenable Olá diferentes estratégias de monitoramentos e como toointerpret Olá dados resultantes.

## <a name="azure-search-metrics"></a>Métrica do Azure Search
Métricas lhe dão visibilidade praticamente em tempo real de seu serviço de pesquisa e estão disponíveis para todos os serviços, sem nenhuma configuração adicional. Eles permitem controlar o desempenho de saudação do seu serviço de backup too30 dias.

O Azure Search coleta dados de três métricas diferentes:

* Pesquisar latência: serviço de pesquisa de saudação de tempo necessário tooprocess consultas de pesquisa, agregadas por minuto.
* QPS (consultas de pesquisa por segundo): o número de consultas de pesquisa recebidas por segundo, agregadas por minuto.
* Percentual das consultas de pesquisa limitadas: o percentual de consultas de pesquisa que foram limitadas, agregadas por minuto.

![Captura de tela da atividade de QPS][1]

### <a name="set-up-alerts"></a>Configurar alertas
Na página de detalhes de métrica hello, você pode configurar alertas tootrigger uma notificação por email ou uma ação automatizada quando uma métrica exceder um limite que você definiu.

Para obter mais informações sobre métricas, verifique a documentação completa de saudação no Monitor do Azure.  

## <a name="how-tootrack-resource-usage"></a>Como o uso de recursos tootrack
Controle o crescimento de saudação de índices e o tamanho do documento pode ajudá-lo a ajustar a capacidade de forma proativa antes de atingir o limite superior de saudação estabelecida para o serviço. Você pode fazer isso no portal de saudação ou programaticamente usando a API REST de saudação.

### <a name="using-hello-portal"></a>Usando o portal de saudação

uso de recursos de toomonitor, exibir contagens de saudação e estatísticas para o serviço no hello [portal](https://portal.azure.com).

1. Entrar toohello [portal](https://portal.azure.com).
2. Abra o painel de serviço de saudação do seu serviço de pesquisa do Azure. Blocos para serviço Olá podem ser encontrados na Home page do hello, ou você pode procurar o serviço de toohello de procurar em Olá JumpBar.

Olá seção uso inclui um medidor que informa qual parte dos recursos disponíveis estão atualmente em uso. Para obter informações sobre os limites por serviço para índices, documentos e armazenamento, consulte [Limites de serviço](search-limits-quotas-capacity.md).

  ![Bloco Uso][2]

> [!NOTE]
> saudação de captura de tela acima para o serviço gratuito hello, que tem um máximo de uma réplica de partição cada e pode somente índices host 3, 10.000 documentos ou 50 MB de dados, o que ocorrer primeiro. Os serviços criados nos tipos de preço Básico ou Standard têm limites de serviço muito maiores. Para obter mais informações sobre como escolher um tipo de preço, consulte [Escolher um tipo de preço ou SKU](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Usando a API REST de saudação
Olá API de REST de pesquisa do Azure e Olá SDK .NET fornecem as métricas de tooservice acesso programático.  Se você estiver usando [indexadores](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload um índice de banco de dados SQL ou banco de dados do Azure Cosmos, mais uma API está disponível tooget números de saudação precisar.

* [Obter estatísticas de índice](/rest/api/searchservice/get-index-statistics)
* [Contar documentos](/rest/api/searchservice/count-documents)
* [Obter o status do indexador](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Como tooexport registra em log e métricas

Você pode exportar os logs de operação Olá para seus dados brutos hello e de serviço para métricas de saudação descritos em Olá anterior seção. Logs de operação que você saiba como o serviço de hello está sendo usado e pode ser consumido por meio do Power BI, quando os dados são copiados tooa conta de armazenamento. O Azure Search fornece um pacote de conteúdo de monitoramento do Power BI para essa finalidade.


### <a name="enabling-monitoring"></a>Habilitar o monitoramento
Abra o serviço de pesquisa do Azure no hello [portal do Azure](http://portal.azure.com) em Olá habilitar monitoramento de opção.

Escolha dados saudação deseja tooexport: Logs, métricas ou ambos. Pode copiá-lo tooa conta de armazenamento, envie-o hub de eventos tooan ou exportá-lo tooLog análise.

![Como tooenable monitoramento no portal de saudação][3]

tooenable usando o PowerShell ou Olá CLI do Azure, consulte a documentação de saudação [aqui](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Esquemas de métrica e logs
Quando os dados de saudação são copiados tooa armazenamento de conta, hello dados estão formatados como JSON e do local em dois contêineres:

* insights-logs-operationlogs: para logs de tráfego de pesquisa
* insights-metrics-pt1m: para métrica

Haverá um blob por hora, por contêiner.

Exemplo de caminho: `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Esquema do log
Olá logs blobs contêm os logs de tráfego do serviço de pesquisa.
Cada blob tem um objeto-raiz chamado **registros** que contém uma matriz de objetos do log.
Cada blob tem registros na operação Olá todos os que ocorrem durante a saudação mesma hora.

| Nome | Tipo | Exemplo | Observações |
| --- | --- | --- | --- |
| tempo real |datetime |"2015-12-07T00:00:43.6872559Z" |Carimbo de hora da operação de saudação |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |Seu ResourceId |
| operationName |string |"Query.Search" |nome de saudação da operação de saudação |
| operationVersion |string |"2015-02-28" |Olá api-version usado |
| categoria |string |"OperationLogs" |constante |
| resultType |string |"Success" |Valores possíveis: Success ou Failure |
| resultSignature |int |200 |Código do resultado HTTP |
| durationMS |int |50 |Duração da operação de saudação em milissegundos |
| propriedades |objeto |Consulte a tabela a seguir de saudação |Objeto que contém os dados específicos da operação |

**Esquema de propriedades**
| Nome | Tipo | Exemplo | Observações |
| --- | --- | --- | --- |
| Descrição |string |"GET /indexes('content')/docs" |ponto de extremidade da operação Olá |
| Consultar |string |"?search=AzureSearch&$count=true&api-version=2015-02-28" |parâmetros de consulta Olá |
| Documentos |int |42 |Número de documentos processados |
| IndexName |string |"testindex" |Nome do índice de saudação associada à operação Olá |

#### <a name="metrics-schema"></a>Esquema de métricas
| Nome | Tipo | Exemplo | Observações |
| --- | --- | --- | --- |
| resourceId |string |"/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE" |id do recurso |
| metricName |string |"Latency" |nome de saudação da métrica de saudação |
| tempo real |datetime |"2015-12-07T00:00:43.6872559Z" |carimbo de hora da operação Olá |
| média |int |64 |valor médio de saudação de amostras de saudação bruto no intervalo de tempo de métrica de saudação |
| mínimo |int |37 |valor mínimo de saudação de amostras de saudação bruto no intervalo de tempo de métrica de saudação |
| máximo |int |78 |valor máximo de saudação de amostras de saudação bruto no intervalo de tempo de métrica de saudação |
| total |int |258 |valor total de saudação de amostras de saudação bruto no intervalo de tempo de métrica de saudação |
| count |int |4 |número de saudação de amostras brutos usado toogenerate métrica de saudação |
| intervalo de tempo |string |"PT1M" |intervalo de tempo de saudação de métrica de saudação na ISO 8601 |

Todas as métricas são reportadas em intervalos de um minuto. Cada métrica expõe valores mínimo, máximo e médios por minuto.

Para métrica de SearchQueriesPerSecond hello, mínimo é o valor mais baixo de saudação para consultas de pesquisa por segundo, que foi registrado durante esse minuto. Olá mesmo se aplica toohello máximo. Médio, é Olá agregação em minutos todo hello.
Pense sobre esse cenário durante um minuto: um segundo de alta carga é hello máximo para SearchQueriesPerSecond, seguido de 58 segundos da carga média e, finalmente, um segundo com apenas uma consulta, que é hello mínimo.

Para ThrottledSearchQueriesPercentage, mínimo, máximo, média e total, todos têm Olá mesmo valor: Olá porcentagem de consultas de pesquisa que foi limitada, do número total de saudação de consultas de pesquisa durante um minuto.

## <a name="analyzing-your-data-with-power-bi"></a>Analisar seus dados com o Power BI

É recomendável usar [Power BI](https://powerbi.microsoft.com) tooexplore e visualizar seus dados. Você pode facilmente conectar tooyour conta de armazenamento do Azure e iniciar rapidamente a análise dos dados.

A pesquisa do Azure fornece um [pacote de conteúdo do Power BI](https://app.powerbi.com/getdata/services/azure-search) que permite que você toomonitor e entender seu tráfego de pesquisa com tabelas e gráficos predefinidos. Ele contém um conjunto de relatórios do Power BI que se conectar a dados tooyour automaticamente e fornecem informações visuais sobre o serviço de pesquisa. Para obter mais informações, consulte Olá [página de Ajuda do pacote de conteúdo](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Painel do Power BI para o Azure Search][4]

## <a name="next-steps"></a>Próximas etapas
Revisão [Dimensionar partições e réplicas](search-limits-quotas-capacity.md) para obter orientação sobre como toobalance Olá alocação de partições e réplicas para um serviço existente.

Visite [Gerenciar o seu serviço do Search no Microsoft Azure](search-manage.md), para obter mais informações sobre a administração do serviço, ou [Desempenho e otimização](search-performance-optimization.md), para obter diretrizes de ajuste.

Saiba mais sobre como criar relatórios incríveis. Confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) para obter detalhes

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
