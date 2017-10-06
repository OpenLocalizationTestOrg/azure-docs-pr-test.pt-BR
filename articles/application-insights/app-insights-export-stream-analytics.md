---
title: "aaaExport usando a análise de fluxo do Azure Application Insights | Microsoft Docs"
description: "Análise de fluxo contínuo pode transformar, filtrar e rota Olá você de exportação de dados do Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Use Stream Analytics tooprocess dados exportados do Application Insights
[O Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) é Olá a ferramenta ideal para o processamento de dados [exportados do Application Insights](app-insights-export-telemetry.md). O Stream Analytics pode extrair dados de várias fontes. Ele pode transformar e filtrar dados de saudação e, em seguida, encaminhá-lo tooa vários coletores.

Neste exemplo, vamos criar um adaptador que usa dados do Application Insights, renomeia e processa alguns dos campos de saudação e direcioná-lo no Power BI.

> [!WARNING]
> Há muito melhor e mais fácil [maneiras recomendadas dados do Application Insights toodisplay no Power BI](app-insights-export-power-bi.md). Olá, caminho ilustrado aqui é apenas um tooillustrate de exemplo como tooprocess de dados exportados.
> 
> 

![Diagrama de bloco para exportação por meio de SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Criar armazenamento no Azure
A exportação contínua sempre gera conta de armazenamento do Azure tooan dados, portanto você precisa de armazenamento de saudação toocreate primeiro.

1. Criar uma conta de armazenamento "clássico" em sua assinatura no hello [portal do Azure](https://portal.azure.com).
   
   ![No portal do Azure, escolha Novo, Dados e Armazenamento](./media/app-insights-export-stream-analytics/030.png)
2. Criar um contêiner
   
    ![No novo armazenamento de hello, selecionar contêineres, clique em bloco de contêineres hello e, em seguida, adicionar](./media/app-insights-export-stream-analytics/040.png)
3. Copie a chave de acesso de armazenamento Olá
   
    Você precisará dele em breve tooset o serviço de análise de fluxo de entrada toohello hello.
   
    ![No armazenamento Olá, abra configurações, chaves e faça uma cópia da saudação chave de acesso primária](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Iniciar a exportação contínua tooAzure armazenamento
[exportação contínua](app-insights-export-telemetry.md) move os dados do Application Insights para o armazenamento do Azure.

1. Na Olá portal do Azure, procure o recurso do Application Insights toohello criado para o seu aplicativo.
   
    ![Selecione Navegar, Application Insights e o nome do seu projeto.](./media/app-insights-export-stream-analytics/050.png)
2. Crie uma exportação contínua.
   
    ![Escolha as Configurações, Exportação Contínua e Adicionar](./media/app-insights-export-stream-analytics/060.png)

    Selecione a conta de armazenamento de saudação criado anteriormente:

    ![Definir o destino de exportação de saudação](./media/app-insights-export-stream-analytics/070.png)

    Defina tipos de evento de saudação desejado toosee:

    ![Escolher os tipos de evento](./media/app-insights-export-stream-analytics/080.png)

1. Deixe que alguns dados sejam acumulados. Agora relaxe e deixe as pessoas usarem seu aplicativo por um tempo. A telemetria chegará e você verá os gráficos estatísticos no [gerenciador de métricas](app-insights-metrics-explorer.md) e eventos individuais na [pesquisa de diagnóstico](app-insights-diagnostic-search.md). 
   
    E, além disso, dados de saudação exportará tooyour armazenamento. 
2. Inspecione dados hello exportada. No Visual Studio, escolha **Exibir/Cloud Explorer**e abra Azure/Armazenamento. (Se você não tiver essa opção de menu, você precisa tooinstall Olá SDK do Azure: Abrir caixa de diálogo de novo projeto hello e abra o Visual C# / nuvem / obter o Microsoft Azure SDK para .NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Anote a parte comum Olá Olá do nome do caminho, que é derivada da chave de nome e a instrumentação do aplicativo hello. 

eventos de saudação são gravados tooblob arquivos no formato JSON. Cada arquivo pode conter um ou mais eventos. Portanto, gostaríamos de dados de evento de saudação tooread e filtrar campos Olá que desejamos. Todos os tipos de coisas que podemos fazer com dados hello, mas nosso plano de hoje é toouse do Stream Analytics toopipe Olá dados tooPower BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Criar uma instância do Azure Stream Analytics
De saudação [Portal clássico do Azure](https://manage.windowsazure.com/), selecione o serviço do Azure Stream Analytics hello e criar um novo trabalho de análise de fluxo:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Quando o novo trabalho de saudação é criado, expanda os detalhes:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Definir local de blob
Defina-a entrada tootake do seu blob de exportação contínua:

![](./media/app-insights-export-stream-analytics/120.png)

Agora, você precisará Olá chave de acesso primário da conta de armazenamento, que você anotou anteriormente. Defina como Olá chave da conta de armazenamento.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Definir padrão de prefixo de caminho
![](./media/app-insights-export-stream-analytics/140.png)

**Ser se tooset Olá formato de data tooYYYY-MM-DD (com traços).**

saudação padrão de prefixo de caminho Especifica onde o Stream Analytics localiza os arquivos de entrada hello no armazenamento de saudação. Você precisa tooset-toohow toocorrespond exportação contínua armazena dados saudação. Defina-o assim:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

Neste exemplo:

* `webapplication27`é o nome de saudação de saudação recurso do Application Insights **todas as letras minúsculas**.
* `1234...`é a chave de instrumentação de saudação de saudação recurso do Application Insights, **omitindo traços**. 
* `PageViews`Olá tipo de dados que você deseja tooanalyze. tipos disponíveis de saudação dependem de filtro Olá definido na exportação contínua. Examinar outros tipos disponíveis de Olá Olá de toosee dados exportados e consulte Olá [exportar modelo de dados](app-insights-export-data-model.md).
* `/{date}/{time}` um padrão escrito literalmente.

> [!NOTE]
> Inspecione Olá armazenamento toomake-se de que obter o caminho de saudação à direita.
> 
> 

### <a name="finish-initial-setup"></a>Concluir a configuração inicial
Confirme o formato de serialização hello:

![Confirme e feche o assistente](./media/app-insights-export-stream-analytics/150.png)

Fechar o Assistente de saudação e aguarde Olá toocomplete de instalação.

> [!TIP]
> Use toodownload de comando de exemplo hello alguns dados. Mantê-lo como um toodebug de exemplo de teste de sua consulta.
> 
> 

## <a name="set-hello-output"></a>Saída de saudação do conjunto
Agora selecione o seu trabalho e definir a saída de hello.

![Selecione o novo canal de saudação, clique em saídas, adicionar, Power BI](./media/app-insights-export-stream-analytics/160.png)

Forneça seu **ou de estudante conta** tooauthorize tooaccess do Stream Analytics o recurso do Power BI. Em seguida, crie um nome para a saída de hello e de tabela e conjunto de dados do hello destino Power BI.

![Crie três nomes](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Consulta de saudação do conjunto
consulta Olá rege tradução de saudação do toooutput de entrada.

![Selecione hello e clique em consulta. Cole o exemplo hello abaixo.](./media/app-insights-export-stream-analytics/180.png)

Use Olá toocheck de função de teste que você receberá uma saída de saudação à direita. Dê a ele dados de exemplo hello que você fez na página de entradas de saudação. 

### <a name="query-toodisplay-counts-of-events"></a>Consulta toodisplay contagens de eventos
Cole esta consulta:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* entrada de exportação é alias Olá apresentamos a entrada de fluxo de toohello
* saída de pbi é Olá alias de saída foi definido
* Usamos [GetElements externa aplicar](https://msdn.microsoft.com/library/azure/dn706229.aspx) porque o nome do evento hello está em um arrray aninhada de JSON. Em seguida, escolhe selecione Olá Olá nome do evento, juntamente com uma contagem do número de saudação de instâncias com esse nome no período de tempo de saudação. Olá [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) cláusula agrupa elementos Olá em períodos de tempo de 1 minuto.

### <a name="query-toodisplay-metric-values"></a>Consulta toodisplay valores da métrica
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Essa consulta detalhada na hora do evento Olá métricas da telemetria tooget hello e valor de métrica de saudação. valores da métrica Olá estão dentro de uma matriz, para que possamos usar linhas de Olá Olá externa GetElements aplicar padrão tooextract. "myMetric" é o nome de saudação da métrica Olá nesse caso. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Consulta tooinclude valores de propriedades de dimensão
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* Essa consulta inclui valores de propriedades de dimensão Olá sem dependendo de uma dimensão específica que está sendo em um índice fixado na matriz de dimensão de saudação.

## <a name="run-hello-job"></a>Executar trabalho Olá
Você pode selecionar uma data no hello após toostart Olá trabalho do. 

![Selecione hello e clique em consulta. Cole o exemplo hello abaixo.](./media/app-insights-export-stream-analytics/190.png)

Aguarde até que o trabalho hello está sendo executado.

## <a name="see-results-in-power-bi"></a>Ver os resultados no Power BI
> [!WARNING]
> Há muito melhor e mais fácil [maneiras recomendadas dados do Application Insights toodisplay no Power BI](app-insights-export-power-bi.md). Olá, caminho ilustrado aqui é apenas um tooillustrate de exemplo como tooprocess de dados exportados.
> 
> 

Abra o Power BI com seu trabalho ou conta de estudante, Olá selecione conjunto de dados e tabela definida como saída de saudação do trabalho de análise de fluxo de saudação.

![No Power BI, selecione o conjunto de dados e os campos.](./media/app-insights-export-stream-analytics/200.png)

Agora você pode usar esse conjunto de dados em relatórios e painéis no [Power BI](https://powerbi.microsoft.com).

![No Power BI, selecione o conjunto de dados e os campos.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Não há dados?
* Verifique que você [formato de data do conjunto Olá](#set-path-prefix-pattern) corretamente tooYYYY-MM-DD (com traços).

## <a name="video"></a>Vídeo
Noam Ben Zeev mostra como tooprocess exportado usando a análise de fluxo de dados.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Exportação contínua](app-insights-export-telemetry.md)
* [Referência de tipos de propriedade hello e valores do modelo de dados detalhados.](app-insights-export-data-model.md)
* [Application Insights](app-insights-overview.md)

