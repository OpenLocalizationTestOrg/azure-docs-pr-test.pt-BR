---
title: "aaaExploring métricas no Azure Application Insights | Microsoft Docs"
description: "Como toointerpret gráficos no explorer métrica e folhas de métrica explorer toocustomize."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Explorar métricas no Application Insights
Métricas no [Application Insights][start] são contagens e valores medidos de eventos enviados em telemetria do seu aplicativo. Eles ajudam você a detectar problemas de desempenho e observar as tendências referentes a como seu aplicativo está sendo usado. Há uma grande variedade de métricas padrão, e você também pode criar suas próprias métricas e eventos personalizados.

Contagens de métricas e eventos são exibidas em gráficos de valores agregados como somas, médias ou contagens.

Aqui está um exemplo de conjunto de gráficos:

![](./media/app-insights-metrics-explorer/01-overview.png)

Você pode encontrar gráficos de métricas em qualquer lugar no portal do Application Insights hello. Na maioria dos casos, eles podem ser personalizados, e você pode adicionar mais folha toohello de gráficos. Na folha de visão geral de saudação, clique nas toomore detalhadas gráficos (que têm cargos como "Servidores"), ou clique em **Metrics Explorer** tooopen uma nova folha de onde você pode criar gráficos personalizados.

## <a name="time-range"></a>Intervalo de tempo
Você pode alterar Olá intervalo de tempo coberto por gráficos hello ou grades em qualquer folha.

![Folha de visão geral de saudação aberto de seu aplicativo no portal do Azure de saudação](./media/app-insights-metrics-explorer/03-range.png)

Se você estiver esperando dados que não apareceram ainda, clique em Atualizar. Gráficos de atualizar a mesmos em intervalos, mas intervalos de saudação são mais tempo para intervalos de tempo maior. Pode levar algum tempo para dados toocome por meio do pipeline de análise de saudação em um gráfico.

toozoom em parte de um gráfico, arraste sobre ele:

![Arraste por parte de um gráfico.](./media/app-insights-metrics-explorer/12-drag.png)

Clique em Olá Desfazer Zoom botão toorestore-lo.

## <a name="granularity-and-point-values"></a>Valores de granularidade e ponto
Passe o mouse sobre Olá gráfico toodisplay Olá valores hello métricas nesse ponto.

![Passe o mouse sobre um gráfico Olá](./media/app-insights-metrics-explorer/02-focus.png)

valor de saudação da métrica de saudação em um ponto específico é agregado no decorrer de saudação precede o intervalo de amostragem.

intervalo de amostragem de saudação ou "granularidade" é mostrada na parte superior de saudação da folha de saudação.

![cabeçalho de saudação de uma folha.](./media/app-insights-metrics-explorer/11-grain.png)

Você pode ajustar a granularidade de saudação na folha de intervalo de tempo de saudação:

![cabeçalho de saudação de uma folha.](./media/app-insights-metrics-explorer/grain.png)

granularidades de saudação disponíveis dependem do intervalo de tempo de saudação que você selecionar. granularidades explícita Olá são granularidade "automática" do toohello alternativas para o intervalo de tempo de saudação.


## <a name="editing-charts-and-grids"></a>Edição de gráficos e grades
tooadd uma nova folha de toohello do gráfico:

![No Metrics Explorer, escolher Adicionar Gráfico](./media/app-insights-metrics-explorer/04-add.png)

Selecione **editar** em um tooedit novo ou existente do gráfico que mostra:

![Selecionar uma ou mais métricas](./media/app-insights-metrics-explorer/08-select.png)

Você pode exibir mais de uma métrica em um gráfico, que não existem restrições sobre combinações de saudação que podem ser exibidas juntos. Assim que você escolha uma métrica, alguns Olá que outras pessoas estão desabilitadas.

Se você codificou [métricas personalizadas] [ track] em seu aplicativo (chamadas tooTrackMetric e TrackEvent) serão listados aqui.

## <a name="segment-your-data"></a>Segmentar os dados
Você pode dividir uma métrica pela propriedade - por exemplo, as exibições de página toocompare em clientes com sistemas operacionais diferentes.

Selecionar um gráfico ou grade, ative o agrupamento e selecionar toogroup uma propriedade por:

