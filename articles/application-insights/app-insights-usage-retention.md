---
title: "análise de retenção aaaUser para aplicativos web com o Azure Application Insights | Documentos da Microsoft"
description: "Quantos usuários retornarem tooyour aplicativo?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Análise de retenção de usuários para aplicativos Web com o Application Insights

recurso de retenção de saudação do [Azure Application Insights](app-insights-overview.md) ajuda a analisar quantos usuários retorna tooyour aplicativo e frequência executar determinadas tarefas ou atingir as metas. Por exemplo, se você executar um site de jogos, você poderá comparar números de saudação de usuários que retornam toohello site depois de perder um jogo com número de saudação que retornam após o vencedor. Esse conhecimento pode ajudar a melhorar a experiência do usuário e sua estratégia de negócios.

## <a name="get-started"></a>Introdução

Se você ainda não vir dados na ferramenta de retenção Olá no portal do Application Insights hello, [Saiba como tooget iniciada com ferramentas de uso de saudação](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>ferramenta de retenção Olá

![Ferramenta de retenção](./media/app-insights-usage-retention/retention.png)

1. barra de ferramentas Olá permite que os usuários toocreate novos relatórios de retenção, abra relatórios existentes de retenção, salvar o relatório de retenção atual ou salvar como, reverter as alterações feitas toosaved relatórios, atualizar dados no relatório hello, relatório de compartilhamento via email ou link direto e saudação de acesso página de documentação. 
2. Por padrão, a retenção mostra todos os usuários que fizeram algo e então voltaram e fizeram outra coisa em um período. Você pode selecionar diferentes combinações de eventos toonarrow Olá enfocam atividades específicas do usuário.
3. Adicione um ou mais filtros para as propriedades. Por exemplo, você pode se concentrar em usuários de um determinado país ou região. Clique em **atualização** depois de definir filtros de saudação. 
4. Olá geral retenção gráfico mostra um resumo de retenção de usuário em Olá período de tempo selecionado. 
5. grade de Olá mostra o número Olá de usuários retidos acordo construtor de consultas toohello # 2. Cada linha representa um cohort de usuários que realizou a qualquer evento no tempo de saudação período mostrado. Cada célula na linha de saudação mostra quantas que cohort retornadas pelo menos uma vez em um período mais recente. Alguns usuários podem retornar em mais de um período. 
6. cartões de insights Olá mostram eventos iniciante cinco principais e cinco principais retornados os usuários de toogive eventos melhor compreensão de seus relatórios de retenção. 

![Foco de mouse de retenção](./media/app-insights-usage-retention/hover.png)

Os usuários podem focalize células no botão de análise de Olá Olá retenção ferramenta tooaccess e dicas de ferramenta explicando célula Olá significa. botão de análise de Olá leva a ferramenta de análise de toohello usuários com usuários de toogenerate uma consulta preenchida previamente da célula de saudação. 

## <a name="use-business-events-tootrack-retention"></a>Use a retenção de tootrack de eventos de negócios

tooget hello mais úteis retenção análise, eventos de medidas que representam as atividades de negócios significativa. 

Por exemplo, muitos usuários podem abrir uma página em seu aplicativo sem jogo Olá exibido. Apenas as exibições de página Olá de controle, portanto, podem fornecer uma estimativa precisa de quantas pessoas retornam tooplay jogo Olá após ele anteriormente. tooget uma visão clara de retorno de players, o aplicativo deve enviar um evento personalizado quando um usuário é reproduzido.  

É uma boa prática toocode eventos personalizados que representam as ações de negócios e usá-los para sua análise de retenção. resultado de jogos do toocapture Olá, é necessário toowrite uma linha de código toosend tooApplication um evento personalizado Insights. Se você escrever em código de página da web hello ou Node. js, ele é semelhante a:

```JavaScript
    appinsights.trackEvent("won game");
```

Ou no código de servidor do ASP.NET:

```C#
   telemetry.TrackEvent("won game");
```

[Saiba mais sobre como escrever eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Próximas etapas
- uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.
    - [Usuários, Sessões, Eventos](app-insights-usage-segmentation.md)
    - [Funis](usage-funnels.md)
    - [Fluxos de Usuário](app-insights-usage-flows.md)
    - [Pastas de trabalho](app-insights-usage-workbooks.md)
    - [Adicionar contexto de usuário](app-insights-usage-send-user-context.md)


