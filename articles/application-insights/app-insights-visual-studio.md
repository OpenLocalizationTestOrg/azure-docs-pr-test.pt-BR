---
title: aaaDebug aplicativos com o Azure Application Insights no Visual Studio | Microsoft Docs
description: "Análise de desempenho do aplicativo Web e diagnóstico durante a depuração e na produção."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Depure seus aplicativos com o Azure Application Insights no Visual Studio
No Visual Studio (2015 e posterior), você pode analisar o desempenho e diagnosticar problemas em seu aplicativo Web ASP.NET na depuração e na produção usando a telemetria do [Application Insights do Azure](app-insights-overview.md).

Se você criou seu aplicativo web do ASP.NET usando o Visual Studio de 2017 ou posterior, ela já tem Olá SDK do Application Insights. Caso contrário, se você ainda não fez isso, [adicionar Application Insights tooyour aplicativo](app-insights-asp-net.md).

toomonitor seu aplicativo quando ele estiver em produção, você normalmente exibir telemetria do Application Insights Olá no hello [portal do Azure](https://portal.azure.com), onde você pode definir alertas e aplicar as avançadas ferramentas de monitoramentos. Mas, para depuração, você também pode pesquisar e analisar a telemetria Olá no Visual Studio. Você pode usar a telemetria do Visual Studio tooanalyze do seu site de produção e de depuração é executado no computador de desenvolvimento. Olá caso, você pode analisar execuções de depuração mesmo se você ainda não tiver configurado Olá SDK toosend telemetria toohello portal do Azure. 

## <a name="run"></a> Depurar seu projeto
Execute seu aplicativo Web no modo de depuração local usando F5. Abra páginas diferentes toogenerate alguns telemetria.

No Visual Studio, você vê uma contagem de eventos de saudação que foram registrados pelo módulo do Application Insights Olá em seu projeto.

![No Visual Studio, o botão do Application Insights Olá mostra durante a depuração.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

Clique neste botão toosearch sua telemetria. 

## <a name="application-insights-search"></a>Pesquisa do Application Insights
janela de pesquisa do Application Insights Olá mostra eventos que foram registrados. (Se você entrou tooAzure ao configurar o Application Insights, você pode pesquisar Olá eventos mesmo Olá portal do Azure.)

![Clique com botão direito hello e escolha o Application Insights, pesquisa](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> Depois que você marque ou desmarque os filtros, clique botão de pesquisa de Olá Olá final do campo de pesquisa de texto de saudação.
>

pesquisa de texto livre Olá funciona em todos os campos em eventos de saudação. Por exemplo, procurar por parte da URL de saudação de uma página. Olá valor ou de uma propriedade, como cidade do cliente; ou palavras específicas em um log de rastreamento.

Clique em qualquer evento toosee suas propriedades detalhadas.

Para solicitações tooyour web app, você pode clicar toohello código.

![Em detalhes da solicitação, clique em código toohello](./media/app-insights-visual-studio/31.png)

Você também pode abrir itens relacionados toohelp diagnosticar solicitações com falha ou exceções.

![Em detalhes da solicitação, role para baixo toorelated itens](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>Exibir exceções e solicitações com falha
Mostrar relatórios de exceção na janela de pesquisa de saudação. (Em alguns tipos mais antigos do aplicativo ASP.NET, você tem muito[configurar monitoramento de exceção](app-insights-asp-net-exceptions.md) toosee exceções que são manipuladas pelo framework hello.)

Clique em uma exceção tooget um rastreamento de pilha. Se o código de saudação do aplicativo hello é aberto no Visual Studio, você pode clicar Olá pilha rastreamento toohello relevantes linha do código de saudação.

![Rastreamento de pilha de exceção](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Exibir resumos de solicitação e a exceção no código Olá
Olá linha Lente de código acima cada método de manipulador, você verá uma contagem de solicitações de saudação e exceções conectadas pelo Application Insights Olá últimas 24 horas.

![Rastreamento de pilha de exceção](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> Lente de código mostra apenas os dados do Application Insights, se você tiver [configurado seu portal do Application Insights do aplicativo toosend telemetria toohello](app-insights-asp-net.md).
>

[Saiba mais sobre o Application Insights no CodeLens](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>Tendências
Tendências é uma ferramenta para visualizar como o seu aplicativo se comporta ao longo do tempo. 

Escolha **explorar tendências de telemetria** do botão de barra de ferramentas do Application Insights hello ou janela de pesquisa do Application Insights. Escolha um dos cinco tooget de consultas comuns iniciado. Você pode analisar conjuntos de dados diferentes com base em tipos de telemetria, intervalos de tempo e outras propriedades. 

toofind anomalias em seus dados, escolha uma das opções de anomalias de saudação no menu suspenso de "Tipo de exibição" hello. Opções de filtragem de saudação na parte inferior da saudação da janela Olá tornam fácil toohone em subconjuntos específicos de sua telemetria.

![Tendências](./media/app-insights-visual-studio/51.png)

[Mais sobre tendências](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>Monitoramento local
(A partir do Visual Studio 2015 atualização 2) Se você ainda não configurou o portal do Application Insights toohello de telemetria do hello SDK toosend (de forma que não há nenhuma chave de instrumentação no applicationinsights. config), em seguida, janela de diagnóstico Olá exibe Telemetria da sessão de depuração mais recente. 

Isso será desejável se você já tiver publicado uma versão anterior do seu aplicativo. Você não quer a telemetria de saudação do seu toobe de sessões de depuração misturados com a telemetria em Olá Olá portal do Application Insights do aplicativo publicado hello.

Também é útil se você tiver algumas [telemetria personalizada](app-insights-api-custom-events-metrics.md) que você deseja toodebug antes de enviar o portal de toohello de telemetria.

* *Primeiro, configurei totalmente portal do Application Insights toosend telemetria toohello. Mas agora gostaria de telemetria de saudação toosee apenas no Visual Studio.*
  
  * Em configurações da janela de pesquisa hello, há um diagnóstico de local de toosearch opção mesmo se seu aplicativo envia o portal de toohello de telemetria.
  * Telemetria toostop enviada toohello portal, comente a linha hello `<instrumentationkey>...` de applicationinsights. config. Quando estiver pronto toosend portal de toohello de telemetria, remova-os.


## <a name="next-steps"></a>Próximas etapas
|  |  |
| --- | --- |
| **[Adicionar mais dados](app-insights-asp-net-more.md)**<br/>Monitorar o uso, a disponibilidade, as dependências e as exceções. Integrar rastreamentos de estruturas de logs. Escrever telemetria personalizada. |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| **[Trabalhando com o portal do Application Insights Olá](app-insights-dashboards.md)**<br/>Exiba painéis, poderosas ferramentas de diagnóstico e análise, alertas, um mapa de dependências em tempo real de seu aplicativo e os dados telemétricos exportados. |![Visual Studio](./media/app-insights-visual-studio/62.png) |