![Selecionar Agrupamento Ativo, então selecionar uma propriedade em Agrupar Por](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Quando você usa o agrupamento, tipos de gráfico de barras e de área de saudação fornecem uma exibição de empilhadas. Isso é adequado em que o método de agregação hello é Sum. Mas, em que o tipo de agregação Olá média, escolha tipos de exibição de grade ou de linha de saudação.
>
>

Se você codificou [métricas personalizadas] [ track] em seu aplicativo e elas incluem os valores de propriedade, você será capaz de tooselect propriedade de Olá na lista de saudação.

Gráfico de saudação é muito pequeno para dados segmentados? Ajuste sua altura:

![Ajuste o controle deslizante de saudação](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Tipos de agregação
legenda Olá no lado de saudação por padrão geralmente mostra o valor de saudação agregada por período de saudação do gráfico de saudação. Se você passar o mouse sobre o gráfico de hello, ele mostra o valor de saudação nesse ponto.

Cada ponto de dados no gráfico de saudação é uma agregação de valores de dados Olá recebida no hello anterior "granularidade" ou o intervalo de amostragem. granularidade de saudação é exibida na parte superior de saudação da folha de saudação e varia de acordo com hello geral escala de tempo do gráfico de saudação.

Métricas podem ser agregadas de maneiras diferentes:

* **Contagem de** é uma contagem de eventos de saudação recebidos no intervalo de amostragem de saudação. Ela é usada para eventos como solicitações. Variações de altura de saudação do gráfico de saudação indica variações na taxa de saudação ocorrem eventos de saudação. Mas observe que o valor numérico Olá muda quando você alterar o intervalo de amostragem de saudação.
* **Soma** adiciona valores de saudação de todos os pontos de dados Olá recebidos no período de saudação do gráfico hello, ou intervalo de amostragem de saudação.
* **Médio** divide Olá soma pelo número de saudação de pontos de dados recebidos por intervalo de saudação.
* **Únicas** são usadas para contagens de usuários e contas. Durante o intervalo de amostragem de hello, ou em período de saudação do gráfico de saudação, Figura Olá mostra contagem de saudação de diferentes usuários vistos no momento.
* **%** – versões de percentual de cada agregação são usadas somente com gráficos segmentados. Olá total sempre adiciona o too100% e gráfico Olá mostra a contribuição relativa Olá dos diferentes componentes de um total.

    ![Agregação de percentual](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Alterar o tipo de agregação Olá

![Editar gráfico hello e, em seguida, selecione a agregação](./media/app-insights-metrics-explorer/05-aggregation.png)

método padrão de saudação para cada métrica é mostrado quando você cria um novo gráfico ou quando todas as métricas serão desmarcadas:

![Cancele a seleção de todos os padrões de saudação toosee de métricas](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Eixo Y do PIN 
Por padrão, um gráfico mostra valores do eixo Y a partir do zero até valores máximo no intervalo de dados hello, toogive uma representação visual de quantum de valores hello. Mas em alguns casos mais de quantum Olá talvez seja interessante toovisually inspecionar pequenas alterações em valores. Para personalizações, como esse uso Olá intervalo edição recurso toopin Olá eixo y mínimo ou máximo valor do eixo y no local desejado.
Clique em "Configurações avançadas" caixa de seleção toobring backup Olá configurações de intervalo de eixo y

![Clique em Configurações Avançadas, selecione Intervalo personalizado e especifique os valores mín. e máx.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filtrar seus dados
métricas de saudação apenas toosee para um conjunto de valores de propriedade selecionado:

![Clicar em Filtro, expandir uma propriedade e verificar alguns valores](./media/app-insights-metrics-explorer/19-filter.png)

Se você não selecionar valores para uma determinada propriedade, ele tem Olá mesmo como selecionar todos eles: não há nenhum filtro nessa propriedade.

Saudação de aviso contagens de eventos ao lado de cada valor de propriedade. Quando você seleciona valores de uma propriedade, Olá conta junto com outros valores são ajustados de propriedade.

Os filtros se aplicam a gráficos de saudação tooall em uma folha. Se você quiser diferentes filtros aplicados toodifferent gráficos, criar e salvar folhas diferentes métricas. Se desejar, você pode fixar gráficos do painel de toohello folhas diferentes, para que você pode vê-los lado a lado.

### <a name="remove-bot-and-web-test-traffic"></a>Remover o tráfego de testes da Web e de bot
Usar o filtro de saudação **tráfego Real ou sintético** e verificar **Real**.

Você também pode filtrar por **Origem do tráfego sintético**.

### <a name="tooadd-properties-toohello-filter-list"></a>lista de filtros de toohello tooadd propriedades
Você gostaria que toofilter telemetria em uma categoria de sua escolha? Por exemplo, talvez você divida seus usuários em categorias diferentes e queira segmentar os dados segundo essas categorias.

[Crie sua própria propriedade](app-insights-api-custom-events-metrics.md#properties). Defina-o um [telemetria inicializador](app-insights-api-custom-events-metrics.md#defaults) toohave aparecem em toda a telemetria - incluindo telemetria padrão Olá enviadas por diferentes módulos do SDK.

## <a name="edit-hello-chart-type"></a>Editar o tipo de gráfico de saudação
Observe que você pode alternar entre gráficos e grades:

![Selecionar uma grade ou um gráfico e escolher um tipo de gráfico](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Salve sua folha de métricas
Quando você tiver criado alguns gráficos, salve-os como favoritos. Você pode escolher se tooshare-lo com outros membros da equipe, se você usar uma conta organizacional.

![Escolher Favorito](./media/app-insights-metrics-explorer/21-favorite-save.png)

novamente, folha de saudação toosee **folha de visão geral de toohello vá** e abrir favoritos:

![Na folha de visão geral de saudação, escolha Favoritos](./media/app-insights-metrics-explorer/22-favorite-get.png)

Se você escolher o intervalo de tempo relativo quando você salva, folha Olá será atualizada com as métricas mais recentes de saudação. Se você escolher o intervalo de tempo absoluto, ele mostrará Olá mesmos dados toda vez.

## <a name="reset-hello-blade"></a>Redefinição Olá folha
Se você editar uma folha, mas, em seguida, você gostaria que o conjunto de backup toohello original salvada tooget, clique em Redefinir.

![Nos botões de saudação na parte superior de saudação do Explorer de métrica](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Live Metrics Stream

Para obter uma exibição imediata da sua telemetria, abra [Live Stream](app-insights-live-stream.md). A maioria das métricas usem tooappear de alguns minutos, devido ao processo de saudação de agregação. Por outro lado, as métricas em tempo real são otimizadas para baixa latência. 

## <a name="set-alerts"></a>Definir alertas
toobe notificado por email sobre valores incomuns de alguma das métricas, adicionar um alerta. Você pode escolher os administradores de contas toohello de email Olá toosend ou toospecific endereços de email.

![No Metrics Explorer, escolher Regras de Alerta, Adicionar Alerta](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[Saiba mais sobre alertas][alerts].


## <a name="continuous-export"></a>Exportação Contínua
Se desejar que os dados sejam exportados de forma contínua para que você possa processá-los externamente, considere usar a [Exportação contínua](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Se você quiser ainda melhores exibições dos dados, você pode [exportar tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Análise
[Análise de](app-insights-analytics.md) é um tooanalyze de maneira mais versátil sua telemetria usando uma linguagem de consulta avançada. Usá-lo se você deseja toocombine resultados de métricas de computação ou executar uma análise detalhada do desempenho recentes do aplicativo. 

Um gráfico de métrica, você pode clicar em Olá análise ícone tooget diretamente toohello equivalente consulta analítica.

## <a name="troubleshooting"></a>Solucionar problemas
*Não vejo dados no gráfico.*

* Os filtros se aplicam a gráficos de saudação tooall na folha de saudação. Certifique-se de que, enquanto você estiver concentrado em um gráfico, você não definiu um filtro que exclui todos os dados de saudação em outro.

    Se você quiser tooset filtros diferentes gráficos diferentes, criá-los em diferentes folhas, salvá-los como algo separados Favoritos. Se desejar, você pode fixá-los toohello painel para que você pode vê-los lado a lado.
* Se um gráfico são agrupados por uma propriedade que não está definida na métrica hello, haverá nada no gráfico de saudação. Tente limpar “agrupar por” ou escolha uma propriedade de agrupamento diferente.
* Haverá dados de desempenho (CPU, taxa de E/S, etc.) disponíveis para serviços Web Java, aplicativos da área de trabalho do Windows, [aplicativos Web e serviços do IIS se você instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md) e os [Serviços de Nuvem do Azure](app-insights-azure.md). Esses dados não estão disponíveis para sites do Azure.

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Próximas etapas
* [Monitorando o uso com o Application Insights](app-insights-web-track-usage.md)
* [Usando a Pesquisa de diagnóstico](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
